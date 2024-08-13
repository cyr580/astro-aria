---
title: A-shell直接下载mp4
description: ''
date: 'Sat Dec 30 2023 21:12:05 GMT+0800 (中国标准时间)'
dateFormatted: 'Sat Dec 30 2023 21:12:05 GMT+0800 (中国标准时间)'
layout: ../../layouts/post.astro
---
# 使用 iOS a-shell App 下载和转换视频教程

在本教程中，我们将介绍如何使用 iOS a-shell App 来下载和转换视频。a-shell 是一个内置了 Python 的终端模拟器，可以让我们在 iOS 设备上运行 Python 脚本。

## 步骤 1：安装 a-shell 应用

首先，在您的 iOS 设备上打开 App Store，并搜索 "a-shell" 应用。下载并安装该应用。

## 步骤 2：编写 Python 脚本

将以下代码复制到一个名为 `yt.py` 的 Python 文件中：

```python
import os
import subprocess
from urllib.parse import urlparse

import yt_dlp

def download_video(url, output_folder):
    ydl_opts = {
        'format': 'bestvideo[ext=mp4]+bestaudio[ext=m4a]/best[ext=mp4]/best',
        'outtmpl': os.path.join(output_folder, '%(title)s.%(ext)s'),
    }

    with yt_dlp.YoutubeDL(ydl_opts) as ydl:
        ydl.download([url])

def convert_to_mp4(input_file, output_folder):
    output_file = os.path.join(output_folder, os.path.splitext(os.path.basename(input_file))[0] + '.mp4')
    subprocess.run(['ffmpeg', '-i', input_file, '-c', 'copy', output_file])

def main():
    video_urls = input("请输入视频链接（多个链接用逗号分隔）: ").split(',')
    output_folder = 'mp4'

    if not os.path.exists(output_folder):
        os.makedirs(output_folder)

    for url in video_urls:
        url = url.strip()
        if not url:
            continue

        try:
            print(f"正在下载视频：{url}")
            download_video(url, output_folder)
        except Exception as e:
            print(f"下载视频时发生错误：{e}")

    # 转换非 mp4 格式文件为 mp4
    for filename in os.listdir(output_folder):
        if filename.lower().endswith(('.mkv', '.flv', '.webm', '.avi', '.mov', '.wmv', '.3gp')):
            input_file = os.path.join(output_folder, filename)
            convert_to_mp4(input_file, output_folder)
            os.remove(input_file)

    print("所有视频下载和转换完成，输出目录：", os.path.abspath(output_folder))

if __name__ == "__main__":
    main()
```

## 步骤 3：使用 a-shell 运行 Python 脚本

1. 打开 a-shell 应用，并点击右上角的 "+" 按钮，创建一个新的脚本。
2. 将 `yt.py` 文件上传到 a-shell 应用中，可以使用 iTunes 文件共享或其他途径将文件拖放到 a-shell App 中。
3. 在 a-shell 终端中输入以下命令来运行脚本：

   ```shell
   python yt.py
   ```

4. 您将被提示输入视频链接，多个链接请用逗号分隔。输入完毕后，脚本将开始下载和转换视频。
5. 所有下载和转换完成后，输出的视频将保存在当前目录下的 "mp4" 文件夹中。

恭喜！您已成功地在 iOS 设备上使用 a-shell App 下载和转换视频。

请注意：
- 请确保您的设备已安装并配置了 yt-dlp 和 ffmpeg。
- 本教程假定您已具备基本的 Python 编程知识。
- 请遵守法律法规和视频平台的使用规定，在下载和使用视频时要遵守相关规定。

希望本教程能帮助到您！如有任何问题，请随时提出。
