# SYSTEM INTELLIGENCE MANIFEST : JARVIX-TRAIL (P4+C6)
## STATUS: SYSTEM KNOWLEDGE LOCKED

### 1. FORENSIC TRUTH (Verified Diagnostic)
*   **Contention Root:** Jitter is physical AXI bus arbitration delay between SDIO (Bridge), I2S (Audio), and LVGL (UI).
*   **Amplificateur :** Cache thrashing provoqué par des buffers PSRAM non-alignés.
*   **Inversion Priorité :** Les tâches FreeRTOS initiales (Meck-P4) étaient toutes à priorité 5, provoquant une starvation des ISR réseau.

### 2. ARCHITECTURAL BLUEPRINT (SRAL Layer)
Tout code ajouté doit respecter ce contrat :
*   **Memory Mapping :** SDIO/I2S buffers -> DRAM interne via `DRAM_ATTR` + alignment 64.
*   **Bus Arbitration :** Accès matériel -> via `BusArbitrator` (SPI/SDIO mutex).
*   **Scheduling :** Priorités -> Bridge (15) > LoRa (12) > Audio (8) > UI (3).
*   **Télémétrie :** Asynchrone uniquement via `EventBus` (No polling).

### 3. PROJECT SOURCE OF TRUTH
*   **Dossier Maître :** `C:/Users/videl/Desktop/lyligo/coreos/JARVIX-TRAIL/`
*   **Pilier Audio :** Drivers purifiés (ESP32-audioI2S).
*   **Pilier Bridge :** esp-hosted (Official v2.6.3+).
*   **Orchestrateur :** `main.cpp` (Service-oriented).

### 4. FORENSIC DATA INDEX
*   **Rapports :** `C:/Users/videl/Desktop/lyligo/coreos/reports/final_audit/*.json`
*   **Contrat :** `JARVIX-TRAIL/include/system_contract.h`
*   **Projets source :** Référentiel forensique dans `C:/Users/videl/Desktop/lyligo/`

*Cette base est synchronisée avec l'agent. Toute future requête système sera analysée par rapport à ce manifest.*
