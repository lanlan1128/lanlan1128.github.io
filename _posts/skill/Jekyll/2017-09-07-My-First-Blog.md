---
layout: post
title: "新手推荐 - 如何搭建一个技术博客"
data: 2017-09-07 16:04:00 +0800
categories: 站点建设
tag: Jekyll
---
* content
{:toc}


本篇文章介绍如何在没有域名的情况下，用`github pages`搭建一个`技术博客`。仅作参考以及本人回顾。错误之处，请留言指正。

<!-- more -->

---------------

## 引言

下面引用知乎中[王超的回答](https://www.zhihu.com/question/19907364)，从他的建议中，我决定用`github pages`搭建自己的博客。这篇文章就是我的第一篇博客。

![知乎回答]({{ '/styles/images/jekyll/2017-09-07-01.png' | prepend: site.baseurl }})

---------------

## Jekyll相关

### 为什么要用jekyll

博客都有固定的头尾布局、拥有博客列表。如果用纯html编写博客，在头尾和博客列表的维护上存在很多冗余繁杂的工作。于是就出现了jekyll。关于jekyll的更多优势，你可以在使用中慢慢总结。

>在正式使用jekyll之前，你可以通过这篇文章[A Guide to Creating and Hosting a Personal Website on GitHub](http://jmcglone.com/guides/github-pages/)用github page创建一个jekyll博客，当你照着它的步骤全部实现后，你发现jekyll完全是你想要的，go ahead。

有关Jekyll的具体内容参考：

+ 中文官方主页： [http://jekyll.com.cn/](http://jekyll.com.cn/)
+ 英文官方主页： [https://jekyllrb.com/](https://jekyllrb.com/)

>通过上面的教程，你知道github pages提供jekyll来编译你的项目。但是如果通过这种方式创建博客，每次你修改了博客内容，如果要预览，就要把每次修改的内容提交到github上，所以你需要在本地上安装jekyll，实现本地预览，直到你的文章排版达到你要的效果，再提交到github上，就可以省去很多不必要的工作。


### 安装Ruby 和 RubyGems

[`Ruby`](http://www.ruby-lang.org/zh_cn/downloads/)是一门语言，不用多解释。而[`RubyGems`](https://rubygems.org/pages/download)其实就是`Ruby`的包管理工具。相当`npm`和`Node`的关系。

因为`Jekyll`是用`Ruby`语言编写的，所以我们需要安装他们。`Ruby`在不同平台上的安装方法会有所不同。网上有很多教程，但是对于新手来说，理解起来总是困难的。最好是在官网平台寻找相关的教程。我用的是window平台，在安装ruby上花了很多时间，最好jekyll官网上找到一篇很实用的教程,在 [Running Jekyll on Windows](http://jekyllrb.com/docs/windows/#installation) 上找到。点击图示的链接地址，跟着教程走就可以了。


### 安装Jekyll

打开终端，输入以下命令：

```ruby
$ gem install jekyll
```

这就ok了。

### 选择Jekyll模板

当我们安装好jekyll，并且按[教程](http://jekyll.com.cn/docs/quickstart/)启动jekyll之后，可以看到`Jekyll`为你生成的页面非常简陋

这个时候，你可以选择用jekyll模板来完善自己的博客站点，如何使用jekyll模板

+ 专门收集模板的网站：[http://jekyllthemes.org/](http://jekyllthemes.org/)
+ 在`Google`上搜索`Jekyll`和`Github`，在人家的仓库中`download`别人的模板(要注意人家是否允许拷贝哦)。

>选择了模板后要根据自己的需求更改，而且主要是在`_config.yml`文件中。

---------------
## 注意事项
>如果你用浏览器打开localhost:4000,出现空白页面，需要写把4000端口关闭，然后再开启jekyll服务。