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
- `esp-hosted\esp_hosted_ng\host\esp_cmd.c:482` [hosted_init] `if (adapter->if_ops && adapter->if_ops->write)`
- `esp-hosted\esp_hosted_ng\host\esp_stats.c:73` [hosted_init] `esp_info("%u adapter->if_ops->alloc_skb failed\n", __LINE__);`
- `esp-hosted\esp_hosted_ng\host\esp_stats.c:95` [hosted_init] `if (!adapter->if_ops || !adapter->if_ops->write) {`
- `esp-hosted\esp_hosted_ng\host\esp_stats.c:69` [flow_control] `if (esp_is_tx_queue_paused(priv)) {`
- `esp-hosted\esp_hosted_ng\host\main.c:175` [hosted_init] `if (!priv->adapter->if_ops ||`
- `esp-hosted\esp_hosted_ng\host\main.c:176` [hosted_init] `!priv->adapter->if_ops->write) {`
- `esp-hosted\esp_hosted_ng\host\main.c:959` [hosted_init] `if (!adapter || !adapter->if_ops || !adapter->if_ops->read)`
- `esp-hosted\esp_hosted_ng\host\main.c:962` [hosted_init] `while ((skb = adapter->if_ops->read(adapter)))`
- `esp-hosted\esp_hosted_ng\host\main.c:970` [hosted_init] `if (!adapter || !adapter->if_ops || !adapter->if_ops->write) {`
- `esp-hosted\esp_hosted_ng\host\main.c:975` [hosted_init] `return adapter->if_ops->write(adapter, skb);`
- `esp-hosted\esp_hosted_ng\host\main.c:924` [flow_control] `int esp_is_tx_queue_paused(struct esp_wifi_device *priv)`
- `esp-hosted\esp_hosted_ng\host\main.c:935` [flow_control] `void esp_tx_pause(struct esp_wifi_device *priv)`
- `esp-hosted\esp_hosted_ng\host\main.c:945` [flow_control] `void esp_tx_resume(struct esp_wifi_device *priv)`
- `esp-hosted\esp_hosted_ng\host\sdio\esp_sdio.c:304` [hosted_init] `static struct esp_if_ops if_ops = {`
- `esp-hosted\esp_hosted_ng\host\sdio\esp_sdio.c:908` [hosted_init] `adapter->if_ops = &if_ops;`
- `esp-hosted\esp_hosted_ng\host\sdio\esp_sdio.c:544` [sdio_bridge] `static int is_sdio_write_buffer_available(u32 buf_needed)`
- `esp-hosted\esp_hosted_ng\host\sdio\esp_sdio.c:659` [sdio_bridge] `ret = is_sdio_write_buffer_available(buf_needed);`
- `esp-hosted\esp_hosted_ng\host\sdio\esp_sdio.c:27` [flow_control] `#define TX_MAX_PENDING_COUNT    200`
- `esp-hosted\esp_hosted_ng\host\sdio\esp_sdio.c:28` [flow_control] `#define TX_RESUME_THRESHOLD     (TX_MAX_PENDING_COUNT/5)`
- `esp-hosted\esp_hosted_ng\host\sdio\esp_sdio.c:36` [flow_control] `static atomic_t tx_pending;`
- `esp-hosted\esp_hosted_ng\host\sdio\esp_sdio.c:257` [flow_control] `atomic_set(&tx_pending, 0);`
- `esp-hosted\esp_hosted_ng\host\sdio\esp_sdio.c:519` [flow_control] `if (cb && cb->priv && (atomic_read(&tx_pending) >= TX_MAX_PENDING_COUNT)) {`
- `esp-hosted\esp_hosted_ng\host\sdio\esp_sdio.c:520` [flow_control] `esp_tx_pause(cb->priv);`
- `esp-hosted\esp_hosted_ng\host\sdio\esp_sdio.c:523` [flow_control] `/*		esp_err("TX Pause busy");*/`
- `esp-hosted\esp_hosted_ng\host\sdio\esp_sdio.c:528` [flow_control] `atomic_inc(&tx_pending);`
- `esp-hosted\esp_hosted_ng\host\sdio\esp_sdio.c:639` [flow_control] `if (atomic_read(&tx_pending))`
- `esp-hosted\esp_hosted_ng\host\sdio\esp_sdio.c:640` [flow_control] `atomic_dec(&tx_pending);`
- `esp-hosted\esp_hosted_ng\host\sdio\esp_sdio.c:646` [flow_control] `if (cb && cb->priv && atomic_read(&tx_pending) < TX_RESUME_THRESHOLD) {`
- `esp-hosted\esp_hosted_ng\host\sdio\esp_sdio.c:647` [flow_control] `esp_tx_resume(cb->priv);`
- `esp-hosted\esp_hosted_ng\host\sdio\esp_sdio.c:764` [flow_control] `atomic_set(&tx_pending, 0);`

## Detail par Sous-systeme

### encryption (12 matches)
- `esp-hosted\esp_hosted_ng\host\esp_cfg80211.c:174` `WLAN_CIPHER_SUITE_CCMP,`
- `esp-hosted\esp_hosted_ng\host\esp_utils.c:15` `case WLAN_CIPHER_SUITE_CCMP:`
- `esp-hosted\esp_hosted_ng\host\include\esp_utils.h:17` `#define WPA_CIPHER_CCMP                 BIT(3)`

### ethernet (46 matches)
- `esp-hosted\esp_hosted_ng\host\esp_cfg80211.c:334` `ETH_HW_ADDR_SET(ndev, esp_wdev->mac_address);`
- `esp-hosted\esp_hosted_ng\host\esp_cmd.c:751` `memcpy(mgmt->da, priv->mac_address, ETH_ALEN); /* own address */`
- `esp-hosted\esp_hosted_ng\host\main.c:445` `ETH_HW_ADDR_SET(ndev, priv->mac_address/*mac_addr->sa_data*/);`

### flow_control (72 matches)
- `esp-hosted\esp_hosted_ng\host\esp_stats.c:69` `if (esp_is_tx_queue_paused(priv)) {`
- `esp-hosted\esp_hosted_ng\host\main.c:924` `int esp_is_tx_queue_paused(struct esp_wifi_device *priv)`
- `esp-hosted\esp_hosted_ng\host\sdio\esp_sdio.c:27` `#define TX_MAX_PENDING_COUNT    200`

### hosted_init (66 matches)
- `esp-hosted\esp_hosted_ng\host\esp_cmd.c:482` `if (adapter->if_ops && adapter->if_ops->write)`
- `esp-hosted\esp_hosted_ng\host\esp_stats.c:73` `esp_info("%u adapter->if_ops->alloc_skb failed\n", __LINE__);`
- `esp-hosted\esp_hosted_ng\host\main.c:175` `if (!priv->adapter->if_ops ||`
- `esp-hosted\esp_hosted_ng\host\sdio\esp_sdio.c:304` `static struct esp_if_ops if_ops = {`

### memory_placement (38 matches)
- `esp-hosted\esp_hosted_ng\esp\esp_driver\network_adapter\main\cmd.c:124` `buf_handle.payload = heap_caps_malloc(buf_handle.payload_len, MALLOC_CAP_DMA);`
- `esp-hosted\esp_hosted_ng\esp\esp_driver\network_adapter\main\sdio_slave_api.c:82` `IRAM_ATTR static void event_cb(uint8_t val)`
- `esp-hosted\esp_hosted_ng\esp\esp_driver\network_adapter\main\slave_bt.c:171` `static IRAM_ATTR void hci_uart_tl_recv_async(uint8_t *buf, uint32_t size,`

### mqtt (80 matches)
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\example_mqtt_client.c:1` `/* MQTT (over TCP) Example`

### psram_usage (10 matches)
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\stats.c:189` `printf("\tDescription\tInternal\tSPIRAM\n");`
- `esp-hosted\esp_hosted_fg\common\utils\esp_hosted_cli.c:88` `printf("\tDescription\tInternal\tSPIRAM\n");`

### ring_buffer (8 matches)
- `esp-hosted\esp_hosted_fg\host\linux\port\src\platform_wrapper.c:150` `perror("Failed to read ringbuffer:\n");`
- `esp-hosted\esp_hosted_fg\host\linux\host_driver\esp32\esp_rb.c:39` `int esp_rb_read_by_user(esp_rb_t *rb, const char __user *buf, size_t sz, int block)`
- `esp-hosted\esp_hosted_fg\host\linux\host_driver\esp32\esp_serial.c:68` `ret_size = esp_rb_read_by_user(&dev->rb, user_buffer, size, !(file->f_flags & O_NONBLOCK));`
- `esp-hosted\esp_hosted_fg\host\linux\host_driver\esp32\esp_rb.h:21` `int esp_rb_read_by_user(esp_rb_t *rb, const char __user *buf, size_t sz, int block);`

### sdio_bridge (253 matches)
- `esp-hosted\esp_hosted_ng\host\sdio\esp_sdio.c:544` `static int is_sdio_write_buffer_available(u32 buf_needed)`
- `esp-hosted\esp_hosted_ng\host\sdio\esp_sdio_api.c:31` `*data = sdio_readb(func, reg, &ret);`
- `esp-hosted\esp_hosted_ng\esp\esp_driver\network_adapter\main\app_main.c:100` `#if CONFIG_ESP_SDIO_HOST_INTERFACE`
- `esp-hosted\esp_hosted_ng\esp\esp_driver\network_adapter\main\cmd.c:234` `#if CONFIG_ESP_SDIO_HOST_INTERFACE`
- `esp-hosted\esp_hosted_ng\esp\esp_driver\network_adapter\main\sdio_slave_api.c:27` `#include "sdio_slave_api.h"`

### spi_bridge (116 matches)
- `esp-hosted\esp_hosted_ng\host\spi\esp_spi.c:289` `struct spi_transfer trans;`
- `esp-hosted\esp_hosted_ng\esp\esp_driver\network_adapter\main\app_main.c:86` `#if CONFIG_ESP_SPI_HOST_INTERFACE`
- `esp-hosted\esp_hosted_ng\esp\esp_driver\network_adapter\main\slave_bt.c:449` `#if CONFIG_ESP_SPI_HOST_INTERFACE`
- `esp-hosted\esp_hosted_ng\esp\esp_driver\network_adapter\main\spi_slave_api.c:25` `#include "driver/spi_slave.h"`

### synchronization (109 matches)
- `esp-hosted\esp_hosted_ng\esp\esp_driver\network_adapter\main\app_main.c:70` `SemaphoreHandle_t wakeup_sem;`
- `esp-hosted\esp_hosted_ng\esp\esp_driver\network_adapter\main\sdio_slave_api.c:54` `extern SemaphoreHandle_t wakeup_sem;`

### task_pinning (4 matches)
- `esp-hosted\esp_hosted_ng\esp\esp_driver\network_adapter\main\sdio_slave_api.c:360` `/* core0 sufficient now */`
- `esp-hosted\esp_hosted_ng\esp\esp_driver\network_adapter\main\spi_slave_api.c:303` `/* core0 sufficient now */`
- `esp-hosted\esp_hosted_ng\esp\esp_driver\network_adapter\main\stats.c:94` `uint32_t percentage_time = (task_elapsed_time * 100UL) / (total_elapsed_time * portNUM_PROCESSORS);`
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\stats.c:158` `uint32_t percentage_time = (task_elapsed_time * 100UL) / (total_elapsed_time * portNUM_PROCESSORS);`

### task_priority (12 matches)
- `esp-hosted\esp_hosted_fg\host\stm32\app\app_main.c:167` `osThreadDef(Arping_Thread, arping_task, osPriorityAboveNormal, 0,`
- `esp-hosted\esp_hosted_fg\host\stm32\common\stats.c:104` `osPriorityAboveNormal, 0, RAW_TP_TX_TASK_STACK_SIZE);`
- `esp-hosted\esp_hosted_fg\host\stm32\driver\transport\sdio\sdio_drv.c:607` `osPriorityAboveNormal, 0, RX_TASK_STACK_SIZE);`
- `esp-hosted\esp_hosted_fg\host\stm32\driver\transport\sdio\sdio_ll.c:377` `HAL_NVIC_SetPriority(SDIO_IRQn, 5, 0);`
- `esp-hosted\esp_hosted_fg\host\stm32\driver\transport\spi\spi_drv.c:268` `osPriorityAboveNormal, 0, TRANSACTION_TASK_STACK_SIZE);`
- `esp-hosted\esp_hosted_fg\host\stm32\app\control\control.c:169` `osThreadDef(SEM_Thread, control_path_task, osPriorityAboveNormal, 0,`
- `esp-hosted\esp_hosted_ng\host\include\adapter.h:14` `#define MAX_PRIORITY_QUEUES             3`

### timestamp (14 matches)
- `esp-hosted\esp_hosted_fg\host\stm32\port\src\platform_wrapper.c:22` `#define MILLISEC_TO_SEC			1000`
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\esp_hosted_coprocessor.c:642` `uint32_t currtime_us = esp_timer_get_time();`
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\host_power_save.c:162` `#define GET_CURR_TIME_IN_MS() esp_timer_get_time()/1000`
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\nw_split_router.c:279` `uint64_t current_time = esp_timer_get_time() >> 10; /* Approx ms */`
- `esp-hosted\esp_hosted_fg\esp\esp_driver\network_adapter\main\slave_control.c:2411` `int64_t current_time = esp_timer_get_time() / 1000; /* Convert to ms */`

### transport_queue (220 matches)
- `esp-hosted\esp_hosted_ng\host\esp_stats.c:69` `if (esp_is_tx_queue_paused(priv)) {`
- `esp-hosted\esp_hosted_ng\host\main.c:866` `skb_queue_tail(&adapter->events_skb_q, skb);`
- `esp-hosted\esp_hosted_ng\host\sdio\esp_sdio.c:256` `skb_queue_purge(&(sdio_context.tx_q[prio_q_idx]));`

### udp (8 matches)
- `esp-hosted\esp_hosted_fg\host\linux\host_control\c_support\nw_helper_func.c:30` `ret = create_socket(AF_INET, SOCK_DGRAM, IPPROTO_IP, &sockfd);`
- `esp-hosted\esp_hosted_fg\common\utils\esp_hosted_cli.c:234` `printf("%d\t%d:%s\t%16s:%d", i, sock_type, sock_type == SOCK_STREAM ? "tcp" : sock_type == SOCK_DGRA`

### wifi_power_save (183 matches)
- `esp-hosted\esp_hosted_ng\host\sdio\esp_sdio.c:830` `generate_slave_intr(context, BIT(ESP_POWER_SAVE_ON));`
- `esp-hosted\esp_hosted_ng\esp\esp_driver\network_adapter\main\app_main.c:68` `volatile uint8_t power_save_on = 0;`
- `esp-hosted\esp_hosted_ng\esp\esp_driver\network_adapter\main\cmd.c:75` `extern volatile uint8_t power_save_on;`