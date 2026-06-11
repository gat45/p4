# Rapport de santé des repos — JARVIX-OS

> Analyse des issues, PRs, bugs, et activité des mainteneurs
> Date : 2026-06-11

---

## 1. esp-hosted (espressif) ★★★ CRITIQUE
**Stars:** 1k | **Issues ouvertes:** 333 | **PR ouvertes:** 18

### Bugs bloquants pour nous
| Issue | Problème | Impact |
|-------|----------|--------|
| [#740](https://github.com/espressif/esp-hosted/issues/740) | **C6 bootloop pendant init SDIO quand P4 en download mode** — TG0_WDT_HPSYS/LP_WDT_SYS en ROM. Testé sur Waveshare P4-WIFI6-Touch-LCD-7B (même board !). Toutes versions 2.8.0→2.12.8 affectées | **BLOQUANT** — impossible à débugger si P4 freeze |
| [#742](https://github.com/espressif/esp-hosted/issues/742) | **esp_hosted 2.12.8 hang + reboot sur activité WiFi élevée** — ouvert il y a 8 jours | **BLOQUANT** — crash en production |
| [#739](https://github.com/espressif/esp-hosted/issues/739) | **sdio_mempool_create assert** avec CONFIG_ESP_HOSTED_MEMPOOL_PREFER_SPIRAM sur P4+C5 (probablement aussi C6) | **BLOQUANT** — peut empêcher PSRAM |
| [#633](https://github.com/espressif/esp-hosted/issues/633) | **ESP non détecté tant que sd-controller non rebind** — exactement le scénario de notre watchdog V2 | **BLOQUANT** — watchdog V2 impuissant |
| [#588](https://github.com/espressif/esp-hosted/issues/588) | **Faible performance SDIO (iperf)** — plusieurs utilisateurs confirment | notre 36 Mbps peut être surfait |
| [#667](https://github.com/espressif/esp-hosted/issues/667) | **Turn off WiFi radio when interface is down** — pas de power management | drain 33mA permanent |
| [#733](https://github.com/espressif/esp-hosted/issues/733) | **Compatibilité API WiFi standard** — esp_hosted_ng utilise sa propre API, pas esp_wifi_init() standard | friction d'intégration |

### Activité mainteneurs
- Dernière release : v2.12.8 (mai 2026)
- Réponse aux issues : lente (certaines ouvertes depuis 2024 sans réponse)
- PRs en attente : 18 ouvertes, certaines depuis des mois
- ⚠️ **Projet en mode maintenance, pas de développement actif visible**

---

## 2. esp-sr (espressif) ★★★ CRITIQUE
**Stars:** 1.4k | **Issues ouvertes:** 41 | **PR ouvertes:** 0

### Bugs bloquants pour nous
| Issue | Problème | Impact |
|-------|----------|--------|
| [#203](https://github.com/espressif/esp-sr/issues/203) | **P4 v1.3 eco2 : WakeNet create_from_config hang dans flash_model_info (hufzip) → TASK_WDT reset** — Le P4 de T-Display P4 est un v1.3 (pas v3.0+). `CONFIG_ESP32P4_SELECTS_REV_LESS_V3=y` requis mais hufzip boucle infiniment. **Aucune solution connue** | **BLOQUANT** — Phase 1 impossible |
| [#210](https://github.com/espressif/esp-sr/issues/210) | AEC distortion en Bluetooth HFP — qualité AEC limitée | dégradé en main-libre |
| [#199](https://github.com/espressif/esp-sr/issues/199) | WakeNet StoreProhibited crash sur ESP32-S3-BOX-3 (IDF 5.3.1) | crash possible |
| [#195](https://github.com/espressif/esp-sr/issues/195) | Sensibilité wake word insuffisante pour parole lente | taux de faux négatifs |
| [#202](https://github.com/espressif/esp-sr/issues/202) | Performance Multinet insuffisante — CPU élevé | confirme notre estim ~25% |

### Activité mainteneurs
- Dernière release : esp-sr v2.4.4
- **0 PR ouvertes** — personne ne contribue activement
- Issues sans réponse depuis des mois
- ⚠️ **Projet semble en stase — aucune fusion de code récente**

---

## 3. LiveKit client-sdk-esp32 ★★ HAUT
**Stars:** 129 | **Issues ouvertes:** 4 | **PR ouvertes:** 7

### Bugs connus
| Issue | Problème | Impact |
|-------|----------|--------|
| [#59](https://github.com/livekit/client-sdk-esp32/issues/59) | **Room create/destroy fails after 4-5 cycles** — assigné à ladvoc, mais **ouvert depuis 6 mois sans résolution**. "Failed to create engine" en cycle | fuite mémoire engine |
| [#86](https://github.com/livekit/client-sdk-esp32/issues/86) | Failed to decode signal responses with LiveKit Server v1.10.0 | incompatibilité serveur |
| [#43](https://github.com/livekit/client-sdk-esp32/issues/43) | Multiple users connected, device can't hear them | multiroom cassé |

### PRs ouvertes importantes
| PR | Description | Statut |
|----|-------------|--------|
| [#67](https://github.com/livekit/client-sdk-esp32/pull/67) | **ESP32-P4 et ESP32-H2 compatibilité** — met à jour esp_wifi_remote + esp_hosted pour P4. Review requested depuis mars 2026 | ⏳ **EN ATTENTE — pas mergé !!** |
| [#89](https://github.com/livekit/client-sdk-esp32/pull/89) | RPC v2 protocol constants | DRAFT |
| [#68](https://github.com/livekit/client-sdk-esp32/pull/68) | Subscribe to multiple audio tracks + RFC 6464 audio level | ouvert, 10 commentaires |

### Activité mainteneurs
- SDK en **Developer Preview** (v0.3.8)
- PR #67 (P4 compat) bloquée — review requested depuis mars
- LiveKit a levé $100M Series C — priorité probablement cloud, pas embedded
- ⚠️ **Le SDK n'est pas encore officiellement compatible P4 sans PR #67**

---

## 4. meshtastic/firmware ★★ HAUT
**Stars:** 7.8k | **Issues ouvertes:** 269 | **PR ouvertes:** 211

### Bugs pertinents
| Issue | Problème | Impact |
|-------|----------|--------|
| [#10692](https://github.com/meshtastic/firmware/issues/10692) | Muzi Superbase unbootable après activation Canned Message | crash firmware |
| [#10510](https://github.com/meshtastic/firmware/issues/10510) | LilyGo T-Echo auto-restart au lieu de shutdown | power management |
| [#10335](https://github.com/meshtastic/firmware/issues/10335) | RAK10720 unreachable over Ethernet après un certain temps | timeout réseau |
| [#10685](https://github.com/meshtastic/firmware/issues/10685) | T-Beam Supreme Compass error | bug capteur |

### Feature requests actifs
- [#8383](https://github.com/meshtastic/firmware/issues/8383) Power saving via GPS acceleromètre
- [#7553](https://github.com/meshtastic/firmware/issues/7553) RGB LED for node status
- [#10687](https://github.com/meshtastic/firmware/issues/10687) Contention window pour nodes portables

### Activité mainteneurs
- 211 PRs ouvertes — très actif
- v3.0 en développement (renommage de fichiers #10296)
- Projet très sain, communauté active

---

## 5. bmorcelli/Launcher (ESP-Launcher) ★ MOYEN
**Stars:** 1.7k | **Issues ouvertes:** 23 | **PR ouvertes:** 3

### Bugs pertinents
| Issue | Problème | Impact |
|-------|----------|--------|
| [#331](https://github.com/bmorcelli/Launcher/issues/331) | **T-Deck Max screen refresh ghosting** — rapporté par **pelgraine** (créateur Meck-P4 !) | touch UI |
| [#332](https://github.com/bmorcelli/Launcher/issues/332) | Error ordering OTA list by "latest" | bug catalogue |
| [#330](https://github.com/bmorcelli/Launcher/issues/330) | Tulip partitions not installing properly (Lilygo T-Deck) | partition bug |
| [#336](https://github.com/bmorcelli/Launcher/issues/336) | **Add Meshcomod (MeshCore touch firmware for LilyGo T-Deck) to LauncherHub** | MeshCore adoption |

### Info clé
- **pelgraine reporte des bugs à bmorcelli** → les devs se parlent
- Nouveaux ports demandés : T3S3, C5 Pancake, Waveshare S3 LCD, M5Stack Tab5
- Launcher très actif (issues de juin 2026)

---

## 6. pelgraine/Meck-P4 ★ MOYEN
**Stars:** 9 | **Issues ouvertes:** 0 | **PR ouvertes:** 0

### Constats
- **Aucune issue** — projet trop petit pour avoir du feedback
- **Aucune PR** — développeur solo
- pelgraine actif sur Launcher (T-Deck Max bug) et probablement Meck-P4 en privé
- Dernier commit : Meck-P4-main (branche main, plus récente que v2)
- ⚠️ **Projet maintenu par une seule personne, risque bus factor**

---

## 7. MeshCore (meshcore-dev) ★★★ ACTIF
**Stars:** 3 031 | **Issues ouvertes:** 597 | **PR ouvertes:** 316
**URL correcte:** https://github.com/meshcore-dev/MeshCore
**Dernière activité:** 8 juin 2026

### Organisation complète
| Repo | Description | Stars |
|------|-------------|-------|
| MeshCore | Protocole mesh principal (C) | 3 031 |
| meshcore-ha | Intégration Home Assistant (Python) | 205 |
| meshcore-cli | Interface CLI (Python) | 160 |
| meshcore_py | Bindings Python | 101 |
| meshcore.js | Bindings JavaScript | 41 |
| map.meshcore.io | Carte MeshCore officielle | 34 |
| flasher.meshcore.io | Flash web de firmware | 19 |
| config.meshcore.io | UI de configuration repeater/room | 1 |
| blog.meshcore.io | Blog | 2 |
| Adafruit_nRF52_Arduino | Fork pour nRF52 | 0 |

### Correctif
- **NOTRE CLONE** : `MeshCore-official/` (merlin-chen/MeshCore) - fonctionnel
- Le code actif est chez `meshcore-dev/MeshCore`
- **597 issues** et **316 PRs** → beaucoup de retours utilisateurs et correctifs disponibles
- Documentation officielle : https://docs.meshcore.io/
- CLI: https://meshcore.ai/docs/mesh-cli (site différent, peut-être un miroir)

---

## 8. RWKV-LM / RWKV-X / rwkv.cpp ★ BAS
- Projets LLM — pas d'impact direct sur le firmware ESP32
- RWKV.cpp actif (ARM64/x86), PR régulières
- RWKV-X en développement (architecture MoE?)
- Aucune pertinence pour le P4

---

## 9. autogen (Microsoft) ★ BAS
**Stars:** 58.9k | **Issues ouvertes:** 533 | **PR ouvertes:** 347

### Tendance
- 533 issues ouvertes — volume élevé de signalements
- 347 PRs — projet très actif
- Focus actuel : gouvernance, sécurité, identité des agents
- Aucun bug rapporté côté ESP32/P4 (logique — c'est un framework Python)
- Utilisation prévue uniquement sur Orange Pi → pas de risque direct

---

## 10. open-interpreter ★ BAS
**Stars:** 63.9k | **Issues ouvertes:** 263

### Problèmes de sécurité
- [#1766](https://github.com/openinterpreter/open-interpreter/issues/1766) **Path Traversal Vulnerability in EditTool.write_file**
- [#1767](https://github.com/openinterpreter/open-interpreter/issues/1767) **/settings endpoint allows modification of sensitive interpreter attributes**
- Vulnérabilités actives non patchées

---

## 11. trail-mate ★ MOYEN
- Issues non vérifiées (docs/audits uniquement en local)
- Architecture de dual-boot MeshCore/Meshtastic validée
- Aucun bug critique connu sur le dual-protocol

---

## 12. stream-video-esp32 ★ MOYEN
- **Repo introuvable** (404) — peut-être supprimé ou renommé depuis le clone
- Fallback vidéo à vérifier

---

## 13. SNN (snntorch, norse) ★ BAS
- Projets de recherche académique
- snntorch : 381 fichiers, PyTorch
- norse : 244 fichiers, PyTorch + Loihi
- **Aucun runtime ESP32** — pure recherche
- Issues principalement sur l'API Python, pas sur l'embarqué

---

## Résumé des risques bloquants

| Priorité | Risque | Repo | Correctif possible |
|----------|--------|------|--------------------|
| **P0** | WakeNet hang sur P4 v1.3 eco2 (hufzip) | esp-sr #203 | Utiliser P4 rev ≥ v3.0, ou contourner WakeNet (VAD-only), ou attendre fix esp-sr |
| **P0** | esp_hosted 2.12.8 reboot sur haut débit WiFi | esp-hosted #742 | Utiliser 2.10.0 ? ou downgrade ? ou SPI fallback ? |
| **P0** | LiveKit PR #67 (P4 compat) pas mergé | LiveKit #67 | Forquer et patcher soi-même |
| **P0** | C6 bootloop si P4 en download mode | esp-hosted #740 | Jamais mettre P4 en download avec C6 alimenté |
| **P1** | LiveKit room leak après 4-5 cycles | LiveKit #59 | Ne pas reconnecter — connexion persistante |
| **P1** | SDIO 0x107 recovery impossible (host side) | esp-hosted #633 | Watchdog V2 = seul espoir (C6 GPIO reset) |
| **P1** | Priorités threads LiveKit (5-20) vs System Governor (1-3) | LiveKit SDK | Audit de toutes les priorités avant intégration |
| **P2** | Vulnerabilités sécurité OI non patchées | open-interpreter | Sandboxer l'usage Orange Pi |
| **P2** | MeshCore plus de dev visible | MeshCore | Forker ou utiliser code stable actuel |
| **P2** | Meck-P4 = bus factor 1 | Meck-P4 | Préparer notre propre fork |
