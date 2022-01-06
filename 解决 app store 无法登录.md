## 解决 `app store` 无法登录

> 群里摸鱼的时候经常发现群友会咨询：“``我的app store为啥无法登录？``”，之前没太在意，这不昨天我想下载个`Transporter`准备上传`ios`应用，才发现我自己的电脑也是无法登录`app store`，于是便有了该教程

## 判断问题

打开终端，输入命令：

```bash
$ ifconfig en0
ifconfig: interface en0 does not exist
```

如果出现`ifconfig: interface en0 does not exist`，那么大概率你的`app store`也是无法正常登录的。之所以出现该问题，是由于小兵的固态硬盘总是安装在不同的机器上出现很多个以太网设备导致的。

如图所示：小兵的网络设备里包含了 `n` 个以太网设备，这些重复的设备导致了网卡不是从 `en0` 开始命名的

![Networks2](https://raw.githubusercontent.com/daliansky/morefine-S500-Hackintosh/main//Docs/images/Tutorials/Networks3.png)

## 解决方法

- 移除 `NetworkInterfaces.plist`

  打开终端，输入命令：

  ```bash
  $ sudo rm -rf /Library/Preferences/SystemConfiguration/NetworkInterfaces.plist*
  Password:
  ```

  输入当前用户的密码，然后回车

- 删除所有的网络设备

  打开 `系统偏好设置` - `网络`，移除左侧所有的网络设备，左侧清空后，点击右下角的`应用`。如图所示：

  ![Networks4](../../morefine-S500-Hackintosh/Docs/images/Tutorials/Networks4.png)

- 重启

- 重新添加网络设备

  ![Networks5](../../morefine-S500-Hackintosh/Docs/images/Tutorials/Networks5.png)

## 检查网络状态

打开终端，输入命令：

```bash
$ ifconfig en0                                                                                               
en0: flags=8863<UP,BROADCAST,SMART,RUNNING,SIMPLEX,MULTICAST> mtu 1500
	options=46b<RXCSUM,TXCSUM,VLAN_HWTAGGING,TSO4,TSO6,CHANNEL_IO>
	ether 00:e2:4c:68:33:20
	inet6 fe80::ce1:3fd8:3799:2a45%en0 prefixlen 64 secured scopeid 0x4
	inet 192.168.105.106 netmask 0xffffff00 broadcast 192.168.105.255
	nd6 options=201<PERFORMNUD,DAD>
	media: autoselect (1000baseT <full-duplex>)
	status: active
```

![Hackintool_Misc](../../morefine-S500-Hackintosh/Docs/images/Tutorials/Hackintool_Misc.png)

## 重新登录 `app store`

成功登录后如图所示：

![appstore](../../morefine-S500-Hackintosh/Docs/images/Tutorials/appstore.png)

## 收工，本教程结束

