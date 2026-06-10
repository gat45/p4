# Script 07: Jitter Simulation

## Configuration
- Frame size: 20 ms
- Loss rate target: 2%
- Jitter range: -5 to +25 ms
- Buffer size: 120 ms

## Résultats
- Frames totales: 500
- Frames perdues: 11 (2.2%)
- Frames tardives (>20ms jitter): 95
- Buffer underruns: 0 (0.0%)
- Buffer overflows: 0 (0.0%)
- Jitter moyen (abs): 11.66 ms
- Jitter max: 25 ms
- Buffer occupancy moyen: 60.0 ms

## Verdict
✅ Underrun rate acceptable (< 1%)
✅ Jitter moyen contrôlé