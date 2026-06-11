# Rapport d'Analyse: Trail-Mate (MeshCore UI)
**Projet:** `trail_mate`

## Statistiques
- Fichiers scannes: 1823
- Fichiers avec matches: 353
- Lignes totales: 608728
- Matches total: 4318

## Distribution par Categorie
- **mesh**: 2082 ??????????????????????????????????????????????????
- **network**: 952 ??????????????????????????????????????????????????
- **timing**: 425 ??????????????????????????????????????????????????
- **rtos**: 249 ??????????????????????????????????????????????????
- **audio**: 240 ??????????????????????????????????????????????????
- **transport**: 230 ??????????????????????????????????????????????????
- **memory**: 140 ??????????????????????????????????????????????????

## ??  Findings Critiques (CRITICAL)
- `trail-mate\platform\esp\idf_common\src\platform_ui_device_runtime.cpp:69` [memory_placement] `stats.ram_total_bytes = heap_caps_get_total_size(MALLOC_CAP_INTERNAL | MALLOC_CAP_8BIT);`
- `trail-mate\platform\esp\idf_common\src\platform_ui_device_runtime.cpp:70` [memory_placement] `stats.ram_free_bytes = heap_caps_get_free_size(MALLOC_CAP_INTERNAL | MALLOC_CAP_8BIT);`
- `trail-mate\platform\esp\arduino_common\src\app_tasks.cpp:147` [flow_control] `bool AppTasks::radio_tasks_paused_ = false;`
- `trail-mate\platform\esp\arduino_common\src\app_tasks.cpp:194` [flow_control] `void AppTasks::pauseRadioTasks()`
- `trail-mate\platform\esp\arduino_common\src\app_tasks.cpp:196` [flow_control] `if (radio_tasks_paused_)`
- `trail-mate\platform\esp\arduino_common\src\app_tasks.cpp:200` [flow_control] `radio_tasks_paused_ = true;`
- `trail-mate\platform\esp\arduino_common\src\app_tasks.cpp:228` [flow_control] `if (!radio_tasks_paused_)`
- `trail-mate\platform\esp\arduino_common\src\app_tasks.cpp:232` [flow_control] `radio_tasks_paused_ = false;`
- `trail-mate\platform\esp\arduino_common\src\exclusive_lora_runtime.cpp:34` [flow_control] `if (!app::AppTasks::areRadioTasksPaused())`
- `trail-mate\platform\esp\arduino_common\src\exclusive_lora_runtime.cpp:36` [flow_control] `app::AppTasks::pauseRadioTasks();`
- `trail-mate\platform\esp\arduino_common\src\exclusive_lora_runtime.cpp:37` [flow_control] `out_session->paused_radio_tasks = true;`
- `trail-mate\platform\esp\arduino_common\src\exclusive_lora_runtime.cpp:57` [flow_control] `if (session->paused_radio_tasks)`
- `trail-mate\platform\esp\arduino_common\src\LV_Helper_v9.cpp:964` [memory_placement] `(unsigned)heap_caps_get_free_size(MALLOC_CAP_INTERNAL),`
- `trail-mate\platform\esp\arduino_common\src\LV_Helper_v9.cpp:965` [memory_placement] `(unsigned)heap_caps_get_free_size(MALLOC_CAP_DMA),`
- `trail-mate\platform\esp\arduino_common\src\LV_Helper_v9.cpp:978` [memory_placement] `buf = (lv_color16_t*)heap_caps_malloc(lv_buffer_size, MALLOC_CAP_DMA);`
- `trail-mate\platform\esp\arduino_common\src\LV_Helper_v9.cpp:979` [memory_placement] `buf1 = (lv_color16_t*)heap_caps_malloc(lv_buffer_size, MALLOC_CAP_DMA);`
- `trail-mate\platform\esp\arduino_common\src\LV_Helper_v9.cpp:1025` [memory_placement] `buf = (lv_color16_t*)heap_caps_malloc(lv_buffer_size, MALLOC_CAP_DMA);`
- `trail-mate\platform\esp\arduino_common\src\LV_Helper_v9.cpp:1026` [memory_placement] `buf1 = (lv_color16_t*)heap_caps_malloc(lv_buffer_size, MALLOC_CAP_DMA);`
- `trail-mate\platform\esp\arduino_common\src\LV_Helper_v9.cpp:1078` [memory_placement] `(unsigned)heap_caps_get_free_size(MALLOC_CAP_INTERNAL),`
- `trail-mate\platform\esp\arduino_common\src\LV_Helper_v9.cpp:1079` [memory_placement] `(unsigned)heap_caps_get_free_size(MALLOC_CAP_DMA),`
- `trail-mate\platform\esp\arduino_common\src\LV_Helper_v9.cpp:1201` [memory_placement] `return MALLOC_CAP_INTERNAL | MALLOC_CAP_8BIT;`
- `trail-mate\platform\esp\arduino_common\src\LV_Helper_v9.cpp:1208` [memory_placement] `return MALLOC_CAP_INTERNAL | MALLOC_CAP_8BIT;`
- `trail-mate\platform\esp\arduino_common\src\memory_diag.cpp:44` [memory_placement] `static_cast<unsigned>(heap_caps_get_free_size(MALLOC_CAP_INTERNAL | MALLOC_CAP_8BIT)),`
- `trail-mate\platform\esp\arduino_common\src\memory_diag.cpp:45` [memory_placement] `static_cast<unsigned>(heap_caps_get_largest_free_block(MALLOC_CAP_INTERNAL | MALLOC_CAP_8BIT)),`
- `trail-mate\platform\esp\arduino_common\src\platform_ui_device_runtime.cpp:67` [memory_placement] `stats.ram_total_bytes = heap_caps_get_total_size(MALLOC_CAP_INTERNAL | MALLOC_CAP_8BIT);`
- `trail-mate\platform\esp\arduino_common\src\platform_ui_device_runtime.cpp:68` [memory_placement] `stats.ram_free_bytes = heap_caps_get_free_size(MALLOC_CAP_INTERNAL | MALLOC_CAP_8BIT);`
- `trail-mate\platform\esp\arduino_common\src\platform_ui_firmware_update_runtime.cpp:498` [memory_placement] `static_cast<unsigned>(heap_caps_get_free_size(MALLOC_CAP_INTERNAL | MALLOC_CAP_8BIT)),`
- `trail-mate\platform\esp\arduino_common\src\platform_ui_firmware_update_runtime.cpp:499` [memory_placement] `static_cast<unsigned>(heap_caps_get_largest_free_block(MALLOC_CAP_INTERNAL | MALLOC_CAP_8BIT)),`
- `trail-mate\platform\esp\arduino_common\src\platform_ui_firmware_update_runtime.cpp:520` [memory_placement] `: (MALLOC_CAP_INTERNAL | MALLOC_CAP_8BIT);`
- `trail-mate\platform\esp\arduino_common\src\platform_ui_firmware_update_runtime.cpp:521` [memory_placement] `const uint32_t secondary_caps = prefer_psram ? (MALLOC_CAP_INTERNAL | MALLOC_CAP_8BIT)`

## Detail par Sous-systeme

### clock_source (2 matches)
- `trail-mate\platform\esp\arduino_common\src\input\morse_engine.cpp:159` `cfg.use_apll = true;`
- `trail-mate\platform\esp\arduino_audio_codec\audio\codec\esp_codec.cpp:312` `.use_apll = true,`

### codec_init (8 matches)
- `trail-mate\platform\esp\arduino_audio_codec\audio\codec\device\es8311\es8311.c:170` `static int es8311_config_fmt(audio_codec_es8311_t* codec, es_i2s_fmt_t fmt)`
- `trail-mate\boards\tlora_pager\src\tlora_pager_board.cpp:467` `log_d("Audio codec (ES8311) initialized successfully");`
- `trail-mate\platform\esp\idf_components\m5stack_tab5\include\bsp\m5stack_tab5.h:91` `*  - Codec ES8311 (configuration only)`
- `trail-mate\platform\esp\arduino_audio_codec\audio\codec\device\include\es8311_codec.h:22` `* @brief ES8311 codec configuration`

### dma_buffer (11 matches)
- `trail-mate\platform\esp\arduino_common\src\input\morse_engine.cpp:139` `if (config_.dma_buf_count <= 0)`
- `trail-mate\platform\esp\arduino_audio_codec\audio\codec\esp_codec.cpp:310` `.dma_buf_count = 2,`
- `trail-mate\platform\esp\arduino_common\include\input\morse_engine.h:48` `int dma_buf_count = 4;`

### encryption (222 matches)
- `trail-mate\platform\nrf52\arduino_common\src\chat\infra\meshcore\meshcore_radio_adapter.cpp:595` `const size_t cipher_len = ::chat::meshcore::encryptThenMac(key16,`
- `trail-mate\platform\nrf52\arduino_common\src\chat\infra\meshtastic\meshtastic_radio_adapter.cpp:2536` `if (!::chat::meshtastic::decryptPkiAesCcm(shared, sizeof(shared), nonce, 8,`
- `trail-mate\platform\linux\common\src\chat\linux_raw_lora_mesh_adapter.cpp:520` `bool aes_ctr_crypt(const std::uint8_t* key,`

### ethernet (4 matches)
- `trail-mate\modules\core_chat\generated\meshtastic\config.pb.h:479` `bool eth_enabled;`
- `trail-mate\modules\core_chat\generated\meshtastic\mesh.pb.h:238` `meshtastic_HardwareModel_T_ETH_ELITE = 91,`

### flow_control (68 matches)
- `trail-mate\platform\esp\arduino_common\src\app_tasks.cpp:147` `bool AppTasks::radio_tasks_paused_ = false;`
- `trail-mate\platform\esp\arduino_common\src\exclusive_lora_runtime.cpp:34` `if (!app::AppTasks::areRadioTasksPaused())`

### i2s_capture (12 matches)
- `trail-mate\platform\esp\idf_components\m5stack_tab5\m5stack_tab5.c:1158` `static esp_err_t bsp_i2s_read(void* audio_buffer, size_t len, size_t* bytes_read, uint32_t timeout_m`
- `trail-mate\platform\esp\arduino_audio_codec\audio\codec\platform\audio_codec_data_i2s.c:581` `int ret = i2s_channel_read(rx_chan, data, size, &bytes_read, 1000);`
- `trail-mate\platform\esp\arduino_common\src\input\morse_engine.cpp:286` `esp_err_t err = i2s_read(config_.i2s_port, buffer.data(), buffer.size() * sizeof(int16_t), &bytes_re`
- `trail-mate\boards\tab5\src\codec_compat.cpp:13` `typedef esp_err_t (*bsp_i2s_read_fn)(void* audio_buffer, size_t len, size_t* bytes_read, uint32_t ti`

### i2s_driver (9 matches)
- `trail-mate\platform\esp\idf_components\m5stack_tab5\m5stack_tab5.c:1018` `ESP_ERROR_CHECK(i2s_channel_init_std_mode(i2s_tx_chan, p_i2s_cfg));`
- `trail-mate\platform\esp\arduino_common\src\input\morse_engine.cpp:163` `if (i2s_driver_install(config_.i2s_port, &cfg, 0, nullptr) != ESP_OK)`
- `trail-mate\platform\esp\arduino_audio_codec\audio\codec\esp_codec.cpp:296` `ESP_ERROR_CHECK(i2s_channel_init_std_mode(tx_channel, &std_cfg_default));`

### i2s_playback (10 matches)
- `trail-mate\platform\esp\idf_components\m5stack_tab5\m5stack_tab5.c:1166` `static esp_err_t bsp_i2s_write(void* audio_buffer, size_t len, size_t* bytes_written, uint32_t timeo`
- `trail-mate\platform\esp\arduino_audio_codec\audio\codec\platform\audio_codec_data_i2s.c:611` `int ret = i2s_channel_write(tx_chan, data, size, &bytes_written, 1000);`
- `trail-mate\boards\tab5\src\codec_compat.cpp:14` `typedef esp_err_t (*bsp_i2s_write_fn)(void* audio_buffer, size_t len, size_t* bytes_written, uint32_`
- `trail-mate\platform\esp\idf_components\m5stack_tab5\include\bsp\m5stack_tab5.h:206` `typedef esp_err_t (*bsp_i2s_write_fn)(void* audio_buffer, size_t len, size_t* bytes_written, uint32_`

### jitter_buffer (45 matches)
- `trail-mate\platform\esp\arduino_common\src\gps\gps_service.cpp:745` `auto decision = service->jitter_filter_.update(raw_lat, raw_lon, now_ms, last_motion_ms);`
- `trail-mate\platform\esp\arduino_common\src\walkie\walkie_service.cpp:34` `constexpr uint8_t kJitterMinPrebufferFrames = 10; // ~200ms (5 frames/packet, 20ms per frame)`

### lora_radio (231 matches)
- `trail-mate\platform\linux\common\src\app\linux_app_services.cpp:198` `std::strcmp(value, "sx1262") == 0)`
- `trail-mate\platform\linux\common\src\chat\linux_raw_lora_mesh_adapter.cpp:796` `.text = "SX1262",`
- `trail-mate\platform\linux\common\src\platform\linux\sx126x_radio.cpp:61` `constexpr std::uint8_t kPaConfigDeviceSelSx1262 = 0x00;`

### memory_placement (33 matches)
- `trail-mate\platform\esp\idf_common\src\platform_ui_device_runtime.cpp:69` `stats.ram_total_bytes = heap_caps_get_total_size(MALLOC_CAP_INTERNAL | MALLOC_CAP_8BIT);`
- `trail-mate\platform\esp\arduino_common\src\LV_Helper_v9.cpp:964` `(unsigned)heap_caps_get_free_size(MALLOC_CAP_INTERNAL),`

### mqtt (945 matches)
- `trail-mate\platform\nrf52\runtime\nrf52_runtime_apply_service.cpp:31` `platform::nrf52::debug_console::printf("[gat562][cfg] applyMesh start proto=%u ok_to_mqtt=%u ignore_`
- `trail-mate\platform\nrf52\arduino_common\src\ble\app_phone_facade.cpp:101` `out.via_mqtt = entry.via_mqtt;`

### psram_usage (107 matches)
- `trail-mate\platform\esp\idf_components\m5stack_tab5\m5stack_tab5.c:1850` `.buff_spiram = cfg->flags.buff_spiram,`
- `trail-mate\platform\linux\common\src\platform\ui\device_runtime.cpp:128` `stats.psram_total_bytes = 0;`
- `trail-mate\platform\esp\idf_components\m5stack_tab5\trail_mate_tab5_runtime.cpp:98` `.buff_spiram = true,`
- `trail-mate\platform\esp\idf_components\t_display_p4\trail_mate_t_display_p4_runtime.cpp:632` `disp_cfg.flags.buff_spiram = false;`
- `trail-mate\platform\esp\idf_common\src\platform_ui_device_runtime.cpp:71` `stats.psram_total_bytes = heap_caps_get_total_size(MALLOC_CAP_SPIRAM);`

### reticulum (596 matches)
- `trail-mate\platform\esp\arduino_common\src\chat\infra\lxmf\lxmf_adapter.cpp:25` `constexpr size_t kMaxPacketLen = reticulum::kReticulumMtu;`

### ring_buffer (12 matches)
- `trail-mate\modules\ui_shared\src\ui\menu\dashboard\dashboard_compass_widget.cpp:266` `char bearing_buf[48];`
- `trail-mate\modules\ui_mono_128x64\src\runtime.cpp:2295` `char bearing_buf[10] = {};`
- `trail-mate\modules\core_sys\include\sys\ringbuf.h:2` `* @file ringbuf.h`

### routing (35 matches)
- `trail-mate\platform\nrf52\arduino_common\src\mesh\nrf52_mesh_runtime_shell.cpp:26` `::mesh::SendResult Nrf52MeshRuntimeShell::sendDirect(`
- `trail-mate\platform\linux\common\src\mesh\linux_mesh_runtime_shell.cpp:26` `::mesh::SendResult LinuxMeshRuntimeShell::sendDirect(`
- `trail-mate\platform\esp\arduino_common\src\mesh\esp_meshtastic_adapter_bridge.cpp:144` `::mesh::SendResult EspMeshtasticAdapterBridge::sendDirect(const ::mesh::DirectMessageCommand& comman`
- `trail-mate\platform\esp\arduino_common\src\mesh\esp_mesh_runtime_shell.cpp:26` `::mesh::SendResult EspMeshRuntimeShell::sendDirect(`
- `trail-mate\platform\esp\arduino_common\src\chat\infra\meshcore\meshcore_adapter.cpp:2826` `sendDirectTextDetailed(channel, text, peer, kTxtTypePlain, &ack_value, nullptr, nullptr);`

### sample_rate_config (131 matches)
- `trail-mate\third_party\codec2\src\codec2.c:1593` `resample_rate_L(&c2->c2const, &model_, rate_K_vec_, c2->rate_K_sample_freqs_kHz, K);`
- `trail-mate\third_party\codec2\src\fdmdv.c:2070` `due to fs=8000 Hz in our simulation noise BW */`
- `trail-mate\third_party\codec2\src\freedv_1600.c:41` `f->modem_sample_rate = FREEDV_FS_8000;`
- `trail-mate\third_party\codec2\src\freedv_2020.c:40` `f->speech_sample_rate = FREEDV_FS_16000;`
- `trail-mate\third_party\codec2\src\freedv_700.c:49` `f->modem_sample_rate = FREEDV_FS_8000;                                       // note weird sample ra`

### spi_bridge (12 matches)
- `trail-mate\platform\esp\idf_common\src\sx126x_radio.cpp:92` `const char* spi_host_name(int host)`

### sync_word (998 matches)
- `trail-mate\third_party\codec2\src\freedv_data_channel.c:58` `0x0840, 0x19c9, 0x2b52, 0x3adb, 0x4e64, 0x5fed, 0x6d76, 0x7cff,`
- `trail-mate\platform\esp\idf_components\t_display_p4\rm69a10_driver.c:36` `{0x2B, (uint8_t[]){0x00, 0x00, 0x04, 0xCF}, 4, 0},`
- `trail-mate\platform\esp\idf_components\sensor_bmi270\src\bmi270.c:157` `0xc8, 0x01, 0x50, 0x98, 0x2e, 0x55, 0xcc, 0xe1, 0x6f, 0x2b, 0x50, 0x98, 0x2e, 0xe0, 0xc9, 0xfb, 0x6f`

### synchronization (178 matches)
- `trail-mate\platform\esp\idf_components\m5stack_tab5\m5stack_tab5.c:49` `static SemaphoreHandle_t sys_i2c_reinit_mutex = NULL;`

### task_pinning (1 matches)
- `trail-mate\platform\esp\arduino_common\src\sstv\sstv_service.cpp:1357` `BaseType_t ok = xTaskCreatePinnedToCore(`

### task_priority (29 matches)
- `trail-mate\platform\esp\arduino_common\src\platform_ui_firmware_update_runtime.cpp:44` `constexpr UBaseType_t kWorkerPriority = 4;`
- `trail-mate\platform\esp\arduino_common\src\ui\widgets\map\map_tiles.cpp:1529` `ensure_tile(ctx, 0, 0, zoom, 0); // Priority 0 = center tile, use current zoom`
- `trail-mate\modules\ui_shared\tests\test_team_rich_payload_projector.cpp:94` `command.priority = 3;`
- `trail-mate\apps\linux_uconsole_gtk\src\platform\gtk\gtk_uconsole_map_logic.cpp:750` `int priority = 0;`
- `trail-mate\apps\esp32_lvgl\tests\esp32_lvgl_runtime_config_smoke.cpp:17` `assert(config.loop_priority == 5);`
- `trail-mate\platform\linux\common\include\ui\widgets\map\map_tiles.h:65` `int priority = 0;`
- `trail-mate\platform\esp\arduino_common\include\input\morse_engine.h:51` `UBaseType_t task_priority = 3;`
- `trail-mate\modules\ui_shared\include\ui\team_actions\team_action_types.h:66` `uint8_t priority = 0;`

### timestamp (425 matches)
- `trail-mate\platform\esp\idf_components\m5stack_tab5\m5stack_tab5.c:214` `uint32_t now_ms = esp_timer_get_time() / 1000;`
- `trail-mate\platform\esp\idf_components\sensor_bmi270\src\accel_gyro_bmi270.c:437` `uint32_t now = esp_timer_get_time() / 1000; // Convert to milliseconds`
- `trail-mate\platform\esp\idf_components\sensor_bmi270\src\bmi2.c:4328` `/* Wait for greater than 2 milliseconds */`
- `trail-mate\platform\nrf52\arduino_common\src\ble\meshtastic_ble.cpp:312` `last_ble_activity_ms_ = millis();`

### transport_queue (60 matches)
- `trail-mate\third_party\codec2\src\mpdecode_core.c:682` `void symbols_to_llrs(float llr[], COMP rx_qpsk_symbols[], float rx_amps[], float EsNo, float mean_am`
- `trail-mate\platform\esp\idf_common\src\ui_dispatcher.cpp:38` `s_queue = xQueueCreate(kQueueDepth, sizeof(Event));`
- `trail-mate\platform\esp\arduino_common\src\app_tasks.cpp:140` `QueueHandle_t AppTasks::radio_tx_queue_ = nullptr;`

### udp (3 matches)
- `trail-mate\modules\ui_shared\src\ui\screens\chat\chat_compose_components.cpp:154` `void ChatComposeScreen::showSendToast(bool ok, bool timeout, const char* message)`
- `trail-mate\modules\ui_shared\include\ui\screens\chat\chat_compose_components.h:67` `void showSendToast(bool ok, bool timeout, const char* message);`

### watchdog (41 matches)
- `trail-mate\platform\esp\idf_components\sensor_bmi270\src\bmi2.c:3415` `* @brief This API sets the i2c watchdog enable in the sensor.`

### wifi_power_save (90 matches)
- `trail-mate\platform\esp\idf_components\sensor_bmi270\src\bmi2.c:1976` `dev->delay_us(BMI2_POWER_SAVE_MODE_DELAY_IN_US, dev->intf_ptr);`