## 进入 `BIOS`
- 打开电源，按键盘的 `DEL` 键进入 `BIOS`
	![morefine S500 BIOS Setup-0001](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/BIOS/BIOS-Setup-0001.png)
	![morefine S500 BIOS Setup-0002](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/BIOS/BIOS-Setup-0002.png)

## 禁用 `Secure Boot`

- 进入 `Security` - `Secure Boot` 选单![BIOS-Setup-0012-0](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/BIOS/BIOS-Setup-0012-0.png)
- 将 `Secire Bppt` 的状态由 `Enabled` 修改为 `Disabled`![BIOS-Setup-0012](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/BIOS/BIOS-Setup-0012.png)

## 关闭 `CFG Lock`

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

## 修改 `DVMT Pre-Allocated` 为 `64MB` 

修改 `DVMT Pre-Allocated` 为 `64MB` ，以便支持 `4K@60Hz` 显示模式

- 进入 `Chipset` - `System Agent (SA) Configuration` 选单![BIOS-Setup-0008](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/BIOS/BIOS-Setup-0008.png)

-  进入 `Graphics Configuration` 选单![BIOS-Setup-0009](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/BIOS/BIOS-Setup-0009.png)

- 光标移动到 `DVMT Pre-Allocated` ，将内存由 `32M` 修改为 `64M`![BIOS-Setup-0010](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/BIOS/BIOS-Setup-0010.png)

  ![BIOS-Setup-0011](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/BIOS/BIOS-Setup-0011.png)

## 调整 `UEFI` 引导选项

如果单 `mscOS` 使用，该选项为非必须调整选项

- 进入 `Boot` 选单

- 进入 `Boot Option #1` ，将 `UEFI OS` 设置为最优先，否则默认会修改为 `Windows Boot Manager`

  ![BIOS-Setup-0014](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/BIOS/BIOS-Setup-0014.png)

  ![BIOS-Setup-0013](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main/Docs/images/BIOS/BIOS-Setup-0013.png)
