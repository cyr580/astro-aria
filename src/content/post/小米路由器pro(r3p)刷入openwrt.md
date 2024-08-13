---
title: 小米路由器Pro(R3P)刷入OpenWrt
description: ''
date: 'Wed Jan 12 2022 19:18:23 GMT+0800 (中国标准时间)'
dateFormatted: 'Wed Jan 12 2022 19:18:23 GMT+0800 (中国标准时间)'
layout: ../../layouts/post.astro
---
![mi](/assets/IMG_1.jpg)
<!-- more -->
# 准备工具
U盘一个(格式化成FAT32格式) 能访问路由器后台、访问SSH、使用U盘的电脑或手机一台 预先下载好OpenWrt固件([下载页面](https://openwrt.org/toh/hwdata/xiaomi/xiaomi_mi_router_3_pro)，找**Firmware OpenWrt Install URL**)
（Github下载地址，[openwrt-ramips-mt7621-xiaomi_mir3p-squashfs-factory.bin](https://github.com/cyr580/openwrt-ramips-mt7621-xiaomi_mir3p/blob/master/openwrt-ramips-mt7621-xiaomi_mir3p-squashfs-factory.bin?raw=true)）

# 刷入开发版固件，获取SSH访问权限
获取到SSH权限之后，才能刷入非官方固件。
小米路由器获取SSH权限的方法是：先刷入开发版固件，用app绑定路由器后，访问开放平台，可以获取到root密码、下载ssh解锁工具。
接下来就按照这个步骤进行操作：

首先，打开MiWiFi下载页，点击ROM图标，找到小米路由器Pro 开发版的下载按钮，点击下载。 开发版最后一次更新时间是2017年8月25日，看样子也不会再更新了，所以直接放[下载链接](http://bigota.miwifi.com/xiaoqiang/rom/r3p/miwifi_r3p_firmware_daddf_2.13.65.bin)。

下载好固件后，直接去路由器后台更新固件，等待重启。

手机下载MiWiFi app，打开并绑定路由器到小米账号，然后卸载。

访问[MiWiFi SSH页面](https://d.miwifi.com/rom/ssh)。登录小米账号后，就可以看到绑定的路由器，后面跟着root密码和一个下载工具包的按钮。记住这个root密码，然后把工具包下载下来，文件名应该是miwifi_ssh.bin。

这个页面写有详细的使用方法，此处复读：
> 1. 请将下载的工具包bin文件复制到U盘（FAT/FAT32格式）的根目录下，保证文件名为miwifi_ssh.bin；
> 2. 断开小米路由器的电源，将U盘插入USB接口；
> 3. 按住reset按钮之后重新接入电源，指示灯变为黄色闪烁状态即可松开reset键；
> 4. 等待3-5秒后安装完成之后，小米路由器会自动重启，之后您就可以尽情折腾啦 ：）

第1步复制miwifi_ssh.bin到U盘的同时，顺便把OpenWrt固件一起放进去，改名为factory.bin。

路由器开机完成后，就可以尝试着拿刚才获取到的root密码访问SSH了。但不一定刚开好机就能访问，可能要等几分钟。

# 刷入OpenWrt固件
假设此时已经将OpenWrt固件放入U盘并改名为<font color=red>factory.bin</font>，也可以**SCP传入/tmp目录**，记得改个简短的文件名，方便操作，如<font color=red>firmware.bin</font>

ssh 进入到路由器，然后执行下面的指令，小米路由器 IP 一般是<font color=red>192.168.31.1</font>

打开ssh，输入以下命令：
```
cd /extdisks/sda1
nvram set flag_try_sys1_failed=1
nvram set flag_try_sys2_failed=0
nvram set flag_boot_success=0
nvram commit
dd if=factory.bin bs=1M count=4 | mtd write - kernel1
mtd erase rootfs0
mtd erase rootfs1
mtd erase overlay
dd if=factory.bin bs=1M skip=4 | mtd write - rootfs0
reboot
```

/extdisks/sda1 对应的是U盘根目录。如果重插过U盘，这个路径可能会有变化。

或者：
```
cd /tmp
nvram set flag_try_sys1_failed=1 
nvram set flag_try_sys2_failed=0 
nvram set flag_boot_success=0 
nvram commit
dd if=firmware.bin bs=1M count=4 | mtd write - kernel1
mtd erase rootfs0
mtd erase rootfs1
mtd erase overlay
dd if=firmware.bin bs=1M skip=4 | mtd write - rootfs0
reboot
```

输入完命令后，路由器会自动重启，之后就会变成OpenWrt了。

# 如果想刷回官方固件
假设此时U盘仍然是FAT/FAT32格式。建议先将U盘里的文件清空。

从刚才的下载页面，下载官方固件，放入U盘，并重命名为miwifi.bin。

打开路由器ssh，输入以下命令：

```
fw_setenv flag_try_sys1_failed 0
fw_setenv flag_try_sys2_failed 1
fw_setenv flag_boot_success 0
```
断电，将U盘插入路由器，按住reset键通电，黄灯闪烁时松开。（同上面的2、3、4步）

等待几分钟，黄灯/蓝灯常亮后，就刷回官方固件了。

# 补充
SCP上传固件
```
scp firmware.bin root@192.168.31.1:/tmp
```

刷完不要着急，等个十分钟左右指示灯变蓝（非要着急拔电源变砖了，后果自负），然后进入后台管理即可
路由器 IP ：<font color=red>192.168.1.1</font>
默认用户名：<font color=red>root</font>
默认密码：<font color=red>password</font>

如果和宽带冲突，自己先别把路由器和宽带连一起，先连路由器和设备登录进去（WiFi 或网线都行），改下路由器的 IP ，<font color=red>网络 -> 接口 -> LAN</font>，改成自己想要的，宽带是 <font color=red>1.1</font>，你随便改个 <font color=red>2.1</font>
