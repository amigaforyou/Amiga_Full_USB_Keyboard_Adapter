# Flashing the adapter


## What you need

- the adapter;
- a FAT32 USB flash drive (for later updates).

Download `Amiga_Full_USB_Keyboard-1.1.1.hex` from [`firmware/`](../firmware/) and check it against `SHA256SUMS`.

## 1. Updating from a USB flash drive

1. Format a USB flash drive as **FAT32** (FAT16/FAT12 also work; exFAT and NTFS do not). A small drive (2–16 GB) is best.
2. Copy the update file to the **root folder** of the drive: `kb_firm_x.x.x.fw` (for example `kb_firm_1.1.1.fw`).
   Any name that starts with `kb_firm_` is accepted; if there are several files, the highest version is taken.
3. **Switch the adapter off** (switch the Amiga off or unplug the adapter).
4. Plug the flash drive **directly** into the USB port of the adapter (not through a hub).
5. Switch on. The LED blinks fast for a few seconds, then:
   - **3 long flashes**: the firmware was updated;
   - **10 fast flashes**: not updated (the reason is in `UPDATE.TXT`), or there is no `kb_firm_*` file on the drive.
6. Switch off, remove the drive, switch on again.

Only a version **higher** than the installed one is installed. The file is checked (signature, checksum, product, firmware image) before anything is written.
If the power fails during the writing, the adapter does not start the incomplete firmware: the LED gives **two short flashes and a pause**,
the Amiga stays in reset. Plug the drive in and switch on again.

### UPDATE.TXT

```
Amiga_Full_USB_Keyboard - firmware update report

File: kb_firm_1.1.1.fw
Update successful. Current version is 1.1.1
Previous version: 1.1.0
```

Other texts: `Firmware file not found...` (no `kb_firm_*` file in the root folder), `Update NOT installed: the file version is not newer than the installed one`,
`signature check failed`, `the file is damaged`, `the file is for another device`, `can not read the file`, `writing to flash failed`.

### LED codes

| LED | Meaning |
|---|---|
| even slow blinking | the firmware is running, no keyboard connected |
| fast blinking, a few seconds | update in progress |
| 3 long flashes | updated |
| 10 fast flashes | not updated / no file on the drive |
| 2 short flashes and a pause | no firmware in the adapter, waiting for a drive |

## Limits

- Plug the drive in **before** switching on. A drive plugged into a running adapter is not read.
- The drive must be plugged **directly** into the adapter, not into a hub or into a keyboard hub.
- The drive is powered by the adapter: use a small one without lights. No hard disks.
- Firmware size is limited to 64 KB (the current one is 35 KB).
- The bootloader itself can only be replaced through an ST-LINK.
- There is no way back to an older version from a USB drive (the version must go up).

## Problems

| Symptom | What to do |
|---|---|
| Nothing happens, no `UPDATE.TXT` | the drive is exFAT/NTFS, or it is not recognised: reformat as FAT32 or try another drive; plug it in before switching on; plug it directly |
| 10 fast flashes | read `UPDATE.TXT` |
| Two short flashes and a pause | no firmware in the adapter: plug in the drive with `kb_firm_*.fw` and switch on |
| Keyboard does not work | tell me the keyboard model in an issue |
