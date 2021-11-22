---
title: something about git and github
date: 2021-11-16 15:17:33
categories:
- 学习
tags:
- git
---

# something about git and github

## 纲要

* 写在前面的话 (100%)
* git与github(100%)
* git操作方式(50%)
* git原理(0%)
* 如何用git进行双系统同步开发(100%)
* .gitignore的编写(100%)
* hexo相关(100%)
* detailed intro of github (include change private repo to public repo, delete repo)(0%)
* git重构(100%)

## 写在前面的话

本blog只记录一些简单的生活中常用的方法，要学习具体的git使用方法还是建议看专门的git教程，可以参考[菜鸟教程](https://www.runoob.com/git/git-tutorial.html)，本人水平有限，文中难免出现一些错误，希望读者谅解并能提出，可以在留言区进行交流与讨论。

## git与github

假设你是一个计算机小白，第一次听到git和githb，首先你得区分这两个东西。git是一个版本控制工具，而github是一个远程的代码托管服务器，代码托管在github中的repositories中。简单说，git是一个能帮你在你本地管理你代码不同版本的工具，而github是一个远程服务器，全球各地的coders能将同名的代码上传到github上，不仅能管理你自己的代码，你还能在github上看到别人公开的代码进行学习和交流，~~甚至你可以找到你学长留下的学校课程的实验源码、作业答案和考试题目~~。github上同时还有许多开源的电子书籍，以及很多学习资料，能帮助你学到许多计算机知识。俗话说得好：“程序员不能失去github，就像西方不能失去耶路撒冷”，我觉得对任何计算机的使用者来说，都需要去了解github，学会git的使用，这时非常有必要的。

## git的常用操作

如果你的电脑没有git，你要做的第一件事就是去安装一个git。git的安装就不用我多说了，网上有大把资料，windows用户直接找到官网下载安装最新版然后一路确认即可。linux一般会自带git，如果没有，也可以去官网下载安装。这里就不再多赘述。

现在大部分人都是在命令行下使用git（无论使用什么系统），因为其简单方便快捷。如果你本身就使用的是Linux操作系统，那命令行操作对你来说可以说是如鱼得水；如果你是windows用户也不要害怕，git的操作并不复杂，真正常用的操作很少，多操作几遍就能记下来，当然如果你有学习命令行操作的想法那更是极好，我在之后的文章中说不定也会讲一些linux系统及命令行操作相关的内容，~~虽然很有可能咕咕咕~~。

接下来是git的使用介绍。

### 初始化与提交:

首先进入你想进行版本控制的文件夹，windows用户可以在文件夹中右键打开git bash（如果你git安装成功的话），linux用户直接进入即可。在命令行中按序输入：

```bash
git init # 创建git
git add . # 将所有文件加入workspace
git commit -m "xxxxx" # 提交工作区文件并加入注释xxxxx
```

这样你就初始化了一个git并进行一次提交了。

`git init`、`git add .`、`git commit -m "xxx"`也是最常用的命令，每当有一个新的想要进行版本控制的目录都可以在其中进行使用`git init`，然后每次更新文件进行`git add .`、`git commit -m "xxx"`操作即可。

### 与github repository连接:

执行了1中操作后你就能在本地进行代码的版本控制了，可如何才能把代码添加到github中自己的repository中呢？操作也很简单。

首先在github中创建一个repository，创建好后会有一个界面告诉你如何操作只需照着上面输入命令即可。其中`git branch -M main`可以忽略，这时将你这个branch的名字改成main，其实可以不改，如果省略了这段代码后面`git push -u origin main`就要相应改成`git push -u origin master`，当然，你完全可以就按着它的步骤来，也不会有任何问题。

连接以后从本地提交到远程只需使用`git push`命令即可，从远程仓库更新本地只需`git pull`命令即可。

**注意：**与github连接可以使用ssh免密操作，具体ssh连接方式可以网上搜索，配置方法也是十分简单。

### 查看git状态:

使用命令`git status`查看当前文件夹与上次提交后的文件状态的对比，这个命令可以很轻松的让我们知道这次我们对文件夹进行了修改，哪些修改没有被git记录下来。

### 克隆仓库:

用`git clone`命令克隆一个仓库，具体方法是当你看到一个仓库想将里面的内容下载到本地时，git clone下那个仓库中`code`按钮下的那个链接，如果进行了ssh绑定，可以直接git clone 那个SSH key，可以不需要账号密码验证。

注意git clone后会在你操作的文件夹下生成一个以仓库名为名字的文件夹，不需要你自行创建文件夹。

### 一些小问题:

工作区是什么？git又是如何进行版本控制的呢？除了上述命令git还有哪些命令呢？这些问题将在以后进行更新，这里只介绍上面这些简单操作。如果有兴趣可以看网上的一些教程，如[菜鸟教程](https://www.runoob.com/git/git-tutorial.html)等。

## git进行双系统同步开发

有了git，双系统开发就简单了许多。你可以将github当作一个免费的服务器，里面可以存放你的代码，当在一个系统进行完工作后进行上传（git push），具体上传方式与上面**初始化与提交**中内容相同；到另一个系统工作时只需将github上的项目git pull下来即可完成同步。

### 优点：

* 操作简单
* 代码存在远程不需要担心硬件备份丢失或损坏
* 哪怕在别的地方也能访问查看，只需打开github网站

### 缺点:

* github对上传文件大小有限制，不能上传过大的文件（貌似有方式可以上传大文件，但看上去有点麻烦，本人平时也就传传代码，没有需求，就没有过多研究）
* 需要梯子（不知道这算不算......）
* 相对于硬件存储，有一定的学习成本，毕竟要写点命令行~~，都2021年了不会还有人不会github吧~~

### 一些小问题:

学到这你已经会git的增(git add ./git commit -m ”xxx”/git push)、查(打开github总会吧)、改(git pull到本地改，改完重新提交)。现在有个很严重的问题，怎么删呢？可见后面**.gitignore的一个重要的问题**内容。

这就要先介绍git还有个很强的功能.gitignore。这个文件会在git add的过程中起作用，能忽略上传文件，使git add的过程中按规则忽略，这样就能避免上传很多不必要的配置文件(如.idea文件夹)，具体 .gitignore的配置规则下面会进行讲解，你要记住的是，每当你进行一个项目，请先创建一个 .gitignore文件，在上传前ignore永远比上传后ignore要简单许多，希望大家都能养成这一个好习惯。

## .gitignore常用写法

* `xxx/`可忽略所有的xxx文件夹（递归搜索）
* `/xxx/`可忽略根目录下xxx文件夹（只忽略根目录）
* `xxx`忽略所有xxx文件
* `*.zip`忽略所有.zip文件（递归）
* `\xxx\`、`!\xxx\abc` 忽略xxx文件夹中除了abc的所有文件

## .gitignore的一个重要的问题

很多人没有一个良好的习惯（没错就是我），没有在一开始就写一个.gitignore文件，而是在git push之后加入了这个文件，然后他就会发现这一点效果都没有......

这是因为这些文件已经进入了版本控制，新编写的规则已经没用了，那该怎么删除一个文件呢？具体步骤如下：

```bash
# 先在文件夹中编写.gitignore文件
git rm -r --cached xxx # 假设要删除文件夹名为xxx
git add .
git commit -m "remove xxx"
git push
```

**注意：**一定要先编写.gitignore再git add，**.gitignore也不能在子文件夹中，必须在根目录中，否则会无效**。`git rm -r --cached xxx`即是删除工作区的xxx，之后如果没有需求可以不用`git add .`，直接commit即可。当然，这样做的话后面再`git add .`的话就会又将xxx放入，所以建议先写.gitignore文件。

## hexo相关

hexo blog就是基于github，详情可见我的另一篇介绍hexo的blog。

我们可以利用git的性质来多平台同步开发hexo。具体方法可见[知乎问题](https://www.zhihu.com/question/21193762)，另一篇介绍hexo的文章也有介绍。

## git 重构

当然，如果你碰到了无法解决的错误，有一个最简单粗暴的方式——删库跑路！！！这是每个程序员所必备的技巧。git 重构方式如下：

* 直接删除项目根目录中的.git文件夹（一般是隐藏文件夹）
* github上删库
* 重新构建git与github的repo并相连

虽然这是必备技巧，但希望大家永远遇不到使用它的这一天。





未完待续.....
