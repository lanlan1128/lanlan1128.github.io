---
layout: post
title: "在nodejs+express中使用session"
date: 2017-05-08
---

## session
<p>
考虑这样一个场景，你进入一个网站，例如淘宝，首先需要进行登录，登录后进入首页，首页有头部，显示你的用户名。当你点击某个商品时，跳转到商品详情页，头部仍然会有你的用户名。当你关闭这个标签页重新进入网站，不需要进行登录操作可以直接进入首页。当你关闭浏览器，在你没有选择记住密码的状态下，再次进入淘宝网，首先呈现在你面前的还是登录页。还有一种情况是，当你登录淘宝后，过一段时间再刷新页面，页面会重定向到登录页要求你再次登录。这一些系列的登录状态维护都是通过session来控制的。
</p>

<p>
众所周知，http是无状态协议。客户端在发起新的请求时，http请求是不会携带用户信息的，这就导致服务端无法保存用户登录状态，识别用户功能。
</p>

<p>
基于这种需求，session应运而生。例如用session做登录验证。当客户端向服务端发起请求时，服务器根据检查请求头是否有cookie保存sessionID，根据sessionID查找登录session。检查是否有相应的用户id，如果存在，则直接进入首页。如果不存在，返回登录页面。当用户登录成功后，把用户id存入这个session中。在session的生命周期内，用户都保持为登录状态。
</p>

## 在nodejs+express中使用session

{::options parse_block_html="true" /}
<p>
在nodejs+express中使用session需要用到 [express-session](https://www.npmjs.com/package/express-session)
</p>

<p>
第一次使用session的人，看了<b>session</b>中对session的介绍，可能会觉得session的使用很复杂，其实express-session把复杂的部分都实现好了。我们只要了解session是怎么实现的就可以了。在使用session过程中，只需要定义好session中间件（了解express中间件的定义）。然后用session存取数据。就几个简单的操作，下面用一个例子做示范。
</p>

## 用express-session实现登录验证的功能
1. 用express-generator生成项目目录 [express应用生成器](http://www.expressjs.com.cn/starter/generator.html)
2. npm install express-session --save
3. 定义session中间件

{% highlight bash %}
	var session = require('express-session');

	// 使用express中间件
	app.use(session({ 
		secret: '',    // reqiured option  ->  对session ID cookie签名
	}));

	// 在所有路径的前面定义一个登录中间件
	app.use(function(req, res, next) {
		if(!req.session.logined) {
			if(req.path === '/login') {
				next();
			} else {
				res.redirect('/login');
			}
		}else {
			next();
		}
	});
	
	// 登录页面登录验证
	router.get('/login', function(req, res, next) {
		if(req.session && req.session.logined) {
			res.redirect('/');
		}else {
			res.render('login', {username: req.cookies.username, password: req.cookies.password});
		}
	});

	// 登录
	router.post('/login', function(req, res, next) {
		var username = req.body.username;
		var password = req.body.password;
		var rememberPass = req.body.rememberPass;

		// 登录验证，通过验证后
		// 设置session
		req.session.logined = true;

		res.json({
			retflg: true,
			retmsg: '登录成功'
		});

	});
{% endhighlight %}





