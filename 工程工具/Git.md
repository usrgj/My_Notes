---
tags: [tools]
title: Git
created: '2025-04-19T12:58:31.503Z'
modified: '2025-08-02T12:02:34.417Z'
---

Git

[Tutorial](https://liaoxuefeng.com/books/git/introduction/index.html)

# 0简介
也许第一次使用git，就是复制粘贴使用了下面的命令
```bash
git clone https://github.com/username/repositorie.git
```
简单说明一下，行的意思是，克隆github上名为`usrname`用户下的名`repositorie`的仓库里的东西

git是什么?github是什么?有什么关系?

通俗地说,git是一个版本控制系统,而github是一个给你存放文件的仓库



### Note

git只能追踪纯文本的变化

### 配置本地信息

`$ git config --global user.name "Your Name"`

`$ git config --global user.email "email@example.com"`

### 初始化目录，使其能被git管理

`$ git init`

### 添加文件到git仓库

`$ git add <file>`可同时多个文件  , 这一步其实是将文件提交至暂存区

`$ git commit -m <message>`message是说明，如  `"wrote a readme file"`；这一步提交为一个版本库

### 查看当前仓库的状态

`$ git status`

### 查看修改了什么

`$ git diff`

### 查看每个版本库的信息

`$ git log`

pull

merge

commit

 git push -u origin dev 

### [**submodule**](https://blog.csdn.net/The_friends/article/details/144848995)

添加子模块

在自己仓库目录下打开终端

```plaintext
git submodule add <子模块 URL> <子模块目录>
//子模块目录可选，若空，则添加整个库
 
git submodule add htps://github.com/xxx/abc.git abc
```

创建目录

`$ mkdir <dirname>`

到某个目录

`$ cd <path>`

显示当前目录

`$ pwd`



`git submodule update --init --recursive `
