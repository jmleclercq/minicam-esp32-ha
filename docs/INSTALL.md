# Install (ESPHome Builder / Dashboard) — MiniCam ESP32

This guide installs the **MiniCam ESP32** firmware using **ESPHome Builder / Dashboard** (Home Assistant add-on) on one of two boards:

- **Seeed Studio XIAO ESP32S3 Sense** -> `esphome/minicam-esp32.yaml`
- **AI-Thinker ESP32-CAM** -> `esphome/minicam-esp32cam.yaml` (see the ESP32-CAM section below)

## Prerequisites
- Home Assistant running
- ESPHome add-on installed and working
- Your `secrets.yaml` contains:
  - `wifi_ssid`
  - `wifi_password`
  - `api_encryption_key`
  - `ota_password`

## 1) Wire & power (XIAO ESP32S3 Sense)
- Plug the XIAO ESP32S3 Sense via **USB-C data cable**.
- Keep the Sense expansion (camera) firmly connected.

## 2) Create or open the device in ESPHome
- Open **ESPHome** in Home Assistant.
- Create a new device or select your existing one (e.g. `minicam-esp32`).

## 3) Paste the firmware YAML
Copy the content of `esphome/minicam-esp32.yaml` into the device configuration.

## 4) First flash (USB)
- Click **INSTALL**
- Choose **Plug into this computer** (USB/Serial)
- Select the detected serial port (e.g. `/dev/ttyACM3`)
- Wait for **Compile** → **Flash** to complete

> If it fails to connect, hold **BOOT** while plugging USB, then retry INSTALL.

## 5) Verify it works
From the ESPHome logs, note the IP address (example: `192.168.1.145`).

Test in a browser:
- Stream: `http://<IP>:8080`
- Snapshot: `http://<IP>:8081`

## 6) Home Assistant integration
Home Assistant should auto-discover the device via ESPHome:
- **Settings → Devices & Services → ESPHome**
- Add the discovered device.

## ESP32-CAM (AI-Thinker) variant
Steps 2, 3, 5, 6 are identical, using `esphome/minicam-esp32cam.yaml`. Differences for the first flash:

1. **With a programming base board (ESP32-CAM-MB)**: plug the ESP32-CAM onto the base and the base into your computer. Nothing else to wire, no jumper.
   **With a bare ESP32-CAM + USB-UART adapter**: wire it and enter flash mode (GPIO0 -> GND), see [`WIRING.md`](WIRING.md).
2. Make sure your user can access the serial port: `sudo usermod -aG dialout $USER`, then re-login.
3. In ESPHome choose **Plug into this computer** and select `/dev/ttyUSB0`
   (or from a terminal: `esphome run esphome/minicam-esp32cam.yaml --device /dev/ttyUSB0`).
4. Only with the bare-board method: remove the GPIO0-GND wire and press RESET.
5. Add the device in Home Assistant (**Settings -> Devices & Services -> ESPHome**) and enter the `api_encryption_key` from your `secrets.yaml`.

## Update via OTA (later)
Once the device is on Wi‑Fi:
- In ESPHome, click **INSTALL**
- Choose **Wirelessly** (OTA)
