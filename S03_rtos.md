# Script 03: Extraction RTOS (Tasks)


## esp-adf (15 tasks)

| Task | Function | Stack | Priority/Param |
|---|---|---|---|
| uart_wakeup_task | `uart_wakeup_task` | 4096 | NULL |
| gpio_task_example | `gpio_task_example` | 4096 | NULL |
| opt_task | `opt_task` | 3072 | (void * |
| RawReadTask | `raw_read_task` | 3072 | (void * |
| RawWriteTask | `raw_write_task` | 3072 | (void * |
| RawReadTask | `raw_read_save` | 3072 | (void * |
| player_task | `esp_audio_state_task` | 4096 | cfg.evt_que |
| player_task | `esp_audio_state_task` | 4096 | cfg.evt_que |
| audio_play_read_task | `audio_play_read_task` | 4096 | NULL |
| task_recv1 | `task_recv1` | 2048 | broadcast |
| task_recv2 | `task_recv2` | 2048 | broadcast |
| task_recv3 | `task_recv3` | 2048 | broadcast |
| task_recv4 | `task_recv4` | 2048 | broadcast |
| task_recv0 | `task_recv0` | 2048 | broadcast |
| i2s_volume_alc_task | `i2s_volume_alc_task` | 4096 | (void * |

## esp-hosted (0 tasks)

| Task | Function | Stack | Priority/Param |
|---|---|---|---|

## xiaozhi (0 tasks)

| Task | Function | Stack | Priority/Param |
|---|---|---|---|

## ha_voice (17 tasks)

| Task | Function | Stack | Priority/Param |
|---|---|---|---|
| alarm_check | `alarm_check_task` | 2048 | NULL |
| ha_reconnect | `ha_reconnect_task` | 6144 | reason_copy |
| led_effect | `led_effect_task` | 4096 | NULL |
| led_test | `led_test_task` | 2048 | NULL |
| music_ctl | `music_control_task` | 4096 | (void * |
| music_ctl | `music_control_task` | 4096 | (void * |
| mqtt_metrics | `mqtt_metrics_task` | 4096 | NULL |
| net_post | `post_connect_task` | 4096 | (void * |
| led_ready | `led_ready_task` | 2048 | NULL |
| mqtt_setup | `mqtt_setup_task` | 4096 | NULL |
| wifi_fallback | `wifi_fallback_task` | 4096 | (void * |
| oled_task | `oled_task` | 4096 | NULL |
| diag_worker | `diag_worker_task` | 4096 | NULL |
| timer_tick | `timer_tick_task` | 3072 | NULL |
| tts_playback | `playback_task` | 8192 | NULL |
| restart | `restart_task` | 2048 | NULL |
| usb_lib | `usb_lib_task` | 4096 | NULL |

## meshcore (11 tasks)

| Task | Function | Stack | Priority/Param |
|---|---|---|---|
| uart_wakeup_task | `uart_wakeup_task` | 4096 | NULL |
| tinyusb_hid_task | `tinyusb_hid_task` | 4096 | NULL |
| app_touch_task | `app_touch_task` | 4096 | NULL |
| tusb_device_task | `tusb_device_task` | 4096 | NULL |
| transfer_task | `transfer_task` | 4096 | NULL |
| i2s_music | `i2s_music` | 4096 | NULL |
| i2s_echo | `i2s_echo` | 8192 | NULL |
| i2s_music | `i2s_music` | 4096 | NULL |
| i2s_echo | `i2s_echo` | 8192 | NULL |
| sdioRecvTask | `sdio_recv_task` | 2048 | NULL |
| deep_sleep_task | `deep_sleep_task` | 4096 | NULL |

## meshtastic (0 tasks)

| Task | Function | Stack | Priority/Param |
|---|---|---|---|

## jarvix (4 tasks)

| Task | Function | Stack | Priority/Param |
|---|---|---|---|
| Radio | `lora_radio_task` | 8192 | NULL |
| Agent | `lua_agent_task` | 32768 | NULL |
| voice_pipeline | `pipeline_task` | 8192 | NULL |
| scanner | `scanner_task` | 8192 | NULL |

## OpenMQTTGateway (3 tasks)

| Task | Function | Stack | Priority/Param |
|---|---|---|---|
| overLimitTemp | `overLimitTemp` | 4000 | NULL |
| ReceivingCmdTask | `receivingCommandTask` | 10000 | taskData |
| updateAndHandleLEDsTask | `updateAndHandleLEDsTask` | 2500 | NULL |

## LoRaMon (0 tasks)

| Task | Function | Stack | Priority/Param |
|---|---|---|---|

## meshtastic-sniffer (0 tasks)

| Task | Function | Stack | Priority/Param |
|---|---|---|---|

## lorawan-sniffer (0 tasks)

| Task | Function | Stack | Priority/Param |
|---|---|---|---|

## RadioLib (0 tasks)

| Task | Function | Stack | Priority/Param |
|---|---|---|---|

## Meck-P4 (11 tasks)

| Task | Function | Stack | Priority/Param |
|---|---|---|---|
| uart_wakeup_task | `uart_wakeup_task` | 4096 | NULL |
| tinyusb_hid_task | `tinyusb_hid_task` | 4096 | NULL |
| app_touch_task | `app_touch_task` | 4096 | NULL |
| tusb_device_task | `tusb_device_task` | 4096 | NULL |
| transfer_task | `transfer_task` | 4096 | NULL |
| i2s_music | `i2s_music` | 4096 | NULL |
| i2s_echo | `i2s_echo` | 8192 | NULL |
| i2s_music | `i2s_music` | 4096 | NULL |
| i2s_echo | `i2s_echo` | 8192 | NULL |
| sdioRecvTask | `sdio_recv_task` | 2048 | NULL |
| deep_sleep_task | `deep_sleep_task` | 4096 | NULL |

## T-Display-P4 (11 tasks)

| Task | Function | Stack | Priority/Param |
|---|---|---|---|
| uart_wakeup_task | `uart_wakeup_task` | 4096 | NULL |
| tinyusb_hid_task | `tinyusb_hid_task` | 4096 | NULL |
| app_touch_task | `app_touch_task` | 4096 | NULL |
| tusb_device_task | `tusb_device_task` | 4096 | NULL |
| transfer_task | `transfer_task` | 4096 | NULL |
| i2s_music | `i2s_music` | 4096 | NULL |
| i2s_echo | `i2s_echo` | 8192 | NULL |
| i2s_music | `i2s_music` | 4096 | NULL |
| i2s_echo | `i2s_echo` | 8192 | NULL |
| sdioRecvTask | `sdio_recv_task` | 2048 | NULL |
| deep_sleep_task | `deep_sleep_task` | 4096 | NULL |

## SigurdOS (0 tasks)

| Task | Function | Stack | Priority/Param |
|---|---|---|---|

## Meck-P4-v2 (11 tasks)

| Task | Function | Stack | Priority/Param |
|---|---|---|---|
| uart_wakeup_task | `uart_wakeup_task` | 4096 | NULL |
| tinyusb_hid_task | `tinyusb_hid_task` | 4096 | NULL |
| app_touch_task | `app_touch_task` | 4096 | NULL |
| tusb_device_task | `tusb_device_task` | 4096 | NULL |
| transfer_task | `transfer_task` | 4096 | NULL |
| i2s_music | `i2s_music` | 4096 | NULL |
| i2s_echo | `i2s_echo` | 8192 | NULL |
| i2s_music | `i2s_music` | 4096 | NULL |
| i2s_echo | `i2s_echo` | 8192 | NULL |
| sdioRecvTask | `sdio_recv_task` | 2048 | NULL |
| deep_sleep_task | `deep_sleep_task` | 4096 | NULL |

## MeshCore-official (0 tasks)

| Task | Function | Stack | Priority/Param |
|---|---|---|---|

## meshtastic-firmware (0 tasks)

| Task | Function | Stack | Priority/Param |
|---|---|---|---|

## trail-mate (4 tasks)

| Task | Function | Stack | Priority/Param |
|---|---|---|---|
| usb_lib | `usb_lib_task` | 4096 | NULL |
| idf_gps | `worker_task` | 6144 | nullptr |
| screen_sleep | `screen_sleep_task` | 4096 | nullptr |
| tab5_heading | `task_main` | 6144 | nullptr |