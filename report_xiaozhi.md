# Rapport d'Analyse: Xiaozhi-ESP32 (Voice Assistant)
**Projet:** `xiaozhi`

## Statistiques
- Fichiers scannes: 317
- Fichiers avec matches: 205
- Lignes totales: 17676
- Matches total: 512

## Distribution par Categorie
- **audio**: 364 ??????????????????????????????????????????????????
- **mesh**: 52 ??????????????????????????????????????????????????
- **network**: 34 ??????????????????????????????????
- **timing**: 25 ?????????????????????????
- **transport**: 18 ??????????????????
- **memory**: 14 ??????????????
- **rtos**: 5 ?????

## ??  Findings Critiques (CRITICAL)
- `xiaozhi-esp32\main\audio\audio_codec.h:14` [dma_buffer] `#define AUDIO_CODEC_DMA_DESC_NUM 6`
- `xiaozhi-esp32\main\audio\audio_codec.h:15` [dma_buffer] `#define AUDIO_CODEC_DMA_FRAME_NUM 240`
- `xiaozhi-esp32\main\audio\audio_service.h:16` [opus_encode] `#include "esp_opus_enc.h"`
- `xiaozhi-esp32\main\audio\audio_service.h:56` [opus_encode] `((duration_ms) == 5 ? ESP_OPUS_ENC_FRAME_DURATION_5_MS :      \`
- `xiaozhi-esp32\main\audio\audio_service.h:57` [opus_encode] `(duration_ms) == 10 ? ESP_OPUS_ENC_FRAME_DURATION_10_MS :    \`
- `xiaozhi-esp32\main\audio\audio_service.h:58` [opus_encode] `(duration_ms) == 20 ? ESP_OPUS_ENC_FRAME_DURATION_20_MS :    \`
- `xiaozhi-esp32\main\audio\audio_service.h:59` [opus_encode] `(duration_ms) == 40 ? ESP_OPUS_ENC_FRAME_DURATION_40_MS :    \`
- `xiaozhi-esp32\main\audio\audio_service.h:60` [opus_encode] `(duration_ms) == 60 ? ESP_OPUS_ENC_FRAME_DURATION_60_MS :    \`
- `xiaozhi-esp32\main\audio\audio_service.h:61` [opus_encode] `(duration_ms) == 80 ? ESP_OPUS_ENC_FRAME_DURATION_80_MS :    \`
- `xiaozhi-esp32\main\audio\audio_service.h:62` [opus_encode] `(duration_ms) == 100 ? ESP_OPUS_ENC_FRAME_DURATION_100_MS :  \`
- `xiaozhi-esp32\main\audio\audio_service.h:63` [opus_encode] `(duration_ms) == 120 ? ESP_OPUS_ENC_FRAME_DURATION_120_MS : -1)`
- `xiaozhi-esp32\main\audio\audio_service.h:65` [opus_encode] `#define AS_OPUS_ENC_CONFIG() {                                                                                    \`
- `xiaozhi-esp32\main\audio\audio_service.h:70` [opus_encode] `.frame_duration     = (esp_opus_enc_frame_duration_t)AS_OPUS_GET_FRAME_DRU_ENUM(OPUS_FRAME_DURATION_MS),  \`
- `xiaozhi-esp32\main\audio\audio_service.h:71` [opus_encode] `.application_mode   = ESP_OPUS_ENC_APPLICATION_AUDIO,                                                     \`
- `xiaozhi-esp32\main\audio\audio_service.h:143` [opus_encode] `void* opus_encoder_ = nullptr;`
- `xiaozhi-esp32\main\led\gpio_led.h:46` [memory_placement] `static bool IRAM_ATTR FadeCallback(const ledc_cb_param_t *param, void *user_arg);`
- `xiaozhi-esp32\main\boards\m5stack-cardputer-adv\tca8418_keyboard.h:151` [memory_placement] `static void IRAM_ATTR GpioIsrHandler(void* arg);`
- `xiaozhi-esp32\main\boards\nulllab-ai-vox-v3\ai_vox3_audio_codec.h:32` [dma_buffer] `.dma_desc_num = AUDIO_CODEC_DMA_DESC_NUM,`
- `xiaozhi-esp32\main\boards\nulllab-ai-vox-v3\ai_vox3_audio_codec.h:33` [dma_buffer] `.dma_frame_num = AUDIO_CODEC_DMA_FRAME_NUM,`
- `xiaozhi-esp32\main\boards\otto-robot\otto_movements.h:74` [jitter_buffer] `void Jitter(float steps = 1, int period = 500, int height = 20);`
- `xiaozhi-esp32\main\boards\otto-robot\power_manager.h:28` [flow_control] `inline static bool battery_update_paused_ = false;  // 静态标志：是否暂停电量更新`
- `xiaozhi-esp32\main\boards\otto-robot\power_manager.h:34` [flow_control] `if (battery_update_paused_) {`
- `xiaozhi-esp32\main\boards\otto-robot\power_manager.h:148` [flow_control] `static void PauseBatteryUpdate() { battery_update_paused_ = true; }`
- `xiaozhi-esp32\main\boards\otto-robot\power_manager.h:149` [flow_control] `static void ResumeBatteryUpdate() { battery_update_paused_ = false; }`
- `xiaozhi-esp32\main\boards\lceda-course-examples\eda-super-bear\eda_super_bear_movements.h:71` [jitter_buffer] `void Jitter(float steps = 1, int period = 500, int height = 20);`
- `xiaozhi-esp32\main\display\lvgl_display\gif\lvgl_gif.h:27` [flow_control] `* Pause GIF animation`
- `xiaozhi-esp32\main\display\lvgl_display\gif\lvgl_gif.h:29` [flow_control] `void Pause();`

## Detail par Sous-systeme

### afe_pipeline (6 matches)
- `xiaozhi-esp32\main\audio\processors\afe_audio_processor.h:4` `#include <esp_afe_sr_models.h>`
- `xiaozhi-esp32\main\audio\wake_words\afe_wake_word.h:8` `#include <esp_afe_sr_models.h>`

### dma_buffer (4 matches)
- `xiaozhi-esp32\main\audio\audio_codec.h:14` `#define AUDIO_CODEC_DMA_DESC_NUM 6`
- `xiaozhi-esp32\main\boards\nulllab-ai-vox-v3\ai_vox3_audio_codec.h:32` `.dma_desc_num = AUDIO_CODEC_DMA_DESC_NUM,`

### encryption (26 matches)
- `xiaozhi-esp32\main\boards\common\blufi.cpp:361` `m_sec->aes = new mbedtls_aes_context();`

### ethernet (3 matches)
- `xiaozhi-esp32\main\boards\common\nt26_board.h:5` `#include <uart_eth_modem.h>`
- `xiaozhi-esp32\main\boards\common\rndis_board.h:10` `#include "iot_eth_netif_glue.h"`

### flow_control (6 matches)
- `xiaozhi-esp32\main\boards\otto-robot\power_manager.h:28` `inline static bool battery_update_paused_ = false;  // 静态标志：是否暂停电量更新`
- `xiaozhi-esp32\main\display\lvgl_display\gif\lvgl_gif.h:27` `* Pause GIF animation`

### i2s_driver (2 matches)
- `xiaozhi-esp32\main\boards\nulllab-ai-vox-v3\ai_vox3_audio_codec.h:58` `ESP_ERROR_CHECK(i2s_channel_init_std_mode(tx_handle_, &std_cfg));`

### jitter_buffer (2 matches)
- `xiaozhi-esp32\main\boards\otto-robot\otto_movements.h:74` `void Jitter(float steps = 1, int period = 500, int height = 20);`
- `xiaozhi-esp32\main\boards\lceda-course-examples\eda-super-bear\eda_super_bear_movements.h:71` `void Jitter(float steps = 1, int period = 500, int height = 20);`

### lora_radio (8 matches)
- `xiaozhi-esp32\main\boards\lilygo-t-display-p4\t_display_p4_config.h:39` `#define XL9535_SX1262_RST Cpp_Bus_Driver::Xl95x5::Pin::IO16`

### memory_placement (2 matches)
- `xiaozhi-esp32\main\led\gpio_led.h:46` `static bool IRAM_ATTR FadeCallback(const ledc_cb_param_t *param, void *user_arg);`
- `xiaozhi-esp32\main\boards\m5stack-cardputer-adv\tca8418_keyboard.h:151` `static void IRAM_ATTR GpioIsrHandler(void* arg);`

### mqtt (15 matches)
- `xiaozhi-esp32\main\ota.h:19` `bool HasMqttConfig() { return has_mqtt_config_; }`
- `xiaozhi-esp32\main\protocols\mqtt_protocol.h:1` `#ifndef MQTT_PROTOCOL_H`

### opus_decode (2 matches)
- `xiaozhi-esp32\main\audio\audio_service.h:17` `#include "esp_opus_dec.h"`

### opus_encode (13 matches)
- `xiaozhi-esp32\main\audio\audio_service.h:16` `#include "esp_opus_enc.h"`

### psram_usage (12 matches)
- `xiaozhi-esp32\main\display\lvgl_display\jpg\image_to_jpeg.cpp:19` `static void* malloc_psram(size_t size) {`

### sample_rate_config (328 matches)
- `xiaozhi-esp32\main\audio\audio_codec.h:33` `inline int input_sample_rate() const { return input_sample_rate_; }`
- `xiaozhi-esp32\main\audio\audio_service.h:66` `.sample_rate        = ESP_AUDIO_SAMPLE_RATE_16K,                                                    `
- `xiaozhi-esp32\main\protocols\protocol.h:11` `int sample_rate = 0;`

### spi_bridge (10 matches)
- `xiaozhi-esp32\main\boards\freenove-esp32s3-display-2.8-lcd\config.h:38` `#define LCD_SPI_HOST          SPI3_HOST`
- `xiaozhi-esp32\main\boards\movecall-moji2-esp32c5\config.h:46` `#define DISPLAY_QSPI_HOST           SPI2_HOST`
- `xiaozhi-esp32\main\boards\wireless-tag-wtp4c5mp07s\config.h:84` `#ifndef SDCARD_SPI_HOST`
- `xiaozhi-esp32\main\boards\xingzhi-abs-2.0\config.h:35` `#define SD_SPI_HOST SPI2_HOST`
- `xiaozhi-esp32\main\boards\xingzhi-metal-1.54-wifi\config.h:28` `#define DISPLAY_SPI_HOST SPI3_HOST`
- `xiaozhi-esp32\main\boards\waveshare\esp32-s3-epaper-1.54\custom_lcd_display.h:21` `int spi_host;`
- `xiaozhi-esp32\main\boards\waveshare\esp32-s3-epaper-3.97\custom_lcd_display.h:21` `int spi_host;`
- `xiaozhi-esp32\main\boards\waveshare\esp32-s3-rlcd-4.2\custom_lcd_display.h:49` `bool mirror_x, bool mirror_y, bool swap_xy,spi_display_config_t spiconfig,spi_host_device_t spi_host`

### sync_word (18 matches)
- `xiaozhi-esp32\main\boards\jiuchuan-s3\esp_lcd_panel_gc9301.c:49` `#define GC9309NA_CMD_RASET         0x2B`
- `xiaozhi-esp32\main\boards\waveshare\esp32-s3-audio-board\esp_lcd_jd9853.c:252` `{0xC8, (uint8_t[]){0x3F, 0x32, 0x29, 0x29, 0x27, 0x2B, 0x27, 0x28, 0x28, 0x26, 0x25, 0x17, 0x12, 0x0`
- `xiaozhi-esp32\main\boards\m5stack-cardputer-adv\tca8418_keyboard.h:73` `KC_TAB = 0x2B,`
- `xiaozhi-esp32\main\boards\m5stack-tab5\config.h:101` `{0x2b, (uint8_t[]){0x00}, 1, 0},`
- `xiaozhi-esp32\main\boards\waveshare\esp32-p4-nano\lcd_init_cmds.h:133` `{0x2B, (uint8_t[]){0x5F}, 1, 0},`
- `xiaozhi-esp32\main\boards\waveshare\esp32-p4-wifi6-touch-lcd\lcd_init_cmds.h:42` `{0xE8, (uint8_t[]){0x08, 0x2D, 0xA0, 0xA0, 0x0A, 0x2F, 0xA0, 0xA0, 0x04, 0x29, 0xA0, 0xA0, 0x06, 0x2`

### task_priority (5 matches)
- `xiaozhi-esp32\main\display\lvgl_display\jpg\jpeg_to_image.c:116` `.intr_priority = 1,`
- `xiaozhi-esp32\main\display\lvgl_display\jpg\image_to_jpeg.cpp:203` `.intr_priority = 0,`
- `xiaozhi-esp32\main\boards\nulllab-ai-vox-v3\ai_vox3_audio_codec.h:35` `.intr_priority = 0,`
- `xiaozhi-esp32\main\boards\sensecap-watcher\config.h:15` `#define CONFIG_SSCMA_PROCESS_TASK_PRIORITY 5`

### timestamp (25 matches)
- `xiaozhi-esp32\main\protocols\protocol.h:21` `uint32_t timestamp;     // Timestamp in milliseconds (used for server-side AEC)`
- `xiaozhi-esp32\main\boards\electron-bot\oscillator.h:67` `long previous_millis_;`
- `xiaozhi-esp32\main\boards\esp-s3-lcd-ev-board\esp_lcd_gc9503.h:30` `unsigned int delay_ms;  /*<! Delay in milliseconds after this command */`
- `xiaozhi-esp32\main\boards\esp-s3-lcd-ev-board-2\esp_lcd_gc9503.h:30` `unsigned int delay_ms;  /*<! Delay in milliseconds after this command */`
- `xiaozhi-esp32\main\boards\kevin-yuying-313lcd\esp_lcd_gc9503.h:30` `unsigned int delay_ms;  /*<! Delay in milliseconds after this command */`
- `xiaozhi-esp32\main\boards\lilygo-t-circle-s3\esp_lcd_gc9d01n.h:17` `unsigned int delay_ms;  /*<! Delay in milliseconds after this command */`
- `xiaozhi-esp32\main\boards\lilygo-t-display-p4\hi8561_driver.h:26` `unsigned int delay_ms; /*<! Delay in milliseconds after this command */`
- `xiaozhi-esp32\main\boards\lilygo-t-display-p4\rm69a10_driver.h:26` `unsigned int delay_ms; /*<! Delay in milliseconds after this command */`

### vad_detection (2 matches)
- `xiaozhi-esp32\main\audio\processors\afe_audio_processor.h:37` `std::function<void(bool speaking)> vad_state_change_callback_;`
- `xiaozhi-esp32\main\audio\processors\no_audio_processor.h:31` `std::function<void(bool speaking)> vad_state_change_callback_;`

### wake_word (5 matches)
- `xiaozhi-esp32\main\audio\wake_words\afe_wake_word.h:41` `char* wakenet_model_ = NULL;`
- `xiaozhi-esp32\main\audio\wake_words\custom_wake_word.h:68` `void ParseWakenetModelConfig();`
- `xiaozhi-esp32\main\audio\wake_words\esp_wake_word.h:33` `esp_wn_iface_t *wakenet_iface_ = nullptr;`

### websocket (16 matches)
- `xiaozhi-esp32\main\ota.h:20` `bool HasWebsocketConfig() { return has_websocket_config_; }`
- `xiaozhi-esp32\main\protocols\websocket_protocol.h:1` `#ifndef _WEBSOCKET_PROTOCOL_H_`
- `xiaozhi-esp32\main\boards\otto-robot\websocket_control_server.h:1` `#ifndef WEBSOCKET_CONTROL_SERVER_H`

### wifi_power_save (2 matches)
- `xiaozhi-esp32\main\boards\common\button.h:14` `Button(gpio_num_t gpio_num, bool active_high = false, uint16_t long_press_time = 0, uint16_t short_p`
- `xiaozhi-esp32\main\boards\common\power_save_timer.h:22` `esp_timer_handle_t power_save_timer_ = nullptr;`