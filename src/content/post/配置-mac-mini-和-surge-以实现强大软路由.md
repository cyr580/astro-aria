---
title: 配置 Mac Mini 和 Surge 以实现强大软路由
description: ''
date: 'Mon Mar 11 2024 20:48:08 GMT+0800 (中国标准时间)'
dateFormatted: 'Mon Mar 11 2024 20:48:08 GMT+0800 (中国标准时间)'
layout: ../../layouts/post.astro
---
# 配置 Mac Mini 和 Surge 以实现强大软路由
1. **准备设备**：
    - 确保拥有 Mac Mini M2 基础型号。
    - 准备一条稳定的网络连接，并使用网线直接连接到 Mac Mini。

2. **安装 Surge**：
    - 在 Mac 上安装 Surge，选择 Surge 4 或 Surge 5 版本均可。
    - 启动 Surge，选择试用版本开始。

3. **基础配置**：
    - 在首次运行 Surge 时，会出现设置向导。仔细阅读并根据引导进行设置。
    - 需要配置的主要项目包括系统代理、增强模式和网关模式。
    - 准备一份配置文件，其中应包含所需的节点和规则。如果你的服务提供商提供配置文件，可以直接使用；如果没有提供，可以使用订阅转换工具生成配置文件。

4. **网络结构配置**：
    - 根据需求选择将 Mac Mini 作为次级路由器还是主路由器。
    - **次级路由器**：将 Mac Mini 通过网线连接到家庭现有路由器。在 Surge 中设置设备，使用系统代理和增强模式。
    - **主路由器**：如果需要，可以通过购买 USB 2.5G 网络卡来提升网络速度。将 Mac Mini 通过网线连接到交换机，并设置为拨号上网，承担家庭网络的主路由器角色。

5. **DHCP 配置**：
    - 在 Surge 中打开 DHCP 功能。如果 Mac Mini 作为主路由器，需要在家庭现有路由器中关闭 DHCP 服务，并让 Surge 接管 DHCP 管理。
    - 配置网络设备选择，选择通过网线连接的网络接口。
    - 根据提示完成 DHCP 服务器设置。默认设置通常适用，但如果你了解相关知识，也可以自定义设置。

6. **设备连接**：
    - 确保需要通过 Surge 网络访问的设备的网关设置指向 Mac Mini 的 IP 地址。不需要翻墙的设备可以保留原有的网关设置，不会受到影响。
    - 对于每个需要使用 Surge 网络的设备，可能需要手动设置使用 Mac Mini 作为网关。

这是一个简化的操作流程概览。具体步骤可能会根据你的网络环境和设备配置有所不同。强烈建议在进行配置之前详细阅读 Surge 的官方文档和指南，以确保正确设置。


[Surge增强模式](https://kb.nssurge.com/surge-knowledge-base/v/zh/faq/common-faqs#zeng-qiang-mo-shi-jian-rong-xing-wen-ti)
[Surge Ponte](https://kb.nssurge.com/surge-knowledge-base/v/zh/guidelines/ponte)
