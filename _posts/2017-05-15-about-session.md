---
layout: post
title: "在nodejs+express中使用session"
date: 2017-05-08
---

## session
当你要理解一项技术的技术的时候，首先应该从这项技术的应用场景开始理解。这样才能由浅入深。
我一开始需要用到session是在做登录验证的时候。于是我在网上找到一很通俗易懂的文章 [关于用户登录session](http://blog.csdn.net/u013865275/article/details/51159102)<br />

<span class="tip-s">下面贴上文章内容（防止文章丢失哈哈，个人觉得写得很好）：</span>
<div class="content">
 首先我们先来了解一下什么是session。其实session就是一块在服务器端开辟的内存空间，就好比客户在服务器端的账户，它们被服务器保存到一个Map中，这个Map被称之为session缓存。session的作用是来跟踪用户的操作状态。
<br>
我们举个例子，比如：服务器端要知道一个当前网站有多少用户在线。我们知道一个用户就一个客户端，那么也就是说服务器端要知道有多少客户端正在访问本网 站，这样服务器端必然要跟踪每一个客户端的状态。
<br>
那么服务器是通过什么跟踪的呢？又是怎么跟踪的呢？哈哈，其实这个问题很简单，比如张三下班后打开电脑，今天第一次访问某宝网站，张三的电脑向某宝网站发出了请求，某宝网站我现 在要访问你，这时呢某宝网站说请出示你的证件，张三的电脑傻了问“证件？？？”这时某宝网站说是今天第一次来访吧，张三的电 脑说是啊，某宝的网站说那就对了看在你诚实的份上给你一个证件吧(这里的证件就是我们说的 sessionID，sessionID:是32位的字母和数字的组合是全地球唯一的，因为sessionID是唯一的所以它的作用是用来区分每个客户端 的，此ID是在session被创建时产生的，而session我们看到了是在第一次访问网站时就会被建立。sessionID会随着应答一起发到客户端 并存放到客户端的内存中，这块客户端的内存就是我们经常说的cookie，下次用户发出请求时，浏览器通过一定规则将本地cookie里的sessionid发送，一一匹配，这样服务器看到 sessionID后到内存寻找，找到了就使用此内存中的数据，否则视为第一次访问本网站)，不过这个证件的有效期只有15分钟，这里的有 效期15分钟，就是我们说的session过期时间。
<br>
什么是session过期时间呢？是这样的，我们想一下我们第一次访问一个网站，这时网站会给我们分 配一个sessionID，而我们只是打开了这个首页后，出去玩了再也没有访问过本网站的其它页面内容，我们是不是还在占用着网络资源呀，占用着 sessionID。那么这时怎么办呢？其实网站服务器很聪明的它会在你从第一次访问后就开始计算时间比如张三打开了某宝网站首页这时某宝网站的服务器就开始计时了 ，1秒,2秒,3秒,4秒,5秒,6秒...在2分钟的时候张三在首页上点击了一条热销商品，这时某宝网站的服务器知道后将刚才记的2分钟清空为0 这时又开始了1秒,2秒,3秒,4秒,5秒,6秒...的计时，直至计时时间达到了15分钟也就是session过期时间，这时某宝网站服务 器会认为这个用户15分钟都没有访问过我了可能己经关机出去玩了，某宝网站服务器会将这个用户在服务器开辟的内存空间释放掉，那么对应内存的 sessionID也就被收回了，等待新来的用户使用，这样我们说一个session就被销毁了。
<br>
到这大家应该有点感觉了吧，session的范围有多大呀，是一个客户端，一个客户端对应着一个session ; 而一个session能存活多长时间有两个方面一方面是看客户端是否在session过期时间内访问网站，这样可以让session存活时间延长，另一方 面是设置的session过期时间是多长。session过期时间我们可以手工设置，如果没有设置就采取服务器默认设置的(例如这里用Tomcat可以在Tomcat/config/web.xml中找到一段如下的代码默认为30分钟： 

{% highlight bash %}
<session-config>  
        <session-timeout>30<session-timeout>  
<session-config>  
{% endhighlight %}

我们还可以在我们的项目中的WEB-INF/web.xml中写入上面的这段代码,设置session过期时间)。
好了知道了这些大家想一个问题：如果我们访问了一个网站，这个网站为我们分配了一个session ，我们现在将IE浏览关闭掉，session会销毁吗？哈哈，想都不用再想了肯定不会。因为session是存放在服务器端的session的销毁只和过期时间有关系，再者客户端关闭怎么会影响到服务器端呢！ 
牢记，sessionId是针对客户端的，一个客户端是一个sessionId，这也就是常用的登录注销处理的原因，对于同一个客户端对同一个服务器的访问，会在session中设置一个key value，这样，就算是不同帐号登录，那也只是不同key，而不会是不同session。
如果注销使用session.invalidate的话，也就会出现无法继续登录了。
</div>


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





