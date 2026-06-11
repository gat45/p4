# Rapport d'Analyse: T-Display-P4 (official)
**Projet:** `tdisplay_p4`

## Statistiques
- Fichiers scannes: 1151
- Fichiers avec matches: 446
- Lignes totales: 235504
- Matches total: 5048

## Distribution par Categorie
- **mesh**: 3024 ??????????????????????????????????????????????????
- **audio**: 811 ??????????????????????????????????????????????????
- **network**: 498 ??????????????????????????????????????????????????
- **transport**: 283 ??????????????????????????????????????????????????
- **rtos**: 152 ??????????????????????????????????????????????????
- **memory**: 152 ??????????????????????????????????????????????????
- **timing**: 128 ??????????????????????????????????????????????????

## ??  Findings Critiques (CRITICAL)
- `T-Display-P4\main\examples\lvgl_9_ui\win_music_play_pause_1_117x117px_rgb565a8.c:20` [flow_control] `#ifndef LV_ATTRIBUTE_IMAGE_WIN_MUSIC_PLAY_PAUSE_1_117X117PX_RGB565A8`
- `T-Display-P4\main\examples\lvgl_9_ui\win_music_play_pause_1_117x117px_rgb565a8.c:21` [flow_control] `#define LV_ATTRIBUTE_IMAGE_WIN_MUSIC_PLAY_PAUSE_1_117X117PX_RGB565A8`
- `T-Display-P4\main\examples\lvgl_9_ui\win_music_play_pause_1_117x117px_rgb565a8.c:24` [flow_control] `const LV_ATTRIBUTE_MEM_ALIGN LV_ATTRIBUTE_LARGE_CONST LV_ATTRIBUTE_IMAGE_WIN_MUSIC_PLAY_PAUSE_1_117X117PX_RGB565A8 uint8`
- `T-Display-P4\main\examples\lvgl_9_ui\win_music_play_pause_1_117x117px_rgb565a8.c:262` [flow_control] `const lv_image_dsc_t win_music_play_pause_1_117x117px_rgb565a8 = {`
- `T-Display-P4\main\examples\lvgl_9_ui\win_music_play_pause_1_117x117px_rgb565a8.c:268` [flow_control] `.data = win_music_play_pause_1_117x117px_rgb565a8_map,`
- `T-Display-P4\main\examples\lvgl_9_ui\win_music_play_pause_2_117x117px_rgb565a8.c:20` [flow_control] `#ifndef LV_ATTRIBUTE_IMAGE_WIN_MUSIC_PLAY_PAUSE_2_117X117PX_RGB565A8`
- `T-Display-P4\main\examples\lvgl_9_ui\win_music_play_pause_2_117x117px_rgb565a8.c:21` [flow_control] `#define LV_ATTRIBUTE_IMAGE_WIN_MUSIC_PLAY_PAUSE_2_117X117PX_RGB565A8`
- `T-Display-P4\main\examples\lvgl_9_ui\win_music_play_pause_2_117x117px_rgb565a8.c:24` [flow_control] `const LV_ATTRIBUTE_MEM_ALIGN LV_ATTRIBUTE_LARGE_CONST LV_ATTRIBUTE_IMAGE_WIN_MUSIC_PLAY_PAUSE_2_117X117PX_RGB565A8 uint8`
- `T-Display-P4\main\examples\lvgl_9_ui\win_music_play_pause_2_117x117px_rgb565a8.c:262` [flow_control] `const lv_image_dsc_t win_music_play_pause_2_117x117px_rgb565a8 = {`
- `T-Display-P4\main\examples\lvgl_9_ui\win_music_play_pause_2_117x117px_rgb565a8.c:268` [flow_control] `.data = win_music_play_pause_2_117x117px_rgb565a8_map,`
- `T-Display-P4\debug\examples\hi8561_ov5640\components\esp_video\src\esp_video.c:20` [memory_placement] `#define ALLOC_RAM_ATTR (MALLOC_CAP_8BIT | MALLOC_CAP_INTERNAL)`
- `T-Display-P4\debug\examples\hi8561_ov5640\components\esp_video\src\esp_video.c:193` [memory_placement] `struct esp_video_stream *IRAM_ATTR esp_video_get_stream(struct esp_video *video, enum v4l2_buf_type type)`
- `T-Display-P4\debug\examples\hi8561_ov5640\components\esp_video\src\esp_video.c:848` [memory_placement] `struct esp_video_buffer_element *IRAM_ATTR esp_video_get_queued_element(struct esp_video *video, uint32_t type)`
- `T-Display-P4\debug\examples\hi8561_ov5640\components\esp_video\src\esp_video.c:879` [memory_placement] `uint8_t *IRAM_ATTR esp_video_get_queued_buffer(struct esp_video *video, uint32_t type)`
- `T-Display-P4\debug\examples\hi8561_ov5640\components\esp_video\src\esp_video.c:933` [memory_placement] `esp_err_t IRAM_ATTR esp_video_done_element(struct esp_video *video, uint32_t type, struct esp_video_buffer_element *elem`
- `T-Display-P4\debug\examples\hi8561_ov5640\components\esp_video\src\esp_video.c:978` [memory_placement] `esp_err_t IRAM_ATTR esp_video_done_buffer(struct esp_video *video, uint32_t type, uint8_t *buffer, uint32_t n)`
- `T-Display-P4\debug\examples\hi8561_ov5640\components\esp_video\src\esp_video.c:1108` [memory_placement] `} else if (info->caps & MALLOC_CAP_INTERNAL) {`
- `T-Display-P4\debug\examples\hi8561_ov5640\components\esp_video\src\esp_video_buffer.c:127` [memory_placement] `struct esp_video_buffer_element *IRAM_ATTR esp_video_buffer_get_element_by_buffer(struct esp_video_buffer *buffer, uint8`
- `T-Display-P4\debug\examples\hi8561_ov5640\components\esp_video\src\esp_video_isp_pipeline.c:1099` [memory_placement] `StaticTask_t *task_ptr = heap_caps_malloc(sizeof(StaticTask_t), MALLOC_CAP_INTERNAL);`
- `T-Display-P4\debug\examples\hi8561_ov5640\components\esp_video\src\device\esp_video_csi_device.c:235` [memory_placement] `static bool IRAM_ATTR csi_video_on_trans_finished(esp_cam_ctlr_handle_t handle, esp_cam_ctlr_trans_t *trans, void *user_`
- `T-Display-P4\debug\examples\hi8561_ov5640\components\esp_video\src\device\esp_video_csi_device.c:253` [memory_placement] `static bool IRAM_ATTR csi_video_on_get_new_trans(esp_cam_ctlr_handle_t handle, esp_cam_ctlr_trans_t *trans, void *user_d`
- `T-Display-P4\debug\examples\hi8561_ov5640\components\esp_video\src\device\esp_video_csi_device.c:606` [memory_placement] `csi_video = heap_caps_calloc(1, sizeof(struct csi_video), MALLOC_CAP_8BIT | MALLOC_CAP_INTERNAL);`
- `T-Display-P4\debug\examples\hi8561_ov5640\components\esp_video\src\device\esp_video_dvp_device.c:100` [memory_placement] `static bool IRAM_ATTR dvp_video_on_trans_finished(esp_cam_ctlr_handle_t handle, esp_cam_ctlr_trans_t *trans, void *user_`
- `T-Display-P4\debug\examples\hi8561_ov5640\components\esp_video\src\device\esp_video_dvp_device.c:111` [memory_placement] `static bool IRAM_ATTR dvp_video_on_get_new_trans(esp_cam_ctlr_handle_t handle, esp_cam_ctlr_trans_t *trans, void *user_d`
- `T-Display-P4\debug\examples\hi8561_ov5640\components\esp_video\src\device\esp_video_dvp_device.c:430` [memory_placement] `dvp_video = heap_caps_calloc(1, sizeof(struct dvp_video), MALLOC_CAP_8BIT | MALLOC_CAP_INTERNAL);`
- `T-Display-P4\debug\examples\hi8561_ov5640\components\esp_video\src\device\esp_video_h264_device.c:466` [memory_placement] `h264_video = heap_caps_calloc(1, sizeof(struct h264_video), MALLOC_CAP_8BIT | MALLOC_CAP_INTERNAL);`
- `T-Display-P4\debug\examples\hi8561_ov5640\components\esp_video\src\device\esp_video_jpeg_device.c:394` [memory_placement] `jpeg_video = heap_caps_calloc(1, sizeof(struct jpeg_video), MALLOC_CAP_8BIT | MALLOC_CAP_INTERNAL);`
- `T-Display-P4\debug\examples\hi8561_ov5640\components\esp_video\src\data_reprocessing\esp32p4\esp_video_swap_byte.c:66` [memory_placement] `esp_err_t IRAM_ATTR esp_video_swap_byte_start(esp_video_swap_byte_t *swap_byte)`
- `T-Display-P4\debug\examples\gpio_interrupt\main\main.c:18` [memory_placement] `static void IRAM_ATTR exit_gpio_isr_handler(void *arg)`
- `T-Display-P4\debug\examples\esp32c6_at_host_sdio_uart\main\app_main.c:16` [sdio_bridge] `#include "sdio_host_log.h"`

## Detail par Sous-systeme

### afe_pipeline (21 matches)
- `T-Display-P4\main\examples\afe\main.cpp:14` `#include "esp_afe_sr_models.h"`

### codec_init (90 matches)
- `T-Display-P4\debug\examples\i2s_es8311\main\i2s_es8311_example.c:30` `static esp_err_t es8311_codec_init(void)`
- `T-Display-P4\main\examples\afe\main.cpp:205` `ES8311->begin(MCLK_MULTIPLE, SAMPLE_RATE, i2s_data_bit_width_t::I2S_DATA_BIT_WIDTH_16BIT);`

### encryption (201 matches)
- `T-Display-P4\debug\examples\hi8561_ov5640\components\esp_video\src\esp_video_isp_pipeline.c:335` `static void config_ccm(esp_video_isp_t *isp, esp_ipa_metadata_t *metadata)`

### ethernet (498 matches)
- `T-Display-P4\debug\examples\ethernet_iperf\main\cmd_ethernet.c:12` `#include "esp_eth.h"`

### flow_control (23 matches)
- `T-Display-P4\main\examples\lvgl_9_ui\win_music_play_pause_1_117x117px_rgb565a8.c:20` `#ifndef LV_ATTRIBUTE_IMAGE_WIN_MUSIC_PLAY_PAUSE_1_117X117PX_RGB565A8`
- `T-Display-P4\main\examples\lvgl_9_ui\win_music_play_pause_2_117x117px_rgb565a8.c:20` `#ifndef LV_ATTRIBUTE_IMAGE_WIN_MUSIC_PLAY_PAUSE_2_117X117PX_RGB565A8`

### hosted_init (1 matches)
- `T-Display-P4\main\examples\esp_hosted_mcu_sdio_wifi\main.cpp:139` `esp_err_t result = esp_hosted_init();`

### i2s_capture (33 matches)
- `T-Display-P4\debug\examples\i2s_es8311\main\i2s_es8311_example.c:170` `ret = i2s_channel_read(rx_handle, mic_data, EXAMPLE_RECV_BUF_SIZE, &bytes_read, 1000);`
- `T-Display-P4\debug\examples\uvc_sc2336\components\cpp_bus_driver\src\bus\iis\hardware_iis.cpp:194` `esp_err_t assert = i2s_channel_read(_chan_rx_handle, data, byte, &buffer, DEFAULT_CPP_BUS_DRIVER_IIS`
- `T-Display-P4\debug\examples\uvc_ov5645\components\cpp_bus_driver\src\bus\iis\hardware_iis.cpp:194` `esp_err_t assert = i2s_channel_read(_chan_rx_handle, data, byte, &buffer, DEFAULT_CPP_BUS_DRIVER_IIS`
- `T-Display-P4\debug\examples\uvc_ov2710\components\cpp_bus_driver\src\bus\iis\hardware_iis.cpp:194` `esp_err_t assert = i2s_channel_read(_chan_rx_handle, data, byte, &buffer, DEFAULT_CPP_BUS_DRIVER_IIS`
- `T-Display-P4\debug\examples\usb_extend_screen\components\cpp_bus_driver\src\bus\iis\hardware_iis.cpp:413` `esp_err_t assert = i2s_channel_read(_chan_rx_handle, data, byte, &buffer, DEFAULT_CPP_BUS_DRIVER_IIS`
- `T-Display-P4\debug\examples\sc2336(green_hue_error)\components\cpp_bus_driver-1.0.0\src\bus\iis\hardware_iis.cpp:194` `esp_err_t assert = i2s_channel_read(_chan_rx_handle, data, byte, &buffer, DEFAULT_CPP_BUS_DRIVER_IIS`

### i2s_driver (124 matches)
- `T-Display-P4\debug\examples\i2s_es8311\main\i2s_es8311_example.c:92` `ESP_ERROR_CHECK(i2s_channel_init_std_mode(tx_handle, &std_cfg));`
- `T-Display-P4\debug\examples\uvc_sc2336\components\cpp_bus_driver\src\bus\iis\hardware_iis.cpp:70` `assert = i2s_channel_init_std_mode(_chan_tx_handle, &std_config);`

### i2s_playback (37 matches)
- `T-Display-P4\debug\examples\i2s_es8311\main\i2s_es8311_example.c:128` `ret = i2s_channel_write(tx_handle, data_ptr, music_pcm_end - data_ptr, &bytes_write, portMAX_DELAY);`
- `T-Display-P4\debug\examples\uvc_sc2336\components\cpp_bus_driver\src\bus\iis\hardware_iis.cpp:213` `esp_err_t assert = i2s_channel_write(_chan_tx_handle, data, byte, &buffer, DEFAULT_CPP_BUS_DRIVER_II`
- `T-Display-P4\debug\examples\uvc_ov5645\components\cpp_bus_driver\src\bus\iis\hardware_iis.cpp:213` `esp_err_t assert = i2s_channel_write(_chan_tx_handle, data, byte, &buffer, DEFAULT_CPP_BUS_DRIVER_II`
- `T-Display-P4\debug\examples\uvc_ov2710\components\cpp_bus_driver\src\bus\iis\hardware_iis.cpp:213` `esp_err_t assert = i2s_channel_write(_chan_tx_handle, data, byte, &buffer, DEFAULT_CPP_BUS_DRIVER_II`
- `T-Display-P4\debug\examples\usb_extend_screen\components\cpp_bus_driver\src\bus\iis\hardware_iis.cpp:432` `esp_err_t assert = i2s_channel_write(_chan_tx_handle, data, byte, &buffer, DEFAULT_CPP_BUS_DRIVER_II`

### lora_radio (682 matches)
- `T-Display-P4\main\keyboard_examples\radiolib_cc1101_send_receive\main.cpp:2` `* @Description: radiolib_cc1101_send_receive`

### memory_placement (79 matches)
- `T-Display-P4\debug\examples\hi8561_ov5640\components\esp_video\src\esp_video.c:20` `#define ALLOC_RAM_ATTR (MALLOC_CAP_8BIT | MALLOC_CAP_INTERNAL)`
- `T-Display-P4\debug\examples\hi8561_ov5640\components\esp_video\src\esp_video_buffer.c:127` `struct esp_video_buffer_element *IRAM_ATTR esp_video_buffer_get_element_by_buffer(struct esp_video_b`
- `T-Display-P4\debug\examples\hi8561_ov5640\components\esp_video\src\esp_video_isp_pipeline.c:1099` `StaticTask_t *task_ptr = heap_caps_malloc(sizeof(StaticTask_t), MALLOC_CAP_INTERNAL);`
- `T-Display-P4\debug\examples\hi8561_ov5640\components\esp_video\src\device\esp_video_csi_device.c:235` `static bool IRAM_ATTR csi_video_on_trans_finished(esp_cam_ctlr_handle_t handle, esp_cam_ctlr_trans_t`

### psram_usage (73 matches)
- `T-Display-P4\debug\examples\video_lcd_display\main\main.c:45` `ESP_ERROR_CHECK(esp_cache_get_alignment(MALLOC_CAP_SPIRAM, &data_cache_line_size));`
- `T-Display-P4\debug\examples\hi8561_ov5640\components\esp_video\src\esp_video.c:1104` `if (info->caps & MALLOC_CAP_SPIRAM) {`
- `T-Display-P4\debug\examples\hi8561_ov5640\components\esp_video\src\esp_video_isp_pipeline.c:60` `#if CONFIG_ISP_PIPELINE_CONTROLLER_TASK_STACK_USE_PSRAM`

### sample_rate_config (485 matches)
- `T-Display-P4\debug\examples\i2s_es8311\main\i2s_es8311_example.c:56` `.sample_frequency = EXAMPLE_SAMPLE_RATE};`
- `T-Display-P4\main\examples\afe\main.cpp:25` `#define SAMPLE_RATE 16000`
- `T-Display-P4\main\examples\aw86224\main.cpp:64` `// AW86224->set_waveform_data_sample_rate(Cpp_Bus_Driver::Aw862xx::Sample_Rate::RATE_12KHZ);`
- `T-Display-P4\main\examples\deep_sleep\main.cpp:40` `#define SAMPLE_RATE 44100`

### sdio_bridge (33 matches)
- `T-Display-P4\debug\examples\esp32c6_at_host_sdio_uart\main\app_main.c:16` `#include "sdio_host_log.h"`
- `T-Display-P4\debug\examples\esp32c6_at_host_sdio_uart\components\sdio_host\sdio_host_transport.c:12` `#include "sdio_host_reg.h"`

### spi_bridge (187 matches)
- `T-Display-P4\debug\examples\ethernet_iperf\components\ethernet_init\ethernet_init.c:159` `ESP_GOTO_ON_ERROR(spi_bus_initialize(CONFIG_EXAMPLE_ETH_SPI_HOST, &buscfg, SPI_DMA_CH_AUTO),`
- `T-Display-P4\debug\examples\ethernet_basic\components\ethernet_init\ethernet_init.c:159` `ESP_GOTO_ON_ERROR(spi_bus_initialize(CONFIG_EXAMPLE_ETH_SPI_HOST, &buscfg, SPI_DMA_CH_AUTO),`

### sync_word (2141 matches)
- `T-Display-P4\main\examples\lvgl_9_ui\win_home_app_icon_camera_110x110px_rgb565a8.c:38` `0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00`

### synchronization (66 matches)
- `T-Display-P4\debug\examples\hi8561_ov5640\components\esp_video\src\esp_video.c:344` `video->mutex = xSemaphoreCreateMutex();`

### task_pinning (6 matches)
- `T-Display-P4\debug\examples\video_lcd_display\main\app_video.c:371` `BaseType_t result = xTaskCreatePinnedToCore(video_stream_task, "video stream task", VIDEO_TASK_STACK`
- `T-Display-P4\debug\examples\hi8561_ov5640\main\app_video.c:371` `BaseType_t result = xTaskCreatePinnedToCore(video_stream_task, "video stream task", VIDEO_TASK_STACK`
- `T-Display-P4\components\private_library\app_video.c:371` `BaseType_t result = xTaskCreatePinnedToCore(video_stream_task, "video stream task", VIDEO_TASK_STACK`
- `T-Display-P4\main\examples\afe\main.cpp:140` `xTaskCreatePinnedToCore(&feed_Task, "feed", 8 * 1024, (void *)afe_data, 5, NULL, 0);`
- `T-Display-P4\debug\examples\usb_extend_screen\main\app_vendor.cpp:151` `xTaskCreatePinnedToCore(transfer_task, "transfer_task", 4096, NULL, CONFIG_VENDOR_TASK_PRIORITY, NUL`

### task_priority (53 matches)
- `T-Display-P4\debug\examples\video_lcd_display\main\app_video.c:26` `#define VIDEO_TASK_PRIORITY             (4)`
- `T-Display-P4\debug\examples\hi8561_ov5640\main\app_video.c:26` `#define VIDEO_TASK_PRIORITY             (4)`
- `T-Display-P4\debug\examples\hi8561_ov5640\components\esp_video\src\esp_video_isp_pipeline.c:33` `#define ISP_TASK_PRIORITY           11`
- `T-Display-P4\debug\examples\hi8561_ov5640\components\esp_video\src\device\esp_video_isp_device.c:804` `.intr_priority = 0,`
- `T-Display-P4\debug\examples\hi8561_ov5640\components\esp_video\src\device\esp_video_jpeg_device.c:120` `.intr_priority = 0,`
- `T-Display-P4\components\private_library\app_video.c:26` `#define VIDEO_TASK_PRIORITY             (4)`
- `T-Display-P4\components\esp_video\src\esp_video_isp_pipeline.c:33` `#define ISP_TASK_PRIORITY           11`
- `T-Display-P4\components\esp_video\src\device\esp_video_isp_device.c:804` `.intr_priority = 0,`
- `T-Display-P4\components\esp_video\src\device\esp_video_jpeg_device.c:120` `.intr_priority = 0,`
- `T-Display-P4\debug\examples\uvc_sc2336\components\cpp_bus_driver\src\bus\iic\hardware_iic_1.cpp:36` `.intr_priority = 0,                // 设置中断优先级`

### timestamp (128 matches)
- `T-Display-P4\debug\examples\video_lcd_display\main\main.c:92` `start_time = esp_timer_get_time();  // Get the initial time for frame rate statistics`
- `T-Display-P4\debug\examples\hi8561_ov5640\components\esp_video\src\data_reprocessing\esp32p4\esp_video_swap_short.c:132` `int64_t start_time_us = esp_timer_get_time();`
- `T-Display-P4\debug\examples\hi8561_ov5640\components\esp_video\examples\video_custom_format\main\app_main.c:219` `int64_t start_time_us = esp_timer_get_time();`
- `T-Display-P4\debug\examples\hi8561_ov5640\components\esp_video\examples\uvc\main\uvc_example.c:426` `us = esp_timer_get_time();`
- `T-Display-P4\debug\examples\hi8561_ov5640\components\esp_video\examples\image_storage\usb_msc\main\tusb_msc_main.c:593` `us = esp_timer_get_time();`

### transport_queue (9 matches)
- `T-Display-P4\main\examples\tusb_serial_device\main.c:84` `app_queue = xQueueCreate(5, sizeof(app_message_t));`
- `T-Display-P4\debug\examples\usb_extend_screen\main\app_hid.c:81` `s_tinyusb_hid->hid_queue = xQueueCreate(10, sizeof(hid_report_t));   // Adjust queue length and item`
- `T-Display-P4\debug\examples\usb_extend_screen\main\usb_frame.c:29` `empty_fb_queue = xQueueCreate(nb_of_fb, sizeof(frame_t *));`
- `T-Display-P4\main\examples\esp_hosted_mcu_sdio_wifi\main.cpp:102` `config->u.sdio.tx_queue_size, config->u.sdio.rx_queue_size);`
- `T-Display-P4\main\examples\lvgl_9_ui\main.cpp:3960` `app_queue = xQueueCreate(5, sizeof(app_message_t));`

### vad_detection (1 matches)
- `T-Display-P4\main\examples\afe\main.cpp:91` `printf("vad state: %d\n", res->vad_state);`

### wake_word (20 matches)
- `T-Display-P4\main\examples\afe\main.cpp:72` `// modify wakenet detection threshold`

### watchdog (27 matches)
- `T-Display-P4\main\keyboard_examples\bq25896\main.cpp:45` `Kode_Bq25896::bq25896_set_watchdog_timer(Bq25896_Handle, Kode_Bq25896::bq25896_watchdog_t::BQ25896_W`
- `T-Display-P4\main\examples\lvgl_9_ui\main.cpp:4973` `Kode_Bq25896::bq25896_set_watchdog_timer(Bq25896_Handle, Kode_Bq25896::bq25896_watchdog_t::BQ25896_W`
- `T-Display-P4\debug\examples\usb_extend_screen\components\cpp_bus_driver\src\chip\iic\sgm41562xx.cpp:148` `status.watchdog_expiration_flag = (chip_flag & 0B00100000) >> 5;`
- `T-Display-P4\debug\examples\iperf\components\cpp_bus_driver\src\chip\iic\sgm41562xx.cpp:148` `status.watchdog_expiration_flag = (chip_flag & 0B00100000) >> 5;`
- `T-Display-P4\debug\examples\hi8561_touch_debug\components\cpp_bus_driver-1.0.0\src\chip\spi\sx126x.cpp:76` `_watchdog_busy = 0;`

### wifi_power_save (29 matches)
- `T-Display-P4\debug\examples\uvc_sc2336\components\cpp_bus_driver\src\chip\sdio\esp_at.cpp:98` `case Sleep_Mode::MODEM_SLEEP:`
- `T-Display-P4\debug\examples\uvc_ov5645\components\cpp_bus_driver\src\chip\sdio\esp_at.cpp:98` `case Sleep_Mode::MODEM_SLEEP:`
- `T-Display-P4\debug\examples\uvc_ov2710\components\cpp_bus_driver\src\chip\sdio\esp_at.cpp:98` `case Sleep_Mode::MODEM_SLEEP:`
- `T-Display-P4\debug\examples\usb_extend_screen\components\cpp_bus_driver\src\chip\iic\aw21009xxx.cpp:61` `bool Aw21009xxx::set_auto_power_save(bool enable)`
- `T-Display-P4\debug\examples\usb_extend_screen\components\cpp_bus_driver\src\chip\sdio\esp_at.cpp:98` `case Sleep_Mode::MODEM_SLEEP:`
- `T-Display-P4\debug\examples\rm69a10_lvgl\components\cpp_bus_driver\src\chip\sdio\esp_at.cpp:98` `case Sleep_Mode::MODEM_SLEEP:`

### wifi_remote (1 matches)
- `T-Display-P4\main\examples\esp_hosted_mcu_sdio_wifi\main.cpp:18` `#include "esp_wifi_remote.h"`