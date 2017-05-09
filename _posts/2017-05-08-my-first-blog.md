---
layout: post
title: "如何建自己的个人技术博客 - 新手推荐"
date: 2017-05-08
---

## 背景
本篇文章适用于没有域名，想要搭建一个简单的静态博客的人参考

下面引用知乎中王超的回答，从他的建议中，我决定用github pages搭建自己的博客
[原文地址](https://www.zhihu.com/question/19907364)。这篇文章就是我用github pages写的第一篇博客。

{::options parse_block_html="true" /}
<div>
![Alt text](/images/post1_img1.png) 
</div>

<br />

## 如何搭建
## 1. 创建github账号
用github pages搭建博客，你需要一个github账号，相信作为一个技术猿，人人应该都有一个github账号，如果你还没有，建议你现在就到 [github](https://github.com){: target="_blank"} 创建一个账号吧。

## 2. 创建github pages项目
这里贴出github官网上的一个创建github page的地址：[github pages](https://pages.github.com/){: target="_blank"}

## 3. 熟悉git的基本操作
如果你对git不熟，你可能对于上面的操作流程不太理解，如果不理解，请参阅这篇文章 [手把手教你使用git](blog.jobbole.com/78960/){: target="_blank"}，跟着作者的思路操作，基本上你就能掌握git的操作了。

## 4. 用jekyll写博客
完成上面的步骤，基本上你就可以用html编写你的博客，并且发布到github上并且通过网络访问了。

博客都有固定的头尾布局、拥有博客列表。如果用纯html编写博客，在头尾和博客列表的维护上存在很多冗余繁杂的工作。于是就出现了jekyll。关于jekyll的更多优势，你可以在使用中慢慢总结。

[A Guide to Creating and Hosting a Personal Website on GitHub](http://jmcglone.com/guides/github-pages/) 这篇文章简单的介绍了为什么要使用jekyll。最主要的是
跟着他的教程用github page创建一个jekyll博客，
当你照着它的步骤全部实现后，你发现jekyll完全是你想要的，go ahead。

## 5. 安装jekyll
为什么要在本地安装jekyll？
每次你修改了博客内容，如果要预览，就要把每次修改的内容提交到github上，但是如果你安装了jekyll，就可以在本地上实现预览（在浏览器上输入类似http:/127.0.0.1:4000） 直到你的文章排版达到你要的效果，在提交到github上，就可以省去很多不必要的工作。

1. 安装ruby（Jekyll使用动态脚本语言Ruby写成）ruby在不同平台上的安装方法会有所不同。网上有很多教程，但是对于新手来说，理解起来总是困难的。最好是在官网平台寻找相关的教程。我用的是window平台，在安装ruby上花了很多时间，最好jekyll官网上找到一篇很实用的教程,在 [jekyll installation](http://jekyllrb.com/docs/installation/#requirements) 上找到。点击图示的链接地址，跟着教程走就可以了。
	{::options parse_block_html="true" /}

	<div>
	![Alt text](/images/post1_img2.png) 
	</div>

2. 安装完jekyll之后，用jekyll初始化一个博客项目。[jekyll quickstart](http://jekyllrb.com/docs/quickstart/) 
	{::options parse_block_html="true" /}

	<div>
	![Alt text](/images/post1_img3.png) 
	</div>

3. 用jekyll调试github pages项目。把你在上一步中创建的myblog文件夹下的Gemfile、Gemfile.lock两个文件放置到你的github pages项目，并且在.gitignore这个文件中把上面两个文件名写入（告诉github不要提交这两个文件）。

注意事项：如果你用浏览器打开localhost:4000,出现空白页面，需要写把4000端口关闭，然后再开启jekyll服务。

