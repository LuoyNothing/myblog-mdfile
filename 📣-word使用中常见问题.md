---
title: 📣 word使用中常见问题
date: 2023-09-13 19:18:22
tags: word
categories: 文档
---

# 📚 Word 解决MathType数学公式粘贴后上浮问题

步骤如下：

1. 双击公式，在Mathtype的菜单栏中选择大小，定义自己想要的大小样式等。调整完整尺寸即可，需要和正文的尺寸调整一致，以下作为参考：

   ```text
   初号 	->	42pt
   小初号	->	36pt
   一号 	->	28pt
   二号 	->	21pt
   小二号	->	18pt
   三号 	->	15.75pt
   四号 	->	14pt
   小四号	->	12pt
   五号 	->	10.5pt
   小五号	->	9pt
   六号 	->	7.875pt
   七号 	->	5.25pt
   ```

2. 然后选择预置→公式预置→保存成一个eqp文件文件。

<p align=center><img src="https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/b0dfef3ad90f4e3298c610451abdf669~tplv-k3u1fbpfcp-jj-mark:0:0:0:0:q75.image#?w=1061&h=403&s=162761&e=png&b=f4f3f3" width="70%"/></p>

3. word菜单栏点击MathType->格式化公式，然后如下图进行操作即可

<p align=center><img src="https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/1b9db39bfa304747824428946d967ec9~tplv-k3u1fbpfcp-jj-mark:0:0:0:0:q75.image#?w=655&h=584&s=66586&e=png&b=f2f2f2" width="50%"/></p>

# 📚 想要在公式里加空格

直接设置格式为文本就可以加空格。

# 📚 公式复制粘贴问题

问题：复制粘贴之后公式变成图片不能编辑

解决：只需要将MathType里的一个设置更改

<p align=center><img src="https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/6509da1ef9254d8aac43fcd9b5542a01~tplv-k3u1fbpfcp-jj-mark:0:0:0:0:q75.image#?w=1323&h=520&s=73409&e=png&b=f5f5f5" width="80%"/></p>

将剪切与复制里的MathML改为 namespace attr2.0 就可以了

# 📚 公式居中和编号右对齐问题

参考：[word中mathtype7公式右编号右对齐解决方法，超实用！ - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/507833012)

这个问题是由于word里面的制表位设置不正确导致的，解决步骤如下：

（1）在布局-->分栏—>更多分栏中找到纸张宽度，记住这个数字，以18.76为例

<p align=center><img src="https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/29c7bdfe3ad943b995ab94cd18654080~tplv-k3u1fbpfcp-jj-mark:0:0:0:0:q75.image#?w=544&h=521&s=34308&e=png&b=f1f1f1" width="30%"/></p>

（2）找到开始—段落—制表位

<p align=center><img src="https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/6828a013f8a14151a5ad326527103afa~tplv-k3u1fbpfcp-jj-mark:0:0:0:0:q75.image#?w=1012&h=193&s=36563&e=png&b=f2f2f2" alt="image.png"  width="50%"/></p>

<p align=center><img src="https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/3280b93687354801a5a9d1d042724fe1~tplv-k3u1fbpfcp-jj-mark:0:0:0:0:q75.image#?w=529&h=893&s=55569&e=png&b=fbfbfb" width="30%"/></p>

（3）如果制表位位置有数据，点击右下角的全部清除

（4）清除之后，在这里输入18.76，同时框选右对齐，然后点击设置

（5）在这里输入18.76 / 2 = 9.38，同时框选居中对齐，然后点击设置，设置完成后点击确定

（6）选中公式所在行，按Backspace删除空格，将公式放到最前面

（7）然后在公式前面按Tab键，就可以将公式居中，在公式和编号之间按Tab键就可以让编号右对齐并且在行末了

**进阶版修改方法**

采用上面那种方法可以单个的解决问题，但是面对大量公式的时候，我们还有更便捷的方法，不过原理都是一样的

（1）点击样式—新建样式（开始-->样式右下角点一下新建样式）

（2）名称随便取，以公式为例名，后续段落样式选正文，在格式里找到制表位，重复二中的步骤即可

（3）在样式里就可以找到刚刚新建的样式，再进行操作就好了
