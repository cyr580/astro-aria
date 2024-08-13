---
title: Bitwarden密码管理器（使用群晖Docker）
description: >-
  Vaultwarden是一款开源的密码管理器，使用Rust编写，是非官方Bitwarden服务器实现。它提供了强大的密码管理功能，并支持多种客户端和浏览器插件。
date: 'Sun Apr 21 2024 23:36:45 GMT+0800 (中国标准时间)'
dateFormatted: 'Sun Apr 21 2024 23:36:45 GMT+0800 (中国标准时间)'
layout: ../../layouts/post.astro
---
### Vaultwarden功能完善与数据安全

Vaultwarden是一款开源的密码管理器，使用Rust编写，是非官方Bitwarden服务器实现。它提供了强大的密码管理功能，并支持多种客户端和浏览器插件。

#### 数据实时同步功能

作为多客户端密码管理软件，实现密码数据在多客户端上实时更新至关重要。启用WebSocket通知是一个解决方案，它用于将相关事件通知给浏览器、Bitwarden的桌面和浏览器扩展客户端。

在Vaultwarden中，默认情况下WebSocket已经集成到80端口中，对于反向代理用户，需要正确配置以传递WebSocket Upgrade和Connection标头。

#### 启用移动客户端推送通知

从Vaultwarden 1.29.0版本开始，可以启用移动客户端的推送通知，无需手动同步即可实现个人密码库的自动同步。

- 访问[Bitwarden官网](https://bitwarden.com/host/)获取INSTALLATION ID和KEY。
- 在docker-compose.yaml中添加相应的环境变量。
- 重启容器后，即可启用推送通知。

#### 浏览器插件使用移动设备登录

通过设置，可以实现使用移动设备登录浏览器插件，而无需每次输入长密码。

1. 在手机客户端设置中打开“使用此设备批准来自其他设备的登录请求”选项。
2. 在浏览器插件设置中，将密码库超时动作设置为注销。
3. 重新登录时，选择使用设备登录，确认手机客户端上的登录请求即可。

#### 关于数据安全

- 设置SIGNUPS_ALLOWED=false和INVITATIONS_ALLOWED=false，禁止新用户注册和邀请。
- 禁用WEB_VAULT_ENABLED，减小暴露面，但不影响客户端使用。
- 接入cloudflare，并自定义规则，如禁止国外IP访问。
- 定期备份数据，并进行异地备份。
- 避免在相同地方备份数据，养成云端备份和密码保存在Vaultwarden的习惯。
