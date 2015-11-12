---
categories:
- 技术文章
date: 2015-11-10T16:07:41+08:00
description: "hugo+github搭建个人博客 hugo教程 个人博客"
keywords:
- Hugo
- 博客
- 搭建
- 部署
- 多说
- GA
- 教程
Tags:
- hugo
- blog
- 教程
title: "Hugo+Github搭建个人博客图文教程"
url: "2015/11/10/hugoblog"
---
### 什么是Hugo?

> Hugo is a general-purpose website framework. Technically speaking, Hugo is a static site generator. 
简单说就是一个静态网站、个人博客工具，和其他博客工具jekyll相比，hugo不需要安装，仅需要一个二进制文件hugo(hugo.exe)。

<!--more-->

### 静态网站生成器
静态网站与动态网站最大的不同是不需要调用数据库生成页面，再返回给用户，而是在访问时直接返回现成的静态页面。
采用静态页面最大的好处就是访问速度快，不需要每次都重新生成页面。博客文章可以在本地以文本的方式维护，不需要使用数据库保存这些文本。

我的Hugo博客：[http://blog.h5super.com/](http://blog.h5super.com/)  ~~刚刚搭建完成，继续完善中

### GitHub Pages

可以直接把网站托管到GitHub Pages。你只需要在GitHub上创建一个项目，然后将生成出来的静态页面文件(public目录下)push到这个项目的gh-pages分支，保证根目录有一个index.html文件即可。这样，一个免费、无限流量的博客系统就搭建完成了。同时，通过github你可以方便对博客文章进行管理和追踪。这样既不会丢失，也能追溯到每一次的内容变化。

### Hugo

Hugo是什么？它主要做了什么？

 1. Hugo只有一个二进制文件（比如Windows里只是一个hugo.exe，我是在windows下面使用的）
 1. Hugo可以将你写好的MarkDown格式的文章自动转换为静态的网页。
 1. Hugo内置web服务器，可以方便的用于本地调试。

### Hello Hugo

Hugo官方主页：[https://gohugo.io/](https://gohugo.io/)

Hugo二进制下载地址：[https://github.com/spf13/hugo/releases](https://github.com/spf13/hugo/releases)

下载下来后，只有一个叫hugo或者hugo.exe的程序。
开始生成自己的站点：

```bash
$ hugo.exe new site myblog
```

然后进入myblog目录下:
```bash
$ cd myblog
```

会看到这样一个目录结构：

```bash
  ▸ archetypes/
  ▸ content/
  ▸ layouts/
  ▸ static/
    config.toml
```

这几个文件夹的作用分别是：

- archetypes：包括内容类型，在创建新内容时自动生成内容的配置
- content：包括网站内容，全部使用markdown格式
- layouts：包括了网站的模版
- static：包括了css, js, fonts, media等资源文件
- config.toml：是网站的配置文件，这是一个TOML文件，全称是Tom's Obvious, Minimal Language。如果你不喜欢这种格式，你可以将config.toml替换为YAML格式的config.yaml，或者json格式的config.json。

创建一个页面：

```bash
$ hugo.exe new about.md
```

如果是博客日志，最好将md文件放在content的post目录里。

```bash
$ hugo.exe new post/firstpage.md
```

执行完后，会在content/post目录自动生成一个MarkDown格式的firstpage.md文件：

```
+++
date = "2015-11-10T17:02:16+08:00"
draft = true
title = "firstpage"

+++
```

+++可以替换为Jekyll一样的\-\-\-，里面的内容是这篇文章的一些信息。下面就可以开始写你的文章内容，比如：

```
+++
date = "2015-11-10T17:02:16+08:00"
draft = true
title = "firstpage"

+++

### Hello Hugo

This is my first blog.

```

同样的方法，你也可以在about.md添加一些内容。然后执行命令
```bash
$ hugo.exe server
```
浏览器里打开：http://127.0.0.1:1313,发现什么也没有，为什么呢？这是由于Hugo默认生成的网站没有任何theme,我们可以从github上下载其
中一个模板,创建一个目录themes：
```bash
$ cd themes
$ git clone https://github.com/spf13/hyde.git
```

再次启动本地调试：

```bash
$ hugo.exe server --theme=hyde --buildDrafts --watch
```

浏览器里打开：http://127.0.0.1:1313

--watch或者-w 选项打开的话，将会监控到文章的改动从而自动去刷新浏览器，不需要自己手工去刷新浏览器，非常方便。

更详细的文档请看：

官方文档：[https://gohugo.io/overview/introduction/](https://gohugo.io/overview/introduction/)

皮肤列表：[https://github.com/spf13/hugoThemes](https://github.com/spf13/hugoThemes)

### 添加评论功能
我是采用多说评论插件，[www.duoshuo.com](http://www.duoshuo.com)，按照提示操作即可。

### Github 部署
在GitHub上创建一个Repository，命名为：`username.github.io` （username替换为你的github用户名）。

在站点根目录执行 `Hugo` 命令生成最终页面：

```bash
$  hugo.exe server --theme=hyde --buildDrafts --watch  -b "http://username.github.io" --appendPort=false
```
```bash
$ cd public
$ git init
$ git remote add origin https://github.com/username/username.github.io.git
$ git add -A
$ git commit -m "first commit"
$ git push -u origin master
```
如果一切顺利，所有静态页面都会生成到 `public` 目录，将pubilc目录里所有文件 `push` 到刚创建的Repository的 `master` 分支。
如果提交过程中有问题，请参照这篇文章[my.oschina.net/juwenz/blog/153350](http://my.oschina.net/juwenz/blog/153350)

参考文章：
  [HugoQuickstart Guide](https://gohugo.io/overview/quickstart/)

