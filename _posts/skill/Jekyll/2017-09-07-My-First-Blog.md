---
layout: post
title: "新手推荐 - 如何搭建一个技术博客"
data: 2017-09-07 16:04:00 +0800
categories: 站点建设
tag: Jekyll
---

- content
  {:toc}
  本篇文章介绍如何在没有域名的情况下，用`github pages`搭建一个`技术博客`。仅作参考以及本人回顾。错误之处，请留言指正。

<!-- more -->

---

## 引言

下面引用知乎中[王超的回答](https://www.zhihu.com/question/19907364)，从他的建议中，我决定用`github pages`搭建自己的博客。

![知乎回答]({{ '/styles/images/jekyll/2017-09-07-01.png' | prepend: site.baseurl }})

---

## 快速入门

这篇文章[A Guide to Creating and Hosting a Personal Website on GitHub](http://jmcglone.com/guides/github-pages/)详细的介绍了如何用 github page 创建一个 Jekyll 博客。包括创建一个帖子，创建一个页面来列出我们的帖子，为帖子创建自定义的链接，为博客创建 RSS。文末还有相关扩展的资源的链接。
当你照着它的步骤全部实现后，你发现 jekyll 完全是你想要的，go ahead。

### 为什么要用 jekyll

博客都有固定的头尾布局、拥有博客列表。如果用纯 html 编写博客，在头尾和博客列表的维护上存在很多冗余繁杂的工作。于是就出现了 jekyll。关于 jekyll 的更多优势，你可以在使用中慢慢总结。

> 通过上面的教程，你知道 github pages 提供 jekyll 来编译你的项目。但是如果通过这种方式创建博客，每次你修改了博客内容，如果要预览，就要把每次修改的内容提交到 github 上，所以你需要在本地上安装 jekyll，实现本地预览，直到你的文章排版达到你要的效果，再提交到 github 上，就可以省去很多不必要的工作。

## 进阶

### 本地搭建 jekyll

#### 安装 Ruby 和 RubyGems

[`Ruby`](http://www.ruby-lang.org/zh_cn/downloads/)是一门语言，不用多解释。而[`RubyGems`](https://rubygems.org/pages/download)其实就是`Ruby`的包管理工具。相当`npm`和`Node`的关系。

因为`Jekyll`是用`Ruby`语言编写的，所以我们需要安装他们。`Ruby`在不同平台上的安装方法会有所不同。网上有很多教程，但是对于新手来说，理解起来总是困难的。最后是在官网平台寻找相关的教程。我用的是 window 平台，在安装 ruby 上花了很多时间，最好 jekyll 官网上找到一篇很实用的教程,在 [Running Jekyll on Windows](http://jekyllrb.com/docs/windows/#installation) 上找到。点击图示的链接地址，跟着教程走就可以了。

> 有时候我们在某些环境下(比如墙内或公司内网)可能不能正常使用 gem，这里提供了参考的解决方案[设置 git/npm/bower/gem 镜像或代理的方法](https://segmentfault.com/a/1190000002435496#item-2-7)

> 有关 Jekyll 的具体内容参考：
>
> - 中文官方主页： [http://jekyll.com.cn/](http://jekyll.com.cn/)
> - 英文官方主页： [https://jekyllrb.com/](https://jekyllrb.com/)

### 选择 Jekyll 模板

当我们安装好 jekyll，并且按[教程](http://jekyll.com.cn/docs/quickstart/)启动 jekyll 之后，可以看到`Jekyll`为你生成的页面非常简便。
这个时候，你可以选择用 jekyll 模板来完善自己的博客站点，如何使用 jekyll 模板

- 专门收集模板的网站：[http://jekyllthemes.org/](http://jekyllthemes.org/)
- 在`Google`上搜索`Jekyll`和`Github`，在人家的仓库中`download`别人的模板(要注意人家是否允许拷贝哦)。

---

## 注意事项

> 如果你用浏览器打开 localhost:4000,出现空白页面，需要写把 4000 端口关闭，然后再开启 jekyll 服务。
