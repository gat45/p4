# Rapport: Reverse Engineering + Analyse Croisée des 4 Nouveaux Repos

**Date:** 11 Juin 2026  
**Auteur:** JARVIX-OS Analysis Engine  
**Objet:** esp-sr, LiveKit SDK, Waveshare P4 Platform, ESP32_Voice_Assistant

---

## 1. Matrice de Couverture (Nouveaux Repos vs JARVIX-OS)

| Fonctionnalité | esp-sr | LiveKit | Waveshare-P4 | ESP32_VA | JARVIX-OS |
|---|---|---|---|---|---|
| **P4 support** | ✅ 2 variantes lib | ✅ officiel | ✅ natif | ❌ | ✅ |
| **C6 support** | ✅ libs C6 | ❌ | ✅ esp_hosted | ❌ | ✅ |
| **AFE (VAD+WakeNet)** | ✅ complet | ✅ via esp_capture | ✅ Brookesia Agent | ❌ | ⚠️ manquant |
| **WakeNet9 "Jarvis"** | ✅ **wn9_jarvis_tts** | ❌ | ❌ | ❌ | ❌ |
| **VADNet1** | ✅ medium/float | ❌ | ✅ via esp-sr | ❌ | ❌ |
| **Opus encode/decode** | ❌ | ✅ intégré | ✅ via GMF | ❌ | ⚠️ partiel |
| **LiveKit client** | ❌ | ✅ v0.3.9 | ❌ | ❌ | ❌ |
| **WebSocket** | ❌ | ✅ esp_ws_client | ✅ esp_ws_client | ✅ Python | ✅ ha_client.c |
| **I2S + ES8311** | ❌ | ✅ custom_hw ex | ✅ 12_I2SCodec ex | ❌ | ❌ |
| **LVGL** | ❌ | ❌ | ✅ v9.4.x | ❌ | ✅ v9.x |
| **SDIO/esp-hosted** | ❌ | ❌ | ✅ esp_wifi_remote | ❌ | ✅ |
| **RPC AI Agent** | ❌ | ✅ livekit_rpc | ✅ Brookesia Agent | ❌ | ❌ |
| **TTS** | ✅ **Chinese only** | ✅ via AI Agent | ✅ Coze/TTS | ✅ Python | ❌ |
| **MultiNet** | ✅ v7 quant P4 | ❌ | ❌ | ❌ | ❌ |
| **ESP-IDF component** | ✅ espressif/esp-sr | ✅ livekit client | ✅ BSP + Brookesia | ❌ | ✅ composants |
| **Camera** | ❌ | ❌ | ✅ OV5647 MIPI | ❌ | ❌ |
| **Mesh/LoRa** | ❌ | ❌ | ❌ | ❌ | ✅ lora_scanner |
| **FreeRTOS prio modèle** | ❌ | ✅ 11 threads documentés | ✅ via Brookesia | ❌ | ⚠️ contradictoire |

**Légende:** ✅ = présent, ❌ = absent, ⚠️ = partiel/incomplet

---

## 2. Analyse Détaillée par Repo

### 2.1 esp-sr (Espressif Speech Recognition Framework)

**Version:** 2.4.6 | **Fichiers:** 393 (336 .h, 11 .cpp, 6 .c, 14 .py) | **Licence:** Espressif

#### Ce qui est CRITIQUE pour JARVIX-OS:

**✅ WakeNet9 "Jarvis" existe!**
- Modèle: `model/wakenet_model/wn9_jarvis_tts/`
- Type: WakeNet9l (large variant, ~1.3x CPU vs standard)
- Taille: ~291 KB flash (wn9_data + wn9_index)
- Seuils: detection window=3, threshold 90%=0.627, threshold 95%=0.632
- Activation Kconfig: `CONFIG_SR_WN_WN9_JARVIS_TTS=y`

**✅ AFE pipeline complet pour P4:**
- AEC + NS/SE + VAD + WakeNet en pipeline configurable
- API: `esp_afe_sr_iface_t` vtable (create/feed/fetch/destroy)
- Frame size: 16kHz PCM, chunksize configurable
- 2 modes: LOW_COST vs HIGH_PERF
- 3 types: SR (speech recog), VC (voice comm), FD (full duplex)
- 3 memory strategies: more internal, balanced, more PSRAM

**✅ Prebuilt libs P4:**
- `libwakenet.a` (776 KB) + `libvadnet.a` (190 KB) + `libnsnet.a` (310 KB)
- `libmultinet.a` (1.1 MB) + `libdl_lib.a` (4.0 MB)
- `libesp_audio_front_end.a` (665 KB) + `libesp_audio_processor.a` (4.5 MB)
- TTS: `libesp_tts_chinese.a` (1.9 MB) + `libvoice_set_xiaole.a` (4.5 MB)
- 2 variantes: standard P4 + P4 rev less v3

**✅ TTS présent mais Chinois seulement:**
- 4 voix: Xiaole (défaut), Xiaoxin, Xiaoxin Custom, Xiaoxin Small
- Données vocales: 2.9-3.8 MB par voix (fichiers .dat)
- API: `esp_tts_parse_chinese()`, `esp_tts_stream_play()`
- **Pas de TTS anglais** — limitation majeure pour JARVIX-OS

**⚠️ Limitations:**
- Pas d'Opus (dépend du projet)
- Pas de WebSocket (dépend du projet)
- Pas d'I2S direct (dépend du BSP)
- TTS chinois uniquement

---

### 2.2 LiveKit ESP32 SDK (client-sdk-esp32)

**Version:** 0.3.9 (Developer Preview) | **Fichiers:** 116 (38 .c, 40 .h, 14 .md) | **Licence:** Apache 2.0

#### Ce qui est CRITIQUE pour JARVIX-OS:

**✅ LiveKit client complet pour P4:**
- Support officiel: `targets: [esp32s3, esp32p4]`
- SDK complet: WebSocket signaling + WebRTC peer + Opus + DataStream + RPC
- Test app avec sdkconfig P4 dédié

**✅ Architecture déjà structurée pour l'audio:**
- `livekit_room_create()` avec `livekit_room_options_t` incluant:
  - `.publish.audio_info` (codec=OPUS, sample_rate=16000, channel_count=1)
  - `.subscribe.audio_info` (même config)
  - Capturer: `esp_capture_handle_t` (esp_capture)
  - Renderer: `av_render_handle_t` (av_render)
- Opus déjà intégré nativement (pas besoin de notre composant opus/)

**✅ AI Agents RPC:**
- `livekit_room_rpc_register()` / `livekit_room_rpc_unregister()`
- Max payload: 15 KB (JSON)
- Handlers avec callback `send_result()`
- Macros: `livekit_rpc_return_ok()`, `livekit_rpc_return_error()`
- **RPC = request-response uniquement** (audio bidir = WebRTC séparé)

**✅ DataStream API:**
- Header + Chunks (15 KB) + Trailer protocol
- Topics registration
- Text (UTF-8 safe chunking) + Binary streams

**✅ 4 exemples:**
1. **voice_agent** → le plus pertinent: Opus 16kHz mono bidirectional + AI Agent RPC
2. **custom_hardware** → init manuel I2S + ES8311 + ES7210 (P4-compatible)
3. **minimal** → connection de base
4. **minimal_video** → avec vidéo

**⚠️ Limitations:**
- **Developer Preview** (pas production ready)
- C6 non supporté (P4 only + S3)
- VAD/WakeNet absents (doit venir de esp-sr)
- LVGL absent (doit être intégré séparément)
- Réseau géré externellement (pas de WiFi dans le SDK lui-même)

**📊 Thread Model LiveKit:**
| Thread | Stack | Prio | Core | Rôle |
|---|---|---|---|---|
| `aenc_0` (Opus) | 40 KB | 10 | 1 | Audio encode |
| `buffer_in` | 6 KB | 10 | 0 | Capture buffer |
| `AUD_SRC` | 40 KB | 15 | — | Audio source |
| `lk_peer_sub` | 25 KB | 18 | 1 | WebRTC subscriber |
| `lk_peer_pub` | 25 KB | 18 | 1 | WebRTC publisher |
| `lk_eng_stream` | 4 KB | 15 | 1 | Media streaming |
| `Adec` | 40 KB | 15 | 0 | Audio decode |
| `ARender` | — | 20 | — | Audio render |
| `engine_task` | 8 KB | 5 | — | Engine state machine |

---

### 2.3 Waveshare ESP32-P4-Platform

**Fichiers:** 3146 (1458 .c, 256 .cpp, 853 .h) | **Licence:** Apache 2.0

#### Ce qui est CRITIQUE pour JARVIX-OS:

**✅ Référence Hardware P4 complète:**
- 7 board variants supportées
- Pinout I2S ES8311 documenté: MCLK=13, BCLK=12, WS=10, DOUT=9, DIN=11, PA=53
- I2C: SDA=7, SCL=8
- Exemple `12_I2SCodec` = le plus propre pour P4 audio bringup

**✅ ESP-Hosted + ESP32-C6 intégré:**
- `CONFIG_SLAVE_IDF_TARGET_ESP32C6=y`
- `CONFIG_ESP_HOSTED_CP_TARGET_ESP32C6=y`
- Composants: `espressif/esp_wifi_remote: "0.14.*"`, `espressif/esp_hosted: "1.4.*"`
- Exemples WiFi: `10_wifistation`, `15_eth2ap`

**✅ Brookesia Framework:**
- Version 0.6.0-beta2
- Agent AI avec AFE pipeline + Coze chat + function calling
- LVGL v9.4.x, Phone UI system
- Audio GMF pipeline (Generic Media Framework)
- **AI Framework désactivé par défaut** (`CONFIG_ESP_BROOKESIA_ENABLE_AI_FRAMEWORK=n`)

**✅ LVGL v9.4.x:**
- 3 DPI buffers (triple partial anti-tear)
- RGB565, résolutions jusqu'à 1280x800
- Touch GT911

**⚠️ Limitations:**
- **Pas de LiveKit** (utilise Coze chat à la place)
- **WakeNet9 absent** (Brookesia utilise VAD seulement)
- **Opus non direct** (GMF + G711A pour uplink)
- **Taille énorme** (3K+ fichiers, framework lourd)

---

### 2.4 ESP32_Voice_Assistant (arpy8)

**Fichiers:** 4 (1 .ino, 1 .h, 2 .md, 1 .py) | **Licence:** MIT

#### Résumé:
- Architecture simple: ESP32 → WebSocket → Python server → TTS/STT/LLM
- Code ESP: `esp-code.ino` (Arduino, pas ESP-IDF)
- Server: `server/main.py` (Python, FastAPI)
- **Pas de P4, pas de C6, pas de I2S, pas d'Opus**
- **Utilité limitée** pour JARVIX-OS, confirme juste l'architecture PC=AI, ESP=hardware

---

## 3. Analyse Croisée: Nouvelles Découvertes vs JARVIX-OS

### 3.1 Contradictions Résolues

| Sujet | Avant | Après |
|---|---|---|
| **Jarvis wake word** | Hypothétique (mentionné dans sdkconfig Meck-P4) | **Confirmé**: `wn9_jarvis_tts` dans esp-sr, WakeNet9l, 291 KB flash |
| **LiveKit remplace ha_client** | Suggestion | **Validé**: architecture complète, P4 supporté, Opus intégré, RPC pour AI Agent |
| **Opus composant séparé** | Nécessaire | **Redondant**: LiveKit a déjà Opus intégré (mais on garde notre composant pour fallback) |
| **I2S + ES8311 config** | Théorique | **Documenté**: GPIO pins Waveshare P4, code exemple `12_I2SCodec` |
| **Thread priorities** | 15-25 (faux) | **Confirmé**: LiveKit utilise 5-20, Meck-P4 utilise 1-3 |

### 3.2 Nouvelles Découvertes

1. **LiveKit RPC + DataStream remplacent tout le custom WebSocket**
   - `livekit_rpc.h` permet AI function calling directement
   - `livekit_data_stream.h` permet streaming de données
   - Plus besoin de parser JSON manuellement pour les commandes AI

2. **esp-sr apporte tout le pipeline audio local**
   - AFE = VAD + WakeNet + AEC + NS + AGC
   - `wn9_jarvis_tts` = wake word "Jarvis" natif
   - MultiNet7 = commandes vocales locales (400 phrases)
   - **Seule limitation**: TTS chinois seulement

3. **Waveshare P4 Platform = la référence hardware**
   - Pinout exact pour T-Display P4
   - I2S + ES8311 déjà opérationnel
   - ESP-Hosted C6 déjà intégré
   - **Différence clé**: utilise Coze (pas LiveKit), pas de WakeNet9

4. **LiveKit SDK a déjà un thread model documenté**
   - 11 threads avec stack/priorité/core
   - Priorités 5-20 (consistent avec notre V3)
   - Peut servir de base pour notre priority budget model

### 3.3 Impact sur l'Architecture JARVIX-OS

#### Avant (plan actuel):
```
P4: ha_client.c (WebSocket custom) → Opus component (notre code) → I2S
C6: wifi_manager.c (proxy) → SDIO → esp-hosted
```

#### Après (recommandé):
```
P4: LiveKit SDK (Opus natif + RPC + DataStream) → esp-sr AFE (VAD+WakeNet) → I2S ES8311
C6: wifi_manager.c (proxy inchangé) → SDIO → esp-hosted
```

**Ce qui change:**
- `ha_client.c` → **remplacé** par LiveKit SDK
- `components/opus/` → optionnel (LiveKit a déjà Opus)
- `components/audio/voice_pipeline.c` → intégré avec esp-sr AFE
- AI Agent → LiveKit RPC (pas de custom WebSocket)
- Wake word → `wn9_jarvis_tts` via esp-sr

**Ce qui reste inchangé:**
- `components/lora_scanner/` (indépendant)
- `components/sdio_watchdog/`
- `components/RadioLib/`
- `components/lvgl_ui/`
- `main/i2s_loopback_benchmark.c`

---

## 4. Recommandations d'Intégration

### Priorité 1 (Immédiat):
- [ ] Intégrer `espressif/esp-sr` via `idf.py add-dependency "espressif/esp-sr^2.4.6"`
- [ ] Activer `CONFIG_SR_WN_WN9_JARVIS_TTS=y` + `CONFIG_SR_VADN_VADNET1_MEDIUM=y`
- [ ] Copier le modèle `wn9_jarvis_tts` dans la partition SPIFFS
- [ ] Intégrer LiveKit SDK via `idf.py add-dependency` (ou copier components/)
- [ ] Adapter `custom_hardware` example pour T-Display P4 pinout

### Priorité 2 (Pipeline Audio):
- [ ] Remplacer `ha_client.c` par `livekit_room_connect()`
- [ ] Connecter AFE (esp-sr) en amont de LiveKit: `afe_feed()` → `livekit publish`
- [ ] Connecter LiveKit subscribe → `av_render_add_audio_data()` → I2S ES8311
- [ ] S'assurer que le buffer sortie AFE alimente directement le capturer LiveKit

### Priorité 3 (AI Agent):
- [ ] Enregistrer RPC handlers pour les fonctions JARVIX-OS
- [ ] Utiliser `livekit_room_data_stream_open()` pour logs/data télémetry
- [ ] Configurer le AI Agent (Python côté serveur) avec les outils RPC

### Priorité 4 (Intégration Complète):
- [ ] Remplacer Coze (Brookesia) par LiveKit dans le Waveshare BSP
- [ ] Benchmark mémoire: esp-sr (500-800 KB PSRAM) + LiveKit (200-400 KB) + LVGL (TBD)
- [ ] Valider que les modèles tiennent dans 16 MB flash + PSRAM

---

## 5. Résumé des Fichiers Clés Indentifiés

| Fichier | Repo | Utilité |
|---|---|---|
| `esp-sr/model/wakenet_model/wn9_jarvis_tts/` | esp-sr | Modèle wake word "Jarvis" |
| `esp-sr/include/esp32p4/esp_afe_sr_iface.h` | esp-sr | API AFE pour P4 |
| `esp-sr/include/esp32p4/esp_afe_config.h` | esp-sr | Configuration AFE |
| `esp-sr/lib/esp32p4/*.a` (11 libs) | esp-sr | Prebuilt libs P4 |
| `client-sdk-esp32/components/livekit/include/livekit.h` | LiveKit | API publique LiveKit |
| `client-sdk-esp32/components/livekit/include/livekit_rpc.h` | LiveKit | API RPC AI Agent |
| `client-sdk-esp32/components/livekit/examples/voice_agent/` | LiveKit | Exemple voix complet |
| `client-sdk-esp32/components/livekit/examples/custom_hardware/board.c` | LiveKit | Init I2S manuel P4 |
| `ESP32-P4-Platform/examples/esp-idf/12_I2SCodec/main/i2s_es8311_example.c` | Waveshare | Exemple I2S ES8311 P4 |
| `ESP32-P4-Platform/firmware/brookesia/components/brookesia_core/ai_framework/agent/audio_processor.c` | Waveshare | Pipeline audio complet (GMF) |

---

## 6. Métriques de Validation (Plan de Mesure)

| Métrique | Cible | Méthode |
|---|---|---|
| **WakeNet9 CPU %** | < 15% (P4 400 MHz) | `esp_timer_get_time()` avant/après afe_fetch() |
| **VADNet1 CPU %** | < 5% | Même méthode |
| **AFE pipeline latency** | < 30ms | afe_feed() → afe_fetch() round-trip |
| **LiveKit Opus encode CPU** | < 10% | Mesure thread aenc_0 |
| **LiveKit WebRTC latency** | < 100ms | `lk_peer_sub` → speaker |
| **SDIO throughput (avec LiveKit)** | > 8 Mbps | iperf3 over esp-hosted |

---

*Rapport généré par reverse_4_new_repos.py + analyse croisée manuelle*
*Données brutes: `reports/reverse_4_new.json`, `reports/reverse_4_new_report.txt`*
