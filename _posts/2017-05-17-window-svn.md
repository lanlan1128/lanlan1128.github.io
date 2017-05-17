---
layout: post
title: window下svn的使用
date: 2017-05-08
---

## 使用svn命令行
如果你安装了TortoiseSVN，打开命令行后，发现提示 command not found，证明你在安装TortoiseSVN的时候，没有选择命令行组件。

解决方案：
1. 重新安装TortoiseSVN，安装过程中选择用svn命令行组件

	{::options parse_block_html="true" /}

	<div>
	![Alt text](/images/post1_img4.png) 
	</div>

<br/><br/>

## 让SVN(TortoiseSVN)提交时忽略node_modules目录（windows）
刚开始想用svn命令行来操作，发现自己对命令行不熟悉，想找一种更快捷的方式。网上找了很多资料，发现一篇博客刚好是我需要的。 [让 SVN (TortoiseSVN)提交时忽略bin和obj目录](http://www.cnblogs.com/yelaiju/p/3145297.html).

大概步骤如下：
1. 打开TortoiseSVN properties属性编辑窗口

	<div>
	![Alt text](/images/post1_img5.png){: .img-m}
	</div>

2. 选择高级选项

	<div>
	![Alt text](/images/post1_img6.png){: .img-m}
	</div>

3. 编辑ignore规则

	<div>
	![Alt text](/images/post1_img7.png){: .img-m}
	</div>

	<span class="tip-s">提示：上图填写的内容为<br>svn:ignore<br>node_modules</span>