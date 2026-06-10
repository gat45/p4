# SYSTEM CHALLENGE DEEP — Cross-Reference Analysis

**Generated:** 10 June 2026  
**Methodology:** Cross-referenced COMPROMIS_TECHNIQUES.md, DESIGN_DECISIONS.md (System Contracts), and all 9 reverse engineering reports against actual JARVIX-OS source code.

---

## 1. RAW DATA INVENTORY (What actually exists in reports vs claims)

### Measured Performance Numbers in Reports

| Metric | Value | Source | Type |
|--------|-------|--------|------|
| Jitter buffer 120ms | 0 underruns, 0 overflows, 11.66ms avg jitter, 25ms max | S07_jitter_sim.md | **Simulated** |
| Frame loss at 2% target | 11/500 = 2.2% | S07_jitter_sim.md | **Simulated** |

### Estimated/Calculated Numbers (NOT measured)

| Metric | Value | Source Report | Notes |
|--------|-------|---------------|-------|
| I2S DMA latency | 1-5ms | TIMING_REPORT.md | Theoretical estimate |
| Opus encode latency | 2-5ms | TIMING_REPORT.md | Theoretical estimate |
| SDIO transport | 1-3ms | TIMING_REPORT.md | Theoretical estimate |
| WiFi TX latency | 1-10ms | TIMING_REPORT.md | Theoretical estimate |
| E2E total latency | 5.5-28ms | TIMING_REPORT.md | Sum of estimates |
| SDIO throughput | 1 Mbps (target) | UNIFIED_MODEL.json | Validation criteria target |
| SDIO throughput | 36 Mbps | COMPROMIS_TECHNIQUES.md | External ref "esp32p4-c6-wifi-test" |
| Opus CPU @ complexity=1 | ~40% | COMPROMIS_TECHNIQUES.md | External ref "esp32_opus benchmarks" |
| Opus CPU @ complexity=5 | ~70% | COMPROMIS_TECHNIQUES.md | External ref "esp32_opus benchmarks" |

### Critical Finding: ZERO measured performance data exists in any report for JARVIX-OS itself. Every performance number is either estimated, calculated, or sourced from external documents not included in the project.

---

## 2. QUESTION-BY-QUESTION ANALYSIS

### Q1: Does the 190ms jitter budget claim conflict with measured data?

**Claim (DESIGN_DECISIONS.md:90-91):**
```
C6 side (WiFi → SDIO):  80-150ms ring buffer
P4 side (SDIO → audio): 20-40ms ring buffer
Total worst-case:       190ms
```

**Actual data (S07_jitter_sim.md):**
- Simulated buffer: 120ms (NOT 190ms)
- Jitter max: 25ms, Avg: 11.66ms
- 0 underruns at 120ms buffer
- Buffer occupancy avg: 60ms

**CONTRADICTION / GAP:**
- The simulation only tested 120ms, not 190ms. The 190ms claim (150+40) is a pure theoretical sum never simulated or measured.
- The simulation suggests 120ms is already sufficient (0 underruns with 25ms max jitter), making 190ms an overestimate.
- No actual WiFi jitter was measured — the simulation uses synthetic jitter (-5 to +25ms), not real WiFi/SDIO conditions.
- **Conflict:** If 120ms works, why claim 190ms? The 190ms number is unsupported design headroom, not a requirement.

### Q2: Does "UART 921600 = 0.9 Mbps" match the reports?

**Claim (COMPROMIS_TECHNIQUES.md:8):**
```
UART DMA ESP32 921600 baud | ~0.9 Mbps | ESP-IDF specs
```

**Report data:** No report measures UART throughput. REVERSE_COMPLETE mentions UART only as fallback route.

**CONFIRMED (mathematically):**
- 921600 baud / 10 bits-per-byte (8N1) = 92160 B/s = 0.9216 Mbps ≈ 0.9 Mbps
- This is standard bit-rate math, not a measurement. The claim itself says "ESP-IDF specs" as source.
- No contradiction with any report data (no report contradicts it).

### Q3: Is Opus complexity=1 CPU 40% measured or estimated?

**Claim (COMPROMIS_TECHNIQUES.md:10):**
```
Opus complexity=1 16kHz | ~40% CPU single-core | esp32_opus benchmarks
```

**Report data:** ZERO Opus CPU measurements exist in any report. REVERSE_COMPLETE mentions Opus configs (64kbps, complexity=10 from esp-adf) but no CPU data. TIMING_REPORT notes "Opus encode spike → CPU overload" as a risk.

**GAP:**
- The source "esp32_opus benchmarks" is not in the project. No benchmark file, no sdkconfig with measurements.
- This is an external reference, not validated against the actual P4 hardware configuration.
- The 40% number is used as foundation for the entire Opus-on-P4 argument, but is untested.

### Q4: Does SDIO throughput of 36 Mbps match source report data?

**Claim (COMPROMIS_TECHNIQUES.md:7):**
```
SDIO réel 40MHz HT20 | 36 Mbps | esp32p4-c6-wifi-test
```

**Report data:**
- UNIFIED_MODEL.json validation criteria: "1 Mbps sustained on SDIO" (stage 2)
- REVERSE_COMPLETE: SDIO frame size 2048B, 20x2048B DMA pool, queue depth 100
- No throughput measurement exists

**GAP:**
- The source "esp32p4-c6-wifi-test" is not in the project reports.
- 36 Mbps at 40MHz 4-bit SDIO is theoretically plausible (40MHz × 4bit = 160Mbps raw, minus overhead ~36Mbps usable).
- The project's own validation criteria only require 1 Mbps, which is 36× lower.
- **CONTRADICTION with ASSERTION:** The claim of 36 Mbps is used to justify SDIO over UART, but 1 Mbps sustained would also be sufficient. The gap between claimed (36) and validated (1) is suspicious.

### Q5: Tasks/priorities in SYSTEM_CONTRACTS vs actual Meck-P4 code?

**CONTRADICTION — Multiple mismatches found:**

| Task | CONTRACTS (DESIGN_DECISIONS.md) | Actual Code | Conflict? |
|------|--------------------------------|-------------|-----------|
| I2S DMA feed | Core 0, prio 25 | audio_capture.c: FEED_TASK_PRIORITY=6 | **YES** (25 vs 6) |
| AFE/VAD | Core 0, prio 22 | audio_capture.c: FETCH_TASK_PRIORITY=5 | **YES** (22 vs 5) |
| SDIO transport | Core 0, prio 18 | sdio_watchdog.c: prio 5 | **YES** (18 vs 5) |
| LoRa scanner | Core 0, prio 18 | lora_scanner.c: prio 18 | CONFIRMED |
| LVGL UI | Core 1, prio 15 | main.cpp: UI_PRIO=20 | **YES** (15 vs 20) |
| Lua agent | Core 1, prio 10 | main.cpp: AGENT_PRIO=15 | **YES** (10 vs 15) |
| Voice pipeline | Core 1, prio 8 | main.cpp: PIPELINE_PRIO=10; voice_pipeline.c:10 | **YES** (8 vs 10) |
| DSP | Not in CONTRACTS | main.cpp: DSP_PRIO=24 | **GAP** (undefined) |
| Meck task | Not in CONTRACTS | meck_app.cpp: prio 3 | **GAP** (undefined) |
| MeckAudio | Not in CONTRACTS | MeckAudio.cpp: prio 5 | **GAP** (undefined) |

**Additional issue:** CONTRACTS states "Jamais de task priority > 20 sans review explicite" but actual code defines RADIO_PRIO=25, DSP_PRIO=24 without any review comment.

### Q6: Is ALPIG 1% CPU claim supported by any data?

**Claim (COMPROMIS_TECHNIQUES.md:106):**
```
ALPIG Level 2 CPU: ~1%
```

**Actual code (lora_scanner.c):**
- Simple additive heuristic classifier with 6 profiles
- 50ms poll interval (20 iterations/sec)
- Arithmetic operations only (add, multiply, sqrt, fminf, float math)
- Running on Core 0 at priority 18 with 8192 byte stack
- No CPU measurement instrumentation exists

**GAP:**
- The 1% claim is a pure estimate. No profiling, no perf counter, no ets_printf cycle measurement.
- The code has no CPU usage tracking or benchmark mode.
- COMPROMIS_TECHNIQUES claims Level 1 = 0.1%, Level 2 = 1% without any supporting methodology.

### Q7: Does the 50-100ms SX1262 switch window appear in any measured data?

**Claim (DESIGN_DECISIONS.md:117, lora_scanner.c:12,376):**
```
Profile switch blind gap: 50-100ms (BLOCKING, no audio here)
```

**Measured data:** NONE

**GAP:**
- The 50-100ms claim is a comment in the code, not a measurement.
- The scanner itself runs at 50ms poll interval, making it impossible to measure sub-50ms events.
- No oscilloscope trace, no timing capture, no empirical data.
- This number appears to be inherited from SX126x datasheet typical reconfiguration time.
- The code calls standby(), setFrequency(), setSpreadingFactor(), setBandwidth(), setSyncWord(), startReceive() — each with SPI transactions but actual duration is never measured.

### Q8: How many TODO/placeholder calls exist?

**From code audit of JARVIX-OS (excluding RadioLib, Opus 3rd-party):**

| Category | Count | Examples |
|----------|-------|---------|
| Direct `TODO` markers | 4 | SD card usage, queue for meck_task, deleteContactByIdx |
| `/* placeholder */` comments | 20+ | UI bodies, covers, battery gauge, settings |
| `show_not_implemented()` stubs | 4 | cb_todo_notes, cb_todo_web, cb_todo_voice, cb_todo_camera |
| Placeholder screens | 3 | scr_not_implemented, scr_admin_setting_placeholder, logged-in placeholder |
| `FIXME` markers | 3 | celt_encoder.c (PSHR16) |
| `"request not implemented"` | 1 | celt.c |
| `// NOT YET IMPLEMENTED` | 1 | MeckUI.cpp admin_cmd_line |

**From REVERSE_COMPLETE.md gap analysis:**
```
JARVIX-OS missing vs ha_voice reference:
- audio_capture.c (feed+fetch tasks)  → CRITICAL
- voice_pipeline.c (state machine)    → CRITICAL
- ha_client.c (WebSocket streaming)   → CRITICAL
- wifi_manager.c (C6 SDIO)            → CRITICAL
- audio_ref_buffer.c (AEC ring)       → HIGH
- tts_player.c (MP3 decode)           → HIGH
- bsp_extra.c (codec HAL)             → CRITICAL
- Opus encoder/decoder                → CRITICAL
- Command queue FSM                   → HIGH
- 3-tier task creation                → MEDIUM
- Jitter buffer double                → HIGH
```
Report says: **"Squelette — 70% manquant"** (Skeleton — 70% missing)

---

## 3. CLAIM SCORING MATRIX (COMPROMIS_TECHNIQUES.md vs Reports)

| Claim | Value | Report Evidence | Score |
|-------|-------|-----------------|-------|
| SDIO 40MHz HT20 throughput | 36 Mbps | Not in reports. External ref. Project validates at 1 Mbps. | **GAP** |
| UART 921600 baud | 0.9 Mbps | Not measured but standard math. No contradiction. | **CONFIRMED** (math) |
| UART 3Mbaud | 3 Mbps | Not measured. Standard math. | **CONFIRMED** (math) |
| Opus complexity=1 CPU | 40% | No project data. External benchmark. | **GAP** |
| Opus complexity=5 CPU | 70% | No project data. External benchmark. | **GAP** |
| WiFi stack CPU C6 | 30-40% | No project data. External benchmark. | **GAP** |
| Opus sur C6 (160MHz) | 60-70% | **Calculated** from 40% × (400/160), not measured | **GAP** |
| Latence UART frame 1024B @921600 | ~11ms | No project data. Pure calculation. | **GAP** |
| Latence SDIO frame 2048B | ~0.5ms | External ref. Not in project reports. | **GAP** |
| SDIO latency/frame | 0.5ms | Same as above | **GAP** |
| CPU overhead SDIO | ~5% | No measurement exists | **GAP** |
| Crypto overhead LoRa | ~2% | No measurement exists | **GAP** |
| Marge supplémentaire | ~5% | No measurement exists | **GAP** |
| Total CPU LoRa+SDIO+Crypto | ~12% | Sum of unmeasured estimates | **GAP** |
| Opus on P4 CPU | 40% → 60% free | External benchmark. Not validated. | **GAP** |
| C6 with Opus+WiFi CPU | 76% → 24% marge | Calculated from estimates. | **GAP** |
| ALPIG Level 1 CPU | ~0.1% | No measurement. No profiler. | **GAP** |
| ALPIG Level 2 CPU | ~1% | No measurement. No profiler. | **GAP** |
| ALPIG Level 3 CPU | ~15% | Suppressed. No measurement. | **GAP** |
| C6 proxy CPU total | ~80% (20% marge) | No measurement. Sum of estimates. | **GAP** |
| WiFi stack CPU | ~40% | External ref. Not in-project. | **GAP** |
| UDP proxy CPU | ~20% | No measurement. Estimate. | **GAP** |
| SDIO bridge CPU | ~15% | No measurement. Estimate. | **GAP** |
| GPIO/watchdog CPU | ~5% | No measurement. Estimate. | **GAP** |

---

## 4. CRITICAL CONTRADICTIONS

### C1: Priority System — Design vs Implementation Mismatch
DESIGN_DECISIONS.md (System Contracts) defines a priority tree that does not match the actual code in main.cpp. Contracts say LVGL=15, code says UI=20. Contracts say Lua=10, code says AGENT=15. Contracts say Audio feed=25, actual feed task runs at 6. The contract also claims "Jamais de task priority > 20 sans review explicite" while code defines RADIO=25 and DSP=24.

### C2: Jitter Budget — 190ms Not Simulated
System Contracts claim 190ms total worst-case jitter (150ms C6 + 40ms P4). The only jitter simulation uses 120ms buffer and succeeds. If 120ms works, 190ms is over-engineered. No real WiFi jitter measurement validates either number.

### C3: SDIO Throughput — 36 Mbps Claimed, 1 Mbps Validated
The COMPROMIS_TECHNIQUES document builds its entire SDIO-vs-UART argument on 36 Mbps throughput from an external test not in the project. The project's own validation criteria (UNIFIED_MODEL.json) require only 1 Mbps. The gap between claimed and validated is 36×.

### C4: ALPIG Performance Claims — Zero Instrumentation
Despite precise CPU claims (0.1%, 1%, 15%), the ALPIG implementation (lora_scanner.c) contains zero CPU timing instrumentation. The classifier is a handful of float comparisons running at 50ms poll interval.

---

## 5. SUMMARY COUNTS

| Rating | Count | Examples |
|--------|-------|---------|
| **CONFIRMED** | 2 | UART 921600=0.9Mbps (math), UART 3Mbaud=3Mbps (math) |
| **PARTIAL** | 1 | Jitter 190ms budget (partially simulated at 120ms, but not at 190ms) |
| **CONTRADICTION** | 4 | Task priorities mismatch (5+ differences), no priority>20 rule violated, DSP_PRIO=24 undefined in contracts |
| **GAP** | 18 | All CPU measurements, all latency measurements, SDIO throughput validation, Opus CPU benchmarks, ALPIG profiling, SX1262 switch timing |
| **UNKNOWN** | 0 | (All claims are assessable) |

**Bottom line: Every performance number in COMPROMIS_TECHNIQUES.md and DESIGN_DECISIONS.md is UNSUPPORTED by project data. The architecture decisions are built on external references and theoretical calculations, not empirical measurement.**
