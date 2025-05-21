# 微星 B350M 迫击炮 黑苹果 OpenCore EFI

## 介绍

[![Static Badge](https://img.shields.io/badge/OpenCore-1.0.2-blue)](https://github.com/acidanthera/OpenCorePkg/releases) [![Static Badge](https://img.shields.io/badge/macOS-15-red)](https://www.apple.com.cn/macos/macos-sequoia/) ![GitHub last commit](https://img.shields.io/github/last-commit/VenenoSix24/MSI-B350M-MORTAR-Hackintosh-OpenCore1.0.2-EFI) ![GitHub License](https://img.shields.io/github/license/VenenoSix24/MSI-B350M-MORTAR-Hackintosh-OpenCore1.0.2-EFI) [![Static Badge](https://img.shields.io/badge/Find%20me-Blog-orange?link=blog.776624.xyz)](https://blog.776624.xyz/)

### 前言

本 EFI 适用于 微星 B350M 迫击炮 主板用户，理论上采用 Ryzen 系 CPU 和 Navi 核心的 GPU 均可使用 ，其他配置根据实际情况稍微修改也可使用

### 版本

OpenCore 版本为 `1.0.2` ，BIOS 版本为 `7A37v1O7`

机型为 `MacPro7,1` ，最高支持 `macOS Sequoia 15.4`

### 关于本机

<img src="https://s2.loli.net/2024/10/22/CfnAZWq1t2KN7dP.jpg" alt="about.png" style="zoom:50%;" />

## 配置

|  硬件  | 型号                                   |
| :----: | :------------------------------------- |
|  主板  | 微星 B350M MORTAR                      |
| 处理器 | AMD Ryzen™ 5 5600                     |
|  显卡  | AMD Radeon RX 6750 GRE 12GB （蓝宝石） |
|  内存  | 玖合 星舞 32G 3200MHz DDR4             |
|  硬盘  | 朗科 SSD NV3000 256G                   |

## 实现功能

- [X] 声卡 (板载) / 网卡 (板载)
- [X] 显卡正常驱动
- [X] ~~USB 定制~~ (当前这版好像有点bug，过两天修复)
- [X] ~~可睡眠 可唤醒~~ (同上)
- [X] 硬解 4K H.264  HEVC
- [X] AppStore iCloud 正常登陆
- [ ] Apple Music / Apple TV
- [ ] 与蓝牙 WIFI 有关的功能暂未测试 （板载无网卡）

## BIOS 设置

|   **选项**   | **状态** |
| :----------------: | :-------------: |
|     SATA Mode     |    选择 AHCI    |
| Above 4G Decoding | 禁用 / Disabled |
| EHCI/XHCI Hand-off | 启用 / Enabled |
|        SVM        | 启用 / Enabled |
|        CSM        | 禁用 / Disabled |
|    Secure Boot    | 禁用 / Disabled |
|    Serial Port    | 禁用 / Disabled |
|   Parallel Port   | 禁用 / Disabled |

如果开启 **Above 4G Decoding** ，**必须**把配置文件 `boot-args` 项中的 `npci=0x3000` 参数删除

推荐主板选择关闭，使用 `npci=0x3000` 参数，二选一即可。

## 使用方法

详细过程参考 **OpenCore文档** ***[官方](https://dortania.github.io/OpenCore-Install-Guide/)***  ***[中文](https://sumingyd.github.io/OpenCore-Install-Guide/)*** / [**国光的黑苹果安装教程**](https://apple.sqlsec.com/) / **[精解OpenCore - 黑果小兵](https://blog.daliansky.net/OpenCore-BootLoader.html)**

1. 下载 EFI 文件
2. 修改 BIOS 设置
3. 修改 `config.plist` 文件

   i. 修改 CPU 核心数

   - 在你的配置文件中转到 `Kernel -> Patch` 找到四个 `algrey - Force cpuid_cores_per_package` 补丁。
   - 修改这些补丁以适配你的 CPU 核心。将这些补丁中的第一对更改为下**表**中的值。
     - 例如，对于具有 6 核的 Ryzen 5 5600，三个修改后的补丁应如下所示：
       - B8 **00** 0000 0000 -> B8 **06** 0000 0000
       - BA **00** 0000 0000 -> BA **06** 0000 0000
       - BA **00** 0000 0090 -> BA **06** 0000 0090
       - BA **00** 0000 00     -> BA **06** 0000 00

   | **CPU 核心** | **十六进制值** |
   | :----------------: | :------------------: |
   |        4 核        |        `04`        |
   |        6 核        |        `06`        |
   |        8 核        |        `08`        |
   |       12 核       |        `0C`        |
   |       16 核       |        `10`        |
   |       24 核       |        `18`        |
   |       32 核       |        `20`        |

   ii. 生成三码，并校验 序列号 在官网是否存在

       使用[GenSMBIOS](https://github.com/corpnewt/GenSMBIOS) 工具生成三码
4. 按照正常流程继续引导即可

## 进阶教程

### 1. 睡眠

首先，测试你的 睡眠 功能是否正常。如果正常，你可以跳过阅读此部分。

如果你有睡眠问题，请定制你的USB端口，定制方法 [**参考这里**](https://apple.sqlsec.com/6-%E5%AE%9E%E7%94%A8%E5%A7%BF%E5%8A%BF/6-1/)。

如果上述方法无效的话，请参考 [**这篇文章**](https://dortania.github.io/OpenCore-Post-Install/universal/sleep.html) 以修复睡眠。

### 2. 开启 HiDPi

使用 **[one-key-hidpi](https://github.com/xzhih/one-key-hidpi)** 项目即可。

1. 一键脚本（拥有良好的网络环境）

   打开终端输入下方命令，即可开启 HiDPi：

   ```
   sh -c "$(curl -fsSL https://raw.githubusercontent.com/xzhih/one-key-hidpi/master/hidpi.sh)"
   ```
2. 本地文件

   克隆 / 下载 **[one-key-hidpi](https://github.com/xzhih/one-key-hidpi)** 项目文件到本地后，解压，双击打开 `hidpi.command`

之后根据实际情况，输入数字选择分辨率重启即可。如未生效自行去设置更改带有 **HiDPi** 的分辨率

### 3. PAT 补丁

|    **Shaneee's**    |   **Algrey's**   |
| :------------------------: | :--------------------: |
|      更好的 GPU 性能      |    更差的 GPU 性能    |
|  可能不适用于 NVIDIA GPU  |      兼容所有 GPU      |
| HDMI / DP 音频可能无法工作 | HDMI / DP 音频正常工作 |
|          默认启用          |        默认禁用        |

本 EFI 默认启用 `Shaneee` 的 `macOS Sequoia 15` PAT 补丁，以发挥更好的 GPU 性能，减少日常使用的掉帧现象。

如需切换请打开 `config.plist` 转到 `Kernel` 中的 `Patch 补丁` 搜索 `mtrr_update_action` 启用/禁用相关 PAT 。

不要同时开启两个 PAT 补丁，因为这样会不起作用。

### 4. 如何使用 .sh 文件

后续两个步骤会用到 shell 命令文件，请参考 **[方法](https://www.jianshu.com/p/e777b6825df5)**

### 5. Adobe 修复

由于缺少 intel_fast_memset 指令，Adobe 应用程序在 AMD 黑苹果上不能正常使用。

你可以运行 **[这个脚本](https://github.com/mikigal/ryzen-hackintosh/blob/master/Resources/adobe_patch.sh)** 来解决，重启系统以使之生效。

### 6. MKL 补丁

有些 macOS 应用程序使用 MKL - 数学核心函数库。但它无法在 AMD CPU 上原生运行

所以我们需要用 **[这个脚本](https://github.com/mikigal/ryzen-hackintosh/blob/master/Resources/ryzen_patch.sh)** 来修补它。

### 7. 修改 CPU 名称

本 EFI 已添加名称修改参数，可直接修改，重启在 OpenCore 引导界面 `Reset NVRAM` 后生效。

打开配置文件转到 `NVRAM -> 4D1FDA02-38C7-4A6A-9CC6-4BCCA8B30102 -> AMD Ryzen™ 5 5600`

将 `AMD Ryzen™ 5 5600` 修改为你想要的名称即可。

## 预览

![desktop.png](https://s2.loli.net/2024/10/22/egLoVsbrFHfuXan.jpg)

## 所需资源

### Plist 文件编辑工具

- [ProperTree](https://github.com/corpnewt/ProperTree)
- [OCAuxiliaryTools](https://github.com/ic005k/OCAuxiliaryTools)
- [OpenCore Configurator](https://mackie100projects.altervista.org/opencore-configurator/)

### 三码生成工具

- **[GenSMBIOS](https://github.com/corpnewt/GenSMBIOS)**

## 鸣谢

> 非常感谢你们的付出！

- [国光酱](https://apple.sqlsec.com/)
- [黑果小兵](https://blog.daliansky.net/)
- [OpenCore](https://github.com/acidanthera/OpenCorePkg)
- [Hackintool](https://github.com/benbaker76/Hackintool)
- [ProperTree](https://github.com/corpnewt/ProperTree)
- [AMD_Vanilla](https://github.com/AMD-OSX/AMD_Vanilla)
- [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS)
- [one-key-hidpi](https://github.com/xzhih/one-key-hidpi)
- [ryzen-hackintosh](https://github.com/mikigal/ryzen-hackintosh)
- [OCAuxiliaryTools](https://github.com/ic005k/OCAuxiliaryTools)
- [OpenCore Configurator](https://mackie100projects.altervista.org/opencore-configurator/)
- [OpenCore Auxiliary Tools](https://github.com/ic005k/QtOpenCoreConfig)
- [OpenCore Legacy Patcher](https://github.com/dortania/OpenCore-Legacy-Patcher)
