---
tags: [Home]
title: Home服务机器人笔记
created: '2025-09-16T10:47:41.869Z'
modified: '2025-09-16T13:50:29.968Z'
---

Home服务机器人笔记

# compreface
镜像文件compreface-all-images，yml文件， .env, sdk（U盘为准）

使用docker时确保路径无中文

## docker安装与配置
顺便安装nvidia-container-toolkit

1. 添加container软件源和秘钥
```bash
distribution=$(. /etc/os-release;echo $ID$VERSION_ID) \
    && curl -fsSL https://nvidia.github.io/libnvidia-container/gpgkey | sudo gpg --dearmor -o /usr/share/keyrings/nvidia-container-toolkit-keyring.gpg \
        && curl -s -L "https://nvidia.github.io/libnvidia-container/$distribution/libnvidia-container.list" | \
                sed 's#deb https://#deb [signed-by=/usr/share/keyrings/nvidia-container-toolkit-keyring.gpg] https://#g' | \
                        sudo tee /etc/apt/sources.list.d/nvidia-container-toolkit.list
```

2. 安装
```bash
sudo apt update
sudo apt install docker docker-compose nvidia-container-toolkit
```

3. 配置docker
```bash
sudo usermod -aG docker $USER
reboot  #重启
```

```bash
sudo systemctl status docker
# 如果未运行，启动服务
sudo systemctl start docker
sudo systemctl restart docker
#检查
docker ps
```

```bash
sudo nvidia-ctk runtime configure --runtime=docker
sudo systemctl restart docker

#验证 
docker run --rm --gpus all nvidia/cuda:11.0-base nvidia-smi
 
```

## 启动容器
```bash
docker load -i compreface-all-images.tar #导入镜像

docker-compose up -d
```

## 调用api
```bash
#如需，先创建环境
pip install opencv-python==4.1.2.30
pip install "urllib3<2.0"
```

修改api-key，即可使用


```bash
docker load -i compreface-all-images.tar


```
