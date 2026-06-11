# Script 04: Audio Pipeline Extraction


## esp-adf

- **afe_init** (8 refs): `examples\protocols\voip\main\voip_app.c`
- **apll** (4 refs): `examples\get-started\pipeline_a2dp_sink_and_hfp\main\a2dp_sink_and_hfp_example.c`
- **dma_buf** (7 refs): `examples\ai_agent\volc_rtc\components\audio_processor\audio_stream_dual_microphones.c`
- **es8311** (5 refs): `components\esp_codec_dev\device\es8311\es8311.c`
- **i2s_init** (4 refs): `components\audio_stream\i2s_stream.c`
- **i2s_read** (8 refs): `examples\protocols\components\av_record\record_i2s_aud.c`
- **i2s_write** (8 refs): `micropython_adf\mod\audio_player.c`
- **opus_dec** (8 refs): `examples\player\pipeline_play_sdcard_music\main\play_sdcard_music_example.c`
- **opus_enc** (6 refs): `examples\recorder\pipeline_recording_to_sdcard\main\recording_to_sdcard_example.c`
- **pipeline** (8 refs): `micropython_adf\mod\audio_recorder.c`
- **ringbuf** (8 refs): `micropython_adf\mod\vfs_stream.h`
- **vad** (8 refs): `examples\speech_recognition\vad\main\example_vad_main.c`
- **wakenet** (8 refs): `examples\speech_recognition\wwe\main\main.c`

## esp-sr

- **afe_init** (8 refs): `test_apps\esp32c5\main\test_aec.cpp`
- **ringbuf** (8 refs): `include\esp32\esp_afe_config.h`
- **vad** (8 refs): `test_apps\esp-sr\main\test_afe.cpp`
- **wakenet** (8 refs): `test_apps\esp32c5\main\test_wakenet.cpp`

## esp-hosted

- **ringbuf** (4 refs): `esp_hosted_fg\host\linux\port\src\platform_wrapper.c`

## xiaozhi

- **afe_init** (2 refs): `main\audio\processors\afe_audio_processor.h`
- **dma_buf** (2 refs): `main\audio\audio_codec.h`
- **i2s_init** (1 refs): `main\boards\nulllab-ai-vox-v3\ai_vox3_audio_codec.h`
- **opus_dec** (1 refs): `main\audio\audio_service.h`
- **opus_enc** (1 refs): `main\audio\audio_service.h`
- **vad** (2 refs): `main\audio\processors\afe_audio_processor.h`
- **wakenet** (3 refs): `main\audio\wake_words\afe_wake_word.h`

## xiaozhi-server


## esp32-aichats


## ha_voice

- **afe_init** (1 refs): `main\audio_capture.c`
- **es8311** (1 refs): `common_components\espressif__esp32_p4_function_ev_board\include\bsp\esp32_p4_function_ev_board.h`
- **i2s_init** (1 refs): `common_components\espressif__esp32_p4_function_ev_board\esp32_p4_function_ev_board.c`
- **i2s_read** (3 refs): `main\audio_capture.c`
- **i2s_write** (6 refs): `main\audio_capture.c`
- **ringbuf** (1 refs): `main\audio_ref_buffer.c`
- **vad** (6 refs): `main\audio_capture.c`
- **wakenet** (2 refs): `main\audio_capture.c`

## ESP32_Voice_Assistant


## client-sdk-esp32

- **es8311** (1 refs): `components\livekit\examples\custom_hardware\main\board.c`
- **i2s_init** (1 refs): `components\livekit\examples\custom_hardware\main\board.c`

## stream-video-esp32

- **apll** (1 refs): `examples\minimal\components\codec_board\codec_init.c`
- **dma_buf** (1 refs): `examples\minimal\components\codec_board\codec_init.c`
- **i2s_init** (1 refs): `examples\minimal\components\codec_board\codec_init.c`
- **opus_enc** (1 refs): `components\stream-video\src\capture\default_capture.c`

## ESP32-audioI2S

- **apll** (2 refs): `src\Audio.h`
- **dma_buf** (3 refs): `src\Audio.cpp`
- **es8311** (2 refs): `examples\ES8311\es8311.cpp`
- **i2s_init** (2 refs): `src\Audio.cpp`
- **i2s_write** (2 refs): `src\Audio.cpp`
- **opus_dec** (6 refs): `src\Audio.cpp`
- **ringbuf** (3 refs): `src\aac_decoder\libfaad\aac_structs.h`
- **vad** (3 refs): `src\opus_decoder\silk.cpp`

## esp32_opus

- **opus_dec** (8 refs): `src\opus.h`
- **opus_enc** (8 refs): `src\opus.h`
- **vad** (4 refs): `src\init_encoder.c`

## meshcore

- **afe_init** (1 refs): `main\examples\afe\main.cpp`
- **es8311** (8 refs): `main\examples\afe\main.cpp`
- **i2s_init** (8 refs): `debug\examples\uvc_sc2336\components\cpp_bus_driver\src\bus\iis\hardware_iis.cpp`
- **i2s_read** (8 refs): `debug\examples\uvc_sc2336\components\cpp_bus_driver\src\bus\iis\hardware_iis.cpp`
- **i2s_write** (8 refs): `debug\examples\uvc_sc2336\components\cpp_bus_driver\src\bus\iis\hardware_iis.cpp`
- **vad** (1 refs): `main\examples\afe\main.cpp`
- **wakenet** (1 refs): `main\examples\afe\main.cpp`

## Meck-P4

- **afe_init** (1 refs): `main\examples\afe\main.cpp`
- **es8311** (8 refs): `main\examples\afe\main.cpp`
- **i2s_init** (8 refs): `debug\examples\uvc_sc2336\components\cpp_bus_driver\src\bus\iis\hardware_iis.cpp`
- **i2s_read** (8 refs): `debug\examples\uvc_sc2336\components\cpp_bus_driver\src\bus\iis\hardware_iis.cpp`
- **i2s_write** (8 refs): `debug\examples\uvc_sc2336\components\cpp_bus_driver\src\bus\iis\hardware_iis.cpp`
- **vad** (1 refs): `main\examples\afe\main.cpp`
- **wakenet** (1 refs): `main\examples\afe\main.cpp`

## Meck-P4-v2

- **afe_init** (1 refs): `main\examples\afe\main.cpp`
- **es8311** (8 refs): `main\examples\afe\main.cpp`
- **i2s_init** (8 refs): `debug\examples\uvc_sc2336\components\cpp_bus_driver\src\bus\iis\hardware_iis.cpp`
- **i2s_read** (8 refs): `debug\examples\uvc_sc2336\components\cpp_bus_driver\src\bus\iis\hardware_iis.cpp`
- **i2s_write** (8 refs): `debug\examples\uvc_sc2336\components\cpp_bus_driver\src\bus\iis\hardware_iis.cpp`
- **vad** (1 refs): `main\examples\afe\main.cpp`
- **wakenet** (1 refs): `main\examples\afe\main.cpp`

## T-Display-P4

- **afe_init** (1 refs): `main\examples\afe\main.cpp`
- **es8311** (8 refs): `main\examples\afe\main.cpp`
- **i2s_init** (8 refs): `debug\examples\uvc_sc2336\components\cpp_bus_driver\src\bus\iis\hardware_iis.cpp`
- **i2s_read** (8 refs): `debug\examples\uvc_sc2336\components\cpp_bus_driver\src\bus\iis\hardware_iis.cpp`
- **i2s_write** (8 refs): `debug\examples\uvc_sc2336\components\cpp_bus_driver\src\bus\iis\hardware_iis.cpp`
- **vad** (1 refs): `main\examples\afe\main.cpp`
- **wakenet** (1 refs): `main\examples\afe\main.cpp`

## T-Connection-P4-Pro

- **ringbuf** (8 refs): `lib\lvgl-9.2.0\src\misc\lv_rb.c`

## ESP32-P4-Platform

- **afe_init** (6 refs): `firmware\brookesia\components\brookesia_core\ai_framework\agent\audio_processor.c`
- **es8311** (2 refs): `examples\esp-idf\18_esp_brookesia_phone\components\esp32_p4_platform\include\bsp\esp32_p4_platform.h`
- **i2s_init** (4 refs): `firmware\brookesia\components\brookesia_core\ai_framework\agent\esp_gmf_setup_peripheral.c`
- **i2s_read** (6 refs): `firmware\brookesia\components\SpecAnalyzer\SpecAnalyzer.cpp`
- **i2s_write** (6 refs): `firmware\brookesia\components\VideoPlayer\VideoPlayer.cpp`
- **ringbuf** (8 refs): `firmware\brookesia\components\brookesia_core\ai_framework\agent\audio_processor.c`
- **vad** (2 refs): `firmware\brookesia\components\brookesia_core\ai_framework\agent\audio_processor.c`
- **wakenet** (2 refs): `firmware\brookesia\components\brookesia_core\ai_framework\agent\audio_processor.c`

## CrowPanel-P4


## esp32p4-c6-wifi-test


## SigurdOS


## meshtastic

- **apll** (1 refs): `src\modules\esp32\AudioModule.cpp`
- **dma_buf** (1 refs): `src\modules\esp32\AudioModule.cpp`
- **es8311** (1 refs): `src\platform\extra_variants\m5stack_cardputer_adv\variant.cpp`
- **i2s_init** (1 refs): `src\modules\esp32\AudioModule.cpp`
- **i2s_read** (1 refs): `src\modules\esp32\AudioModule.cpp`
- **i2s_write** (1 refs): `src\modules\esp32\AudioModule.cpp`

## meshtastic-firmware

- **apll** (1 refs): `src\modules\esp32\AudioModule.cpp`
- **dma_buf** (1 refs): `src\modules\esp32\AudioModule.cpp`
- **es8311** (1 refs): `src\platform\extra_variants\m5stack_cardputer_adv\variant.cpp`
- **i2s_init** (1 refs): `src\modules\esp32\AudioModule.cpp`
- **i2s_read** (1 refs): `src\modules\esp32\AudioModule.cpp`
- **i2s_write** (1 refs): `src\modules\esp32\AudioModule.cpp`

## jarvix

- **afe_init** (1 refs): `components\audio\audio_capture.c`
- **dma_buf** (2 refs): `main\i2s_loopback_benchmark.c`
- **es8311** (2 refs): `components\audio\bsp_extra.c`
- **i2s_init** (3 refs): `main\i2s_loopback_benchmark.c`
- **i2s_read** (4 refs): `main\i2s_loopback_benchmark.c`
- **i2s_write** (8 refs): `main\i2s_loopback_benchmark.c`
- **opus_dec** (8 refs): `components\audio\tts_player.c`
- **opus_enc** (8 refs): `components\opus\src\opus.h`
- **vad** (7 refs): `main\main.cpp`
- **wakenet** (1 refs): `components\audio\audio_capture.c`

## OpenMQTTGateway


## LoRaMon


## RadioLib


## SX1262-Arduino-ESP32-driver


## MeshCore-official


## MeshCore-dup


## trail-mate

- **apll** (2 refs): `platform\esp\arduino_common\src\input\morse_engine.cpp`
- **dma_buf** (3 refs): `platform\esp\arduino_common\src\input\morse_engine.cpp`
- **es8311** (4 refs): `platform\esp\idf_components\m5stack_tab5\include\bsp\m5stack_tab5.h`
- **i2s_init** (3 refs): `platform\esp\idf_components\m5stack_tab5\m5stack_tab5.c`
- **i2s_read** (5 refs): `platform\esp\idf_components\m5stack_tab5\m5stack_tab5.c`
- **i2s_write** (4 refs): `platform\esp\idf_components\m5stack_tab5\m5stack_tab5.c`
- **ringbuf** (1 refs): `modules\core_sys\include\sys\ringbuf.h`

## lunarcore


## meshcomod

- **apll** (1 refs): `examples\companion_radio\ui-touch\UITask.cpp`
- **dma_buf** (1 refs): `examples\companion_radio\ui-touch\UITask.cpp`
- **i2s_init** (1 refs): `examples\companion_radio\ui-touch\UITask.cpp`
- **i2s_write** (1 refs): `examples\companion_radio\ui-touch\UITask.cpp`

## akita-bridge


## awesome-meshcore


## RWKV-LM


## RWKV-X


## rwkv.cpp


## snntorch


## norse


## open-interpreter


## autogen


## gat45-p4
