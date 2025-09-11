---
tags: [tools]
title: Git
created: '2025-04-19T12:58:31.503Z'
modified: '2025-09-11T12:59:33.795Z'
---

Git

[Tutorial](https://liaoxuefeng.com/books/git/introduction/index.html)

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


`git checkout -b <new branch name>`创建新分支，并切换到新分支


`git submodule update --init --recursive `

### clone
克隆时选择的urls将作为关联远程地址，后续与远程仓库交互时，都使用该urls对应的协议等
比如说，通过https克隆，则无法通过ssh推送

### ssh
本地生成ssh后，在github添加秘钥
即可通过ssh克隆和推送


|操作|命令|说明|
|---|---|---|
| **查看当前远程仓库** | `git remote -v`                                                     | 显示已关联的远程仓库地址（如 `origin`）。                           |
| **移除旧远程仓库**   | `git remote remove <rep name>`                                          | 解除与旧仓库的连接（若远程名不是 `origin`，替换为对应的名称）。      |
| **添加新远程仓库**   | `git remote add origin <新仓库URL>`                                  | 关联新仓库，例如：<br>`git remote add origin https://github.com/user/new-repo.git` |
| **推送代码到新仓库** | `git push -u origin <分支名>`<br>（如 `git push -u origin main`）    | 首次推送需加 `-u` 关联分支，后续可直接用 `git push`。               |
| **强制推送**（慎用） | `git push -f origin <分支名>`                                       | 覆盖远程仓库历史（需谨慎操作）。                                     |



