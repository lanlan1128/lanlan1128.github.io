---
layout: post
title: windows下svn的使用
date: 2017-09-08
tag: svn 
---
* content
{:toc}

`windows`下`svn`的常用命令行和使用方法

<!-- more -->

---------------

## 使用svn命令行
如果你安装了TortoiseSVN，打开命令行输入svn，提示 command not found，证明你在安装TortoiseSVN的时候，没有选择命令行组件。解决方案有
+ 重新安装TortoiseSVN，安装过程中选择用svn命令行组件<br>
![svn安装]({{ '/styles/images/tool/svn/1.png' | prepend: site.baseurl }}){:width="50%"}

---------------

## svn ignore 
>在开发过程中，我们可能会遇到这种情况，svn目录中的某些文件不想提交到服务器上，例如node_modules文件夹（因为pagepack.json文件已维护了这些信息）。对命令行不熟悉的可以用下面这种更快捷的方法，参考链接 [让SVN(TortoiseSVN)提交时忽略bin和obj目录](http://www.cnblogs.com/yelaiju/p/3145297.html).

步骤如下：
+ 打开TortoiseSVN properties属性编辑窗口<br>
	![svn安装]({{ '/styles/images/tool/svn/2.png' | prepend: site.baseurl }}){:width="50%"}

+ 选择高级选项<br>
	![svn安装]({{ '/styles/images/tool/svn/3.png' | prepend: site.baseurl }}){:width="50%"}


+ 编辑ignore规则<br>
	![svn安装]({{ '/styles/images/tool/svn/4.png' | prepend: site.baseurl }}){:width="50%"}

