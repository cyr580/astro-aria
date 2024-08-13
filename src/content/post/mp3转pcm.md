---
title: mp3转pcm
description: ''
date: 'Tue Dec 13 2022 07:13:00 GMT+0800 (中国标准时间)'
dateFormatted: 'Tue Dec 13 2022 07:13:00 GMT+0800 (中国标准时间)'
layout: ../../layouts/post.astro
---
![图片](/assets/02.jpeg)


```

ffmpeg -i E:\ss\10m-bwl.mp3 -acodec pcm_s16le -f s16le -ac 1 -ar 16000 E:\ss\10m-bwl.pcm
ffmpeg -i E:\ss\20m-bwl.mp3 -acodec pcm_s16le -f s16le -ac 1 -ar 16000 E:\ss\20m-bwl.pcm
ffmpeg -i E:\ss\21m-ll.mp3 -acodec pcm_s16le -f s16le -ac 1 -ar 16000 E:\ss\21m-ll.pcm
ffmpeg -i E:\ss\25m-wl.mp3 -acodec pcm_s16le -f s16le -ac 1 -ar 16000 E:\ss\25m-wl.pcm

```
