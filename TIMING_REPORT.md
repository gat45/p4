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
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\esp_hosted_coprocessor.c:642` `uint32_t currtime_us = esp_timer_get_time();`
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\host_power_save.c:162` `#define GET_CURR_TIME_IN_MS() esp_timer_get_time()/1000`
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\host_power_save.c:233` `host_wakeup_time = esp_timer_get_time() / 1000; /* Convert to ms */`
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\nw_split_router.c:279` `uint64_t current_time = esp_timer_get_time() >> 10; /* Approx ms */`
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\nw_split_router.c:314` `uint64_t current_time = esp_timer_get_time() >> 10; /* Approx ms */`

### ESP-ADF (Audio Framework)
- `esp-adf\components\audio_sal\audio_sys.c:62` `int64_t milliseconds = te.tv_sec * 1000LL + te.tv_usec / 1000;`
- `esp-adf\components\audio_sal\audio_sys.c:63` `return milliseconds;`
- `esp-adf\components\ota_service\ota_proc_default.c:61` `int64_t cur_time = esp_timer_get_time();`
- `esp-adf\components\ota_service\ota_proc_default.c:180` `int64_t last_time = esp_timer_get_time();`
- `esp-adf\components\ota_service\ota_proc_default.c:280` `int64_t last_time = esp_timer_get_time();`

### Xiaozhi-ESP32 (Voice Assistant)
- `xiaozhi-esp32\main\protocols\protocol.h:21` `uint32_t timestamp;     // Timestamp in milliseconds (used for server-side AEC)`
- `xiaozhi-esp32\main\boards\electron-bot\oscillator.h:67` `long previous_millis_;`
- `xiaozhi-esp32\main\boards\electron-bot\oscillator.h:68` `long current_millis_;`
- `xiaozhi-esp32\main\boards\electron-bot\oscillator.h:77` `long previous_servo_command_millis_;`
- `xiaozhi-esp32\main\boards\esp-s3-lcd-ev-board\esp_lcd_gc9503.h:30` `unsigned int delay_ms;  /*<! Delay in milliseconds after this command */`

### MeshCore (LoRa Mesh)
- `Meck-P4-main\components\esp_video\examples\capture_stream\main\capture_stream_main.c:351` `int64_t start_time_us = esp_timer_get_time();`
- `Meck-P4-main\components\esp_video\examples\capture_stream\main\capture_stream_main.c:352` `while (esp_timer_get_time() - start_time_us < (CAPTURE_SECONDS * 1000 * 1000)) {`
- `Meck-P4-main\components\esp_video\examples\image_storage\sd_card\main\sd_card_main.c:659` `us = esp_timer_get_time();`
- `Meck-P4-main\components\esp_video\examples\image_storage\sd_card\main\sd_card_main.c:689` `current_time_us = esp_timer_get_time();`
- `Meck-P4-main\components\esp_video\examples\image_storage\sd_card\main\sd_card_main.c:729` `int64_t start_time_us = esp_timer_get_time();`

### Meshtastic (LoRa Mesh)
- `firmware-develop\src\DebugConfiguration.cpp:194` `this->_client->print(int(millis() / 1000));`
- `firmware-develop\src\main.cpp:401` `serialSinceMsec = millis();`
- `firmware-develop\src\main.cpp:1178` `lastRadioMissedIrqPoll = millis();`
- `firmware-develop\src\main.cpp:1185` `lastAgcReset = millis();`
- `firmware-develop\src\main.cpp:1193` `lastPrint = millis();`

### JARVIX-OS (Notre Projet)
- `JARVIX-OS\components\lora_scanner\lora_scanner.c:216` `uint32_t window_start = xTaskGetTickCount() * portTICK_PERIOD_MS;`
- `JARVIX-OS\components\lora_scanner\lora_scanner.c:244` `uint32_t elapsed = (xTaskGetTickCount() * portTICK_PERIOD_MS) - window_start;`
- `JARVIX-OS\components\lora_scanner\lora_scanner.c:265` `window_start = xTaskGetTickCount() * portTICK_PERIOD_MS;`
- `JARVIX-OS\components\meshcore\MeckUI.cpp:494` `static uint32_t   g_delete_confirm_until = 0;   // millis deadline for tap-again`
- `JARVIX-OS\components\meshcore\MeckUI.cpp:555` `static uint32_t  g_voice_send_complete_ms   = 0;     // millis when send should be done`

## Risques Temporels par Sous-systeme

| Risque | Impact | Mitigation | Source |
|---|---|---|---|
| DMA underrun (I2S) | Audio clic/crash | IRAM_ATTR buffers, APLL clock | ha_voice |
| SDIO burst collapse | Perte frames | Backpressure + queue sizing | esp_hosted |
| WiFi modem sleep jitter | Latence fantome 5-10ms | WIFI_PS_NONE | ha_voice |
| Opus encode spike | CPU overload | Mesurer sur P4, reduire complexity | esp_adf |
| RTOS priority inversion | Audio bloque | Strict priority hierarchy | tous |
| Clock drift P4<->C6 | Buffer overflow/underflow | Timestamp sync | esp_hosted |
