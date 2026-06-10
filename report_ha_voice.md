# Rapport d'Analyse: Home Assistant Voice Assistant (P4+C6)
**Projet:** `ha_voice`

## Statistiques
- Fichiers scannes: 49
- Fichiers avec matches: 34
- Lignes totales: 11748
- Matches total: 769

## Distribution par Categorie
- **network**: 469 ??????????????????????????????????????????????????
- **audio**: 99 ??????????????????????????????????????????????????
- **rtos**: 92 ??????????????????????????????????????????????????
- **transport**: 56 ??????????????????????????????????????????????????
- **memory**: 33 ?????????????????????????????????
- **mesh**: 11 ???????????
- **timing**: 9 ?????????

## ??  Findings Critiques (CRITICAL)
- `Home-Assistant-MQTT-Voice-Assistant\main\audio_capture.c:49` [memory_placement] `heap_caps_get_free_size(MALLOC_CAP_INTERNAL | MALLOC_CAP_8BIT);`
- `Home-Assistant-MQTT-Voice-Assistant\main\audio_capture.c:63` [memory_placement] `MALLOC_CAP_SPIRAM | MALLOC_CAP_INTERNAL | MALLOC_CAP_8BIT);`
- `Home-Assistant-MQTT-Voice-Assistant\main\audio_capture.c:69` [memory_placement] `heap_caps_get_free_size(MALLOC_CAP_INTERNAL | MALLOC_CAP_8BIT);`
- `Home-Assistant-MQTT-Voice-Assistant\main\audio_capture.c:87` [memory_placement] `MALLOC_CAP_INTERNAL | MALLOC_CAP_8BIT);`
- `Home-Assistant-MQTT-Voice-Assistant\main\local_music_player.c:91` [flow_control] `case AUDIO_PLAYER_CALLBACK_EVENT_PAUSE:`
- `Home-Assistant-MQTT-Voice-Assistant\main\local_music_player.c:92` [flow_control] `player_state = MUSIC_STATE_PAUSED;`
- `Home-Assistant-MQTT-Voice-Assistant\main\local_music_player.c:180` [flow_control] `player_state == MUSIC_STATE_PAUSED) {`
- `Home-Assistant-MQTT-Voice-Assistant\main\local_music_player.c:214` [flow_control] `// If paused, resume`
- `Home-Assistant-MQTT-Voice-Assistant\main\local_music_player.c:215` [flow_control] `if (player_state == MUSIC_STATE_PAUSED) {`
- `Home-Assistant-MQTT-Voice-Assistant\main\local_music_player.c:283` [flow_control] `* @brief Pause playing music`
- `Home-Assistant-MQTT-Voice-Assistant\main\local_music_player.c:285` [flow_control] `esp_err_t local_music_player_pause(void) {`
- `Home-Assistant-MQTT-Voice-Assistant\main\local_music_player.c:287` [flow_control] `ESP_LOGW(TAG, "Cannot pause - not playing");`
- `Home-Assistant-MQTT-Voice-Assistant\main\local_music_player.c:293` [flow_control] `// Use audio player pause (queues pause request)`
- `Home-Assistant-MQTT-Voice-Assistant\main\local_music_player.c:294` [flow_control] `esp_err_t ret = audio_player_pause();`
- `Home-Assistant-MQTT-Voice-Assistant\main\local_music_player.c:296` [flow_control] `ESP_LOGE(TAG, "Failed to pause audio player");`
- `Home-Assistant-MQTT-Voice-Assistant\main\local_music_player.c:300` [flow_control] `player_state = MUSIC_STATE_PAUSED;`
- `Home-Assistant-MQTT-Voice-Assistant\main\local_music_player.c:313` [flow_control] `if (!player_initialized || player_state != MUSIC_STATE_PAUSED) {`
- `Home-Assistant-MQTT-Voice-Assistant\main\local_music_player.c:314` [flow_control] `ESP_LOGW(TAG, "Cannot resume - not paused");`
- `Home-Assistant-MQTT-Voice-Assistant\main\main.c:144` [flow_control] `case MUSIC_STATE_PAUSED:`
- `Home-Assistant-MQTT-Voice-Assistant\main\main.c:145` [flow_control] `return "PAUSED";`
- `Home-Assistant-MQTT-Voice-Assistant\main\main.c:739` [flow_control] `(state == MUSIC_STATE_PLAYING || state == MUSIC_STATE_PAUSED);`
- `Home-Assistant-MQTT-Voice-Assistant\main\main.c:746` [flow_control] `} else if (state == MUSIC_STATE_PAUSED) {`
- `Home-Assistant-MQTT-Voice-Assistant\main\main.c:747` [flow_control] `oled_state = OLED_MUSIC_PAUSED;`
- `Home-Assistant-MQTT-Voice-Assistant\main\mqtt_ha.c:54` [flow_control] `"homeassistant/button/esp32p4_voice_assistant/music_pause/config",`
- `Home-Assistant-MQTT-Voice-Assistant\main\oled_status.c:575` [flow_control] `case OLED_MUSIC_PAUSED: mus = "PAU"; break;`
- `Home-Assistant-MQTT-Voice-Assistant\main\ota_update.c:333` [memory_placement] `(unsigned)heap_caps_get_free_size(MALLOC_CAP_INTERNAL | MALLOC_CAP_8BIT));`
- `Home-Assistant-MQTT-Voice-Assistant\main\ota_update.c:339` [memory_placement] `MALLOC_CAP_INTERNAL | MALLOC_CAP_8BIT);`
- `Home-Assistant-MQTT-Voice-Assistant\main\voice_pipeline.c:81` [flow_control] `static bool music_paused_for_tts = false;`
- `Home-Assistant-MQTT-Voice-Assistant\main\voice_pipeline.c:376` [flow_control] `local_music_player_get_state() == MUSIC_STATE_PAUSED)) {`
- `Home-Assistant-MQTT-Voice-Assistant\main\voice_pipeline.c:648` [flow_control] `if (music_paused_for_tts) {`

## Detail par Sous-systeme

### afe_pipeline (20 matches)
- `Home-Assistant-MQTT-Voice-Assistant\main\audio_capture.c:11` `#include "esp_afe_sr_iface.h"`

### codec_init (1 matches)
- `Home-Assistant-MQTT-Voice-Assistant\common_components\espressif__esp32_p4_function_ev_board\include\bsp\esp32_p4_function_ev_board.h:87` `*  - Codec ES8311 (configuration only)`

### encryption (9 matches)
- `Home-Assistant-MQTT-Voice-Assistant\main\voice_pipeline.c:1317` `if (strcmp(word, "jedanaest") == 0)`

### ethernet (37 matches)
- `Home-Assistant-MQTT-Voice-Assistant\main\network_manager.c:12` `#include "esp_eth.h"`

### flow_control (50 matches)
- `Home-Assistant-MQTT-Voice-Assistant\main\local_music_player.c:91` `case AUDIO_PLAYER_CALLBACK_EVENT_PAUSE:`

### i2s_capture (10 matches)
- `Home-Assistant-MQTT-Voice-Assistant\main\audio_capture.c:31` `#define I2S_READ_LEN 512`
- `Home-Assistant-MQTT-Voice-Assistant\common_components\bsp_extra\src\bsp_board_extra.c:99` `esp_err_t bsp_extra_i2s_read(void *audio_buffer, size_t len, size_t *bytes_read, uint32_t timeout_ms`
- `Home-Assistant-MQTT-Voice-Assistant\common_components\bsp_extra\include\bsp_board_extra.h:133` `esp_err_t bsp_extra_i2s_read(void *audio_buffer, size_t len, size_t *bytes_read, uint32_t timeout_ms`

### i2s_driver (2 matches)
- `Home-Assistant-MQTT-Voice-Assistant\common_components\espressif__esp32_p4_function_ev_board\esp32_p4_function_ev_board.c:233` `ESP_ERROR_CHECK(i2s_channel_init_std_mode(i2s_tx_chan, p_i2s_cfg));`

### i2s_playback (15 matches)
- `Home-Assistant-MQTT-Voice-Assistant\main\audio_capture.c:331` `bsp_extra_i2s_write_register_callback(audio_ref_buffer_write);`
- `Home-Assistant-MQTT-Voice-Assistant\main\beep_tone.c:88` `ret = bsp_extra_i2s_write(pcm_buffer, bytes_to_write, &bytes_written, 1000);`
- `Home-Assistant-MQTT-Voice-Assistant\main\tts_player.c:134` `bsp_extra_i2s_write(pcm_buffer, pcm_bytes, &bytes_written, 0);`
- `Home-Assistant-MQTT-Voice-Assistant\main\wake_prompt.c:142` `bsp_extra_i2s_write(pcm_buffer, pcm_bytes, &bytes_written, 0);`
- `Home-Assistant-MQTT-Voice-Assistant\common_components\bsp_extra\src\bsp_board_extra.c:44` `static i2s_write_callback_t i2s_write_cb = NULL;`

### memory_placement (6 matches)
- `Home-Assistant-MQTT-Voice-Assistant\main\audio_capture.c:49` `heap_caps_get_free_size(MALLOC_CAP_INTERNAL | MALLOC_CAP_8BIT);`
- `Home-Assistant-MQTT-Voice-Assistant\main\ota_update.c:333` `(unsigned)heap_caps_get_free_size(MALLOC_CAP_INTERNAL | MALLOC_CAP_8BIT));`

### mqtt (389 matches)
- `Home-Assistant-MQTT-Voice-Assistant\main\main.c:28` `#include "mqtt_ha.h"`

### psram_usage (27 matches)
- `Home-Assistant-MQTT-Voice-Assistant\main\audio_capture.c:50` `size_t free_psram =`

### ring_buffer (8 matches)
- `Home-Assistant-MQTT-Voice-Assistant\main\audio_ref_buffer.c:3` `#include "freertos/ringbuf.h"`

### sample_rate_config (13 matches)
- `Home-Assistant-MQTT-Voice-Assistant\main\beep_tone.c:13` `#define BEEP_SAMPLE_RATE 16000 // 16kHz sample rate`
- `Home-Assistant-MQTT-Voice-Assistant\main\ha_client.c:634` `cJSON_AddNumberToObject(input, "sample_rate", 16000);`
- `Home-Assistant-MQTT-Voice-Assistant\common_components\espressif__esp32_p4_function_ev_board\esp32_p4_function_ev_board.c:70` `#define BSP_I2S_DUPLEX_MONO_CFG(_sample_rate)                                                       `
- `Home-Assistant-MQTT-Voice-Assistant\common_components\bsp_extra\src\bsp_board_extra.c:159` `.sample_rate = rate,`

### spi_bridge (1 matches)
- `Home-Assistant-MQTT-Voice-Assistant\main\main.c:19` `#include "driver/sdspi_host.h"`

### sync_word (2 matches)
- `Home-Assistant-MQTT-Voice-Assistant\main\tts_player.c:96` `int offset = MP3FindSyncWord(read_ptr, bytes_left);`
- `Home-Assistant-MQTT-Voice-Assistant\main\wake_prompt.c:113` `int offset = MP3FindSyncWord(read_ptr, bytes_left);`

### synchronization (39 matches)
- `Home-Assistant-MQTT-Voice-Assistant\main\audio_capture.c:147` `// Thread-safe is_running flag protected by spinlock`
- `Home-Assistant-MQTT-Voice-Assistant\main\ha_client.c:38` `// Callbacks - protected by spinlock for thread safety`
- `Home-Assistant-MQTT-Voice-Assistant\main\oled_status.c:59` `static SemaphoreHandle_t status_mutex = NULL;`
- `Home-Assistant-MQTT-Voice-Assistant\main\timer_manager.c:20` `static SemaphoreHandle_t timer_mutex = NULL;`

### task_pinning (5 matches)
- `Home-Assistant-MQTT-Voice-Assistant\main\audio_capture.c:28` `#define AFE_TASK_CORE 1`
- `Home-Assistant-MQTT-Voice-Assistant\main\sys_diag.c:143` `.idle_core_mask = (1 << portNUM_PROCESSORS) - 1, // Monitor idle tasks too`

### task_priority (4 matches)
- `Home-Assistant-MQTT-Voice-Assistant\main\audio_capture.c:27` `#define AFE_TASK_PRIORITY 5`
- `Home-Assistant-MQTT-Voice-Assistant\main\ota_update.c:22` `#define OTA_TASK_PRIORITY 2`
- `Home-Assistant-MQTT-Voice-Assistant\common_components\bsp_extra\src\bsp_board_extra.c:330` `.priority = 5`

### timestamp (9 matches)
- `Home-Assistant-MQTT-Voice-Assistant\main\main.c:202` `(unsigned long long)(esp_timer_get_time() / 1000000ULL));`
- `Home-Assistant-MQTT-Voice-Assistant\main\oled_status.c:398` `uint64_t uptime = (uint64_t)(esp_timer_get_time() / 1000000ULL);`
- `Home-Assistant-MQTT-Voice-Assistant\main\timer_manager.c:291` `TickType_t last_wake = xTaskGetTickCount();`
- `Home-Assistant-MQTT-Voice-Assistant\main\webserial.c:294` `ip_str, esp_timer_get_time() / 1000000, voice_pipeline_is_running());`
- `Home-Assistant-MQTT-Voice-Assistant\main\beep_tone.h:23` `* @param duration Duration of the beep in milliseconds (e.g., 100, 150, 200)`

### transport_queue (2 matches)
- `Home-Assistant-MQTT-Voice-Assistant\main\tts_player.c:252` `audio_queue = xQueueCreate(TTS_QUEUE_SIZE, sizeof(audio_chunk_t));`
- `Home-Assistant-MQTT-Voice-Assistant\main\voice_pipeline.c:174` `pipeline_cmd_queue = xQueueCreate(10, sizeof(pipeline_cmd_t));`

### vad_detection (27 matches)
- `Home-Assistant-MQTT-Voice-Assistant\main\audio_capture.c:239` `int vad_state_prev = -1;`
- `Home-Assistant-MQTT-Voice-Assistant\main\main.c:551` `static void mqtt_vad_silence_callback(const char *entity_id,`

### wake_word (3 matches)
- `Home-Assistant-MQTT-Voice-Assistant\main\audio_capture.c:252` `if (res->wakeup_state == WAKENET_DETECTED) {`
- `Home-Assistant-MQTT-Voice-Assistant\common_components\bsp_extra\include\bsp_board_extra.h:25` `#define CODEC_DEFAULT_CHANNEL               (1)     // MONO - required by ESP-SR WakeNet`

### watchdog (44 matches)
- `Home-Assistant-MQTT-Voice-Assistant\main\audio_capture.c:179` `sys_diag_wdt_add(); // Monitor`
- `Home-Assistant-MQTT-Voice-Assistant\main\main.c:838` `// 4. Watchdog Init (30 seconds timeout)`

### websocket (43 matches)
- `Home-Assistant-MQTT-Voice-Assistant\main\ha_client.c:3` `* WebSocket client for HA Assist Pipeline`

### wifi_remote (3 matches)
- `Home-Assistant-MQTT-Voice-Assistant\main\wifi_manager.c:3` `* Uses ESP32-C6 coprocessor via SDIO (esp_wifi_remote)`
- `Home-Assistant-MQTT-Voice-Assistant\main\wifi_manager.h:20` `* via SDIO interface (esp_wifi_remote). It will block until connection`