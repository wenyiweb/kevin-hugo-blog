---
categories:
- 技术文章
date: 2015-11-12T17:09:44+08:00
description: ""
keywords:
- 部署
- github
- gitcafe
- 教程
- 博客
- 域名绑定
tags:
- gitcafe
title: "Hugo搭建个人博客部署Github和gitcafe教程"
url: "2015/11/12/Hugo搭建个人博客部署Github和gitcafe教程"
---

由于github拒绝Baiduspider，所以你的博客只能通过google搜索到，但是为了让不能使用google的但是又渴望学习的同学们也能看到你的博客，所以介绍一下gitcafe的部署，官方的文档写的很清楚[[官方文档]](https://help.gitcafe.com/manuals/help/)。

<!--more-->

> GitCafe将以代码托管为核心业务，提供一系列优质前沿的服务来帮助到中国IT领域的开发者、项目以及企业更好地学习与成长。

> Git是目前世界上最流行最优秀的项目版本控制系统之一，Cafe的意思为咖啡馆，象征着程序员文化。在GitCafe这个平台上，开发者可以轻松的在线协作共同开发出一个又一个开源或者私有项目。通过GitCafe，开发项目的控制与团队管理将变得方便与有效。

> 在GitCafe的网站以及团队，我希望每一个用户和员工都能感受到浓厚纯正的黑客精神与文化，发现和理解计算机技术的真正魅力与潜力，激励每一位中国的开发者去开发出更多更有趣的东西。

### 安装 GIT


Windows 平台

下载 [msysGit](https://msysgit.github.io/) 进行安装。安装完成后可以在应用程序界面找到 Git Bash 和 Git GUI 两个软件；其中，Git Bash 是一个 Bash 的模拟环境，让 Windows 用户可以像 Linux / Unix 环境一样使用 Git 命令； Git GUI 是一个图形界面的 Git 管理工具，提供了很好的可视化 git diff差异比较。我们推荐从 Git Bash 入手学习 Git 的使用。
![](https://gitcafe-image.b0.upaiyun.com/423be76eeecff1b3cf0d7e83687bfb25.png)
***
Mac OS X 平台

下载 [Mac OS X 版本的 Git 安装包](https://github.com/timcharper/git_osx_installer/downloads)进行安装 。 
> 你可能会遇到这样的提示 xcode-select: note: no develper tools were found ... ，这说明你的 Mac 上 还没有安装 command line developer tools ，可以按照命令行的提示进行安装，或直接在命令行中输入 xcode-select --install 回车后进行安装。

如果你的 Mac 之前安装了 homebrew ，可以直接输入 brew install git 进行安装。
***
Linux 平台

多数 Linux 发行版已经预编译 Git 的二进制包，可以通过包管理器直接安装。根据你使用的发行版，选择下面对应的命令进行安装。

Debian/Ubuntu apt-get install git
> 如果你使用 Ubuntu 10.04、Debian 5.0（lenny）或更老的版本，请使用 apt-get install git-core命令进行安装。在老版本的 Debian 中，软件包 git 实际上是 GNU Interactive Tools ，而非我们熟知的版本控制系统。但由于 Git 的影响力越来越大，现在已经将 GNU Interactive Tools 改为 gnuit，git-core 正式改为 git。

Fedora / CentOS yum install git
Gentoo emerge --ask --verbose dev-vcs/git
Arch Linux pacman -S git

### Gitcafe 部署

1. 创建SSH密钥：

```bash
$ mkdir ~/.ssh
$ cd  ~/.ssh
$ ssh-keygen -t rsa -C "YOUR_EMAIL@YOUREMAIL.COM"
Generating public/private rsa key pair.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in ~/.ssh/id_rsa.
Your public key has been saved in ~/.ssh/id_rsa.pub.
The key fingerprint is:
15:81:d2:7a:c6:6c:0f:ec:b0:b6:d4:18:b8:d1:41:48 YOUR_EMAIL@YOUREMAIL.COM
$ cat id_rsa.pub
```
然后再Gitcafe中点击账户设置，新建SSH KEY，粘贴刚才打印的key

测试是否连接成功

```bash
$ ssh -T git@gitcafe.com
```
按照提示输入yes。最后，如果出现这个提示

```bash
Hi USERNAME! You've successfully authenticated, but GitCafe does not provide shell access.
```
恭喜你，连接成功。
2. 提交项目

在Gitcafe上新建一个项目，例如，项目名为myblog。
hugo教程请参考[Hugo+Github搭建个人博客图文教程](http://blog.h5super.com/2015/11/10/hugoblog/)
本教程使用上一篇文章中创建的myblog。进入public目录，然后执行以下命令：

```bash
$ cd  ~/.ssh
$ ssh-keygen -t dsb -C "YOUR_EMAIL@YOUREMAIL.COM"
Generating public/private rsa key pair.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
The key fingerprint is:
$ cat id_dsb.pub
# 到 Github 网站个人设置项里添加 SSH 公钥，随后测试是否能连接到 Github
# 在 Github 网站新建 username.github.io 项目
# cd 进入本地项目文件夹
$ git remote add ghorigin git@github.com:username/username.github.io.git #添加远程仓库地址，ghorigin 指代 Github 远程仓库，区别于 Gitcafe 仓库的 origin
```

然后打开gitcafe刚才创建的项目，点击继续按钮，将会看到push的所有文件。

### GitHub 部署

1. 创建SSH密钥：

方法个上面已经介绍过了，由于刚才创建的名字是id_rsa.pub已经被Gitcafe占用，这里用rds命名。

2. 提交项目

Github部署，请参考[Hugo+Github搭建个人博客图文教程](http://blog.h5super.com/2015/11/10/hugoblog/)

### 域名解析

如果你使用个性域名，请参考该方法将域名同时只想Github和Gitcafe，使国内和国外用户自动访问gitcafe和github。

![](asset/20151112.jpg)