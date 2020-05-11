---
layout: post
title: "session 和 token 的工作原理"
date: 2020-05-09 15:21:00 +0800
categories: nodejs
tags:
  - session
  - token
  - Nodejs
  - express
---

- content
  {:toc}
  介绍 session 和 token 的工作原理

<!-- more -->

---

## session

session 技术是为了解决 http 协议是无状态的协议（即 http 协议无法让服务端识别两个请求是否来自同一个客户端）而建立机制。session 的工作流程一般如下：

- 1.客户端向服务端发送请求
- 2.服务端接收到请求后，给每个客户端生成唯一的标识 sessionID， 如果 sessionID 是首次生成，则在响应头的 set-cookie 字段写入 sessionID
- 3.客户端以后向服务端发送请求时，请求头会自动携带 cookie，服务端即可通过请求头获取 cookie 中的 sessionID

流程图参考：  
![session+cookie工作流程]({{ '/styles/images/server/session.png' | prepend: site.baseurl }}){:width="500"}

示例 demo 见下文

## token

token 是获取信息的凭证。JWT 是其中一种实现方式。可以理解为用户登录成功后，服务端给用户发送一个用户的令牌（包含用户信息），客户端把令牌存储在本地，以后每次向服务端发请求时携带上令牌，服务端验证用户令牌是否有效。关于 JWT 的工作原理和用法，可以参考阮一峰老师的[JSON Web Token 入门教程](https://www.ruanyifeng.com/blog/2018/07/json_web_token-tutorial.html)

### 存储 token 的方式

- 1.存储到 cookie 中
- 2.存储到 localStorage 中

### 客户端发送 token 的方式

- 1.可以把 token 放到 cookie 中，以后每次请求可以自动发送，但是这样跨域不能访问
- 2.可以把 token 写到每次请求的请求头的 Authorization 字段，对于 get 请求，可以写道 url 后面
- 2.可以把 token 放入到请求体中

示例 demo 见下文

## session 和 token 对比

### session+cookie 实现的缺陷

- 1.分布式服务的 session 不能实现共享。需要对 session 做持久化管理
- 2.服务端通过 set-cookie 的方式向客户端写入 cookie，客户端的请求就会自动携带 cookie，容易被其它网站攻击（详见上面的示例 demo）

### token 的安全性比 session+cookie 高

示例 demo：
[nodejs+express 实现的 session 登录](https://github.com/lanlan1128/session_token_simple_demo)
