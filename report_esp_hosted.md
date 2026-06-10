# Rapport d'Analyse: ESP-Hosted (P4<->C6 Bridge)
**Projet:** `esp_hosted`

## Statistiques
- Fichiers scannes: 166
- Fichiers avec matches: 96
- Lignes totales: 56619
- Matches total: 1251

## Distribution par Categorie
- **transport**: 910 ??????????????????????????????????????????????????
- **network**: 134 ??????????????????????????????????????????????????
- **rtos**: 125 ??????????????????????????????????????????????????
- **memory**: 48 ????????????????????????????????????????????????
- **timing**: 14 ??????????????
- **mesh**: 12 ????????????
- **audio**: 8 ????????

## ??  Findings Critiques (CRITICAL)
- `esp-hosted\esp_hosted_fg\common\utils\esp_hosted_cli.c:93` [memory_placement] `heap_caps_get_largest_free_block(MALLOC_CAP_8BIT | MALLOC_CAP_INTERNAL),`
- `esp-hosted\esp_hosted_fg\common\utils\esp_hosted_cli.c:96` [memory_placement] `heap_caps_get_minimum_free_size(MALLOC_CAP_8BIT | MALLOC_CAP_INTERNAL),`
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\esp_hosted_coprocessor.c:319` [hosted_init] `if (if_context && if_context->if_ops && if_context->if_ops->write) {`
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\esp_hosted_coprocessor.c:330` [hosted_init] `if_context->if_ops->write(if_handle, buf_handle);`
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\esp_hosted_coprocessor.c:509` [hosted_init] `if (if_context && if_context->if_ops && if_context->if_ops->read) {`
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\esp_hosted_coprocessor.c:510` [hosted_init] `int len = if_context->if_ops->read(if_handle, &buf_handle);`
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\esp_hosted_coprocessor.c:987` [hosted_init] `if_context = interface_insert_driver(event_handler);`
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\esp_hosted_coprocessor.c:995` [hosted_init] `if (!if_context || !if_context->if_ops) {`
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\esp_hosted_coprocessor.c:1000` [hosted_init] `if_handle = if_context->if_ops->init();`
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\esp_hosted_coprocessor.c:632` [memory_placement] `static void IRAM_ATTR gpio_resetpin_isr_handler(void* arg)`
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\example_mqtt_client.c:255` [flow_control] `esp_err_t example_mqtt_pause(void)`
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\sdio_slave_api.c:103` [hosted_init] `if_ops_t if_ops = {`
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\sdio_slave_api.c:137` [hosted_init] `interface_context_t *interface_insert_driver(int (*event_handler)(uint8_t val))`
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\sdio_slave_api.c:143` [hosted_init] `context.if_ops = &if_ops;`
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\sdio_slave_api.c:24` [sdio_bridge] `#include "sdio_slave_api.h"`
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\sdio_slave_api.c:25` [sdio_bridge] `#include "driver/sdio_slave.h"`
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\sdio_slave_api.c:26` [sdio_bridge] `#include "soc/sdio_slave_periph.h"`
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\sdio_slave_api.c:33` [sdio_bridge] `#define SIMPLIFIED_SDIO_SLAVE            1`
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\sdio_slave_api.c:37` [sdio_bridge] `static uint8_t sdio_slave_rx_buffer[SDIO_RX_BUFFER_NUM][SDIO_RX_BUFFER_SIZE];`
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\sdio_slave_api.c:43` [sdio_bridge] `static const char *TAG = "SDIO_SLAVE";`
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\sdio_slave_api.c:45` [sdio_bridge] `#if !SIMPLIFIED_SDIO_SLAVE`
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\sdio_slave_api.c:71` [sdio_bridge] `#if !SIMPLIFIED_SDIO_SLAVE`
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\sdio_slave_api.c:82` [sdio_bridge] `#define SDIO_SLAVE_TIMING SDIO_SLAVE_TIMING_PSEND_PSAMPLE`
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\sdio_slave_api.c:84` [sdio_bridge] `#define SDIO_SLAVE_TIMING SDIO_SLAVE_TIMING_NSEND_PSAMPLE`
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\sdio_slave_api.c:86` [sdio_bridge] `#define SDIO_SLAVE_TIMING SDIO_SLAVE_TIMING_PSEND_NSAMPLE`
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\sdio_slave_api.c:88` [sdio_bridge] `#define SDIO_SLAVE_TIMING SDIO_SLAVE_TIMING_NSEND_NSAMPLE`
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\sdio_slave_api.c:93` [sdio_bridge] `static interface_handle_t * sdio_init(void);`
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\sdio_slave_api.c:94` [sdio_bridge] `static int32_t sdio_write(interface_handle_t *handle, interface_buffer_handle_t *buf_handle);`
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\sdio_slave_api.c:95` [sdio_bridge] `static int sdio_read(interface_handle_t *if_handle, interface_buffer_handle_t *buf_handle);`
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\sdio_slave_api.c:98` [sdio_bridge] `#if !SIMPLIFIED_SDIO_SLAVE`

## Detail par Sous-systeme

### encryption (12 matches)
- `esp-hosted\esp_hosted_ng\host\esp_cfg80211.c:174` `WLAN_CIPHER_SUITE_CCMP,`
- `esp-hosted\esp_hosted_ng\host\esp_utils.c:15` `case WLAN_CIPHER_SUITE_CCMP:`
- `esp-hosted\esp_hosted_ng\esp\esp_driver\lib\esp_wifi_driver.h:26` `WIFI_WPA_ALG_CCMP   = 3,`
- `esp-hosted\esp_hosted_ng\esp\esp_driver\network_adapter\main\esp_wifi_driver.h:26` `WIFI_WPA_ALG_CCMP   = 3,`
- `esp-hosted\esp_hosted_ng\host\include\esp_utils.h:17` `#define WPA_CIPHER_CCMP                 BIT(3)`

### ethernet (46 matches)
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\esp_hosted_coprocessor.c:77` `#define ETH_DATA_LEN                     1500`
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\nw_split_router.c:351` `struct eth_hdr *ethhdr = (struct eth_hdr *)frame_data;`
- `esp-hosted\esp_hosted_fg\host\linux\host_driver\esp32\esp_serial.c:122` `if (left_len > ETH_DATA_LEN) {`
- `esp-hosted\esp_hosted_fg\host\linux\host_driver\esp32\main.c:144` `.ndo_validate_addr = eth_validate_addr,`

### flow_control (72 matches)
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\example_mqtt_client.c:255` `esp_err_t example_mqtt_pause(void)`
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\slave_control.c:275` `example_mqtt_pause();`
- `esp-hosted\esp_hosted_fg\host\linux\host_control\c_support\hosted_shell.c:1214` `//sleep(1);  // Brief pause (removed for faster exit)`
- `esp-hosted\esp_hosted_fg\host\linux\host_driver\esp32\esp_stats.c:73` `if (esp_is_tx_queue_paused()) {`
- `esp-hosted\esp_hosted_fg\host\linux\host_driver\esp32\main.c:651` `int esp_is_tx_queue_paused(void)`
- `esp-hosted\esp_hosted_fg\host\linux\host_driver\esp32\sdio\esp_sdio.c:40` `#define TX_RESUME_THRESHOLD     (TX_MAX_PENDING_COUNT/5)`

### hosted_init (66 matches)
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\esp_hosted_coprocessor.c:319` `if (if_context && if_context->if_ops && if_context->if_ops->write) {`
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\sdio_slave_api.c:103` `if_ops_t if_ops = {`

### memory_placement (38 matches)
- `esp-hosted\esp_hosted_fg\common\utils\esp_hosted_cli.c:93` `heap_caps_get_largest_free_block(MALLOC_CAP_8BIT | MALLOC_CAP_INTERNAL),`
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\esp_hosted_coprocessor.c:632` `static void IRAM_ATTR gpio_resetpin_isr_handler(void* arg)`
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\sdio_slave_api.c:155` `IRAM_ATTR static void event_cb(uint8_t val)`
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\slave_bt.c:196` `static IRAM_ATTR void hci_uart_tl_recv_async(uint8_t *buf, uint32_t size,`
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\spi_slave_api.c:155` `static DRAM_ATTR uint8_t dummy_buffer[SPI_BUFFER_SIZE] __attribute__((aligned(4)));`

### mqtt (80 matches)
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\example_mqtt_client.c:1` `/* MQTT (over TCP) Example`

### psram_usage (10 matches)
- `esp-hosted\esp_hosted_fg\common\utils\esp_hosted_cli.c:88` `printf("\tDescription\tInternal\tSPIRAM\n");`
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\stats.c:189` `printf("\tDescription\tInternal\tSPIRAM\n");`

### ring_buffer (8 matches)
- `esp-hosted\esp_hosted_fg\host\linux\host_driver\esp32\esp_rb.c:39` `int esp_rb_read_by_user(esp_rb_t *rb, const char __user *buf, size_t sz, int block)`
- `esp-hosted\esp_hosted_fg\host\linux\host_driver\esp32\esp_serial.c:68` `ret_size = esp_rb_read_by_user(&dev->rb, user_buffer, size, !(file->f_flags & O_NONBLOCK));`
- `esp-hosted\esp_hosted_fg\host\linux\port\src\platform_wrapper.c:150` `perror("Failed to read ringbuffer:\n");`
- `esp-hosted\esp_hosted_fg\host\linux\host_driver\esp32\esp_rb.h:21` `int esp_rb_read_by_user(esp_rb_t *rb, const char __user *buf, size_t sz, int block);`

### sdio_bridge (253 matches)
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\sdio_slave_api.c:24` `#include "sdio_slave_api.h"`

### spi_bridge (116 matches)
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\esp_hosted_coprocessor.c:113` `#if CONFIG_ESP_SPI_HOST_INTERFACE`
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\slave_bt.c:593` `#if CONFIG_ESP_SPI_HOST_INTERFACE`
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\spi_slave_api.c:26` `#include "driver/spi_slave.h"`

### synchronization (109 matches)
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\esp_hosted_coprocessor.c:92` `SemaphoreHandle_t host_reset_sem;`
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\host_power_save.c:21` `SemaphoreHandle_t wakeup_sem;`

### task_pinning (4 matches)
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\stats.c:158` `uint32_t percentage_time = (task_elapsed_time * 100UL) / (total_elapsed_time * portNUM_PROCESSORS);`
- `esp-hosted\esp_hosted_ng\esp\esp_driver\network_adapter\main\sdio_slave_api.c:360` `/* core0 sufficient now */`
- `esp-hosted\esp_hosted_ng\esp\esp_driver\network_adapter\main\spi_slave_api.c:303` `/* core0 sufficient now */`
- `esp-hosted\esp_hosted_ng\esp\esp_driver\network_adapter\main\stats.c:94` `uint32_t percentage_time = (task_elapsed_time * 100UL) / (total_elapsed_time * portNUM_PROCESSORS);`

### task_priority (12 matches)
- `esp-hosted\esp_hosted_fg\host\stm32\app\app_main.c:167` `osThreadDef(Arping_Thread, arping_task, osPriorityAboveNormal, 0,`
- `esp-hosted\esp_hosted_fg\host\stm32\common\stats.c:104` `osPriorityAboveNormal, 0, RAW_TP_TX_TASK_STACK_SIZE);`
- `esp-hosted\esp_hosted_fg\host\stm32\app\control\control.c:169` `osThreadDef(SEM_Thread, control_path_task, osPriorityAboveNormal, 0,`
- `esp-hosted\esp_hosted_fg\host\stm32\driver\transport\sdio\sdio_drv.c:607` `osPriorityAboveNormal, 0, RX_TASK_STACK_SIZE);`
- `esp-hosted\esp_hosted_fg\host\stm32\driver\transport\sdio\sdio_ll.c:377` `HAL_NVIC_SetPriority(SDIO_IRQn, 5, 0);`
- `esp-hosted\esp_hosted_fg\host\stm32\driver\transport\spi\spi_drv.c:268` `osPriorityAboveNormal, 0, TRANSACTION_TASK_STACK_SIZE);`
- `esp-hosted\esp_hosted_fg\common\include\adapter.h:18` `#define MAX_PRIORITY_QUEUES                       3`

### timestamp (14 matches)
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\esp_hosted_coprocessor.c:642` `uint32_t currtime_us = esp_timer_get_time();`
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\host_power_save.c:162` `#define GET_CURR_TIME_IN_MS() esp_timer_get_time()/1000`
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\nw_split_router.c:279` `uint64_t current_time = esp_timer_get_time() >> 10; /* Approx ms */`
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\slave_control.c:2411` `int64_t current_time = esp_timer_get_time() / 1000; /* Convert to ms */`
- `esp-hosted\esp_hosted_fg\host\stm32\port\src\platform_wrapper.c:22` `#define MILLISEC_TO_SEC			1000`

### transport_queue (220 matches)
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\esp_hosted_coprocessor.c:75` `#define TO_HOST_QUEUE_SIZE               10`
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\protocomm_pserial.c:330` `pserial_cfg->req_queue = xQueueCreate(REQ_Q_MAX, sizeof(serial_arg_t));`
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\sdio_slave_api.c:34` `#define SDIO_DRIVER_TX_QUEUE_SIZE        10`

### udp (8 matches)
- `esp-hosted\esp_hosted_fg\common\utils\esp_hosted_cli.c:234` `printf("%d\t%d:%s\t%16s:%d", i, sock_type, sock_type == SOCK_STREAM ? "tcp" : sock_type == SOCK_DGRA`
- `esp-hosted\esp_hosted_fg\host\linux\host_control\c_support\nw_helper_func.c:30` `ret = create_socket(AF_INET, SOCK_DGRAM, IPPROTO_IP, &sockfd);`

### wifi_power_save (183 matches)
- `esp-hosted\esp_hosted_fg\common\esp_hosted_config.pb-c.c:6502` `"req_set_power_save_mode",`