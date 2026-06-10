# Script 06: Memory & Timing Patterns


## Comptage de patterns par repo

| Pattern | esp-adf | esp-hosted | xiaozhi | ha_voice | meshcore | meshtastic | jarvix | OpenMQTTGa | LoRaMon | meshtastic | lorawan-sn | RadioLib | Meck-P4 | T-Display- | SigurdOS | Meck-P4-v2 | MeshCore-o | meshtastic | trail-mate |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| axi_prio | 0 | 0 | 0 | 0 | 0 | 1 | 0 | 0 | 0 | 0 | 0 | 4 | 0 | 0 | 0 | 0 | 2 | 1 | 0 |
| cache_disable | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| dram_attr | 0 | 1 | 0 | 0 | 2 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 2 | 2 | 0 | 2 | 0 | 0 | 0 |
| iram_attr | 12 | 20 | 2 | 0 | 48 | 17 | 1 | 0 | 0 | 0 | 0 | 2 | 48 | 48 | 1 | 48 | 0 | 17 | 1 |
| malloc_dma | 4 | 12 | 0 | 0 | 15 | 0 | 4 | 0 | 0 | 0 | 0 | 0 | 14 | 15 | 0 | 14 | 0 | 0 | 4 |
| malloc_internal | 5 | 0 | 0 | 0 | 2 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 2 | 2 | 8 | 2 | 0 | 0 | 0 |
| malloc_psram | 8 | 0 | 2 | 1 | 28 | 0 | 3 | 0 | 0 | 0 | 0 | 0 | 35 | 25 | 11 | 35 | 0 | 0 | 1 |
| psram_alloc | 105 | 10 | 14 | 31 | 131 | 123 | 57 | 4 | 0 | 0 | 0 | 0 | 163 | 73 | 132 | 163 | 3 | 123 | 133 |
| semaphore | 68 | 110 | 0 | 41 | 196 | 14 | 150 | 78 | 0 | 0 | 0 | 0 | 196 | 73 | 0 | 196 | 6 | 14 | 184 |
| timestamp | 21 | 8 | 0 | 8 | 148 | 0 | 44 | 0 | 0 | 0 | 0 | 5 | 151 | 106 | 1 | 151 | 0 | 0 | 18 |
| watchdog | 2 | 0 | 0 | 30 | 37 | 96 | 9 | 18 | 0 | 5 | 0 | 2 | 42 | 31 | 4 | 42 | 4 | 96 | 43 |