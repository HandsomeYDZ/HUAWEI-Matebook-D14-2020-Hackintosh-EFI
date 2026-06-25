# HUAWEI MateBook D14 2020 Hackintosh EFI

[中文](README.md)

OpenCore EFI for HUAWEI MateBook D14 2020.

- OpenCore: `1.0.7`
- Tested macOS: Ventura `13.7.8`
- Laptop model: HUAWEI MateBook D14 2020
- CPU: i7-10510U
- GPU: UHD-620
- Screen: BOE 1920 x 1080

This repository keeps only the EFI files needed for booting and can be used as a reference for the same laptop model.

## Before You Use

The `EFI/OC/config.plist` in this repository is sanitized. The following machine-unique SMBIOS values were replaced with placeholders:

- `PlatformInfo -> Generic -> SystemSerialNumber`
- `PlatformInfo -> Generic -> MLB`
- `PlatformInfo -> Generic -> SystemUUID`
- `PlatformInfo -> Generic -> ROM`

Generate your own SMBIOS values before booting. Do not boot directly with the placeholder values from this repository.

## BIOS Prerequisites

This EFI is prepared for a machine with the following BIOS-level changes already applied:

- `CFG Lock` is disabled
- `DVMT Pre-Allocated 64MB` is enabled

Because DVMT 64MB is already enabled on this machine, this `config.plist` does not keep the framebuffer memory limit patches.

If `CFG Lock` is still enabled on your machine, enable this OpenCore quirk:

- `Kernel -> Quirks -> AppleXcpmCfgLock`

If `DVMT 64MB` is not enabled on your machine, you may need to add suitable iGPU framebuffer properties. Reference values:

- `framebuffer-fbmem`: `Data`, `00009000`, interpreted as 9 MiB in little-endian
- `framebuffer-stolenmem`: `Data`, `00003001`, interpreted as 19 MiB in little-endian

Together they use 28 MiB, which is below 32 MiB. The exact values may still need adjustment based on your BIOS settings, iGPU platform ID, and WhateverGreen/OpenCore configuration.

## Working

- Screen brightness control works.
- USB works.
- Shallow sleep works with `hibernatemode 0`.
- Lid-close sleep works.
- Lid-open wake works.
- Wi-Fi works.
- Built-in speakers work.
- Trackpad works.
- Bluetooth works partially, but some devices cannot connect.
- Other basic features are configured in the EFI, but real-machine testing is recommended.

## Not Fixed or Imperfect

- Disk sleep restore is not fixed; deep hibernation or resume-from-disk still does not work properly.
- Bluetooth is imperfect, and some devices may fail to connect.
- The power button is imperfect; pressing it after entering macOS does nothing.
- AirDrop is unusable: the phone cannot see the laptop, and sending from the laptop to the phone does not work.
- Fingerprint reader is not supported.
- Any unlisted feature should be verified on the actual machine.

## Notes

- Back up your currently working EFI before replacing it.
- This EFI is not guaranteed to work on every hardware revision of the same model.
- If you have not changed CFG Lock and DVMT in BIOS, read the BIOS prerequisites first.
- Before updating macOS, OpenCore, or kexts, keep a bootable fallback EFI.
