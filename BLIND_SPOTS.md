# Angles morts du roadmap JARVIX-OS

## Critique — résoudre avant Phase 1

### 1. ESP-SR CPU réel bien plus élevé qu'estimé
Benchmarks officiels ESP-SR pour P4 @400MHz :
- AFE (MR+FD+HIGH_PERF) : Feed 12.5% + Fetch 9.8% = **~22% CPU**
- WakeNet9 : 2.6ms/frame (32ms) = **~8% CPU**
- MultiNet7 : 8ms/frame (32ms) = **25% CPU**
- **Total pipeline parole : ~55% CPU** — rien que la reconnaissance vocale

Notre estimation de 40% pour Opus était trop optimiste. Avec Opus + SDIO + LVGL, on dépasse 100% sur un seul core. **Il faut un plan d'affinité de core explicite.**

### 2. Aucun plan d'affinité de cores P4
Le P4 a **2 cores RISC-V @400MHz**. Nous n'avons jamais décidé :
- Core 0 : AFE + WakeNet + MultiNet + Opus ? (bouffe ~80% CPU)
- Core 1 : SDIO + LVGL + Lua + MeshCore ? (risque de conflit UI/réseau)
- **Priorité critique** : découpage core×tâche avant toute implémentation

### 3. LiveKit SDK en Developer Preview (v0.3.8)
- Pas prêt pour la production (bugs possibles, APIs instables)
- Utilise `esp_capture` + Protobuf → consommation heap inconnue sur PSRAM
- Modèle de threads LiveKit : priorités **5-20** — en conflit direct avec notre System Governor (1-3) et les tâches IDF par défaut
- **Risque d'inversion de priorité** non évalué

### 4. Gestion du firmware C6 (slave_fw)
- Le C6 a besoin d'un firmware `esp_hosted` slave spécifique
- Flashé une fois à l'offset `0x310000` (partition `slave_fw`)
- Les cartes Waveshare livrées avec v0.0.0 (défectueux Bluetooth)
- **Aucune procédure documentée** pour flasher/mettre à jour le firmware C6
- Le roadmap suppose que le C6 marche "out of the box" — c'est faux pour certains lots

## Important — à intégrer dans le plan

### 5. Consommation et brownout
- P4 + C6 + WiFi + I2S + LVGL = pic possible >500mA
- Bug connu : CHIP_PU du C6 maintenu HIGH quand P4 dort → **33mA parasite** (fuite)
- Aucun condensateur de découplage (470µF) spécifié dans le design
- Aucune gestion de mode sommeil/batterie
- **Recommandé** : ajouter Phase 0.5 : test de brownout sous charge maximale

### 6. Alternative esp-wifi-remote (plus simple qu'esp-hosted raw)
- Espressif a sorti `esp_wifi_remote` qui encapsule `esp_hosted` avec API WiFi standard
- `idf.py add-dependency "espressif/esp_wifi_remote"` + `esp_wifi_remote` component
- Transparent : `esp_wifi_init()` marche comme sur un ESP32 normal
- **Simplifie l'étape 4** (intégration esp-hosted NG) — utiliser `esp_wifi_remote` au lieu de `esp_hosted` directement

### 7. Pas de stratégie OTA pour le firmware P4
- Comment mettre à jour le firmware en production ?
- Via LiveKit data channel ? Via serveur HTTPS ?
- Partition OTA_0 + OTA_1 ? Taille disponible ~6.5MB sur 16MB flash
- **Absence totale** de mécanisme de mise à jour dans le roadmap

### 8. Validation SX1262 sur T-Display P4 spécifiquement
- Le DIO1 passe par XL9535 (I2C expander) → pas de IRQ fiable
- Nous avons déjà documenté le SPI polling comme solution, mais **aucun test réel** avec RadioLib sur ce board
- La modification XL9535 P01 → SKY13453 SPDT pour antenne = non testée

## Secondaire — à documenter mais pas bloquant

### 9. Flashage en production
- C6 firmware : Flashé via ESP-Prog sur header PROG_C6 (P4 en bootloader mode)
- P4 firmware : USB-C UART standard
- Aucune procédure de test assembleur définie

### 10. Sécurité du lien SDIO
- SDIO 4-bit 40MHz sans chiffrement entre P4 et C6
- Si quelqu'un écoute les lignes SDIO, tout le traffic WiFi est visible
- Solution : session DTLS au niveau LiveKit (déjà fait), mais trafic SDIO nu

### 11. Taille des firmwares MeshCore vs Meshtastic
- Pour le dual-boot ESP-Launcher, besoin de connaître la taille de chaque firmware
- Partition OTA ~6.5MB chacune
- Meck-P4-main actuel fait ~2.5MB avec LVGL + MeshCore + RadioLib → tient
- Meshtastic (basé sur trail-mate) pourrait être plus gros → **à vérifier**

### 12. Monitoring / débogage terrain
- Comment diagnostiquer un crash sur un déploiement terrain ?
- Pas de port série dans le produit final
- **Solution** : télémétrie LiveKit data channel + core dump sur SD
- Absent du roadmap

---

## Résumé des actions à ajouter au roadmap

| Priorité | Action |
|----------|--------|
| **P0** | Définir l'affinité de cores P4 (Core 0 vs Core 1) |
| **P0** | Mesurer CPU réel AFE + WakeNet + MultiNet sur P4 |
| **P0** | Valider version du firmware C6 et procédure de flash |
| **P1** | Tester brownout sous charge max (WiFi + SDIO + I2S + LVGL) |
| **P1** | Remplacer esp-hosted NG par esp_wifi_remote (plus simple) |
| **P1** | Résoudre le conflit de priorités LiveKit (5-20) vs System Governor (1-3) |
| **P2** | Ajouter stratégie OTA (HTTPS ou LiveKit data channel) |
| **P2** | Valider RadioLib + SX1262 SPI polling sur T-Display P4 réel |
| **P2** | Ajouter monitoring terrain (télémétrie + core dump sur SD) |
