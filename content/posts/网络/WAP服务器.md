---
title: "WAP服务器"
description: 
date: 2022-07-12T14:37:29+08:00
draft: false
categories:
  - network
tags:
  - WAP
---

-----
# 网络层复习
- 应用层：解决要传递什么数据
- 传输层：解决如何传递数据，使用udp,tcp理解位快递公司
- 网络层：定位目标的ip地址
- 链路层：使用工具进行传输
- 建立链接的三次握手
- 数据传输
- 断开链接的四次挥手
<!--more-->
---

# HTTP协议
- 而浏览器和服务器之间的传输协议是HTTP
- HTML是一种用来定义网页的文本，会HTML，就可以编写网页；
- HTTP是在网络上传输HTML的协议，用于浏览器和服务器的通信
- cookie写入：字典方式，key:value
- cookie:
- 只要访问浏览器服务器会默认向客户端写入一些信息：key:value(respomse)---->保存到浏览器的cookice
- 目的：
- key:value--->jseesionID:xxxxx
- 作用1:
- 第二次又去访问服务器，request请求中携带jsessionID去服务器，服务器收到携带的jsessionid之后，就知道是否曾经访问过网站
- 作用2:
- cookie中可以保存一些相关的数据
- HTTP请求由四部分组成：请求行，请求头，空行，请求体
### request:客户端请求
- GET / HTTP/1.1请求行
- HTTP请求方式：
- GET  获取信息，让服务器返回文本或者图片、html的代码等
- POST 修改已经存在的数据，修改成什么样子，携带数据给服务器（修改信息）
- PUT 保存数据，也可以使用get和post
- DELETE 删除数据 也可以使用get和post
- OPTION 询问服务器的某种支持特性
- HEAD 返回数据，仅仅返回报文头
- TRACE：请求服务器回送收到的请求信息，用于测试或诊断
- 主要区别在于1.1版本允许多个HTTP请求复用一个TCP连接，以加快传输速度。
- Host：主机名
- User-Agent：用户代理，使用说明浏览器或者什么操作系统
- Accept-Language：服务器支持语言
- Cache-Control：no-cache网页缓存控制（每次都会访问）max-age过期之前不会重复访问。
- Accept-Encoding：申明自己接收的编码方法
- Connection:keep-alive 连接方式保存活跃（长连接）
- Pragma:no-cache 缓存来源no-cache信息，不缓存页面数据
- Accept-Charset：请求报头域用于指定客户端接受的字符集，缺省表示任何字符集都可以接受
- Date：请求发送的时间和日期
- Except：请求特定的服务器行为
- If-Match：请求内容与实体相匹配才有效
- If-Modified-Since：如果请求的部分在指定时间之后被修改则请求成功，未被修改则返回304代码
### response:服务器回应
- 一个http响应报文由：响应行 、响应头、空行和响应数据（响应体）4个部分组成，
- Content-Type指示响应的内容，这里是text/html表示HTML网页。
- Location：用于重定向接受者到一个新的位置
- Content-Language：响应体的语言
- Content-Length：响应体的长度
- Date：原始服务器消息发出的时间
- refresh：表示浏览器应该在多少时间之后刷新文档，以秒记。
- Server：web服务器软件名称。如：Server: Apache/1.3.27 (Unix) (Red-Hat/Linux)
- Set-Cookie：设置Http Cookie
- 浏览器获取你的响应体里面的内容并翻译展示给浏览器界面
- 响应行：
- HTTP/1.1（HTTP协议版本1.1）200状态码 OK（说明成功）
### HTTP请求过程
-  步骤1：浏览器首先向服务器发送HTTP请求，请求包括：
-  方法：GET还是POST，GET仅请求资源，POST会附带用户数据；
-  路径：/full/url/path；
-  域名：由Host头指定：Host: www.baidu.com
-  如果是POST，那么请求还包括一个Body，包含用户数据，例如上传图片的数据等（响应体）
-  步骤2：服务器向浏览器返回HTTP响应，响应包括：
-  响应代码
-  响应类型：由Content-Type指定；
-  通常服务器的HTTP响应会携带内容，也就是有一个Body，包含响应的内容，网页的HTML源码就在Body中
-  步骤3：如果浏览器还需要继续向服务器请求其他资源，比如图片，就再次发出HTTP请求，重复步骤1、2。
-  一个HTTP请求只处理一个资源(此时就可以理解为TCP协议中的短连接，每个链接只获取一个资源，如需要多个就需要建立多个链接)
-  步骤4：浏览器根据返回的数据进行解析，最终呈现在我们面前
### HTTP格式
-  一个HTTP包含Header和Body两部分，其中Body是可选的。
-  HTTP协议是一种文本协议
-   HTTP GET请求的格式：
-        GET /path HTTP/1.1
        Header1: Value1
        Header2: Value2
        Header3: Value3
- 每个Header一行一个，换行符是\r\n
-  HTTP POST请求的格式：
-       POST /path HTTP/1.1
        Header1: Value1
        Header2: Value2
        Header3: Value3

        body data goes here...

- 当遇到连续两个\r\n时，Header部分结束，后面的数据全部是Body。
- HTTP响应的格式：
-      200 OK
        Header1: Value1
        Header2: Value2
        Header3: Value3

        body data goes here...
- HTTP响应如果包含body，也是通过\r\n来分隔的。
- Body的数据类型由Content-Type头来确定如果是网页，Body就是文本，如果是图片，Body就是图片的二进制数据。
- 当存在Content-Encoding时，Body数据是被压缩的，最常见的压缩方式是==gzip==
- 需要将Body数据先解压缩gzip解压缩才能得到真正的数据
### Get请求携带数据量的各种限制及解决办法、Post请求说明 
- Get请求携带数据量的各种限制及解决办法
- Http Get方法提交的数据大小长度并没有限制，HTTP协议规范没有对URL长度进行限制。这个限制是特定的浏览器及服务器对它的限制。
- URL最好不要超过IE的最大长度限制(2083个字符），当然，如果URL不直接提供给用户，而是提供给程序调用，这时的长度就只受Web服务器影响了。
- 注：对于中文的传递，最终会为urlencode后的编码形式进行传递，如果浏览器的编码为UTF8的话，一个汉字最终编码后的字符长度为9个字符。
-  POST请求长度限制：
-  理论上讲，POST是没有大小限制的。HTTP协议规范也没有进行大小限制，起限制作用的是服务器的处理程序的处理能力。
### 扩展URI和URL
-  URI的子集URL
-  什么是URI？：
-  Web上每种可用的资源，如 HTML文档、图像、视频片段、程序等都由一个通用资源标志符(Universal Resource Identifier， URI)进行定位。 
-  URI通常由三部分组成：
-  ①访问资源的命名机制； http://
-  ②存放资源的主机名；www.baidu
-  ③资源自身 的名称，由路径表示。/html/html
-  URL的格式由三部分组成： 
-  URL是URI的一个子集。它是Uniform Resource Locator的缩写，译为“统一资源定位 符”。
-  URL是Internet上描述信息资源的字符串，主要用在各种WWW客户程序和服务器程序上。
-  URL的一般格式为(带方括号[]的为可选项)：
-  protocol :// hostname[:port] / path / [;parameters][?query]#fragment
-  第一部分是协议(或称为服务方式) protocol
-  第二部分是存有该资源的主机IP地址(有时也包括端口号)
-  第三部分是主机资源的具体地址，如目录和文件名等。
-  第一部分和第二部分用“://”符号隔开，第二部分和第三部分用“/”符号隔开。
-  第一部分和第二部分是不可缺少的，第三部分有时可以省略
### URL和URI简单比较（关键）
-  但也不是所有的URI都是URL哦
-  让URI能成为URL的当然就是那个“访问机制”，“网络位置”
-  例如.http:// or ftp://.
-  ==URN是唯一标识的一部分，就是一个特殊的名字。==
-  换句话说，URI属于父类，而URL属于URI的子类。URL是URI的一个子集。
-  URI的定义是：统一资源标识符；
-  URL的定义是：统一资源定位符。
-  二者的区别在于，URI表示请求服务器的路径，定义这么一个资源。
-  而URL同时说明要如何访问这个资源（http://）。
-  爬虫最主要的处理对象就是URL，它根据URL地址取得所需要的文件内容，然后对它 进行进一步的处理。
### URN
-  统一资源名称 (Uniform Resource Name, URN)
-  唯一标识一个实体的标识符，但是不能给出实体的位置。系统可以先在本地寻找一个实体，在它试着在Web上找到该实体之前。它也允许Web位置改变，然而这个实体却还是能够被找
-  URI和URL和URN
-  URI包括URL,URN其中L(location)代表位置N代表名字name
-  URL代表资源的地址信息，URN则代表某个资源独一无二的名称
-  由于URL或URN的目的，都是用来标识某个资源，后来的标准指定了URI，而URL与URN成为URI的子集

