# MASTER SYSTEM MAP & FORENSIC INDEX : LYLYGO

Ce document centralise l'intégralité de l'audit forensique et la structure de l'écosystème unifié `JARVIX-TRAIL`.

## 1. STRUCTURE UNIFIÉE (`C:\Users\videl\Desktop\lyligo\coreos\JARVIX-TRAIL\`)
Le projet `JARVIX-TRAIL` est la seule source de vérité architecturale.
```text
/include/
  - system_contract.h        # CONTRAT : Priorités, DMA, Bus, Mémoire
  - service_base.h           # Interface Service
  - t_display_p4_board.h     # Pin mapping (Golden Reference)
/main/
  - main.cpp                 # ORCHESTRATEUR (Asynchrone/Non-bloquant)
/core/
  - event_bus.cpp            # Bus d'événements (Normalisation)
  - bus_arbitrator.cpp       # Arbitrage matériel (SPI/SDIO/I2S)
/services/
  - bridge_service.cpp       # ESP-HOSTED (Stable)
  - audio_service.cpp        # ESP32-audioI2S (Stable)
  - voice_agent_service.cpp  # Inférence/Logique métier
```

## 2. INDEX DES RAPPORTS FORENSIQUES (`C:\Users\videl\Desktop\lyligo\coreos\reports\final_audit\`)
*   `MASTER_FORENSIC_REPORT.json` : Corrélation APK / Firmware.
*   `CROSS_REF_REPORT.json` : Audit architectural croisé.
*   `TOTAL_LOGIC_REPORT.json` : Catalogue des fonctions et dépendances.
*   `BUS_LOAD_REPORT.json` : Analyse de saturation bus (Jitter roots).
*   `MEMORY_LOCALITY_REPORT.json` : Profil DMA et Cache usage.
*   `MASTER_SYSTEM_STRESS_REPORT.json` : Rapport de pression systémique.

## 3. ÉTAT DE SYNCHRONISATION
L'écosystème est maintenant unifié. Le `JARVIX-TRAIL` est la base de production. Les autres dossiers (`Meck-P4`, etc.) ne servent plus que de **référentiel forensique** pour l'extraction de drivers.

*Source de vérité verrouillée.*
