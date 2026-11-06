# Home Assistant — Dashboard cards & tips

Once the device is added through the ESPHome integration, you can display the camera in a dashboard.

## Option A — Use the ESPHome camera entity (recommended)
1. Edit your dashboard
2. **Add card** -> **Picture glance** (or **Picture Entity**)
3. Select the camera entity exposed by ESPHome (entity name depends on your setup)

For a **live** view, set `camera_view: live` (the default `auto` only shows a refreshed still image):

```yaml
type: picture-glance
camera_view: live
fit_mode: cover
camera_image: camera.<your_camera_entity>
entities:
  - entity: camera.<your_camera_entity>
```

> **"Idle" state is normal.** An ESPHome camera entity shows *Idle* (*Inactif*) until someone opens the card; Home Assistant then asks the device to start streaming. The first image can take a few seconds on a weak Wi‑Fi link.

## Option B — Generic Camera (bypass the ESPHome API)
If the entity does not display, or you want a stream independent of the API:
**Settings -> Devices & Services -> Add integration -> Generic Camera**
- Still image URL: `http://<IP>:8081/`
- Stream source URL: `http://<IP>:8080/`

## Option C — Use the HTTP stream for quick debugging
- Stream URL: `http://<IP>:8080`
- Snapshot URL: `http://<IP>:8081`

Add a **Webpage** card and paste the stream URL. Keep only one client on the stream at a time: the ESP32 handles very few simultaneous connections.

## Practical control entities to add
If you enabled the `restart` button (see YAML):
- Add a **Button** card linked to the restart entity for quick recovery.

## Networking notes
- Make sure Home Assistant and the device are on the same LAN/VLAN.
- mDNS names (may depend on your network):
  - XIAO ESP32S3 Sense: `minicam-esp32.local`
  - ESP32-CAM: `minicam-esp32cam.local`

## ESP32-CAM flash LED
The ESP32-CAM config exposes the on-board white LED as a **Light** entity (`MiniCam ESP32-CAM Flash`). It is very bright and gets hot: keep it off when not needed.
