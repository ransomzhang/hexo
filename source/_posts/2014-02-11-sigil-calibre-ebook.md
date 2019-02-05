---
title: "用Sigil及calibre制作电子书"
categories: 
- 折腾
description: 电子书制作软件
tags: 
- sigil
- kindle
---

自从习惯用kindle pw阅读后，现在都很难集中精力在电脑屏幕看一大段文章，觉得费神费力。

能把好的文章、博客、文档、自己整理的资料等等这些都搬到kpw上是件多么惬意的事。可以说制作电子书已经成为了刚需，于是Google就跟我说了用Sigil加Calibre，就是用Sigil做成规范的ePub格式，然后用Calibre转换成任意自己想要的格式。

这里下[Sigil](https://code.google.com/p/sigil/)，它托管在Google code，但源代码现在是放在github，支持Windows, Mac, Linux。[Userguide](https://code.google.com/p/sigil/downloads/detail?name=Sigil_User_Guide_0_7_2.epub&can=2&q=)写得挺详细的。

这是界面，支持多语言：

![](/images/sigil/11.jpg)

说来惭愧，最近才在学git，于是发现这个[ProGit](http://git-scm.com/book/zh)，可惜官方只有英文版epub格式下载，看了，中文只有网页版，于是就想自己制作一个。下面以这本书为个例子介绍一下怎么弄。

说到底，ePub格式就是个zip格式的压缩包，里面定义了各个文件夹，分别包含了文本、图片等各种素材，如图2

![图2](/images/sigil/22.jpg))

- Text文件夹包含的是xhtml格式文件，定义了封面，文本
- Styles文件夹：用来修饰xhtml的CSS文件
- Images放着所有的图片文件，就主要这三个文件夹，其它暂时用不到

在Text下右键，“添加空白HTML文件”，就自动创建了一个名为Seciton0001.xhtml的空白文件。然后把你想要的内容复制进去就好了，可以是纯文本或网页格式的。见图3

![图3](/images/sigil/33.jpg)

其实就是WYSIWYW（所见即所得），可以审查它的各个元素。见图4

![图4](/images/sigil/44.jpg)

接着把所要放的内容的逐个放到各个xhtml文件上，可以在格式菜单进行**加粗**、*斜体*修饰等等。
需要说明的是标题h1、h2、h3等(图4)是用来定义书本的章节的，由小到大是包含关系，p定义段落。定义好各个页面的标题后就可以为我们的书本创建目录了。菜单工具->目录->生成目录（图5），通过层级选项来确定要包括的目录层次，然后OK，就自动生成了目录（图6）。

![图4](/images/sigil/55.jpg)

![图5](/images/sigil/66.jpg)

![图6](/images/sigil/77.jpg)

接下来添加个封面，不然就没脸见人：菜单工具->生成封面，在素材中添加准备好的图片。

![图7](/images/sigil/88.jpg)

最后，让我们为本书润色一下，菜单工具->元素据编辑器，添加上标题、作者等参数。

![图8](/images/sigil/99.jpg)

到目前为止，一本书所需要的基本东东就都搞定，保存下来，自动生成了一个标准的epub格式文件。
有了它，在把它添加进[calibre](http://calibre-ebook.com/)，选择转换书籍，转换成你所需要的各种格式。

![图9](/images/sigil/00.jpg)
Done.
