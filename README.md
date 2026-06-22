# Dell Precision 7740 OpenCore EFI

近完美黑苹果 EFI，适用于 Dell Precision 7740 移动工作站。

## 硬件配置

| 项目 | 规格 |
|------|------|
| CPU | Intel Core i7-9750H (Coffee Lake) |
| 内存 | 32GB DDR4 |
| dGPU | AMD Radeon Pro WX7130 8GB |
| 显卡模式 | 混合显卡 (iGPU + dGPU) |
| Thunderbolt | 未测试 |

## 功能状态

| 功能 | 状态 | 备注 |
|------|------|------|
| 混合显卡 | ✅ 完美 | iGPU + WX7130 共存 |
| S3 睡眠 | ✅ 完美 | 关盖休眠，实测2天后唤醒正常 |
| 有线网络 | ✅ 完美 | |
| Wi-Fi | ✅ 完美 | Intel 无线网卡 + AirportItlwm |
| 蓝牙 | ✅ 完美 | |
| 声音 | ✅ 完美 | |
| 摄像头 | ✅ 完美 | |
| 触摸板 | ✅ 完美 | VoodooI2C + 双排按键均正常 |
| USB | ✅ 完美 | USBToolBox 定制映射 |
| 读卡器 | ✅ 完美 | Realtek |
| 雷电 | ⚠️ 未测试 | |

## 引导器

- **OpenCore** — EFI 位于 `EFI/OC/` 下
- 使用 `BOOTx64.efi` (OpenCore 伪装为 Microsoft Boot Manager)

## Kexts (34)

主要 kexts：
- **Lilu** + **VirtualSMC** 系列 (传感器/电池/处理器)
- **WhateverGreen** (显卡)
- **AppleALC** (音频)
- **VoodooI2C** + **VoodooI2CHID** (触摸板)
- **AirportItlwm** + IntelBT 系列 (Wi-Fi/蓝牙)
- **HibernationFixup** (休眠)
- **NVMeFix** (NVMe 电源管理)
- **USBToolBox** + **UTBMap** (USB 定制映射)
- **SMCDellSensors** (Dell 专用传感器)

## 使用方法

1. 下载本仓库 ZIP 或 clone
2. 将 `EFI` 文件夹复制到 EFI 分区根目录
3. 如需定制 USB 映射，编辑 `EFI/OC/Kexts/UTBMap.kext/Contents/Info.plist`

## 声明

本 EFI 基于个人设备调优，仅供学习参考。不同批次/配置的 Precision 7740 可能需要微调 SSDT 和 config.plist。
