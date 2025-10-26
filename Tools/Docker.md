---
tags: [Ubuntu]
title: Docker
created: '2025-08-02T11:18:28.290Z'
modified: '2025-10-16T16:18:24.259Z'
---

Docker
# 代理
## 拉取镜像代理（守护进程配置代理）
```bash
sudo mkdir -p /etc/systemd/system/docker.service.d
sudo gedit /etc/systemd/system/docker.service.d/http-proxy.conf 
#写入
```
```ini
[Service]
Environment="HTTP_PROXY=127.0.0.1:7890"
Environment="HTTPS_PROXY=127.0.0.1:7890"
```
```bash
#重启
sudo systemctl daemon-reload
sudo systemctl restart docker
#验证
systemctl show --property=Environment docker
```
`NO_PROXY`用于指定不需要通过代理访问的地址
