# HUAWEI MateBook D14 2020 Hackintosh EFI

OpenCore EFI for HUAWEI MateBook D14 2020.

This repository contains a cleaned EFI copy prepared from `/Volumes/EFI/EFI`.
Machine-unique SMBIOS values have been removed from `EFI/OC/config.plist`.
Before using this EFI, generate your own values and replace:

- `PlatformInfo -> Generic -> SystemSerialNumber`
- `PlatformInfo -> Generic -> MLB`
- `PlatformInfo -> Generic -> SystemUUID`
- `PlatformInfo -> Generic -> ROM`

## Current Status

Configured or fixed in this EFI:

- OpenCore boot with `BOOTx64.efi` and `OpenCore.efi`.
- Intel iGPU support through WhateverGreen.
- Audio support through AppleALC and VerbStub.
- Battery status through SMCBatteryManager.
- Keyboard, trackpad, and I2C HID input through VoodooPS2Controller, VoodooI2C, and VoodooI2CHID.
- USB mapping through USBToolBox, UTBMap, USBMap, and related SSDTs.
- Intel Wi-Fi through AirportItlwm.
- Intel Bluetooth through IntelBluetoothFirmware, IntelBTPatcher, and BlueToolFixup.
- NVMe fixes through NVMeFix.
- CPU power management through CPUFriend, CPUFriendDataProvider, and SSDT-PLUG.
- Disabled unsupported discrete GPU through SSDT-dGPU-Off.
- Sleep/hibernation repair is being tested with HibernationFixup.

Not fixed or still needs verification:

- Fingerprint reader and Touch ID are not supported.
- AirDrop, Handoff, Apple Watch unlock, and other Continuity features are limited with Intel Wi-Fi.
- Sleep, wake, and hibernation still need longer real-world testing.
- HDMI or external display output needs verification.
- SD card reader support needs verification.
- DRM playback, Sidecar, and other Apple ecosystem features need verification.
- Built-in camera and microphone status should be confirmed on the target machine.

## Notes

- The uploaded `config.plist` is intentionally sanitized and is not ready to boot until SMBIOS values are regenerated.
- Old config backups, boot logs, zip archives, Spotlight files, trash folders, and AppleDouble metadata are not included.
- Keep a known-good EFI backup before replacing the EFI partition.
