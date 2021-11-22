---
title: introduction of hexo
date: 2021-05-08 11:27:17
categories:
- 建站相关
tags: 
- hexo
- blog
---

# 本篇文章用来记录配置HEXO时碰到的问题

## 纲要：

* 简单介绍使用背景(为什么用) 
* hexo安装
* 部署方法
* 主题
* 评论功能
* 文章写法
* 数学公式与mermaid
* 标签、分类、页面创建方式(包括菜单中设置这些页面)
* 背景（本地img、bg加url、协议冲突、文件部署方式）大坑！
* 未完善功能：文章封面、页面顶部图、留言板、友链、音乐、movie等......
* 与wordpress比较
* 多终端工作（补充）
* 结束语

## 缘起：

怎么说呢，从接触计算机开始，就想要拥有一个自己的网站，因为我认为这会是一件很cool的事情。当时的我对计算机的底层毫无了解(虽然现在也是QAQ)， 而网站作为普通用户与计算机交互的重要接口，自然对当时想要了解计算机的我有着强烈的吸引力，拥有一个自己的网站的想法便应际而生。之后到了大学被C语言疯狂折磨，一直觉得底层的代码实现是件枯燥无聊的事情，认为计算机的主要功能应该是面向大众也就是交互友好应该是最重要的，然而当时完全是对着黑框框编程。现在的我则完全相反，黑框框多香，SB才喜欢做交互(笑)。当然，也正是因为这些底层方面的学习(从用户的角度来说的底层而不是计算机底层，或者说是代码层吧，毕竟电路什么的还是赶紧爬吧)， ~~让我学会了百度和google，~~ 让我有能力真的作出一些能让我稍有成就感的东西，所以我决定开始圆我之前的梦——做一个网站。正当我苦恼做什么网站时，我 ~~某个帅哥~~ 同学做了一个blog个人主页并与我分享。“This is  what I want”。向他了解相关问题后，我便开始了我的blog之旅。我也会将~~它~~他的友链放在本blog上 ~~(如果自己没鸽的话)~~ ，大家可以去逛逛。

## hexo安装：

建议自行百度....

一般单独弄一个文件夹存所有的文件，我的文件夹名为blog，一下所有操作均在blog目录下进行。

## 部署方式：

简单四部曲：

```shell
hexo clean # 清理缓存
hexo g # 本地部署
hexo s # 进入本地链接查看本地部署情况
hexo d # deploy 部署到githubpage
```

熟练使用后可直接两步完成：

```shell
hexo clean # 清理缓存
hexo d -g # 直接部署
```

如果你是第一次使用hexo，请先记住如上命令，毕竟这将是你接下来用的最多的命令，没有之一。

## 主题选择：

我选择主题butterfly，其实还有很多很好用的主题当然都大同小异，butterfly的可拓展性非常高，这也使得其配置十分复杂，当然直接用默认配置也行，开装即用，但我就喜欢花里胡哨，哼（鬼脸）。

要想配置好自己的炫酷的网页，首先要学会的就是看butterfly的文档，这里给出链接 https://butterfly.js.org/posts/21cfbf15/ 。这篇文档本身也是用hexo搭建的用的就是butterfly自己的主题，许多地方可以模仿借鉴。

## 主题介绍：

此处内容主要概括介绍butterfly文档中重要的地方，至少是我配置过程中遇到的问题。

### 1.主题安装与修改配置文件

安装按文档说明即可。

修改配置文件指文档“升级建议”部分。即复制 `./themes/butterfly/_config.yml `内容到blog目录下并重命名为 `_config.butterfly.yml` 然后之后的配置全在该文件中配置即可。

`_config.yml` 也是配置文件，hexo会自动将两者合并，可以粗浅的认为`_config.yml` 是hexo基础配置而 `_config.butterfly.yml` 则为主题带有的高端配置。

### 2.blog文件夹文件介绍

这里介绍一下blog文件夹中的主要文件

1. node_modeles:没什么卵用
2. **public**:所有发布之后的东西的前端全部存在这个文件夹，所以如果要改前端渲染可以在这里面改。但既然选择了主题，这些东西自然不需要自己动手。唯一对你有用的是public/img文件夹，里面可以存放图片，可以视作全局可用的img，这样能直接调用而不用给出url，但不推荐这么做，因为这个文件夹是不能再分类的，所有图都放在一起显得非常繁杂，建议只放一些封面等图片。
3. scaffolds:不知道是干啥的
4. **source**:第二个有用的文件夹，你所写的md文件就全在source\\_post中。如果将\_config.butterfly.yml中的post_asset_folder:设置为true（后面会说到），就可以看到每篇blog会自动生成的blog文件夹以及blog的md文件，文件夹中存一些需要的图片（具体使用工具为hexo-asset-image，github：https://github.com/xcodebuild/hexo-asset-image，也有一些坑，后面会提到）。最后是categories、link、tags文件夹，分别对应你自己设置的categories、link、tags（后面也会讲到）。
5. **themes**：里面会有一个butterfly文件夹，主要是主题配置文件，本人也未弄清楚里面究竟有啥，未来仍值得探索。唯一对你有用的是source/img文件夹，里面可以存放图片，可以视作全局可用的img，这样能直接调用而不用给出url，但不推荐这么做，因为这个文件夹是不能再分类的，所有图都放在一起显得非常繁杂，建议只放一些封面等图片。
6. \_config.butterfly.yml(\_config.yml):下面会主要介绍的文件，用于配置blog文件。

### 2.配置文件基本介绍

主要介绍一下配置文件的格式。

文件主要的格式就是对每一个模块写一个enable的选项，可以开启某些功能并对该模块进行一系列的个性化配置，如果想知道每个模块是干什么的可以去看官方文档(见上面链接)，这里只介绍一些我使用了的功能，以及说一下会有什么坑。

#### 背景：

首先第一个修改的当然是背景，这个直接找到配置文件中background选项，注意如果格式是url(....)，不能直接写文件路径，特别是使用本地路径时也要使用url(path)的方式写。

**还有一个巨大巨大的坑！！！！！！！！！！** githubpage现在使用的是https协议，而本地部署和配置文件给出的网链格式都是http协议，从用户的角度简单来说就是你你如果使用他的http的网链格式，你在`hexo s`的本地部署中是能看到你配置的背景的，但当你deploy之后会发现githubpage上根本就无法显示。不要问我这个bug是怎么找到的(这个神秘BUG真的卡了我快整整一天，用一天调一个背景，感觉自己就是个傻逼)，我直接打开了检查界面发现明明是有这张图的但无法显示就有了上述猜测，用了一张https的图就成功了.....，所以这个东西是真的蠢，你的本地部署和发布界面只有一个能显示，逼死强迫症。

对于上述问题的解决办法，推荐使用我现在使用的方法，使用本地路径，将图片存在上述的img文件夹中。注意配置文件中好像默认进入了butterfly/source文件，所以写相对路径时不需要加前缀，只需要使用`/img/xxx.jpg`这种方法即可，这里xxx.jpg得先存到img文件夹中。

#### 数学公式与mermaid：

这个如果有需要的话看看doc就好了，实现起来没什么难度，只是可能很多人不知道，butterfly主题能支持这些功能，好吧之前我就不知道，还困扰了好久。

#### 标签、分类、页面创建方式：

这个也是看看doc就好了，注意在主页面中是可以给出这些按钮的，doc中也有写到，只需设置menu选项即可。本人的menu设置如下：

```yaml
menu:
  首页: / || fas fa-home
  时间轴: /archives/ || fas fa-archive
  标签: /tags/ || fas fa-tags
  分类: /categories/ || fas fa-folder-open
  清单||fas fa-list:
    - Music || /music/ || fas fa-music
    - Movie || /movies/ || fas fa-video
  Link: /link/ || fas fa-link
  About: /about/ || fas fa-heart
```

#### 评论：

本人评论系统使用valine，感觉配置起来最简单，具体配置方法还是见doc，实在不想多重复，毕竟我也讲不明白。可以参考本人的评论配置，配置如下：

```json
# valine
# https://valine.js.org
valine:
  appId: xxxxxxxxxxxxxxxxxxxxxxxxxxxx # leancloud application app id
  appKey: xxxxxxxxxxxxxxxxxxxxxxxxxxx # leancloud application app key
  pageSize: 10 # comment list page size
  avatar: mp # gravatar style https://valine.js.org/#/avatar
  lang: en # i18n: zh-CN/zh-TW/en/ja
  placeholder: Please leave your footprints # valine comment input placeholder (like: Please leave your footprints)
  guest_info: nick,mail,link # valine comment header info (nick/mail/link)
  recordIP: false # Record reviewer IP
  serverURLs: # This configuration is suitable for domestic custom domain name users, overseas version will be automatically detected (no need to manually fill in)
  bg: # valine background
  emojiCDN: '//i0.hdslb.com/bfs/emote/' # emoji CDN
  enableQQ: false # enable the Nickname box to automatically get QQ Nickname and QQ Avatar
  requiredFields: nick,mail # required fields (nick/mail)
  option:
```

其中appId与appKey需要根据官网指示去valine的网站申请，相当于借用他的服务器，这样就可以在你的静态网站中实现用户之间的交互了。

#### 未实现的功能：

文章封面、页面顶部图、留言板、友链、音乐、movie等......

在最近有时间的情况下我应该会加入以上功能，doc中也有配置方法以及成果展示，个人感觉还是挺棒的，~~希望读者能在有生之年看到，~~应该很快就会在我的blog上上线。 

## 如何创建文章：

只需到你的blog目录下输入：

```shell
hexo new "title"
```

其中，`title`是文章标题，输入后，就会在`source/_post`文件夹下创建文件`title.md`如果还在之前配置了`post_asset_folder:true`，则还会创建名为`title`的文件夹，可在里面存入文章需要的图片等，方便路径引用。

创建后的md文件开头会有文章配置内容，用---线隔开，可以加入一些内容来配置标签种类背景图等，例如本文章的配置如下：

```markdown
---
title: hexo配置的那些坑
date: 2021-05-08 11:27:17
categories:
- 建站相关
tags: 
- hexo
- blog
---
```

具体配置方式可见文档，文档中都有详细介绍（可能还需要看看hexo的官方文档）。

## 如何删除文章：

有了创建自然就会有删除，~~当你挖了一个坑后开始后悔时，最直接的方式就是删库跑路~~，hexo并没有删除文章的命令，只能自己手动删除，只需要删除xxx.md文件及其对应的文件管理文件夹（若没有设置post_asset_folder则不需要）。**之后要进行hexo clean操作** 再进行`hexo d -g` 即可。

## hexo与wordpress的比较：

本人同时也租了一个服务器搭建了wordpress的blog，但最后还是选择了放弃更新wordpress的blog，选择使用hexo，主要原因如下：

* 本以为wordpress的个性化程度更高但实际上挺低的，大多数wordpress主题似乎并不注重个性化设置，只有一些比较基础的选项供开发者选择，似乎其本意是想搭建一个专注与写blog的平台，对于各种炫酷功能并不是很重视，这对一些只是想写blog的用户就非常适合，可以专注于blog而不需要管其他的东西。但我觉得既然是自己的网站，网站的个性化设计也是很重要的一方面，对于不会写前端的我hexo提供了一个很好的方式来实现网站前端的个性化，只需要配置yml文件即可，可以说其已经非常成熟，比较适合我，不过人各有所需，很多人也会使用wordpress，但我觉得既然这样为什么不直接去CSDN写呢......
* 不太习惯wordpress的文章写作形式。wordpress就是类似正常的blog书写网站如csdn的写作形式，对于习惯使用markdown的我感觉非常非常非常的别扭，markdown的优势就是能让人更加专注于文章内容而不需要在一文章版式，习惯了这种书写方式后就再也不想在写作过程中思考排版了，但很可惜wordpress并不支持markdown格式书写。虽然其有插件能实现markdown书写，但毕竟不是原生markdown，用起来还是很难受，体验并不好，而hexo可以直接使用原生markdown在markdown编辑器立直接写作，所以还是比较喜欢hexo的方式。
* wordpress也不是没有好处，因为是自己的网站，可以自己绑定域名，而hexo只能依附于githubpage(好像也能绑定其他域名，但我不会，也不想去研究了)，不过这点对我来说倒也无所谓，个人觉得使用xxx.github.io也没啥.......当然这看个人需求。

基于这些原因，我还是选择了hexo，现在也将他调教的越来越顺手，以后也会用他写更多的文章。

## 杂项（补充）

### 多终端工作

如果你现在在自己的笔记本上写的博客，部署在了网站上，那么你在家里用台式机，或者实验室的台式机，发现你电脑里面没有博客的文件，或者要换电脑了，最后不知道怎么移动文件，怎么办？

答案是利用git的分支系统，这样每次打开不一样的电脑，只需要进行简单的配置和在github上把文件同步下来，就可以无缝操作了。具体方法可见该[知乎问题](https://www.zhihu.com/question/21193762)。原理机制与操作方式都有详细的介绍。

### 文章改名

注意md文档中开头的配置内容中的title只是决定blog网页中打开该文章后最上面的title显示什么，要想修改blog主页中文章的标题需要修改.md文件名，同时对同名文件夹也要进行同样的修改。

## 结束语

总的来说，hexo是一个相对来讲好入门，简单便捷的写blog的方式，网上有大量的教程，也有丰富的主题供使用者使用，更有许多优秀的blog可供新手学习和借鉴。哪怕你是计算机小白，对于计算机的认识只停留在开机关机打游戏，你也可以在很短的时间内学会用hexo写blog。“世上无难事，只怕有心人”，在互联网如此发达的今天，相信你只要有一颗想学习的心，付出努力，任何东西都能学会。在两年前我就是那么一个对计算机认识仅仅停留在开机关机打游戏的人，学会这些也不过是兴趣使然，一个想写自己网站的念头驱使着我学了很多东西，现在回头看这些看上去十分困难的东西也就不过如此，我并不觉得自己天赋异禀，也走了许多弯路，但弯弯绕绕，我还是走到了这里，未来的路还很长，我也不会就此止步。但不管怎么说，这个小时候的愿望也算是实现了，又有什么比实现自己的愿望更加令人开心的呢。

用一句古话来形容技术是很合适的，”闻道有先后，术业有专攻“。技术从来都不难，互联网也有大量的教程教你去怎么做，你可能会碰到很多大佬你觉得他为什么什么都会，特别是计算机方面，可能在你还在学C学的苦苦挣扎的时候，你的同学已经开始玩转python、java，你可能会有深深的绝望感，但实际上不过是他们学了这些而已，你学了你也会，不要害怕，努力向前，技术是一片没有尽头的海洋，只要你找准一个方向努力向前，终将有所收获。

望所有人都能在无尽的海洋中找到属于自己的那一片港湾。

完。2021.9.4

![img](./introduction-of-hexo/68794244_p0.jpg)

