---
title: 📣 git基本操作（下），欢迎食用~
date: 2023-08-31 23:19:51
tags: git
---

<meta name="referrer" content="no-referrer"/>

本篇是学习([廖雪峰Git学习](https://link.juejin.cn/?target=https%3A%2F%2Fwww.liaoxuefeng.com%2Fwiki%2F896043488029600%2F898732864121440 "https://www.liaoxuefeng.com/wiki/896043488029600/898732864121440"))所写的学习总结笔记，方便自己后续回顾复习。

# 📚 远程仓库
在上篇中学到的git功能，其实在集中式版本管理系统中也能实现。Git是分布式版本控制系统，同一个Git仓库，可以分布到不同的机器上。下面介绍一下git杀手级功能之一：远程仓库。

首先需要先注册github账号，github是提供Git仓库托管服务的，所以只要注册一个GitHub账号，就可以免费获得Git远程仓库。由于你的本地Git仓库和GitHub仓库之间的传输是通过SSH加密的，所以需要一点设置：

**第1步：创建SSH Key。**

在用户主目录下（我的电脑C:\Users\Administrator），看看有没有.ssh目录，如果有，再看看这个目录下有没有`id_rsa`和`id_rsa.pub`这两个文件，如果已经有了，可直接跳到下一步。如果没有，打开Shell（Windows下打开Git Bash），创建SSH Key：
```复制代码
ssh-keygen -t rsa -C "填写你的邮箱"
```
你需要把邮件地址换成你自己的邮件地址，然后一路回车，使用默认值即可，由于这个Key也不是用于军事目的，所以也无需设置密码。
<p align=center><img src="https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/a216ec3ad4594c3fba913f6996d8c3fa~tplv-k3u1fbpfcp-jj-mark:0:0:0:0:q75.image#?w=722&h=79&s=11141&e=png&b=000000" width="70%" /></p>

可以在用户主目录里找到`.ssh`目录，里面有`id_rsa`和`id_rsa.pub`两个文件，这两个就是SSH Key的秘钥对，`id_rsa`是私钥，不能泄露出去，`id_rsa.pub`是公钥，可以放心地告诉任何人。

**第2步：登陆GitHub，增加SSH Keys**

步骤为：①setting--> ②SSH and GPG keys --> ③new SSH key

填上任意Title，在Key文本框里粘贴`id_rsa.pub`文件（公钥）的内容即可

> 为什么GitHub需要SSH Key呢？
>
> 因为GitHub需要识别出你推送的提交确实是你推送的，而不是别人冒充的，而Git支持SSH协议，所以，GitHub只要知道了你的公钥，就可以确认只有你自己才能推送。

当然，GitHub允许你添加多个Key。假定你有若干电脑，你一会儿在公司提交，一会儿在家里提交，只要把每台电脑的Key都添加到GitHub，就可以在每台电脑上往GitHub推送了。

## 🌸 添加远程仓库
**本地仓库-->远程仓库**

现在你在本地有一个git仓库，然后你想在github新建一个git远程仓库并让两个仓库进行同步，这样github上的仓库既可以用于备份，也可以让其他人通过该仓库进行协作。

**1.在github上新建仓库，名字可以和本地仓库不同。**

新建仓库后可以根据GitHub给的提示来进行操作，提示如下：

<p align=center><img src="https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/b313b7b908a848fc8a0910284548378c~tplv-k3u1fbpfcp-jj-mark:0:0:0:0:q75.image#?w=898&h=162&s=24628&e=png&b=f5f8fa"  width="70%"/></p>

在本地仓库git bash中运行下列代码（根据自己的远程仓库提示来操作）：

```复制代码
git remote add origin git@github.com:LuoyNothing/mygit.git
```
添加后，远程库的名字就是`origin`，这里的**origin为本地客户端认为的远程仓库的名字**，也可以改成别的，但是`origin`这个名字一看就知道是远程库。

> 在多人协作的时候，每个人都有自己的git本地客户端和本地仓库，每个人都可以给同一个远程仓库在本地指定不同的名字。
>
> 只不过，origin是git客户端默认的远程仓库的名字，如果我们在关联时将远程仓库的名字指定为origin，在push的时候可以不指定远程仓库的名字，默认push到origin关联的远程仓库。如果修改了名字，在push的时候必须写上指定的远程仓库的名字。

**2.把本地库的所有内容推送到远程库上**

在本地仓库git bash中接着运行：
```
git push -u <远程分支> <本地分支>
git push -u origin master
```
把本地库的内容推送到远程，用`git push`命令，实际上是把当前分支`master`推送到远程。

由于远程库是空的，我们第一次推送`master`分支时，加上了`-u`参数，Git不但会把本地的`master`分支内容推送的远程新的`master`分支，还会把本地的`master`分支和远程的`master`分支关联起来，在以后的推送或者拉取时就可以简化命令。

推送步骤完成。
以后在本地仓库进行修改后要推送到远程仓库，直接执行`git push origin master`

把本地`master`分支的最新修改推送至GitHub，现在，你就拥有了真正的分布式版本库！

## 🌸 删除远程仓库

**1.解绑远程仓库和本地仓库连接**

可以先查看一下远程库信息：`git remote -v`。然后根据名字删除，比如删除origin：`git remote rm origin`

**2.在github上真正删除远程仓库**

## 🌸 从远程仓库克隆

使用`git clone 地址`就可以克隆完成。地址中Git支持多种协议，包括`https`，但`ssh`协议速度最快。
# 📚 分支管理
## 🌸 分支的理解

在开发一个项目的时候，团队负责人会给每个团队成员划分不同的任务。如果每个人都在主分支上进行项目开发，这样会影响其他人的工作。因此为了不影响其他人的工作，可以每个人新开一个分支来完成自己的任务，最后测试没问题再合并到主分支上，最后所有人的任务分支都合并到主分支上则可完成项目协作开发。当然实际开发中，可能有些许不同，比如按照任务来新建分支，然后安排某人来开发这个分支，或者几个人负责一个分支，然后根据提交的情况来查看每个人的工作量。

每个人都有本地仓库和远程仓库，一般在项目开发中，自己本地开发完之后提交到远程仓库中属于自己的分支，避免数据遗失。

每一次commit都会有提交描述和提交时间，git会将这些commit根据提交时间来串成一个时间线。截止目前只有一个时间线，在git里叫主分支，名字为master。

`HEAD`严格来说不是指向提交，而是指向`master`，`master`才是指向提交的，所以，`HEAD`指向的就是当前分支。一开始的时候，`master`分支是一条线，Git用`master`指向最新的提交，再用`HEAD`指向`master`，就能确定当前分支，以及当前分支的提交点：

<p align=center><img src="https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/01449c510d5d48e9bc10c9754f7fdb36~tplv-k3u1fbpfcp-jj-mark:0:0:0:0:q75.image#?w=1098&h=534&s=27587&e=png&b=ffffff" width="50%" /></p>

每一次提交，master分支都会向前走一步，随着提交次数的增多，master分支就越来越长。

## 🌸 创建与合并分支

创建一个新分支，名字为：dev。


```
// 创建分支dev
git branch dev
// 切换分支dev
方式一：git checkout dev
方式二：git switch dev
// 创建并切换分支
方式一：git checkout -b dev
方式二(更语义，和前面撤销工作区的更新不产生冲突)：git switch -c dev
// 查看当前所有分支
git branch
```

当创建了分支dev之后，Git新建了一个指针叫`dev`，指向`master`相同的提交，再把`HEAD`指向`dev`，就表示当前分支在`dev`上：

<p align=center><img src="https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e01ac7674c024d04950a2243a3325493~tplv-k3u1fbpfcp-jj-mark:0:0:0:0:q75.image#?w=1098&h=698&s=32261&e=png&b=ffffff" width="50%"/></p>

从现在开始，对工作区的修改和提交就是针对`dev`分支了，比如新提交一次(add+commit)后，`dev`指针往前移动一步，而`master`指针不变：

<p align=center><img src="https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/4ae82b830d984b0faf27135813427461~tplv-k3u1fbpfcp-jj-mark:0:0:0:0:q75.image#?w=1468&h=670&s=40357&e=png&b=ffffff" alt="image.png" width="50%" /></p>

假如我们在`dev`上的工作完成了，就可以把`dev`合并到`master`上。Git怎么合并呢？最简单的方法，就是直接把`master`指向`dev`的当前提交，就完成了合并：
```
// `git merge`命令用于合并指定分支到当前分支。
git merge dev
```
这次合并是“快进模式”，也就是直接把`master`指向`dev`的当前提交，所以合并速度非常快。
<p align=center><img src="https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e57e9c6356bf4c0fa36d8541f4d8f344~tplv-k3u1fbpfcp-jj-mark:0:0:0:0:q75.image#?w=1468&h=658&s=40546&e=png&b=ffffff"  width="50%"/></p>

合并完分支后，甚至可以删除`dev`分支。删除`dev`分支就是把`dev`指针给删掉，删掉后，我们就剩下了一条`master`分支：
```
// 删除分支dev
git branch -d dev
```
因为创建、合并和删除分支非常快，所以Git鼓励你使用分支完成某个任务，合并后再删掉分支，这和直接在`master`分支上工作效果是一样的，但过程更安全。

## 🌸 解决冲突

## 🌸 分支管理策略




# 📚 命令汇总
- 远程仓库
    - 连接本地仓库和远程仓库：`git remote add origin git@github.com:LuoyNothing/mygit.git`
    - 第一次推送到远程仓库：`git push -u origin master`
    - 后续更新推送：`git push origin master`
    - 查看远程库信息：`git remote -v`
    - 删除本地仓库和远程仓库的连接：`git remote rm origin`
    - 从远程仓库克隆：`git clone 地址`
- 分支
    - 创建与合并分支
        - 创建分支：`git branch <name>`
        - 切换分支：`git switch <name>`
        - 创建并切换分支：`git switch -c <name>`
        - 合并分支：`git merge <name>`
        - 删除分支：`git branch -d <name>`




下篇在此结束，您花了5分钟又复习了一次相关知识，如果对你还有一点帮助的话，不妨给个小赞鼓励一下吧😊，感谢观看！
