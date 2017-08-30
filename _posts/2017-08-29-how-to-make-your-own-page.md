---
layout:     post
title:      "如何快速地搭建个人博客？"
subtitle:   "找别人做好的搬过来就行了"
date:       2017-08-29 16:00:00
author:     "Sirius"
header-img: "img/blog-front.jpg"
tags:
    - github
    - howTo
    - blog
---
 > 你们很快就会有 “写博客” 这个作业了。

<!-- TOC -->

- [谨以此文献给还是小白的我](#谨以此文献给还是小白的我)
- [Github Page](#github-page)
    - [什么是 Github？](#什么是-github)
    - [那 Page 怎么来？](#那-page-怎么来)
- [由此开始](#由此开始)
    - [注册 github 账户](#注册-github-账户)
    - [创建一个 repository](#创建一个-repository)
    - [New Template Renovation, A.K.A NTR](#new-template-renovation-aka-ntr)
        - [从别人手上夺过来](#从别人手上夺过来)
        - [染上自己的颜色](#染上自己的颜色)
    - [将你在本地的更改同步至 GitHub](#将你在本地的更改同步至-github)
- [更多玩法](#更多玩法)
    - [实时预览自己的成果](#实时预览自己的成果)
    - [为自己的博客添加评论系统](#为自己的博客添加评论系统)
    - [定制域名！](#定制域名)

<!-- /TOC -->

# 谨以此文献给还是小白的我

写一篇博客，可以说是我校软件工程导论的开篇作业了。

诚然，诸位大可注册一个简书账户，然后随便写点用了Markdown格式的东西上去，再呼朋唤友评论几句，就算是达到了老师的标准。

> 我当年就是这么做的。

你甘心于此吗？

如果你的答案是否定的，我的这一篇博客或许能帮你建起一个 ~~真正~~ 属于自己的博客。

>建立在GitHub上的网站当然需要遵守相关的用户守则，也就是说，你并不能完全地主宰自己文章的命运。
>但是，相比于微信推送和微博，你的自由依然广阔。

# Github Page

## 什么是 Github？

Github 是一个代码托管网站，时常被戏称为全球最大的同性交友平台。全世界无数程序员都会来到这里，“相互借鉴”，“协同合作”。我们可以把自己写的代码上传，这样全世界的Github用户都能够看到你的作品。或许过几天我会写一篇单独的博客来详细介绍一下GitHub。

## 那 Page 怎么来？

就像我刚才提到的，我们把自己的代码上传到 GitHub 上，GitHub 会帮助我们将代码转换为像这里一样的网页，也就是博客了。

可是，要写一个优雅美观的网页对我来说实在是太难了，所幸 GitHub 提供了一套类似于模板的工具——Jekyll。Jekyll能把一些特定的文件组合翻译成一个网页。这样，我们就只需要专注于博客内容本身就可以了。

# 由此开始

## 注册 github 账户

>你在找切换语言的选项吗？不存在的。请好好学习英语，并且善用 google translate。

## 创建一个 repository

> a place, building, or receptacle where things are or may be stored.

翻译成大白话，就是储存你的代码的“仓库”。

请将这个 repository 命名为 `[yourname].github.io` 。

![创建仓库](http://ovi1rdu1p.bkt.clouddn.com/create-repo.png)

## New Template Renovation, A.K.A NTR

关于一个什么样的样式才是好的，这个问题实在是与诸位的审美有关，在此我便以github page 的第一个主题 `Cayman theme`为例，来讲讲怎么把别人的示例改成自己的博客。

### 从别人手上夺过来

从 [Cayman theme](https://github.com/pages-themes/cayman) 下载压缩包，保存并解压到随便一个位置。

![下载模板](http://ovi1rdu1p.bkt.clouddn.com/download-cayman.png)

现在，解压出来的文件夹里面的文件结构应该是这样的：
```
Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----        2017/8/30      0:17                .sass-cache
d-----        2017/8/14     23:00                assets
d-----        2017/8/14     23:00                script
d-----        2017/8/14     23:00                _layouts
d-----        2017/8/14     23:00                _sass
d-----        2017/8/30      0:21                _site
------        2017/8/14     23:00             37 .gitignore
------        2017/8/14     23:00            101 .travis.yml
------        2017/8/14     23:00             71 another-page.md
------        2017/8/14     23:00           3247 CODE_OF_CONDUCT.md
------        2017/8/14     23:00           1750 CONTRIBUTING.md
------        2017/8/14     23:00             39 Gemfile
-a----        2017/8/30      0:17           1319 Gemfile.lock
------        2017/8/14     23:00           2648 index.md
------        2017/8/14     23:00            706 jekyll-theme-cayman.gemspec
------        2017/8/14     23:00           6555 LICENSE
------        2017/8/14     23:00           3926 README.md
------        2017/8/14     23:00          31970 thumbnail.png
------        2017/8/14     23:00            152 _config.yml
```

### 染上自己的颜色

打开 `_config.yml` 文件，更改如下内容，这会改变你的页眉上面的文字。

```
title: [your title]
description: [description of your blog]
show_downloads: false
google_analytics:
theme: jekyll-theme-cayman
```

再打开  `index.md` ,这是你博客的首页，你需要在这上面写一些你想放在首页的话，和文章的超链接。超链接的格式如下：

```
[Link to another page](another-page).
//[文章的题目](文章的markdown文件的文件名)
```

注意！请留意 `.md` 文件的开头。这是一份重要的声明，如果你手贱把它删除了，那么你的文章布局就会荡然无存。
```
---
layout: default
---
```
>当然，这些layout都是可以自己定制的。在这个模板中，layout只有default一种。如果你看上了别家的layout，大可复制下来放进自己的——layouts文件夹中，这样就可以用了。

如果你需要往博客上再增加一篇文章，你只需要在 `CAYMAN-MASTER` 文件夹下面新建一个Markdown 文件，然后把这个markdown文件的超链接加在主页上就可以了。

## 将你在本地的更改同步至 GitHub

在 `[yourname].github.io` 这个仓库里面，选择upload file，并将`CAYMAN-MASTER` 文件夹内的全部内容上传，选择 `commit change`。

![上传文件](http://ovi1rdu1p.bkt.clouddn.com/upload-file.png)

选择 settings，转到 GitHub Pages 一栏，将 source 改为 master branch。

如果不出意外的话，你会看到一行绿色的字，显示

 ``` 
 Your site is published at http://[yourname].github.io/
 ```

 这就说明你的博客已经正常运行啦！你可以先喝一口茶，然后进入 `http://[yourname].github.io/ ` 来观赏自己的成果。

 ![完成的样子](http://ovi1rdu1p.bkt.clouddn.com/blog-done.png)

> 从上传完毕到网站生成可能需要一段时间，建议先等待15分钟再行查看。

# 更多玩法

## 实时预览自己的成果

## 为自己的博客添加评论系统

## 定制域名！

To be continued...

