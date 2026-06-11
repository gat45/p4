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
- `esp-adf\micropython_adf\mod\audio_player.c:190` [flow_control] `if (state.status == AUDIO_STATUS_RUNNING || state.status == AUDIO_STATUS_PAUSED) {`
- `esp-adf\micropython_adf\mod\audio_player.c:194` [flow_control] `while (wait-- && (state.status == AUDIO_STATUS_RUNNING || state.status == AUDIO_STATUS_PAUSED)) {`
- `esp-adf\micropython_adf\mod\audio_player.c:244` [flow_control] `static mp_obj_t audio_player_pause(mp_obj_t self_in)`
- `esp-adf\micropython_adf\mod\audio_player.c:247` [flow_control] `return mp_obj_new_int(esp_audio_pause(self->player));`
- `esp-adf\micropython_adf\mod\audio_player.c:249` [flow_control] `static MP_DEFINE_CONST_FUN_OBJ_1(audio_player_pause_obj, audio_player_pause);`
- `esp-adf\micropython_adf\mod\audio_player.c:350` [flow_control] `{ MP_ROM_QSTR(MP_QSTR_pause), MP_ROM_PTR(&audio_player_pause_obj) },`
- `esp-adf\micropython_adf\mod\audio_player.c:362` [flow_control] `{ MP_ROM_QSTR(MP_QSTR_STATUS_PAUSED), MP_ROM_INT(AUDIO_STATUS_PAUSED) },`
- `esp-adf\micropython_adf\mod\modaudio.c:45` [memory_placement] `mp_obj_dict_store(dict, MP_ROM_QSTR(MP_QSTR_inter), MP_OBJ_TO_PTR(mp_obj_new_int(heap_caps_get_free_size(MALLOC_CAP_INTE`
- `esp-adf\micropython_adf\mod\modaudio.c:46` [memory_placement] `mp_obj_dict_store(dict, MP_ROM_QSTR(MP_QSTR_dram), MP_OBJ_TO_PTR(mp_obj_new_int(heap_caps_get_free_size(MALLOC_CAP_INTER`
- `esp-adf\micropython_adf\mod\vfs_stream.c:229` [flow_control] `if (AEL_STATE_PAUSED != audio_element_get_state(self)) {`
- `esp-adf\examples\system\power_save\main\audio_sleep_wakeup.c:291` [memory_placement] `static void IRAM_ATTR gpio_isr_handler(void* arg)`
- `esp-adf\examples\recorder\pipeline_recording_to_sdcard\main\recording_to_sdcard_example.c:27` [opus_encode] `#elif defined (CONFIG_CHOICE_OPUS_ENCODER)`
- `esp-adf\examples\recorder\pipeline_recording_to_sdcard\main\recording_to_sdcard_example.c:28` [opus_encode] `#include "opus_encoder.h"`
- `esp-adf\examples\recorder\pipeline_recording_to_sdcard\main\recording_to_sdcard_example.c:45` [opus_encode] `#if defined (CONFIG_CHOICE_OPUS_ENCODER)`
- `esp-adf\examples\recorder\pipeline_recording_to_sdcard\main\recording_to_sdcard_example.c:93` [opus_encode] `#elif defined (CONFIG_CHOICE_OPUS_ENCODER)`
- `esp-adf\examples\recorder\pipeline_recording_to_sdcard\main\recording_to_sdcard_example.c:151` [opus_encode] `#elif defined (CONFIG_CHOICE_OPUS_ENCODER)`
- `esp-adf\examples\recorder\pipeline_recording_to_sdcard\main\recording_to_sdcard_example.c:152` [opus_encode] `opus_encoder_cfg_t opus_cfg = DEFAULT_OPUS_ENCODER_CONFIG();`
- `esp-adf\examples\recorder\pipeline_recording_to_sdcard\main\recording_to_sdcard_example.c:171` [opus_encode] `audio_encoder = encoder_opus_init(&opus_cfg);`
- `esp-adf\examples\recorder\pipeline_recording_to_sdcard\main\recording_to_sdcard_example.c:205` [opus_encode] `#elif defined (CONFIG_CHOICE_OPUS_ENCODER)`
- `esp-adf\examples\recorder\pipeline_recording_to_sdcard\main\recording_to_sdcard_example.c:223` [opus_encode] `#elif defined (CONFIG_CHOICE_OPUS_ENCODER)`
- `esp-adf\examples\recorder\pipeline_recording_to_sdcard\main\recording_to_sdcard_example.c:256` [opus_encode] `#elif defined (CONFIG_CHOICE_OPUS_ENCODER)`
- `esp-adf\examples\recorder\pipeline_recording_to_sdcard\main\recording_to_sdcard_example.c:309` [opus_encode] `#if defined (CONFIG_CHOICE_OPUS_ENCODER) && defined (CONFIG_CHOICE_AAC_ENCODER) && defined (CONFIG_ESP_LYRAT_MINI_V1_1_B`
- `esp-adf\examples\recorder\pipeline_recording_to_sdcard\main\recording_to_sdcard_example.c:327` [opus_encode] `#if defined (CONFIG_CHOICE_OPUS_ENCODER) && defined (CONFIG_CHOICE_AAC_ENCODER) && defined (CONFIG_ESP_LYRAT_MINI_V1_1_B`
- `esp-adf\examples\protocols\components\cli_console\src\console.c:58` [memory_placement] `(int)heap_caps_get_free_size(MALLOC_CAP_INTERNAL), (int)heap_caps_get_free_size(MALLOC_CAP_INTERNAL | MALLOC_CAP_8BIT));`
- `esp-adf\examples\player\pipeline_sdcard_mp3_control\main\play_sdcard_mp3_control_example.c:45` [flow_control] `to start, pause, resume, finish current song and adjust volume`
- `esp-adf\examples\player\pipeline_sdcard_mp3_control\main\play_sdcard_mp3_control_example.c:64` [flow_control] `audio_pipeline_pause(pipeline);`
- `esp-adf\examples\player\pipeline_sdcard_mp3_control\main\play_sdcard_mp3_control_example.c:66` [flow_control] `case AEL_STATE_PAUSED :`
- `esp-adf\examples\player\pipeline_sdcard_mp3_control\main\play_sdcard_mp3_control_example.c:200` [flow_control] `ESP_LOGW(TAG, "      [Play] to start, pause and resume, [Set] next song.");`
- `esp-adf\examples\player\pipeline_hfp_stream\main\pipeline_hfp_stream_example.c:49` [flow_control] `audio_pipeline_pause(pipeline_out);`
- `esp-adf\examples\player\pipeline_hfp_stream\main\pipeline_hfp_stream_example.c:50` [flow_control] `audio_pipeline_pause(pipeline_in);`

## Detail par Sous-systeme

### afe_pipeline (128 matches)
- `esp-adf\examples\protocols\voip\main\voip_app.c:22` `#include "algorithm_stream.h"`
- `esp-adf\examples\protocols\esp-rtsp\main\main.c:18` `#include "algorithm_stream.h"`
- `esp-adf\examples\protocols\esp-rtc\main\main.c:18` `#include "algorithm_stream.h"`
- `esp-adf\examples\protocols\components\audio_flash_tone\audio_player_int_tone.c:33` `#include "algorithm_stream.h"`
- `esp-adf\examples\protocols\components\av_stream\av_stream.c:339` `fat_info.bits = ALGORITHM_STREAM_DEFAULT_SAMPLE_BIT;`
- `esp-adf\examples\protocols\components\av_stream\av_stream_hal\av_stream_hal_audio.c:30` `#include "algorithm_stream.h"`
- `esp-adf\examples\dueros\main\dueros_app.c:64` `#include "algorithm_stream.h"`
- `esp-adf\examples\ai_agent\coze_ws_app\main\audio_processor.c:42` `#include "esp_afe_config.h"`

### clock_source (6 matches)
- `esp-adf\examples\get-started\pipeline_a2dp_sink_and_hfp\main\a2dp_sink_and_hfp_example.c:409` `i2s_cfg2.i2s_config.use_apll = false;`
- `esp-adf\components\esp_codec_dev\test_apps\codec_dev_test\main\test_board.c:192` `.use_apll = true,`
- `esp-adf\components\audio_hal\test\test_audio_hal.c:54` `.use_apll = 1,`
- `esp-adf\components\audio_stream\include\i2s_stream.h:95` `.use_apll = true,                                                       \`

### codec_init (25 matches)
- `esp-adf\components\esp_codec_dev\device\es8311\es8311.c:215` `static int es8311_config_fmt(audio_codec_es8311_t *codec, es_i2s_fmt_t fmt)`
- `esp-adf\components\audio_hal\test\test_audio_hal.c:131` `audio_hal_codec_config_t es8311_cfg = AUDIO_CODEC_DEFAULT_CONFIG();`
- `esp-adf\components\audio_hal\driver\es8311\es8311.c:72` `.audio_codec_initialize = es8311_codec_init,`

### dma_buffer (21 matches)
- `esp-adf\examples\ai_agent\volc_rtc\components\audio_processor\audio_stream_dual_microphones.c:156` `i2s_cfg.chan_cfg.dma_desc_num = 6;`
- `esp-adf\examples\ai_agent\volc_rtc\components\audio_processor\audio_stream_single_microphone.c:149` `i2s_cfg.chan_cfg.dma_desc_num = 6;`
- `esp-adf\examples\advanced_examples\algorithm\main\algorithm_examples.c:153` `i2s_w_cfg.chan_cfg.dma_desc_num = 6;`
- `esp-adf\components\audio_stream\i2s_stream.c:142` `int index = i2s->config.i2s_config.dma_buf_count;`
- `esp-adf\components\esp_codec_dev\test_apps\codec_dev_test\main\test_board.c:190` `.dma_buf_count = 2,`

### encryption (105 matches)
- `esp-adf\examples\korvo_du1906\main\app_control.c:266` `air_info.aes_key = CONFIG_AIRKISS_KEY;`
- `esp-adf\examples\dueros\main\dueros_app.c:566` `air_info.aes_key = CONFIG_DUER_AIRKISS_KEY;`
- `esp-adf\components\audio_stream\http_stream.c:48` `#include "aes/esp_aes.h"`

### flow_control (239 matches)
- `esp-adf\micropython_adf\mod\audio_player.c:190` `if (state.status == AUDIO_STATUS_RUNNING || state.status == AUDIO_STATUS_PAUSED) {`
- `esp-adf\micropython_adf\mod\vfs_stream.c:229` `if (AEL_STATE_PAUSED != audio_element_get_state(self)) {`
- `esp-adf\examples\player\pipeline_sdcard_mp3_control\main\play_sdcard_mp3_control_example.c:45` `to start, pause, resume, finish current song and adjust volume`

### i2s_capture (72 matches)
- `esp-adf\examples\protocols\components\av_record\record_i2s_aud.c:27` `audio_element_handle_t i2s_reader;`

### i2s_driver (21 matches)
- `esp-adf\components\audio_stream\i2s_stream.c:172` `static esp_err_t _i2s_open(audio_element_handle_t self)`
- `esp-adf\components\audio_stream\i2s_stream_idf5.c:120` `ret |= i2s_channel_init_std_mode(i2s_key_slot[i2s->port].tx_handle, &i2s_key_slot[i2s->port].tx_std_`

### i2s_playback (152 matches)
- `esp-adf\micropython_adf\mod\audio_player.c:144` `i2s_stream_cfg_t i2s_writer = I2S_STREAM_CFG_DEFAULT_WITH_PARA(I2S_NUM_0, 48000, I2S_DATA_BIT_WIDTH_`
- `esp-adf\examples\speech_recognition\wwe\main\main.c:129` `i2s_stream_cfg_t i2s_writer = I2S_STREAM_CFG_DEFAULT_WITH_PARA(I2S_NUM_0, 48000, I2S_DATA_BIT_WIDTH_`
- `esp-adf\examples\protocols\components\audio_flash_tone\audio_player_int_tone.c:41` `static audio_element_handle_t i2s_writer;`

### memory_placement (31 matches)
- `esp-adf\micropython_adf\mod\modaudio.c:45` `mp_obj_dict_store(dict, MP_ROM_QSTR(MP_QSTR_inter), MP_OBJ_TO_PTR(mp_obj_new_int(heap_caps_get_free_`
- `esp-adf\examples\system\power_save\main\audio_sleep_wakeup.c:291` `static void IRAM_ATTR gpio_isr_handler(void* arg)`
- `esp-adf\examples\protocols\components\cli_console\src\console.c:58` `(int)heap_caps_get_free_size(MALLOC_CAP_INTERNAL), (int)heap_caps_get_free_size(MALLOC_CAP_INTERNAL `
- `esp-adf\examples\display\music_player\components\lvgl_gui\lv_port\lv_port.c:76` `static IRAM_ATTR void touchpad_read(lv_indev_drv_t *indev_drv, lv_indev_data_t *data)`
- `esp-adf\examples\display\led_pixels\components\pixel_renderer\led_driver\ws2812_rmt\ws2812_rmt.c:96` `static void IRAM_ATTR ws2812_rmt_adapter(const void *src, rmt_item32_t *dest, size_t src_size,`
- `esp-adf\examples\display\led_pixels\components\pixel_renderer\led_driver\ws2812_spi\ws2812_spi.c:193` `led_dev->buf =  heap_caps_malloc( led_num * WS2812_SPI_LED_BUF, MALLOC_CAP_DMA);`
- `esp-adf\examples\display\lcd_jpeg\main\lcd_jpeg_example_main.c:71` `s_lines[i] = heap_caps_malloc(LCD_H_RES * PARALLEL_LINES * sizeof(uint16_t), MALLOC_CAP_DMA);`
- `esp-adf\examples\display\lcd_camera\main\img_convert.c:90` `int16_t *y_data = heap_caps_malloc_prefer(buf_size * sizeof(int16_t), 2, MALLOC_CAP_8BIT | MALLOC_CA`

### mqtt (10 matches)
- `esp-adf\examples\korvo_du1906\components\bds_light\include\bds_client_event.h:53` `EVENT_RECV_MQTT_PUSH_URL,`
- `esp-adf\examples\korvo_du1906\components\bdsc_engine\include\auth_task.h:41` `const char *mqtt_username;`
- `esp-adf\examples\korvo_du1906\components\bdsc_engine\include\bdsc_engine.h:27` `#include "mqtt_client.h"`
- `esp-adf\examples\korvo_du1906\components\bdsc_engine\include\bdsc_profile.h:42` `char *mqtt_broker;`

### opus_decode (71 matches)
- `esp-adf\examples\player\pipeline_play_sdcard_music\main\play_sdcard_music_example.c:26` `#elif CONFIG_AUDIO_SUPPORT_OPUS_DECODER`
- `esp-adf\examples\player\pipeline_http_select_decoder\main\play_http_select_decoder_example.c:63` `#elif defined SELECT_OPUS_DECODER`

### opus_encode (33 matches)
- `esp-adf\examples\recorder\pipeline_recording_to_sdcard\main\recording_to_sdcard_example.c:27` `#elif defined (CONFIG_CHOICE_OPUS_ENCODER)`

### psram_usage (92 matches)
- `esp-adf\micropython_adf\mod\modaudio.c:41` `#ifdef CONFIG_SPIRAM_BOOT_INIT`
- `esp-adf\examples\speech_recognition\wwe\main\main.c:338` `recorder_sr_cfg.afe_cfg->memory_alloc_mode = AFE_MEMORY_ALLOC_MORE_PSRAM;`
- `esp-adf\examples\protocols\components\cli_console\src\console.c:56` `#ifdef CONFIG_SPIRAM_BOOT_INIT`
- `esp-adf\examples\dueros\main\duer_audio_wrapper.c:151` `if (audio_mem_spiram_stack_is_enabled()) {`
- `esp-adf\examples\display\lcd_camera\main\img_convert.c:90` `int16_t *y_data = heap_caps_malloc_prefer(buf_size * sizeof(int16_t), 2, MALLOC_CAP_8BIT | MALLOC_CA`
- `esp-adf\examples\display\dual_eyes\main\esp_dual_eye_player.c:30` `#define TASK_STACK_IN_PSRAM       (true) // If you read file from flash, must set this to false`

### ring_buffer (497 matches)
- `esp-adf\examples\recorder\pipeline_wav_amr_sdcard\main\pipeline_wav_amr_sdcard.c:137` `ESP_LOGI(TAG, "[4.6] Create ringbuf to link  i2s");`
- `esp-adf\examples\recorder\pipeline_recording_to_sdcard\main\recording_to_sdcard_example.c:287` `audio_element_set_ringbuf_done(i2s_stream_reader);`
- `esp-adf\examples\recorder\pipeline_raw_http\main\record_raw_http.c:135` `audio_pipeline_reset_ringbuffer(pipeline);`
- `esp-adf\examples\recorder\element_wav_amr_sdcard\main\element_wav_amr_sdcard.c:19` `#define RING_BUFFER_SIZE (2048)`

### sample_rate_config (477 matches)
- `esp-adf\micropython_adf\mod\audio_player.c:110` `cfg.resample_rate = 48000;`
- `esp-adf\micropython_adf\mod\audio_recorder.c:184` `out_stream_info.sample_rates = 16000;`
- `esp-adf\micropython_adf\mod\vfs_stream.c:217` `wav_head_init(wav_info, info.sample_rates, info.bits, info.channels);`
- `esp-adf\examples\system\power_save\main\audio_power_save.c:138` `ESP_LOGI(TAG, "[ * ] Receive music info from mp3 decoder, sample_rates=%d, bits=%d, ch=%d",`
- `esp-adf\examples\speech_recognition\wwe\main\main.c:70` `#ifndef CODEC_ADC_SAMPLE_RATE`

### spi_bridge (25 matches)
- `esp-adf\examples\display\led_pixels\components\pixel_renderer\led_driver\ws2812_spi\ws2812_spi.c:42` `#define WS2812_SPI_HOST          (SPI2_HOST)`
- `esp-adf\components\esp_peripherals\lib\sdcard\sdcard.c:131` `sdmmc_host_t host = SDSPI_HOST_DEFAULT();`
- `esp-adf\components\esp_codec_dev\platform\audio_codec_ctrl_spi.c:41` `spi_host_device_t host_id = SPI2_HOST;`

### sync_word (3269 matches)
- `esp-adf\examples\display\music_player\main\assets\img_lv_demo_music_btn_corner_large.c:18` `0x49, 0x2b, 0x49, 0x1c, 0x49, 0x04, 0x49, 0x00, 0x49, 0x00, 0x49, 0x00, 0x49, 0x00, 0x49, 0x00, 0x49`

### synchronization (66 matches)
- `esp-adf\examples\korvo_du1906\components\audio_player\audio_player_manager.c:69` `xSemaphoreHandle                lock_handle;`
- `esp-adf\examples\korvo_du1906\components\audio_player\audio_player_pipeline_int_tone.c:45` `SemaphoreHandle_t sem_mutex;`
- `esp-adf\examples\dueros\main\duer_audio_wrapper.c:81` `static SemaphoreHandle_t        s_mutex     = NULL;`

### task_pinning (8 matches)
- `esp-adf\examples\korvo_du1906\main\app_sys_tools.c:48` `xTaskCreatePinnedToCore(sys_monitor_task, "sys_monitor_task", (2 * 1024), NULL, 1, NULL, 1);`
- `esp-adf\examples\dueros\main\dueros_app.c:500` `xTaskCreatePinnedToCore(sys_monitor_task, "sys_monitor_task", (4 * 1024), NULL, 1, NULL, 1);`
- `esp-adf\examples\display\dual_eyes\main\esp_dual_eye_ui.c:17` `#define UI_TASK_CORE          0`
- `esp-adf\components\audio_sal\audio_sys.c:124` `percentage_time = (task_elapsed_time * 100UL) / (total_elapsed_time * portNUM_PROCESSORS);`
- `esp-adf\components\audio_sal\audio_thread.c:86` `if (xTaskCreatePinnedToCore(main_func, name, stack, arg, prio, (TASK_HANDLE_T*)p_handle, core_id) !=`
- `esp-adf\components\esp_dispatcher\audio_service.c:72` `if (pdPASS != xTaskCreatePinnedToCore(config->task_func,`
- `esp-adf\components\audio_stream\include\aec_stream.h:31` `#define AEC_STREAM_PINNED_TO_CORE     0`
- `esp-adf\components\audio_stream\include\algorithm_stream.h:35` `#define ALGORITHM_STREAM_PINNED_TO_CORE     0`

### task_priority (19 matches)
- `esp-adf\examples\protocols\rtmp\main\rtmp_push_app.c:105` `.thread_cfg = {.priority = 10, .stack_size = 10*1024},`
- `esp-adf\examples\protocols\rtmp\main\rtmp_server_app.c:90` `.thread_cfg = {.priority = 10, .stack_size = 5*1024},`
- `esp-adf\examples\protocols\rtmp\main\rtmp_src_app.c:52` `.thread_cfg = {.priority = 10, .stack_size = 5*1024},`
- `esp-adf\examples\display\dual_eyes\main\esp_dual_eye_ui.c:16` `#define UI_TASK_PRIORITY      3`
- `esp-adf\examples\ai_agent\volc_rtc\main\volc_rtc.c:306` `byte_rtc_set_params(s_volc_rtc.engine,"{\"rtc\":{\"thread\":{\"priority\":6}}}");`
- `esp-adf\examples\ai_agent\coze_ws_app\main\audio_processor.c:80` `#define AUDIO_RECORD_PIP_TASK_PRIORITY      (5)`
- `esp-adf\components\audio_stream\algorithm_stream.c:147` `afe_config->afe_perferred_priority = 21;`
- `esp-adf\components\bluetooth_service\hfp_stream.c:40` `#define ESP_HFP_TASK_PRIORITY    23`
- `esp-adf\components\display_service\display_service.c:42` `#define DISPLAY_TASK_PRIORITY           5`

### timestamp (66 matches)
- `esp-adf\examples\protocols\rtmp\main\rtmp_push_app.c:163` `uint32_t start_time = esp_timer_get_time() / 1000;`
- `esp-adf\examples\protocols\rtmp\main\rtmp_server_app.c:107` `uint32_t start_time = esp_timer_get_time() / 1000;`
- `esp-adf\examples\protocols\rtmp\main\rtmp_src_app.c:64` `uint32_t start_time = esp_timer_get_time() / 1000;`
- `esp-adf\examples\protocols\esp-rtsp\main\rtsp_service.c:41` `stream_first_pts = esp_timer_get_time() / 1000;`
- `esp-adf\examples\protocols\components\av_record\av_record.c:67` `return (uint32_t) (esp_timer_get_time() / 1000);`
- `esp-adf\examples\protocols\components\av_stream\av_stream.c:136` `return esp_timer_get_time() / 1000;`

### transport_queue (48 matches)
- `esp-adf\examples\system\power_save\main\audio_sleep_wakeup.c:360` `gpio_evt_queue = xQueueCreate(10, sizeof(uint32_t));`
- `esp-adf\examples\speech_recognition\wwe\main\main.c:464` `rec_q = xQueueCreate(3, sizeof(int));`
- `esp-adf\examples\protocols\components\av_stream\av_stream.c:408` `av_stream->aenc_queue = xQueueCreate(1, sizeof(av_stream_frame_t));`
- `esp-adf\examples\korvo_du1906\components\audio_player\audio_player_helper_raw.c:149` `xQueueHandle que = xQueueCreate(3, sizeof(audio_player_state_t));`
- `esp-adf\examples\korvo_du1906\components\audio_player\audio_player_manager.c:260` `s_player->sync_state_que = xQueueCreate(1, sizeof(esp_audio_state_t));`
- `esp-adf\examples\korvo_du1906\components\audio_player\test\audio_player_if_test.c:102` `QueueHandle_t player_que = xQueueCreate(3, sizeof(audio_player_state_t));`

### udp (13 matches)
- `esp-adf\components\audio_sal\audio_queue.c:54` `ret = xQueueSendToFront((QueueHandle_t)queue, item, block_time_ms / portTICK_PERIOD_MS);`
- `esp-adf\components\dueros_service\dueros_service.c:105` `xQueueSendToFront(que, &evt, 0) ;`
- `esp-adf\components\esp_peripherals\periph_is31fl3216.c:118` `xQueueSendToFront(que, &evt, 0) ;`
- `esp-adf\components\ota_service\ota_service.c:76` `xQueueSendToFront(que, &evt, 0);`
- `esp-adf\components\wifi_service\airkiss_config\airkiss_config.c:166` `send_socket = socket(AF_INET, SOCK_DGRAM, 0);`

### vad_detection (22 matches)
- `esp-adf\examples\speech_recognition\vad\main\example_vad_main.c:92` `vad_state_t vad_state = vad_process(vad_inst, vad_buff, VAD_SAMPLE_RATE_HZ, VAD_FRAME_LENGTH_MS);`
- `esp-adf\examples\ai_agent\volc_rtc\components\audio_processor\audio_processor.c:360` `recorder_sr_cfg.afe_cfg->vad_init = false;`
- `esp-adf\examples\ai_agent\coze_ws_app\main\audio_processor.c:424` `audio_recorder.afe_cfg->vad_init = VAD_ENABLE;`
- `esp-adf\components\audio_recorder\recorder_sr.c:109` `ESP_LOGV(TAG, "wake %d, vad %d", afe_result->wakeup_state, afe_result->vad_state);`
- `esp-adf\components\audio_stream\algorithm_stream.c:123` `switch (res->vad_state) {`

### wake_word (36 matches)
- `esp-adf\examples\speech_recognition\wwe\main\main.c:64` `#define WAKENET_ENABLE      (true)`
- `esp-adf\examples\dueros\main\duer_audio_wrapper.c:264` `recorder_sr_cfg.afe_cfg->wakenet_mode = DET_MODE_90;`
- `esp-adf\examples\ai_agent\volc_rtc\components\audio_processor\audio_processor.c:358` `recorder_sr_cfg.afe_cfg->wakenet_init = false;`
- `esp-adf\examples\ai_agent\volc_rtc\components\audio_processor\audio_stream_single_microphone.c:203` `recorder_sr_cfg.afe_cfg->wakenet_mode = DET_MODE_90;`
- `esp-adf\examples\ai_agent\coze_ws_app\main\audio_processor.c:370` `ESP_LOGI(TAG, "WAKEUP_START [%d : %d]", info->wake_word_index, info->wakenet_model_index);`

### watchdog (2 matches)
- `esp-adf\examples\protocols\rtmp\main\rtmp_app_setting.c:37` `"sUsp53DsNvCCtWDT6fd9D1v+BB6nDk/FCPKhtjYOwOAZlX4wWNSZpRNr5dfrxKsb\n"`
- `esp-adf\components\coredump_upload_service\coredump_upload_service.c:173` `case ESP_RST_TASK_WDT:`

### websocket (11 matches)
- `esp-adf\examples\ai_agent\coze_ws_app\main\coze_chat_app.c:94` `chat_config.websocket_buffer_size = 4096;`
- `esp-adf\components\esp_coze\include\esp_coze_chat.h:12` `#include "esp_websocket_client.h"`

### wifi_power_save (13 matches)
- `esp-adf\examples\system\power_save\main\audio_power_save.c:28` `#define WIFI_POWER_SAVE_TEST           0`