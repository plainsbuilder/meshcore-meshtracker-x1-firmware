# MeshCore firmware for the Seeed SenseCAP MeshTracker X1

Prebuilt [MeshCore](https://meshcore.co.uk) firmware for the **Seeed SenseCAP MeshTracker X1**
(nRF52840 + Semtech LR2021 + dual-band L1/L5 GNSS). This is the card tracker that ships with Meshtastic.

X1 support is now merged into official MeshCore
([meshcore-dev/MeshCore#3112](https://github.com/meshcore-dev/MeshCore/pull/3112)).
These builds are the full X1 feature set: current MeshCore dev (`9b4a591`, 2026-08-06)
plus the follow up features from
[meshcore-dev/MeshCore#3122](https://github.com/meshcore-dev/MeshCore/pull/3122)
(source branch: [`plainsbuilder/MeshCore@x1-notifications`](https://github.com/plainsbuilder/MeshCore/tree/x1-notifications)).
Use these until the next official MeshCore release ships with the X1 built in.

**On top of stock companion firmware:**

* Color coded status blinks: green heartbeat, blue when the app is connected, amber
  when messages are waiting, red on low battery, plus a short rainbow sweep on boot
  and on message arrival
* Vibration on incoming messages, whether or not the app is connected
* Triple press cycles alert modes: Buzz+Vibe, Buzz only, Vibe only, Silent. Each mode
  confirms by tone and/or vibration, and the setting persists across reboots
* SPA06 barometer reported through telemetry (temperature and pressure in the app)
* Charge status on the LED while docked: amber breathing while charging, dim green when full

**All features are hardware verified on a real X1:** boot, BLE pairing, two-way
over-the-air messaging with delivery ACKs, GPS fix, battery sensing, notifications,
haptics and charge display.

## Which file do I flash?

| File | Use case |
|------|----------|
| [`MeshCore_MeshTracker_X1_companion_radio_ble.uf2`](firmware/MeshCore_MeshTracker_X1_companion_radio_ble.uf2) | **Most people want this.** Pairs with the MeshCore phone app over Bluetooth. Pairing PIN: `123456` |
| [`MeshCore_MeshTracker_X1_companion_radio_usb.uf2`](firmware/MeshCore_MeshTracker_X1_companion_radio_usb.uf2) | Companion over USB serial instead of BLE |
| [`MeshCore_MeshTracker_X1_repeater.uf2`](firmware/MeshCore_MeshTracker_X1_repeater.uf2) | Standalone repeater (default admin password: `password`) |
| [`MeshCore_MeshTracker_X1_room_server.uf2`](firmware/MeshCore_MeshTracker_X1_room_server.uf2) | Room/BBS server (default room password: `hello`) |

The `*-dfu.zip` files are the same firmware packaged for `adafruit-nrfutil` serial DFU,
if you prefer flashing over the serial port instead of UF2 drag-and-drop.

## Flashing

1. **Enter DFU mode:** hold the device button, then quickly connect the USB-C cable twice.
   The LED goes solid and an `X1` / `X1-BOOT` drive appears on your computer.
2. **Copy one `.uf2` file** onto that drive. The device reboots into MeshCore by itself.
3. First boot after switching from Meshtastic can take ~30 s while it formats its
   settings storage.

Going back to Meshtastic works the same way: enter DFU mode and flash a Meshtastic X1 UF2.

## After flashing

- **Set your region's radio preset** in the MeshCore app. Builds default to
  869.618 MHz / BW 62.5 / SF 8 (EU). US meshes typically use 910.525 MHz / BW 250 / SF 10.
- **GPS is off by default** (saves battery). Enable it in the app: node settings →
  sensor settings → set `gps` to `1`. First fix needs sky view and may take a minute
  or two; later fixes are faster.
- Power on: single button press. Power off: hold the button ~5 s.

## Disclaimer

Community build, provided as-is. Not affiliated with Seeed Studio or the MeshCore team.
Flash at your own risk. Firmware is MIT-licensed like MeshCore itself (see [LICENSE](LICENSE)).
