# 全景录制中转cos播放卡顿问题

## 问题架构说明
1、 全景录制

2、 使用 cos 作为录制中转

![](.full-record-cos-play-stuck_images/arch.png)

## 问题原因

1、transcode 函数 以流式的方式从 cos 拉取视频分片，进行转码，并转存回 cos，默认生成的 mp4 的 `moov` 元数据信息并不在头部，会导致视频播放偶现卡顿问题。

备注：使用 cfs（本地存储）作为录制中转不会有这种问题

## 解决办法

给 transcode 函数新增环境变量：`FMP4=mp4`
