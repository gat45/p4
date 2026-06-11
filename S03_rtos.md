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

## esp-sr (0 tasks)

| Task | Function | Stack | Priority/Param |
|---|---|---|---|

## esp-hosted (0 tasks)

| Task | Function | Stack | Priority/Param |
|---|---|---|---|

## xiaozhi (0 tasks)

| Task | Function | Stack | Priority/Param |
|---|---|---|---|

## xiaozhi-server (0 tasks)

| Task | Function | Stack | Priority/Param |
|---|---|---|---|

## esp32-aichats (0 tasks)

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

## ESP32_Voice_Assistant (0 tasks)

| Task | Function | Stack | Priority/Param |
|---|---|---|---|

## client-sdk-esp32 (0 tasks)

| Task | Function | Stack | Priority/Param |
|---|---|---|---|

## stream-video-esp32 (7 tasks)

| Task | Function | Stack | Priority/Param |
|---|---|---|---|
| stream_flow | `stream_flow_task` | 6144 | NULL |
| audio_mon | `audio_monitor_task` | 4096 | s_sink |
| sfu_health | `sfu_health_monitor_task` | 4096 | client |
| sfu_reconn | `sfu_reconnect_task` | 4096 | client |
| sfu_publish | `publish_task` | 8192 | client |
| signaling_reconnect | `reconnect_task` | 4096 | client |
| signaling_health | `health_monitor_task` | 4096 | client |

## ESP32-audioI2S (2 tasks)

| Task | Function | Stack | Priority/Param |
|---|---|---|---|
| wavWriter | `wavWriterTask` | 4096 | nullptr |
| samplerate_monitor | `samplerate_monitor_task` | 2048 | NULL |

## esp32_opus (0 tasks)

| Task | Function | Stack | Priority/Param |
|---|---|---|---|

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

## T-Connection-P4-Pro (1 tasks)

| Task | Function | Stack | Priority/Param |
|---|---|---|---|
| touch_int_handler | `touch_int_handler` | 2048 | NULL |

## ESP32-P4-Platform (11 tasks)

| Task | Function | Stack | Priority/Param |
|---|---|---|---|
| avi_play_task | `playTask` | 32768 | this |
| sampler | `sampler_task` | 3072 | NULL |
| printer | `printer_task` | 3072 | NULL |
| console | `console_task` | 4096 | NULL |
| usb_lib | `usb_lib_task` | 4096 | NULL |
| flow_ctl | `eth2wifi_flow_control_task` | 2048 | NULL |
| i2s_music | `i2s_music` | 4096 | NULL |
| i2s_echo | `i2s_echo` | 8192 | NULL |
| gpio_event_task | `gpio_event_task` | 3072 | NULL |
| producer | `producer_task` | 3072 | NULL |
| consumer | `consumer_task` | 3072 | NULL |

## CrowPanel-P4 (0 tasks)

| Task | Function | Stack | Priority/Param |
|---|---|---|---|

## esp32p4-c6-wifi-test (2 tasks)

| Task | Function | Stack | Priority/Param |
|---|---|---|---|
| udp_tx | `udp_stream_task` | 4096 | NULL |
| tcp_tx | `tcp_stream_task` | 4096 | NULL |

## SigurdOS (0 tasks)

| Task | Function | Stack | Priority/Param |
|---|---|---|---|

## meshtastic (0 tasks)

| Task | Function | Stack | Priority/Param |
|---|---|---|---|

## meshtastic-firmware (0 tasks)

| Task | Function | Stack | Priority/Param |
|---|---|---|---|

## jarvix (8 tasks)

| Task | Function | Stack | Priority/Param |
|---|---|---|---|
| i2s_cap | `capture_task` | 4096 | NULL |
| i2s_pb | `playback_task` | 4096 | NULL |
| i2s_met | `metrics_task` | 4096 | NULL |
| Radio | `lora_radio_task` | 8192 | NULL |
| Agent | `lua_agent_task` | 32768 | NULL |
| voice_pipeline | `pipeline_task` | 8192 | NULL |
| scanner | `scanner_task` | 8192 | NULL |
| sdio_wd | `watchdog_task` | 4096 | NULL |

## OpenMQTTGateway (3 tasks)

| Task | Function | Stack | Priority/Param |
|---|---|---|---|
| overLimitTemp | `overLimitTemp` | 4000 | NULL |
| ReceivingCmdTask | `receivingCommandTask` | 10000 | taskData |
| updateAndHandleLEDsTask | `updateAndHandleLEDsTask` | 2500 | NULL |

## LoRaMon (0 tasks)

| Task | Function | Stack | Priority/Param |
|---|---|---|---|

## RadioLib (0 tasks)

| Task | Function | Stack | Priority/Param |
|---|---|---|---|

## SX1262-Arduino-ESP32-driver (0 tasks)

| Task | Function | Stack | Priority/Param |
|---|---|---|---|

## MeshCore-official (0 tasks)

| Task | Function | Stack | Priority/Param |
|---|---|---|---|

## MeshCore-dup (0 tasks)

| Task | Function | Stack | Priority/Param |
|---|---|---|---|

## trail-mate (4 tasks)

| Task | Function | Stack | Priority/Param |
|---|---|---|---|
| usb_lib | `usb_lib_task` | 4096 | NULL |
| idf_gps | `worker_task` | 6144 | nullptr |
| screen_sleep | `screen_sleep_task` | 4096 | nullptr |
| tab5_heading | `task_main` | 6144 | nullptr |

## lunarcore (0 tasks)

| Task | Function | Stack | Priority/Param |
|---|---|---|---|

## meshcomod (3 tasks)

| Task | Function | Stack | Priority/Param |
|---|---|---|---|
| touch_poll | `touchPollTaskFn` | 4096 | // 4 KB stack â€” only calls heltecV4CapTouchCheck
      nul |
| tdeck_touch | `touchPollTask` | 3072 | nullptr |
| notify | `tdeckNotifyTaskFn` | 4096 | nullptr |

## akita-bridge (0 tasks)

| Task | Function | Stack | Priority/Param |
|---|---|---|---|

## awesome-meshcore (0 tasks)

| Task | Function | Stack | Priority/Param |
|---|---|---|---|

## RWKV-LM (0 tasks)

| Task | Function | Stack | Priority/Param |
|---|---|---|---|

## RWKV-X (0 tasks)

| Task | Function | Stack | Priority/Param |
|---|---|---|---|

## rwkv.cpp (0 tasks)

| Task | Function | Stack | Priority/Param |
|---|---|---|---|

## snntorch (0 tasks)

| Task | Function | Stack | Priority/Param |
|---|---|---|---|

## norse (0 tasks)

| Task | Function | Stack | Priority/Param |
|---|---|---|---|

## open-interpreter (0 tasks)

| Task | Function | Stack | Priority/Param |
|---|---|---|---|

## autogen (0 tasks)

| Task | Function | Stack | Priority/Param |
|---|---|---|---|

## gat45-p4 (0 tasks)

| Task | Function | Stack | Priority/Param |
|---|---|---|---|