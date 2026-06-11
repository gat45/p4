# Architecture Unifiée P4/C6 — Synthèse

## Principe: Single Deterministic Audio Runtime

```
┌─────────────────────────────────────────────┐
│              ORANGE PI (Server)              │
│   STT → LLM → TTS → Opus encode → UDP      │
└──────────────────────┬──────────────────────┘
                       │ UDP Opus 20ms
┌──────────────────────┴──────────────────────┐
│           ESP32-C6 (Network Modem)          │
│  WiFi PS=NONE │ UDP RX/TX │ SDIO bridge    │
│  Jitter buffer: 80-150ms                    │
│  Priority: SDIO > WiFi > application        │
└──────────────────────┬──────────────────────┘
                       │ SDIO 2048B frames
┌──────────────────────┴──────────────────────┐
│           ESP32-P4 (Audio Core)             │
│  Core 0: I2S DMA → Opus Enc → SDIO TX      │
│          AFE/VAD (priority 22)              │
│  Core 1: LVGL UI (priority 15)             │
│          Lua Agent (priority 10)            │
│  Memory: DMA=IRAM, UI=PSRAM, Agent=PSRAM   │
│  Jitter buffer: 20-40ms                     │
└─────────────────────────────────────────────┘
```

## Classification des Paradigmes

| Paradigme | Où | Contrainte |
|---|---|---|
| **Streaming temps réel** | P4 Core 0 | Deadline 20ms, DMA IRAM |
| **Transport asynchrone** | C6 | Backpressure, queue sizing |
| **Event-driven** | P4 Core 1 | Non-déterministe, LVGL/Lua |
| **Network opportuniste** | WiFi C6 | Jitter 5-10ms (beacon) |

## Primitives Extraites

### Audio
- afe_init: `main\audio_capture.c`
- es8311: `common_components\espressif__esp32_p4_function_ev_board\include\bsp\esp32_p4_function_ev_board.h`
- i2s_init: `common_components\espressif__esp32_p4_function_ev_board\esp32_p4_function_ev_board.c`
- i2s_read: `main\audio_capture.c`
- i2s_write: `main\audio_capture.c`
- ringbuf: `main\audio_ref_buffer.c`
- vad: `main\audio_capture.c`
- wakenet: `main\audio_capture.c`

### Transport
- backpressure: `esp_hosted_ng\host\esp_stats.c`
- dma_alloc: `esp_hosted_ng\esp\esp_driver\network_adapter\main\cmd.c`
- handshake: `esp_hosted_ng\host\spi\esp_spi.c`
- iramo: `esp_hosted_ng\esp\esp_driver\network_adapter\main\cmd.c`
- priority_queue: `esp_hosted_ng\host\include\adapter.h`
- queue_create: `esp_hosted_ng\esp\esp_driver\network_adapter\main\app_main.c`
- sdio_init: `esp_hosted_ng\esp\esp_driver\network_adapter\main\sdio_slave_api.c`
- sdio_read: `esp_hosted_ng\host\sdio\esp_sdio_api.c`
- sdio_write: `esp_hosted_ng\host\sdio\esp_sdio.c`
- spi_slave_init: `esp_hosted_ng\esp\esp_driver\network_adapter\main\spi_slave_api.c`
- wifi_ps: `esp_hosted_fg\host\linux\host_control\c_support\test_utils.c`
- zero_copy: `esp_hosted_ng\host\esp_bt.c`

### RTOS Tasks critiques
- `alarm_check` stack=2048 prio=NULL
- `ha_reconnect` stack=6144 prio=reason_copy
- `led_effect` stack=4096 prio=NULL
- `led_test` stack=2048 prio=NULL
- `music_ctl` stack=4096 prio=(void *
- `music_ctl` stack=4096 prio=(void *
- `mqtt_metrics` stack=4096 prio=NULL
- `net_post` stack=4096 prio=(void *
- `led_ready` stack=2048 prio=NULL
- `mqtt_setup` stack=4096 prio=NULL

## Validation Pipeline

### Étape 1: Loopback I2S (P4 seul)
- Source: `esp-adf/examples/audio_processing/pipeline_passthru/`
- + `ha_voice/common_components/bsp_extra/src/bsp_board_extra.c`
- Critères: 0 underrun / 60s, CPU < 30% Core 0

### Étape 2: Transport P4↔C6
- Source: `esp-hosted/esp/esp_driver/network_adapter/main/sdio_slave_api.c`
- + `ha_voice/main/wifi_manager.c`
- Critères: burst 100 frames 0 loss, backpressure recovery < 100ms

### Étape 3: Pipeline Complet
- Source: `ha_voice/main/voice_pipeline.c` + `ha_voice/main/ha_client.c`
- Critères: E2E latency < 500ms, jitter < 40ms, 5 min continuous
