# RAPPORT REVERSE COMPLET — Tous Projets Analysés
**Date:** 10 Juin 2026  
**Portée:** 7 projets, 30+ fichiers critiques, tous les sous-systèmes

---

## 1. RÉSUMÉ EXÉCUTIF

| Projet | Fichiers lus | Patterns extraits | Verdict |
|---|---|---|---|
| **ha_voice** | 7 (bsp_extra, audio_capture, voice_pipeline, ha_client, wifi_manager, audio_ref_buffer, sdkconfig) | AEC hook, dual-task AFE, command queue FSM, binary WS frames, C6 WiFi remote, 3-tier task creation | ✅ Référence pipeline audio complète |
| **esp-hosted** | 7 (adapter.h, sdio_slave_api, spi_slave_api, app_main, esp_sdio, esp_spi, interface.h) | Wire protocol 12B, SDIO 20×2048 DMA pool, SPI handshake GPIO, backpressure thresholds, zero-copy WiFi, priority queues | ✅ Transport P4↔C6 complet |
| **esp-adf** | 8 (ringbuf, i2s_stream, algorithm_stream, audio_element, audio_pipeline, audio_mem, recording_example, coze_ws) | Ring buffer semaphore flow, element→rb→element chain, SPIRAM-aware alloc, Opus 64kbps config, pipeline link/run/stop | ✅ Framework audio modulaire |
| **xiaozhi** | 5 (audio_service, afe_processor, afe_wake_word, sdkconfig.esp32p4, README) | Opus 60ms frames, queue-based encode/decode, dual AFE instances (wake+VAD), P4+C6 co-proc | ✅ Voice assistant production |
| **meshcore** | 5 (Dispatcher, Mesh, Packet, P4SX1262Radio, target) | 1-byte header, flood/direct/zero-hop routing, polling radio model, sync word 0x1424, cpp_bus_driver wrapping | ✅ Mesh LoRa compact |
| **meshtastic** | 6 (RadioInterface, SX126xInterface, Router, FloodingRouter, NextHopRouter, portnums.pb.h) | 16-byte protobuf header, ISR radio model, next-hop learning, RETICULUM_TUNNEL_APP=76, RadioLib wrapping | ✅ Mesh LoRa production |
| **JARVIX-OS** | 3 (main.cpp, linker.ld, memory_watchdog.h) | 2 tasks only (Radio+Lua), IRAM isolation linker, heap watchdog | ⚠️ Squelette — 70% manquant |

---

## 2. PRIMITIVES CRITIQUES EXTRAITES

### 2.1 AUDIO — Ce qu'il faut réutiliser

| Primitive | Source exacte | Ligne | Comment l'utiliser dans JARVIX |
|---|---|---|---|
| **AEC reference hook** | `ha_voice/bsp_extra/src/bsp_board_extra.c` | 141-143 | `bsp_extra_i2s_write_register_callback(audio_ref_buffer_write)` — hook AVANT écriture I2S pour capturer le signal de référence |
| **Codec reorder ES8311** | `ha_voice/bsp_extra/src/bsp_board_extra.c` | 180-201 | Fermer record → Fermer playback → Ouvrir playback EN PREMIER → Ouvrir record EN DERNIER (ES8311 ADC quirk) |
| **Dual-task AFE** | `ha_voice/main/audio_capture.c` | 178-307 | feed_task (Core 0, prio 6, 8KB) lit I2S → fetch_task (Core 1, prio 5, 16KB) traite AFE/VAD/WakeNet |
| **3-tier task creation** | `ha_voice/main/audio_capture.c` | 78-111 | Interne → PSRAM → Static PSRAM (fallback en cascade) |
| **Ring buffer AEC** | `ha_voice/main/audio_ref_buffer.c` | 24-63 | 16KB, zero-timeout write (non-blocking), silence fill on underread |
| **Command queue FSM** | `ha_voice/main/voice_pipeline.c` | 48-61, 296-495 | Enum de commandes + FreeRTOS queue + task switch (12KB stack PSRAM) |
| **Binary WS audio frame** | `ha_voice/main/ha_client.c` | 660-686 | `[1-byte handler_id] + [PCM/Opus data]`, send_bin avec 2s timeout |
| **Opus config** | `esp-adf/examples/recorder/.../recording_to_sdcard_example.c` | 152-156 | 16kHz, mono, 64kbps, complexity=10 |
| **Element→Ringbuf chain** | `esp-adf/components/audio_pipeline/audio_pipeline.c` | 495-521 | `rb_create(el->out_rb_size, 1)` entre chaque élément (défaut 8KB) |
| **SPIRAM-aware alloc** | `esp-adf/components/audio_sal/audio_mem.c` | 65-77 | `audio_malloc()` → `heap_caps_malloc(MALLOC_CAP_SPIRAM)` automatique |
| **Audio element task loop** | `esp-adf/components/audio_pipeline/audio_element.c` | 460-507 | `wait cmd → process → repeat`, STOPPED/TASK_DESTROYED event bits |

### 2.2 TRANSPORT — Wire protocol P4↔C6

| Primitive | Source exacte | Ligne | Détails |
|---|---|---|---|
| **12-byte header** | `esp-hosted/host/include/adapter.h` | 27-45 | `if_type:4 + if_num:4`, `flags`, `packet_type`, `len(LE16)`, `offset(LE16)`, `checksum(LE16)`, `reserved` |
| **Interface types** | `esp-hosted/host/include/adapter.h` | 66-73 | STA=0, AP=1, HCI=2, INTERNAL=3, TEST=4 |
| **Priority queues** | `esp-hosted/host/include/adapter.h` | 128 | HIGH=0 (control), MID=1 (BT), LOW=2 (WiFi) |
| **SDIO DMA pool** | `esp-hosted/esp/.../sdio_slave_api.c` | 40 | 20 buffers × 2048B statiques, pas de heap |
| **Zero-copy WiFi** | `esp-hosted/esp/.../sdio_slave_api.c` | 262-265 | Header dans le headroom `wifi_pkt_rx_ctrl_t`, pas de memcpy |
| **SPI handshake** | `esp-hosted/esp/.../spi_slave_api.c` | 341-355 | GPIO HS HIGH = ready, LOW = busy. GPIO DR HIGH = data pending |
| **Backpressure SDIO** | `esp-hosted/host/sdio/esp_sdio.c` | 27-28 | TX_MAX=200, RESUME=40, drop si plein |
| **Backpressure SPI** | `esp-hosted/host/spi/esp_spi.c` | 21-22 | TX_MAX=100, RESUME=20, `netif_stop_queue()` |
| **App bridge** | `esp-hosted/esp/.../app_main.c` | 517-574 | `process_rx_pkt`: DATA→`esp_wifi_internal_tx()`, CMD→handler |
| **SDIO queue depth** | `esp-hosted/esp/.../app_main.c` | 84-94 | SPI=20, SDIO=100 (to_host_queue) |

### 2.3 MESH — Switch MeshCore↔Meshtastic

| Primitive | MeshCore | Meshtastic |
|---|---|---|
| **Sync word** | `0x1424` (`target.cpp:94`) | `0x2B` (`RadioLibInterface.h:84`) |
| **Header** | 1-byte (2b route + 4b type + 2b version) | 16-byte (NodeNum to/from, PacketId, flags, channel) |
| **Radio driver** | `cpp_bus_driver::Sx126x` (polling) | RadioLib `SX1262` (ISR via DIO1) |
| **Routing** | Flood+path-hash, Direct+precomputed path | Hop-limit flood, NextHop learning from ACK relay |
| **Encryption** | AES-128 CBC + HMAC (per-peer ECDH) | AES-CTR channel / AES-256-CCM PKI |
| **Payload** | Raw binary (max 184B) | Protobuf `MeshPacket` |
| **Packet pool** | `PacketManager` (alloc/free/queue) | `PointerQueue` (fromRadioQueue) |

**Verdict switch:** Dual firmware partition (OTA_0=MeshCore, OTA_1=Meshtastic). NVS flag pour sélection. Pas de switch runtime possible (drivers incompatibles: polling vs ISR).

### 2.4 MEMORY & RTOS — Patterns extraits

| Pattern | Source | Usage |
|---|---|---|
| **IRAM_ATTR** | esp-hosted: 20 refs, meshcore: 48 refs | Fonctions critiques DMA/IRQ en mémoire interne |
| **MALLOC_CAP_DMA** | esp-hosted: 12 refs, meshcore: 15 refs | Buffers DMA contigus |
| **MALLOC_CAP_SPIRAM** | esp-adf: 8 refs, meshcore: 28 refs | Stacks/buffs larges en PSRAM |
| **Semaphore** | esp-adf: 68, esp-hosted: 110, jarvix: 131 | Flow control + sync |
| **portMUX spinlock** | ha_voice/audio_capture.c:148-162 | Flag `is_running` cross-task |
| **Event group bits** | ha_voice/ha_client.c:54-57 | CONNECTED_BIT, AUTHENTICATED_BIT, AUDIO_READY_BIT |
| **Static task create** | ha_voice/voice_pipeline.c:213-226 | Stack en PSRAM via `xTaskCreateStatic` |
| **Watchdog feed** | ha_voice/sys_diag.c:138-169 | TWDT configurable, feed dans les longues opérations |

---

## 3. CE QUE JARVIX-OS N'A PAS (Gap Analysis)

| Composant | ha_voice a | JARVIX n'a pas | Priorité |
|---|---|---|---|
| `audio_capture.c` (feed+fetch tasks) | ✅ | ❌ | **CRITIQUE** |
| `voice_pipeline.c` (state machine) | ✅ | ❌ | **CRITIQUE** |
| `ha_client.c` (WebSocket streaming) | ✅ | ❌ | **CRITIQUE** |
| `wifi_manager.c` (C6 SDIO) | ✅ | ❌ | **CRITIQUE** |
| `audio_ref_buffer.c` (AEC ring) | ✅ | ❌ | HAUTE |
| `tts_player.c` (MP3 decode) | ✅ | ❌ | HAUTE |
| `bsp_extra.c` (codec HAL) | ✅ | ❌ (a es8311.cpp basique) | **CRITIQUE** |
| Opus encoder/decoder | ✅ | ❌ | **CRITIQUE** |
| Command queue FSM | ✅ | ❌ | HAUTE |
| 3-tier task creation | ✅ | ❌ | MOYENNE |
| Jitter buffer double | Concept | ❌ | HAUTE |

---

## 4. MODÈLE D'EXÉCUTION UNIFIÉ POUR JARVIX-OS

```
┌─────────────────────────────────────────────────────┐
│                ORANGE PI (Serveur)                   │
│   STT → LLM → TTS → Opus encode → UDP 20ms        │
└──────────────────────┬──────────────────────────────┘
                       │ UDP (Opus 16-32kbps)
┌──────────────────────┴──────────────────────────────┐
│             ESP32-C6 (Modem Réseau)                  │
│  WiFi PS=NONE │ UDP RX/TX │ SDIO bridge             │
│  Jitter buffer: 80-150ms                             │
│  Priority: SDIO_IRQ > WiFi_IRQ > application        │
│  Queue: 100 items (to_host_queue)                    │
│  DMA: 20×2048B pool statique                         │
└──────────────────────┬──────────────────────────────┘
                       │ SDIO (2048B frames, 12B header)
┌──────────────────────┴──────────────────────────────┐
│             ESP32-P4 (Audio Deterministe)            │
│                                                     │
│  Core 0 (Temps réel):                               │
│    I2S DMA read → Opus encode → SDIO TX             │
│    AFE/VAD/WakeNet (prio 22)                        │
│    Memory: MALLOC_CAP_DMA (IRAM)                    │
│    Deadline: 20ms/frame                              │
│                                                     │
│  Core 1 (Application):                              │
│    LVGL UI (prio 15)                                │
│    Lua Agent (prio 10)                               │
│    LoRa Radio (prio 25)                              │
│    Memory: PSRAM                                     │
│                                                     │
│  Jitter buffer P4: 20-40ms                           │
│  AEC reference: 16KB ring buffer (zero-timeout)      │
└─────────────────────────────────────────────────────┘
```

---

## 5. VALIDATION PIPELINE — Ordre Industriel

### Étape 1: Loopback I2S (P4 seul, 0 réseau)
**Fichiers sources:** `ha_voice/bsp_extra/src/bsp_board_extra.c` + `esp-adf/examples/audio_processing/pipeline_passthru/`
- Initialiser ES8311 avec le codec reorder (play first, record last)
- Créer pipeline: `[i2s_reader] → [opus_encoder] → [opus_decoder] → [i2s_writer]`
- Critères: **0 DMA underrun / 60s**, CPU < 30% Core 0

### Étape 2: Transport P4↔C6 (pas de WiFi)
**Fichiers sources:** `esp-hosted/esp/.../sdio_slave_api.c` + `esp-hosted/esp/.../app_main.c`
- Flasher C6 avec firmware esp-hosted network_adapter
- P4 envoie frames Opus via SDIO → C6 loopback
- Critères: **burst 100 frames 0 loss**, backpressure recovery < 100ms

### Étape 3: Pipeline Complet (P4+C6+Server)
**Fichiers sources:** `ha_voice/voice_pipeline.c` + `ha_voice/ha_client.c`
- WiFi PS=NONE sur C6
- UDP streaming Opus 20ms vers serveur
- Critères: **E2E latency < 500ms**, jitter < 40ms, 5 min continuous

### Étape 4: Mesh Mode Switch
**Fichiers sources:** `meshcore/target.cpp` + `meshtastic/RadioInterface.h`
- Dual partition OTA: MeshCore (ota_0) + Meshtastic (ota_1)
- NVS flag pour sélection au boot
- Reset radio + reinit complète

---

## 6. CONSTANTES CRITIQUES (pour le code)

| Paramètre | Valeur | Source |
|---|---|---|
| I2S read len | 512 samples | ha_voice/audio_capture.c:31 |
| Opus frame duration | 20ms (ha_voice) / 60ms (xiaozhi) | ha_voice + xiaozhi |
| Opus bitrate | 16-64 kbps | esp-adf/recording_example |
| SDIO frame size | 2048 bytes | esp-hosted/sdio_slave_api.c |
| SPI frame size | 1600 bytes | esp-hosted/esp_spi.h |
| SDIO queue depth | 100 (to_host_queue) | esp-hosted/app_main.c:93 |
| SPI queue depth | 20 (to_host_queue) | esp-hosted/app_main.c:90 |
| SDIO DMA pool | 20 × 2048B static | esp-hosted/sdio_slave_api.c:40 |
| Backpressure SDIO | TX_MAX=200, RESUME=40 | esp-hosted/esp_sdio.c:27 |
| Backpressure SPI | TX_MAX=100, RESUME=20 | esp-hosted/esp_spi.c:21 |
| AEC ring buffer | 16KB, zero-timeout | ha_voice/audio_ref_buffer.c:32 |
| Pipeline ring buffer | 8KB default | esp-adf/audio_pipeline.h:43 |
| Jitter buffer P4 | 20-40ms | Architecture synthesis |
| Jitter buffer C6 | 80-150ms | Architecture synthesis |
| Feed task stack | 8KB internal | ha_voice/audio_capture.c:34 |
| Fetch task stack | 16KB (fallback chain) | ha_voice/audio_capture.c:113 |
| Pipeline task stack | 12KB PSRAM | ha_voice/voice_pipeline.c:72 |
| MeshCore sync word | 0x1424 | meshcore/target.cpp:94 |
| Meshtastic sync word | 0x2B | meshtastic/RadioLibInterface.h:84 |
| Wire protocol header | 12 bytes | esp-hosted/adapter.h:27 |
| ES8311 codec reorder | Play first, record last | ha_voice/bsp_extra.c:180 |

---

*Fin du rapport reverse — Tous projets analysés*
