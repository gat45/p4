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
- `Meck-P4-main\main\examples\lvgl_9_ui\win_home_app_icon_camera_110x110px_rgb565a8.c:38` `0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00`
- `Meck-P4-main\main\examples\lvgl_9_ui\win_home_app_icon_camera_110x110px_rgb565a8.c:39` `0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00`
- `Meck-P4-main\main\examples\lvgl_9_ui\win_home_app_icon_camera_110x110px_rgb565a8.c:41` `0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00`
- `Meck-P4-main\main\keyboard_examples\radiolib_cc1101_send_receive\main.cpp:2` `* @Description: radiolib_cc1101_send_receive`
- `Meck-P4-main\main\keyboard_examples\radiolib_cc1101_send_receive\main.cpp:16` `#include "RadioLib.h"`
- `Meck-P4-main\main\keyboard_examples\radiolib_cc1101_send_receive\main.cpp:17` `#include "radiolib_bridge_driver.h"`
- `Meck-P4-main\components\meshcore\MeckUI.cpp:5723` `mesh->sendFlood(adv);`
- `Meck-P4-main\components\meshcore\MeckUI.cpp:12267` `//   Trace Path:    Run Trace → createTrace + sendDirect(TRACE flavoured),`
- `Meck-P4-main\components\meshcore\MeckUI.cpp:12581` `mesh->sendDirect(pkt, path_buf, path_byte_len);`

### Meshtastic
- `firmware-develop\src\input\MPR121Keyboard.cpp:14` `#define _MPR121_REG_MAX_HALF_DELTA_RISING 0x2B`
- `firmware-develop\src\mesh\LR11x0Interface.cpp:98` `int res = lora.begin(getFreq(), bw, sf, cr, syncWord, power, preambleLength, tcxoVoltage);`
- `firmware-develop\src\mesh\LR11x0Interface.cpp:104` `res = lora.begin(getFreq(), bw, sf, cr, syncWord, power, preambleLength, tcxoVoltage);`
- `firmware-develop\src\DisplayFormatters.cpp:8` `// If use_preset is false, always return "Custom" — callers such as RadioInterface and Channels`
- `firmware-develop\src\main.cpp:13` `#include "RadioLibInterface.h"`
- `firmware-develop\src\main.cpp:265` `RadioLibHal *RadioLibHAL = NULL;`
- `firmware-develop\test\test_mqtt\MQTT.cpp:363` `void test_sendDirectlyConnectedDecoded(void)`
- `firmware-develop\test\test_mqtt\MQTT.cpp:376` `void test_sendDirectlyConnectedEncrypted(void)`
- `firmware-develop\test\test_mqtt\MQTT.cpp:887` `RUN_TEST(test_sendDirectlyConnectedDecoded);`
