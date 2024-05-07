---
title: "TOKEN验证详解"
date: 2019-10-01T14:03:37+08:00
draft: false
categories:
  - token
---
<!--more-->

# 为什么使用token验证

- 在web领域基于token的身份验证随处可变，在大多说使用web API的互联网公司中，tokens是多用户下处理认证的最佳方式

## 一下几点特性会让你在程序中使用基于Token 的身份验证

- 无状态、可扩展
- 支持移动设备
- 跨程序调用
- 安全
- 那些使用基于Token的身份验证的大佬们
- 大部分你见到过的API和WEB应用都是用tokens，列如facebook, twitter, google+, github等

## Token的起源
- 在介绍基于token的身份验证的原理与优势之前，不妨先看看之前的认证都是怎么做的

        基于服务器的验证
        我们都是知道HTTP协议是无状态的，这种无状态意味着程序需要验证每一次请求，从而辨别客户端的身份。
        在这之前，程序都是通过在服务端存储的登录信息来辨别请求的。这种方式一般都是通过存储Session来完成。
        随着Web，应用程序，已经移动端的兴起，这种验证的方式逐渐暴露出了问题。尤其是在可扩展性方面。

## 基于服务器的验证方式暴露的一些问题

    1、session：每次认证用户发起请求时， 服务器需要去创建一个记录来存储信息， 当越来越多的用户发请求时， 内存的开销也会不断增加

    2、可获振兴：在服务端的内存中使用session存储的登录信息，办所而来的是可扩展性问题

    3、CORS（跨域资源共享）： 当我们需要让数据跨多台移动设备上使用时， 跨域资源共享回事一个让人头疼的问题， 在使用ajax抓取另一个域的资源，就可以会出现禁止请求的情况

    4、CSRF（跨站请求伪造）： 用户在访问银行网站时， 他们很容易受到跨站请求伪造的攻击， 并且能够被利用其访问其他网站

    在这些问题中，可扩展性是最突出，因此我们有必要去寻求一种更有行之有效的方法

## 基于TOKEN的验证原理

    基于Token的身份验证是无状态的，我们不将用户信息存在服务器或Session中。

    这种概念解决了在服务端存储信息时的许多问题

    　　NoSession意味着你的程序可以根据需要去增减机器，而不用去担心用户是否登录。

    基于Token的身份验证的过程如下:

    1.用户通过用户名和密码发送请求。

    2.程序验证。

    3.程序返回一个签名的token 给客户端。

    4.客户端储存token,并且每次用于每次发送请求。

    5.服务端验证token并返回数据。

    每一次请求都需要token。token应该在HTTP的头部发送从而保证了Http请求无状态。我们同样通过设置服务器属性Access-Control-Allow-Origin:* ，让服务器能接受到来自所有域的请求。需要主要的是，在ACAO头部标明(designating)*时，不得带有像HTTP认证，客户端SSL证书和cookies的证书。

## 代码实例流程：

```js
//用户第一次登录
username pwd client_type 
//接口判断
if(token&uid){
   查询token表
    $token=where uid =uid 
    if($token==token){
      登录成功！！
          返回token 和 uid
    }else{
      登录失败！！
    }
}

if(usename powd client_type){
     检验用户名和密码
    if（正确）{
       得到uid 并 生成token（md5( uid.pwd.time() 自己定义规则 )）
        if(uid不存在){
            into token 表   id uid token
        }else{
            where uid=$uid 修改token
        }
        返回token 和 uid
    }else{
        返回错误信息；    
        }
}

```

## 客户端c进行文件存储uid 和token

    下次再次登录时使用uid和token
    实现了用户登录的互踢
    当我们在程序中认证了信息并取得token之后，我们便能通过这个Token做许多的事情。

    我们甚至能基于创建一个基于权限的token传给第三方应用程序，这些第三方程序能够获取到我们的数据（当然只有在我们允许的特定的token）

## Tokens的优势
- 无状态、可扩展

        在客户端存储的Tokens是无状态的，并且能够被扩展。基于这种无状态和不存储Session信息，负载负载均衡器能够将用户信息从一个服务传到其他服务器上。

        如果我们将已验证的用户的信息保存在Session中，则每次请求都需要用户向已验证的服务器发送验证信息(称为Session亲和性)。用户量大时，可能会造成一些拥堵。但是不要着急。使用tokens之后这些问题都迎刃而解，因为tokens自己hold住了用户的验证信息。

## 安全性

    请求中发送token而不再是发送cookie能够防止CSRF(跨站请求伪造)。即使在客户端使用cookie存储token，cookie也仅仅是一个存储机制而不是用于认证。不将信息存储在Session中，让我们少了对session操作。 

    token是有时效的，一段时间之后用户需要重新验证。我们也不一定需要等到token自动失效，token有撤回的操作，通过token revocataion可以使一个特定的token或是一组有相同认证的token无效。

## 可扩展性（）

    Tokens能够创建与其它程序共享权限的程序。例如，能将一个随便的社交帐号和自己的大号(Fackbook或是Twitter)联系起来。当通过服务登录Twitter(我们将这个过程Buffer)时，我们可以将这些Buffer附到Twitter的数据流上(we are allowing Buffer to post to our Twitter stream)。

    使用tokens时，可以提供可选的权限给第三方应用程序。当用户想让另一个应用程序访问它们的数据，我们可以通过建立自己的API，得出特殊权限的tokens。

## 多平台跨域

    我们提前先来谈论一下CORS(跨域资源共享)，对应用程序和服务进行扩展的时候，需要介入各种各种的设备和应用程序。

    Having our API just serve data, we can also make the design choice to serve assets from a CDN. This eliminates the issues that CORS brings up after we set a quick header configuration for our application.

    只要用户有一个通过了验证的token，数据和资源就能够在任何域上被请求到。

<span style="margin:0px; padding:0px; color:rgb(255,255,255); background-color:rgb(0,0,0)"><code class=" language-javascript" style="margin:0px; padding:0px">          Access<span class="token operator" style="margin:0px; padding:0px">-Control<span class="token operator" style="margin:0px; padding:0px">-Allow<span class="token operator" style="margin:0px; padding:0px">-Origin<span class="token punctuation" style="margin:0px; padding:0px">: <span class="token operator" style="margin:0px; padding:0px">*       <br style="margin:0px; padding:0px" /></span></span></span></span></span></code></span>

## 基于标准

    创建token的时候，你可以设定一些选项。我们在后续的文章中会进行更加详尽的描述，但是标准的用法会在JSON Web Tokens体现。

    最近的程序和文档是供给JSON Web Tokens的。它支持众多的语言。这意味在未来的使用中你可以真正的转换你的认证机制。

## 总结
    这篇文章仅仅是介绍了为什么选择基于Token的身份验证，并且怎样使用它。

