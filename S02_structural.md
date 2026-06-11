# Script 02: Extraction Structurelle


## esp-adf (80 fichiers)

| Keyword | Fichiers |
|---|---|
| audio | 69 |
| stream | 51 |
| codec | 44 |
| i2s | 34 |
| task | 33 |
| buffer | 23 |
| wifi | 17 |
| ringbuf | 12 |
| queue | 7 |
| opus | 5 |
| es8311 | 5 |
| afe | 4 |
| vad | 2 |
| wakenet | 1 |
| udp | 1 |

### Top fichiers

- `micropython_adf\mod\audio_player.c` → task, stream, i2s, codec, audio
- `micropython_adf\mod\audio_recorder.c` → task, stream, i2s, codec, audio
- `micropython_adf\mod\modaudio.c` → codec, audio, stream
- `micropython_adf\mod\modaudio.h` → audio
- `micropython_adf\mod\vfs_stream.c` → task, opus, buffer, stream, audio
- `micropython_adf\mod\vfs_stream.h` → task, buffer, stream, ringbuf, audio
- `micropython_adf\boards\include\board_init.h` → codec, audio
- `micropython_adf\boards\korvo2v3\board_init.c` → codec, es8311, audio
- `micropython_adf\boards\korvo2v3\mpconfigboard.h` → audio
- `micropython_adf\boards\lyrat43\board_init.c` → codec, audio
- `micropython_adf\boards\lyrat43\mpconfigboard.h` → audio
- `micropython_adf\boards\lyratmini\board_init.c` → codec, es8311, audio
- `micropython_adf\boards\lyratmini\mpconfigboard.h` → audio
- `examples\system\wpa2_enterprise\main\wpa2_enterprise_example.c` → wifi, audio, task
- `examples\system\power_save\main\audio_power_save.c` → task, stream, i2s, wifi, codec, audio

## esp-sr (80 fichiers)

| Keyword | Fichiers |
|---|---|
| audio | 45 |
| queue | 24 |
| wakenet | 22 |
| task | 21 |
| buffer | 19 |
| stream | 17 |
| afe | 15 |
| vad | 15 |
| ringbuf | 7 |
| dma | 6 |
| i2s | 3 |

### Top fichiers

- `src\esp_process_sdkconfig.c` → afe
- `test_apps\esp32c5\main\app_main.cpp` → task
- `test_apps\esp32c5\main\audio_test_file.h` → audio
- `test_apps\esp32c5\main\test_aec.cpp` → vad, task, buffer, audio, afe
- `test_apps\esp32c5\main\test_wakenet.cpp` → wakenet, queue, task, buffer, audio
- `test_apps\esp-tts\main\app_main.cpp` → task
- `test_apps\esp-tts\main\test_chinese_tts.c` → task
- `test_apps\esp-tts\main\test_chinese_tts.cpp` → task
- `test_apps\esp-sr\main\app_main.cpp` → task
- `test_apps\esp-sr\main\test_afe.cpp` → wakenet, vad, task, queue, i2s, audio, afe
- `test_apps\esp-sr\main\test_mfcc.cpp` → buffer
- `test_apps\esp-sr\main\test_multinet.cpp` → audio, buffer, queue, task
- `test_apps\esp-sr\main\test_vadnet.cpp` → vad, queue, task, buffer, audio
- `test_apps\esp-sr\main\test_wakenet.cpp` → wakenet, queue, task, buffer, audio
- `test_apps\esp-sr\main\samples\audio_test_file.h` → audio

## esp-hosted (80 fichiers)

| Keyword | Fichiers |
|---|---|
| buffer | 49 |
| sdio | 34 |
| queue | 31 |
| wifi | 28 |
| task | 24 |
| stream | 9 |
| dma | 8 |
| esp_hosted | 3 |
| spi_slave | 1 |
| flow_control | 1 |
| ringbuf | 1 |

### Top fichiers

- `esp_hosted_ng\host\esp_bt.c` → buffer, sdio
- `esp_hosted_ng\host\esp_cfg80211.c` → wifi, queue
- `esp_hosted_ng\host\esp_cmd.c` → wifi, buffer, queue, task
- `esp_hosted_ng\host\esp_debugfs.c` → buffer
- `esp_hosted_ng\host\esp_stats.c` → wifi, queue, task
- `esp_hosted_ng\host\esp_utils.c` → wifi
- `esp_hosted_ng\host\main.c` → queue, task, buffer, sdio, wifi
- `esp_hosted_ng\host\include\adapter.h` → wifi, sdio, queue, dma
- `esp_hosted_ng\host\include\esp.h` → wifi, queue, sdio
- `esp_hosted_ng\host\include\esp_api.h` → wifi, queue, sdio
- `esp_hosted_ng\host\include\esp_cfg80211.h` → wifi
- `esp_hosted_ng\host\include\esp_cmd.h` → wifi, task
- `esp_hosted_ng\host\include\esp_kernel_port.h` → queue
- `esp_hosted_ng\host\include\esp_stats.h` → queue
- `esp_hosted_ng\host\include\esp_utils.h` → wifi

## xiaozhi (80 fichiers)

| Keyword | Fichiers |
|---|---|
| audio | 52 |
| codec | 33 |
| i2s | 33 |
| task | 21 |
| es8311 | 16 |
| buffer | 12 |
| stream | 9 |
| wifi | 8 |
| vad | 4 |
| afe | 4 |
| dma | 3 |
| queue | 3 |
| opus | 3 |
| udp | 2 |

### Top fichiers

- `main\application.h` → audio, vad, task, afe
- `main\device_state.h` → wifi, audio
- `main\system_info.h` → task
- `main\audio\audio_codec.h` → dma, codec, audio, i2s
- `main\audio\audio_processor.h` → codec, audio, vad
- `main\audio\audio_service.h` → queue, task, vad, opus, stream, codec, audio, afe
- `main\audio\wake_word.h` → codec, opus, audio
- `main\led\circular_strip.h` → task
- `main\led\gpio_led.h` → task
- `main\led\single_led.h` → task
- `main\protocols\mqtt_protocol.h` → udp, audio, stream, afe
- `main\protocols\protocol.h` → opus, audio, stream
- `main\protocols\websocket_protocol.h` → audio, stream
- `main\display\lvgl_display\gif\gifdec.c` → buffer
- `main\display\lvgl_display\gif\gifdec.h` → buffer

## xiaozhi-server (0 fichiers)

| Keyword | Fichiers |
|---|---|

### Top fichiers


## esp32-aichats (0 fichiers)

| Keyword | Fichiers |
|---|---|

### Top fichiers


## ha_voice (40 fichiers)

| Keyword | Fichiers |
|---|---|
| buffer | 21 |
| audio | 21 |
| task | 18 |
| codec | 13 |
| afe | 13 |
| i2s | 12 |
| wifi | 12 |
| vad | 10 |
| stream | 7 |
| es8311 | 4 |
| queue | 4 |
| sdio | 3 |
| wakenet | 2 |
| dma | 2 |
| ringbuf | 1 |
| esp_hosted | 1 |

### Top fichiers

- `main\alarm_manager.c` → task
- `main\audio_capture.c` → wakenet, vad, task, buffer, stream, i2s, codec, audio, afe
- `main\audio_capture.h` → es8311, vad, task, buffer, stream, codec, audio, afe
- `main\audio_ref_buffer.c` → buffer, ringbuf, stream, audio, afe
- `main\audio_ref_buffer.h` → audio, buffer, i2s, afe
- `main\beep_tone.c` → codec, audio, buffer, i2s
- `main\beep_tone.h` → audio
- `main\ha_client.c` → task, buffer, stream, audio, afe
- `main\ha_client.h` → audio, buffer, stream
- `main\led_status.c` → task
- `main\local_music_player.c` → codec, audio, queue, i2s
- `main\local_music_player.h` → wifi, buffer
- `main\main.c` → vad, task, i2s, wifi, codec, audio, afe
- `main\mqtt_ha.c` → wifi, vad, queue
- `main\mqtt_ha.h` → wifi, vad

## ESP32_Voice_Assistant (1 fichiers)

| Keyword | Fichiers |
|---|---|
| wifi | 1 |

### Top fichiers

- `esp-code\secrets.example.h` → wifi

## client-sdk-esp32 (52 fichiers)

| Keyword | Fichiers |
|---|---|
| audio | 28 |
| stream | 24 |
| codec | 23 |
| buffer | 15 |
| opus | 10 |
| i2s | 9 |
| afe | 4 |
| task | 4 |
| jitter | 3 |
| queue | 2 |
| es8311 | 2 |
| udp | 1 |
| wifi | 1 |

### Top fichiers

- `components\third_party\nanopb\include\pb.h` → buffer, stream
- `components\third_party\nanopb\include\pb_decode.h` → buffer, stream
- `components\third_party\nanopb\include\pb_encode.h` → buffer, stream
- `components\third_party\nanopb\src\pb_common.c` → stream
- `components\third_party\nanopb\src\pb_decode.c` → buffer, stream, afe
- `components\third_party\nanopb\src\pb_encode.c` → buffer, stream, afe
- `components\sandbox_token\src\livekit_sandbox.c` → buffer
- `components\livekit\core\common.h` → audio, stream
- `components\livekit\core\data_stream_reader.c` → stream
- `components\livekit\core\data_stream_reader.h` → stream
- `components\livekit\core\data_stream_writer.c` → stream
- `components\livekit\core\data_stream_writer.h` → stream
- `components\livekit\core\engine.c` → queue, task, opus, buffer, stream, codec, audio, afe
- `components\livekit\core\livekit.c` → codec, opus, audio, stream
- `components\livekit\core\peer.c` → codec, audio, stream, task

## stream-video-esp32 (48 fichiers)

| Keyword | Fichiers |
|---|---|
| stream | 38 |
| audio | 17 |
| codec | 14 |
| buffer | 10 |
| i2s | 7 |
| task | 6 |
| udp | 3 |
| es8311 | 3 |
| opus | 3 |
| dma | 2 |
| queue | 2 |
| wifi | 1 |

### Top fichiers

- `examples\minimal\main\app_token.c` → buffer, stream
- `examples\minimal\main\app_token.h` → stream
- `examples\minimal\main\main.c` → task, stream, wifi, udp, audio
- `examples\minimal\components\codec_board\cfg_parse.c` → codec, es8311, i2s
- `examples\minimal\components\codec_board\codec_board.c` → codec, i2s
- `examples\minimal\components\codec_board\codec_init.c` → es8311, dma, i2s, codec, audio
- `examples\minimal\components\codec_board\dummy_codec.c` → codec, audio
- `examples\minimal\components\codec_board\dummy_codec.h` → codec, audio, i2s
- `examples\minimal\components\codec_board\lcd_init.c` → codec, task, queue, dma
- `examples\minimal\components\codec_board\drv\tca9554.c` → codec, audio
- `examples\minimal\components\codec_board\drv\tca9554.h` → codec
- `examples\minimal\components\codec_board\include\codec_board.h` → codec, es8311, i2s
- `examples\minimal\components\codec_board\include\codec_init.h` → codec, i2s
- `components\stream-video\generated\models.pb.c` → codec, audio, stream
- `components\stream-video\generated\models.pb.h` → codec, audio, stream

## ESP32-audioI2S (50 fichiers)

| Keyword | Fichiers |
|---|---|
| audio | 34 |
| stream | 30 |
| buffer | 23 |
| i2s | 16 |
| codec | 14 |
| task | 13 |
| opus | 12 |
| afe | 11 |
| wifi | 7 |
| dma | 6 |
| vad | 5 |
| queue | 3 |
| ringbuf | 3 |
| es8311 | 3 |

### Top fichiers

- `src\Audio.cpp` → queue, dma, task, opus, buffer, stream, i2s, codec, audio, afe
- `src\Audio.h` → queue, dma, task, opus, buffer, stream, i2s, wifi, codec, audio
- `src\audiolib_structs.hpp` → queue, opus, buffer, stream, i2s, audio
- `src\psram_unique_ptr.hpp` → buffer, stream, codec, audio, afe
- `src\aac_decoder\aac_decoder.cpp` → audio, stream
- `src\aac_decoder\aac_decoder.h` → audio, stream
- `src\flac_decoder\flac_decoder.cpp` → audio, buffer, stream, dma
- `src\flac_decoder\flac_decoder.h` → audio, buffer, stream, dma
- `src\mp3_decoder\mp3_decoder.cpp` → audio, buffer, stream, afe
- `src\mp3_decoder\mp3_decoder.h` → audio, stream
- `src\mp3_decoder\structs.h` → buffer, stream
- `src\mp3_decoder\tables.h` → stream
- `src\opus_decoder\celt.cpp` → opus, buffer, stream
- `src\opus_decoder\celt.h` → opus, audio
- `src\opus_decoder\celt_defines.h` → opus, buffer

## esp32_opus (80 fichiers)

| Keyword | Fichiers |
|---|---|
| opus | 78 |
| buffer | 21 |
| stream | 11 |
| vad | 9 |
| audio | 8 |
| afe | 6 |
| codec | 6 |

### Top fichiers

- `src\A2NLSF.c` → opus
- `src\analysis.c` → vad, opus, buffer, audio, afe
- `src\analysis.h` → opus, buffer
- `src\ana_filt_bank_1.c` → opus
- `src\API.h` → audio, opus, buffer, vad
- `src\apply_sine_window_FIX.c` → opus
- `src\arch.h` → opus, afe
- `src\autocorr_FIX.c` → opus
- `src\bands.c` → opus, stream
- `src\bands.h` → opus
- `src\biquad_alt.c` → opus
- `src\burg_modified_FIX.c` → opus
- `src\bwexpander.c` → opus
- `src\bwexpander_32.c` → opus
- `src\celt.c` → opus, buffer, stream

## meshcore (80 fichiers)

| Keyword | Fichiers |
|---|---|
| buffer | 51 |
| task | 39 |
| sdio | 16 |
| dma | 14 |
| i2s | 13 |
| stream | 13 |
| wifi | 10 |
| es8311 | 9 |
| queue | 8 |
| afe | 6 |
| audio | 3 |
| codec | 3 |
| wakenet | 1 |
| vad | 1 |
| esp_hosted | 1 |

### Top fichiers

- `main\keyboard_examples\bq25896\main.cpp` → task, dma, afe
- `main\keyboard_examples\radiolib_cc1101_send_receive\main.cpp` → task
- `main\keyboard_examples\radiolib_nrf24l01_send_receive\main.cpp` → task
- `main\keyboard_examples\screen_tca8418_lvgl_touch_draw\main.cpp` → task, buffer, dma, afe
- `main\keyboard_examples\st25r3916\main.cpp` → task
- `main\keyboard_examples\st25r3916\st25r3916_driver.cpp` → wifi, buffer
- `main\keyboard_examples\tca8418\main.cpp` → task
- `main\keyboard_examples\xl9555\main.cpp` → task
- `main\examples\afe\main.cpp` → wakenet, es8311, vad, task, buffer, i2s, audio, afe
- `main\examples\aw86224\main.cpp` → task
- `main\examples\bq27220\main.cpp` → task, dma
- `main\examples\deep_sleep\gpio_wakeup.cpp` → task
- `main\examples\deep_sleep\main.cpp` → es8311, task, buffer, stream, i2s, sdio, wifi
- `main\examples\deep_sleep\uart_wakeup.cpp` → buffer, queue, task
- `main\examples\es8311\main.cpp` → es8311, task, buffer, i2s

## Meck-P4 (80 fichiers)

| Keyword | Fichiers |
|---|---|
| buffer | 51 |
| task | 39 |
| sdio | 16 |
| dma | 14 |
| i2s | 13 |
| stream | 13 |
| wifi | 10 |
| es8311 | 9 |
| queue | 8 |
| afe | 6 |
| audio | 3 |
| codec | 3 |
| wakenet | 1 |
| vad | 1 |
| esp_hosted | 1 |

### Top fichiers

- `main\keyboard_examples\bq25896\main.cpp` → task, dma, afe
- `main\keyboard_examples\radiolib_cc1101_send_receive\main.cpp` → task
- `main\keyboard_examples\radiolib_nrf24l01_send_receive\main.cpp` → task
- `main\keyboard_examples\screen_tca8418_lvgl_touch_draw\main.cpp` → task, buffer, dma, afe
- `main\keyboard_examples\st25r3916\main.cpp` → task
- `main\keyboard_examples\st25r3916\st25r3916_driver.cpp` → wifi, buffer
- `main\keyboard_examples\tca8418\main.cpp` → task
- `main\keyboard_examples\xl9555\main.cpp` → task
- `main\examples\afe\main.cpp` → wakenet, es8311, vad, task, buffer, i2s, audio, afe
- `main\examples\aw86224\main.cpp` → task
- `main\examples\bq27220\main.cpp` → task, dma
- `main\examples\deep_sleep\gpio_wakeup.cpp` → task
- `main\examples\deep_sleep\main.cpp` → es8311, task, buffer, stream, i2s, sdio, wifi
- `main\examples\deep_sleep\uart_wakeup.cpp` → buffer, queue, task
- `main\examples\es8311\main.cpp` → es8311, task, buffer, i2s

## Meck-P4-v2 (80 fichiers)

| Keyword | Fichiers |
|---|---|
| buffer | 51 |
| task | 39 |
| sdio | 16 |
| dma | 14 |
| i2s | 13 |
| stream | 13 |
| wifi | 10 |
| es8311 | 9 |
| queue | 8 |
| afe | 6 |
| audio | 3 |
| codec | 3 |
| wakenet | 1 |
| vad | 1 |
| esp_hosted | 1 |

### Top fichiers

- `main\keyboard_examples\bq25896\main.cpp` → task, dma, afe
- `main\keyboard_examples\radiolib_cc1101_send_receive\main.cpp` → task
- `main\keyboard_examples\radiolib_nrf24l01_send_receive\main.cpp` → task
- `main\keyboard_examples\screen_tca8418_lvgl_touch_draw\main.cpp` → task, buffer, dma, afe
- `main\keyboard_examples\st25r3916\main.cpp` → task
- `main\keyboard_examples\st25r3916\st25r3916_driver.cpp` → wifi, buffer
- `main\keyboard_examples\tca8418\main.cpp` → task
- `main\keyboard_examples\xl9555\main.cpp` → task
- `main\examples\afe\main.cpp` → wakenet, es8311, vad, task, buffer, i2s, audio, afe
- `main\examples\aw86224\main.cpp` → task
- `main\examples\bq27220\main.cpp` → task, dma
- `main\examples\deep_sleep\gpio_wakeup.cpp` → task
- `main\examples\deep_sleep\main.cpp` → es8311, task, buffer, stream, i2s, sdio, wifi
- `main\examples\deep_sleep\uart_wakeup.cpp` → buffer, queue, task
- `main\examples\es8311\main.cpp` → es8311, task, buffer, i2s

## T-Display-P4 (80 fichiers)

| Keyword | Fichiers |
|---|---|
| buffer | 51 |
| task | 39 |
| sdio | 16 |
| dma | 14 |
| i2s | 13 |
| stream | 13 |
| wifi | 10 |
| es8311 | 9 |
| queue | 8 |
| afe | 6 |
| audio | 3 |
| codec | 2 |
| wakenet | 1 |
| vad | 1 |
| esp_hosted | 1 |

### Top fichiers

- `main\keyboard_examples\bq25896\main.cpp` → task, dma, afe
- `main\keyboard_examples\radiolib_cc1101_send_receive\main.cpp` → task
- `main\keyboard_examples\radiolib_nrf24l01_send_receive\main.cpp` → task
- `main\keyboard_examples\screen_tca8418_lvgl_touch_draw\main.cpp` → task, buffer, dma, afe
- `main\keyboard_examples\st25r3916\main.cpp` → task
- `main\keyboard_examples\st25r3916\st25r3916_driver.cpp` → wifi, buffer
- `main\keyboard_examples\tca8418\main.cpp` → task
- `main\keyboard_examples\xl9555\main.cpp` → task
- `main\examples\afe\main.cpp` → wakenet, es8311, vad, task, buffer, i2s, audio, afe
- `main\examples\aw86224\main.cpp` → task
- `main\examples\bq27220\main.cpp` → task, dma
- `main\examples\deep_sleep\gpio_wakeup.cpp` → task
- `main\examples\deep_sleep\main.cpp` → es8311, task, buffer, stream, i2s, sdio, wifi
- `main\examples\deep_sleep\uart_wakeup.cpp` → buffer, queue, task
- `main\examples\es8311\main.cpp` → es8311, task, buffer, i2s

## T-Connection-P4-Pro (80 fichiers)

| Keyword | Fichiers |
|---|---|
| buffer | 52 |
| afe | 18 |
| stream | 16 |
| wifi | 14 |
| audio | 14 |
| dma | 10 |
| queue | 7 |
| task | 4 |
| vad | 2 |

### Top fichiers

- `include\config.h` → wifi
- `lib\lv_conf.h` → buffer, queue, task
- `lib\esp32c6_at\esp32c6_at.cpp` → wifi
- `lib\esp32c6_at\esp32c6_at.h` → wifi
- `lib\esp32c6_slave\esp32c6_slave.cpp` → wifi, dma
- `lib\esp32c6_slave\esp32c6_slave.h` → wifi, dma
- `lib\ESP32_Display_Panel\esp_panel_board_custom_conf.h` → buffer
- `lib\ESP32_Display_Panel\esp_panel_board_supported_conf.h` → wifi
- `lib\hyn_driver_for_esp32\hyn_core.c` → queue, task
- `lib\hyn_driver_for_esp32\hyn_core.h` → queue, task
- `lib\hyn_driver_for_esp32\hyn_i2c.c` → buffer
- `lib\lvgl-9.2.0\lv_conf_template.h` → buffer, queue, task
- `lib\TinyGPSPlus\src\TinyGPS++.cpp` → buffer
- `lib\TinyGPSPlus\src\TinyGPS++.h` → buffer
- `lib\RadioLib\src\BuildOpt.h` → wifi, afe

## ESP32-P4-Platform (80 fichiers)

| Keyword | Fichiers |
|---|---|
| wifi | 51 |
| task | 20 |
| buffer | 19 |
| audio | 14 |
| codec | 6 |
| i2s | 5 |
| queue | 5 |
| vad | 4 |
| afe | 3 |
| stream | 2 |
| es8311 | 2 |
| wakenet | 1 |
| opus | 1 |
| ringbuf | 1 |

### Top fichiers

- `firmware\brookesia\main\main.cpp` → wifi, codec, buffer, task
- `firmware\brookesia\components\Camera\Camera.cpp` → buffer, stream, task
- `firmware\brookesia\components\Camera\Camera.hpp` → buffer, task
- `firmware\brookesia\components\MusicPlayer\MusicPlayer.cpp` → audio
- `firmware\brookesia\components\Settings\Settings.cpp` → wifi, buffer, vad
- `firmware\brookesia\components\Settings\Settings.hpp` → wifi, vad
- `firmware\brookesia\components\SpecAnalyzer\SpecAnalyzer.cpp` → audio, task, buffer, i2s
- `firmware\brookesia\components\SpecAnalyzer\SpecAnalyzer.hpp` → audio, task, buffer, i2s
- `firmware\brookesia\components\VideoPlayer\VideoPlayer.cpp` → task, buffer, i2s, codec, audio
- `firmware\brookesia\components\VideoPlayer\VideoPlayer.hpp` → audio, buffer, task
- `firmware\brookesia\components\Settings\assets\WIFI.c` → wifi
- `firmware\brookesia\components\Settings\assets\wifi_1.c` → wifi
- `firmware\brookesia\components\Settings\assets\wifi_2.c` → wifi
- `firmware\brookesia\components\Settings\assets\wifi_3.c` → wifi
- `firmware\brookesia\components\Settings\assets\wifi_4.c` → wifi

## CrowPanel-P4 (18 fichiers)

| Keyword | Fichiers |
|---|---|
| buffer | 13 |
| wifi | 5 |
| task | 4 |
| dma | 4 |

### Top fichiers

- `example\V1.0\Arduino_Code\Lesson05-Touchscreen\esp_panel_board_custom_conf.h` → buffer
- `example\V1.0\Arduino_Code\Lesson05-Touchscreen\libraries\ESP32_Display_Panel\esp_panel_board_custom_conf.h` → buffer
- `example\V1.0\Arduino_Code\Lesson05-Touchscreen\libraries\ESP32_Display_Panel\esp_panel_board_supported_conf.h` → wifi
- `example\V1.0\Arduino_Code\Lesson05-Touchscreen\libraries\ESP32_Display_Panel\examples\arduino\gui\lvgl_v8\simple_port\esp_panel_board_custom_conf.h` → buffer
- `example\V1.0\Arduino_Code\Lesson05-Touchscreen\libraries\ESP32_Display_Panel\examples\arduino\gui\lvgl_v8\simple_port\esp_panel_board_supported_conf.h` → wifi
- `example\V1.0\Arduino_Code\Lesson05-Touchscreen\libraries\ESP32_Display_Panel\examples\arduino\gui\lvgl_v8\simple_port\lvgl_v8_port.cpp` → buffer, task
- `example\V1.0\Arduino_Code\Lesson05-Touchscreen\libraries\ESP32_Display_Panel\examples\arduino\gui\lvgl_v8\simple_port\lvgl_v8_port.h` → task, buffer, dma
- `example\V1.0\Arduino_Code\Lesson05-Touchscreen\libraries\ESP32_Display_Panel\examples\arduino\gui\lvgl_v8\simple_port\lv_conf.h` → buffer, dma
- `example\V1.0\Arduino_Code\Lesson05-Touchscreen\libraries\ESP32_Display_Panel\examples\arduino\gui\lvgl_v8\simple_rotation\esp_panel_board_custom_conf.h` → buffer
- `example\V1.0\Arduino_Code\Lesson05-Touchscreen\libraries\ESP32_Display_Panel\examples\arduino\gui\lvgl_v8\simple_rotation\esp_panel_board_supported_conf.h` → wifi
- `example\V1.0\Arduino_Code\Lesson05-Touchscreen\libraries\ESP32_Display_Panel\examples\arduino\gui\lvgl_v8\simple_rotation\lvgl_v8_port.cpp` → buffer, task
- `example\V1.0\Arduino_Code\Lesson05-Touchscreen\libraries\ESP32_Display_Panel\examples\arduino\gui\lvgl_v8\simple_rotation\lvgl_v8_port.h` → task, buffer, dma
- `example\V1.0\Arduino_Code\Lesson05-Touchscreen\libraries\ESP32_Display_Panel\examples\arduino\gui\lvgl_v8\simple_rotation\lv_conf.h` → buffer, dma
- `example\V1.0\Arduino_Code\Lesson05-Touchscreen\libraries\ESP32_Display_Panel\examples\arduino\gui\lvgl_v8\squareline_port\esp_panel_board_custom_conf.h` → buffer
- `example\V1.0\Arduino_Code\Lesson05-Touchscreen\libraries\ESP32_Display_Panel\examples\arduino\gui\lvgl_v8\squareline_port\esp_panel_board_supported_conf.h` → wifi

## esp32p4-c6-wifi-test (5 fichiers)

| Keyword | Fichiers |
|---|---|
| wifi | 5 |
| esp_hosted | 3 |
| buffer | 3 |
| task | 2 |
| sdio | 2 |
| stream | 1 |
| udp | 1 |

### Top fichiers

- `main\app_main.c` → task, esp_hosted, buffer, stream, sdio, wifi, udp
- `main\wifi_raw.c` → wifi, esp_hosted, buffer
- `main\wifi_raw.h` → wifi, buffer
- `main\wifi_raw_msgs.h` → wifi
- `c6-ota-flasher\main\app_main.c` → wifi, esp_hosted, task, sdio

## SigurdOS (80 fichiers)

| Keyword | Fichiers |
|---|---|
| buffer | 38 |
| wifi | 25 |
| queue | 21 |
| afe | 20 |
| dma | 10 |
| task | 10 |
| stream | 7 |
| audio | 2 |
| vad | 1 |

### Top fichiers

- `src\main.cpp` → wifi
- `test\mocks\Arduino.h` → stream, buffer, queue, dma
- `test\mocks\LovyanGFX.hpp` → dma
- `test\mocks\lvgl.h` → wifi, buffer
- `test\mocks\MeshCore.h` → stream
- `test\mocks\mock_mesh_wrapper.cpp` → queue
- `test\mocks\Stream.h` → stream
- `test\test_build_info\main.cpp` → afe
- `test\test_channel_menu\test_channel_menu.cpp` → dma
- `test\test_channel_validation\test_channel_validation.cpp` → buffer, dma
- `test\test_chat_config\test_chat_config.cpp` → buffer, dma
- `test\test_chat_truncation\main.cpp` → buffer
- `test\test_chat_truncation\test_chat_truncation.cpp` → buffer
- `test\test_companion_protocol\test_companion_protocol.cpp` → queue, afe
- `test\test_contact_paging\test_contact_paging.cpp` → afe

## meshtastic (80 fichiers)

| Keyword | Fichiers |
|---|---|
| wifi | 32 |
| dma | 17 |
| buffer | 15 |
| afe | 11 |
| stream | 10 |
| i2s | 10 |
| audio | 7 |
| queue | 5 |
| udp | 4 |
| task | 3 |
| codec | 2 |
| es8311 | 2 |

### Top fichiers

- `.clusterfuzzlite\router_fuzzer.cpp` → buffer, queue, stream
- `src\AudioThread.h` → audio, i2s
- `src\configuration.h` → wifi, audio, afe
- `src\DebugConfiguration.cpp` → udp
- `src\DebugConfiguration.h` → wifi, udp
- `src\freertosinc.h` → queue, task
- `src\FSCommon.cpp` → buffer
- `src\GpioLogic.h` → stream
- `src\main.cpp` → queue, dma, buffer, stream, i2s, wifi, udp, audio, afe
- `src\main.h` → udp, audio, i2s
- `src\meshUtils.cpp` → buffer
- `src\meshUtils.h` → buffer
- `src\MessageStore.cpp` → buffer, queue, afe
- `src\MessageStore.h` → buffer, queue, afe
- `src\network-stubs.cpp` → wifi

## meshtastic-firmware (80 fichiers)

| Keyword | Fichiers |
|---|---|
| wifi | 32 |
| dma | 17 |
| buffer | 15 |
| afe | 11 |
| stream | 10 |
| i2s | 10 |
| audio | 7 |
| queue | 5 |
| udp | 4 |
| task | 3 |
| codec | 2 |
| es8311 | 2 |

### Top fichiers

- `.clusterfuzzlite\router_fuzzer.cpp` → buffer, queue, stream
- `src\AudioThread.h` → audio, i2s
- `src\configuration.h` → wifi, audio, afe
- `src\DebugConfiguration.cpp` → udp
- `src\DebugConfiguration.h` → wifi, udp
- `src\freertosinc.h` → queue, task
- `src\FSCommon.cpp` → buffer
- `src\GpioLogic.h` → stream
- `src\main.cpp` → queue, dma, buffer, stream, i2s, wifi, udp, audio, afe
- `src\main.h` → udp, audio, i2s
- `src\meshUtils.cpp` → buffer
- `src\meshUtils.h` → buffer
- `src\MessageStore.cpp` → buffer, queue, afe
- `src\MessageStore.h` → buffer, queue, afe
- `src\network-stubs.cpp` → wifi

## jarvix (80 fichiers)

| Keyword | Fichiers |
|---|---|
| buffer | 43 |
| task | 35 |
| audio | 34 |
| afe | 25 |
| queue | 24 |
| stream | 22 |
| wifi | 19 |
| vad | 15 |
| dma | 14 |
| i2s | 14 |
| sdio | 14 |
| es8311 | 12 |
| codec | 12 |
| opus | 6 |
| jitter | 2 |
| wakenet | 1 |
| esp_hosted | 1 |

### Top fichiers

- `main\i2s_loopback_benchmark.c` → es8311, jitter, dma, task, buffer, i2s, sdio, wifi, codec, audio
- `main\main.cpp` → es8311, vad, task, opus, buffer, stream, i2s, sdio, wifi, audio
- `main\memory_watchdog.h` → afe
- `components\audio\audio_capture.c` → wakenet, es8311, vad, dma, task, buffer, stream, i2s, codec, audio, afe
- `components\audio\audio_capture.h` → es8311, vad, task, buffer, codec, audio, afe
- `components\audio\audio_ref_buffer.c` → audio, buffer, dma
- `components\audio\audio_ref_buffer.h` → audio, buffer, i2s, afe
- `components\audio\bsp_extra.c` → dma, es8311, buffer, i2s
- `components\audio\bsp_extra.h` → es8311, i2s
- `components\audio\ha_client.c` → audio, buffer, stream, task
- `components\audio\ha_client.h` → audio, opus, buffer, stream
- `components\audio\tts_player.c` → queue, dma, task, opus, buffer, i2s, audio
- `components\audio\tts_player.h` → opus, buffer, i2s
- `components\audio\voice_pipeline.c` → vad, audio, queue, task
- `components\audio\voice_pipeline.h` → audio, vad

## OpenMQTTGateway (58 fichiers)

| Keyword | Fichiers |
|---|---|
| buffer | 48 |
| queue | 44 |
| wifi | 25 |
| task | 15 |
| dma | 6 |
| stream | 6 |
| afe | 2 |

### Top fichiers

- `main\actuatorONOFF.cpp` → task, buffer, queue, dma
- `main\blufi.cpp` → wifi, buffer, task
- `main\boardTheengs.cpp` → wifi, dma
- `main\commonRF.cpp` → wifi, buffer, queue, task
- `main\config_C37_YL83_HMRD.h` → wifi
- `main\config_DS1820.h` → wifi
- `main\config_GFSunInverter.h` → wifi
- `main\config_RN8209.h` → task
- `main\config_SERIAL.h` → wifi, buffer
- `main\config_SSD1306.h` → wifi, buffer
- `main\config_WebContent.h` → wifi, buffer
- `main\config_WebUI.h` → wifi, buffer, queue, stream
- `main\displaySSD1306.cpp` → wifi, buffer, queue, stream
- `main\gateway2G.cpp` → buffer, queue
- `main\gatewayBLEConnect.cpp` → buffer, queue, task

## LoRaMon (0 fichiers)

| Keyword | Fichiers |
|---|---|

### Top fichiers


## RadioLib (80 fichiers)

| Keyword | Fichiers |
|---|---|
| buffer | 51 |
| afe | 24 |
| stream | 17 |
| audio | 14 |
| dma | 9 |
| wifi | 8 |
| task | 4 |
| queue | 3 |
| vad | 2 |
| jitter | 1 |

### Top fichiers

- `src\BuildOpt.h` → wifi, buffer, afe
- `src\Hal.h` → buffer
- `src\Module.cpp` → buffer, stream
- `src\Module.h` → stream, afe
- `src\TypeDef.h` → wifi, buffer, queue
- `src\utils\ConvCode.h` → buffer
- `src\utils\CRC.h` → buffer
- `src\utils\Cryptography.cpp` → buffer, stream
- `src\utils\Cryptography.h` → buffer
- `src\utils\Utils.cpp` → buffer
- `src\protocols\ADSB\ADSB.h` → buffer
- `src\protocols\AFSK\AFSK.h` → audio
- `src\protocols\APRS\APRS.cpp` → buffer
- `src\protocols\AX25\AX25.cpp` → audio, buffer
- `src\protocols\AX25\AX25.h` → audio, buffer

## SX1262-Arduino-ESP32-driver (2 fichiers)

| Keyword | Fichiers |
|---|---|
| buffer | 2 |
| wifi | 1 |
| afe | 1 |

### Top fichiers

- `SX126x.cpp` → wifi, buffer, afe
- `SX126x.h` → buffer

## MeshCore-official (80 fichiers)

| Keyword | Fichiers |
|---|---|
| buffer | 38 |
| queue | 25 |
| afe | 15 |
| stream | 13 |
| wifi | 13 |
| task | 7 |
| dma | 4 |
| flow_control | 1 |
| jitter | 1 |

### Top fichiers

- `src\Dispatcher.cpp` → queue
- `src\Dispatcher.h` → queue, task
- `src\Identity.cpp` → stream
- `src\Identity.h` → buffer, stream
- `src\Mesh.h` → task
- `src\Packet.h` → buffer
- `src\Utils.cpp` → stream
- `src\Utils.h` → stream
- `variants\generic_espnow\target.cpp` → wifi
- `variants\heltec_t096\LoRaFEMControl.cpp` → afe
- `variants\heltec_t096\LoRaFEMControl.h` → afe
- `variants\heltec_t096\T096Board.cpp` → afe
- `variants\heltec_t096\T096Board.h` → afe
- `variants\heltec_tracker_v2\HeltecTrackerV2Board.cpp` → afe
- `variants\heltec_tracker_v2\HeltecTrackerV2Board.h` → afe

## MeshCore-dup (80 fichiers)

| Keyword | Fichiers |
|---|---|
| buffer | 38 |
| queue | 25 |
| afe | 15 |
| stream | 13 |
| wifi | 13 |
| task | 7 |
| dma | 4 |
| flow_control | 1 |
| jitter | 1 |

### Top fichiers

- `src\Dispatcher.cpp` → queue
- `src\Dispatcher.h` → queue, task
- `src\Identity.cpp` → stream
- `src\Identity.h` → buffer, stream
- `src\Mesh.h` → task
- `src\Packet.h` → buffer
- `src\Utils.cpp` → stream
- `src\Utils.h` → stream
- `variants\generic_espnow\target.cpp` → wifi
- `variants\heltec_t096\LoRaFEMControl.cpp` → afe
- `variants\heltec_t096\LoRaFEMControl.h` → afe
- `variants\heltec_t096\T096Board.cpp` → afe
- `variants\heltec_t096\T096Board.h` → afe
- `variants\heltec_tracker_v2\HeltecTrackerV2Board.cpp` → afe
- `variants\heltec_tracker_v2\HeltecTrackerV2Board.h` → afe

## trail-mate (80 fichiers)

| Keyword | Fichiers |
|---|---|
| codec | 67 |
| buffer | 23 |
| audio | 7 |
| stream | 7 |
| afe | 3 |
| i2s | 2 |
| es8311 | 1 |
| queue | 1 |
| dma | 1 |

### Top fichiers

- `variants\lilygo_tlora_pager\pins_arduino.h` → codec, es8311, audio, i2s
- `variants\lilygo_twatch_s3\pins_arduino.h` → audio
- `variants\tdeck\pins_arduino.h` → i2s
- `third_party\codec2\src\c2file.h` → codec
- `third_party\codec2\src\c2wideband.h` → codec
- `third_party\codec2\src\c2wideband_map.h` → codec
- `third_party\codec2\src\codebook.c` → codec
- `third_party\codec2\src\codebookd.c` → codec
- `third_party\codec2\src\codebookge.c` → codec
- `third_party\codec2\src\codebookjmv.c` → codec
- `third_party\codec2\src\codebooknewamp1.c` → codec
- `third_party\codec2\src\codebooknewamp1_energy.c` → codec
- `third_party\codec2\src\codebooknewamp2.c` → codec
- `third_party\codec2\src\codebooknewamp2_energy.c` → codec
- `third_party\codec2\src\codec2.c` → codec, audio, buffer

## lunarcore (0 fichiers)

| Keyword | Fichiers |
|---|---|

### Top fichiers


## meshcomod (80 fichiers)

| Keyword | Fichiers |
|---|---|
| wifi | 33 |
| buffer | 20 |
| afe | 18 |
| queue | 16 |
| stream | 16 |
| task | 13 |
| dma | 6 |
| jitter | 1 |

### Top fichiers

- `include\LvglPsramAlloc.h` → wifi, dma
- `include\lv_conf.h` → jitter, task, dma, buffer, wifi
- `src\Dispatcher.cpp` → queue
- `src\Dispatcher.h` → queue, task
- `src\Identity.cpp` → stream
- `src\Identity.h` → buffer, stream
- `src\LvglPsramAlloc.cpp` → afe
- `src\Mesh.h` → task
- `src\MeshCore.h` → wifi
- `src\Packet.h` → buffer
- `src\Utils.cpp` → stream
- `src\Utils.h` → stream
- `variants\generic_espnow\target.cpp` → wifi
- `variants\heltec_t096\LoRaFEMControl.cpp` → afe
- `variants\heltec_t096\LoRaFEMControl.h` → afe

## akita-bridge (0 fichiers)

| Keyword | Fichiers |
|---|---|

### Top fichiers


## awesome-meshcore (0 fichiers)

| Keyword | Fichiers |
|---|---|

### Top fichiers


## RWKV-LM (0 fichiers)

| Keyword | Fichiers |
|---|---|

### Top fichiers


## RWKV-X (1 fichiers)

| Keyword | Fichiers |
|---|---|
| stream | 1 |

### Top fichiers

- `package\src\rwkv_x\cuda\wrapper.cpp` → stream

## rwkv.cpp (4 fichiers)

| Keyword | Fichiers |
|---|---|
| buffer | 4 |
| stream | 1 |
| afe | 1 |

### Top fichiers

- `rwkv.cpp` → buffer, stream
- `rwkv.h` → buffer, afe
- `tests\test_ggml_basics.c` → buffer
- `tests\test_quantized_matmul_on_gpu.c` → buffer

## snntorch (0 fichiers)

| Keyword | Fichiers |
|---|---|

### Top fichiers


## norse (0 fichiers)

| Keyword | Fichiers |
|---|---|

### Top fichiers


## open-interpreter (5 fichiers)

| Keyword | Fichiers |
|---|---|
| afe | 3 |
| buffer | 3 |
| queue | 1 |

### Top fichiers

- `codex-rs\vendor\bubblewrap\bind-mount.c` → afe
- `codex-rs\vendor\bubblewrap\bubblewrap.c` → buffer, queue, afe
- `codex-rs\vendor\bubblewrap\network.c` → buffer
- `codex-rs\vendor\bubblewrap\utils.c` → buffer
- `codex-rs\vendor\bubblewrap\utils.h` → afe

## autogen (0 fichiers)

| Keyword | Fichiers |
|---|---|

### Top fichiers


## gat45-p4 (0 fichiers)

| Keyword | Fichiers |
|---|---|

### Top fichiers
