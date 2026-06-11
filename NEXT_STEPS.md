# Prochaines étapes — JARVIX-OS

## 1. Intégrer LiveKit SDK comme composant ESP-IDF
- Remplacer `ha_client.c` (WebSocket custom) + composants Opus par le SDK LiveKit
- Configurer `livekit_init()`, `livekit_connect()`, `livekit_track_publish()`
- Valider la stack bidirectionnelle Opus 16kHz mono
- Utiliser l'exemple `voice_agent` comme référence
- Priorité: **Haute** — débloque toute la pipeline audio

## 2. Phase 0 : I2S loopback P4-only
- Flasher et exécuter `i2s_loopback_benchmark.c` sur le T-Display P4 réel
- Valider I2S 16kHz mono, trames de 20ms
- Mesurer p50/p95/p99, underruns/overruns DMA
- Valider que ES8311 peut être initialisé en playback+record simultané
- Priorité: **Haute** — prérequis physique à toute pipeline audio

## 3. Phase 1 : Pipeline audio complète sur P4
- AFE (acquisition I2S) → Opus encode → LiveKit transport
- Activer WakeNet9 avec mot-clé "Jarvis" (déjà compilé dans sdkconfig)
- Valider VAD + capture continue
- Priorité: **Haute** — première version fonctionnelle de la voix

## 4. Intégrer esp-hosted NG dans l'app principale
- Déplacer l'initialisation SDIO de l'exemple séparé vers le main app
- Configurer `esp_hosted_init()` avec watchdog V2
- Valider que C6 est détecté et que le lien WiFi est opérationnel
- Priorité: **Haute** — nécessaire pour toute communication WiFi

## 5. Phase 2 : Transport P4↔C6 SDIO
- Pipeline audio complète : mic → I2S → SDIO → C6 → WiFi → Orange Pi
- Valider la latence SDIO sous charge (buffer double avec jitter)
- Activer le watchdog V2 (reset GPIO C6 en cas de 0x107)
- Priorité: **Haute** — goulot d'étranglement principal

## 6. Benchmark Opus complexity=1 sur P4 réel
- Mesurer le CPU réel pour encode+decode Opus à complexity=1
- Valider l'hypothèse de 40% CPU sur P4
- Tester la stabilité sous charge combinée (SDIO + I2S + LVGL)
- Priorité: **Moyenne** — nécessaire avant mise en production

## 7. Benchmark SDIO sustained throughput sous charge WiFi
- Mesurer le débit réel soutenu (pas le pic bus de 36 Mbps)
- Tester avec WiFi actif (UDP 50/100/200 pkt/s)
- Identifier le point de saturation du C6 (théorique ~46.5 Mbps)
- Priorité: **Moyenne** — valide le dimensionnement

## 8. Phase 3 : Pipeline E2E complète
- Boucle complète : mic P4 → encode Opus → SDIO → C6 → WiFi LiveKit → Orange Pi
- Retour audio : Orange Pi → LiveKit → C6 → SDIO → P4 → decode Opus → I2S → haut-parleur
- Latence totale mesurée (objectif <500ms aller-retour)
- Priorité: **Haute** — livrable fonctionnel principal

## 9. Aligner les priorités RTOS
- Corriger les priorités dans le code pour correspondre aux bands logiques V3
- System Governor : I2S DMA=HARD LOCK, SDIO=HIGH, SX1262=MEDIUM, LVGL=LOW, Lua=BEST EFFORT
- Supprimer les contradictions entre fichiers (1-3 vs 15-25)
- Priorité: **Basse** — optimisation après validation fonctionnelle

## 10. Implémenter le dual-boot MeshCore/Meshtastic (ESP-Launcher)
- Adapter le mécanisme OTA d'ESP-Launcher (bmorcelli)
- Partition A = firmware MeshCore, Partition B = firmware Meshtastic
- Stocker les .bin des deux firmwares sur carte SD
- Menu de sélection au boot
- Pas de commutation runtime (sync word non fiable)
- Priorité: **Basse** — fonctionnalité secondaire

---

## Ordre recommandé
```
Phase 0 (I2S loopback) → LiveKit SDK → Phase 1 (audio P4)
→ esp-hosted NG → Phase 2 (SDIO) → Phase 3 (E2E)
→ Benchmarks (Opus + SDIO) → RTOS priorities → Dual-boot
```
