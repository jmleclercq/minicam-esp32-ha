# Roadmap

Ongoing work on the MiniCam ESPHome cameras for Home Assistant.

## Milestone 1 — Camera foundation ✅
- [x] Flashable ESPHome config
- [x] Wi‑Fi + API + OTA
- [x] Camera working (PSRAM enabled)
- [x] HTTP stream + snapshot endpoints
- [x] Second board supported: AI-Thinker ESP32-CAM (validated on hardware: boots, camera + Wi-Fi OK)
- [x] Shared config (`common.yaml`) and CI validation of the YAML files

## Milestone 2 — Physical enclosure & mounting
- [ ] Pick / design an enclosure (3D print, off-the-shelf, wall mount)
- [ ] Camera placement (angle, field of view, anti-glare)
- [ ] Cable management

## Milestone 3 — Power strategy (clean install)
- [ ] Keep USB-C 5V (baseline)
- [ ] Investigate direct 5V input (regulated) without a bulky charger
- [ ] Optional: PoE-to-5V splitter (external), if wall-mounted

## Milestone 4 — Reliability & performance
- [ ] Watchdog / auto-restart strategy
- [ ] Camera tuning (resolution, JPEG quality, FPS)
- [ ] Wi‑Fi roaming / reconnection robustness (external antenna on ESP32-CAM)

## Milestone 5 — Advanced features (optional)
- [ ] Motion detection workflow (HA-side)
- [ ] Local snapshots to storage (SD / HA)
- [ ] Audio (mic) experimentation if relevant
- [ ] Privacy controls (physical shutter / disable stream)
