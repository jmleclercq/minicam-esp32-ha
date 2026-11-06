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

## ESP32-CAM (AI-Thinker) + FT232

### `Permission denied: /dev/ttyUSB0`
Add your user to the `dialout` group, then log out and back in:
```
sudo usermod -aG dialout $USER
```

### `Failed to connect to ESP32: Wrong boot mode` / `Timed out waiting for packet header`
- Connect **GPIO0 to GND** *before* powering/resetting, then press RESET.
- Check TX/RX are crossed (FT232 TX -> U0R, FT232 RX -> U0T).
- Power from **5 V** (not 3.3 V): the ESP32-CAM draws too much for weak 3.3 V supplies.

### Boot loop / brownout after flashing
- Remove the GPIO0-GND jumper, then press RESET.
- Use a good 5 V supply (USB hub or powered port); weak power causes brownouts when Wi-Fi + camera start.

### `psram` / boot error on ESP32-CAM
Do not use `mode: octal` on the ESP32-CAM: it has quad PSRAM. Keep a plain `psram:` block.
