# Wiring / Notes

## XIAO ESP32S3 Sense

### Camera
On the **XIAO ESP32S3 Sense**, the camera sits on the Sense expansion board (OV2640 or OV3660 depending on the batch).

The `esp32_camera` pin mapping in the YAML is based on Seeed's reference example.

### Buttons
- **BOOT**: useful to force bootloader mode if needed
- **RESET**: reboots the device

### Antenna
The XIAO has a U.FL connector to improve Wi-Fi/BT range if you have the external antenna.

## AI-Thinker ESP32-CAM (ESP32-S)

The ESP32-CAM has **no native USB**. Two ways to flash it:

### Option A — Programming base board (ESP32-CAM-MB, recommended)
Plug the ESP32-CAM onto the base board and connect the base to your computer with a USB cable.
- **No wiring needed**: the base handles boot mode and reset automatically.
- **No GPIO0-GND jumper needed.**
- The serial port appears as `/dev/ttyUSB0` (validated with an FT232R-based base, `0403:6001`).

### Option B — Bare ESP32-CAM + external USB-UART adapter (FT232 / CP2102 / CH340)
| Adapter | ESP32-CAM |
|---|---|
| 5V (jumper set to 5V) | 5V |
| GND | GND |
| TX | U0R (GPIO3) |
| RX | U0T (GPIO1) |

Flash mode:
1. Connect **GPIO0 to GND** (jumper wire).
2. Press **RESET** (or re-plug power).
3. Flash (`esphome run esphome/ai-thinker-esp32-cam.yaml`, select `/dev/ttyUSB0`).
4. Remove the GPIO0-GND wire, press **RESET** to boot the firmware.

### Camera pinout used in `ai-thinker-esp32-cam.yaml`
| Signal | GPIO |
|---|---|
| XCLK | 0 |
| SDA / SCL | 26 / 27 |
| D0-D7 | 5, 18, 19, 21, 36, 39, 34, 35 |
| VSYNC / HREF / PCLK | 25 / 23 / 22 |
| Power down | 32 |
| Flash LED | 4 |
