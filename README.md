# Dell Precision 7740 OpenCore EFI

> OpenCore 引导的 Dell Precision 7740 黑苹果 EFI，基于 macOS Sonoma。  
> **三码已清除，使用前请自行生成并填入 `config.plist`。**

## ⚠️ 重要提醒

**所有三码（Serial Number / MLB / System UUID）已替换为占位值，使用前务必自行生成！**

生成工具：[GenSMBIOS](https://github.com/corpnewt/GenSMBIOS)

```
./GenSMBIOS MacBookPro16,4
```

将生成的值填入 `EFI/OC/config.plist` → `PlatformInfo` → `Generic`：
- `SystemSerialNumber`
- `MLB`
- `SystemUUID`

## 硬件配置

| 项目 | 规格 |
|------|------|
| 机型 | Dell Precision 7740 移动工作站 |
| CPU | Intel Core i7-9750H (Coffee Lake, 6C12T, 2.6–4.5 GHz) |
| 内存 | 32GB DDR4 |
| iGPU | Intel UHD Graphics 630 |
| dGPU | AMD Radeon Pro WX7130 8GB ( Ellesmere, Polaris 10 ) |
| 显卡模式 | 混合显卡 (iGPU + dGPU 共存) |
| 音频 | Realtek ALC289 |
| Wi-Fi | Intel Wireless (AirportItlwm) |
| 蓝牙 | Intel Bluetooth |
| 触摸板 | I2C 触摸板 (VoodooI2C) |
| SMBIOS | MacBookPro16,4 |

## 功能状态

| 功能 | 状态 | 备注 |
|------|:----:|------|
| 混合显卡 (iGPU + WX7130) | ✅ | iGPU 负责 UI/日常，dGPU 按需加载 |
| S3 睡眠唤醒 | ✅ | 关盖休眠实测 2 天后正常唤醒 |
| 有线网络 (Intel I219) | ✅ | IntelMausi |
| Wi-Fi | ✅ | AirportItlwm 2.3.0 |
| 蓝牙 | ✅ | IntelBluetoothFirmware + BlueToolFixup |
| 音频 (内置扬声器 + 耳机) | ✅ | AppleALC |
| 摄像头 | ✅ | |
| I2C 触摸板 (手势/多点触控) | ✅ | VoodooI2C + VoodooI2CHID |
| 触摸板物理按键 (上下两排) | ✅ | |
| USB 定制映射 | ✅ | USBToolBox + UTBMap |
| SD 读卡器 | ✅ | RealtekCardReader + RealtekCardReaderFriend |
| 键盘快捷键 (亮度/音量) | ✅ | BrightnessKeys |
| NVMe 电源管理 | ✅ | NVMeFix |
| 休眠修复 | ✅ | HibernationFixup |
| 传感器 (温度/风扇/电池) | ✅ | VirtualSMC + SMCDellSensors + SMCProcessor |
| Thunderbolt | ⚠️ | 未测试 |
| HDMI/DP 外接显示 | ⚠️ | 未测试 |

## OpenCore 配置概要

| 项目 | 值 |
|------|-----|
| SMBIOS | MacBookPro16,4 |
| PickerMode | External |
| SecureBootModel | Default |
| ProvideCurrentCpuInfo | false |
| ScanPolicy | 0 |

## Kexts (34)

### 核心
| Kext | 版本 | 用途 |
|------|------|------|
| Lilu | 1.7.2 | 核心补丁框架 |
| VirtualSMC | 1.3.8 | SMC 仿真 |
| WhateverGreen | 1.7.1 | 显卡补丁 |
| AppleALC | 1.9.7 | 音频 |

### 网络
| Kext | 版本 | 用途 |
|------|------|------|
| AirportItlwm | 2.3.0 | Intel Wi-Fi |
| AirportBrcmFixup | — | Wi-Fi 补丁 |
| IntelBluetoothFirmware | 2.4.0 | Intel BT 固件上传 |
| IntelBluetoothInjector | — | Intel BT 注入 |
| IntelBTPatcher | — | Intel BT 补丁 |
| BlueToolFixup | — | Sonoma BT 修复 |
| BrcmPatchRAM3 | — | BT RAM 补丁 |
| BrcmFirmwareData | — | BT 固件数据 |
| IntelMausi | — | Intel I219 有线网络 |

### 传感器
| Kext | 版本 | 用途 |
|------|------|------|
| SMCSuperIO | — | 主板传感器 |
| SMCProcessor | 1.3.8 | CPU 温度 |
| SMCDellSensors | 1.3.8 | Dell 专用传感器 |
| SMCBatteryManager | — | 电池状态 |
| RadeonSensor | — | AMD GPU 温度 |

### 输入
| Kext | 版本 | 用途 |
|------|------|------|
| VoodooI2C | 2.9.1 | I2C 触摸板主驱动 |
| VoodooI2CHID | — | I2C HID 协议 |
| VoodooPS2Controller | — | PS/2 键盘/触控板/Trackpad |
| AlpsHID | — | Alps HID 设备 |
| BrightnessKeys | — | 亮度快捷键 |

### 存储 & 电源
| Kext | 版本 | 用途 |
|------|------|------|
| NVMeFix | — | NVMe 电源管理 |
| CPUFriend | — | CPU 电源管理 |
| CPUFriendDataProvider | — | CPU 频率配置 |
| HibernationFixup | 1.5.4 | 休眠修复 |
| CpuTscSync | — | CPU TSC 同步 |

### USB
| Kext | 版本 | 用途 |
|------|------|------|
| USBToolBox | 1.1.1 | USB 定制映射 |
| UTBMap | — | USB 端口映射数据 |

### 其他
| Kext | 版本 | 用途 |
|------|------|------|
| RealtekCardReader | — | SD 读卡器 |
| RealtekCardReaderFriend | — | 读卡器电源管理 |
| AGPMInjector | — | GPU 电源管理注入 |
| XHCI-unsupported | — | XHCI 控制器支持 |

## ACPI (38 SSDTs)

关键自定义 SSDT：
- `SSDT-dGPU-iGPU-WX7130` — WX7130 混合显卡模式
- `SSDT-15-OCWork-dell` — Dell 专用补丁
- `SSDT-16-RMCF-OnOff-Trackpad` — 触摸板按键
- `SSDT-14-LIDpatch` — 关盖唤醒
- `SSDT-13-PTSWAK` / `SSDT-PTSWAK` — 休眠唤醒补丁
- `SSDT-06-PNLF-CFL` — Coffee Lake 背光
- `SSDT-XCPM` — CPU 电源管理
- `SSDT-USBX` — USB 电源属性

## 使用方法

1. 下载本仓库 ZIP 或 `git clone`
2. **生成三码并填入 `config.plist`**（见上方提醒）
3. 将 `EFI` 文件夹复制到 EFI 分区根目录
4. 重启引导

### 生成三码

```bash
# 安装 GenSMBIOS
git clone https://github.com/corpnewt/GenSMBIOS
cd GenSMBIOS
./GenSMBIOS MacBookPro16,4

# 将输出的 Serial / MLB / UUID 填入 config.plist → PlatformInfo → Generic
```

## 适用系统

- macOS Sonoma (14.x)
- 理论兼容 macOS Ventura / Monterey（Coffee Lake i7-9750H）

## 致谢

- [Acidanthera](https://github.com/acidanthera) — OpenCore, Lilu, VirtualSMC, WhateverGreen, AppleALC 等
- [VoodooI2C](https://github.com/VoodooI2C) — I2C 触摸板驱动
- [USBToolBox](https://github.com/USBToolBox) — USB 定制映射
- [IntelBluetoothFirmware](https://github.com/OpenIntelWireless) — Intel 蓝牙固件
- [Dortania](https://dortania.github.io) — OpenCore 安装指南

## License

MIT

## 声明

本 EFI 基于个人设备 (Dell Precision 7740, i7-9750H, WX7130) 调优。不同批次/配置的机器可能需要微调 SSDT 和 config.plist。仅供学习参考，使用风险自负。
