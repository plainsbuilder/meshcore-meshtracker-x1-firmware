# MeshCore firmware for the Seeed SenseCAP MeshTracker X1

Prebuilt [MeshCore](https://meshcore.co.uk) firmware for the **Seeed SenseCAP MeshTracker X1**
(nRF52840 + Semtech LR2021 + dual-band L1/L5 GNSS). This is the card tracker that ships with Meshtastic.

These builds come from the port submitted upstream in
[meshcore-dev/MeshCore#3112](https://github.com/meshcore-dev/MeshCore/pull/3112)
(source branch: [`Hacuchino-hash/MeshCore@add-meshtracker-x1`](https://github.com/Hacuchino-hash/MeshCore/tree/add-meshtracker-x1)),
built against MeshCore master `03b6ef4` with RadioLib 7.7.1.

**Verified on real hardware:** boots, BLE pairing with the MeshCore app, two-way
over-the-air messaging with other MeshCore nodes (delivery ACKs), GPS fix, and
battery sensing (4.30 V full on the X1's high-voltage cell).

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
