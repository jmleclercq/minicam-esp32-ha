# MiniCam ESP32 — ESPHome cameras (XIAO ESP32S3 Sense & ESP32-CAM) for Home Assistant

![ESPHome](https://img.shields.io/badge/ESPHome-Compatible-000000?logo=esphome)
![Home Assistant](https://img.shields.io/badge/Home%20Assistant-Compatible-41BDF5?logo=homeassistant&logoColor=white)
![ESP32-S3](https://img.shields.io/badge/ESP32-S3-blue)
![License](https://img.shields.io/badge/License-MIT-green)
![Status](https://img.shields.io/badge/Status-Active-success)

This repository is a **starter + working reference** for a Home Assistant **control screen project** built with ESPHome.
The first validated milestone is a **fully working camera**, supported on two boards:

| Board | Config | Flashing |
|---|---|---|
| Seeed Studio **XIAO ESP32S3 Sense** | [`esphome/minicam-esp32.yaml`](esphome/minicam-esp32.yaml) | Native USB-C |
| **AI-Thinker ESP32-CAM** (ESP32-S, OV2640) | [`esphome/minicam-esp32cam.yaml`](esphome/minicam-esp32cam.yaml) | Programming base board (ESP32-CAM-MB) or external USB-UART adapter |

---

## What you get (current status)

- ✅ Working ESPHome firmware (Wi-Fi, API encryption, OTA)
- ✅ PSRAM enabled (required for camera)
- ✅ Camera initialized and stable
- ✅ HTTP endpoints:
  - Stream: `http://<IP>:8080`
  - Snapshot: `http://<IP>:8081`
- ✅ Home Assistant integration via ESPHome API

---

## Next goal

Turn this into a **Home Assistant control screen**:
- UI/UX definition
- Display selection + drivers
- ESPHome display stack (LVGL or display component)
- Core controls (lights, scenes, thermostats, Sonos)
- Reliability + enclosure + clean power

See [`ROADMAP.md`](ROADMAP.md).

---

## Quick install

1) Add secrets (or reuse your existing `secrets.yaml`), based on [`esphome/secrets.yaml.example`](esphome/secrets.yaml.example):
- `wifi_ssid`, `wifi_password`, `api_encryption_key`, `ota_password`

2) Flash from ESPHome Builder/Dashboard:
- Use the config matching your board (`minicam-esp32.yaml` for XIAO, `minicam-esp32cam.yaml` for ESP32-CAM)
- Install via USB (ESP32-CAM: programming base or USB-UART adapter) for first flash, then OTA

3) Verify:
- Stream: `http://<IP>:8080`
- Snapshot: `http://<IP>:8081`

Full step-by-step guide: [`docs/INSTALL.md`](docs/INSTALL.md)

---

## Repository structure

```
├── LICENSE
├── README.md
├── ROADMAP.md
├── docs/
│   ├── INSTALL.md            # Step-by-step flashing & first setup (both boards)
│   ├── HOME_ASSISTANT.md     # Dashboard cards & HA integration tips
│   ├── WIRING.md             # Camera, buttons, antenna, ESP32-CAM wiring (programming base or USB-UART adapter)
│   └── TROUBLESHOOTING.md    # Common issues and fixes
└── esphome/
    ├── minicam-esp32.yaml    # ESPHome config — XIAO ESP32S3 Sense
    ├── minicam-esp32cam.yaml # ESPHome config — AI-Thinker ESP32-CAM
    └── secrets.yaml.example  # Template for secrets.yaml (not committed)
```

## Documentation

- [Install guide](docs/INSTALL.md)
- [Home Assistant integration](docs/HOME_ASSISTANT.md)
- [Wiring notes](docs/WIRING.md)
- [Troubleshooting](docs/TROUBLESHOOTING.md)
