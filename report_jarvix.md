# Rapport d'Analyse: JARVIX-OS (Notre Projet)
**Projet:** `jarvix`

## Statistiques
- Fichiers scannes: 153
- Fichiers avec matches: 86
- Lignes totales: 171561
- Matches total: 3565

## Distribution par Categorie
- **mesh**: 2825 ??????????????????????????????????????????????????
- **timing**: 244 ??????????????????????????????????????????????????
- **rtos**: 200 ??????????????????????????????????????????????????
- **audio**: 93 ??????????????????????????????????????????????????
- **transport**: 89 ??????????????????????????????????????????????????
- **memory**: 61 ??????????????????????????????????????????????????
- **network**: 53 ??????????????????????????????????????????????????

## ??  Findings Critiques (CRITICAL)
- `JARVIX-OS\components\audio\audio_capture.c:74` [memory_placement] `int16_t *mic_buff = heap_caps_malloc(I2S_READ_LEN * sizeof(int16_t), MALLOC_CAP_DMA);`
- `JARVIX-OS\components\audio\audio_capture.c:75` [memory_placement] `int16_t *ref_buff = heap_caps_malloc(I2S_READ_LEN * sizeof(int16_t), MALLOC_CAP_DMA);`
- `JARVIX-OS\components\audio\audio_capture.c:76` [memory_placement] `int16_t *afe_buff = heap_caps_malloc(I2S_READ_LEN * 2 * sizeof(int16_t), MALLOC_CAP_DMA);`
- `JARVIX-OS\components\audio\audio_ref_buffer.c:31` [memory_placement] `ring_buf = heap_caps_malloc(size, MALLOC_CAP_DMA | MALLOC_CAP_8BIT);`
- `JARVIX-OS\components\audio\wifi_manager.c:3` [wifi_remote] `* ESP32-C6 coprocessor via SDIO (esp_wifi_remote)`
- `JARVIX-OS\components\audio\wifi_manager.c:10` [wifi_remote] `#include "esp_wifi_remote.h"`
- `JARVIX-OS\components\chmorgan__esp-audio-player\test\audio_player_test.c:224` [flow_control] `expected_event = AUDIO_PLAYER_CALLBACK_EVENT_PAUSE;`
- `JARVIX-OS\components\chmorgan__esp-audio-player\test\audio_player_test.c:225` [flow_control] `ret = audio_player_pause();`
- `JARVIX-OS\components\chmorgan__esp-audio-player\test\audio_player_test.c:228` [flow_control] `// wait for paused event to arrive`
- `JARVIX-OS\components\chmorgan__esp-audio-player\test\audio_player_test.c:232` [flow_control] `TEST_ASSERT_EQUAL(state, AUDIO_PLAYER_STATE_PAUSE);`
- `JARVIX-OS\components\chmorgan__esp-audio-player\test\audio_player_test.c:241` [flow_control] `// wait for paused event to arrive`
- `JARVIX-OS\components\chmorgan__esp-audio-player\audio_player.cpp:46` [flow_control] `AUDIO_PLAYER_REQUEST_PAUSE,              /**< pause playback */`
- `JARVIX-OS\components\chmorgan__esp-audio-player\audio_player.cpp:47` [flow_control] `AUDIO_PLAYER_REQUEST_RESUME,             /**< resumed paused playback */`
- `JARVIX-OS\components\chmorgan__esp-audio-player\audio_player.cpp:131` [flow_control] `case AUDIO_PLAYER_CALLBACK_EVENT_PAUSE:`
- `JARVIX-OS\components\chmorgan__esp-audio-player\audio_player.cpp:132` [flow_control] `return "AUDIO_PLAYER_CALLBACK_EVENT_PAUSE";`
- `JARVIX-OS\components\chmorgan__esp-audio-player\audio_player.cpp:151` [flow_control] `case AUDIO_PLAYER_STATE_PAUSE:`
- `JARVIX-OS\components\chmorgan__esp-audio-player\audio_player.cpp:152` [flow_control] `event = AUDIO_PLAYER_CALLBACK_EVENT_PAUSE;`
- `JARVIX-OS\components\chmorgan__esp-audio-player\audio_player.cpp:284` [flow_control] `if (AUDIO_PLAYER_REQUEST_PAUSE == audio_event.type) {`
- `JARVIX-OS\components\chmorgan__esp-audio-player\audio_player.cpp:285` [flow_control] `// receive the pause event to take it off of the queue`
- `JARVIX-OS\components\chmorgan__esp-audio-player\audio_player.cpp:288` [flow_control] `set_state(i, AUDIO_PLAYER_STATE_PAUSE);`
- `JARVIX-OS\components\chmorgan__esp-audio-player\audio_player.cpp:486` [flow_control] `esp_err_t audio_player_pause(void)`
- `JARVIX-OS\components\chmorgan__esp-audio-player\audio_player.cpp:489` [flow_control] `audio_player_event_t event = { .type = AUDIO_PLAYER_REQUEST_PAUSE, .fp = NULL };`
- `JARVIX-OS\components\meshcore\MeckAudio.cpp:118` [flow_control] `* This also distinguishes a prepared-but-unstarted file (state PAUSED)`
- `JARVIX-OS\components\meshcore\MeckAudio.cpp:119` [flow_control] `* from a genuine mid-file pause (state PAUSED, g_prepared false) so the`
- `JARVIX-OS\components\meshcore\MeckAudio.cpp:127` [flow_control] `* is actually PLAYING/PAUSED, so it cannot leak onto a later real EOF. */`
- `JARVIX-OS\components\meshcore\MeckAudio.cpp:422` [flow_control] `case AUDIO_PLAYER_CALLBACK_EVENT_PAUSE:`
- `JARVIX-OS\components\meshcore\MeckAudio.cpp:424` [flow_control] `g_state = MECK_AUDIO_STATE_PAUSED;`
- `JARVIX-OS\components\meshcore\MeckAudio.cpp:470` [flow_control] `* file that the user opened or seeked-while-paused but did not start).`
- `JARVIX-OS\components\meshcore\MeckAudio.cpp:486` [flow_control] `* state, but do NOT hand it to chmorgan. Leaves the player in PAUSED with`
- `JARVIX-OS\components\meshcore\MeckAudio.cpp:554` [flow_control] `set_state(MECK_AUDIO_STATE_PAUSED);`

## Detail par Sous-systeme

### afe_pipeline (7 matches)
- `JARVIX-OS\components\audio\audio_capture.c:109` `if (afe_handle && afe_handle->feed) {`

### codec_init (6 matches)
- `JARVIX-OS\components\meshcore\es8311.cpp:5` `* same I2S channel LilyGo's ES8311_Init() configured at boot, sharing the`

### encryption (58 matches)
- `JARVIX-OS\components\meshcore\meshcore_src\Mesh.cpp:466` `len += Utils::encryptThenMAC(secret, &packet->payload[len], data, data_len);`
- `JARVIX-OS\components\meshcore\meshcore_src\Utils.cpp:2` `#include <AES.h>`

### flow_control (72 matches)
- `JARVIX-OS\components\chmorgan__esp-audio-player\test\audio_player_test.c:224` `expected_event = AUDIO_PLAYER_CALLBACK_EVENT_PAUSE;`
- `JARVIX-OS\components\chmorgan__esp-audio-player\audio_player.cpp:46` `AUDIO_PLAYER_REQUEST_PAUSE,              /**< pause playback */`

### i2s_capture (7 matches)
- `JARVIX-OS\components\audio\audio_capture.c:24` `#define I2S_READ_LEN          512 // Samples per read (32ms @ 16kHz)`

### i2s_driver (3 matches)
- `JARVIX-OS\components\chmorgan__esp-audio-player\test\audio_player_test.c:130` `ESP_ERROR_CHECK(i2s_channel_init_std_mode(*tx_channel, p_i2s_cfg));`

### i2s_playback (11 matches)
- `JARVIX-OS\components\audio\audio_capture.c:211` `bsp_extra_i2s_write_register_callback(audio_ref_buffer_write);`
- `JARVIX-OS\components\chmorgan__esp-audio-player\test\audio_player_test.c:70` `static esp_err_t bsp_i2s_write(void * audio_buffer, size_t len, size_t *bytes_written, uint32_t time`
- `JARVIX-OS\components\meshcore\es8311.cpp:102` `esp_err_t meck_audio_i2s_write(void *audio_buffer, size_t len,`
- `JARVIX-OS\components\meshcore\MeckAudio.cpp:75` `esp_err_t meck_audio_i2s_write(void *buf, size_t len,`

### jitter_buffer (2 matches)
- `JARVIX-OS\components\meshcore\MeckUI.cpp:9658` `// height in normal use, but suppressing the bar guarantees no jitter`

### lora_radio (125 matches)
- `JARVIX-OS\components\lora_scanner\lora_scanner.c:5` `*   L1 PHYSICAL  — SX1262 radio profile (one at a time)`
- `JARVIX-OS\components\meshcore\MeckUI.cpp:403` `// Noise floor display cache. The estimator itself lives in P4SX1262Radio`
- `JARVIX-OS\components\meshcore\target.cpp:5` `* (XL9535, SX1262, SPI buses, etc.) at file scope as `auto` declarations`

### memory_placement (5 matches)
- `JARVIX-OS\components\audio\audio_capture.c:74` `int16_t *mic_buff = heap_caps_malloc(I2S_READ_LEN * sizeof(int16_t), MALLOC_CAP_DMA);`
- `JARVIX-OS\components\audio\audio_ref_buffer.c:31` `ring_buf = heap_caps_malloc(size, MALLOC_CAP_DMA | MALLOC_CAP_8BIT);`
- `JARVIX-OS\components\private_library\radiolib_bridge_driver.cpp:17` `void IRAM_ATTR Interrupt_Callback_Template(void *arg)`

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

### psram_usage (56 matches)
- `JARVIX-OS\main\main.cpp:131` `// 8. Tâche Lua (Core 1 - Isolation Heap/PSRAM)`
- `JARVIX-OS\components\meshcore\es8311.cpp:219` `*   3. Loop: meck_audio_mic_read(buf, len) into PSRAM buffer`
- `JARVIX-OS\components\meshcore\MeckAudio.cpp:620` `* stack_size vs stack_in_psram), adjust here. */`
- `JARVIX-OS\components\meshcore\MeckMapScreen.cpp:99` `// still a modest PSRAM cost for the widget structs themselves`
- `JARVIX-OS\components\meshcore\MeckUI.cpp:628` `// are allocated lazily from PSRAM on first message touching that contact,`

### ring_buffer (14 matches)
- `JARVIX-OS\components\audio\audio_ref_buffer.c:18` `static uint8_t *ring_buf = NULL;`

### routing (92 matches)
- `JARVIX-OS\components\meshcore\MeckUI.cpp:5477` `mesh->sendFlood(adv);`
- `JARVIX-OS\components\meshcore\meck_app.cpp:48` `// marks every outgoing packet in the seen-table at sendFlood time, which`

### sample_rate_config (33 matches)
- `JARVIX-OS\components\chmorgan__esp-audio-player\test\audio_player_test.c:60` `#define BSP_I2S_DUPLEX_MONO_CFG(_sample_rate)                                                       `
- `JARVIX-OS\components\chmorgan__esp-audio-player\audio_mp3.cpp:147` `pData->fmt.sample_rate = frame_info.samprate;`
- `JARVIX-OS\components\chmorgan__esp-audio-player\audio_player.cpp:362` `if ((i2s_format.sample_rate != i->output.fmt.sample_rate) ||`
- `JARVIX-OS\components\chmorgan__esp-audio-player\audio_wav.cpp:45` `LOGI_2("sample_rate=%d, channels=%d, bps=%d",`
- `JARVIX-OS\components\meshcore\es8311.cpp:231` `bool meck_audio_mic_start(uint32_t sample_rate)`

### sync_word (2550 matches)
- `JARVIX-OS\components\lora_scanner\lora_scanner.c:30` `[RADIO_PROF_MESHTASTIC_LF] = {12, 500, 0x2B, 868100000, "MeshtLF"},`
- `JARVIX-OS\components\meshcore\meck_emoji_14.c:177` `0x49,0xfe,0xaa,0xfe,0x06,0xd5,0x46,0x83,0xca,0x8b,0x2b,0x9c,0x0a,0x94,0x0a,0x94,0x2b,0x9c,0xca,0x93,`

### synchronization (149 matches)
- `JARVIX-OS\components\audio\audio_capture.c:43` `static portMUX_TYPE running_mux = portMUX_INITIALIZER_UNLOCKED;`
- `JARVIX-OS\components\audio\audio_ref_buffer.c:22` `static SemaphoreHandle_t mutex = NULL;`
- `JARVIX-OS\components\lora_scanner\lora_scanner.c:52` `static SemaphoreHandle_t  feat_mutex;`

### task_pinning (27 matches)
- `JARVIX-OS\components\audio\audio_capture.c:20` `#define FEED_TASK_CORE        0   // Core 0 for real-time`
- `JARVIX-OS\components\audio\voice_pipeline.c:237` `BaseType_t ret = xTaskCreatePinnedToCore(`

### task_priority (15 matches)
- `JARVIX-OS\components\audio\audio_capture.c:19` `#define FEED_TASK_PRIORITY    6   // High priority for I2S reading`
- `JARVIX-OS\components\private_library\app_video.c:26` `#define VIDEO_TASK_PRIORITY             (4)`
- `JARVIX-OS\components\chmorgan__esp-audio-player\test\audio_player_test.c:103` `.priority = 0,`
- `JARVIX-OS\components\meshcore\MeckAudio.cpp:617` `cfg.priority     = 5;`
- `JARVIX-OS\components\meshcore\meshcore_src\Dispatcher.cpp:267` `uint8_t priority = (action >> 24) - 1;`
- `JARVIX-OS\components\meshcore\meshcore_src\Mesh.cpp:61` `return ACTION_RETRANSMIT_DELAYED(5, d);  // schedule with priority 5 (for now), maybe make configura`
- `JARVIX-OS\components\meshcore\meshcore_src\StaticPoolPacketManager.cpp:60` `bool PacketQueue::add(mesh::Packet* packet, uint8_t priority, uint32_t scheduled_for) {`

### timestamp (244 matches)
- `JARVIX-OS\components\lora_scanner\lora_scanner.c:216` `uint32_t window_start = xTaskGetTickCount() * portTICK_PERIOD_MS;`
- `JARVIX-OS\components\meshcore\MeckUI.cpp:494` `static uint32_t   g_delete_confirm_until = 0;   // millis deadline for tap-again`

### transport_queue (12 matches)
- `JARVIX-OS\components\audio\voice_pipeline.c:214` `cmd_queue = xQueueCreate(10, sizeof(pipeline_cmd_t));`
- `JARVIX-OS\components\lora_scanner\lora_scanner.c:287` `evt_queue  = xQueueCreate(32, sizeof(pkt_event_t));`
- `JARVIX-OS\components\chmorgan__esp-audio-player\test\audio_player_test.c:183` `event_queue = xQueueCreate(1, sizeof(audio_player_callback_event_t));`
- `JARVIX-OS\components\chmorgan__esp-audio-player\audio_player.cpp:538` `instance.event_queue = xQueueCreate(4, sizeof(audio_player_event_t));`
- `JARVIX-OS\components\meshcore\MeckUI.cpp:13151` `(unsigned)s.curr_tx_queue_len,`
- `JARVIX-OS\components\meshcore\meshcore_src\StaticPoolPacketManager.cpp:71` `StaticPoolPacketManager::StaticPoolPacketManager(int pool_size): unused(pool_size), send_queue(pool_`
- `JARVIX-OS\components\meshcore\MeckMesh.h:131` `uint16_t curr_tx_queue_len;`

### vad_detection (9 matches)
- `JARVIX-OS\components\audio\audio_capture.c:134` `int vad_state_prev = -1;`
- `JARVIX-OS\main\main.cpp:107` `.vad_speech_threshold = 180,`
- `JARVIX-OS\components\audio\voice_pipeline.h:57` `uint32_t vad_speech_threshold;`

### wake_word (1 matches)
- `JARVIX-OS\components\audio\audio_capture.c:150` `if (res->wakeup_state == WAKENET_DETECTED) {`

### watchdog (9 matches)
- `JARVIX-OS\main\main.cpp:3` `#include "esp_task_wdt.h"`
- `JARVIX-OS\components\chmorgan__esp-audio-player\audio_mp3.cpp:63` `* and fire the task watchdog. Skip the tag header explicitly so the`
- `JARVIX-OS\components\meshcore\es8311.cpp:101` `* a stuck codec causes the task watchdog to fire after 5s. */`
- `JARVIX-OS\components\meshcore\MeckUI.cpp:11920` `// watchdog reset in esp_ipc_isr_waiting_for_finish_cmd.`
- `JARVIX-OS\components\meshcore\SerialC6WiFiInterface.cpp:104` `// to keep IDLE0 alive and prevent the task watchdog from firing.`
- `JARVIX-OS\main\memory_watchdog.h:1` `#ifndef MEMORY_WATCHDOG_H`

### websocket (43 matches)
- `JARVIX-OS\components\audio\ha_client.c:3` `* WebSocket streaming to Home Assistant / Server`

### wifi_power_save (1 matches)
- `JARVIX-OS\components\audio\wifi_manager.c:130` `ESP_ERROR_CHECK(esp_wifi_set_ps(WIFI_PS_NONE));`

### wifi_remote (4 matches)
- `JARVIX-OS\components\audio\wifi_manager.c:3` `* ESP32-C6 coprocessor via SDIO (esp_wifi_remote)`
- `JARVIX-OS\components\meshcore\MeckAudio.cpp:15` `* version that conflicted with LilyGo's pinned esp_hosted / esp_wifi_remote.`
- `JARVIX-OS\components\audio\wifi_manager.h:3` `* ESP32-C6 coprocessor via SDIO (esp_wifi_remote)`