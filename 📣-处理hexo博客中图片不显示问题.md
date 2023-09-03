---
title: 📣 处理hexo博客中图片不显示问题
date: 2023-08-31 17:37:33
categories: 个人博客
tags: 个人博客
comments: true
---

<meta name="referrer" content="no-referrer"/>

在解决这个问题的过程中，我经历了三个阶段，很磨人最终还是回到了起点，发现最初的方法最好，如果赶时间，可以直接看第三个阶段。

# 🌸第一阶段：将图片保存在本地

搭建好个人博客网站之后，写了两篇markdown文章（这时候我图片用的是网络地址），然后按照hexo三连上传了文章，最后在浏览器打开发现图像不显示：

<p align=center><img src="https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/68a0dd8fb049474f93f6d088d8dc2471~tplv-k3u1fbpfcp-jj-mark:0:0:0:0:q75.image#?w=984&h=235&s=32490&e=png&b=fbfbfb" width="60%" /></p>

一般图片显示不出来很大的原因是路径不对。于是我去查看了图片路径，确实找不到相应的图片。然后我参考[相关资料](http://etrd.org/2017/01/23/hexo%E4%B8%AD%E5%AE%8C%E7%BE%8E%E6%8F%92%E5%85%A5%E6%9C%AC%E5%9C%B0%E5%9B%BE%E7%89%87/)了解到`hexo g`指令是将md文件生成html页面，然后每篇博文生成的html页面最后都是放在用年月日做文件夹的下面，例如：`E:\myblog\public\2023\08\31\test`。

下面是我参考[养恐龙](https://leay.net/2019/12/25/hexo/)、[ETRD](http://etrd.org/2017/01/23/hexo中完美插入本地图片/)、[金牛大王](https://blog.csdn.net/m0_43401436/article/details/107191688)三位的回答，最终解决了我的问题。

**第一步**：确保你的Hexo的配置文件\_config.yml里面有这个选项配置，并将其置为true

    post_asset_folder: true

这个功能实际上是Hexo官方文档中提到的资源文件夹功能，它的作用在于当你使用`hexo n "文章名"`生成一篇新文章时，会在`\source\_posts`目录下生成一个 文章名.md 文件外，附带生成一个与 文章名 同名的文件夹，可以用它来存放这篇文章的所有资源，比如图片，附件等。

<p align=center><img src="https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/66e0f2f20d7f4791a68b3973bf2f2734~tplv-k3u1fbpfcp-jj-mark:0:0:0:0:q75.image#?w=758&h=225&s=31200&e=png&b=ffffff"  width=" 60%"/></p>

【注】你也可以自己在 _posts 文件夹下自动生成md文件和相同名字的文件夹（用于存放图片）

**第二步**：typora中的图像保存位置设置

点开文件——>偏好设置，设置如下：

<p align=center><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/993af5c7afec466eaec981af9ac662ed~tplv-k3u1fbpfcp-jj-mark:0:0:0:0:q75.image#?w=1613&h=657&s=64676&e=png&b=fafafa" width="60%"/></p>

修改好后，图片引用路径就在和博文同名的文件夹（新建博文名为test）的图片，如图所示：

<p align=center><img src="https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/cc88f5524f094d118bedc8456e650126~tplv-k3u1fbpfcp-jj-mark:0:0:0:0:q75.image#?w=918&h=103&s=12423&e=png&b=ffffff" width="60%"/></p>

**第三步**：安装插件

在根目录下打开git bash，然后运行以下命令，如果有安装淘宝镜像，第一个改为cnpm即可。

    npm install https://github.com/xcodebuild/hexo-asset-image.git

运行结果如下图所示，图为安装成功：

<p align=center><img src="https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/059d60bdaded4a0fa0f1ac61286f187e~tplv-k3u1fbpfcp-jj-mark:0:0:0:0:q75.image#?w=722&h=242&s=25251&e=png&b=000000" width="70%"/></p>

该插件的作用：将图片等静态资源的引用路径转化为绝对路径。

【注】我最开始不是用的上面命令安装的，用的是`npm install hexo-asset-image -- save`，该命令安装的是插件 hexo-asset-image 1.0 ，这个版本有点问题，安装后图片不能正常显示，查看图片路径被渲染成了 `/.xx/abc.png` 的格式（xx 是域名后缀）。最后采用上面的命令才成功。



如何卸载该插件？路径：`\blog\node_modules\hexo-asset-image`，直接删除文件夹，我试过没问题。

# 🌸 第二阶段：将图片保存到图床

网上查了一些有关md文件中图片的保存位置，发现除了在本地保存外，还可以采用图床进行保存，可以尝试一下[PicGo](https://github.com/Molunerfinn/PicGo) 这个图床上传工具，也方便md文件在其他站的上传。

参考资料：[前端小雪](https://blog.csdn.net/weixin_61529967/article/details/132273065)、[刘昕hrf](https://blog.csdn.net/weixin_43447266/article/details/132490718)、[杨 戬](https://blog.csdn.net/weixin_45525272/article/details/125387761)

我根据上面三个参考回答实现了将图片保存到gitee图床中。

我的图床：gitee平台

# 🌸 第三阶段：图片采用网络地址

参考[野猿新一](https://blog.csdn.net/mqdxiaoxiao/article/details/96770756)的回答，图片路径还是引用网络地址，想要在hexo博客中查看到网络地址的图片，直接在文章Front-matter下加一句：`<meta name="referrer" content="no-referrer"/>`即可，如下图所示：

<p align=center><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/b0f3200872db4755a847a50c37e6327a~tplv-k3u1fbpfcp-jj-mark:0:0:0:0:q75.image#?w=758&h=291&s=28703&e=png&b=f9f9f9" width="70%"/></p>

最终发现就是加了这一句就可以显示网络地址图片了，我哭死┭┮﹏┭┮。也不需要插件了，也不需要找个地方保存图片！

还有一个小问题就是，hexo博客网络图片下方可能会出现image.png，如果所示：

<p align=center><img src="https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/f4cccaa212ee4ca0ac5b2cd4f85c41d7~tplv-k3u1fbpfcp-jj-mark:0:0:0:0:q75.image#?w=809&h=170&s=55087&e=png&b=f5f5f5" width="60%" /></p>

解决办法就是把alt这一块（下图圈的地方）去掉即可：

<p align=center><img src="https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/43fc18d732d14116a6f8fedf7de8de30~tplv-k3u1fbpfcp-jj-mark:0:0:0:0:q75.image#?w=1331&h=174&s=61361&e=png&b=fffefe" width="60%" /></p>


本篇结束！
