---
tags: [通识]
title: ssh
created: '2025-09-11T13:02:17.098Z'
modified: '2025-09-11T13:13:16.612Z'
---

ssh

ubuntu生成ssh
```bash
ls ~/.ssh/  #检查是否有秘钥

mkdir ~/.ssh # 如果没有秘钥

ssh-keygen -t rsa -b 4096 -C "your_email@example.com" #生成秘钥文件，邮箱仅作为秘钥的注释信息

eval "$(ssh-agent -s)" #启用ssh-agent

ssh-add ~/.ssh/id_rsa #添加私钥

ssh -T git@github.com #测试，例如对于 GitHub
```
复制`~/.ssh/id_rsa.pub`中的内容即为秘钥

ubuntu删除ssh
```bash
eval "$(ssh-agent -k)" #停止 ssh-agent

rm -rf ~/.ssh/ #如果在该路径
```
