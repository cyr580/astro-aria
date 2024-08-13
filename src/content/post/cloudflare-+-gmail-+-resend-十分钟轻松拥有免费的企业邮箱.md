---
title: Cloudflare + Gmail + Resend 十分钟轻松拥有免费的企业邮箱
description: >-
  创建一个企业邮箱对于提升你的品牌形象和管理邮件非常重要，尤其是对于独立开发者和初创公司来说。本文介绍了一个完全免费的方法来设置企业邮箱，利用Cloudflare、Gmail和Resend的结合使用。
date: 'Mon Jul 01 2024 01:52:27 GMT+0800 (中国标准时间)'
dateFormatted: 'Mon Jul 01 2024 01:52:27 GMT+0800 (中国标准时间)'
layout: ../../layouts/post.astro
---

创建一个企业邮箱对于提升你的品牌形象和管理邮件非常重要，尤其是对于独立开发者和初创公司来说。本文介绍了一个完全免费的方法来设置企业邮箱，利用Cloudflare、Gmail和Resend的结合使用。以下是详细步骤：

# 前提条件

确保你已拥有一个域名，并且此域名的DNS管理权在Cloudflare上。

# 步骤1：设置Cloudflare邮件转发至Gmail

1. 登录Cloudflare，找到「电子邮件路由」选项，进入。
2. 在目标规则标签中启用Catch-All功能，并点击编辑。
3. 设置转发规则，将所有邮件都转发到你的Gmail邮箱。
	• 利用Gmail的”+“功能，例如yourname+anytag@gmail.com，可以帮助你更好地管理邮件。

# 步骤2：在Resend获取API Key

1. 创建Resend账户并登陆，找到API Keys标签下申请新的API Key。
2. 记下或保存SMTP设置信息，稍后设置Gmail时会用到。

# 步骤3：配置Gmail利用Resend服务发送邮件

1. 在Gmail设置中找到「账户和导入」或「账户」，点击「添加另一个邮件地址」。
2. 输入你在步骤1设置的企业邮箱名称和地址。
3. 输入步骤2中获得的Resend SMTP服务信息，使用获取的API Key作为密码。
4. 完成SMTP设置后，查收Gmail发出的确认邮件并确认。

# 完成！

现在，你就可以使用自己的企业邮箱来发送和接收邮件了，而且这整个流程是完全免费的。适用于独立开发者、小企业或任何预算有限但希望建立专业形象的人士。

查看详细信息和示意图，请访问原始文章：Cloudflare + Gmail + Resend 完全免费企业邮箱设置教程。

这个方法不仅经济实惠，同时提供了强大的灵活性和高度的定制性，让你的通信更加专业，同时也为你的业务或个人品牌增添亮点。


原文链接：[https://cleanclip.cc/zh/developer/cloudflare-worker-gmail-resend-enterprise-email](https://cleanclip.cc/zh/developer/cloudflare-worker-gmail-resend-enterprise-email)
