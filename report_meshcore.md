# Rapport d'Analyse: MeshCore (LoRa Mesh)
**Projet:** `meshcore`

## Statistiques
- Fichiers scannes: 1487
- Fichiers avec matches: 539
- Lignes totales: 430616
- Matches total: 8459

## Distribution par Categorie
- **mesh**: 5723 ??????????????????????????????????????????????????
- **audio**: 925 ??????????????????????????????????????????????????
- **network**: 514 ??????????????????????????????????????????????????
- **timing**: 383 ??????????????????????????????????????????????????
- **transport**: 374 ??????????????????????????????????????????????????
- **rtos**: 300 ??????????????????????????????????????????????????
- **memory**: 240 ??????????????????????????????????????????????????

## ??  Findings Critiques (CRITICAL)
- `Meck-P4-main\main\examples\lvgl_9_ui\win_music_play_pause_1_117x117px_rgb565a8.c:20` [flow_control] `#ifndef LV_ATTRIBUTE_IMAGE_WIN_MUSIC_PLAY_PAUSE_1_117X117PX_RGB565A8`
- `Meck-P4-main\main\examples\lvgl_9_ui\win_music_play_pause_1_117x117px_rgb565a8.c:21` [flow_control] `#define LV_ATTRIBUTE_IMAGE_WIN_MUSIC_PLAY_PAUSE_1_117X117PX_RGB565A8`
- `Meck-P4-main\main\examples\lvgl_9_ui\win_music_play_pause_1_117x117px_rgb565a8.c:24` [flow_control] `const LV_ATTRIBUTE_MEM_ALIGN LV_ATTRIBUTE_LARGE_CONST LV_ATTRIBUTE_IMAGE_WIN_MUSIC_PLAY_PAUSE_1_117X117PX_RGB565A8 uint8`
- `Meck-P4-main\main\examples\lvgl_9_ui\win_music_play_pause_1_117x117px_rgb565a8.c:262` [flow_control] `const lv_image_dsc_t win_music_play_pause_1_117x117px_rgb565a8 = {`
- `Meck-P4-main\main\examples\lvgl_9_ui\win_music_play_pause_1_117x117px_rgb565a8.c:268` [flow_control] `.data = win_music_play_pause_1_117x117px_rgb565a8_map,`
- `Meck-P4-main\main\examples\lvgl_9_ui\win_music_play_pause_2_117x117px_rgb565a8.c:20` [flow_control] `#ifndef LV_ATTRIBUTE_IMAGE_WIN_MUSIC_PLAY_PAUSE_2_117X117PX_RGB565A8`
- `Meck-P4-main\main\examples\lvgl_9_ui\win_music_play_pause_2_117x117px_rgb565a8.c:21` [flow_control] `#define LV_ATTRIBUTE_IMAGE_WIN_MUSIC_PLAY_PAUSE_2_117X117PX_RGB565A8`
- `Meck-P4-main\main\examples\lvgl_9_ui\win_music_play_pause_2_117x117px_rgb565a8.c:24` [flow_control] `const LV_ATTRIBUTE_MEM_ALIGN LV_ATTRIBUTE_LARGE_CONST LV_ATTRIBUTE_IMAGE_WIN_MUSIC_PLAY_PAUSE_2_117X117PX_RGB565A8 uint8`
- `Meck-P4-main\main\examples\lvgl_9_ui\win_music_play_pause_2_117x117px_rgb565a8.c:262` [flow_control] `const lv_image_dsc_t win_music_play_pause_2_117x117px_rgb565a8 = {`
- `Meck-P4-main\main\examples\lvgl_9_ui\win_music_play_pause_2_117x117px_rgb565a8.c:268` [flow_control] `.data = win_music_play_pause_2_117x117px_rgb565a8_map,`
- `Meck-P4-main\debug\examples\hi8561_ov5640\components\esp_video\src\esp_video.c:20` [memory_placement] `#define ALLOC_RAM_ATTR (MALLOC_CAP_8BIT | MALLOC_CAP_INTERNAL)`
- `Meck-P4-main\debug\examples\hi8561_ov5640\components\esp_video\src\esp_video.c:193` [memory_placement] `struct esp_video_stream *IRAM_ATTR esp_video_get_stream(struct esp_video *video, enum v4l2_buf_type type)`
- `Meck-P4-main\debug\examples\hi8561_ov5640\components\esp_video\src\esp_video.c:848` [memory_placement] `struct esp_video_buffer_element *IRAM_ATTR esp_video_get_queued_element(struct esp_video *video, uint32_t type)`
- `Meck-P4-main\debug\examples\hi8561_ov5640\components\esp_video\src\esp_video.c:879` [memory_placement] `uint8_t *IRAM_ATTR esp_video_get_queued_buffer(struct esp_video *video, uint32_t type)`
- `Meck-P4-main\debug\examples\hi8561_ov5640\components\esp_video\src\esp_video.c:933` [memory_placement] `esp_err_t IRAM_ATTR esp_video_done_element(struct esp_video *video, uint32_t type, struct esp_video_buffer_element *elem`
- `Meck-P4-main\debug\examples\hi8561_ov5640\components\esp_video\src\esp_video.c:978` [memory_placement] `esp_err_t IRAM_ATTR esp_video_done_buffer(struct esp_video *video, uint32_t type, uint8_t *buffer, uint32_t n)`
- `Meck-P4-main\debug\examples\hi8561_ov5640\components\esp_video\src\esp_video.c:1108` [memory_placement] `} else if (info->caps & MALLOC_CAP_INTERNAL) {`
- `Meck-P4-main\debug\examples\hi8561_ov5640\components\esp_video\src\esp_video_buffer.c:127` [memory_placement] `struct esp_video_buffer_element *IRAM_ATTR esp_video_buffer_get_element_by_buffer(struct esp_video_buffer *buffer, uint8`
- `Meck-P4-main\debug\examples\hi8561_ov5640\components\esp_video\src\esp_video_isp_pipeline.c:1099` [memory_placement] `StaticTask_t *task_ptr = heap_caps_malloc(sizeof(StaticTask_t), MALLOC_CAP_INTERNAL);`
- `Meck-P4-main\debug\examples\hi8561_ov5640\components\esp_video\src\device\esp_video_csi_device.c:235` [memory_placement] `static bool IRAM_ATTR csi_video_on_trans_finished(esp_cam_ctlr_handle_t handle, esp_cam_ctlr_trans_t *trans, void *user_`
- `Meck-P4-main\debug\examples\hi8561_ov5640\components\esp_video\src\device\esp_video_csi_device.c:253` [memory_placement] `static bool IRAM_ATTR csi_video_on_get_new_trans(esp_cam_ctlr_handle_t handle, esp_cam_ctlr_trans_t *trans, void *user_d`
- `Meck-P4-main\debug\examples\hi8561_ov5640\components\esp_video\src\device\esp_video_csi_device.c:606` [memory_placement] `csi_video = heap_caps_calloc(1, sizeof(struct csi_video), MALLOC_CAP_8BIT | MALLOC_CAP_INTERNAL);`
- `Meck-P4-main\debug\examples\hi8561_ov5640\components\esp_video\src\device\esp_video_dvp_device.c:100` [memory_placement] `static bool IRAM_ATTR dvp_video_on_trans_finished(esp_cam_ctlr_handle_t handle, esp_cam_ctlr_trans_t *trans, void *user_`
- `Meck-P4-main\debug\examples\hi8561_ov5640\components\esp_video\src\device\esp_video_dvp_device.c:111` [memory_placement] `static bool IRAM_ATTR dvp_video_on_get_new_trans(esp_cam_ctlr_handle_t handle, esp_cam_ctlr_trans_t *trans, void *user_d`
- `Meck-P4-main\debug\examples\hi8561_ov5640\components\esp_video\src\device\esp_video_dvp_device.c:430` [memory_placement] `dvp_video = heap_caps_calloc(1, sizeof(struct dvp_video), MALLOC_CAP_8BIT | MALLOC_CAP_INTERNAL);`
- `Meck-P4-main\debug\examples\hi8561_ov5640\components\esp_video\src\device\esp_video_h264_device.c:466` [memory_placement] `h264_video = heap_caps_calloc(1, sizeof(struct h264_video), MALLOC_CAP_8BIT | MALLOC_CAP_INTERNAL);`
- `Meck-P4-main\debug\examples\hi8561_ov5640\components\esp_video\src\device\esp_video_jpeg_device.c:394` [memory_placement] `jpeg_video = heap_caps_calloc(1, sizeof(struct jpeg_video), MALLOC_CAP_8BIT | MALLOC_CAP_INTERNAL);`
- `Meck-P4-main\debug\examples\hi8561_ov5640\components\esp_video\src\data_reprocessing\esp32p4\esp_video_swap_byte.c:66` [memory_placement] `esp_err_t IRAM_ATTR esp_video_swap_byte_start(esp_video_swap_byte_t *swap_byte)`
- `Meck-P4-main\debug\examples\gpio_interrupt\main\main.c:18` [memory_placement] `static void IRAM_ATTR exit_gpio_isr_handler(void *arg)`
- `Meck-P4-main\debug\examples\esp32c6_at_host_sdio_uart\main\app_main.c:16` [sdio_bridge] `#include "sdio_host_log.h"`

## Detail par Sous-systeme

### afe_pipeline (21 matches)
- `Meck-P4-main\main\examples\afe\main.cpp:14` `#include "esp_afe_sr_models.h"`

### codec_init (103 matches)
- `Meck-P4-main\debug\examples\i2s_es8311\main\i2s_es8311_example.c:30` `static esp_err_t es8311_codec_init(void)`
- `Meck-P4-main\main\examples\afe\main.cpp:205` `ES8311->begin(MCLK_MULTIPLE, SAMPLE_RATE, i2s_data_bit_width_t::I2S_DATA_BIT_WIDTH_16BIT);`

### encryption (259 matches)
- `Meck-P4-main\debug\examples\hi8561_ov5640\components\esp_video\src\esp_video_isp_pipeline.c:335` `static void config_ccm(esp_video_isp_t *isp, esp_ipa_metadata_t *metadata)`

### ethernet (514 matches)
- `Meck-P4-main\debug\examples\ethernet_iperf\main\cmd_ethernet.c:12` `#include "esp_eth.h"`

### flow_control (100 matches)
- `Meck-P4-main\main\examples\lvgl_9_ui\win_music_play_pause_1_117x117px_rgb565a8.c:20` `#ifndef LV_ATTRIBUTE_IMAGE_WIN_MUSIC_PLAY_PAUSE_1_117X117PX_RGB565A8`
- `Meck-P4-main\main\examples\lvgl_9_ui\win_music_play_pause_2_117x117px_rgb565a8.c:20` `#ifndef LV_ATTRIBUTE_IMAGE_WIN_MUSIC_PLAY_PAUSE_2_117X117PX_RGB565A8`

### hosted_init (1 matches)
- `Meck-P4-main\main\examples\esp_hosted_mcu_sdio_wifi\main.cpp:139` `esp_err_t result = esp_hosted_init();`

### i2s_capture (33 matches)
- `Meck-P4-main\debug\examples\i2s_es8311\main\i2s_es8311_example.c:170` `ret = i2s_channel_read(rx_handle, mic_data, EXAMPLE_RECV_BUF_SIZE, &bytes_read, 1000);`
- `Meck-P4-main\debug\examples\uvc_sc2336\components\cpp_bus_driver\src\bus\iis\hardware_iis.cpp:194` `esp_err_t assert = i2s_channel_read(_chan_rx_handle, data, byte, &buffer, DEFAULT_CPP_BUS_DRIVER_IIS`
- `Meck-P4-main\debug\examples\uvc_ov5645\components\cpp_bus_driver\src\bus\iis\hardware_iis.cpp:194` `esp_err_t assert = i2s_channel_read(_chan_rx_handle, data, byte, &buffer, DEFAULT_CPP_BUS_DRIVER_IIS`
- `Meck-P4-main\debug\examples\uvc_ov2710\components\cpp_bus_driver\src\bus\iis\hardware_iis.cpp:194` `esp_err_t assert = i2s_channel_read(_chan_rx_handle, data, byte, &buffer, DEFAULT_CPP_BUS_DRIVER_IIS`
- `Meck-P4-main\debug\examples\usb_extend_screen\components\cpp_bus_driver\src\bus\iis\hardware_iis.cpp:413` `esp_err_t assert = i2s_channel_read(_chan_rx_handle, data, byte, &buffer, DEFAULT_CPP_BUS_DRIVER_IIS`
- `Meck-P4-main\debug\examples\sc2336(green_hue_error)\components\cpp_bus_driver-1.0.0\src\bus\iis\hardware_iis.cpp:194` `esp_err_t assert = i2s_channel_read(_chan_rx_handle, data, byte, &buffer, DEFAULT_CPP_BUS_DRIVER_IIS`

### i2s_driver (127 matches)
- `Meck-P4-main\debug\examples\i2s_es8311\main\i2s_es8311_example.c:92` `ESP_ERROR_CHECK(i2s_channel_init_std_mode(tx_handle, &std_cfg));`
- `Meck-P4-main\components\chmorgan__esp-audio-player\test\audio_player_test.c:130` `ESP_ERROR_CHECK(i2s_channel_init_std_mode(*tx_channel, p_i2s_cfg));`
- `Meck-P4-main\debug\examples\uvc_sc2336\components\cpp_bus_driver\src\bus\iis\hardware_iis.cpp:70` `assert = i2s_channel_init_std_mode(_chan_tx_handle, &std_config);`

### i2s_playback (47 matches)
- `Meck-P4-main\debug\examples\i2s_es8311\main\i2s_es8311_example.c:128` `ret = i2s_channel_write(tx_handle, data_ptr, music_pcm_end - data_ptr, &bytes_write, portMAX_DELAY);`
- `Meck-P4-main\components\chmorgan__esp-audio-player\test\audio_player_test.c:70` `static esp_err_t bsp_i2s_write(void * audio_buffer, size_t len, size_t *bytes_written, uint32_t time`
- `Meck-P4-main\debug\examples\uvc_sc2336\components\cpp_bus_driver\src\bus\iis\hardware_iis.cpp:213` `esp_err_t assert = i2s_channel_write(_chan_tx_handle, data, byte, &buffer, DEFAULT_CPP_BUS_DRIVER_II`
- `Meck-P4-main\debug\examples\uvc_ov5645\components\cpp_bus_driver\src\bus\iis\hardware_iis.cpp:213` `esp_err_t assert = i2s_channel_write(_chan_tx_handle, data, byte, &buffer, DEFAULT_CPP_BUS_DRIVER_II`

### jitter_buffer (2 matches)
- `Meck-P4-main\components\meshcore\MeckUI.cpp:11421` `// height in normal use, but suppressing the bar guarantees no jitter`

### lora_radio (759 matches)
- `Meck-P4-main\main\keyboard_examples\radiolib_cc1101_send_receive\main.cpp:2` `* @Description: radiolib_cc1101_send_receive`

### memory_placement (79 matches)
- `Meck-P4-main\debug\examples\hi8561_ov5640\components\esp_video\src\esp_video.c:20` `#define ALLOC_RAM_ATTR (MALLOC_CAP_8BIT | MALLOC_CAP_INTERNAL)`
- `Meck-P4-main\debug\examples\hi8561_ov5640\components\esp_video\src\esp_video_buffer.c:127` `struct esp_video_buffer_element *IRAM_ATTR esp_video_buffer_get_element_by_buffer(struct esp_video_b`
- `Meck-P4-main\debug\examples\hi8561_ov5640\components\esp_video\src\esp_video_isp_pipeline.c:1099` `StaticTask_t *task_ptr = heap_caps_malloc(sizeof(StaticTask_t), MALLOC_CAP_INTERNAL);`
- `Meck-P4-main\debug\examples\hi8561_ov5640\components\esp_video\src\device\esp_video_csi_device.c:235` `static bool IRAM_ATTR csi_video_on_trans_finished(esp_cam_ctlr_handle_t handle, esp_cam_ctlr_trans_t`

### psram_usage (161 matches)
- `Meck-P4-main\debug\examples\video_lcd_display\main\main.c:45` `ESP_ERROR_CHECK(esp_cache_get_alignment(MALLOC_CAP_SPIRAM, &data_cache_line_size));`
- `Meck-P4-main\debug\examples\hi8561_ov5640\components\esp_video\src\esp_video.c:1104` `if (info->caps & MALLOC_CAP_SPIRAM) {`
- `Meck-P4-main\debug\examples\hi8561_ov5640\components\esp_video\src\esp_video_isp_pipeline.c:60` `#if CONFIG_ISP_PIPELINE_CONTROLLER_TASK_STACK_USE_PSRAM`

### routing (92 matches)
- `Meck-P4-main\components\meshcore\MeckUI.cpp:5723` `mesh->sendFlood(adv);`
- `Meck-P4-main\components\meshcore\meck_app.cpp:48` `// marks every outgoing packet in the seen-table at sendFlood time, which`

### sample_rate_config (571 matches)
- `Meck-P4-main\debug\examples\i2s_es8311\main\i2s_es8311_example.c:56` `.sample_frequency = EXAMPLE_SAMPLE_RATE};`
- `Meck-P4-main\components\codec2\src\c2sim.c:69` `int Fs = 8000;`
- `Meck-P4-main\components\codec2\src\ch.c:144` `Fs = 8000;`
- `Meck-P4-main\components\codec2\src\codec2.c:1505` `resample_rate_L(&c2->c2const, &model_, rate_K_vec_,`

### sdio_bridge (33 matches)
- `Meck-P4-main\debug\examples\esp32c6_at_host_sdio_uart\main\app_main.c:16` `#include "sdio_host_log.h"`
- `Meck-P4-main\debug\examples\esp32c6_at_host_sdio_uart\components\sdio_host\sdio_host_transport.c:12` `#include "sdio_host_reg.h"`

### spi_bridge (187 matches)
- `Meck-P4-main\debug\examples\ethernet_iperf\components\ethernet_init\ethernet_init.c:159` `ESP_GOTO_ON_ERROR(spi_bus_initialize(CONFIG_EXAMPLE_ETH_SPI_HOST, &buscfg, SPI_DMA_CH_AUTO),`
- `Meck-P4-main\debug\examples\ethernet_basic\components\ethernet_init\ethernet_init.c:159` `ESP_GOTO_ON_ERROR(spi_bus_initialize(CONFIG_EXAMPLE_ETH_SPI_HOST, &buscfg, SPI_DMA_CH_AUTO),`

### sync_word (4613 matches)
- `Meck-P4-main\main\examples\lvgl_9_ui\win_home_app_icon_camera_110x110px_rgb565a8.c:38` `0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00`

### synchronization (189 matches)
- `Meck-P4-main\debug\examples\hi8561_ov5640\components\esp_video\src\esp_video.c:344` `video->mutex = xSemaphoreCreateMutex();`

### task_pinning (8 matches)
- `Meck-P4-main\debug\examples\video_lcd_display\main\app_video.c:371` `BaseType_t result = xTaskCreatePinnedToCore(video_stream_task, "video stream task", VIDEO_TASK_STACK`
- `Meck-P4-main\debug\examples\hi8561_ov5640\main\app_video.c:371` `BaseType_t result = xTaskCreatePinnedToCore(video_stream_task, "video stream task", VIDEO_TASK_STACK`
- `Meck-P4-main\components\private_library\app_video.c:371` `BaseType_t result = xTaskCreatePinnedToCore(video_stream_task, "video stream task", VIDEO_TASK_STACK`
- `Meck-P4-main\main\examples\afe\main.cpp:140` `xTaskCreatePinnedToCore(&feed_Task, "feed", 8 * 1024, (void *)afe_data, 5, NULL, 0);`
- `Meck-P4-main\debug\examples\usb_extend_screen\main\app_vendor.cpp:151` `xTaskCreatePinnedToCore(transfer_task, "transfer_task", 4096, NULL, CONFIG_VENDOR_TASK_PRIORITY, NUL`
- `Meck-P4-main\components\chmorgan__esp-audio-player\audio_player.cpp:562` `task_val = xTaskCreatePinnedToCore(`
- `Meck-P4-main\components\meshcore\MeckAudio.cpp:618` `cfg.coreID       = 1;             /* core 1; LVGL is on core 0 */`

### task_priority (65 matches)
- `Meck-P4-main\debug\examples\video_lcd_display\main\app_video.c:26` `#define VIDEO_TASK_PRIORITY             (4)`
- `Meck-P4-main\debug\examples\hi8561_ov5640\main\app_video.c:26` `#define VIDEO_TASK_PRIORITY             (4)`
- `Meck-P4-main\debug\examples\hi8561_ov5640\components\esp_video\src\esp_video_isp_pipeline.c:33` `#define ISP_TASK_PRIORITY           11`
- `Meck-P4-main\debug\examples\hi8561_ov5640\components\esp_video\src\device\esp_video_isp_device.c:804` `.intr_priority = 0,`
- `Meck-P4-main\debug\examples\hi8561_ov5640\components\esp_video\src\device\esp_video_jpeg_device.c:120` `.intr_priority = 0,`
- `Meck-P4-main\components\private_library\app_video.c:26` `#define VIDEO_TASK_PRIORITY             (4)`
- `Meck-P4-main\components\esp_video\src\esp_video_isp_pipeline.c:33` `#define ISP_TASK_PRIORITY           11`
- `Meck-P4-main\components\esp_video\src\device\esp_video_isp_device.c:804` `.intr_priority = 0,`
- `Meck-P4-main\components\esp_video\src\device\esp_video_jpeg_device.c:120` `.intr_priority = 0,`
- `Meck-P4-main\components\chmorgan__esp-audio-player\test\audio_player_test.c:103` `.priority = 0,`

### timestamp (383 matches)
- `Meck-P4-main\debug\examples\video_lcd_display\main\main.c:92` `start_time = esp_timer_get_time();  // Get the initial time for frame rate statistics`
- `Meck-P4-main\debug\examples\hi8561_ov5640\components\esp_video\src\data_reprocessing\esp32p4\esp_video_swap_short.c:132` `int64_t start_time_us = esp_timer_get_time();`
- `Meck-P4-main\debug\examples\hi8561_ov5640\components\esp_video\examples\video_custom_format\main\app_main.c:219` `int64_t start_time_us = esp_timer_get_time();`
- `Meck-P4-main\debug\examples\hi8561_ov5640\components\esp_video\examples\uvc\main\uvc_example.c:426` `us = esp_timer_get_time();`
- `Meck-P4-main\debug\examples\hi8561_ov5640\components\esp_video\examples\image_storage\usb_msc\main\tusb_msc_main.c:593` `us = esp_timer_get_time();`

### transport_queue (22 matches)
- `Meck-P4-main\main\examples\tusb_serial_device\main.c:84` `app_queue = xQueueCreate(5, sizeof(app_message_t));`
- `Meck-P4-main\debug\examples\usb_extend_screen\main\app_hid.c:81` `s_tinyusb_hid->hid_queue = xQueueCreate(10, sizeof(hid_report_t));   // Adjust queue length and item`
- `Meck-P4-main\debug\examples\usb_extend_screen\main\usb_frame.c:29` `empty_fb_queue = xQueueCreate(nb_of_fb, sizeof(frame_t *));`
- `Meck-P4-main\components\codec2\src\mpdecode_core.c:636` `void symbols_to_llrs(float llr[], COMP rx_qpsk_symbols[], float rx_amps[],`
- `Meck-P4-main\components\chmorgan__esp-audio-player\test\audio_player_test.c:183` `event_queue = xQueueCreate(1, sizeof(audio_player_callback_event_t));`
- `Meck-P4-main\main\examples\esp_hosted_mcu_sdio_wifi\main.cpp:102` `config->u.sdio.tx_queue_size, config->u.sdio.rx_queue_size);`

### vad_detection (1 matches)
- `Meck-P4-main\main\examples\afe\main.cpp:91` `printf("vad state: %d\n", res->vad_state);`

### wake_word (20 matches)
- `Meck-P4-main\main\examples\afe\main.cpp:72` `// modify wakenet detection threshold`

### watchdog (38 matches)
- `Meck-P4-main\main\keyboard_examples\bq25896\main.cpp:45` `Kode_Bq25896::bq25896_set_watchdog_timer(Bq25896_Handle, Kode_Bq25896::bq25896_watchdog_t::BQ25896_W`
- `Meck-P4-main\main\examples\lvgl_9_ui\main.cpp:5803` `// trip the watchdog.`
- `Meck-P4-main\debug\examples\usb_extend_screen\components\cpp_bus_driver\src\chip\iic\sgm41562xx.cpp:148` `status.watchdog_expiration_flag = (chip_flag & 0B00100000) >> 5;`
- `Meck-P4-main\debug\examples\iperf\components\cpp_bus_driver\src\chip\iic\sgm41562xx.cpp:148` `status.watchdog_expiration_flag = (chip_flag & 0B00100000) >> 5;`
- `Meck-P4-main\debug\examples\hi8561_touch_debug\components\cpp_bus_driver-1.0.0\src\chip\spi\sx126x.cpp:76` `_watchdog_busy = 0;`

### wifi_power_save (29 matches)
- `Meck-P4-main\debug\examples\uvc_sc2336\components\cpp_bus_driver\src\chip\sdio\esp_at.cpp:98` `case Sleep_Mode::MODEM_SLEEP:`
- `Meck-P4-main\debug\examples\uvc_ov5645\components\cpp_bus_driver\src\chip\sdio\esp_at.cpp:98` `case Sleep_Mode::MODEM_SLEEP:`
- `Meck-P4-main\debug\examples\uvc_ov2710\components\cpp_bus_driver\src\chip\sdio\esp_at.cpp:98` `case Sleep_Mode::MODEM_SLEEP:`
- `Meck-P4-main\debug\examples\usb_extend_screen\components\cpp_bus_driver\src\chip\iic\aw21009xxx.cpp:61` `bool Aw21009xxx::set_auto_power_save(bool enable)`
- `Meck-P4-main\debug\examples\usb_extend_screen\components\cpp_bus_driver\src\chip\sdio\esp_at.cpp:98` `case Sleep_Mode::MODEM_SLEEP:`
- `Meck-P4-main\debug\examples\rm69a10_lvgl\components\cpp_bus_driver\src\chip\sdio\esp_at.cpp:98` `case Sleep_Mode::MODEM_SLEEP:`

### wifi_remote (2 matches)
- `Meck-P4-main\main\examples\esp_hosted_mcu_sdio_wifi\main.cpp:18` `#include "esp_wifi_remote.h"`
- `Meck-P4-main\components\meshcore\MeckAudio.cpp:15` `* version that conflicted with LilyGo's pinned esp_hosted / esp_wifi_remote.`