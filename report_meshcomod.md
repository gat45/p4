# Rapport d'Analyse: meshecomod (MeshCore bridge)
**Projet:** `meshcomod`

## Statistiques
- Fichiers scannes: 636
- Fichiers avec matches: 273
- Lignes totales: 112790
- Matches total: 2140

## Distribution par Categorie
- **mesh**: 1053 ??????????????????????????????????????????????????
- **timing**: 670 ??????????????????????????????????????????????????
- **memory**: 166 ??????????????????????????????????????????????????
- **rtos**: 95 ??????????????????????????????????????????????????
- **transport**: 70 ??????????????????????????????????????????????????
- **network**: 67 ??????????????????????????????????????????????????
- **audio**: 19 ???????????????????

## ??  Findings Critiques (CRITICAL)
- `meshcomod\src\helpers\esp32\MultiTransportCompanionInterface.cpp:6` [flow_control] `: _tcp_port(0), _ws_port(0), _tcp_started(false), _ws_started(false), _tcp_enabled(true), _isEnabled(false), _broadcast(`
- `meshcomod\src\helpers\esp32\MultiTransportCompanionInterface.cpp:125` [flow_control] `_ota_ws_listen_paused = false;`
- `meshcomod\src\helpers\esp32\MultiTransportCompanionInterface.cpp:159` [flow_control] `_ws.pauseListen();`
- `meshcomod\src\helpers\esp32\MultiTransportCompanionInterface.cpp:160` [flow_control] `_ota_ws_listen_paused = true;`
- `meshcomod\src\helpers\esp32\MultiTransportCompanionInterface.cpp:161` [flow_control] `meshcoreRepeaterTcpOtaEmitLine("OTA: paused WS listen (client kept, no new connections)");`
- `meshcomod\src\helpers\esp32\MultiTransportCompanionInterface.cpp:185` [flow_control] `if (_ota_ws_listen_paused) {`
- `meshcomod\src\helpers\esp32\MultiTransportCompanionInterface.cpp:187` [flow_control] `_ota_ws_listen_paused = false;`
- `meshcomod\src\helpers\esp32\WebSocketCompanionServer.cpp:96` [flow_control] `void WebSocketCompanionServer::pauseListen() {`
- `meshcomod\src\helpers\input\TDeckTrackball.cpp:27` [memory_placement] `static void IRAM_ATTR isrUp()    { ++s_cnt_up; }`
- `meshcomod\src\helpers\input\TDeckTrackball.cpp:28` [memory_placement] `static void IRAM_ATTR isrDown()  { ++s_cnt_down; }`
- `meshcomod\src\helpers\input\TDeckTrackball.cpp:29` [memory_placement] `static void IRAM_ATTR isrLeft()  { ++s_cnt_left; }`
- `meshcomod\src\helpers\input\TDeckTrackball.cpp:30` [memory_placement] `static void IRAM_ATTR isrRight() { ++s_cnt_right; }`
- `meshcomod\examples\repeater_tcp\main.cpp:56` [flow_control] `static bool s_rep_ota_ws_listen_paused = false;`
- `meshcomod\examples\repeater_tcp\main.cpp:61` [flow_control] `s_rep_ota_ws_listen_paused = false;`
- `meshcomod\examples\repeater_tcp\main.cpp:78` [flow_control] `ws_server.pauseListen();`
- `meshcomod\examples\repeater_tcp\main.cpp:79` [flow_control] `s_rep_ota_ws_listen_paused = true;`
- `meshcomod\examples\repeater_tcp\main.cpp:80` [flow_control] `meshcoreRepeaterTcpOtaEmitLine("OTA: paused repeater WS listen (client kept)");`
- `meshcomod\examples\repeater_tcp\main.cpp:90` [flow_control] `if (s_rep_ota_ws_listen_paused && s_rep_ws_started) {`
- `meshcomod\examples\repeater_tcp\main.cpp:92` [flow_control] `s_rep_ota_ws_listen_paused = false;`
- `meshcomod\examples\repeater_tcp\main.cpp:107` [flow_control] `s_rep_ota_ws_listen_paused = false;`
- `meshcomod\examples\companion_radio\ui-touch\UITask.cpp:302` [dma_buffer] `cfg.dma_buf_count = 4;`
- `meshcomod\examples\companion_radio\ui-touch\UITask.cpp:303` [dma_buffer] `cfg.dma_buf_len = 256;`
- `meshcomod\examples\companion_radio\ui-touch\UITask.cpp:1524` [jitter_buffer] `// The old fixed-step jump on release was the source of "jittery / jumpy"`
- `meshcomod\examples\companion_radio\ui-touch\UITask.cpp:8711` [jitter_buffer] `// Per-board battery sampler: EMA over the noisy ADC so the value doesn't jitter`
- `meshcomod\examples\companion_radio\ui-touch\UITask.cpp:8749` [jitter_buffer] `// Normally hold for 20 s to kill jitter — BUT publish at once when the charge`
- `meshcomod\examples\companion_radio\ui-touch\UITask.cpp:13278` [jitter_buffer] `// pixels of jitter back to the proper grid.`
- `meshcomod\examples\companion_radio\ui-touch\UITask.cpp:13329` [jitter_buffer] `// jitter we introduced during PRESSING goes away.`
- `meshcomod\examples\companion_radio\ui-touch\UITask.cpp:1444` [flow_control] `"Wi-Fi update is paused while we fix some issues.\n"`
- `meshcomod\examples\companion_radio\ui-touch\UITask.cpp:1450` [flow_control] `g_lv.task->showAlert("Update manually at flasher.meshcomod.com\n(Wi-Fi update is paused for now)", 3500);`
- `meshcomod\examples\companion_radio\ui-touch\UITask.cpp:1938` [flow_control] `// place; a short pause (or tapping a different key) commits the highlighted one.`

## Detail par Sous-systeme

### clock_source (1 matches)
- `meshcomod\examples\companion_radio\ui-touch\UITask.cpp:304` `cfg.use_apll = false;`

### dma_buffer (2 matches)
- `meshcomod\examples\companion_radio\ui-touch\UITask.cpp:302` `cfg.dma_buf_count = 4;`

### encryption (87 matches)
- `meshcomod\src\Mesh.cpp:465` `len += Utils::encryptThenMAC(secret, &packet->payload[len], data, data_len);`
- `meshcomod\src\Utils.cpp:2` `#include <AES.h>`

### ethernet (1 matches)
- `meshcomod\src\helpers\bridges\ESPNowBridge.cpp:54` `memset(peerInfo.peer_addr, 0xFF, ESP_NOW_ETH_ALEN); // Broadcast address`

### flow_control (37 matches)
- `meshcomod\src\helpers\esp32\MultiTransportCompanionInterface.cpp:6` `: _tcp_port(0), _ws_port(0), _tcp_started(false), _ws_started(false), _tcp_enabled(true), _isEnabled`
- `meshcomod\src\helpers\esp32\WebSocketCompanionServer.cpp:96` `void WebSocketCompanionServer::pauseListen() {`
- `meshcomod\examples\repeater_tcp\main.cpp:56` `static bool s_rep_ota_ws_listen_paused = false;`

### i2s_driver (2 matches)
- `meshcomod\examples\companion_radio\ui-touch\UITask.cpp:306` `if (i2s_driver_install(kI2sPort, &cfg, 0, nullptr) != ESP_OK) return false;`

### i2s_playback (2 matches)
- `meshcomod\examples\companion_radio\ui-touch\UITask.cpp:337` `i2s_write(kI2sPort, buf, n * sizeof(int16_t), &bw, pdMS_TO_TICKS(200));`

### jitter_buffer (10 matches)
- `meshcomod\examples\companion_radio\ui-touch\UITask.cpp:1524` `// The old fixed-step jump on release was the source of "jittery / jumpy"`
- `meshcomod\include\lv_conf.h:40` `// children of a vertical-scroll view) would jitter past 10 px and turn into a`
- `meshcomod\lib\nrf52\include\nrf_soc.h:96` `#define NRF_RADIO_START_JITTER_US         (2)                 /**< The maximum jitter in @ref NRF_RA`
- `meshcomod\lib\nrf52\s140_nrf52_7.3.0_API\include\nrf_soc.h:96` `#define NRF_RADIO_START_JITTER_US         (2)                 /**< The maximum jitter in @ref NRF_RA`

### lora_radio (628 matches)
- `meshcomod\variants\ebyte_eora_s3\target.cpp:41` `int status = radio.begin(LORA_FREQ, LORA_BW, LORA_SF, LORA_CR, RADIOLIB_SX126X_SYNC_WORD_PRIVATE, LO`
- `meshcomod\variants\gat562_30s_mesh_kit\GAT56230SMeshKitBoard.cpp:56` `delay(10);   // give sx1262 some time to power up`
- `meshcomod\variants\gat562_mesh_evb_pro\GAT562EVBProBoard.cpp:51` `delay(10);   // give sx1268 some time to power up`
- `meshcomod\variants\gat562_mesh_tracker_pro\GAT562MeshTrackerProBoard.cpp:56` `delay(10);   // give sx1262 some time to power up`
- `meshcomod\variants\gat562_mesh_watch13\GAT56MeshWatch13Board.cpp:45` `delay(10);   // give sx1262 some time to power up`
- `meshcomod\variants\heltec_t114\T114Board.cpp:58` `delay(10); // give sx1262 some time to power up`
- `meshcomod\variants\ikoka_handheld_nrf\IkokaNrf52Board.cpp:37` `delay(10); // give sx1262 some time to power up`
- `meshcomod\variants\ikoka_nano_nrf\IkokaNanoNRFBoard.cpp:32` `delay(10);   // give sx1262 some time to power up`
- `meshcomod\variants\ikoka_stick_nrf\IkokaStickNRFBoard.cpp:32` `delay(10);   // give sx1262 some time to power up`

### memory_placement (20 matches)
- `meshcomod\src\helpers\input\TDeckTrackball.cpp:27` `static void IRAM_ATTR isrUp()    { ++s_cnt_up; }`
- `meshcomod\examples\companion_radio\ui-touch\UITask.cpp:4611` `const size_t i_tot  = heap_caps_get_total_size(MALLOC_CAP_INTERNAL | MALLOC_CAP_8BIT);`

### psram_usage (146 matches)
- `meshcomod\src\LvglPsramAlloc.cpp:1` `#include "LvglPsramAlloc.h"`

### routing (154 matches)
- `meshcomod\src\Mesh.cpp:122` `action = routeRecvPacket(pkt);`

### sample_rate_config (2 matches)
- `meshcomod\src\helpers\sensors\EnvironmentSensorManager.cpp:518` `bsec_iaq.updateSubscription(outputs, 6, BSEC_SAMPLE_RATE_LP);`
- `meshcomod\examples\companion_radio\ui-touch\UITask.cpp:297` `cfg.sample_rate = kI2sSampleRate;`

### sync_word (184 matches)
- `meshcomod\examples\companion_radio\ui-touch\extras_font_12.c:89` `0x2b, 0xb4, 0x0, 0x4, 0x70, 0x33, 0x49, 0x0,`

### synchronization (5 matches)
- `meshcomod\arch\stm32\Adafruit_LittleFS_stm32\src\Adafruit_LittleFS.cpp:51` `// _mutex = xSemaphoreCreateMutexStatic(&this->_MutexStorageSpace);`
- `meshcomod\src\helpers\ESP32Board.h:18` `static inline portMUX_TYPE sleepMux = portMUX_INITIALIZER_UNLOCKED;`
- `meshcomod\arch\stm32\Adafruit_LittleFS_stm32\src\Adafruit_LittleFS.h:79` `void   _lockFS  (void) { }//xSemaphoreTake(_mutex,  portMAX_DELAY); }`

### task_pinning (26 matches)
- `meshcomod\src\helpers\input\HeltecV4CapTouch.cpp:357` `// Pinned to core 0 because Arduino's loop() — which runs LVGL and the mesh`
- `meshcomod\src\helpers\input\TDeckKeyboard.cpp:20` `// poll (core 0). The keyboard's C3 firmware sets the backlight on an I2C write.`
- `meshcomod\src\helpers\input\TDeckTouch.cpp:342` `// Background poll on core 0 so the GT911 I2C round-trips never stall the LVGL`
- `meshcomod\examples\companion_radio\MyMesh.cpp:93` `#define STATS_TYPE_CORE               0`
- `meshcomod\examples\companion_radio\ui-touch\UITask.cpp:3976` `if (s_wdt_heavy_depth++ == 0) { disableCore0WDT(); disableCore1WDT(); }`

### task_priority (43 matches)
- `meshcomod\src\Dispatcher.cpp:273` `uint8_t priority = (action >> 24) - 1;`
- `meshcomod\src\Mesh.cpp:63` `return ACTION_RETRANSMIT_DELAYED(5, d);  // schedule with priority 5 (for now), maybe make configura`
- `meshcomod\src\helpers\NRF52Board.cpp:33` `// Priority 101 ensures this runs before SystemInit (102) and before`
- `meshcomod\src\helpers\StaticPoolPacketManager.cpp:60` `bool PacketQueue::add(mesh::Packet* packet, uint8_t priority, uint32_t scheduled_for) {`
- `meshcomod\src\helpers\esp32\SerialBLEInterface.cpp:185` `auto isLowPriority = [](const uint8_t* data, size_t sz) -> bool {`
- `meshcomod\examples\companion_radio\MyMesh.cpp:3699` `uint8_t priority = cmd_frame[1];`
- `meshcomod\src\Dispatcher.h:90` `virtual void queueOutbound(Packet* packet, uint8_t priority, uint32_t scheduled_for) = 0;`

### timestamp (670 matches)
- `meshcomod\src\Dispatcher.cpp:15` `#define MAX_RX_DELAY_MILLIS        32000  // 32 seconds`

### transport_queue (33 matches)
- `meshcomod\src\helpers\StaticPoolPacketManager.cpp:71` `StaticPoolPacketManager::StaticPoolPacketManager(int pool_size): unused(pool_size), send_queue(pool_`
- `meshcomod\examples\simple_repeater\MyMesh.cpp:232` `stats.curr_tx_queue_len = _mgr->getOutboundTotal();`
- `meshcomod\examples\simple_room_server\MyMesh.cpp:33` `uint16_t curr_tx_queue_len;`
- `meshcomod\examples\companion_radio\ui-touch\UITask.cpp:12049` `s_tile_fetch_queue = xQueueCreate(k_tile_fetch_queue_size, sizeof(TileFetchReq));`
- `meshcomod\src\helpers\StaticPoolPacketManager.h:22` `PacketQueue unused, send_queue, rx_queue;`
- `meshcomod\lib\nrf52\include\ble_gattc.h:118` `#define BLE_GATTC_WRITE_CMD_TX_QUEUE_SIZE_DEFAULT  1 /**< Default number of Write without Response t`

### watchdog (21 matches)
- `meshcomod\src\helpers\NRF52Board.cpp:71` `if (reason & POWER_RESETREAS_DOG_Msk) return "Watchdog";`
- `meshcomod\src\helpers\nrf52\SerialBLEInterface.cpp:8` `#define BLE_HEALTH_CHECK_INTERVAL  10000  // Advertising watchdog check every 10 seconds`
- `meshcomod\examples\companion_radio\ui-touch\UITask.cpp:3966` `// Heavy-flash-write watchdog guard (ref-counted, nesting-safe). A large or`

### websocket (66 matches)
- `meshcomod\src\helpers\CommonCLI.cpp:256` `strcpy(reply, "ERR: HTTP OTA must be started from Wi-Fi TCP or WebSocket session (not USB serial)");`
- `meshcomod\src\helpers\esp32\MultiTransportCompanionInterface.cpp:31` `// Plain WebSocket: start only when Wi-Fi has an address (caller defers TCP/WS start after splash).`