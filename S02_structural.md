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

- `micropython_adf\mod\audio_player.c` → audio, stream, task, i2s, codec
- `micropython_adf\mod\audio_recorder.c` → audio, stream, task, i2s, codec
- `micropython_adf\mod\modaudio.c` → audio, stream, codec
- `micropython_adf\mod\modaudio.h` → audio
- `micropython_adf\mod\vfs_stream.c` → audio, buffer, stream, task, opus
- `micropython_adf\mod\vfs_stream.h` → audio, buffer, stream, task, ringbuf
- `micropython_adf\boards\include\board_init.h` → audio, codec
- `micropython_adf\boards\korvo2v3\board_init.c` → audio, es8311, codec
- `micropython_adf\boards\korvo2v3\mpconfigboard.h` → audio
- `micropython_adf\boards\lyrat43\board_init.c` → audio, codec
- `micropython_adf\boards\lyrat43\mpconfigboard.h` → audio
- `micropython_adf\boards\lyratmini\board_init.c` → audio, es8311, codec
- `micropython_adf\boards\lyratmini\mpconfigboard.h` → audio
- `examples\system\wpa2_enterprise\main\wpa2_enterprise_example.c` → wifi, audio, task
- `examples\system\power_save\main\audio_power_save.c` → audio, stream, wifi, task, i2s, codec

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

- `esp_hosted_ng\host\esp_bt.c` → sdio, buffer
- `esp_hosted_ng\host\esp_cfg80211.c` → wifi, queue
- `esp_hosted_ng\host\esp_cmd.c` → wifi, queue, task, buffer
- `esp_hosted_ng\host\esp_debugfs.c` → buffer
- `esp_hosted_ng\host\esp_stats.c` → wifi, queue, task
- `esp_hosted_ng\host\esp_utils.c` → wifi
- `esp_hosted_ng\host\main.c` → sdio, buffer, wifi, task, queue
- `esp_hosted_ng\host\include\adapter.h` → wifi, dma, queue, sdio
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
| i2s | 33 |
| codec | 33 |
| task | 21 |
| es8311 | 16 |
| buffer | 12 |
| stream | 9 |
| wifi | 8 |
| afe | 4 |
| vad | 4 |
| dma | 3 |
| queue | 3 |
| opus | 3 |
| udp | 2 |

### Top fichiers

- `main\application.h` → afe, audio, task, vad
- `main\device_state.h` → wifi, audio
- `main\system_info.h` → task
- `main\audio\audio_codec.h` → audio, dma, i2s, codec
- `main\audio\audio_processor.h` → audio, codec, vad
- `main\audio\audio_service.h` → audio, afe, vad, stream, task, queue, opus, codec
- `main\audio\wake_word.h` → audio, opus, codec
- `main\led\circular_strip.h` → task
- `main\led\gpio_led.h` → task
- `main\led\single_led.h` → task
- `main\protocols\mqtt_protocol.h` → udp, audio, stream, afe
- `main\protocols\protocol.h` → audio, stream, opus
- `main\protocols\websocket_protocol.h` → audio, stream
- `main\display\lvgl_display\gif\gifdec.c` → buffer
- `main\display\lvgl_display\gif\gifdec.h` → buffer

## ha_voice (40 fichiers)

| Keyword | Fichiers |
|---|---|
| audio | 21 |
| buffer | 21 |
| task | 18 |
| afe | 13 |
| codec | 13 |
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
- `main\audio_capture.c` → audio, afe, buffer, wakenet, vad, stream, task, i2s, codec
- `main\audio_capture.h` → audio, afe, buffer, es8311, vad, stream, task, codec
- `main\audio_ref_buffer.c` → audio, afe, buffer, stream, ringbuf
- `main\audio_ref_buffer.h` → audio, i2s, buffer, afe
- `main\beep_tone.c` → audio, i2s, buffer, codec
- `main\beep_tone.h` → audio
- `main\ha_client.c` → audio, afe, buffer, stream, task
- `main\ha_client.h` → audio, stream, buffer
- `main\led_status.c` → task
- `main\local_music_player.c` → queue, audio, i2s, codec
- `main\local_music_player.h` → wifi, buffer
- `main\main.c` → audio, afe, vad, wifi, task, i2s, codec
- `main\mqtt_ha.c` → wifi, queue, vad
- `main\mqtt_ha.h` → wifi, vad

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

- `main\keyboard_examples\bq25896\main.cpp` → dma, task, afe
- `main\keyboard_examples\radiolib_cc1101_send_receive\main.cpp` → task
- `main\keyboard_examples\radiolib_nrf24l01_send_receive\main.cpp` → task
- `main\keyboard_examples\screen_tca8418_lvgl_touch_draw\main.cpp` → dma, task, buffer, afe
- `main\keyboard_examples\st25r3916\main.cpp` → task
- `main\keyboard_examples\st25r3916\st25r3916_driver.cpp` → wifi, buffer
- `main\keyboard_examples\tca8418\main.cpp` → task
- `main\keyboard_examples\xl9555\main.cpp` → task
- `main\examples\afe\main.cpp` → audio, afe, buffer, es8311, wakenet, vad, task, i2s
- `main\examples\aw86224\main.cpp` → task
- `main\examples\bq27220\main.cpp` → dma, task
- `main\examples\deep_sleep\gpio_wakeup.cpp` → task
- `main\examples\deep_sleep\main.cpp` → sdio, buffer, es8311, stream, wifi, task, i2s
- `main\examples\deep_sleep\uart_wakeup.cpp` → queue, task, buffer
- `main\examples\es8311\main.cpp` → task, i2s, buffer, es8311

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
| es8311 | 2 |
| codec | 2 |

### Top fichiers

- `.clusterfuzzlite\router_fuzzer.cpp` → queue, stream, buffer
- `src\AudioThread.h` → audio, i2s
- `src\configuration.h` → wifi, audio, afe
- `src\DebugConfiguration.cpp` → udp
- `src\DebugConfiguration.h` → wifi, udp
- `src\freertosinc.h` → queue, task
- `src\FSCommon.cpp` → buffer
- `src\GpioLogic.h` → stream
- `src\main.cpp` → audio, afe, buffer, stream, wifi, dma, i2s, queue, udp
- `src\main.h` → audio, udp, i2s
- `src\meshUtils.cpp` → buffer
- `src\meshUtils.h` → buffer
- `src\MessageStore.cpp` → queue, afe, buffer
- `src\MessageStore.h` → queue, afe, buffer
- `src\network-stubs.cpp` → wifi

## jarvix (80 fichiers)

| Keyword | Fichiers |
|---|---|
| buffer | 37 |
| task | 35 |
| audio | 32 |
| queue | 25 |
| stream | 20 |
| afe | 20 |
| vad | 15 |
| wifi | 15 |
| sdio | 12 |
| dma | 11 |
| codec | 11 |
| es8311 | 9 |
| i2s | 8 |
| opus | 3 |
| wakenet | 1 |
| esp_hosted | 1 |
| jitter | 1 |

### Top fichiers

- `main\main.cpp` → audio, sdio, vad, stream, wifi, task
- `main\memory_watchdog.h` → afe
- `components\audio\audio_capture.c` → audio, afe, buffer, es8311, wakenet, vad, stream, dma, i2s, task, codec
- `components\audio\audio_capture.h` → audio, afe, buffer, es8311, vad, task, codec
- `components\audio\audio_ref_buffer.c` → dma, audio, buffer
- `components\audio\audio_ref_buffer.h` → audio, i2s, buffer, afe
- `components\audio\ha_client.c` → audio, task, stream, buffer
- `components\audio\ha_client.h` → opus, audio, stream, buffer
- `components\audio\voice_pipeline.c` → queue, audio, task, vad
- `components\audio\voice_pipeline.h` → audio, vad
- `components\audio\wifi_manager.c` → wifi, task, sdio
- `components\audio\wifi_manager.h` → wifi, sdio
- `components\chmorgan__esp-audio-player\audio_decode_types.h` → audio
- `components\chmorgan__esp-audio-player\audio_log.h` → audio
- `components\chmorgan__esp-audio-player\audio_mp3.cpp` → audio, task, buffer, afe

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

- `main\actuatorONOFF.cpp` → queue, dma, task, buffer
- `main\blufi.cpp` → wifi, task, buffer
- `main\boardTheengs.cpp` → wifi, dma
- `main\commonRF.cpp` → wifi, queue, task, buffer
- `main\config_C37_YL83_HMRD.h` → wifi
- `main\config_DS1820.h` → wifi
- `main\config_GFSunInverter.h` → wifi
- `main\config_RN8209.h` → task
- `main\config_SERIAL.h` → wifi, buffer
- `main\config_SSD1306.h` → wifi, buffer
- `main\config_WebContent.h` → wifi, buffer
- `main\config_WebUI.h` → wifi, queue, stream, buffer
- `main\displaySSD1306.cpp` → wifi, queue, stream, buffer
- `main\gateway2G.cpp` → queue, buffer
- `main\gatewayBLEConnect.cpp` → queue, task, buffer

## LoRaMon (0 fichiers)

| Keyword | Fichiers |
|---|---|

### Top fichiers


## meshtastic-sniffer (69 fichiers)

| Keyword | Fichiers |
|---|---|
| stream | 41 |
| buffer | 37 |
| afe | 16 |
| queue | 13 |
| udp | 6 |
| wifi | 3 |
| backpressure | 2 |
| audio | 2 |
| dma | 1 |
| task | 1 |
| jitter | 1 |
| vad | 1 |

### Top fichiers

- `airspy.c` → stream
- `airspy.h` → stream
- `announce.c` → stream, buffer
- `archive.c` → afe, stream
- `bladerf.c` → stream, buffer
- `bladerf.h` → stream
- `blocking_queue.h` → queue, afe
- `c2.h` → dma, buffer
- `c2_dealer.c` → buffer
- `channelizer.c` → stream
- `channelizer.h` → stream, buffer
- `dedup.c` → buffer
- `dedup.h` → afe, buffer
- `fair_lock.h` → queue, afe
- `feed.c` → wifi, udp, stream, buffer

## lorawan-sniffer (0 fichiers)

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

- `src\BuildOpt.h` → wifi, afe, buffer
- `src\Hal.h` → buffer
- `src\Module.cpp` → stream, buffer
- `src\Module.h` → afe, stream
- `src\TypeDef.h` → wifi, queue, buffer
- `src\utils\ConvCode.h` → buffer
- `src\utils\CRC.h` → buffer
- `src\utils\Cryptography.cpp` → stream, buffer
- `src\utils\Cryptography.h` → buffer
- `src\utils\Utils.cpp` → buffer
- `src\protocols\ADSB\ADSB.h` → buffer
- `src\protocols\AFSK\AFSK.h` → audio
- `src\protocols\APRS\APRS.cpp` → buffer
- `src\protocols\AX25\AX25.cpp` → audio, buffer
- `src\protocols\AX25\AX25.h` → audio, buffer

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

- `main\keyboard_examples\bq25896\main.cpp` → dma, task, afe
- `main\keyboard_examples\radiolib_cc1101_send_receive\main.cpp` → task
- `main\keyboard_examples\radiolib_nrf24l01_send_receive\main.cpp` → task
- `main\keyboard_examples\screen_tca8418_lvgl_touch_draw\main.cpp` → dma, task, buffer, afe
- `main\keyboard_examples\st25r3916\main.cpp` → task
- `main\keyboard_examples\st25r3916\st25r3916_driver.cpp` → wifi, buffer
- `main\keyboard_examples\tca8418\main.cpp` → task
- `main\keyboard_examples\xl9555\main.cpp` → task
- `main\examples\afe\main.cpp` → audio, afe, buffer, es8311, wakenet, vad, task, i2s
- `main\examples\aw86224\main.cpp` → task
- `main\examples\bq27220\main.cpp` → dma, task
- `main\examples\deep_sleep\gpio_wakeup.cpp` → task
- `main\examples\deep_sleep\main.cpp` → sdio, buffer, es8311, stream, wifi, task, i2s
- `main\examples\deep_sleep\uart_wakeup.cpp` → queue, task, buffer
- `main\examples\es8311\main.cpp` → task, i2s, buffer, es8311

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

- `main\keyboard_examples\bq25896\main.cpp` → dma, task, afe
- `main\keyboard_examples\radiolib_cc1101_send_receive\main.cpp` → task
- `main\keyboard_examples\radiolib_nrf24l01_send_receive\main.cpp` → task
- `main\keyboard_examples\screen_tca8418_lvgl_touch_draw\main.cpp` → dma, task, buffer, afe
- `main\keyboard_examples\st25r3916\main.cpp` → task
- `main\keyboard_examples\st25r3916\st25r3916_driver.cpp` → wifi, buffer
- `main\keyboard_examples\tca8418\main.cpp` → task
- `main\keyboard_examples\xl9555\main.cpp` → task
- `main\examples\afe\main.cpp` → audio, afe, buffer, es8311, wakenet, vad, task, i2s
- `main\examples\aw86224\main.cpp` → task
- `main\examples\bq27220\main.cpp` → dma, task
- `main\examples\deep_sleep\gpio_wakeup.cpp` → task
- `main\examples\deep_sleep\main.cpp` → sdio, buffer, es8311, stream, wifi, task, i2s
- `main\examples\deep_sleep\uart_wakeup.cpp` → queue, task, buffer
- `main\examples\es8311\main.cpp` → task, i2s, buffer, es8311

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
- `test\mocks\Arduino.h` → queue, dma, stream, buffer
- `test\mocks\LovyanGFX.hpp` → dma
- `test\mocks\lvgl.h` → wifi, buffer
- `test\mocks\MeshCore.h` → stream
- `test\mocks\mock_mesh_wrapper.cpp` → queue
- `test\mocks\Stream.h` → stream
- `test\test_build_info\main.cpp` → afe
- `test\test_channel_menu\test_channel_menu.cpp` → dma
- `test\test_channel_validation\test_channel_validation.cpp` → dma, buffer
- `test\test_chat_config\test_chat_config.cpp` → dma, buffer
- `test\test_chat_truncation\main.cpp` → buffer
- `test\test_chat_truncation\test_chat_truncation.cpp` → buffer
- `test\test_companion_protocol\test_companion_protocol.cpp` → queue, afe
- `test\test_contact_paging\test_contact_paging.cpp` → afe

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

- `main\keyboard_examples\bq25896\main.cpp` → dma, task, afe
- `main\keyboard_examples\radiolib_cc1101_send_receive\main.cpp` → task
- `main\keyboard_examples\radiolib_nrf24l01_send_receive\main.cpp` → task
- `main\keyboard_examples\screen_tca8418_lvgl_touch_draw\main.cpp` → dma, task, buffer, afe
- `main\keyboard_examples\st25r3916\main.cpp` → task
- `main\keyboard_examples\st25r3916\st25r3916_driver.cpp` → wifi, buffer
- `main\keyboard_examples\tca8418\main.cpp` → task
- `main\keyboard_examples\xl9555\main.cpp` → task
- `main\examples\afe\main.cpp` → audio, afe, buffer, es8311, wakenet, vad, task, i2s
- `main\examples\aw86224\main.cpp` → task
- `main\examples\bq27220\main.cpp` → dma, task
- `main\examples\deep_sleep\gpio_wakeup.cpp` → task
- `main\examples\deep_sleep\main.cpp` → sdio, buffer, es8311, stream, wifi, task, i2s
- `main\examples\deep_sleep\uart_wakeup.cpp` → queue, task, buffer
- `main\examples\es8311\main.cpp` → task, i2s, buffer, es8311

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
- `src\Identity.h` → stream, buffer
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
| es8311 | 2 |
| codec | 2 |

### Top fichiers

- `.clusterfuzzlite\router_fuzzer.cpp` → queue, stream, buffer
- `src\AudioThread.h` → audio, i2s
- `src\configuration.h` → wifi, audio, afe
- `src\DebugConfiguration.cpp` → udp
- `src\DebugConfiguration.h` → wifi, udp
- `src\freertosinc.h` → queue, task
- `src\FSCommon.cpp` → buffer
- `src\GpioLogic.h` → stream
- `src\main.cpp` → audio, afe, buffer, stream, wifi, dma, i2s, queue, udp
- `src\main.h` → audio, udp, i2s
- `src\meshUtils.cpp` → buffer
- `src\meshUtils.h` → buffer
- `src\MessageStore.cpp` → queue, afe, buffer
- `src\MessageStore.h` → queue, afe, buffer
- `src\network-stubs.cpp` → wifi

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

- `variants\lilygo_tlora_pager\pins_arduino.h` → audio, i2s, es8311, codec
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
- `third_party\codec2\src\codec2.c` → audio, buffer, codec