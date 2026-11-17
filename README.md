# Amiga Full USB Keyboard Adapter

**Use a normal USB keyboard on your Amiga.** A small adapter plugs into the Amiga keyboard port and speaks the
original Amiga keyboard protocol. No drivers, no software on the Amiga side.

This repository holds the description of the adapter
and the **base firmware** (version 1.1.1) with a bootloader that updates the firmware **from a USB flash drive**.


## Features

- USB HID keyboards, wireless keyboard dongles, keyboards with a built-in hub (tested with an Apple A1243).
- Amiga 500 / 600 / 1000 / 1200 / 2000 / 3000 / 4000 / CD32 (hardware variants below).
- Amiga reset from the keyboard: <kbd>Ctrl</kbd>+<kbd>Left Amiga</kbd>+<kbd>Right Amiga</kbd>,
  <kbd>Ctrl</kbd>+<kbd>Left Alt</kbd>+<kbd>Right Alt</kbd> or <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>Del</kbd>.
- Caps Lock LED works on the USB keyboard.
- Handles keyboards that send more than 6 keys, ISO keys, NumLock, two Ctrl keys, and keys that are held while the keyboard is unplugged.
- **Firmware update from a USB flash drive**: copy `kb_firm_x.x.x.fw` to a FAT32 drive, plug it into the adapter, switch on.
  The update file is signed (Ed25519) and encrypted (XChaCha20); a foreign or damaged file is refused, an older version is not installed.
  The result is written to `UPDATE.TXT` on the drive.
- Status LED: blinks evenly while waiting for a keyboard.

## Download

Everything is in [`firmware/`](firmware/):

| File | What it is |
|---|---|
| `kb_firm_1.1.1.fw` | update file for a USB flash drive (for adapters that already run this bootloader) |
| `SHA256SUMS` | checksums |

## Flashing in short

1. **First time**  Step by step: [docs/flashing.md](docs/flashing.md). Put `kb_firm_x.x.x.fw` in the root folder of a FAT32 USB flash drive,
   plug the drive into the **switched-off**
   adapter, switch on, wait ten seconds. Three long LED flashes mean "updated"; read `UPDATE.TXT` on the drive for details.


## Status

-  update from a USB flash drive (also the "file not found" report), an Apple A1243 keyboard with its built-in hub 
- **Do not plug the flash drive into a running adapter**: switch the power off first.

