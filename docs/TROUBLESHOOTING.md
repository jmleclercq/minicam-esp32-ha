# Troubleshooting (first basics)

## Camera doesn't start (ESP_FAIL)
1. Check that the Sense (camera) board is properly seated.
2. Confirm PSRAM is enabled (see `psram:` in the YAML).
3. Lower the resolution (e.g. `640x480`) to test.
4. Update ESPHome if needed (or try Arduino vs ESP-IDF framework).
5. Check the logs: `esphome logs ...`

## Device not discovered by HA
- Make sure HA and the device are on the same network.
- Check the `api:` section and that your firewall isn't blocking it.

## ESP32-CAM (AI-Thinker)

### `Permission denied: /dev/ttyUSB0`
Add your user to the `dialout` group, then log out and back in:
```
sudo usermod -aG dialout $USER
```

### `Failed to connect to ESP32: Wrong boot mode` / `Timed out waiting for packet header`
- **Programming base board**: re-seat the ESP32-CAM on the base, try another USB cable/port.
- **Bare board + USB-UART adapter**: connect **GPIO0 to GND** *before* powering/resetting, then press RESET; check TX/RX are crossed (adapter TX -> U0R, adapter RX -> U0T); power from **5 V**.

### Boot loop / brownout after flashing
- Bare board: remove the GPIO0-GND jumper, then press RESET.
- Use a good 5 V supply (powered USB port); weak power causes brownouts when Wi-Fi + camera start.

### Slow stream / high latency
The ESP32-CAM is sensitive to Wi-Fi signal. Check the `WiFi Signal` sensor, move the board closer to the access point, or use an external antenna (change the resistor on the board to select the U.FL connector).

### Image upside down
Set `vertical_flip` / `horizontal_mirror` under `esp32_camera:` in the YAML.

### `psram` / boot error on ESP32-CAM
Do not use `mode: octal` on the ESP32-CAM: it has quad PSRAM. Keep a plain `psram:` block.
