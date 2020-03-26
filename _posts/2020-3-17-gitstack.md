---
layout: 		post
title: 			"Gitstack"
subtitle: 		'代码托管'
author: 		"CJ"
header-img: 	"img/post-bg-tools.jpg"
header-mask: 	0.3
catalog: 		true
mathjax:        true
tags:
  - 代码辅助工具
---

## 安装
进入[传送门](https://gitstack.com/)，找到下方的下载，然后点击安装(需要释放80端口)，如果发现80端口占用，可以使用命令`netstat -ano|findstr 80`找到占用进程，然后进任务管理器kill🔪掉。

![](/img/in-posts/20200317-gitstack-1.png)

之后的事就很容易了，在`Respositories`创建仓库，然后创建几个用户给自己的小伙伴，拉一个项目的`group`，然后加入某个项目。

新创建的项目克隆到本机，然后就是git正常的操作了。

🌟push到远程仓库需要输入的是项目里的成员用户名和密码，如果多次输错无法更改就用清除命令`credential-manager uninstall`清除缓存的用户名与密码。

## git用法总结
#### 用户信息
第一次使用需要配置用户信息
git config --global user.name "<用户名>"
git config -- global user.email <邮箱地址>

然后就能用下面的命令查看(一般文件在主目录的.gitconfig)
git config --list

🌟单项目如果要调整配置信息就去掉globa

git help <操作码> 🌰：git help config

#### 正常操作
目录的几个命令
ls 显示当前文件夹文件
cd <路径名>|.. 进入该目录|上级目录

git init 当前目录初始化

git clone <地址> 将已有远程仓库项目下载到本地

git pull 从远程仓库拉取更新

git push origin master 向远程仓库提交代码

git add <文件名>|. 将文件加入暂存区|所有文件

git commit -m '<描述信息>' 提交更新(-m前加-a可以跳过add的步骤)

git status 各子文件所处的状态

git log 查看日志

git mv <文件名> <新文件名> 文件重命名

git rm <文件名> 删除文件

git reset HEAD <文件名>

git checkout -- <文件名> 撤销内容操作到上一个版本(慎用，会数据丢失)

![](/img/in-posts/20200317-file-status.png)

#### 分支操作
git branch <分支名> 在当前commit对象上创建分支
git checkout <分支名> 切换分支
git merge <分支名> 合并分支
git branch -d <分支名> 删除分支

应用场景：我现在有一个网站,里面有原有内容，我这时候有个新的需求要做，创建一个newReq分支(git branch newReq)，同时我有一个bug要修复，创建一个bug1分支(git branch bug1)，我修复了bug1，切回master然后合并bug1和主支，当我再做newReq如果操作了同一个文件夹，就会出现冲突。
![](/img/in-posts/20200318-branch.png)
git利用`<<<<<<<`，`=======`，`>>>>>>>`标记不同分支的内容，修改之后提交就能成功合并了。

bug修复
先用`git stash`保存工作现成，创建临时分支，修复完提交，然后记录下提交的hash码，进入`git cherry-pick <hash码>`，然后使用`git stash pop`回到工作现场，修复冲突之后提交，可以合并主支。
![](/img/in-posts/20200318-cherry-pick.png)