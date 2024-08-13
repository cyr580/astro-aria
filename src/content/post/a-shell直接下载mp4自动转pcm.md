---
title: A-shell直接下载mp4自动转pcm
description: ''
date: 'Sun Dec 17 2023 20:00:00 GMT+0800 (中国标准时间)'
dateFormatted: 'Sun Dec 17 2023 20:00:00 GMT+0800 (中国标准时间)'
layout: ../../layouts/post.astro
---
# a-shell：一款支持多窗口的iOS终端，彻底改变了用户与设备互动的方式。

## 软件详情
其直观的设计和强大的功能使其成为实现无缝多任务处理和高效命令执行的首选工具。无论你是开发人员、系统管理员还是休闲用户，a-shell都提供了一个适应你需求的强大环境。通过不断的更新和庞大的社区支持，a-shell成为移动生产力不断发展的典范。

## 准备工作
1. 安装a-shell（yt-dlp ffmpeg）
2. 安装Textastic

## 使用ChatGPT创建脚本
输入提示：作为Python专家，利用yt-dlp和ffmpeg帮我创建一个脚本，能够自动下载视频并使用shell命令将其转换为PCM格式。

```sh
#!/bin/bash

# 创建保存视频的目录（如果不存在）
mkdir -p mp4

# 获取要下载的视频链接
read -p "请输入要下载的视频链接 (如果不想下载，直接回车跳过): " video_link

# 如果提供了下载链接，则使用yt-dlp下载视频到mp4目录中
if [ -n "$video_link" ]; then
    yt-dlp --format 'bestvideo+bestaudio/best' --merge-output-format mp4 -o "mp4/%(title)s.%(ext)s" "$video_link"
    echo "下载完成！"
fi

# 创建保存音频的目录（如果不存在）
mkdir -p pcm

# 遍历mp4文件夹中的所有mp4文件
for mp4_file in mp4/*.mp4; do
    # 使用参数展开获取文件名和扩展名
    filename="${mp4_file##*/}"
    filename_no_ext="${filename%.*}"
    
    # 使用ffmpeg将mp4文件转换为pcm
    ffmpeg -i "$mp4_file" -vn -acodec pcm_s8 -ar 22050 -ac 2 -f s8 "pcm/${filename_no_ext}.pcm"
done

echo "转换完成！"
```

## 打开a-shell
输入命令：

```
sh ./mp4topcm.sh
```

## 保存
下载的mp4文件在sh同目录下的mp4文件夹，转换好的pcm在同目录下的pcm文件夹。
