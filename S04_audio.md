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

## ha_voice

- **afe_init** (1 refs): `main\audio_capture.c`
- **es8311** (1 refs): `common_components\espressif__esp32_p4_function_ev_board\include\bsp\esp32_p4_function_ev_board.h`
- **i2s_init** (1 refs): `common_components\espressif__esp32_p4_function_ev_board\esp32_p4_function_ev_board.c`
- **i2s_read** (3 refs): `main\audio_capture.c`
- **i2s_write** (6 refs): `main\audio_capture.c`
- **ringbuf** (1 refs): `main\audio_ref_buffer.c`
- **vad** (6 refs): `main\audio_capture.c`
- **wakenet** (2 refs): `main\audio_capture.c`

## meshcore

- **afe_init** (1 refs): `main\examples\afe\main.cpp`
- **es8311** (8 refs): `main\examples\afe\main.cpp`
- **i2s_init** (8 refs): `debug\examples\uvc_sc2336\components\cpp_bus_driver\src\bus\iis\hardware_iis.cpp`
- **i2s_read** (8 refs): `debug\examples\uvc_sc2336\components\cpp_bus_driver\src\bus\iis\hardware_iis.cpp`
- **i2s_write** (8 refs): `debug\examples\uvc_sc2336\components\cpp_bus_driver\src\bus\iis\hardware_iis.cpp`
- **vad** (1 refs): `main\examples\afe\main.cpp`
- **wakenet** (1 refs): `main\examples\afe\main.cpp`

## meshtastic

- **apll** (1 refs): `src\modules\esp32\AudioModule.cpp`
- **dma_buf** (1 refs): `src\modules\esp32\AudioModule.cpp`
- **es8311** (1 refs): `src\platform\extra_variants\m5stack_cardputer_adv\variant.cpp`
- **i2s_init** (1 refs): `src\modules\esp32\AudioModule.cpp`
- **i2s_read** (1 refs): `src\modules\esp32\AudioModule.cpp`
- **i2s_write** (1 refs): `src\modules\esp32\AudioModule.cpp`

## jarvix

- **afe_init** (1 refs): `components\audio\audio_capture.c`
- **es8311** (1 refs): `components\meshcore\es8311.cpp`
- **i2s_init** (1 refs): `components\chmorgan__esp-audio-player\test\audio_player_test.c`
- **i2s_read** (1 refs): `components\audio\audio_capture.c`
- **i2s_write** (4 refs): `components\audio\audio_capture.c`
- **vad** (3 refs): `main\main.cpp`
- **wakenet** (1 refs): `components\audio\audio_capture.c`

## OpenMQTTGateway


## LoRaMon


## meshtastic-sniffer


## lorawan-sniffer


## RadioLib


## Meck-P4

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

## SigurdOS


## Meck-P4-v2

- **afe_init** (1 refs): `main\examples\afe\main.cpp`
- **es8311** (8 refs): `main\examples\afe\main.cpp`
- **i2s_init** (8 refs): `debug\examples\uvc_sc2336\components\cpp_bus_driver\src\bus\iis\hardware_iis.cpp`
- **i2s_read** (8 refs): `debug\examples\uvc_sc2336\components\cpp_bus_driver\src\bus\iis\hardware_iis.cpp`
- **i2s_write** (8 refs): `debug\examples\uvc_sc2336\components\cpp_bus_driver\src\bus\iis\hardware_iis.cpp`
- **vad** (1 refs): `main\examples\afe\main.cpp`
- **wakenet** (1 refs): `main\examples\afe\main.cpp`

## MeshCore-official


## meshtastic-firmware

- **apll** (1 refs): `src\modules\esp32\AudioModule.cpp`
- **dma_buf** (1 refs): `src\modules\esp32\AudioModule.cpp`
- **es8311** (1 refs): `src\platform\extra_variants\m5stack_cardputer_adv\variant.cpp`
- **i2s_init** (1 refs): `src\modules\esp32\AudioModule.cpp`
- **i2s_read** (1 refs): `src\modules\esp32\AudioModule.cpp`
- **i2s_write** (1 refs): `src\modules\esp32\AudioModule.cpp`

## trail-mate

- **apll** (2 refs): `platform\esp\arduino_common\src\input\morse_engine.cpp`
- **dma_buf** (3 refs): `platform\esp\arduino_common\src\input\morse_engine.cpp`
- **es8311** (4 refs): `platform\esp\idf_components\m5stack_tab5\include\bsp\m5stack_tab5.h`
- **i2s_init** (3 refs): `platform\esp\idf_components\m5stack_tab5\m5stack_tab5.c`
- **i2s_read** (5 refs): `platform\esp\idf_components\m5stack_tab5\m5stack_tab5.c`
- **i2s_write** (4 refs): `platform\esp\idf_components\m5stack_tab5\m5stack_tab5.c`
- **ringbuf** (1 refs): `modules\core_sys\include\sys\ringbuf.h`