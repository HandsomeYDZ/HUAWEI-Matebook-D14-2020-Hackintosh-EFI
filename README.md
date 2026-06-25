# HUAWEI MateBook D14 2020 Hackintosh EFI

[English](README-EN.md)

适用于 HUAWEI MateBook D14 2020 的 OpenCore EFI。

- OpenCore: `1.0.7`
- 测试系统：macOS Ventura `13.7.8`
- 笔记本型号：HUAWEI MateBook D14 2020
- CPU: i7-10510U
- GPU: UHD-620
- 屏幕：BOE 1920 x 1080

本仓库仅保留启动所需的 EFI 文件，可作为同型号机器的配置参考。

## 使用前必看

仓库中的 `EFI/OC/config.plist` 已经脱敏，以下 SMBIOS 唯一信息已替换为占位值：

- `PlatformInfo -> Generic -> SystemSerialNumber`
- `PlatformInfo -> Generic -> MLB`
- `PlatformInfo -> Generic -> SystemUUID`
- `PlatformInfo -> Generic -> ROM`

使用前请自己重新生成 SMBIOS，不要直接使用仓库里的占位值启动。

## BIOS 前置条件

当前这份 EFI 基于本机已经完成以下 BIOS 设置的前提整理：

- 已关闭 `CFG Lock`
- 已开启 `DVMT Pre-Allocated 64MB`

因为本机已经开启 DVMT 64MB，所以 `config.plist` 里没有再保留限制核显预分配显存的 framebuffer 参数。

如果你的机器没有关闭 `CFG Lock`，需要在 OpenCore 中开启：

- `Kernel -> Quirks -> AppleXcpmCfgLock`

如果你的机器没有开启 `DVMT 64MB`，通常还需要自行补回合适的核显 framebuffer 参数。参考值如下：

- `framebuffer-fbmem`: `Data`, `00009000`，按 little-endian 计算为 9 MiB
- `framebuffer-stolenmem`: `Data`, `00003001`，按 little-endian 计算为 19 MiB

两者合计 28 MiB，小于 32 MiB。具体仍需按你的 BIOS 状态、核显平台 ID 和 WhateverGreen/OpenCore 配置方式调整。

## 已修复或工作正常

- 屏幕亮度调节正常。
- USB 正常。
- 浅睡眠正常，当前使用 `hibernatemode 0`。
- 合盖睡眠正常。
- 开盖唤醒正常。
- Wi-Fi 正常。
- 扬声器正常。
- 触控板正常。
- 蓝牙可用，但部分设备无法连接。
- 其他基础功能已随 EFI 配置完成，建议以实机测试为准。

## 未修复或不完美

- 磁盘睡眠恢复未修复，也就是深度休眠/写盘恢复仍不正常。
- 蓝牙不完美，部分设备可能无法连接。
- 开关机按键不完美，进入 macOS 后按电源键没有反应。
- AirDrop 残废，无法使用：手机看不到电脑，电脑即使能发现手机也无法正常发送。
- 指纹识别不可用。
- 其他未列出的功能请以实际测试为准。

## 注意事项

- 替换 EFI 前请先备份你当前可正常启动的 EFI。
- 这份 EFI 不保证适用于所有同型号不同批次机器。
- 如果你没有做 BIOS 层面的 CFG Lock 和 DVMT 修改，请先阅读上面的 BIOS 前置条件。
- 更新 macOS、OpenCore 或 kext 前，建议先保留一份可回滚的启动盘。
