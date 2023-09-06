---
title: 📣 git基本操作（上），命令总结清单在最后
date: 2023-08-31 00:09:48
tags: git
categories: 前端
---

<meta name="referrer" content="no-referrer"/>

本篇是学习([廖雪峰Git学习](https://www.liaoxuefeng.com/wiki/896043488029600/898732864121440))所写的学习总结笔记

# 📚 git简介
git 是一个版本控制工具，可以用于团队协作。git可以记录之前修改过的内容版本，方便在需要的时候回退到之前的版本，还支持团队内部进行协作更新内容。

用起来大概就是下面这样子，可以记录修改的版本，谁修改的，修改了哪些内容以及日期：

<p align=center><img src="https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/ecd727d76fe64229bfd2e1d715d2fd02~tplv-k3u1fbpfcp-jj-mark:0:0:0:0:q75.image#?w=1154&h=335&e=png&b=ffffff" width:"50%" /></p>

Git是分布式版本控制系统，分布式版本控制系统根本没有“中央服务器”，每个人的电脑上都是一个完整的版本库，这样，你工作的时候，就不需要联网了，因为版本库就在你自己的电脑上。

Git还具有极其强大的分支管理

# 📚 git安装
在这里只描述windows上安装git

在Windows上使用Git，可以从Git官网直接[下载安装程序](https://git-scm.com/downloads)，然后按默认选项安装即可。

安装完成后，在开始菜单里找到“Git”->“Git Bash”，蹦出一个类似命令行窗口的东西，就说明Git安装成功！

安装完成后，还需要最后一步设置，在命令行输入：

```
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```

因为是分布式版本控制系统，所以需要知道你是谁。注意`git config`命令的`--global`参数，用了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置，当然也可以对某个仓库指定不同的用户名和Email地址。

## 🌸 名词解释
- **工作区**：本地电脑存放文件的文件夹

- **暂存区(index/stage)**：在使用git管理项目文件的时候，其本地的项目文件会多出一个.git的文件夹，将这个.git文件夹称之为版本库。版本库中包含2个部分，一部分就是暂存区,顾名思义就是暂时存放文件的地方，通常使用add命令将工作区的文件添加到暂存区里；

- **本地仓库**：.git文件夹里还包括git自动创建的第一个分支：master，并且将HEAD指针指向master分支。使用commit命令可以将暂存区中的文件添加到本地仓库中；

- **远程仓库**：不是在本地仓库中，项目代码在远程git服务器上，比如项目放在github上，就是一个远程仓库，通常使用clone命令将远程仓库拷贝到本地仓库中，更新后推送到远程仓库中即可；

  <p align=center><img src="https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/f1e326bcd19941c1816661245c2a40e8~tplv-k3u1fbpfcp-jj-mark:0:0:0:0:q75.image#?w=795&h=427&e=png&b=fdfdfd"  width="50%"/></p>

你可以简单理解为，需要提交的文件修改通通放到暂存区，然后，一次性提交暂存区的所有修改。

## 🌸 本地仓库

**1.创建版本库：**
    什么是版本库呢？英文名**repository**，可以简单理解为一个文件夹，该文件夹下的文件都可以被Git管理起来。

通过`git init`命令将这个文件夹变为git可以管理的仓库。建好仓库之后，会出现一个.git文件，该文件是git跟踪管理版本库的，千万不能修改！如果没有该文件，说明是默认隐藏的，输入`ls -ah`就可以看见。

**2.在版本库中加文件**

所有的版本控制系统其实只能监控文本文件的改动，比如txt文件，网页，所有的程序代码等，git也不例外。而图片、视频这些二进制文件，虽然也能用版本控制系统管理，但是不能跟踪文件的变化，word文件也是二进制文件。

接下来就是上次文件的步骤：首先新建一个readme.txt文件，并随便写入一些内容
- `git add readme.txt`
- `git commit -m "write readme txt"`

`git add readme.txt` 表示告诉git,将文件添加到暂存区中，无输出则成功。也可以采用`git add .`表示添加变更的文件到暂存区；

`git commit -m "本次提交的说明"` 表示告诉git，将代码提交到仓库，后面附带对本次提交的说明。该语句执行完会返回一个文件被修改，插入了n行内容（取决于你写了多少内容）。为什么Git添加文件需要`add`，`commit`一共两步呢？因为`commit`可以一次提交很多文件，所以你可以多次`add`不同的文件。

<img src="https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/70ca0240e2ca4c1193b646f0e9a1df1d~tplv-k3u1fbpfcp-jj-mark:0:0:0:0:q75.image#?w=722&h=156&e=png&b=000000" width="50%" />

如果文件有修改，则再执行以上2个步骤即可。

# 📚 时光穿梭机

## 🌸 版本回退

要回到之前的版本，我们可以使用`git log --pretty=oneline`命令显示从最近到最远的提交日志。

<p align=center><img src="https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e6d23155076742b1a7dcace8365cc55f~tplv-k3u1fbpfcp-jj-mark:0:0:0:0:q75.image#?w=722&h=84&e=png&b=000000"  width="70%"/></p>

首先，Git必须知道当前版本是哪个版本，在Git中，用`HEAD`表示当前版本。假如我们要回到第一版本，可以使用`git reset --hard 版本号`，版本号就是黄色的那一个字符串。

1.回退到第一版本，当前在第三版本

<img src="https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/7111c1745a1242c29dd0e5c9f5818686~tplv-k3u1fbpfcp-jj-mark:0:0:0:0:q75.image#?w=722&h=362&s=52170&e=png&b=000000" width="50%" />

2.回退到第三版本，当前在第一版本

<img src="https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/94fd6cce736346f5941d55d1530a7ee8~tplv-k3u1fbpfcp-jj-mark:0:0:0:0:q75.image#?w=722&h=157&e=png&b=000000" width="50%" />

3.如果想回到新的版本，但是找不到版本号：可以使用git reflog来查看你的每一次命令（从近到远）

<img src="https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/7f53986ed2b84dca806390fe52c19b8b~tplv-k3u1fbpfcp-jj-mark:0:0:0:0:q75.image#?w=722&h=410&e=png&b=000000" width="50%" />

在上图中就可以找到最新版本的版本号，版本号可以不写全，但也不能写太少，防止版本号重复。

## 🌸 撤销修改
`git checkout -- file`可以丢弃工作区的修改，意思就是，把文件在工作区的修改全部撤销，这里有两种情况：
- 文件自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；利用`cat`命令可以查看文件里的内容，这里要撤销最新的修改，最后一行（已成功）
  
  <p align=center><img src="https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/9163aac12fa247a9b317752e7513c3e9~tplv-k3u1fbpfcp-jj-mark:0:0:0:0:q75.image#?w=483&h=233&e=png&b=000000"  width="50%" /></p>
  
- 文件已经添加到暂存区(stage)。可以使用`git reset HEAD 文件名+后缀`来把暂存区的修改撤销掉（unstage），重新放回工作区。然后`git checkout -- file`即可

  <p align=center><img src="https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/71d07765f66a4466b52c60ee8848975e~tplv-k3u1fbpfcp-jj-mark:0:0:0:0:q75.image#?w=459&h=386&e=png&b=000000"  width="40%"/></p>

现在，假设你不但改错了东西，还从暂存区提交到了版本库，怎么办呢？还记得版本回退吗？可以回退到上一个版本。不过，这是有条件的，就是你还没有把自己的本地版本库推送到远程，如果提交到远程仓库就G啦。

## 🌸 删除文件
在工作区删除文件之后，工作区和版本库就不一样了，git status可以告知你删除了什么文件。下面分为2种情况
- 确实要删除文件，在版本库中也有删除。则直接用命令`git rm <file>`删掉，并且`git commit`
- 如果是误删。在工作区删除了文件，但是版本库中还有，则恢复文件：`git checkout -- <file>`。`git checkout`其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”。

> 【注】未添加到版本库的文件被删除掉是不能被恢复的！

常见错误的解决办法：

```git
//取消http代理
git config --global --unset http.proxy
//取消https代理 
git config --global --unset https.proxy

git config --global http.sslVerify "false"
```



## 🌸 命令总结：

- 初始化版本库

    - `git init` 创建版本库
- 添加文件
    - `git add <file>` 将文件加入版本库，`git add .`添加所有的变更文件到暂存区
    - `git commit -m "提交说明内容"` 将文件提交到版本库
- 回退文件版本
    - `git status` 查看仓库当前的状态
    - `git diff 文件名+后缀` 查看某文件的更改内容
    - `git log` 显示从最近到最远的提交日志，`git log --pretty=oneline`显示的内容更精简。
    - `git reset --hard 版本号` 回退到某个版本
    - `git reflog` 如果不知道版本号，可以查看之前使用过的命令，从而找到版本号
- 撤销修改
    - `git checkout -- <file>`可以丢弃工作区的修改
    - `git reset HEAD 文件名+后缀`来把暂存区的修改撤销掉（unstage）

上篇在此结束，您花了5分钟又学到了新的知识，如果对你还有一点帮助的话，不妨给个小赞鼓励一下吧😊，感谢观看！