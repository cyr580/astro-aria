---
title: 将小爱音箱接入ChatGPT（使用群晖Docker）
description: >-
  将小爱音箱接入ChatGPT（使用群晖Docker）用于将小爱音箱接入ChatGPT，使用群晖Docker和开源项目实现：[xiaogpt](https://github.com/yihong0618/xiaogpt)
date: 'Mon Apr 08 2024 08:09:35 GMT+0800 (中国标准时间)'
dateFormatted: 'Mon Apr 08 2024 08:09:35 GMT+0800 (中国标准时间)'
layout: ../../layouts/post.astro
---
将小爱音箱接入ChatGPT（使用群晖Docker）

以下是整理和概括的步骤，用于将小爱音箱接入ChatGPT，使用群晖Docker和开源项目实现：[xiaogpt](https://github.com/yihong0618/xiaogpt)

### 1. 获取设备 DID 和 Hardware

#### 使用 Yonsm/MiService 项目：
- **环境要求**：Ubuntu 系统，安装 Python 环境。
- **项目地址**：[https://github.com/Yonsm/MiService](https://github.com/Yonsm/MiService)
- **操作步骤**：
  1. 克隆项目：`git clone https://github.com/Yonsm/MiService.git`
  2. 安装依赖项：`pip install aiohttp`
  3. 运行命令：`python3 micli.py mina`
  4. 成功执行后，会返回设备的 "miotDID" 和 "hardware"。
  5. ”name“: ”小爱音箱Pro2“,
     ”model“: ”xiaomi.wifispeaker.lx06“,
     ”did“: ”xxxxxxxx“,
     ”token“: ”xxxxxxxxxxxxxx“

### 2. 配置文件内容示例

创建配置文件内容如下，包含必要的账户信息、密钥以及设备信息等：

```json
{
  "hardware": "LX06",
  "account": "输入账号",
  "password": "输入密码",
  "openai_key": "sk-Ab2xxxxxx",
  "glm_key": "",
  "bard_token": "",
  "serpapi_api_key": "",
  "cookie": "",
  "mi_did": "输入DID",
  "use_command": false,
  "mute_xiaoai": true,
  "verbose": false,
  "bot": "chatgptapi",
  "tts": "mi",
  "edge_tts_voice": "zh-CN-XiaoxiaoNeural",
  "prompt": "请用100字以内回答",
  "keyword": ["请"],
  "change_prompt_keyword": ["更改提示词"],
  "start_conversation": "继续刚才的问题",
  "end_conversation": "结束刚才的问题",
  "stream": false,
  "proxy": "http://192.xxx.xx.xx:7890",
  "api_base": "http://192.xxx.xx.xx:8888/v1 or https://abc-def.openai.azure.com/",
  "gpt_options": {}
}
```

### 3. 上传配置文件至群晖

1. 在 Docker 目录下创建一个 `xiaogpt` 文件夹。
2. 将配置文件保存为 `config.json`。
3. 上传到 `/docker/xiaogpt/config` 目录下。

### 4. 启动服务

使用Docker命令启动服务：

```
docker run -v /volume1/docker/xiaogpt/config:/config yihong0618/xiaogpt —config=/config/config.json
```

**注意**：`/volume1/docker/xiaogpt/config` 路径需替换为你创建的配置文件实际路径。

### 5. 检查服务状态

- 进入群晖容器管理器，确认是否存在名为 类似`competent_hertz` 的容器。
- 查看日志，确认小爱音箱与 GPT 的对话是否正常。

**更新**（20240114）：运行上述命令后，将只启动一个名为类似 `competent_hertz` 的容器，确认该容器运行正常即可。

通过上述步骤，你可以将小爱音箱与 ChatGPT 连接起来，使其支持更智能的对话功能。

### 6. 踩坑SSL报错

Navigate to
cd /Applications/Python\ 3.7/

Click on Install Certificates.command

This should solve it.
