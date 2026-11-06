# MiniCam ESP32 — ESPHome cameras (XIAO ESP32S3 Sense & ESP32-CAM) for Home Assistant

![ESPHome](https://img.shields.io/badge/ESPHome-Compatible-000000?logo=esphome)
![Home Assistant](https://img.shields.io/badge/Home%20Assistant-Compatible-41BDF5?logo=homeassistant&logoColor=white)
![ESP32](https://img.shields.io/badge/ESP32%20%7C%20ESP32--S3-blue)
![CI](https://github.com/jmleclercq/minicam-esp32-ha/actions/workflows/validate.yml/badge.svg)
![License](https://img.shields.io/badge/License-MIT-green)
![Status](https://img.shields.io/badge/Status-Active-success)

This repository is a **starter + working reference** for ESPHome-based **cameras for Home Assistant**.
It provides a **fully working camera**, supported on two boards:

| Board | Config | Flashing |
|---|---|---|
| Seeed Studio **XIAO ESP32S3 Sense** | [`esphome/seeed-xiao-esp32s3-sense.yaml`](esphome/seeed-xiao-esp32s3-sense.yaml) | Native USB-C |
| **AI-Thinker ESP32-CAM** (ESP32-S, OV2640) | [`esphome/ai-thinker-esp32-cam.yaml`](esphome/ai-thinker-esp32-cam.yaml) | Programming base board (ESP32-CAM-MB) or external USB-UART adapter |

---

## What you get (current status)

- ✅ Working ESPHome firmware (Wi‑Fi, API encryption, OTA)
- ✅ Shared config in [`esphome/common.yaml`](esphome/common.yaml), board-specific files stay small
- ✅ Camera initialized and stable (PSRAM enabled)
- ✅ HTTP endpoints:
  - Stream: `http://<IP>:8080`
  - Snapshot: `http://<IP>:8081`
- ✅ Home Assistant integration via ESPHome API
- ESP32-CAM defaults to **320x240** (~3–4 fps over a weak Wi‑Fi link); XIAO ESP32S3 Sense uses 640x480

---

## Next goal

Reliability, enclosure and clean power for the cameras.

See [`ROADMAP.md`](ROADMAP.md).

---

## Quick install

1) Add secrets (or reuse your existing `secrets.yaml`), based on [`esphome/secrets.yaml.example`](esphome/secrets.yaml.example):
- `wifi_ssid`, `wifi_password`, `api_encryption_key`, `ota_password`, `ap_password`

2) Flash from ESPHome Builder/Dashboard:
- Use the config matching your board (`seeed-xiao-esp32s3-sense.yaml` for XIAO, `ai-thinker-esp32-cam.yaml` for ESP32-CAM). Both include `common.yaml`, so copy it next to them
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
    ├── common.yaml                    # Shared config (Wi-Fi, API, OTA, sensors, HTTP endpoints)
    ├── seeed-xiao-esp32s3-sense.yaml  # ESPHome config — XIAO ESP32S3 Sense (camera + board)
    ├── ai-thinker-esp32-cam.yaml      # ESPHome config — AI-Thinker ESP32-CAM (camera + board)
    └── secrets.yaml.example           # Template for secrets.yaml (not committed)
```

## Documentation

- [Install guide](docs/INSTALL.md)
- [Home Assistant integration](docs/HOME_ASSISTANT.md)
- [Wiring notes](docs/WIRING.md)
- [Troubleshooting](docs/TROUBLESHOOTING.md)
