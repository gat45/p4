# Rapport d'Analyse: ESP-ADF (Audio Framework)
**Projet:** `esp_adf`

## Statistiques
- Fichiers scannes: 907
- Fichiers avec matches: 349
- Lignes totales: 105513
- Matches total: 5578

## Distribution par Categorie
- **mesh**: 3374 ??????????????????????????????????????????????????
- **audio**: 1561 ??????????????????????????????????????????????????
- **transport**: 325 ??????????????????????????????????????????????????
- **memory**: 123 ??????????????????????????????????????????????????
- **rtos**: 95 ??????????????????????????????????????????????????
- **timing**: 66 ??????????????????????????????????????????????????
- **network**: 34 ??????????????????????????????????

## ??  Findings Critiques (CRITICAL)
- `esp-adf\components\audio_pipeline\audio_element.c:133` [flow_control] `const static int PAUSED_BIT = BIT5;`
- `esp-adf\components\audio_pipeline\audio_element.c:278` [flow_control] `if (el->state != AEL_STATE_INIT && el->state != AEL_STATE_RUNNING && el->state != AEL_STATE_PAUSED) {`
- `esp-adf\components\audio_pipeline\audio_element.c:313` [flow_control] `case AEL_MSG_CMD_PAUSE:`
- `esp-adf\components\audio_pipeline\audio_element.c:314` [flow_control] `el->state = AEL_STATE_PAUSED;`
- `esp-adf\components\audio_pipeline\audio_element.c:317` [flow_control] `audio_element_report_status(el, AEL_STATUS_STATE_PAUSED);`
- `esp-adf\components\audio_pipeline\audio_element.c:319` [flow_control] `ESP_LOGI(TAG, "[%s] AEL_MSG_CMD_PAUSE", el->tag);`
- `esp-adf\components\audio_pipeline\audio_element.c:320` [flow_control] `xEventGroupSetBits(el->state_event, PAUSED_BIT);`
- `esp-adf\components\audio_pipeline\audio_element.c:1168` [flow_control] `esp_err_t audio_element_pause(audio_element_handle_t el)`
- `esp-adf\components\audio_pipeline\audio_element.c:1171` [flow_control] `ESP_LOGW(TAG, "[%s] Element has not create when AUDIO_ELEMENT_PAUSE", el->tag);`
- `esp-adf\components\audio_pipeline\audio_element.c:1174` [flow_control] `if ((el->state >= AEL_STATE_PAUSED)) {`
- `esp-adf\components\audio_pipeline\audio_element.c:1175` [flow_control] `audio_element_force_set_state(el, AEL_STATE_PAUSED);`
- `esp-adf\components\audio_pipeline\audio_element.c:1176` [flow_control] `ESP_LOGD(TAG, "[%s] Element already paused, state:%d", el->tag, el->state);`
- `esp-adf\components\audio_pipeline\audio_element.c:1179` [flow_control] `xEventGroupClearBits(el->state_event, PAUSED_BIT);`
- `esp-adf\components\audio_pipeline\audio_element.c:1182` [flow_control] `audio_element_force_set_state(el, AEL_STATE_PAUSED);`
- `esp-adf\components\audio_pipeline\audio_element.c:1185` [flow_control] `if (audio_element_cmd_send(el, AEL_MSG_CMD_PAUSE) != ESP_OK) {`
- `esp-adf\components\audio_pipeline\audio_element.c:1186` [flow_control] `ESP_LOGE(TAG, "[%s] Element send cmd error when AUDIO_ELEMENT_PAUSE", el->tag);`
- `esp-adf\components\audio_pipeline\audio_element.c:1189` [flow_control] `EventBits_t uxBits = xEventGroupWaitBits(el->state_event, PAUSED_BIT, false, true, DEFAULT_MAX_WAIT_TIME);`
- `esp-adf\components\audio_pipeline\audio_element.c:1191` [flow_control] `if (uxBits & PAUSED_BIT) {`
- `esp-adf\components\audio_pipeline\audio_element.c:1251` [flow_control] `if (el->state == AEL_STATE_PAUSED) {`
- `esp-adf\components\audio_pipeline\audio_pipeline.c:328` [flow_control] `esp_err_t audio_pipeline_pause(audio_pipeline_handle_t pipeline)`
- `esp-adf\components\audio_pipeline\audio_pipeline.c:335` [flow_control] `ESP_LOGD(TAG, "pause [%s]  %p", audio_element_get_tag(el_item->el), el_item->el);`
- `esp-adf\components\audio_pipeline\audio_pipeline.c:336` [flow_control] `audio_element_pause(el_item->el);`
- `esp-adf\components\audio_pipeline\audio_pipeline.c:692` [flow_control] `} else if (status == AEL_STATUS_STATE_PAUSED) {`
- `esp-adf\components\audio_pipeline\audio_pipeline.c:696` [flow_control] `ESP_LOGW(TAG, "Check AEL PAUSED, pl:%p, el:%p, tag:%16s, state:%d, wanted:%d", pipeline, item->el,`
- `esp-adf\components\audio_pipeline\audio_pipeline.c:834` [flow_control] `|| (audio_element_get_state(el_item->el) == AEL_STATE_PAUSED)`
- `esp-adf\components\audio_sal\audio_mem.c:157` [memory_placement] `data = heap_caps_calloc_prefer(n, size, 2,  MALLOC_CAP_DEFAULT | MALLOC_CAP_INTERNAL | MALLOC_CAP_8BIT, MALLOC_CAP_DEFAU`
- `esp-adf\components\audio_sal\audio_mem.c:159` [memory_placement] `data = heap_caps_calloc(n, size, MALLOC_CAP_INTERNAL | MALLOC_CAP_8BIT);`
- `esp-adf\components\audio_sal\audio_mem.c:171` [memory_placement] `(int)heap_caps_get_free_size(MALLOC_CAP_INTERNAL), (int)heap_caps_get_free_size(MALLOC_CAP_INTERNAL | MALLOC_CAP_8BIT), `
- `esp-adf\components\audio_stream\fatfs_stream.c:249` [flow_control] `if (AEL_STATE_PAUSED != audio_element_get_state(self)) {`
- `esp-adf\components\audio_stream\http_stream.c:649` [flow_control] `if (AEL_STATE_PAUSED != audio_element_get_state(self)) {`

## Detail par Sous-systeme

### afe_pipeline (128 matches)
- `esp-adf\components\audio_recorder\recorder_sr.c:40` `#include "esp_afe_sr_models.h"`

### clock_source (6 matches)
- `esp-adf\components\audio_hal\test\test_audio_hal.c:54` `.use_apll = 1,`
- `esp-adf\components\esp_codec_dev\test_apps\codec_dev_test\main\test_board.c:192` `.use_apll = true,`
- `esp-adf\examples\get-started\pipeline_a2dp_sink_and_hfp\main\a2dp_sink_and_hfp_example.c:409` `i2s_cfg2.i2s_config.use_apll = false;`
- `esp-adf\components\audio_stream\include\i2s_stream.h:95` `.use_apll = true,                                                       \`

### codec_init (25 matches)
- `esp-adf\components\audio_hal\test\test_audio_hal.c:131` `audio_hal_codec_config_t es8311_cfg = AUDIO_CODEC_DEFAULT_CONFIG();`
- `esp-adf\components\audio_hal\driver\es8311\es8311.c:72` `.audio_codec_initialize = es8311_codec_init,`

### dma_buffer (21 matches)
- `esp-adf\components\audio_stream\i2s_stream.c:142` `int index = i2s->config.i2s_config.dma_buf_count;`
- `esp-adf\components\audio_hal\test\test_audio_hal.c:52` `.dma_buf_count = 3,`
- `esp-adf\components\esp_codec_dev\test_apps\codec_dev_test\main\test_board.c:190` `.dma_buf_count = 2,`
- `esp-adf\examples\advanced_examples\algorithm\main\algorithm_examples.c:153` `i2s_w_cfg.chan_cfg.dma_desc_num = 6;`

### encryption (105 matches)
- `esp-adf\components\audio_stream\http_stream.c:48` `#include "aes/esp_aes.h"`

### flow_control (239 matches)
- `esp-adf\components\audio_pipeline\audio_element.c:133` `const static int PAUSED_BIT = BIT5;`

### i2s_capture (72 matches)
- `esp-adf\components\audio_stream\i2s_stream.c:225` `static int _i2s_read(audio_element_handle_t self, char *buffer, int len, TickType_t ticks_to_wait, v`
- `esp-adf\components\audio_stream\i2s_stream_idf5.c:495` `static int _i2s_read(audio_element_handle_t self, char *buffer, int len, TickType_t ticks_to_wait, v`
- `esp-adf\components\audio_stream\test\i2s_stream_test.c:221` `TEST_ASSERT_EQUAL(ESP_OK, audio_pipeline_register(pipeline, i2s_stream_reader, "i2s_read"));`
- `esp-adf\components\esp_codec_dev\platform\audio_codec_data_i2s.c:642` `int ret = i2s_channel_read(rx_chan, data, size, &bytes_read, DEFAULT_WAIT_TIMEOUT);`

### i2s_driver (21 matches)
- `esp-adf\components\audio_stream\i2s_stream.c:172` `static esp_err_t _i2s_open(audio_element_handle_t self)`
- `esp-adf\components\audio_stream\i2s_stream_idf5.c:120` `ret |= i2s_channel_init_std_mode(i2s_key_slot[i2s->port].tx_handle, &i2s_key_slot[i2s->port].tx_std_`

### i2s_playback (152 matches)
- `esp-adf\components\audio_stream\i2s_stream.c:242` `static int _i2s_write(audio_element_handle_t self, char *buffer, int len, TickType_t ticks_to_wait, `
- `esp-adf\components\audio_stream\i2s_stream_idf5.c:469` `static esp_err_t i2s_channel_write_expand(i2s_stream_t *i2s, const char *src, size_t src_len, int sr`

### memory_placement (31 matches)
- `esp-adf\components\audio_sal\audio_mem.c:157` `data = heap_caps_calloc_prefer(n, size, 2,  MALLOC_CAP_DEFAULT | MALLOC_CAP_INTERNAL | MALLOC_CAP_8B`
- `esp-adf\components\audio_stream\pwm_stream.c:122` `pwm_data_handle_t data = heap_caps_calloc(1, sizeof(data_list_t), MALLOC_CAP_INTERNAL | MALLOC_CAP_8`

### mqtt (10 matches)
- `esp-adf\examples\korvo_du1906\components\bdsc_engine\include\auth_task.h:41` `const char *mqtt_username;`
- `esp-adf\examples\korvo_du1906\components\bdsc_engine\include\bdsc_engine.h:27` `#include "mqtt_client.h"`
- `esp-adf\examples\korvo_du1906\components\bdsc_engine\include\bdsc_profile.h:42` `char *mqtt_broker;`
- `esp-adf\examples\korvo_du1906\components\bds_light\include\bds_client_event.h:53` `EVENT_RECV_MQTT_PUSH_URL,`

### opus_decode (71 matches)
- `esp-adf\examples\advanced_examples\audio_mixer_tone\main\audio_mixer_example.c:451` `DEFAULT_ESP_OPUS_DECODER_CONFIG(),`
- `esp-adf\examples\advanced_examples\multi-room\main\multi_room.c:202` `DEFAULT_ESP_OPUS_DECODER_CONFIG(),`
- `esp-adf\examples\ai_agent\coze_ws_app\main\audio_processor.c:36` `#include "esp_opus_dec.h"`

### opus_encode (33 matches)
- `esp-adf\examples\ai_agent\coze_ws_app\main\audio_processor.c:33` `#include "esp_opus_enc.h"`

### psram_usage (92 matches)
- `esp-adf\components\audio_sal\audio_mem.c:68` `#if CONFIG_SPIRAM_BOOT_INIT`

### ring_buffer (497 matches)
- `esp-adf\components\audio_pipeline\audio_element.c:59` `ringbuf_handle_t            *rb;`

### sample_rate_config (477 matches)
- `esp-adf\components\audio_mixer\audio_mixer.c:275` `if (CHECK_OUT_OF_RANGE(config->sample_rate, SAMPLERATE_MIN, SAMPLERATE_MAX)) {`
- `esp-adf\components\audio_pipeline\audio_element.c:1444` `esp_err_t audio_element_set_music_info(audio_element_handle_t el, int sample_rates, int channels, in`
- `esp-adf\components\audio_stream\aec_stream.c:77` `ESP_LOGW(TAG, "Create AEC, handle %p, mic: %d, total_ch_num: %d, sample_rate: %d, chunk size: %d", a`
- `esp-adf\components\audio_stream\algorithm_stream.c:54` `int                           sample_rate;`

### spi_bridge (25 matches)
- `esp-adf\components\audio_hal\driver\zl38063\api_lib\vproc_common.c:23` `#define SPI_HOST_NUM SPI2_HOST`
- `esp-adf\components\esp_codec_dev\platform\audio_codec_ctrl_spi.c:41` `spi_host_device_t host_id = SPI2_HOST;`

### sync_word (3269 matches)
- `esp-adf\examples\display\music_player\main\assets\img_lv_demo_music_btn_corner_large.c:18` `0x49, 0x2b, 0x49, 0x1c, 0x49, 0x04, 0x49, 0x00, 0x49, 0x00, 0x49, 0x00, 0x49, 0x00, 0x49, 0x00, 0x49`

### synchronization (66 matches)
- `esp-adf\components\audio_pipeline\audio_element.c:109` `xSemaphoreHandle            lock;`
- `esp-adf\components\audio_pipeline\audio_pipeline.c:69` `xSemaphoreHandle            lock;`
- `esp-adf\components\audio_pipeline\ringbuf.c:43` `SemaphoreHandle_t can_read;`

### task_pinning (8 matches)
- `esp-adf\components\audio_sal\audio_sys.c:124` `percentage_time = (task_elapsed_time * 100UL) / (total_elapsed_time * portNUM_PROCESSORS);`
- `esp-adf\components\audio_sal\audio_thread.c:86` `if (xTaskCreatePinnedToCore(main_func, name, stack, arg, prio, (TASK_HANDLE_T*)p_handle, core_id) !=`
- `esp-adf\components\esp_dispatcher\audio_service.c:72` `if (pdPASS != xTaskCreatePinnedToCore(config->task_func,`
- `esp-adf\examples\display\dual_eyes\main\esp_dual_eye_ui.c:17` `#define UI_TASK_CORE          0`
- `esp-adf\examples\dueros\main\dueros_app.c:500` `xTaskCreatePinnedToCore(sys_monitor_task, "sys_monitor_task", (4 * 1024), NULL, 1, NULL, 1);`
- `esp-adf\examples\korvo_du1906\main\app_sys_tools.c:48` `xTaskCreatePinnedToCore(sys_monitor_task, "sys_monitor_task", (2 * 1024), NULL, 1, NULL, 1);`
- `esp-adf\components\audio_stream\include\aec_stream.h:31` `#define AEC_STREAM_PINNED_TO_CORE     0`
- `esp-adf\components\audio_stream\include\algorithm_stream.h:35` `#define ALGORITHM_STREAM_PINNED_TO_CORE     0`

### task_priority (19 matches)
- `esp-adf\components\audio_stream\algorithm_stream.c:147` `afe_config->afe_perferred_priority = 21;`
- `esp-adf\components\bluetooth_service\hfp_stream.c:40` `#define ESP_HFP_TASK_PRIORITY    23`
- `esp-adf\components\display_service\display_service.c:42` `#define DISPLAY_TASK_PRIORITY           5`
- `esp-adf\components\dueros_service\dueros_service.c:53` `#define DUEROS_TASK_PRIORITY        5`
- `esp-adf\components\esp_peripherals\periph_is31fl3216.c:36` `#define IS31FL3216_TASK_PRIORITY    3`
- `esp-adf\components\wifi_service\airkiss_config\airkiss_config.c:55` `#define AIRKISS_NOTIFY_TASK_PRIORITY    3`
- `esp-adf\examples\ai_agent\coze_ws_app\main\audio_processor.c:80` `#define AUDIO_RECORD_PIP_TASK_PRIORITY      (5)`
- `esp-adf\examples\ai_agent\volc_rtc\main\volc_rtc.c:306` `byte_rtc_set_params(s_volc_rtc.engine,"{\"rtc\":{\"thread\":{\"priority\":6}}}");`

### timestamp (66 matches)
- `esp-adf\components\audio_sal\audio_sys.c:62` `int64_t milliseconds = te.tv_sec * 1000LL + te.tv_usec / 1000;`
- `esp-adf\components\ota_service\ota_proc_default.c:61` `int64_t cur_time = esp_timer_get_time();`
- `esp-adf\components\esp_peripherals\lib\button\button.c:45` `long long milliseconds = te.tv_sec * 1000LL + te.tv_usec / 1000;`
- `esp-adf\components\esp_peripherals\lib\touch\touch.c:77` `long long milliseconds = te.tv_sec * 1000LL + te.tv_usec / 1000; // calculate milliseconds`
- `esp-adf\examples\ai_agent\coze_ws_app\main\audio_processor.c:166` `if ((esp_timer_get_time() - start_tm) / 1000000 > AEC_RECORD_TIME) {`

### transport_queue (48 matches)
- `esp-adf\components\audio_pipeline\audio_event_iface.c:76` `evt->queue_set = xQueueCreateSet(evt->queue_set_size);`
- `esp-adf\components\audio_recorder\audio_recorder.c:515` `recorder->cmd_queue = xQueueCreate(DEFAULT_CMD_Q_LEN, sizeof(recorder_msg_t));`
- `esp-adf\components\audio_sal\audio_queue.c:34` `handle = (QueueHandle_t)xQueueCreate(queue_len, item_size);`
- `esp-adf\components\battery_service\battery_service.c:250` `battery_service->serv_q = xQueueCreate(3, sizeof(battery_msg_t));`
- `esp-adf\components\bluetooth_service\a2dp_stream.c:347` `s_aadp_handler.a2dp_queue = xQueueCreate(A2DP_STREAM_QUEUE_SIZE, sizeof(a2dp_data_t));`
- `esp-adf\components\coredump_upload_service\coredump_upload_service.c:224` `uploader->cmd_q = xQueueCreate(2, sizeof(coredump_msg_t));`
- `esp-adf\components\dueros_service\dueros_service.c:384` `serv->duer_que = xQueueCreate(3, sizeof(duer_task_msg_t));`

### udp (13 matches)
- `esp-adf\components\audio_sal\audio_queue.c:54` `ret = xQueueSendToFront((QueueHandle_t)queue, item, block_time_ms / portTICK_PERIOD_MS);`
- `esp-adf\components\dueros_service\dueros_service.c:105` `xQueueSendToFront(que, &evt, 0) ;`
- `esp-adf\components\esp_peripherals\periph_is31fl3216.c:118` `xQueueSendToFront(que, &evt, 0) ;`
- `esp-adf\components\ota_service\ota_service.c:76` `xQueueSendToFront(que, &evt, 0);`
- `esp-adf\components\wifi_service\airkiss_config\airkiss_config.c:166` `send_socket = socket(AF_INET, SOCK_DGRAM, 0);`

### vad_detection (22 matches)
- `esp-adf\components\audio_recorder\recorder_sr.c:109` `ESP_LOGV(TAG, "wake %d, vad %d", afe_result->wakeup_state, afe_result->vad_state);`
- `esp-adf\components\audio_stream\algorithm_stream.c:123` `switch (res->vad_state) {`
- `esp-adf\components\audio_recorder\test\test_audio_recorder.c:464` `recorder_sr_cfg.afe_cfg.vad_init = false;`

### wake_word (36 matches)
- `esp-adf\components\audio_recorder\audio_recorder.c:629` `esp_err_t audio_recorder_wakenet_enable(audio_rec_handle_t handle, bool enable)`
- `esp-adf\components\audio_recorder\recorder_sr.c:111` `case WAKENET_CHANNEL_VERIFIED:`

### watchdog (2 matches)
- `esp-adf\components\coredump_upload_service\coredump_upload_service.c:173` `case ESP_RST_TASK_WDT:`
- `esp-adf\examples\protocols\rtmp\main\rtmp_app_setting.c:37` `"sUsp53DsNvCCtWDT6fd9D1v+BB6nDk/FCPKhtjYOwOAZlX4wWNSZpRNr5dfrxKsb\n"`

### websocket (11 matches)
- `esp-adf\examples\ai_agent\coze_ws_app\main\coze_chat_app.c:94` `chat_config.websocket_buffer_size = 4096;`
- `esp-adf\components\esp_coze\include\esp_coze_chat.h:12` `#include "esp_websocket_client.h"`

### wifi_power_save (13 matches)
- `esp-adf\components\esp_peripherals\periph_wifi.c:428` `ESP_ERROR_CHECK(esp_wifi_set_ps(WIFI_PS_MIN_MODEM));`
- `esp-adf\examples\ota\main\ota_example.c:172` `esp_wifi_set_ps(WIFI_PS_NONE);`
- `esp-adf\examples\system\power_save\main\audio_power_save.c:28` `#define WIFI_POWER_SAVE_TEST           0`