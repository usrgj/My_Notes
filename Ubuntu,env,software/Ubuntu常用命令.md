---
tags: [Ubuntu]
title: Ubuntu常用命令
created: '2025-07-17T12:55:01.096Z'
modified: '2025-10-08T10:05:06.790Z'
---

Ubuntu常用命令

```bash
tar -I 'zstd -9 -T0' -cvf archive.tar.zst dir/
tar -I 'zstd -9 -T0' -cvf archive.tar.zst choose_frames_middle/*/*_finish.json
# v参数是在终端输出进度
zstd -cd 文件名.tar.zst | tar -xf -
```

```bash
#只清空文件，保留目录结构
find /sdcard/Download/ -type f -delete
```

```bash
rsync -avh --partial --progress matlab.zst /media/gj/MyDisk/Software/
```

# apt & dpkg
[在包相关笔记中](../通识/包.md)

# ls
### **基本用法**
|命令|说明|
|---|---|
|`ls`|列出当前目录下内容|
|`ls /path/`|列出指定目录内容|

### **常用选项**
| 选项 | 说明 |
|------|------|
| `-l`| 以长格式显示（详细信息，包括权限、所有者、大小等） |
|`-d */`|仅列出目录|
| `-a`| 显示所有文件（包括隐藏文件，以 `.` 开头的文件） |
| `-h`| 与 `-l` 一起使用，以人类可读格式显示文件大小（如 KB、MB） |
| `-t`| 按修改时间排序（最新修改的在前） |
| `-r`| 反向排序 |
| `-S`| 按文件大小排序（大的在前） |
| `-R`| 递归列出子目录内容 |
| `--color` | 彩色显示（通常默认启用） |
|`--ignore="*.cpp"`|忽略某些文件,如"*.cpp"是忽略后缀为cpp的文件|
|`--time-style="+%Y-%m-%d"`|自定义时间格式|
|`mkdir <dir name>`|创建路径|
|`cd <path>`|到指定路径|
|`pwd`|显示当前终端所在路径|

# Dell长寿法
## 电池
```bash
# 查看电池状态，结合watch使用。power不是实时的，除非有大变化，否则两分钟更新一次
upower -i $(upower -e | grep BAT)

# 下面是Dell特定方法
# 安装Dell Linux工具
sudo apt install smbios-utils

# 查看当前配置
sudo smbios-battery-ctl --get-charging-cfg

# 设置为主要使用交流电源
sudo smbios-battery-ctl --set-charging-mode=primarily_ac

#设置为硬性阈值
sudo smbios-battery-ctl --set-charging-mode=custom
sudo smbios-battery-ctl --set-custom-charge-interval=50 80

```

# 字体
## 常用字体
宋体和黑体直接从win复制过来`simsun.ttc` `simhei.ttf`
```bash

```
微软的 corefonts（包含 Times New Roman, Arial, Courier New 等），你可以通过终端直接安装。
```bash
sudo apt update
sudo apt install ttf-mscorefonts-installer
```
更新字体缓存
```bash
sudo fc-cache -f -v
```