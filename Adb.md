---
tags: [tools]
title: Adb
created: '2025-11-04T03:21:33.393Z'
modified: '2025-11-04T03:27:44.781Z'
---

Adb

## 安装
```bash
sudo apt update
sudo apt install android-tools-adb android-tools-fastboot
```

# 华为手机
## 连接
插上数据线，在开发人员选项中打开adb调试
```bash
#若显示设备序列号并标注为`device`，则表示连接成功
adb devices
```

## 包名
在手机上，软件要用包名指示
```bash
#查看所有安装的包
adb shell pm list packages
```
当然使用雪豹速清查看软件和对应的包名更方便

## 停用
```bash
#停用/隐藏应用（保留数据但不可见）
#但应用仍存在于系统中，不会影响依赖它的功能。
adb shell pm disable-user <包名>

#恢复（重新显示）
adb shell pm enable <包名>
```
