---
title: ros1
created: '2025-08-03T12:18:10.438Z'
modified: '2025-08-03T12:32:45.067Z'
---

ros1

# 安装
> 基于ubuntu22，使用docker容器来与本地ros2隔离，下面一键安装会有安装docker

终端
```bash
source <(wget -qO- http://fishros.com/install)
```
选择一键安装:ROS Docker版
这里选择noetic版本

下载镜像部分会出现`error`,这是因为镜像源被ban了,但先不急，继续往下，直到完成流程。

新开一个终端,称为终端2
执行
```bash
sudo docker pull swr.cn-north-4.myhuaweicloud.com/ddn-k8s/docker.io/fishros2/ros:noetic-desktop-full
```
这里是使用了[国内的镜像源](https://docker.aityp.com/image/docker.io/fishros2/ros:noetic-desktop-full)

下载好image后，复制一键安装的终端中，`4.生成容器`部分的命令，并将最后的image文件替换成`swr.cn-north-4.myhuaweicloud.com/ddn-k8s/docker.io/fishros2/ros:noetic-desktop-full`,
再到终端2中执行该命令

容器创建完成
