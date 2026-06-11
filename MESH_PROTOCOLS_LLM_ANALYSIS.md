# Rapport: Protocoles Mesh + LLM/Agent — Analyse Approfondie

**Date:** 11 Juin 2026  
**Sources:** MeshCore-official (merlin-chen), meshtastic-firmware, trail-mate, Meck-P4-main,  
autogen, open-interpreter, RWKV.cpp, snntorch, norse, gat45/p4

---

## PARTIE 1: PROTOCOLES MESH — ARCHITECTURE

### 1.1 MeshCore — Analyse Complète du Protocole

#### Identité & Crypto

| Propriété | Valeur |
|-----------|--------|
| **Identity** | Ed25519 keypair (32B pub + 64B priv) |
| **Key exchange** | X25519 ECDH (via `ed25519_key_exchange`) |
| **Chiffrement payload** | AES-128-ECB + HMAC-SHA256 (MAC 2B tronqué) |
| **Chiffrement groupe** | Clé 16B PSK (SHA256 du nom pour canal public) |
| **Signature** | Ed25519 (advert, identities) |
| **Aléatoire** | Pas de nonce — ECB déterministe (même clair + même clé = même chiffré) |
| **Intégrité** | Oui — HMAC-SHA256 tronqué à 2B (couvre le ciphertext) |

**⚠️ Faiblesse crypto:** AES-128-ECB sans nonce = vulnérable à l'analyse statistique. Mais en pratique, les paquets sont courts (max 184B payload, 12 blocs AES) et changeants. Le HMAC 2B est court (1/65536 faux positif).

#### Format de Trame (Packet)

```
[0]       header (1B): [1:0]=route_type, [5:2]=payload_type, [7:6]=payload_version
[1..4]    transport_codes (4B, optionnel si TRANSPORT_FLOOD/DIRECT)
[n]       path_len (1B): [1:0]=hash_size-1, [7:2]=hash_count
[n+1..]   path[] (hash_count × hash_size octets)
          payload[] (jusqu'à MAX_PACKET_PAYLOAD = 184B)
```

**Route types:** FLOOD (0x01), DIRECT (0x02), TRANSPORT_FLOOD (0x00), TRANSPORT_DIRECT (0x03)  
**Payload types:** REQ, RESPONSE, TXT_MSG, ACK, ADVERT, GRP_TXT, GRP_DATA, ANON_REQ, PATH, TRACE, MULTIPART, CONTROL, RAW_CUSTOM

#### Routage

- **Primaire:** Flood routing — chaque noeud ajoute son hash au path et retransmet avec délai aléatoire
- **Secondaire:** Direct routing (source-routed) — chemin pré-établi, priority 0
- **Dedup:** SHA256(payload) tronqué à 8B, buffer circulaire de 160 entrées
- **Path max:** 64B (jusqu'à ~63 noeuds)
- **Transport codes:** 4B pour zoning régional (ex: "au-nsw")

#### Paramètres Radio (Meck-P4 "Australia Narrow")

| Paramètre | Valeur |
|-----------|--------|
| Fréquence | 916.575 MHz |
| Bandwidth | 62.5 kHz |
| Spreading Factor | 7 |
| Coding Rate | 4/8 |
| TX Power | 22 dBm |
| Sync Word | **0x1424** (2B) |
| Preamble | 32 symboles |
| MTU | 255B |
| Payload max | 184B |

#### Couche Radio

- **SPI polling** exclusif — pas de DIO1 (XL9535 jugé non fiable)
- `checkRecv()` lit le registre IRQ directement via SPI (`get_irq_flag()`)
- `loop()` tick à 10ms (dans `meck_task` priority 3)
- Pas de CSMA/CA, pas de CAD — envoi dès que le canal semble libre

#### Voice over LoRa (Meck-Voice / Codec2)

| Propriété | Valeur |
|-----------|--------|
| Codec | Codec2 1200bps |
| Frame audio | 40ms → 6B encodé |
| Échantillonnage | 44100 Hz → downsample 8000 Hz |
| Paquet LoRa | 150B de payload voix + 6B header (magic 0x56 + sessionID + index) |
| Session max | 12 secondes (~300 frames × 6B = 1800B = 12 paquets) |
| Type MeshCore | RAW_CUSTOM (0x0F) — pas de crypto |

---

### 1.2 Meshtastic — Analyse Complète du Protocole

#### Identité & Crypto

| Propriété | Valeur |
|-----------|--------|
| **Identity** | X25519 keypair (32B pub) |
| **Key exchange** | X25519 ECDH → AES-256-CCM (PKI messages) |
| **Chiffrement canal** | AES-128-CTR ou AES-256-CTR (stream cipher, PAS d'authentification) |
| **Intégrité canal** | **AUCUNE** — CTR est malléable |
| **Intégrité PKI** | Oui — CCM 8B MAC |

**⚠️ Faiblesse crypto canal:** AES-CTR sans MAC = corruption/modification silencieuse possible. Les paquets canal peuvent être altérés sans détection. Le PKI est plus sûr (CCM avec MAC).

#### Format de Trame (Packet)

```
Header 16B: [from:4][to:4][id:4][flags:1][channel:1][padding:2]
Payload: jusqu'à 237-239B
```

Le payload est protobuf-encodé (type, canal, données) — contrairement à MeshCore qui est binaire fixe.

#### Routage

- **Primaire:** FloodingRouter — inondation avec history
- **Secondaire:** NextHopRouter — apprentissage du prochain saut
- **ACK:** ReliableRouter — ACK + retry (jusqu'à HOP_MAX=7)
- **Dedup:** PacketHistory (packet IDs 32-bit avec timeout)
- **CSMA/CA:** CAD (Channel Activity Detection) avec fenêtre de contention aléatoire (3-8 slots)

#### Paramètres Radio (LongFast)

| Paramètre | Valeur |
|-----------|--------|
| Fréquence | DJB2 hash du nom de canal (ex: 906.875 MHz pour "LongFast") |
| Bandwidth | 250 kHz |
| Spreading Factor | 11 |
| Coding Rate | 4/5 |
| TX Power | 20 dBm (max) |
| Sync Word | **0x2B** (1B) |
| Preamble | 16 symboles |
| MTU | 255B |
| Payload max | 237B |

#### Couche Radio

- **Interrupt-driven** — DIO1 = RX_DONE/TX_DONE IRQ
- CSMA/CA avec CAD — écoute avant de parler
- RX duty cycling — mode sleep entre fenêtres RX
- Double buffering DMA (SX126x)

#### Fonctionnalités Avancées

- **MQTT Gateway** — protocole complet `msh/{channelId}/{gatewayId}`
- **Over-IP** — UDP multicast 224.0.0.69:4403, TCP API port 4403
- **NodeDB** — découverte automatique, position, télémetrie
- **Deep sleep** — CPU off, RTC wake, LoRa DIO1 réveil
- **Max nodes:** 100 (ESP32), 250 (ESP32-S3)

---

### 1.3 Comparaison Directe: MeshCore vs Meshtastic

| Aspect | MeshCore | Meshtastic |
|--------|----------|------------|
| **Sync Word** | 0x1424 (2B) | 0x2B (1B) |
| **Identity** | Ed25519 (signature + DH) | X25519 (DH only) |
| **Chiffrement canal** | AES-128-ECB + HMAC-SHA256 ✅ | AES-128/256-CTR (no auth) ❌ |
| **Chiffrement DM** | AES-128-ECB + HMAC (même schéma) | AES-256-CCM (authentifié) ✅ |
| **Intégrité** | HMAC 2B (court mais présent) | Canal: aucune. PKI: CCM 8B |
| **Format trame** | Binaire fixe 1B header | Binaire 16B header + protobuf |
| **Routage** | Flood + Direct (path) | Flood + NextHop + Reliable |
| **CSMA/CA** | NON (envoi direct) | OUI (CAD + contention) |
| **RX mode** | Polling SPI (10ms tick) | Interrupt-driven (DIO1) |
| **Payload max** | 184B | 237B |
| **Hop limit** | Implicite (path max 64B) | Explicite (HOP_MAX=7) |
| **MQTT/IP** | NON (radio only) | OUI (MQTT + UDP + TCP) |
| **Deep sleep** | NON (délégation plateforme) | OUI (built-in) |
| **Voice** | Codec2 1200bps (Meck-Voice) | NON |
| **Nodes max** | Pas de limite explicite | 100-250 |
| **Communauté** | Petite (~10 devs) | Très large (~1000+ devs) |

---

## PARTIE 2: COEXISTENCE SUR T-DISPLAY P4

### 2.1 Contrainte Matérielle — UN SEUL SX1262

Le T-Display P4 a **un seul module LoRa** (SX1262 ou SX1276 selon variante).  
Connecteurs: **MMCX1** = SX1262 (868/915MHz), **MMCX2** = réservé 2.4GHz (pas encore sorti).

Les deux protocoles ne peuvent PAS tourner simultanément sur la même radio.

### 2.2 Possibilités de Coexistence

#### Option A: Dual Partition Firmware (approche Meck-P4)

Changer de firmware entre MeshCore et Meshtastic via double partition OTA.

- **Avantages:** Simplicité, optimisation hardware par protocole
- **Inconvénients:** Reboot nécessaire, pas de commutation runtime
- **Qui le fait:** Meck-P4 (n'a que MeshCore), pas de dual partition encore

#### Option B: Protocol Switching Runtime (approche trail-mate)

Reconfigurer la radio à chaud pour basculer entre protocoles.

```
1. Stop radio RX
2. Changer params (sync word, freq, BW, SF, CR)
3. Clear buffer + IRQ flags
4. Re-enter RX mode avec nouveau sync word
```

**Temps de reconfiguration SX1262:** ~10-15ms (setPacketParams + setModulationParams + setSyncWord + setRx)

**Validé par trail-mate:** trail-mate implémente `MeshCoreAdapter` et `MeshtasticAdapter` qui partagent la même radio physique en alternance.

**Défis:**
- Pendant le switch (~15ms), aucun paquet n'est reçu
- Si un paquet MeshCore arrive pendant une fenêtre Meshtastic → perdu (mauvais sync word → pas d'IRQ)
- Perte de paquets proportionnelle au ratio de temps alloué
- Les ACK Meshtastic (timeout 5-30s) peuvent expirer

#### Option C: Time-Slicing (Round Robin)

Allouer des fenêtres temporelles fixes: 30s MeshCore, 30s Meshtastic.

| Fenêtre | Protocole | Sync Word | SF/BW |
|---------|-----------|-----------|-------|
| T0-30s | MeshCore | 0x1424 | SF7/BW62.5 |
| T30-60s | Meshtastic | 0x2B | SF11/BW250 |
| T60-90s | MeshCore | 0x1424 | SF7/BW62.5 |
| ... | ... | ... | ... |

**Problème:** SF7 vs SF11 sont orthogonaux — mais les fréquences peuvent différer. Si les fréquences sont proches, l'émetteur Meshtastic peut saturer le récepteur MeshCore (jamais assez proche pour créer de l'interférence de blocage, car les bandes sont partagées).

#### Option D: Dual Radio (Futur)

Si MMCX2 devient disponible pour 2.4GHz LoRa (ou module séparé):
- SX1262 (868/915MHz) → MeshCore (LoRa classique)
- Module 2.4GHz → Meshtastic (ou autre)

**2.4GHz LoRa n'existe pas encore commercialement** (SX1280 = 2.4GHz mais incompatible avec le protocole LoRaWAN classique). Certains développements Meshtastic expérimentaux sur SX1280 existent mais pas en production.

### 2.3 Analyse: Compatibilité Radio

La question clé: **Peuvent-ils partager la même fréquence ?**

| Scenario | Fonctionne ? | Raison |
|----------|-------------|--------|
| Même freq, SF différent | **Oui** | Les SF sont orthogonaux (CDMA-like). SF7 n'entend pas SF11 |
| Même freq, même SF, sync word différent | **Oui** | Sync word = filtre hardware SX1262. Paquet rejeté au niveau radio |
| Même freq, même SF, même sync word | **Interférence** | Collision pure. CSMA/CA de Meshtastic vs pas de CSMA MeshCore |
| Freq différente > 1MHz | **Oui** | Filtrage bande passante — pas d'interférence |

**Conclusion:** MeshCore (916.575 MHz, SF7, 0x1424) et Meshtastic (906.875 MHz, SF11, 0x2B) sont **totalement orthogonaux** sur tous les plans: fréquence, SF, sync word. Ils peuvent coexister sur la même radio **en alternance temporelle** sans perte due aux interférences.

### 2.4 Référence: trail-mate Implementation

trail-mate (`C:\Users\videl\Desktop\lyligo\trail-mate`) est le SEUL projet qui implémente les deux protocoles:

```
modules/
  core_chat/
    src/infra/
      meshcore/   → MeshCore protocol helpers, crypto, region presets
      meshtastic/ → Meshtastic protocol helpers (MT radio config)
      radio/      → Radio abstraction (SX1262 packet IO)
  core_mesh/
    src/protocol/
      meshcore/   → MeshCore identity flow, packet codec, receive flow
      meshtastic/ → Meshtastic adapter
```

**Architecture trail-mate:**
- `SX1262RadioPacketIo` → couche radio bas niveau (SPI polling)
- `MeshCoreAdapter` / `MeshtasticAdapter` → implémentent une interface `RadioProtocol` commune
- `ChatProtocolStack` → dispatche entre les deux protocoles
- Le switch de protocole reconfigure: `setSyncWord()`, `setFrequency()`, `setModulationParams()`, `setBandwidth()`

**Leçons de trail-mate pour JARVIX-OS:**
- L'architecture à adaptateurs séparés est la bonne
- Le temps de reconfiguration SX1262 est acceptable (~15ms)
- Le défi principal est le **buffer management** (paquets reçus pendant le switch)
- trail-mate ne fait PAS de time-slicing — il choisit un protocole au démarrage et reste dessus

---

## PARTIE 3: STACK LLM/AGENT POUR ORANGE PI

### 3.1 Architecture Proposée

```
┌─────────────────────────────────────────────────────┐
│                   ORANGE PI (RK3588)                 │
│                                                      │
│  ┌──────────┐   ┌──────────────┐   ┌─────────────┐  │
│  │ RWKV.cpp  │   │   autogen    │   │open-interpr.│  │
│  │ Inférence │◄──┤ Orchestrateur│──►│ Exécution   │  │
│  │  LLM      │   │  multi-agent │   │  commandes  │  │
│  └──────────┘   └──────────────┘   └─────────────┘  │
│       │                │                  │          │
│       ▼                ▼                  ▼          │
│  ┌─────────────────────────────────────────────────┐ │
│  │           LiveKit Server / AI Agent              │ │
│  │  Opus ↔ WebRTC ↔ RPC ↔ DataStream               │ │
│  └──────────────────────┬──────────────────────────┘ │
└─────────────────────────┼────────────────────────────┘
                          │ UDP Opus 16-32kbps
                          ▼
┌─────────────────────────────────────────────────────┐
│                  ESP32-C6 (WiFi Modem)                │
│  UDP proxy 80-150ms jitter buffer                    │
└──────────────────────┬──────────────────────────────┘
                          │ SDIO 2048B frames
                          ▼
┌─────────────────────────────────────────────────────┐
│                  ESP32-P4 (Audio Core)                │
│  LiveKit SDK + esp-sr AFE + I2S ES8311               │
│  + SX1262 (MeshCore ou Meshtastic)                    │
└─────────────────────────────────────────────────────┘
```

### 3.2 RWKV.cpp pour l'Inférence LLM

| Propriété | Valeur |
|-----------|--------|
| **Repo** | `github.com/RWKV/rwkv.cpp` |
| **Language** | C++17 |
| **Format modèle** | GGML/GGUF |
| **Architecture** | RWKV-6, RWKV-7 "Goose" |
| **CPU** | ARM64 (RK3588), x86_64 |
| **RAM** | ~2-8GB selon taille modèle |
| **Performance RK3588** | ~15-30 tok/s (RWKV-7 1.5B quant Q4) |
| **ESP32** | ❌ PAS supporté (ARM64/x86 only) |

**Avantage clé:** Pas de KV-cache — mémoire constante (O(1)) quelle que soit la longueur du contexte. Idéal pour les systèmes à mémoire fixe.

**Désavantage:** Modèles plus petits disponibles (max ~14B paramètres). RWKV-7 "Goose" (14B) est le plus gros à date.

**Usage dans JARVIX-OS:**
- Modèle de chat (~1.5B-3B) pour la conversation vocale
- Contexte fenêtré (derniers N tours de dialogue)
- Prompt engineering pour le contrôle des outils (RPC, DataStream)

### 3.3 autogen pour l'Orchestration Multi-Agents

| Propriété | Valeur |
|-----------|--------|
| **Repo** | `github.com/microsoft/autogen` |
| **Language** | Python |
| **Version** | 0.4+ (core API) |
| **Architecture** | Agents asynchrones avec files de messages |

**Architecture d'agents proposée pour JARVIX-OS:**

```
┌──────────────┐
│ Agent Audio  │─── RPC → P4: play_tts(), set_volume(), vad_status()
├──────────────┤
│ Agent LoRa   │─── RPC → P4: send_mesh(), scan_lora(), mesh_status()
├──────────────┤
│ Agent Système│─── RPC → P4: battery(), cpu_temp(), wifi_status()
├──────────────┤
│ Agent LLM    │─── RWKV.cpp: generate(), chat(), summarize()
├──────────────┤
│ Orchestrateur│─── Coordonne les agents, gère le dialogue
└──────────────┘
```

**Flux typique:**
```
User: "Envoie un message LoRa à Paul et vérifie la batterie"
→ Orchestrateur → Agent LLM (parse intent)
                → Agent LoRa (RPC send_dm)
                → Agent Système (RPC battery)
                → Agent LLM (synthèse: "Message envoyé, batterie 72%")
                → Agent Audio (RPC play_tts: réponse vocale)
```

### 3.4 open-interpreter pour l'Exécution Autonome

| Propriété | Valeur |
|-----------|--------|
| **Repo** | `github.com/openinterpreter/open-interpreter` |
| **Language** | Python |
| **Fonction** | LLM contrôle terminal + fichiers |
| **Utilité JARVIX** | Exécution de scripts, logs, maintenance auto |

**Usage:** L'agent "Système" d'autogen délègue à open-interpreter pour:
- Analyser les logs du P4 (via DataStream)
- Modifier la configuration (fichiers YAML)
- Lancer des scripts de diagnostic
- Sauvegarder/restaurer des configurations mesh

### 3.5 SNN (snntorch + norse) pour ALPIG

| Propriété | snntorch | norse |
|-----------|----------|-------|
| **Repo** | `jeshraghian/snntorch` | `norse/norse` |
| **Language** | Python (PyTorch) | Python (PyTorch) |
| **État** | Production-ready (docs, tutos) | Recherche |
| **Utilité** | Entraînement de SNN sur GPU | Entraînement + simulation |
| **Cible P4** | Indirect — modèle entraîné puis exporté | Indirect |

**Potentiel pour ALPIG (Adaptive LoRa Pattern Identification):**
- SNN consomme **~100x moins d'énergie** que CNN/RNN équivalents
- Le P4 a un NPU (Neural Processing Unit) qui pourrait accélérer l'inférence SNN
- **Scenario:** Classifier les motifs RF (LoRa, WiFi, bruit) avec un SNN entraîné sur snntorch
- **Défis:** Pas de runtime SNN pour ESP32-P4 actuellement — nécessite export TFLite ou implémentation manuelle

**Roadmap:**
1. **Phase recherche:** Entraîner SNN sur snntorch avec données RF synthétiques
2. **Phase validation:** Comparer précision SNN vs ALPIG v2 heuristique
3. **Phase portage:** Exporter le modèle entraîné → TFLite → ESP32-P4 NPU
4. **Phase intégration:** Remplacer ALPIG v2 heuristique par SNN (< 1% CPU)

---

## PARTIE 4: RECOMMANDATIONS D'ARCHITECTURE

### 4.1 Priorité 1 — Choix du Protocole Mesh

**Recommandation: MeshCore comme protocole PRIMAIRE**

| Raison | Détail |
|--------|--------|
| **Codec2 voice** | Seul MeshCore supporte la voix sur LoRa (Meck-Voice), fonctionnalité clé de JARVIX-OS |
| **Sécurité** | HMAC présent (même court) — Meshtastic canal n'a AUCUNE intégrité |
| **Meck-P4 integration** | Meck-P4 a déjà l'infrastructure complète : radio, identity, UI, voice |
| **Deterministic** | Pas de CSMA/CA = timing prévisible pour audio |
| **Communauté** | Plus petite mais plus focalisée sur P4 |

**Meshtastic en SECONDARY** — pour interopérabilité avec le réseau Meshtastic existant.

### 4.2 Priorité 2 — Dual Protocol Strategy

**Phase 1 (Immédiat):** MeshCore only
- Utiliser l'infra Meck-P4 existante
- Intégrer MeshCore-official comme composant séparé
- Pas de dual protocole

**Phase 2 (3-6 mois):** Runtime switch (trail-mate model)
- Implémenter l'architecture à adaptateurs
- Time-slicing optionnel avec perte de paquets minimisée
- UI: indicateur de protocole actif

**Phase 3 (6-12 mois):** Dual radio si MMCX2 disponible
- SX1262 (868/915MHz) → MeshCore (voix + mesh)
- 2.4GHz → Meshtastic (interop) ou réseau LoRaWAN

### 4.3 Priorité 3 — Orange Pi Server Stack

```
Couche 1: RWKV.cpp → inférence LLM (chat, compréhension)
Couche 2: autogen → orchestration multi-agents
Couche 3: open-interpreter → exécution commandes système
Couche 4: LiveKit Server → transport Opus/WebRTC/RPC vers P4
```

**Déploiement:**
- Orange Pi 5 (RK3588, 8-16GB RAM)
- RWKV-7 1.5B Q4 (20-30 tok/s)
- autogen 0.4+ (Python)
- LiveKit Server Docker

### 4.4 Priorité 4 — ALPIG & SNN (Recherche)

- Entraîner SNN sur snntorch avec données RF
- Valider sur Orange Pi (pas P4)
- Si concluant (>90% précision, <1% CPU): portage vers P4 NPU

---

## PARTIE 5: FICHIERS CLÉS IDENTIFIÉS

| Fichier | Utilité |
|---------|---------|
| `MeshCore-official/src/Packet.h` | Format de trame MeshCore |
| `MeshCore-official/src/Identity.h` | Crypto Ed25519 + ECDH |
| `MeshCore-official/src/Mesh.h` | API routing MeshCore |
| `Meck-P4-main/components/meshcore/P4SX1262Radio.h` | Adaptateur radio SX1262 SPI polling |
| `Meck-P4-main/components/meshcore/MeckVoice.h` | Voix Codec2 sur LoRa |
| `Meck-P4-main/components/meshcore/variant.h` | Paramètres radio par région |
| `trail-mate/docs/meshcore/packet_structure.md` | Documentation format paquet MeshCore |
| `trail-mate/modules/core_chat/src/infra/meshcore/meshcore_protocol_helpers.cpp` | Implémentation helpers MeshCore |
| `trail-mate/modules/core_chat/src/infra/meshcore/mc_region_presets.cpp` | 17 presets régionaux MeshCore |
| `trail-mate/modules/core_chat/include/chat/infra/meshtastic/mt_radio_config.h` | Config radio Meshtastic |
| `gat45/p4/ARCHITECTURE_SYNTHESIS.md` | Architecture unifiée P4/C6 |
| `gat45/p4/REVERSE_COMPLETE.md` | Reverse complet avec gap analysis |
| `gat45/p4/UNIFIED_MODEL.json` | Modèle unifié (priorités, deadlines, constantes) |

---

**Rapport généré depuis l'analyse de 37 repos.**  
**Données brutes:** `reports/reverse_all_37.json` | `reports/REVERSE_ALL_37_CROISE.md`
