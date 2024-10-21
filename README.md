# 微星 B350M 迫击炮 黑苹果 OpenCore EFI

## 介绍

[![Static Badge](https://img.shields.io/badge/OpenCore-1.0.2-blue)](https://github.com/acidanthera/OpenCorePkg/releases)[![Static Badge](https://img.shields.io/badge/macOS-15-red)](https://www.apple.com.cn/macos/macos-sequoia/)

本 EFI 适用于 微星 B350M 迫击炮 主板用户，理论上采用 Ryzen 系 CPU 和 Navi 核心的 GPU 均可使用 ，其他配置根据实际情况稍微修改也可使用

所使用的 OpenCore 版本为 `1.0.2` ，BIOS 版本为 `7A37v1O7` ，机型为 `MacPro7,1` ，最高支持 `macOS Sequoia 15` 

## 配置

|  硬件  |                  型号                  |
| :----: | :------------------------------------: |
|  主板  |           微星 B350M MORTAR            |
| 处理器 |           AMD Ryzen™ 5 5600            |
|  显卡  | AMD Radeon RX 6750 GRE 12GB （蓝宝石） |
|  内存  |       玖合 星舞 32G 3200MHz DDR4       |
|  硬盘  |          朗科 SSD NV3000 256G          |

## BIOS

|      **选项**      | **状态** |
| :----------------: | :------: |
|     SATA Mode      |   AHCI   |
| Above 4G Decoding  | Enabled  |
| EHCI/XHCI Hand-off | Enabled  |
|        SVM         | Enabled  |
|        CSM         | Disabled |
|    Secure Boot     | Disabled |
|    Serial Port     | Disabled |
|   Parallel Port    | Disabled |

## 实现功能

- [x]  声卡 (板载) / 网卡 (板载)
- [x] 显卡正常驱动
- [x] USB 定制
- [x] 硬解 4K H.264  HEVC
- [x] 可睡眠 可唤醒
- [x] AppStore iCloud 正常登陆
- [x]  Apple Music / Apple TV
- [ ] 与蓝牙 WIFI 有关的功能暂未测试 （板载无网卡）

## 使用方法

1. 下载 EFI 文件

2. 修改 BIOS 设置

3. 修改 `config.plist` 文件

   i. 修改 CPU 核心数

   ii. 生成三码，并校验 序列号 在官网是否存在

4. 按照正常流程继续引导即可

## 预览



## 相关链接

## 鸣谢

- [黑果小兵](https://blog.daliansky.net/)
- [Hackintool](https://github.com/benbaker76/Hackintool)
- [OpenCore](https://github.com/acidanthera/OpenCorePkg)
- [OpenCore Auxiliary Tools](https://github.com/ic005k/QtOpenCoreConfig)
- [OpenCore Legacy Patcher](https://github.com/dortania/OpenCore-Legacy-Patcher)

