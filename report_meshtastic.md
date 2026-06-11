# Rapport d'Analyse: Meshtastic (firmware-develop)
**Projet:** `meshtastic`

## Statistiques
- Fichiers scannes: 1185
- Fichiers avec matches: 491
- Lignes totales: 146969
- Matches total: 3683

## Distribution par Categorie
- **mesh**: 1815 ??????????????????????????????????????????????????
- **network**: 846 ??????????????????????????????????????????????????
- **timing**: 601 ??????????????????????????????????????????????????
- **rtos**: 161 ??????????????????????????????????????????????????
- **memory**: 125 ??????????????????????????????????????????????????
- **transport**: 118 ??????????????????????????????????????????????????
- **audio**: 17 ?????????????????

## ??  Findings Critiques (CRITICAL)
- `firmware-develop\src\platform\esp32\iram-quirk.c:11` [memory_placement] `IRAM_ATTR esp_err_t stub_probe(esp_flash_t *chip, uint32_t flash_id)`
- `firmware-develop\src\platform\esp32\IramMemcpy.c:23` [memory_placement] `static inline bool IRAM_ATTR cache_is_enabled(void)`
- `firmware-develop\src\platform\esp32\IramMemcpy.c:28` [memory_placement] `extern void *IRAM_ATTR __wrap_memcpy(void *dst, const void *src, size_t n)`
- `firmware-develop\src\platform\esp32\IramMemset.c:23` [memory_placement] `static inline bool IRAM_ATTR cache_is_enabled(void)`
- `firmware-develop\src\platform\esp32\IramMemset.c:28` [memory_placement] `extern void *IRAM_ATTR __wrap_memset(void *dst, int c, size_t n)`
- `firmware-develop\src\main.cpp:229` [flow_control] `bool pauseBluetoothLogging = false;`
- `firmware-develop\src\main.cpp:300` [flow_control] `// 3x: blink for 300 ms, pause for 300 ms`
- `firmware-develop\src\RedirectablePrint.cpp:222` [flow_control] `if (config.security.debug_log_api_enabled && !pauseBluetoothLogging) {`
- `firmware-develop\src\concurrency\BinarySemaphoreFreeRTOS.cpp:33` [memory_placement] `IRAM_ATTR void BinarySemaphoreFreeRTOS::giveFromISR(BaseType_t *pxHigherPriorityTaskWoken)`
- `firmware-develop\src\concurrency\BinarySemaphorePosix.cpp:76` [memory_placement] `IRAM_ATTR void BinarySemaphorePosix::giveFromISR(BaseType_t *pxHigherPriorityTaskWoken)`
- `firmware-develop\src\concurrency\BinarySemaphorePosix.cpp:99` [memory_placement] `IRAM_ATTR void BinarySemaphorePosix::giveFromISR(BaseType_t *pxHigherPriorityTaskWoken) {}`
- `firmware-develop\src\concurrency\InterruptableDelay.cpp:30` [memory_placement] `IRAM_ATTR void InterruptableDelay::interruptFromISR(BaseType_t *pxHigherPriorityTaskWoken)`
- `firmware-develop\src\concurrency\NotifiedWorkerThread.cpp:26` [memory_placement] `IRAM_ATTR bool NotifiedWorkerThread::notifyCommon(uint32_t v, bool overwrite)`
- `firmware-develop\src\concurrency\NotifiedWorkerThread.cpp:49` [memory_placement] `* This must be inline or IRAM_ATTR on ESP32`
- `firmware-develop\src\concurrency\NotifiedWorkerThread.cpp:51` [memory_placement] `IRAM_ATTR bool NotifiedWorkerThread::notifyFromISR(BaseType_t *highPriWoken, uint32_t v, bool overwrite)`
- `firmware-develop\src\graphics\Screen.cpp:186` [jitter_buffer] `// - Strong damping for tiny deltas (jitter)`
- `firmware-develop\src\graphics\Screen.cpp:243` [flow_control] `NotificationRenderer::pauseBanner = false;`
- `firmware-develop\src\graphics\Screen.cpp:257` [flow_control] `nodeDB->pause_sort(true);`
- `firmware-develop\src\graphics\Screen.cpp:263` [flow_control] `NotificationRenderer::pauseBanner = false;`
- `firmware-develop\src\graphics\Screen.cpp:285` [flow_control] `NotificationRenderer::pauseBanner = false;`
- `firmware-develop\src\graphics\Screen.cpp:310` [flow_control] `NotificationRenderer::pauseBanner = false;`
- `firmware-develop\src\graphics\Screen.cpp:965` [flow_control] `NotificationRenderer::pauseBanner = true;`
- `firmware-develop\src\graphics\Screen.cpp:979` [flow_control] `NotificationRenderer::pauseBanner = false;`
- `firmware-develop\src\graphics\Screen.cpp:1120` [flow_control] `EINK_ADD_FRAMEFLAG(dispdev, COSMETIC); // Really ugly to see ghosting from "screen paused"`
- `firmware-develop\src\mesh\NodeDB.cpp:2631` [flow_control] `void NodeDB::pause_sort(bool paused)`
- `firmware-develop\src\mesh\NodeDB.cpp:2633` [flow_control] `sortingIsPaused = paused;`
- `firmware-develop\src\mesh\NodeDB.cpp:2638` [flow_control] `if (!sortingIsPaused && (lastSort == 0 || !Throttle::isWithinTimespanMs(lastSort, 1000 * 5))) {`
- `firmware-develop\src\mesh\PhoneAPI.cpp:72` [flow_control] `pauseBluetoothLogging = true;`
- `firmware-develop\src\mesh\PhoneAPI.cpp:158` [flow_control] `pauseBluetoothLogging = false;`
- `firmware-develop\src\mesh\PhoneAPI.cpp:585` [flow_control] `pauseBluetoothLogging = false;`

## Detail par Sous-systeme

### clock_source (1 matches)
- `firmware-develop\src\modules\esp32\AudioModule.cpp:161` `.use_apll = false,`

### codec_init (1 matches)
- `firmware-develop\src\platform\extra_variants\m5stack_cardputer_adv\variant.cpp:77` `// extra ES8311 init`

### dma_buffer (2 matches)
- `firmware-develop\src\modules\esp32\AudioModule.cpp:159` `.dma_buf_count = 8,`

### encryption (192 matches)
- `firmware-develop\test\test_crypto\test_main.cpp:2` `#include "CryptoEngine.h"`

### ethernet (88 matches)
- `firmware-develop\src\mesh\NodeDB.cpp:992` `config.network.eth_enabled = true;`
- `firmware-develop\src\mesh\eth\ethClient.cpp:12` `#define ETH_DHCP_TIMEOUT_MS 10000`

### flow_control (51 matches)
- `firmware-develop\src\main.cpp:229` `bool pauseBluetoothLogging = false;`
- `firmware-develop\src\RedirectablePrint.cpp:222` `if (config.security.debug_log_api_enabled && !pauseBluetoothLogging) {`
- `firmware-develop\src\graphics\Screen.cpp:243` `NotificationRenderer::pauseBanner = false;`

### i2s_capture (1 matches)
- `firmware-develop\src\modules\esp32\AudioModule.cpp:218` `res = i2s_read(I2S_PORT, adc_buffer + adc_buffer_index, adc_buffer_size - adc_buffer_index, &bytesIn`

### i2s_driver (2 matches)
- `firmware-develop\src\modules\esp32\AudioModule.cpp:164` `res = i2s_driver_install(I2S_PORT, &i2s_config, 0, NULL);`

### i2s_playback (2 matches)
- `firmware-develop\src\modules\esp32\AudioModule.cpp:74` `i2s_write(I2S_PORT, &audioModule->output_buffer, audioModule->adc_buffer_size, &bytesOut,`

### jitter_buffer (6 matches)
- `firmware-develop\src\graphics\Screen.cpp:186` `// - Strong damping for tiny deltas (jitter)`
- `firmware-develop\src\modules\TrafficManagementModule.cpp:84` `* when GPS jitter causes small coordinate changes.`
- `firmware-develop\src\platform\nrf52\softdevice\nrf_soc.h:101` `#define NRF_RADIO_START_JITTER_US                                                                   `

### lora_radio (1402 matches)
- `firmware-develop\src\DisplayFormatters.cpp:8` `// If use_preset is false, always return "Custom" — callers such as RadioInterface and Channels`
- `firmware-develop\src\main.cpp:13` `#include "RadioLibInterface.h"`
- `firmware-develop\src\sleep.cpp:26` `#include <RadioLib.h>`

### memory_placement (17 matches)
- `firmware-develop\src\platform\esp32\iram-quirk.c:11` `IRAM_ATTR esp_err_t stub_probe(esp_flash_t *chip, uint32_t flash_id)`
- `firmware-develop\src\platform\esp32\IramMemcpy.c:23` `static inline bool IRAM_ATTR cache_is_enabled(void)`
- `firmware-develop\src\platform\esp32\IramMemset.c:23` `static inline bool IRAM_ATTR cache_is_enabled(void)`
- `firmware-develop\src\concurrency\BinarySemaphoreFreeRTOS.cpp:33` `IRAM_ATTR void BinarySemaphoreFreeRTOS::giveFromISR(BaseType_t *pxHigherPriorityTaskWoken)`
- `firmware-develop\src\concurrency\BinarySemaphorePosix.cpp:76` `IRAM_ATTR void BinarySemaphorePosix::giveFromISR(BaseType_t *pxHigherPriorityTaskWoken)`
- `firmware-develop\src\concurrency\InterruptableDelay.cpp:30` `IRAM_ATTR void InterruptableDelay::interruptFromISR(BaseType_t *pxHigherPriorityTaskWoken)`
- `firmware-develop\src\concurrency\NotifiedWorkerThread.cpp:26` `IRAM_ATTR bool NotifiedWorkerThread::notifyCommon(uint32_t v, bool overwrite)`

### mqtt (652 matches)
- `firmware-develop\.clusterfuzzlite\router_fuzzer.cpp:99` `moduleConfig.has_mqtt = true;`
- `firmware-develop\src\main.cpp:81` `#if !MESHTASTIC_EXCLUDE_MQTT`
- `firmware-develop\src\Power.cpp:66` `#if defined(DEBUG_HEAP_MQTT) && !MESHTASTIC_EXCLUDE_MQTT`

### psram_usage (108 matches)
- `firmware-develop\src\main.cpp:405` `#if defined(ARCH_ESP32) && defined(BOARD_HAS_PSRAM)`
- `firmware-develop\src\memGet.cpp:6` `* information about free heap, heap size, free psram and psram size. The functions are`

### reticulum (2 matches)
- `firmware-develop\src\mesh\generated\meshtastic\portnums.pb.h:148` `/* Reticulum Network Stack Tunnel App`

### routing (57 matches)
- `firmware-develop\test\test_mqtt\MQTT.cpp:363` `void test_sendDirectlyConnectedDecoded(void)`
- `firmware-develop\src\mesh\FloodingRouter.cpp:1` `#include "FloodingRouter.h"`

### sample_rate_config (2 matches)
- `firmware-develop\src\modules\esp32\AudioModule.cpp:154` `.sample_rate = 8000,`
- `firmware-develop\src\modules\Telemetry\Sensor\BME680Sensor.cpp:42` `if (!bme680.updateSubscription(sensorList, ARRAY_LEN(sensorList), BSEC_SAMPLE_RATE_LP)) {`

### spi_bridge (36 matches)
- `firmware-develop\src\graphics\TFTDisplay.cpp:39` `cfg.spi_host = ST7735_SPI_HOST; // ESP32-S2,S3,C3 : SPI2_HOST or SPI3_HOST / ESP32 : VSPI_HOST or HS`
- `firmware-develop\src\graphics\tftSetup.cpp:89` `.spi_host = (uint16_t)portduino_config.display_spi_dev_int}})`

### sync_word (162 matches)
- `firmware-develop\src\input\MPR121Keyboard.cpp:14` `#define _MPR121_REG_MAX_HALF_DELTA_RISING 0x2B`
- `firmware-develop\src\mesh\LR11x0Interface.cpp:98` `int res = lora.begin(getFreq(), bw, sf, cr, syncWord, power, preambleLength, tcxoVoltage);`
- `firmware-develop\src\mesh\LR20x0Interface.cpp:114` `int res = lora.begin(getFreq(), bw, sf, cr, syncWord, power, preambleLength, tcxoVoltage);`

### synchronization (14 matches)
- `firmware-develop\src\RedirectablePrint.cpp:26` `inDebugPrint = xSemaphoreCreateMutexStatic(&this->_MutexStorageSpace);`
- `firmware-develop\src\concurrency\BinarySemaphoreFreeRTOS.cpp:10` `BinarySemaphoreFreeRTOS::BinarySemaphoreFreeRTOS() : semaphore(xSemaphoreCreateBinary())`
- `firmware-develop\src\concurrency\Lock.cpp:9` `Lock::Lock() : handle(xSemaphoreCreateBinary())`

### task_pinning (12 matches)
- `firmware-develop\src\graphics\EInkParallelDisplay.cpp:128` `BaseType_t rc = xTaskCreatePinnedToCore(EInkParallelDisplay::asyncFullUpdateTask, "epd_full", 4096 /`
- `firmware-develop\src\graphics\tftSetup.cpp:134` `xTaskCreatePinnedToCore(tft_task_handler, "tft", TFT_TASK_STACK_SIZE, NULL, 1, NULL, 0);`
- `firmware-develop\variants\nrf52840\diy\nrf52_promicro_diy_tcxo\variant.h:184` `| Waveshare    | Core1262-HF      | yes  | Ext       |                                       |`
- `firmware-develop\variants\esp32s3\bpi_picow_esp32_s3\variant.h:30` `// WaveShare Core1262-868M OK`
- `firmware-develop\variants\esp32c6\m5stack_unitc6l\variant.h:26` `// WaveShare Core1262-868M OK`
- `firmware-develop\variants\esp32c3\ai-c3\variant.h:19` `// WaveShare Core1262-868M`
- `firmware-develop\variants\esp32c3\m5stack-stamp-c3\variant.h:29` `// WaveShare Core1262-868M OK`

### task_priority (52 matches)
- `firmware-develop\src\DebugConfiguration.cpp:89` `Syslog &Syslog::defaultPriority(uint16_t pri)`
- `firmware-develop\src\mesh\MeshPacketQueue.cpp:25` `auto p1p = getPriority(p1), p2p = getPriority(p2);`
- `firmware-develop\src\mesh\RadioInterface.cpp:757` `if (p->priority != 0)`
- `firmware-develop\src\platform\nrf52\main-nrf52.cpp:393` `NVIC_SetPriority(DebugMonitor_IRQn, 6UL);`
- `firmware-develop\src\DebugConfiguration.h:197` `Syslog &defaultPriority(uint16_t pri = LOGLEVEL_KERN);`
- `firmware-develop\src\freertosinc.h:39` `#define tskIDLE_PRIORITY 0`

### timestamp (601 matches)
- `firmware-develop\src\DebugConfiguration.cpp:194` `this->_client->print(int(millis() / 1000));`
- `firmware-develop\src\main.cpp:401` `serialSinceMsec = millis();`
- `firmware-develop\src\MessageStore.cpp:73` `sm.timestamp = millis() / 1000;`

### transport_queue (25 matches)
- `firmware-develop\src\input\InputBroker.cpp:62` `inputEventQueue = xQueueCreate(5, sizeof(InputEvent));`
- `firmware-develop\src\mesh\MeshService.cpp:70` `: toPhoneQueue(MAX_RX_TOPHONE), toPhoneQueueStatusQueue(MAX_RX_QUEUESTATUS_TOPHONE),`
- `firmware-develop\src\mesh\Router.cpp:40` `(MAX_RX_TOPHONE + MAX_RX_FROMRADIO + 2 * MAX_TX_QUEUE +                                             `
- `firmware-develop\src\mesh\mesh-pb-constants.h:26` `#ifndef MAX_RX_QUEUESTATUS_TOPHONE`
- `firmware-develop\src\mesh\MeshService.h:55` `StaticPointerQueue<meshtastic_QueueStatus, MAX_RX_QUEUESTATUS_TOPHONE> toPhoneQueueStatusQueue;`
- `firmware-develop\src\mesh\RadioInterface.h:18` `#define MAX_TX_QUEUE 16 // max number of packets which can be waiting for transmission`

### udp (106 matches)
- `firmware-develop\src\mesh\MeshModule.cpp:185` `service->sendToMesh(currentReply);`
- `firmware-develop\src\mesh\MeshService.cpp:114` `sendToPhone(packetPool.allocCopy(*mp));`
- `firmware-develop\src\mesh\Router.cpp:775` `// reply broadcast goes through MeshService::sendToMesh -> Router::sendLocal,`
- `firmware-develop\src\modules\CannedMessageModule.cpp:1078` `service->sendToMesh(p, RX_SRC_LOCAL, true);`
- `firmware-develop\src\modules\DetectionSensorModule.cpp:136` `service->sendToMesh(p);`

### watchdog (83 matches)
- `firmware-develop\src\sleep.cpp:151` `reason = "taskWatchdog";`
- `firmware-develop\variants\nrf52840\meshlink\variant.cpp:21` `digitalWrite(PIN_WD_EN, HIGH); // Enable the Watchdog at boot`

### wifi_power_save (6 matches)
- `firmware-develop\src\motion\BMI270Sensor.cpp:22` `#define BMI270_PWR_CONF_ADV_POWER_SAVE_DISABLED 0x00`
- `firmware-develop\src\mesh\wifi\WiFiAPClient.cpp:375` `esp_wifi_set_ps(WIFI_PS_NONE); // Disable radio power saving`
- `firmware-develop\src\graphics\niche\InkHUD\Applets\System\Menu\MenuApplet.cpp:572` `case TOGGLE_POWER_SAVE:`
- `firmware-develop\src\graphics\niche\InkHUD\Applets\System\Menu\MenuAction.h:113` `TOGGLE_POWER_SAVE,`