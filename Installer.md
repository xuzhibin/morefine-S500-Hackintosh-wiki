# Monterey安装教程

> 
>
> 喝着现磨的咖啡，整理下思绪，写下全新的`Monterey`安装教程吧。

## 安装前准备

以前的安装教程都是只写教程本身的操作，没有往外延伸。

现在都已经是2021年了，全新的`Monterey`已经发布，无论是硬件还是`macOS`系统本身，已经有了翻天覆地的变化。

### 硬件准备：

在使用`macOS`之前，需要先了解下硬件都有哪些限制，也就是哪些硬件是被支持的，哪些是不被支持的。

#### 电脑配置

|   规格    |                           详细信息                           |
| :-------: | :----------------------------------------------------------: |
| 电脑型号  |                        morefine S500                         |
| 操作系统  |                 macOS `Monterey` / `Big Sur`                 |
|  处理器   |               英特尔 酷睿 i9-10880H 8核16线程                |
|   内存    |                      32 GB DDR4 2933MHz                      |
|  硬盘1/2  |            支持双NVMe或NVMe+SATA SSD或双SATA SSD             |
|  硬盘/3   |                    可接SATA 2.5寸硬盘/SSD                    |
|   显卡    |                    Intel UHD Graphics 630                    |
|  显示器   |                              无                              |
|   声卡    |                   Realtek ALC662 `alcid=5`                   |
| 无线网卡  | m.2 NGFF插槽，默认出厂为 `Intel AX200` 已更换为[BCM94360Z3](https://blog.daliansky.net/uploads/WeChatandShop.png) |
| 有线网卡1 |   **Realtek RTL8168H/8111H PCI Express Gigabit Ethernet**    |
| 有线网卡2 |   **Realtek RTL8168H/8111H PCI Express Gigabit Ethernet**    |

#### 固态硬盘

在大多数情况下，所有基于SATA的驱动器均受支持，大多数NVMe驱动器也受支持。只有少数例外：

- 三星PM981(a) / PM991和美光2200S NVMe SSD
  - 这些固态硬盘不兼容（导致内核[崩溃](https://github.com/acidanthera/NVMeFix/releases)），因此需要[NVMeFix.kext](https://github.com/acidanthera/NVMeFix/releases)来修复这些内核[崩溃](https://github.com/acidanthera/NVMeFix/releases)。请注意，即使使用`NVMeFix.kext`，这些驱动器仍可能会导致启动问题。
  - 与此相关的是，三星970 EVO Plus NVMe SSD也有同样的问题，但已在固件更新中得到修复。可在[此处](https://www.samsung.com/semiconductor/minisite/ssd/download/tools/)获取固件更新（通过Samsung Magician或可启动ISO的Windows）。
  - 还要注意，macOS不支持使用[Intel傲腾(Optane Memory)](https://www.intel.com/content/www/us/en/architecture-and-technology/optane-memory.html)或[Micron 3D XPoint](https://www.micron.com/products/advanced-solutions/3d-xpoint-technology)进行HDD加速的笔记本电脑。一些用户报告说在Catalina取得了成功，甚至具有读写支持，但我们强烈建议您卸下驱动器以防止任何潜在的启动问题。

#### 无线网卡

支持的m.2 NGFF无线网卡：

- 博通：

  绝大多数的博通(Boardcom)可以得到免驱或者通过添加驱动得到支持；

- INTEL：

  感谢[@zxystd](https://github.com/zxystd)团队开发的[OpenIntelWireless](https://openintelwireless.github.io/General/Installation.html)

### 软件准备

#### 操作系统：

一个可以制作安装U盘的操作系统，包括但不限于`macOS` / `Windows` / `Linux`等

比如：

- 运行`macOS`的苹果电脑；
- 运行`Windows`或者`PE`的电脑；
- 基于`Live CD`模式运行的`Linux`系统等等；

#### 软件或者用到的工具：

##### md5检查器：

- Windows:
  - [WinMD5](https://www.winmd5.com/)
- macOS或者Linux自带：
  - `md5` for macOS
  - `md5sum` for linux

##### 磁盘分区工具

- Windows:
  - [Disk Genuis](https://www.diskgenius.cn/)
- macOS或者Linux：
  - 略

##### U盘制作工具

- [etcher](http://etcher.io/)
- [transmac](https://www.acutesystems.com/scrtm.htm)

#### 创建USB安装盘

##### 下载安装镜像

- 本站下载：[请点击前往](https://blog.daliansky.net/categories/%E4%B8%8B%E8%BD%BD/%E9%95%9C%E5%83%8F/)

##### 校验`md5`值

- `Windows`环境：

  利用刚才下载的[WinMD5](https://www.winmd5.com/)检查md5值是否正确，如果md5值不相同**必须重新下载安装镜像，不要心存侥幸** 

  ![WinMD5](https://images.daliansky.net/d/YmBXVA8q/blog/BigSur/WinMD5.png?download=1)

- `macOS`环境：

  ```bash
  # md5 macOS\ Monterey\ 12.0.1\ 21A559\ Installer\ for\ morefine\ S500\ 11-15-2021.dmg
  MD5 (macOS Monterey 12.0.1 21A559 Installer for morefine S500 11-15-2021.dmg) = f16ec7f118da22c66b9f0a46a1cd8c12
  ```

  

##### 将安装镜像写到`USB`上（制作安装镜像）

- 镜像制作：

    - 下载[balenaEtcher](https://etcher.io)，选择安装镜像，选择需要制作的U盘，点击 `Flash` 即可。***Windows10需要以管理员权限运行***![etcher](https://images.daliansky.net/d/YmBXVA8q/blog/etcher.png?download=1)

#### 查找适合自己的`EFI`

- 本站：[Hackintosh黑苹果长期维护机型整理清单](https://blog.daliansky.net/Hackintosh-long-term-maintenance-model-checklist.html) 
- 其它：
  - 远景：http://bbs.pcbeta.com
  - tonymacx86:  https://www.tonymacx86.com
  - insanelymac: [insanelymac.com](https://www.insanelymac.com/) 
  - 谷歌: https://www.google.com

#### 替换USB安装盘里的`EFI`

如果USB安装盘自带的EFI无法完成安装或者安装后不完美，那么就需要执行替换EFI的操作

- 操作过程：（略）

## 安装`Monterey`

### `BIOS` 设置

以 `morefine S500` 为例图解

- 进入 `BIOS`

  - 打开电源，按键盘的 `DEL` 键进入 `BIOS`
    ![morefine S500 BIOS Setup-0001](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/BIOS/BIOS-Setup-0001.png)
    ![morefine S500 BIOS Setup-0002](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/BIOS/BIOS-Setup-0002.png)

  #### 禁用 `Secure Boot`

  - 进入 `Security` - `Secure Boot` 选单![BIOS-Setup-0012-0](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/BIOS/BIOS-Setup-0012-0.png)
  - 将 `Secire Bppt` 的状态由 `Enabled` 修改为 `Disabled`![BIOS-Setup-0012](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/BIOS/BIOS-Setup-0012.png)

  #### 关闭 `CFG Lock`

  - 进入 `Advanced` - `Power & Performance` 选单

    ![BIOS-Setup-0003](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/BIOS/BIOS-Setup-0003.png)

  - 进入 `CPU - Power Management Control` 选单

    ![BIOS-Setup-0004](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/BIOS/BIOS-Setup-0004.png)

  - 光标移动到最后一行 `CPU Lock Configuration`  选单

    ![BIOS-Setup-0005](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/BIOS/BIOS-Setup-0005.png)

  - 将 `CFG Lock` 的状态由 `Enabled` 修改为 `Disabled`

    ![BIOS-Setup-0006](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/BIOS/BIOS-Setup-0006.png)

    ![BIOS-Setup-0007](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/BIOS/BIOS-Setup-0007.png)

  - 按 `ESC` 键退回到主界面

  #### 修改 `DVMT Pre-Allocated` 为 `64MB` 

  修改 `DVMT Pre-Allocated` 为 `64MB` ，以便支持 `4K@60Hz` 显示模式

  - 进入 `Chipset` - `System Agent (SA) Configuration` 选单![BIOS-Setup-0008](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/BIOS/BIOS-Setup-0008.png)

  - 进入 `Graphics Configuration` 选单![BIOS-Setup-0009](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/BIOS/BIOS-Setup-0009.png)

  - 光标移动到 `DVMT Pre-Allocated` ，将内存由 `32M` 修改为 `64M`![BIOS-Setup-0010](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/BIOS/BIOS-Setup-0010.png)

    ![BIOS-Setup-0011](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/BIOS/BIOS-Setup-0011.png)

  #### 调整 `UEFI` 引导选项

  如果单 `mscOS` 使用，该选项为非必须调整选项

  - 进入 `Boot` 选单

  - 进入 `Boot Option #1` ，将 `UEFI OS` 设置为最优先，否则默认会修改为 `Windows Boot Manager`

    ![BIOS-Setup-0014](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/BIOS/BIOS-Setup-0014.png)

    ![BIOS-Setup-0013](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/BIOS/BIOS-Setup-0013.png)

### 安装`macOS Monterey`

开机，按`F11`选择U盘引导，光标移动到`EFI USB Device`选择`OpenCore`分区启动：

进入`OpenCore`主引导界面，选择`Install macOS Monterey`，直接回车进入`OpenCore`引导，这期间会显示引导日志，也就是常见的`-v`(`啰嗦模式`)，如果不幸卡住了，请拍照发到`QQ群`里寻求帮助，也可以移步：[macOS BigSur 11.0安装中常见的问题及解决方法](https://blog.daliansky.net/Common-problems-and-solutions-in-macOS-BigSur-11.0-installation.html)；不会操作`OpenCore`的请事先补课：[精解OpenCore](https://blog.daliansky.net/OpenCore-BootLoader.html) 

![morefine-S500-Monterey-Installer-0001](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/Installer/morefine-S500-Monterey-Installer-0001.png)

![morefine-S500-Monterey-Installer-0002](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/Installer/morefine-S500-Monterey-Installer-0002.png)

![morefine-S500-Monterey-Installer-0003](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/Installer/morefine-S500-Monterey-Installer-0003.png)

很多的机友都是会在这个地方翻车。出现问题请进群反馈，请提供翻车照片及机器配置图。**不提供任何信息直接发问就是耍流氓**

![morefine-S500-Monterey-Installer-0004](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/Installer/morefine-S500-Monterey-Installer-0004.png)

这个过程需要1-2分钟,耐心等待，进入安装程序,出现语言选择界面

![BigSur_Installer_04](https://images.daliansky.net/d/YmBXVA8q/blog/BigSur/BigSur_Installer_04.png?download=1)

选择`简体中文`，点击`→` 继续

![morefine-S500-Monterey-Installer-0005](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/Installer/morefine-S500-Monterey-Installer-0005.png)

出现安装界面，选择`磁盘工具`，点击`继续`

![morefine-S500-Monterey-Installer-0006](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/Installer/morefine-S500-Monterey-Installer-0006.png)

进入`磁盘工具`，点击下图所示，选择`显示所有设备`

![morefine-S500-Monterey-Installer-0007](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/Installer/morefine-S500-Monterey-Installer-0007.png)

> ***在`磁盘工具`里面所做的操作涉及到你的数据安全，请认真仔细确认后再操作，否则由此造成的一切后果本站概不负责。***

![morefine-S500-Monterey-Installer-0008](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/Installer/morefine-S500-Monterey-Installer-0008.png)

图示中为在安装过 `Windows 10` 的磁盘中分区安装`  macOS Monterey`***本例中 `FreeSpace` 为将要安装的磁盘分区名称，请根据你的设备选择相应的磁盘***

![morefine-S500-Monterey-Installer-0010](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/Installer/morefine-S500-Monterey-Installer-0010.png)

点击`抹掉`，在弹出的窗口中输入：名称：`Hackintosher`；格式：`APFS`；

> ***假设您的磁盘是空的或者数据是已经备份过的,别怪我没提醒你!!!***

![morefine-S500-Monterey-Installer-0011](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/Installer/morefine-S500-Monterey-Installer-0011.png)

![morefine-S500-Monterey-Installer-0012](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/Installer/morefine-S500-Monterey-Installer-0012.png)

![morefine-S500-Monterey-Installer-0013](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/Installer/morefine-S500-Monterey-Installer-0013.png)

点击`抹除`，然后等待操作结束，点击`完成`，通过菜单选择`退出磁盘工具`或者按窗口左上角红色按钮离开磁盘工具

![morefine-S500-Monterey-Installer-0015](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/Installer/morefine-S500-Monterey-Installer-0015.png)返回到安装界面，选择`安装macOS Monterey`，点击`继续`

![morefine-S500-Monterey-Installer-0016](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/Installer/morefine-S500-Monterey-Installer-0016.png)

点击`同意`，继续

![morefine-S500-Monterey-Installer-0017](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/Installer/morefine-S500-Monterey-Installer-0017.png)

阅读许可协议的条款，点击 `同意` 

![morefine-S500-Monterey-Installer-0018](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/Installer/morefine-S500-Monterey-Installer-0018.png)

选择将要安装的磁盘卷标`Hackintosher`，点击`继续`

![morefine-S500-Monterey-Installer-0019](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/Installer/morefine-S500-Monterey-Installer-0019.png)

它会把USB安装盘上的安装文件预复制到要安装的系统分区里，这个过程通常会持续1-2分钟，之后系统会自动重启，进入第二阶段的安装

![morefine-S500-Monterey-Installer-0020](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/Installer/morefine-S500-Monterey-Installer-0020.png)

重启后继续安装，在安装期间，通常会自动重启4-5遍

![morefine-S500-Monterey-Installer-0023](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/Installer/morefine-S500-Monterey-Installer-0023.png)

![morefine-S500-Monterey-Installer-0025](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/Installer/morefine-S500-Monterey-Installer-0025.png)

![morefine-S500-Monterey-Installer-0026](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/Installer/morefine-S500-Monterey-Installer-0026.png)

![morefine-S500-Monterey-Installer-0027](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/Installer/morefine-S500-Monterey-Installer-0027.png)

![morefine-S500-Monterey-Installer-0028](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/Installer/morefine-S500-Monterey-Installer-0028.png)

![morefine-S500-Monterey-Installer-0030](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/Installer/morefine-S500-Monterey-Installer-0030.png)

![morefine-S500-Monterey-Installer-0031](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/Installer/morefine-S500-Monterey-Installer-0031.png)

安装`Monterey`的时间通常是安装`Catalina`的2倍，请务必耐心等待；安装完成后，会进入`设置向导`

![morefine-S500-Monterey-Installer-0032](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/Installer/morefine-S500-Monterey-Installer-0032.png)

选择`国家和地区`：`中国大陆`，点击 `继续` 按钮

![morefine-S500-Monterey-Installer-0033](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/Installer/morefine-S500-Monterey-Installer-0033.png)

设置键盘，使用默认值，点击 `继续` 按钮

![morefine-S500-Monterey-Installer-0034](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/Installer/morefine-S500-Monterey-Installer-0034.png)

进入辅助功能设置，默认不设置，选择 `以后` 继续

![morefine-S500-Monterey-Installer-0035](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/Installer/morefine-S500-Monterey-Installer-0035.png)

进入网络连接设置，点击`其它网络选项`

![morefine-S500-Monterey-Installer-0036](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/Installer/morefine-S500-Monterey-Installer-0036.png)

弹出提示信息：`我的电脑不接入互联网`，点击 `继续` 按钮

![morefine-S500-Monterey-Installer-0037](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/Installer/morefine-S500-Monterey-Installer-0037.png)

出现数据与隐私，阅读后点击 `继续` 按钮

![morefine-S500-Monterey-Installer-0038](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/Installer/morefine-S500-Monterey-Installer-0038.png)

出现迁移助理，如果全新安装而不使用`Time Machine`恢复数据，请点击`以后`继续

![morefine-S500-Monterey-Installer-0039](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/Installer/morefine-S500-Monterey-Installer-0039.png)

出现 `使用您的Apple ID登录`，请选择 `稍后设置` 

![morefine-S500-Monterey-Installer-0040](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/Installer/morefine-S500-Monterey-Installer-0040.png)

在弹窗提示选择 `跳过`

![morefine-S500-Monterey-Installer-0041](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/Installer/morefine-S500-Monterey-Installer-0041.png)

出现条款与条件，请阅读后，点击`同意`继续

![morefine-S500-Monterey-Installer-0042](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/Installer/morefine-S500-Monterey-Installer-0042.png)

在弹窗提示上再次点击`同意`，继续

![morefine-S500-Monterey-Installer-0044](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/Installer/morefine-S500-Monterey-Installer-0044.png)

出现创建用户账号窗口，输入用户名和密码，点击 `继续` 按钮

![morefine-S500-Monterey-Installer-0045](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/Installer/morefine-S500-Monterey-Installer-0045.png)

出现 `启用定位服务`窗口，点击  `继续` 按钮

![morefine-S500-Monterey-Installer-0046](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/Installer/morefine-S500-Monterey-Installer-0046.png)

在弹窗提示上再次点击`不使用`，继续

![morefine-S500-Monterey-Installer-0047](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/Installer/morefine-S500-Monterey-Installer-0047.png)

出现 `选择您的时区`，通过地图点击靠近您的位置的具体城市，点击 `继续` 按钮

![morefine-S500-Monterey-Installer-0048](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/Installer/morefine-S500-Monterey-Installer-0048.png)

出现分析窗口，取消勾选 `与Apple共享Mac分析` 点击 `继续` 按钮

![morefine-S500-Monterey-Installer-0049](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/Installer/morefine-S500-Monterey-Installer-0049.png)

出现屏幕使用时间窗口，点击`Set Up Later`继续

![morefine-S500-Monterey-Installer-0050](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/Installer/morefine-S500-Monterey-Installer-0050.png)

出现`Siri`设置界面，点击 `继续` 按钮

![morefine-S500-Monterey-Installer-0051](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/Installer/morefine-S500-Monterey-Installer-0051.png)

选择`Siri`语言，点击 `继续` 按钮

![morefine-S500-Monterey-Installer-0052](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/Installer/morefine-S500-Monterey-Installer-0052.png)

进入 `选择Siri声音` 界面，选择 `声音1`,点击 `继续` 按钮

![morefine-S500-Monterey-Installer-0053](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/Installer/morefine-S500-Monterey-Installer-0053.png)

进入`Siri`改善和听写界面，选择`以后`，点击 `继续` 按钮

![morefine-S500-Monterey-Installer-0054](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/Installer/morefine-S500-Monterey-Installer-0054.png)

弹出界面，让你选择外观

![morefine-S500-Monterey-Installer-0055](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/Installer/morefine-S500-Monterey-Installer-0055.png)

您可以根据个人的喜好选择浅色主题或者深色主题，点击 `继续` 按钮

设置向导完成，根据选择主题的不同，分别进入不同的界面

![morefine-S500-Monterey-Installer-0056](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/Installer/morefine-S500-Monterey-Installer-0056.png)

出现桌面后,可能会弹出 `键盘设置助理`，直接点击 `退出` 按钮，这样 整个的安装向导就完成了。

![morefine-S500-Monterey-Installer-0057](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/Installer/morefine-S500-Monterey-Installer-0057.png)

![morefine-S500-Monterey-Installer-0058](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/Installer/morefine-S500-Monterey-Installer-0058.png)

## 安装后的系统设置

系统安装后,你可以先喝杯咖啡兴奋会儿,马上还有更艰巨的任务在等着你呢

先打开终端，输入命令：

```bash
sudo spctl --master-disable		# 启用macOS安装应用允许任何来源
```

*目的是允许安装第三方下载的macOS应用程序*

## 感谢名单

- [Apple](https://www.apple.com/) 的 macOS
- [RehabMan](https://github.com/rehabman)维护的项目：[OS-X-Clover-Laptop-Config](https://github.com/RehabMan/OS-X-Clover-Laptop-Config) [Laptop-DSDT-Patch](https://github.com/RehabMan/Laptop-DSDT-Patch) [OS-X-USB-Inject-All](https://github.com/RehabMan/OS-X-USB-Inject-All)等
- [Acidanthera](https://github.com/acidanthera) 维护的项目：[OpenCorePkg](https://github.com/acidanthera/OpenCorePkg) [lilu](https://github.com/acidanthera/Lilu) [AirportBrcmFixup](https://github.com/acidanthera/AirportBrcmFixup) [WhateverGreen](https://github.com/acidanthera/WhateverGreen) [VirtualSMC](https://github.com/acidanthera/VirtualSMC) [AppleALC](https://github.com/acidanthera/AppleALC) [BrcmPatchRAM](https://github.com/acidanthera/BrcmPatchRAM) [MaciASL](https://github.com/acidanthera/MaciASL) 等
- [headkaze](https://www.insanelymac.com/forum/profile/1364628-headkaze/) 提供的工具：[hackintool](https://github.com/headkaze/Hackintool) [PinConfigurator](https://github.com/headkaze/PinConfigurator) [BrcmPatchRAM](https://www.insanelymac.com/forum/topic/339175-brcmpatchram2-for-1015-catalina-broadcom-bluetooth-firmware-upload/)
- [CloverHackyColor](https://github.com/CloverHackyColor)维护的项目：[CloverBootloader](https://github.com/CloverHackyColor/CloverBootloader) [CloverThemes](https://github.com/CloverHackyColor/CloverThemes)
- [ic005k](https://github.com/ic005k/)维护的项目：[OpenCore Auxiliary Tools OpenCore Configurator OCAT](https://github.com/ic005k/QtOpenCoreConfig)
- 宪武整理的：[P-little](https://github.com/daliansky/P-little) [OC-little](https://github.com/daliansky/OC-little)
- [chris1111](https://github.com/chris1111)维护的项目：[VoodooHDA](https://github.com/chris1111/VoodooHDA-2.9.2-Clover-V15) [Wireless USB Adapter Clover](https://github.com/chris1111/Wireless-USB-Adapter-Clover)
- [zxystd](https://github.com/zxystd)开发的[itlwm](https://github.com/zxystd/itlwm) [IntelBluetoothFirmware](https://github.com/zxystd/IntelBluetoothFirmware)
- [lihaoyun6](https://github.com/lihaoyun6)提供的工具：[CPU-S](https://github.com/lihaoyun6/CPU-S) [macOS-Displays-icon](https://github.com/lihaoyun6/macOS-Displays-icon) [SidecarPatcher](https://github.com/lihaoyun6/SidecarPatcher)
- [xzhih](https://github.com/xzhih)提供的工具：[one-key-hidpi](https://github.com/xzhih/one-key-hidpi)
- [Bat.bat](https://github.com/williambj1)更新维护的[精解 OpenCore](https://blog.daliansky.net/OpenCore-BootLoader.html)
- [athlonreg](https://github.com/athlonreg)更新维护的[OpenCore 0.5+ 部件补丁](https://blog.cloudops.ml/ocbook/) [Common-patches-for-hackintosh](https://github.com/athlonreg/Common-patches-for-hackintosh)
- [stevezhengshiqi](https://github.com/stevezhengshiqi) 更新维护的 [XiaoMi NoteBook Pro Hackintosh](https://github.com/daliansky/XiaoMi-Pro-Hackintosh) 和 [one-key-cpufriend](https://github.com/stevezhengshiqi/one-key-cpufriend)
- [Miracle-Sakuno](https://github.com/Miracle-Sakuno) 整理的各平台配置文件
- [github.com](github.com)
- [码云 gitee.io](gitee.io)
- [扣钉 coding.net](coding.net)

## 参考及引用：

- https://deviwiki.com/wiki/Dell
- https://deviwiki.com/wiki/Dell_Wireless_1820A_(DW1820A)
- [Hervé]([https://osxlatitude.com/profile/4953-herv%C3%A9/](https://osxlatitude.com/profile/4953-hervé/)) 更新的Broadcom 4350:https://osxlatitude.com/forums/topic/12169-bcm4350-cards-registry-of-cardslaptops-interop/
- [Hervé]([https://osxlatitude.com/profile/4953-herv%C3%A9/](https://osxlatitude.com/profile/4953-hervé/)) 更新的DW1820A支持机型列表:https://osxlatitude.com/forums/topic/11322-broadcom-bcm4350-cards-under-high-sierramojave/
- [nickhx](https://osxlatitude.com/profile/129953-nickhx/) 提供的蓝牙驱动：https://osxlatitude.com/forums/topic/11540-dw1820a-for-7490-help/?do=findComment&comment=92833
- [xjn819](https://blog.xjn819.com/)： [使用OpenCore引导黑苹果](https://blog.xjn819.com/?p=543) [300系列主板正确使用AptioMemoryFix.efi的姿势(重写版）](https://blog.xjn819.com/?p=317) 
- [dortania](https://github.com/dortania) 
- [insanelymac.com](https://www.insanelymac.com/) 
- [tonymacx86.com](https://www.tonymacx86.com/) 
- [远景论坛](http://bbs.pcbeta.com)
- [applelife.ru](https://applelife.ru/) 
- [olarila.com](https://www.olarila.com/)

