---
title: UltraUXThemePatcher破解主题不成功
description: ''
date: 'Sat Jan 15 2022 19:29:37 GMT+0800 (中国标准时间)'
dateFormatted: 'Sat Jan 15 2022 19:29:37 GMT+0800 (中国标准时间)'
layout: ../../layouts/post.astro
---
![](https://s2.loli.net/2022/01/15/y4XoUTxJkCPj9mG.jpg)
<!-- More --> 
01，为免造成系统错误，使用前必须 [创建系统还原点](https://zhutix.com/10tutorials/huanyuan/)；造成严重后果，本站概不负责！

02，Win10在进行系统重大更新前(比如1803升级1809)必须将主题切换到默认主题，然后卸载本补丁再进行系统升级操作！

03，UltraUxThemePatcher会更改系统dll文件，故部分杀软会报毒，请放心使用！安装前请务必退出各种安全软件！

04，本补丁兼容WinXP/7/8/8.1/10/11，不兼容Win10 1511（10586）（[查看版本号](https://zhutix.com/moe/study/winver-banben/)）及预览版系统

05，Win10系统如果安装本补丁后重启出现闪屏，请查阅 [Win10系统开机闪屏解决方法](https://zhutix.com/study/win10-heiping-jj/)

06，请右键 – 以管理员身份运行本补丁

### 提示not supported

如果提示not supported，也许是因为你用的预览版Win10，补丁暂未支持，静等作者更新；如果你用的老版本Win10，请尝试安装老版本补丁：

[https://pan.baidu.com/s/1B3HJGwnPmJvel9JpqqQzdw](https://pan.baidu.com/s/1B3HJGwnPmJvel9JpqqQzdw) 提取码：qftm

* * *

### 验证是否破解成功

如果安装本补丁后应用主题无效，请再次打开安装程序，停留在破解详情界面（如下图），看下面红色框内的项是否显示的是 **patched**

如果是，则说明你破解成功，如果有任意一项显示 **NOT patched** 则不成功！

Win10 1709/1803/1809/1903/1909，第一个框会提示**no need to patch**，意思不需要破解，不用理会！

![](https://dl.zhutix.net/2018/11/UltraUxThemePatcher351.jpg)

**如果破解不成功，请继续往下看**

**右键以管理员身份再次运行此软件，安装！**如果仍显示NOT patched，请采用下面的方法：

下载 [此文件](https://dl.zhutix.net/2018/12/guanliyuan.zip)，运行里面的“添加管理员取得所有权到右键菜单.reg”

打开C:\\Windows\\System32，搜素Themeui，在搜索结果内的Themeui.dll上右键-管理员取得所有权

返回C:\\Windows\\System32，搜素Uxinit，在搜索结果内的Uxinit.dll上右键-管理员取得所有权

Win7和Win8还需要搜索Uxtheme.dll，以同样的方法获取管理员权限

**然后右键以管理员身份重新安装破解补丁，重启电脑即可！**

**破解成功，但仍无法使用主题？往下看**

部分主题需要更改 [项目显示大小为100%](https://zhutix.com/study/xm100/) 才能正常使用，特别是一些动漫主题、钢铁侠主题、仿制主题等，简约主题一般不需要！

**破解成功、项目大小也是100%，仍无法使用主题？往下看**

一般情况下是优化软件把主题服务给优化掉了，我们需要开启它！首先打开计算机管理：

在此电脑上右键-管理；或者在开始按钮处右键 – 计算机管理；或者在键盘上按“WIN+R”快捷键，打开运行界面，输入“services.msc”指令（图1）；打开服务项，找到Themes服务，在Themes上右键-属性（图2）；查看服务状态是否是已停止，如果是，点击下面的启动，然后在启动类型里面选择“自动”，确定！（图3）；再次应用主题就OK了！

[![](https://dl.zhutix.net/2018/12/themeswufu.jpg)](https://dl.zhutix.net/2018/12/themeswufu.jpg)

**如果以上方法用后仍无法使用主题**

那真无奈了，你这种情况我们也是前所未见，请重装系统，安装微软原版系统镜像：

[https://zhutix.com/10tutorials/win10-iso/](https://zhutix.com/10tutorials/win10-iso/)

* * *

### 卸载

![](https://dl.zhutix.net/2019/04/5234.png)

Win10在进行大更新（比如[180-1903](tel:180-1903)）前，必须卸载这个补丁，否则电脑会闪屏！

进入C:\\Program Files (x86)\\UltraUXThemePatcher运行卸载程序，按照默认选项卸载即可，或打开系统设置(或控制面板)卸载。

如果你已经因此闪屏请查阅解决方法：[https://zhutix.com/study/win10-heiping-jj/](https://zhutix.com/study/win10-heiping-jj/)

### 更新日志

2021年11月20日 支持Win11 Insider版本支持Win10 21H2、takeowner 错误已修复

2020年11月16日 支持下一个主要更新21H1，重大更新后的问题应得到解决（机翻-\_-||）

2021年1月8日 支持21H2

2021年1月17日 修复了显示文本中的错误

2021年4月16日 支持下一个主要更新21H2

2021年6月19日 支持下一次重大更新21H2

2021年7月4日 支持 Windows 11 Insider 版本

2021年9月4日 支持 Windows 11 Insider 版本 支持下一个主要的 Windows 10 更新 21H2
