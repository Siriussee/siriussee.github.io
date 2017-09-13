---
layout:     post
title:      "如何快速地搭建个人博客？"
subtitle:   "找别人做好的搬过来就行了"
date:       2017-08-29 16:00:00
author:     "Sirius"
header-img: "img/blog-front.jpg"
tags:
    - GitHub
    - howTo
    - blog
---
 > 你们很快就会有 “写博客” 这个作业了。

<!-- TOC -->

- [谨以此文献给还是小白的我](#谨以此文献给还是小白的我)
- [GitHub Page](#github-page)
    - [什么是 GitHub？](#什么是-github)
    - [那 Page 怎么来？](#那-page-怎么来)
- [由此开始](#由此开始)
    - [注册 GitHub 账户](#注册-github-账户)
    - [创建一个 repository](#创建一个-repository)
    - [New Template Renovation, A.K.A NTR](#new-template-renovation-aka-ntr)
        - [从别人手上夺过来](#从别人手上夺过来)
        - [染上自己的颜色](#染上自己的颜色)
    - [将你在本地的更改同步至 GitHub](#将你在本地的更改同步至-github)
- [更多玩法](#更多玩法)
    - [实时预览自己的成果](#实时预览自己的成果)
    - [为自己的博客添加评论系统](#为自己的博客添加评论系统)
        - [为他们默哀](#为他们默哀)
        - [Gitment](#gitment)
        - [评价](#评价)
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

# GitHub Page

## 什么是 GitHub？

GitHub 是一个代码托管网站，时常被戏称为全球最大的同性交友平台。全世界无数程序员都会来到这里，“相互借鉴”，“协同合作”。我们可以把自己写的代码上传，这样全世界的GitHub用户都能够看到你的作品。或许过几天我会写一篇单独的博客来详细介绍一下GitHub。

## 那 Page 怎么来？

就像我刚才提到的，我们把自己的代码上传到 GitHub 上，GitHub 会帮助我们将代码转换为像这里一样的网页，也就是博客了。

可是，要写一个优雅美观的网页对我来说实在是太难了，所幸 GitHub 提供了一套类似于模板的工具——Jekyll。Jekyll能把一些特定的文件组合翻译成一个网页。这样，我们就只需要专注于博客内容本身就可以了。

# 由此开始

## 注册 GitHub 账户

>你在找切换语言的选项吗？不存在的。请好好学习英语，并且善用 google translate。

## 创建一个 repository

> a place, building, or receptacle where things are or may be stored.

翻译成大白话，就是储存你的代码的“仓库”。

请将这个 repository 命名为 `[yourname].GitHub.io` 。

![创建仓库](http://ovi1rdu1p.bkt.clouddn.com/create-repo.png)

## New Template Renovation, A.K.A NTR

关于一个什么样的样式才是好的，这个问题实在是与诸位的审美有关，在此我便以GitHub page 的第一个主题 `Cayman theme`为例，来讲讲怎么把别人的示例改成自己的博客。

### 从别人手上夺过来

从 [Cayman theme](https://GitHub.com/pages-themes/cayman) 下载压缩包，保存并解压到随便一个位置。

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

在 `[yourname].GitHub.io` 这个仓库里面，选择upload file，并将`CAYMAN-MASTER` 文件夹内的全部内容上传，选择 `commit change`。

![上传文件](http://ovi1rdu1p.bkt.clouddn.com/upload-file.png)

选择 settings，转到 GitHub Pages 一栏，将 source 改为 master branch。

如果不出意外的话，你会看到一行绿色的字，显示

 ``` 
 Your site is published at http://[yourname].GitHub.io/
 ```

 这就说明你的博客已经正常运行啦！你可以先喝一口茶，然后进入 `http://[yourname].GitHub.io/ ` 来观赏自己的成果。

 ![完成的样子](http://ovi1rdu1p.bkt.clouddn.com/blog-done.png)

> 从上传完毕到网站生成可能需要一段时间，建议先等待15分钟再行查看。

# 更多玩法

## 实时预览自己的成果

## 为自己的博客添加评论系统

评论系统当然是一个博客必不可上的一环。没有评论，就没有作者和读者的交流，读者的问题没法解决，文章的不足之处也无法及时纠正。所以，便有了这一节的内容，为自己的博客添加评论系统。

### 为他们默哀

许多个人博客的评论系统都是由多说或者 Disqus 提供的，然而这两者在中国都举步维艰。

 * **多说** 据称因为常年免费运营，缺少收益，已在今年关闭。
 * **Disqus** 惨遭墙暴，朋友笑称 “因为 #禁评”。

```
Ping to: disqus.com
Checkpoint	                        Result                  	IP
United States - Atlanta (usatl02)	OK	0.223	0.256	0.302	151.101.0.134
Australia - Sydney (ausyd03)	        OK	0.429	0.494	0.565	151.101.192.134
United States - Boston (usbos02)	OK	0.830	0.951	1.072	151.101.128.134
China - Beijing (cnbjs02)	        Packets lost (100%)		243.185.187.39
Switzerland - Zurich (chzrh01)  	OK	10.548	10.574	10.620	151.101.0.134
China - Shanghai (cnsha02)	        Packets lost (100%)		243.185.187.39
```

### Gitment

>upadte 2017/09/13
>我发现这个 Gitment 似乎不是这样用的，然而这段时间事务繁杂，无心写blog，容我何时偷闲来重新整理这一部分的内容。
>为了避免 gitment 造成的困扰，我决定暂时关闭本 blog 的 gitment 系统。有事请在 Telegram @SiriusSee 。感谢。

所幸天无绝人之路，[Gitment](https://imsun.net/posts/gitment-introduction/)横空出世。

Gitment使用Github的issue功能来当作储存评论的仓库，这样就解决了评论的储存问题。此外，由于Github本身支持Markdown格式的issue，所以说，我们的评论甚至可以用Markdown格式来写。

使用 Gitment 首先需要注册一个 [OAuth Application](https://github.com/settings/applications/new)

![reg](http://ovi1rdu1p.bkt.clouddn.com/oauth-app.png)

Application name 可以随便填，但是 Homepage URL 和 callback URL 请务必填写你的域名。创建成功后，页面上会显示 client id 和 client secret，复制下来，留待后用。

>如果你没有使用个性域名的话，请在这两栏输入`[yourname].github.io`

然后，开一个新的repo，以后你的所有评论都会以issue的形式存在这个repo里面。

最后，在你的每篇博文最末尾加上这样一串代码:

```javascript
<div id="container"></div>
<link rel="stylesheet" href="https://imsun.GitHub.io/gitment/style/default.css">
<script src="https://imsun.GitHub.io/gitment/dist/gitment.browser.js"></script>
<script>
var gitment = new Gitment({
  id: 'location.href',
  owner: '[your github user name]',
  repo: '[name of your new repo]',
  oauth: {
    client_id: '[your client_id]',
    client_secret: '[your client_secret]',
  },
})
gitment.render('container')
</script>
```

`git push` 一下，Gitment 系统就能在你的文章下面出现了。
不过还有一步，你需要 “初始化” 这个评论系统，其他人才能在这里留言。
如果你用于储存comment的repo是一个全新的状态，初始化可能会失败。为了解决这个问题，你可以去那个repo上面创建一个`README.md`。

### 评价

Gitment存在一些微小的不足，但是瑕不掩瑜。

* ++免费
* +支持markdown格式的评论
* +界面简洁，而且可定制
* -只有拥有 GitHub account 的用户才能够进行评论
* -没有办法直接在一条评论下面回复

## 定制域名！

To be continued...
