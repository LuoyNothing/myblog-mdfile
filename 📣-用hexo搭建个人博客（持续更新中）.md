---
title: 📣 用hexo搭建个人博客（持续更新中）
date: 2023-08-30
categories: 前端
tags: 个人博客
comments: true
---

<meta name="referrer" content="no-referrer"/>

本文记录自己搭建个人博客的历程，欢迎收看~

# 📚 搭建基础的个人博客
> **前提：需安装了git 和 nodejs**

1. 安装hexo。先新建一个文件夹，在该文件夹下打开git bash，然后运行`npm install -g hexo-cli`
  
  <p align=center><img src="https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/5cf3229ac3df4442b4be56bd18e0aea4~tplv-k3u1fbpfcp-jj-mark:0:0:0:0:q75.image#?w=708&h=353&s=35036&e=png&b=f7f7f7" width="50%"/></p>
  
2. 初始化hexo，命令为：`hexo init` ，出现下图结果就表示初始化成功！

  <p align=center><img src="https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/a26b0a3e34474736ad89da964b780fce~tplv-k3u1fbpfcp-jj-mark:0:0:0:0:q75.image#?w=722&h=101&s=10725&e=png&b=000000" width="70%"/></p>
  
  新建完成后，在路径下会产生一些文件和文件夹：
  
  <p align=center><img src="https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/6b966396263f42a8b814307a95898acc~tplv-k3u1fbpfcp-jj-mark:0:0:0:0:q75.image#?w=802&h=319&s=29387&e=png&b=fffefe" width="50%" /></p>
  
  

-   `_config.yml`：俗称站点配置文件，很多与博客网站的格式、内容相关的设置都需要在里面改。
-   `node_modules`:存储Hexo插件的文件，可以实现各种扩展功能。一般不需要管。
-   `package.json`：相关描述的，比如名字、版本。
-   `scaffolds`：模板文件夹，里面的`post.md`文件可以设置每一篇博客的模板。具体用起来就知道能干嘛了。
-   `source`：非常重要。所有的个人文件都在里面！
-   `themes`：主题文件夹，可以从[Hexo主题官网](https://link.juejin.cn?target=https%3A%2F%2Fhexo.io%2Fthemes%2F "https://hexo.io/themes/")或者网上大神的Github主页下载各种各样美观的主题，让自己的网站变得逼格高端的关键！


3. 启动服务器

命令为：`hexo server`，或者简写：`hexo s`，然后打开浏览器，在地址栏输入：localhost:4000回车就可以得到如下结果：(ctrl+c可关闭服务)

<p align=center><img src="https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/f108fb71f11e48a393a221ea96c47829~tplv-k3u1fbpfcp-jj-mark:0:0:0:0:q75.image#?w=1844&h=1084&s=647678&e=png&b=f4f3f3" alt="image.png" width="50%" /></p>

至此，您的Hexo博客已经搭建在本地。

4.上传到github

在github创建仓库，仓库名为：<Github账号名称>.github.io（必须是这个，否则后续打不开）。安装`hexo-deployer-git`插件。在命令行（即Git Bash）运行以下命令即可（也可以走淘宝镜像，淘宝镜像就是换成cnpm）：

```
npm install hexo-deployer-git --save
```
添加SSH key，如果已添加可以不用管。如果未添加，可以参考[添加SSH key](https://www.liaoxuefeng.com/wiki/896043488029600/896954117292416)，我这里已经添加，接着下一步；

5. 修改`_config.yml`（在站点目录下）。文件末尾修改为：
```
# Deployment
## Docs: https://hexo.io/docs/one-command-deployment
deploy:
  type: git
  repo: git@github.com:LuoyNothing/LuoyNothing.github.io.git
  branch: main
```
6.生成页面并上传到github

```
// 生成页面：
hexo g
// 上传到github: 
hexo d
```
执行完上面两个命令，并出现下图结果即表示上传成功。

<p align=center><img src="https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/22d714419ddf40fc9c44f7d6ac4a8eb8~tplv-k3u1fbpfcp-jj-mark:0:0:0:0:q75.image#?w=722&h=303&s=44296&e=png&b=000000" width="50%" /></p>

至此，您的Hexo博客已经搭建在GitHub上，访问域名为：https://luoynothing.github.io/

<p align=center><img src="https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/fe722b935d254d849c4a5f8a24f29300~tplv-k3u1fbpfcp-jj-mark:0:0:0:0:q75.image#?w=1920&h=1086&s=911964&e=png&b=f5f4f4" width="50%" /></p>

访问博客，开始的页面是初始化页面，没有做美化和增加内容。

## 🌸 域名绑定

还未绑定


# 📚 文档学习

官网文档：[文档 | Hexo](https://hexo.io/zh-cn/docs/)

## 🌸 修改主题
我的博客修改的主题是fluid（[ Hexo Fluid 用户手册](https://hexo.fluid-dev.com/docs/start/)）,github([fluid Hexo 主题](https://github.com/fluid-dev/hexo-theme-fluid))，以下是详细步骤：

1. 下载主题

**方式一**：推荐通过 npm 直接安装，进入博客目录执行命令：`npm install --save hexo-theme-fluid`

然后在博客目录下创建 `_config.fluid.yml`，将主题的_config.yml内容复制过去。

**方式二**：下载 [最新 release 版本](https://github.com/fluid-dev/hexo-theme-fluid/releases)解压到 themes 目录，并将解压出的文件夹重命名为 `fluid`。

我采用的是方式二。

2. 然后采用hexo三连，就可以在本地查看到主题修改
```
// 清除缓存文件 `db.json` 和已生成的静态文件 `public`。
hexo cl 
// 生成网站静态文件到默认设置的 `public` 文件夹。
hexo g
// 启动本地服务器，用于预览主题。
hexo s
```
下图表示换主题成功！然后可以用`localhost:4000`来访问个人博客

<p align=center><img src="https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c5643b5e6987401997f520c8cad74c84~tplv-k3u1fbpfcp-jj-mark:0:0:0:0:q75.image#?w=722&h=631&s=57034&e=png&b=000000" width="50%" /></p>

3. 部署到github上：

hexo三连：
```
// 清除缓存文件 `db.json` 和已生成的静态文件 `public`。
hexo cl 
// 生成网站静态文件到默认设置的 `public` 文件夹。
hexo g
// 部署到远程仓库里
hexo d
```
然后可以用https://luoynothing.github.io/ 来访问个人博客了。

## 🌸 发布文章 

1.新建md文件。在网站根目录下git bash，输入`hexo new <title>`，执行该命令，Hexo会在`/source/_posts`目录下创建一篇新的文章。

2.上传到github，就是hexo三连操作。

```
// 清除缓存文件 `db.json` 和已生成的静态文件 `public`。
hexo cl 
// 生成网站静态文件到默认设置的 `public` 文件夹。
hexo g
// 部署到远程仓库里
hexo d
```



# 📚 博客更新说明

**2023-8-30**	

1.成功搭建博客

2.博客文章：

​	1.封面字段：标题、发布时间、关键字

​		摘要：去掉摘要

​	2.封面进去：发布时间、更新时间、字数、阅读时长​

3.标签和分类：

分类1：前端

​	子类：html css等

分类2：持续更新

标签：相当于关键字吧，里面的某个知识点

4.博客中的图片不显示问题



