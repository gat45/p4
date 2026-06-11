# Rapport Croisé: 37 Repos — Analyse Multi-Domaine

**Date:** 11 Juin 2026  
**Méthode:** `reverse_all_37.py` — 47 features keyword-matching sur 35 repos trouvés  
**Données brutes:** `reports/reverse_all_37.json`

---

## 1. Synthèse par Catégorie (Classement)

### Audio Pipeline (I2S, ES8311, AFE, VAD, WakeNet, Opus, TTS)
| Rang | Repo | Score | Points forts |
|------|------|-------|-------------|
| 1 | **esp-adf** | **9/12** | I2S, ES8311, ES7210, AFE, VAD, Opus, G711, PCM, TTS |
| 2 | **xiaozhi-esp32** | **8/12** | I2S, ES8311, ES7210, AFE, WakeNet, Opus, PCM, TTS |
| 2 | **HA-Voice** | **8/12** | I2S, ES8311, AFE, VAD, WakeNet, PCM, TTS, STT |
| 2 | **JARVIX-OS** | **8/12** | ES8311, AFE, VAD, WakeNet, Opus, PCM, TTS, STT |
| 5 | **client-sdk-esp32** | **7/12** | I2S, ES8311, ES7210, AFE, Opus, G711, TTS |
| 5 | **ESP32-audioI2S** | **7/12** | I2S, ES8311, AFE, VAD, Opus, PCM, TTS |
| 7 | **stream-video-esp32** | **4/12** | I2S, ES8311, ES7210, Opus |
| 8 | **Meck-P4-main** | **4/12** | I2S, AFE, VAD, STT |

### LLM & Inférence (RWKV, GGML, LLaMA, SNN, Agent)
| Rang | Repo | Score | Points forts |
|------|------|-------|-------------|
| 1 | **rwkv.cpp** | **3/8** | RWKV, GGML, LLaMA |
| 1 | **snntorch** | **3/8** | snnTorch, AutoGen, Agent |
| 1 | **autogen** | **3/8** | LLaMA, AutoGen, Agent |
| 4 | **esp-adf** | **2/8** | AutoGen, Agent |
| 4 | **HA-Voice** | **2/8** | AutoGen, Agent |
| 4 | **open-interpreter** | **2/8** | LLaMA, Agent |

### Réseau & Streaming (WebSocket, LiveKit, WebRTC)
| Rang | Repo | Score | Points forts |
|------|------|-------|-------------|
| 1 | **client-sdk-esp32** | **4/5** | WebSocket, LiveKit, WebRTC, SIP |
| 2 | **stream-video-esp32** | **3/5** | WebSocket, LiveKit, WebRTC |
| 3 | **esp-adf** | **2/5** | WebSocket, SIP |
| 3 | **xiaozhi-esp32** | **2/5** | WebSocket, MQTT |

### Transport P4↔C6 (SDIO, SPI, UART)
| Rang | Repo | Score | Points forts |
|------|------|-------|-------------|
| 1 | **Meck-P4-main** | **3/3** | SDIO, SPI, UART |
| 1 | **esp-hosted** | **3/3** | SDIO, SPI, UART |
| 1 | **stream-video-esp32** | **2/3** | SDIO, SPI |
| 4 | **T-Display-P4** | **2/3** | SDIO, SPI |
| 4 | **esp32p4-c6-wifi-test** | **2/3** | SDIO, UART |

### LoRa & Mesh (SX1262, SX1276, Meshtastic, MeshCore)
| Rang | Repo | Score | Points forts |
|------|------|-------|-------------|
| 1 | **JARVIX-OS** | **5/5** | SX1262, SX1276, LoRa, Meshtastic, MeshCore |
| 2 | **meshtastic-firmware** | **4/5** | SX1262, LoRa, Meshtastic, MeshCore |
| 2 | **firmware-develop** | **4/5** | SX1262, LoRa, Meshtastic, MeshCore |
| 2 | **trail-mate** | **4/5** | SX1262, LoRa, Meshtastic, MeshCore |
| 5 | **Meck-P4-main** | **3/5** | SX1262, LoRa, MeshCore |

---

## 2. Nouveautés vs Connaissances Précédentes

### 2.1 stream-video-esp32 — **NOUVEAU RIVAL DE LIVEKIT**

GetStream/stream-video-esp32 est un SDK audio/video *spécifiquement conçu* pour ESP32-P4/S3 avec:
- **LiveKit intégré** comme backend (`components/stream-video/idf_component.yml:livekit`)
- WebRTC + WebSocket + Opus 16kHz
- I2S + ES8311 + ES7210 (codec board)
- SDIO + SPI pour transport
- Documentation API `docs/api_reference.md`
- **Avantage vs LiveKit SDK**: Plus orienté "video doorbell"/intercom, mais ajoute du video streaming que LiveKit SDK vanilla n'a pas

### 2.2 ESP32-audioI2S — **BIBLIOTHÈQUE AUDIO ARDUINO**
- 112 fichiers, populaire pour proto rapide
- Gère MP3/AAC/AAC/FLAC streaming HTTP
- Nécessite PSRAM
- Utile pour **prototype rapide** mais pas pour architecture agentique JARVIX-OS

### 2.3 T-Connection-P4-Pro — **CARTE LILYGO AVEC SX1276**
- 4051 fichiers (!), grosse librairie LVGL 9.2.0 + ESP32_Display_Panel
- **SX1276** (pas SX1262) — confirmation: LilyGO utilise SX1276 pour le module LoRa
- SPI + UART + LVGL + Display
- **Pas d'AFE, pas d'Opus, pas de WakeNet** — juste une plateforme HMI
- Important pour le **LoRa driver spécifique** à la carte

### 2.4 SX1262-Arduino-ESP32-driver — **DRIVER SX1266 MODERNE**
- 4 fichiers seulement — driver Arduino pur
- Compatible P4 via SPI
- Alternative plus légère à RadioLib
- **Utilité**: driver de référence si RadioLib a des soucis de compatibilité P4

### 2.5 RWKV.cpp — **INFÉRENCE LLM EMBARQUÉE**
- 83 fichiers, implémentation C++ de RWKV
- Support GGML/GGUF — compatible avec les modèles quantifiés
- Peut tourner sur ARM64/RK3588 (Orange Pi)
- **Pas de support ESP32** — CPU x86/ARM uniquement
- Utile pour le **Orange Pi serveur**

### 2.6 open-interpreter — **AGENT DE CODE AUTONOME**
- 4269 fichiers, projet mature
- Permet à un LLM de contrôler terminal/fichiers
- Pour **Orange Pi** (pas ESP32)
- Peut servir de base pour l'agent serveur JARVIX-AGENT

### 2.7 autogen — **FRAMEWORK MULTI-AGENTS MICROSOFT**
- 1837 fichiers
- Architecture multi-agents: diviser tâches audio/LoRa/système entre agents
- Pour **Orange Pi** — orchestration côté serveur

### 2.8 snntorch + norse — **SNN (SPIKING NEURAL NETWORKS)**
- snnTorch: 381 fichiers, PyTorch-compatible
- Norse: 244 fichiers, PyTorch-compatible
- **Recherche** — pas encore applicable en production embarquée
- SNN = ultra basse consommation, potentiel pour inference on-device ESP32-P4

---

## 3. Hiérarchie des Repos par Domaine JARVIX-OS

### P4 Audio Pipeline
```
esp-adf (référence) → client-sdk-esp32 (LiveKit) → stream-video-esp32 (WebRTC)
    ↕                        ↕
esp-sr (VAD+WakeNet)    ESP32-audioI2S (Arduino proto)
```

### P4 Transport
```
esp-hosted (SDIO/SPI) → esp32p4-c6-wifi-test (benchmarks)
    ↕
T-Display-P4, T-Connection-P4-Pro, Meck-P4-main (implémentations)
```

### LoRa/Mesh
```
meshtastic-firmware → firmware-develop → trail-mate → JARVIX-OS
    ↕                        ↕
RadioLib-master ←→ SX1262-Arduino-ESP32-driver
```

### LLM/Agent (Orange Pi Server)
```
RWKV.cpp → open-interpreter → autogen
    ↕                ↕
snntorch → norse (recherche SNN)
```

---

## 4. Analyse Croisée: Impacts sur JARVIX-OS

### Découverte 1: stream-video-esp32 — alternative plus légère à LiveKit SDK
- Même backend LiveKit mais plus orienté intercom/doorbell
- Si le SDK LiveKit vanilla a des bugs sur P4, essayer stream-video-esp32
- **Recommandation**: Garder LiveKit SDK comme primaire, stream-video comme backup

### Découverte 2: T-Connection-P4-Pro utilise SX1276, pas SX1262
- Notre lora_scanner cible SX1262 — vérifier si LilyGO T-Display P4 utilise SX1276 ou SX1262
- Impact: peut nécessiter driver SX1276 dans RadioLib (déjà présent)

### Découverte 3: esp-adf est le roi incontesté de l'audio
- 9/12 features audio — référence absolue
- Pipeline audio: source → codec → filter → sink
- **Suggestion**: Utiliser l'architecture pipeline d'esp-adf comme modèle architectural, même si on utilise LiveKit pour le transport

### Découverte 4: RWKV.cpp ne tourne PAS sur ESP32
- CPU seulement (ARM64/x86) — pour Orange Pi
- Confirme: LLM reste côté serveur, pas sur ESP32-P4
- SNN (snntorch/norse) = recherche, pas production

### Découverte 5: autogen + open-interpreter = orchestration côté serveur
- open-interpreter = exécution autonome (contrôle terminal/fichiers)
- autogen = coordination multi-agents
- **Architecture suggérée**: autogen orchestre → open-interpreter exécute → RWKV.cpp fait inférence

---

## 5. Recommandations Prioritaires Mises à Jour

### P4 Audio (short-term)
1. **Intégrer esp-sr** → AFE + `wn9_jarvis_tts` + VADNet1
2. **Intégrer LiveKit SDK** → remplacer ha_client.c + Opus component
3. **Utiliser i2s_es8311_example.c** (Waveshare) comme référence I2S pour T-Display P4

### P4 LoRa (short-term)
4. **Vérifier SX1262 vs SX1276** sur T-Display P4 physique
5. **Adapter lora_scanner.c** si nécessaire

### Orange Pi Server (medium-term)
6. **Déployer RWKV.cpp** comme backend LLM
7. **Configurer autogen** pour l'orchestration multi-agents
8. **Intégrer open-interpreter** pour exécution de commandes

### Recherche (long-term)
9. **Évaluer snntorch/norse** pour classification LoRa basse consommation
10. **Explorer SNN sur P4** pour ALPIG v2 (ultra low power classification)

---

## 6. Matrice Finale: 35 Repos × 8 Domaines

Voir `reports/reverse_all_37.json` pour la matrice complète.

**Top 5 Repos les plus complets** (tous domaines confondus):
| Repo | Score total (max 47) | Domaines couverts |
|------|---------------------|-------------------|
| **esp-adf** | 25+ | Audio, Network, UI, LLM, Hardware, RTOS |
| **client-sdk-esp32** | 22+ | Audio, Network, UI, Hardware, RTOS |
| **HA-Voice** | 22+ | Audio, Network, Transport, UI, Hardware, RTOS |
| **xiaozhi-esp32** | 18+ | Audio, Network, UI, Hardware |
| **JARVIX-OS** | 18+ | Audio, Network, Transport, LoRa, UI, RTOS |

JARVIX-OS est le seul à couvrir **tous les domaines** (audio + réseau + transport + LoRa + UI + RTOS) mais reste faible en LLM et hardware P4-specific.
