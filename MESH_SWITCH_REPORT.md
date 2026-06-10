# Rapport Mesh: Switch MeshCore <-> Meshtastic

## Incompatibilites Fondamentales

| Aspect | MeshCore | Meshtastic | Switch Possible? |
|---|---|---|---|
| Sync Word | `0x1424` | `0x2b` | ? Registre simple |
| Packet Header | 1-byte compact | 16-byte protobuf | ? Format incompatible |
| Routing | Flood/Direct path-hash | Flood+NextHop+Relay | ? Logique differente |
| Encryption | AES-128 CBC + HMAC | AES-CTR / AES-256-CCM | ? Cles incompatibles |
| Identity | Ed25519 keys | 32-bit NodeNum | ? Mapping necessaire |
| Radio Driver | cpp_bus_driver | RadioLib | ?? Deux drivers separes |
| Serialization | Raw binary | Protobuf | ? Formats differents |

## Strategie de Switch Recommandee

### Option A: Dual Boot (Recommandee)
- 2 partitions OTA: MeshCore sur `ota_0`, Meshtastic sur `ota_1`
- NVS flag pour selectionner le mode au boot
- Reset radio + reinit complete au switch
- Avantage: Pas de contamination croisee
- Inconvenient: Switch lent (reboot necessaire)

### Option B: Runtime Switch (Complexe)
- Un seul firmware avec les deux stacks
- Radio abstract layer commun
- Swap du protocol stack en memoire
- Avantage: Switch rapide
- Inconvenient: Complexite elevee, risque de bugs

## Fichiers Cles pour le Switch

### MeshCore
- `Meck-P4-main\components\meshcore\meck_emoji_14.c:177` `0x49,0xfe,0xaa,0xfe,0x06,0xd5,0x46,0x83,0xca,0x8b,0x2b,0x9c,0x0a,0x94,0x0a,0x94,0x2b,0x9c,0xca,0x93,`
- `Meck-P4-main\components\meshcore\meck_emoji_14.c:225` `0x49,0xfe,0x28,0xfe,0x53,0xff,0x6f,0x63,0x90,0x6b,0x33,0xff,0x27,0xfe,0xf1,0xfe,0x98,0xff,0x97,0xff,`
- `Meck-P4-main\components\meshcore\meck_emoji_14.c:288` `0xff,0xff,0xcc,0x81,0x37,0x01,0x00,0x00,0x06,0x2b,0x4f,0x77,0x52,0x00,0x3a,0x26,0x00,0x00,0x13,0x5e,`
- `Meck-P4-main\components\meshcore\MeckUI.cpp:403` `// Noise floor display cache. The estimator itself lives in P4SX1262Radio`
- `Meck-P4-main\components\meshcore\MeckUI.cpp:3578` `// GetRssiInst (opcode 0x15) sampled every ~2 s in P4SX1262Radio's`
- `Meck-P4-main\components\meshcore\MeckUI.cpp:11901` `// sampling happens in P4SX1262Radio under the SPI lock; we just`
- `Meck-P4-main\components\meshcore\MeckUI.cpp:5477` `mesh->sendFlood(adv);`
- `Meck-P4-main\components\meshcore\MeckUI.cpp:10492` `//   Trace Path:    Run Trace → createTrace + sendDirect(TRACE flavoured),`
- `Meck-P4-main\components\meshcore\MeckUI.cpp:10806` `mesh->sendDirect(pkt, path_buf, path_byte_len);`

### Meshtastic
- `firmware-develop\src\input\MPR121Keyboard.cpp:14` `#define _MPR121_REG_MAX_HALF_DELTA_RISING 0x2B`
- `firmware-develop\src\mesh\LR11x0Interface.cpp:98` `int res = lora.begin(getFreq(), bw, sf, cr, syncWord, power, preambleLength, tcxoVoltage);`
- `firmware-develop\src\mesh\LR11x0Interface.cpp:104` `res = lora.begin(getFreq(), bw, sf, cr, syncWord, power, preambleLength, tcxoVoltage);`
- `firmware-develop\src\DisplayFormatters.cpp:8` `// If use_preset is false, always return "Custom" — callers such as RadioInterface and Channels`
- `firmware-develop\src\main.cpp:13` `#include "RadioLibInterface.h"`
- `firmware-develop\src\main.cpp:265` `RadioLibHal *RadioLibHAL = NULL;`
- `firmware-develop\src\mesh\FloodingRouter.cpp:1` `#include "FloodingRouter.h"`
- `firmware-develop\src\mesh\FloodingRouter.cpp:12` `FloodingRouter::FloodingRouter() {}`
- `firmware-develop\src\mesh\FloodingRouter.cpp:19` `ErrorCode FloodingRouter::send(meshtastic_MeshPacket *p)`
