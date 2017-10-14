---
layout:     post
title:      "Photoshop简明教程II"
subtitle:   "You Are Not Prepared!"
date:       2017-10-12 13:00:00
author:     "Sirius"
header-img: "img/ps_2.jpg"
tags:
    - Photoshop
    - howTo
---

>声明：本教程部分演绎自[Adobe Photoshop Tutorials](https://helpx.adobe.com/photoshop/tutorials.html), 版权属于Adode公司所有。本教程全部内容仅供个人学习使用，不得用作商业用途。

# 如何处理海报设计中的元素关系？

<!-- TOC -->

- [如何处理海报设计中的元素关系？](#如何处理海报设计中的元素关系)
    - [海报中的元素](#海报中的元素)
        - [背景](#背景)
        - [文字](#文字)
        - [图片](#图片)
    - [元素之间如何和谐共处？](#元素之间如何和谐共处)
        - [示例1：如何处理背景与文字的关系？](#示例1如何处理背景与文字的关系)
            - [打开背景图，创建画板](#打开背景图创建画板)
            - [输入一些文字，并使其与背景图相谐](#输入一些文字并使其与背景图相谐)
            - [如法炮制，再来一张](#如法炮制再来一张)
            - [导出，](#导出)

<!-- /TOC -->

## 海报中的元素

如果简单的对海报中的各个元素进行一下分类，我发现，海报的基础元素不外乎三种：

**背景，文字和图片**。

### 背景

顾名思义，海报的最底层图案。它可以是简单的纯色背景、纯色**渐变背景**，也可以是 **低多边形背景**（low poly）、**涂鸦式色彩对撞背景**，甚至，一些简单的照片，施以滤镜处理之后，也能够成为一个优秀的海报背景图。

![pic of all kinds of bg-pic](http://ovi1rdu1p.bkt.clouddn.com/bg-of-poster.jpg)

### 文字

作为活动海报而言是至关重要的一环。**背景几乎不承载具体信息**，图片对于信息的传达效果有限，而文字无疑就成为了信息传达的不二选择。然而，文字的数量，排布，大小，颜色，还有字体的选择，统统都会对信息的传达造成影响。有些时候，**不恰当的处理对于一张海报来说，是毁灭性的**。

![an ugly poster](http://ovi1rdu1p.bkt.clouddn.com/ugly-card.jpg)

与文字关联程度最高的毫无疑问就是背景了。文字类型的选取，与背景息息相关。


### 图片

为什么我把图片和背景分开来讲？此处所指的 "图片" **独立于前文提及的背景图片**。与背景不同，这些图片是与文字内容有紧密的逻辑关系的。

比如，一场活动需要通过微信公众号报名，那么，公众号的**二维码**就是海报设计中的 "图片" 要素。

又比如，我想以 Batman 为主题制作一章海报，那这张海报中自然要出现 Batman 的形象，那这个展现 Batman 形象的图片，我将它从“背景”独立出来，称为“图片”。

![batman-poster](http://ovi1rdu1p.bkt.clouddn.com/batman-poster.jpg)

或者有人会问：如果海报需要展现的主体占据了极大的部分，我能不能把它作为背景呢？我的回答是不能。任何的设计，如果让“图片”成为了主角而挤占了“文字”的空间，那么它所能够传达的信息一定是不足的。如果的确存在需要一个极大的图片作为传达主题的媒介，我建议你把这个图片和背景结合起来。

![batman-poster](https://i.pinimg.com/736x/14/0c/63/140c630ef8775f9d65239816269d12cc--totoro-poster-my-neighbor-totoro.jpg)

## 元素之间如何和谐共处？

看十万字长篇大论不如动手实践。在这一部分，我会通过一些简单的例子来讲解元素之间的关系，以及如何处理它们之间的关系来使整体更加协调。此外，在讲解这些例子的过程中，我也会讲解一些上一次内培没有提及的 PS 工具使用方法。

### 示例1：如何处理背景与文字的关系？

> 此部分演绎自 Adobe Support [How to create a poster](https://helpx.adobe.com/photoshop/how-to/make-poster.html?playlist=/content/help/en/ccx/v1/collection/product/photoshop/segment/designer/explevel/beginner/applaunch/basictraining/collection.ccx.js?ref)。如果对于我提及的具体操作存在疑问，可以进入超链接观看教学视频。

#### 打开背景图，创建画板

我们将 `make-poster` 文件夹下的 `washington-leaf.jpg` 拖入 PS 的空白处以打开它。

为了使日后我们能为这副海报增加不同的版本，我们为 `washington-leaf.jpg` 创建一个 **画板**。选中 **背景** 图层，点击顶栏 **图层** 选项卡，再选择 **新建 - 来自图层的画板** 选项卡，不妨命名为 **leaf** 画板，并选择确定。

![create](http://ovi1rdu1p.bkt.clouddn.com/create-new-huaban.png)

此时，在原先图片的左上方会出现画板的名字，图层侧边栏中也会出现画板的名字。

#### 输入一些文字，并使其与背景图相谐

选择 **文字工具** ，在图片的上半部分输入 `THE BLUE RIDGES TOUR`, 调整文字的大小和字体，使其与背景图片相宜。

关于字体的选择，这可能涉及个人审美，我对此不会强求。同时，我在此讲一下我对于字体选择的看法。

大部分字体具有一种与生俱来的**刻板印象**。比如说，看到**微软雅黑**，我们就会不由自主地感受到一股“商务风”；而谈及**哥特体**（Fraktur），我们就会想起中世纪后段的西欧；至于谈及**行楷**，那么面前浮现的肯定是中国的古风古韵。如果各位对于背景应该配何种字体没有明确的想法，我个人建议各位选择衬线较少、体型较粗的字体。

> [衬线](https://zh.wikipedia.org/wiki/%E8%A1%AC%E7%BA%BF%E4%BD%93)指的是字形笔画末端的装饰细节部分。无衬线字体在西文中习惯称 sans-serif ，其中 sans 为法语的“无”的意思。中文将 Serif 按照字义翻译成 "衬线" 或 "字脚" ，顾名思义就是装饰陪衬的作用。

我们可以打开侧边栏的 **字符** 选项卡，对文字的垂直与水平缩放、字距与行距进行微调。我使用的字体大小是 `297pt`， 行距是 `250pt`， 诸位可以根据自己对于字体的选择来进行调整。

> 字符选项卡通常在右侧边栏即可找到。如果你因为手贱不小心把它删掉了的话，可以在 文字工具 的 上边栏 的 倒数第二个按钮 “切换字符和段落面板” 中重新找到它们。

字符选项卡同样提供了**调整颜色**的按钮，我们可以在这里调整文字的颜色。单击设置文本颜色按钮，会弹出一个**拾色器框**。将光标移出拾色器框的范围，光标会变成一个胶头滴管的形状，你可以在**当前图层单击选取当前点的颜色**。

拾色器的存在为我们寻找合适的颜色提供了一条捷径：我们能够轻易地选取**与背景图案相近的**颜色。设计一张各元素和谐的海报，文字的颜色可以与背景相近，或者与背景形成鲜明的对比。

![contrast-in-color](http://ovi1rdu1p.bkt.clouddn.com/contrast-in-color.jpg)

我们暂时先不讨论如何设计一张对比鲜明的海报，而是关注如何寻找一个与背景色相近而又具有一定识别度的文字颜色。以手头的这张海报为例，主体颜色是**偏暗的黄色**，那我们可以考虑选取一个**相对比较明亮的黄色**作为文字颜色。落实到具体操作上，就是使用拾色器选取叶片的颜色，然后在颜色选框内将取色的点**稍微向左上角拉动**，就能得到比较合适的颜色了。

![choose-color](http://ovi1rdu1p.bkt.clouddn.com/choose-color.png)

#### 如法炮制，再来一张

还记得我们刚才建立的 画板 吧？

选中 图层选项卡中的 **leaf** 画板，然后选择 **图层-复制画板** ，得到 **leaf** 的拷贝，我们将其命名为 **river**

删除 **river** 画板下的 `washington-leaf.jpg` 图层，然后把 `Yosemite-river.jpg` 放到 `leaf.jpg` 的位置。

同时，按照我们上面提到的方法，改变文字的颜色，使其与背景相和。

#### 导出，

以及为什么要使用[画板](https://helpx.adobe.com/cn/photoshop/using/artboards.html)。

如上次内培所言，选择 **导出为** 对文件进行导出。

此时，你会发现，"导出为" 窗口左边显示了两个文件，分别是我们之间建立的 **leaf** 画板 和 **river** 画板。我们可以很方便地对他们进行分别导出。

我们在这次设计中，采取了 "画板" 这一技巧创建了两份形制类似的海报，这便向我们揭示了画板的一个作用 —— **版本控制**。我们可以利用画板工具产生复数个不同版本的设计作品。

需要留意的是，我们可以把画板理解为一种高级的图层组，和图层组一样，画板能够包括一部分图层，并且能够作为整体进行操作。但是，画板之间**不允许嵌套**。