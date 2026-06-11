# Rapport d'Analyse: JARVIX-OS (Notre Projet)
**Projet:** `jarvix`

## Statistiques
- Fichiers scannes: 575
- Fichiers avec matches: 314
- Lignes totales: 326412
- Matches total: 21562

## Distribution par Categorie
- **mesh**: 20182 ??????????????????????????????????????????????????
- **timing**: 437 ??????????????????????????????????????????????????
- **audio**: 404 ??????????????????????????????????????????????????
- **rtos**: 277 ??????????????????????????????????????????????????
- **transport**: 128 ??????????????????????????????????????????????????
- **memory**: 79 ??????????????????????????????????????????????????
- **network**: 55 ??????????????????????????????????????????????????

## ??  Findings Critiques (CRITICAL)
- `JARVIX-OS\main\i2s_loopback_benchmark.c:103` [dma_buffer] `.dma_desc_num = DMA_BUFFER_COUNT,`
- `JARVIX-OS\main\i2s_loopback_benchmark.c:104` [dma_buffer] `.dma_frame_num = DMA_BUFFER_LEN,`
- `JARVIX-OS\main\i2s_loopback_benchmark.c:132` [dma_buffer] `.dma_desc_num = DMA_BUFFER_COUNT,`
- `JARVIX-OS\main\i2s_loopback_benchmark.c:133` [dma_buffer] `.dma_frame_num = DMA_BUFFER_LEN,`
- `JARVIX-OS\main\i2s_loopback_benchmark.c:4` [jitter_buffer] `* Mesure: jitter audio brut, DMA starvation, latency réelle.`
- `JARVIX-OS\main\i2s_loopback_benchmark.c:17` [jitter_buffer] `*   - Jitter percentile (p50/p95/p99)`
- `JARVIX-OS\main\i2s_loopback_benchmark.c:209` [memory_placement] `int16_t *frame = heap_caps_malloc(BYTES_PER_FRAME, MALLOC_CAP_DMA);`
- `JARVIX-OS\main\i2s_loopback_benchmark.c:262` [memory_placement] `int16_t *frame = heap_caps_malloc(BYTES_PER_FRAME, MALLOC_CAP_DMA);`
- `JARVIX-OS\components\audio\audio_capture.c:74` [memory_placement] `int16_t *mic_buff = heap_caps_malloc(I2S_READ_LEN * sizeof(int16_t), MALLOC_CAP_DMA);`
- `JARVIX-OS\components\audio\audio_capture.c:75` [memory_placement] `int16_t *ref_buff = heap_caps_malloc(I2S_READ_LEN * sizeof(int16_t), MALLOC_CAP_DMA);`
- `JARVIX-OS\components\audio\audio_capture.c:76` [memory_placement] `int16_t *afe_buff = heap_caps_malloc(I2S_READ_LEN * 2 * sizeof(int16_t), MALLOC_CAP_DMA);`
- `JARVIX-OS\components\audio\audio_ref_buffer.c:31` [memory_placement] `ring_buf = heap_caps_malloc(size, MALLOC_CAP_DMA | MALLOC_CAP_8BIT);`
- `JARVIX-OS\components\audio\bsp_extra.c:89` [dma_buffer] `.dma_desc_num = DMA_BUFFER_COUNT,`
- `JARVIX-OS\components\audio\bsp_extra.c:90` [dma_buffer] `.dma_frame_num = DMA_BUFFER_LEN,`
- `JARVIX-OS\components\audio\bsp_extra.c:112` [dma_buffer] `.dma_desc_num = DMA_BUFFER_COUNT,`
- `JARVIX-OS\components\audio\bsp_extra.c:113` [dma_buffer] `.dma_frame_num = DMA_BUFFER_LEN,`
- `JARVIX-OS\components\audio\tts_player.c:182` [flow_control] `void tts_player_pause(void) {`
- `JARVIX-OS\components\audio\tts_player.c:185` [flow_control] `player_state = TTS_STATE_PAUSED;`
- `JARVIX-OS\components\audio\tts_player.c:192` [flow_control] `if (player_state == TTS_STATE_PAUSED) {`
- `JARVIX-OS\components\audio\tts_player.c:47` [memory_placement] `int16_t *pcm_buf = heap_caps_malloc(PCM_BYTES_MAX, MALLOC_CAP_DMA);`
- `JARVIX-OS\components\audio\wifi_manager.c:3` [wifi_remote] `* ESP32-C6 coprocessor via SDIO (esp_wifi_remote)`
- `JARVIX-OS\components\audio\wifi_manager.c:10` [wifi_remote] `#include "esp_wifi_remote.h"`
- `JARVIX-OS\components\sdio_watchdog\sdio_watchdog.c:8` [sdio_bridge] `*   P4 GPIO → C6 EN pin → C6 reboot → sdio_slave_reset() sur C6`
- `JARVIX-OS\components\sdio_watchdog\sdio_watchdog.c:13` [sdio_bridge] `*   esp-hosted/esp_hosted_ng/esp/.../sdio_slave_api.c:464 (sdio_slave_reset)`
- `JARVIX-OS\components\sdio_watchdog\sdio_watchdog.c:14` [sdio_bridge] `*   esp-hosted/esp_hosted_fg/esp/.../sdio_slave_api.c:694 (sdio_slave_reset)`
- `JARVIX-OS\components\sdio_watchdog\sdio_watchdog.c:96` [sdio_bridge] `* Après reset C6, le slave appelle sdio_slave_reset() puis sdio_slave_start().`
- `JARVIX-OS\components\sdio_watchdog\sdio_watchdog.c:128` [sdio_bridge] `*   3. Wait C6 boot + sdio_slave_reset() + sdio_slave_start()`
- `JARVIX-OS\components\sdio_watchdog\sdio_watchdog.c:126` [flow_control] `*   1. PAUSE audio pipeline (callback si registré)`
- `JARVIX-OS\components\sdio_watchdog\sdio_watchdog.c:140` [flow_control] `/* Step 1: Notify system to pause audio */`
- `JARVIX-OS\components\sdio_watchdog\sdio_watchdog.c:141` [flow_control] `if (s_cfg.pause_audio_cb) {`

## Detail par Sous-systeme

### afe_pipeline (7 matches)
- `JARVIX-OS\components\audio\audio_capture.c:109` `if (afe_handle && afe_handle->feed) {`

### codec_init (9 matches)
- `JARVIX-OS\components\audio\bsp_extra.c:28` `static void es8311_init(void) {`
- `JARVIX-OS\components\meshcore\es8311.cpp:5` `* same I2S channel LilyGo's ES8311_Init() configured at boot, sharing the`

### dma_buffer (8 matches)
- `JARVIX-OS\main\i2s_loopback_benchmark.c:103` `.dma_desc_num = DMA_BUFFER_COUNT,`
- `JARVIX-OS\components\audio\bsp_extra.c:89` `.dma_desc_num = DMA_BUFFER_COUNT,`

### encryption (388 matches)
- `JARVIX-OS\components\opus\src\pitch_analysis_core_FIX.c:109` `opus_int32 CC[ PE_NB_CBKS_STAGE2_EXT ], CCmax, CCmax_b, CCmax_new_b, CCmax_new;`

### flow_control (105 matches)
- `JARVIX-OS\components\audio\tts_player.c:182` `void tts_player_pause(void) {`
- `JARVIX-OS\components\sdio_watchdog\sdio_watchdog.c:126` `*   1. PAUSE audio pipeline (callback si registré)`

### i2s_capture (11 matches)
- `JARVIX-OS\main\i2s_loopback_benchmark.c:222` `esp_err_t ret = i2s_channel_read(rx_handle, frame,`
- `JARVIX-OS\components\audio\audio_capture.c:24` `#define I2S_READ_LEN          512 // Samples per read (32ms @ 16kHz)`
- `JARVIX-OS\components\audio\bsp_extra.c:163` `esp_err_t bsp_extra_i2s_read(void *dest, size_t size, size_t *bytes_read, uint32_t timeout_ms) {`

### i2s_driver (7 matches)
- `JARVIX-OS\main\i2s_loopback_benchmark.c:126` `ESP_RETURN_ON_ERROR(i2s_channel_init_std_mode(tx_handle, &tx_std_cfg), TAG, "tx std");`
- `JARVIX-OS\components\audio\bsp_extra.c:107` `ESP_RETURN_ON_ERROR(i2s_channel_init_std_mode(tx_handle, &tx_std_cfg), TAG, "tx std");`
- `JARVIX-OS\components\chmorgan__esp-audio-player\test\audio_player_test.c:130` `ESP_ERROR_CHECK(i2s_channel_init_std_mode(*tx_channel, p_i2s_cfg));`

### i2s_playback (21 matches)
- `JARVIX-OS\main\i2s_loopback_benchmark.c:280` `esp_err_t ret = i2s_channel_write(tx_handle, frame,`
- `JARVIX-OS\components\audio\audio_capture.c:211` `bsp_extra_i2s_write_register_callback(audio_ref_buffer_write);`
- `JARVIX-OS\components\audio\bsp_extra.c:16` `static bsp_i2s_write_cb_t write_callback = NULL;`
- `JARVIX-OS\components\audio\tts_player.c:69` `esp_err_t ret = i2s_channel_write(tx_handle, pcm_buf, bytes, &written, portMAX_DELAY);`
- `JARVIX-OS\components\chmorgan__esp-audio-player\test\audio_player_test.c:70` `static esp_err_t bsp_i2s_write(void * audio_buffer, size_t len, size_t *bytes_written, uint32_t time`

### jitter_buffer (16 matches)
- `JARVIX-OS\main\i2s_loopback_benchmark.c:4` `* Mesure: jitter audio brut, DMA starvation, latency réelle.`
- `JARVIX-OS\components\opus\src\opus_encoder.c:111` `opus_val16   delay_buffer[MAX_ENCODER_BUFFER*2];`

### lora_radio (14117 matches)
- `JARVIX-OS\components\lora_scanner\lora_scanner.c:5` `*   L1 PHYSICAL  — SX1262 radio profile (one at a time)`

### memory_placement (10 matches)
- `JARVIX-OS\main\i2s_loopback_benchmark.c:209` `int16_t *frame = heap_caps_malloc(BYTES_PER_FRAME, MALLOC_CAP_DMA);`
- `JARVIX-OS\components\audio\audio_capture.c:74` `int16_t *mic_buff = heap_caps_malloc(I2S_READ_LEN * sizeof(int16_t), MALLOC_CAP_DMA);`
- `JARVIX-OS\components\audio\audio_ref_buffer.c:31` `ring_buf = heap_caps_malloc(size, MALLOC_CAP_DMA | MALLOC_CAP_8BIT);`
- `JARVIX-OS\components\audio\tts_player.c:47` `int16_t *pcm_buf = heap_caps_malloc(PCM_BYTES_MAX, MALLOC_CAP_DMA);`
- `JARVIX-OS\components\private_library\radiolib_bridge_driver.cpp:17` `void IRAM_ATTR Interrupt_Callback_Template(void *arg)`
- `JARVIX-OS\components\RadioLib\src\protocols\LoRaWAN\LoRaWAN.cpp:1561` `IRAM_ATTR`
- `JARVIX-OS\components\RadioLib\src\protocols\Pager\Pager.cpp:19` `IRAM_ATTR`

### mqtt (10 matches)
- `JARVIX-OS\components\audio\audio_capture.c:4` `* Based on: Home-Assistant-MQTT-Voice-Assistant/audio_capture.c`
- `JARVIX-OS\components\audio\audio_ref_buffer.c:5` `* Based on: Home-Assistant-MQTT-Voice-Assistant/audio_ref_buffer.c`
- `JARVIX-OS\components\audio\ha_client.c:5` `* Based on: Home-Assistant-MQTT-Voice-Assistant/ha_client.c`
- `JARVIX-OS\components\audio\voice_pipeline.c:5` `* Based on: Home-Assistant-MQTT-Voice-Assistant/voice_pipeline.c`
- `JARVIX-OS\components\audio\wifi_manager.c:5` `* Based on: Home-Assistant-MQTT-Voice-Assistant/wifi_manager.c`
- `JARVIX-OS\components\audio\audio_capture.h:6` `* Based on: Home-Assistant-MQTT-Voice-Assistant/audio_capture.c`
- `JARVIX-OS\components\audio\audio_ref_buffer.h:5` `* Based on: Home-Assistant-MQTT-Voice-Assistant/audio_ref_buffer.c`
- `JARVIX-OS\components\audio\ha_client.h:5` `* Based on: Home-Assistant-MQTT-Voice-Assistant/ha_client.h`
- `JARVIX-OS\components\audio\voice_pipeline.h:5` `* Based on: Home-Assistant-MQTT-Voice-Assistant/voice_pipeline.h`
- `JARVIX-OS\components\audio\wifi_manager.h:5` `* Based on: Home-Assistant-MQTT-Voice-Assistant/wifi_manager.c`

### opus_decode (108 matches)
- `JARVIX-OS\components\audio\tts_player.c:15` `#define OPUS_DECODE_FRAME_MS 20`

### opus_encode (114 matches)
- `JARVIX-OS\components\opus\src\opus_encoder.c:93` `#define OPUS_ENCODER_RESET_START stream_channels`

### psram_usage (69 matches)
- `JARVIX-OS\main\main.cpp:153` `// 10. Tâche Lua (Core 1 - Isolation Heap/PSRAM)`
- `JARVIX-OS\components\meshcore\es8311.cpp:219` `*   3. Loop: meck_audio_mic_read(buf, len) into PSRAM buffer`
- `JARVIX-OS\components\meshcore\MeckAudio.cpp:620` `* stack_size vs stack_in_psram), adjust here. */`
- `JARVIX-OS\components\meshcore\MeckMapScreen.cpp:99` `// still a modest PSRAM cost for the widget structs themselves`
- `JARVIX-OS\components\meshcore\MeckNotesUI.cpp:632` `* and is ample for hand-typed text. Allocated once in PSRAM (not internal BSS)`
- `JARVIX-OS\components\meshcore\MeckUI.cpp:628` `// are allocated lazily from PSRAM on first message touching that contact,`

### ring_buffer (25 matches)
- `JARVIX-OS\main\i2s_loopback_benchmark.c:57` `#define RING_BUF_COUNT   4`

### routing (92 matches)
- `JARVIX-OS\components\meshcore\MeckUI.cpp:5477` `mesh->sendFlood(adv);`
- `JARVIX-OS\components\meshcore\meck_app.cpp:48` `// marks every outgoing packet in the seen-table at sendFlood time, which`

### sample_rate_config (57 matches)
- `JARVIX-OS\main\i2s_loopback_benchmark.c:45` `#define SAMPLE_RATE     16000`
- `JARVIX-OS\components\audio\bsp_extra.c:96` `.clk_cfg = I2S_STD_CLK_DEFAULT_CONFIG(BSP_I2S_SAMPLE_RATE),`
- `JARVIX-OS\components\audio\tts_player.c:87` `if (!config || config->sample_rate == 0) {`

### sdio_bridge (5 matches)
- `JARVIX-OS\components\sdio_watchdog\sdio_watchdog.c:8` `*   P4 GPIO → C6 EN pin → C6 reboot → sdio_slave_reset() sur C6`

### sync_word (5585 matches)
- `JARVIX-OS\components\audio\bsp_extra.c:69` `es8311_write_reg(0x2B, 0x00);`
- `JARVIX-OS\components\lora_scanner\lora_scanner.c:30` `[RADIO_PROF_MESHTASTIC_LF] = {12, 500, 0x2B, 868100000, "MeshtLF"},`
- `JARVIX-OS\components\meshcore\meck_emoji_14.c:177` `0x49,0xfe,0xaa,0xfe,0x06,0xd5,0x46,0x83,0xca,0x8b,0x2b,0x9c,0x0a,0x94,0x0a,0x94,0x2b,0x9c,0xca,0x93,`

### synchronization (169 matches)
- `JARVIX-OS\main\i2s_loopback_benchmark.c:72` `static SemaphoreHandle_t ring_lock;`
- `JARVIX-OS\components\audio\audio_capture.c:43` `static portMUX_TYPE running_mux = portMUX_INITIALIZER_UNLOCKED;`
- `JARVIX-OS\components\audio\audio_ref_buffer.c:22` `static SemaphoreHandle_t mutex = NULL;`

### task_pinning (43 matches)
- `JARVIX-OS\main\i2s_loopback_benchmark.c:9` `*   core 0: DMA + audio feed`
- `JARVIX-OS\components\audio\audio_capture.c:20` `#define FEED_TASK_CORE        0   // Core 0 for real-time`

### task_priority (26 matches)
- `JARVIX-OS\components\audio\audio_capture.c:19` `#define FEED_TASK_PRIORITY    6   // High priority for I2S reading`
- `JARVIX-OS\components\audio\tts_player.c:20` `#define TASK_PRIORITY        5`
- `JARVIX-OS\components\private_library\app_video.c:26` `#define VIDEO_TASK_PRIORITY             (4)`
- `JARVIX-OS\components\sdio_watchdog\sdio_watchdog.c:313` `/* Priority 5 — below SDIO, LoRa, LVGL but above idle */`
- `JARVIX-OS\components\opus\src\celt_decoder.c:1069` `fine_quant, fine_priority, C, LM, dec, 0, 0, 0);`
- `JARVIX-OS\components\opus\src\celt_encoder.c:2200` `fine_quant, fine_priority, C, LM, enc, 1, st->lastCodedBands, signalBandwidth);`
- `JARVIX-OS\components\opus\src\rate.c:495` `fine_priority[j] = 1;`

### timestamp (437 matches)
- `JARVIX-OS\main\i2s_loopback_benchmark.c:219` `int64_t t0 = esp_timer_get_time();`
- `JARVIX-OS\components\lora_scanner\lora_scanner.c:224` `uint32_t window_start = xTaskGetTickCount() * portTICK_PERIOD_MS;`

### transport_queue (13 matches)
- `JARVIX-OS\components\audio\tts_player.c:96` `opus_queue = xQueueCreate(OPUS_QUEUE_LEN, sizeof(opus_packet_t));`
- `JARVIX-OS\components\audio\voice_pipeline.c:214` `cmd_queue = xQueueCreate(10, sizeof(pipeline_cmd_t));`
- `JARVIX-OS\components\lora_scanner\lora_scanner.c:328` `evt_queue  = xQueueCreate(32, sizeof(pkt_event_t));`
- `JARVIX-OS\components\chmorgan__esp-audio-player\test\audio_player_test.c:183` `event_queue = xQueueCreate(1, sizeof(audio_player_callback_event_t));`
- `JARVIX-OS\components\chmorgan__esp-audio-player\audio_player.cpp:538` `instance.event_queue = xQueueCreate(4, sizeof(audio_player_event_t));`
- `JARVIX-OS\components\meshcore\MeckUI.cpp:13151` `(unsigned)s.curr_tx_queue_len,`
- `JARVIX-OS\components\meshcore\meshcore_src\StaticPoolPacketManager.cpp:71` `StaticPoolPacketManager::StaticPoolPacketManager(int pool_size): unused(pool_size), send_queue(pool_`

### udp (2 matches)
- `JARVIX-OS\components\RadioLib\src\protocols\Pager\Pager.cpp:64` `int16_t PagerClient::sendTone(uint32_t addr) {`
- `JARVIX-OS\components\RadioLib\src\protocols\Pager\Pager.h:87` `int16_t sendTone(uint32_t addr);`

### vad_detection (20 matches)
- `JARVIX-OS\components\audio\audio_capture.c:134` `int vad_state_prev = -1;`
- `JARVIX-OS\components\opus\src\init_encoder.c:59` `ret += silk_VAD_Init( &psEnc->sCmn.sVAD );`
- `JARVIX-OS\components\opus\src\VAD.c:37` `silk_VAD_state              *psSilk_VAD         /* I/O  Pointer to Silk VAD state                   `

### wake_word (1 matches)
- `JARVIX-OS\components\audio\audio_capture.c:150` `if (res->wakeup_state == WAKENET_DETECTED) {`

### watchdog (39 matches)
- `JARVIX-OS\main\i2s_loopback_benchmark.c:410` `/* Main task exits — watchdog will keep running */`
- `JARVIX-OS\components\sdio_watchdog\sdio_watchdog.c:2` `* SDIO Error Recovery Watchdog — Version 2`

### websocket (43 matches)
- `JARVIX-OS\components\audio\ha_client.c:3` `* WebSocket streaming to Home Assistant / Server`

### wifi_power_save (1 matches)
- `JARVIX-OS\components\audio\wifi_manager.c:130` `ESP_ERROR_CHECK(esp_wifi_set_ps(WIFI_PS_NONE));`

### wifi_remote (4 matches)
- `JARVIX-OS\components\audio\wifi_manager.c:3` `* ESP32-C6 coprocessor via SDIO (esp_wifi_remote)`
- `JARVIX-OS\components\meshcore\MeckAudio.cpp:15` `* version that conflicted with LilyGo's pinned esp_hosted / esp_wifi_remote.`
- `JARVIX-OS\components\audio\wifi_manager.h:3` `* ESP32-C6 coprocessor via SDIO (esp_wifi_remote)`