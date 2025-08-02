---
tags: [Ubuntu]
title: Clion
created: '2025-07-26T11:45:53.505Z'
modified: '2025-07-26T12:14:46.545Z'
---

Clion

[一篇csdn](https://blog.csdn.net/caiqidong321/article/details/130126200)

# 安装
1. [下载压缩包](https://www.jetbrains.com/clion/)
2. 解压
3. 解压后文件夹移至/opt
```bash
sudo cp -rf ./CLion-2025.1.4/ /opt
# 这是copy命令
```
4. 在移动后`clion-2025.1.4/bin`路径下
```bash
sh clion.sh
```
5. 在**Tools**中创建快捷入口

# 更新
1. 上面的1至4步相同
2. 删除旧的clion
```bash
sudo rm -rf clionxxxxx
```
3. 取消收藏夹中的clion
4. 在显示应用程序（即右下角）中搜索clion，重新添加至收藏夹即可
