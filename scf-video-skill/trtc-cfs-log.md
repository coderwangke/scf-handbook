# TRTC 输入在线媒体流的日志配置

[TRTC 输入在线媒体流](https://cloud.tencent.com/document/product/583/55102) 是基于 `TRTC linux SDK` 实现的，并在云函数上运行，实现将已有的录播视频推送到 TRTC 房间进行直播。 默认只有标准输出日志，当有错误发生时，无法暴露 `SDK` 上的相关日志，无法继续深入排查。

接下来主要介绍下如何配置 `SDK` 的日志获取。

## 添加文件系统

### 网络配置

开启私有网络并设置

页面路径：函数设置 -> 高级设置 -> 网络配置

![](/.trtc-cfs-log\_images/trtc-cfs-网络配置.png)

### 文件系统

开启文件系统，选择期望的 `cfs` 文件系统，并正确设置远程目录和挂载点（本地目录，例如/mnt）

![](/.trtc-cfs-log\_images/trtc-cfs.png)

### 环境变量

通过环境变量 `LOG_PATH` 配置日志路径

![](/.trtc-cfs-log\_images/trtc-sdk-env.png)
