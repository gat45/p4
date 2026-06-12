# MASTER ARCHITECTURAL & FORENSIC BLUEPRINT: JARVIX-TRAIL (P4+C6)

## 1. STATUS: ARCHITECTURE LOCKED & STABILIZED
Le projet `JARVIX-TRAIL` est l'unique source de vérité. L'écosystème dispersé (50+ projets `lyligo`) a été audité, nettoyé et unifié sous un **System Resource Arbitration Layer (SRAL)**.

## 2. FORENSIC DIAGNOSTIC (Jitter Source)
*   **Cause Racine :** Contention matérielle sur le bus AXI/AHB due à l'overlap des accès DMA (SDIO vs I2S) et inefficacité du cache (Cache Thrashing).
*   **Preuve :** 56 KB de buffers dans `Meck-P4` (instable) vs 0.6 KB dans `trail-mate` (référence).
*   **Normalisation :** Suppression de la télémétrie bloquante (`esp_timer_get_time`) et alignement des DMA bursts sur 64 octets.

## 3. SYSTEM CONTRACT LAYER (`include/system_contract.h`)
Ce fichier définit les contraintes inviolables du build :
*   **DMA Arbitrage :** `DMA_BURST_SIZE_BYTES 64` (Standardisation AXI).
*   **Priorités FreeRTOS :** Bridge (15) > LoRa (12) > Audio (8) > UI (3).
*   **Locality Mémoire :** Usage exclusif de `DRAM_ATTR` pour les buffers de bus pour éliminer la contention PSRAM.

## 4. INTEGRATION & BUILD BLUEPRINT
1.  **Orchestrateur :** `main.cpp` (Service-oriented, asynchrone via `EventBus`).
2.  **Build System :** `CMakeLists.txt` unifié (Isolation des targets, injection forcée du contrat).
3.  **Sécurité :** `safe_flash_manager.py` (Backup forensique avant chaque écriture).
4.  **Nettoyage :** Dépôts "Polluants" (ex: `Meck-P4`) isolés. Utiliser `trail-mate` comme structure de référence.

## 5. RECOVERY PROTOCOL (No Brick Strategy)
*   En cas de crash : Restaurer via `p4_firmware_dump.bin`.
*   Toute nouvelle bibliothèque doit être déclarée dans le `CMakeLists` racine pour éviter le *shadowing* de symboles.
*   Ne jamais modifier les priorités sans mettre à jour `system_contract.h`.

*Système verrouillé. Toute déviation de ce contrat physique entraîne une rupture de la stabilité AXI.*
