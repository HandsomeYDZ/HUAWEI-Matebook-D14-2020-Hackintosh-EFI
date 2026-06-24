# HUAWEI MateBook D14 2020 Hackintosh EFI

适用于 HUAWEI MateBook D14 2020 的 OpenCore EFI。

OpenCore EFI for HUAWEI MateBook D14 2020.

- OpenCore: `1.0.7`
- Tested macOS: Ventura `13.7.8`
- Laptop model: HUAWEI MateBook D14 2020
- CPU: i7-10510U
- GPU: UHD-620
- Screen: BOE 1920 x 1080

本仓库仅保留启动所需的 EFI 文件，可作为同型号机器的配置参考。

This repository keeps only the EFI files needed for booting and can be used as a reference for the same laptop model.

## 使用前必看 / Before You Use

仓库中的 `EFI/OC/config.plist` 已经脱敏，以下 SMBIOS 唯一信息已替换为占位值：

The `EFI/OC/config.plist` in this repository is sanitized. The following machine-unique SMBIOS values were replaced with placeholders:

- `PlatformInfo -> Generic -> SystemSerialNumber`
- `PlatformInfo -> Generic -> MLB`
- `PlatformInfo -> Generic -> SystemUUID`
- `PlatformInfo -> Generic -> ROM`

使用前请自己重新生成 SMBIOS，不要直接使用仓库里的占位值启动。

Generate your own SMBIOS values before booting. Do not boot directly with the placeholder values from this repository.

## BIOS 前置条件 / BIOS Prerequisites

当前这份 EFI 基于本机已经完成以下 BIOS 设置的前提整理：

This EFI is prepared for a machine with the following BIOS-level changes already applied:

- 已关闭 `CFG Lock` / `CFG Lock` is disabled
- 已开启 `DVMT Pre-Allocated 64MB` / `DVMT Pre-Allocated 64MB` is enabled

因为本机已经开启 DVMT 64MB，所以 `config.plist` 里没有再保留限制核显预分配显存的 framebuffer 参数。

Because DVMT 64MB is already enabled on this machine, this `config.plist` does not keep the framebuffer memory limit patches.

如果你的机器没有关闭 `CFG Lock`，需要在 OpenCore 中开启：

If `CFG Lock` is still enabled on your machine, enable this OpenCore quirk:

- `Kernel -> Quirks -> AppleXcpmCfgLock`

如果你的机器没有开启 `DVMT 64MB`，通常还需要自行补回合适的核显 framebuffer 参数，例如：

If `DVMT 64MB` is not enabled on your machine, you may need to add suitable iGPU framebuffer properties, such as:

- `framebuffer-stolenmem`
- `framebuffer-fbmem`

具体数值请按你的 BIOS 状态、核显平台 ID 和 WhateverGreen/OpenCore 配置方式调整。

The exact values depend on your BIOS settings, iGPU platform ID, and WhateverGreen/OpenCore configuration.

## 已修复或工作正常 / Working

- 屏幕亮度调节正常。 / Screen brightness control works.
- USB 正常。 / USB works.
- 浅睡眠正常，当前使用 `hibernatemode 0`。 / Shallow sleep works with `hibernatemode 0`.
- 合盖睡眠正常。 / Lid-close sleep works.
- 开盖唤醒正常。 / Lid-open wake works.
- Wi-Fi 正常。 / Wi-Fi works.
- 扬声器正常。 / Built-in speakers work.
- 触控板正常。 / Trackpad works.
- 蓝牙可用，但部分设备无法连接。 / Bluetooth works partially, but some devices cannot connect.
- 其他基础功能已随 EFI 配置完成，建议以实机测试为准。 / Other basic features are configured in the EFI, but real-machine testing is recommended.

## 未修复或不完美 / Not Fixed or Imperfect

- 磁盘睡眠恢复未修复，也就是深度休眠/写盘恢复仍不正常。 / Disk sleep restore is not fixed; deep hibernation or resume-from-disk still does not work properly.
- 蓝牙不完美，部分设备可能无法连接。 / Bluetooth is imperfect, and some devices may fail to connect.
- 开关机按键不完美，进入 macOS 后按电源键没有反应。 / The power button is imperfect; pressing it after entering macOS does nothing.
- AirDrop 之前测试可用，但目前不可用或不稳定，原因未确认。 / AirDrop worked in earlier testing, but it is currently unavailable or unstable for unknown reasons.
- 指纹识别不可用。 / Fingerprint reader is not supported.
- 其他未列出的功能请以实际测试为准。 / Any unlisted feature should be verified on the actual machine.

## 注意事项 / Notes

- 替换 EFI 前请先备份你当前可正常启动的 EFI。 / Back up your currently working EFI before replacing it.
- 这份 EFI 不保证适用于所有同型号不同批次机器。 / This EFI is not guaranteed to work on every hardware revision of the same model.
- 如果你没有做 BIOS 层面的 CFG Lock 和 DVMT 修改，请先阅读上面的 BIOS 前置条件。 / If you have not changed CFG Lock and DVMT in BIOS, read the BIOS prerequisites first.
- 更新 macOS、OpenCore 或 kext 前，建议先保留一份可回滚的启动盘。 / Before updating macOS, OpenCore, or kexts, keep a bootable fallback EFI.
