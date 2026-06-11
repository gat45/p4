# Rapport Temporel: Contraintes de Latence et Jitter

## Modele de Latence End-to-End

```
Micro -> I2S DMA (P4) -> Opus Encode (P4) -> SDIO -> C6 -> WiFi -> Reseau -> Serveur
   ?         ?                ?              ?       ?       ?
   ?     ~1-5 ms           ~2-5 ms        ~1-3ms  ~1-5ms  variable
   ?                                              ?
   ?????? jitter buffer P4 (20-40 ms) ?????????????
                   ?
                   ??????? jitter buffer C6 (80-150 ms) ???????
```

## Budget de Latence Total

| Composant | Latence Min | Latence Max | Jitter Acceptable |
|---|---|---|---|
| I2S DMA (P4) | 1 ms | 5 ms | < 2 ms |
| Opus Encode (P4) | 2 ms | 5 ms | < 1 ms |
| SDIO Transport | 1 ms | 3 ms | < 2 ms |
| WiFi TX (C6) | 1 ms | 10 ms | < 5 ms |
| Network (LAN) | 0.5 ms | 5 ms | < 3 ms |
| **Total** | **5.5 ms** | **28 ms** | **< 13 ms** |

## Points de Mesure Critiques

### Home Assistant Voice Assistant (P4+C6)
- `Home-Assistant-MQTT-Voice-Assistant\main\main.c:202` `(unsigned long long)(esp_timer_get_time() / 1000000ULL));`
- `Home-Assistant-MQTT-Voice-Assistant\main\main.c:755` `int64_t last_change = esp_timer_get_time();`
- `Home-Assistant-MQTT-Voice-Assistant\main\main.c:759` `int64_t now = esp_timer_get_time();`
- `Home-Assistant-MQTT-Voice-Assistant\main\oled_status.c:398` `uint64_t uptime = (uint64_t)(esp_timer_get_time() / 1000000ULL);`
- `Home-Assistant-MQTT-Voice-Assistant\main\oled_status.c:644` `int64_t last_page_switch = esp_timer_get_time();`

### ESP-Hosted (P4<->C6 Bridge)
- `esp-hosted\esp_hosted_fg\host\stm32\port\src\platform_wrapper.c:22` `#define MILLISEC_TO_SEC			1000`
- `esp-hosted\esp_hosted_fg\host\stm32\port\src\platform_wrapper.c:24` `#define SEC_TO_MILLISEC(x) (1000*(x))`
- `esp-hosted\esp_hosted_fg\host\stm32\port\src\platform_wrapper.c:247` `return osSemaphoreWait(*sem_id, SEC_TO_MILLISEC(timeout));`
- `esp-hosted\esp_hosted_fg\host\stm32\port\src\platform_wrapper.c:354` `ret = osTimerStart (timer_handle->timer_id, SEC_TO_MILLISEC(duration));`
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\esp_hosted_coprocessor.c:642` `uint32_t currtime_us = esp_timer_get_time();`

### ESP-ADF (Audio Framework)
- `esp-adf\examples\protocols\rtmp\main\rtmp_push_app.c:163` `uint32_t start_time = esp_timer_get_time() / 1000;`
- `esp-adf\examples\protocols\rtmp\main\rtmp_push_app.c:166` `uint32_t cur_time = esp_timer_get_time() / 1000;`
- `esp-adf\examples\protocols\rtmp\main\rtmp_server_app.c:107` `uint32_t start_time = esp_timer_get_time() / 1000;`
- `esp-adf\examples\protocols\rtmp\main\rtmp_server_app.c:110` `uint32_t cur_time = esp_timer_get_time() / 1000;`
- `esp-adf\examples\protocols\rtmp\main\rtmp_src_app.c:64` `uint32_t start_time = esp_timer_get_time() / 1000;`

### Xiaozhi-ESP32 (Voice Assistant)
- `xiaozhi-esp32\main\protocols\protocol.h:21` `uint32_t timestamp;     // Timestamp in milliseconds (used for server-side AEC)`
- `xiaozhi-esp32\main\display\lvgl_display\gif\lvgl_gif.h:62` `* Get loop delay in milliseconds (delay between loops)`
- `xiaozhi-esp32\main\display\lvgl_display\gif\lvgl_gif.h:67` `* Set loop delay in milliseconds (delay between loops)`
- `xiaozhi-esp32\main\display\lvgl_display\gif\lvgl_gif.h:68` `* @param delay_ms Delay in milliseconds before starting next loop. 0 means no delay.`
- `xiaozhi-esp32\main\display\lvgl_display\gif\lvgl_gif.h:101` `uint32_t loop_delay_ms_;      // Delay between loops in milliseconds`

### MeshCore (LoRa Mesh)
- `Meck-P4-main\debug\examples\video_lcd_display\main\main.c:92` `start_time = esp_timer_get_time();  // Get the initial time for frame rate statistics`
- `Meck-P4-main\debug\examples\video_lcd_display\main\main.c:101` `int64_t end_time = esp_timer_get_time();`
- `Meck-P4-main\debug\examples\hi8561_ov5640\components\esp_video\src\data_reprocessing\esp32p4\esp_video_swap_short.c:132` `int64_t start_time_us = esp_timer_get_time();`
- `Meck-P4-main\debug\examples\hi8561_ov5640\components\esp_video\src\data_reprocessing\esp32p4\esp_video_swap_short.c:147` `int64_t end_time_us = esp_timer_get_time();`
- `Meck-P4-main\debug\examples\hi8561_ov5640\components\esp_video\examples\video_custom_format\main\app_main.c:219` `int64_t start_time_us = esp_timer_get_time();`

### Meshtastic (firmware-develop)
- `firmware-develop\src\DebugConfiguration.cpp:194` `this->_client->print(int(millis() / 1000));`
- `firmware-develop\src\main.cpp:401` `serialSinceMsec = millis();`
- `firmware-develop\src\main.cpp:1178` `lastRadioMissedIrqPoll = millis();`
- `firmware-develop\src\main.cpp:1185` `lastAgcReset = millis();`
- `firmware-develop\src\main.cpp:1193` `lastPrint = millis();`

### Trail-Mate (MeshCore UI)
- `trail-mate\platform\esp\idf_components\m5stack_tab5\m5stack_tab5.c:214` `uint32_t now_ms = esp_timer_get_time() / 1000;`
- `trail-mate\platform\esp\idf_components\sensor_bmi270\src\accel_gyro_bmi270.c:437` `uint32_t now = esp_timer_get_time() / 1000; // Convert to milliseconds`
- `trail-mate\platform\esp\idf_components\sensor_bmi270\src\accel_gyro_bmi270.c:517` `uint32_t now = esp_timer_get_time() / 1000; // Convert to milliseconds`
- `trail-mate\platform\esp\idf_components\sensor_bmi270\src\accel_gyro_bmi270.c:534` `uint64_t m = (uint64_t)esp_timer_get_time();`
- `trail-mate\platform\esp\idf_components\sensor_bmi270\src\accel_gyro_bmi270.c:540` `while ((uint64_t)esp_timer_get_time() > e)`

### meshecomod (MeshCore bridge)
- `meshcomod\src\Dispatcher.cpp:15` `#define MAX_RX_DELAY_MILLIS        32000  // 32 seconds`
- `meshcomod\src\Dispatcher.cpp:27` `radio_nonrx_start = _ms->getMillis();`
- `meshcomod\src\Dispatcher.cpp:32` `last_budget_update = _ms->getMillis();`
- `meshcomod\src\Dispatcher.cpp:43` `unsigned long now = _ms->getMillis();`
- `meshcomod\src\Dispatcher.cpp:71` `if (millisHasNowPassed(next_floor_calib_time)) {`

### Meck-P4 (T-Display P4 UI)
- `Meck-P4\debug\examples\video_lcd_display\main\main.c:92` `start_time = esp_timer_get_time();  // Get the initial time for frame rate statistics`
- `Meck-P4\debug\examples\video_lcd_display\main\main.c:101` `int64_t end_time = esp_timer_get_time();`
- `Meck-P4\debug\examples\hi8561_ov5640\components\esp_video\src\data_reprocessing\esp32p4\esp_video_swap_short.c:132` `int64_t start_time_us = esp_timer_get_time();`
- `Meck-P4\debug\examples\hi8561_ov5640\components\esp_video\src\data_reprocessing\esp32p4\esp_video_swap_short.c:147` `int64_t end_time_us = esp_timer_get_time();`
- `Meck-P4\debug\examples\hi8561_ov5640\components\esp_video\examples\video_custom_format\main\app_main.c:219` `int64_t start_time_us = esp_timer_get_time();`

### T-Display-P4 (official)
- `T-Display-P4\debug\examples\video_lcd_display\main\main.c:92` `start_time = esp_timer_get_time();  // Get the initial time for frame rate statistics`
- `T-Display-P4\debug\examples\video_lcd_display\main\main.c:101` `int64_t end_time = esp_timer_get_time();`
- `T-Display-P4\debug\examples\hi8561_ov5640\components\esp_video\src\data_reprocessing\esp32p4\esp_video_swap_short.c:132` `int64_t start_time_us = esp_timer_get_time();`
- `T-Display-P4\debug\examples\hi8561_ov5640\components\esp_video\src\data_reprocessing\esp32p4\esp_video_swap_short.c:147` `int64_t end_time_us = esp_timer_get_time();`
- `T-Display-P4\debug\examples\hi8561_ov5640\components\esp_video\examples\video_custom_format\main\app_main.c:219` `int64_t start_time_us = esp_timer_get_time();`

### JARVIX-OS (Notre Projet)
- `JARVIX-OS\main\i2s_loopback_benchmark.c:219` `int64_t t0 = esp_timer_get_time();`
- `JARVIX-OS\main\i2s_loopback_benchmark.c:230` `int64_t t1 = esp_timer_get_time();`
- `JARVIX-OS\main\i2s_loopback_benchmark.c:277` `int64_t t0 = esp_timer_get_time();`
- `JARVIX-OS\main\i2s_loopback_benchmark.c:288` `int64_t t1 = esp_timer_get_time();`
- `JARVIX-OS\main\i2s_loopback_benchmark.c:304` `int64_t t_start = esp_timer_get_time();`

## Risques Temporels par Sous-systeme

| Risque | Impact | Mitigation | Source |
|---|---|---|---|
| DMA underrun (I2S) | Audio clic/crash | IRAM_ATTR buffers, APLL clock | ha_voice |
| SDIO burst collapse | Perte frames | Backpressure + queue sizing | esp_hosted |
| WiFi modem sleep jitter | Latence fantome 5-10ms | WIFI_PS_NONE | ha_voice |
| Opus encode spike | CPU overload | Mesurer sur P4, reduire complexity | esp_adf |
| RTOS priority inversion | Audio bloque | Strict priority hierarchy | tous |
| Clock drift P4<->C6 | Buffer overflow/underflow | Timestamp sync | esp_hosted |
