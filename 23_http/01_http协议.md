## http

概念: 超文本传输协议 ( Hyper Text Transfer Protocol )

定义了客户端和服务器通信时, 发送数据的格式

##### 特点 

1. 基于 TCP/IP 协议
2. 默认端口号: 80
3. 基于请求 / 响应模型的: 一次请求对应一次响应.
4. 无状态的: 每次请求之间相互独立, 不依赖于上一次请求.



##### 历史版本 

目前HTTP协议的版本就是1.1, 但是大部分服务器也支持1.0版本, 主要区别在于1.1版本允许多个HTTP请求复用一个TCP连接, 以加快传输速度.



##### 请求消息数据格式

每个HTTP请求和响应都遵循相同的格式, 一个 HTTP 请求包含Header和Body两部分, 其中Body是可选的.

分为 4 个部分:

1. 请求行

   请求方式    url     协议/版本

   GET  https://www.google.com/  HTTP/1.1

2. 请求头

   User-Agent: 浏览器告诉服务器, 使用的浏览器版本信息.

   Referer: http://localhost/login.html  ( 防盗链, 统计工作(从哪儿来) )

3. 请求空行

   用于分割请求头与请求体

4. 请求体 ( 正文 )

   body ( 只有 POST 方法才有请求体 )



##### 响应消息数据格式

1. 响应行

   ```
   HTTP/2.0 200 OK
   ```

2. 响应头

   ```
   Accept-Ranges: bytes
   Content-Length: 362
   Content-Type: text/html
   Date: Fri, 22 Nov 2019 13:22:38 GMT
   ETag: W/"362-1574257176387"
   Last-Modified: Wed, 20 Nov 2019 13:39:36 GMT
   Server: Apache-Coyote/1.1
   ```

3. 响应空行

4. 响应体

   ```html
   <!DOCTYPE html>
   <html lang="en">
   <head>
       <meta charset="UTF-8">
       <title>UserLogin</title>
   </head>
   <body>
       <form action="/login" method="post">
           用户名: <input type="text" name="username"> <br>
           密码:    <input type="password" name="passwd"> <br>
           <input type="submit" value="login">
       </form>
   </body>
   </html>
   ```



##### 响应状态码

1xx: 服务器接收客户端消息, 但没有接收完成, 等待一段时间后, 发送 1xx 状态码

2xx: 成功

3xx: 重定向, 302 (重定向), 304 (访问缓存)

4xx: 客户端错误, 400 (请求无效),  404 (没有对应的资源),  405(请求方式不被允许)

5xx: 服务器内部发生错误.



###### 完 !