## cookie (小甜点)

##### 概念

指某些网站为了辨别用户身份、进行会话跟踪而储存在用户本地的数据（通常经过加密）  (http 是无状态的协议)

在一次会话的多次请求间, 共享数据, 由服务端将数据保存到浏览器中.



##### 使用

1. 服务端创建 cookie 对象, 绑定数据. (键值对形式)
   `new Cookie(String name, String value)`

2. 发送 cookie 对象

   `response.addCookie(Cookie cookie)`

3. 服务端获取 cookie, 拿到数据. (给浏览器设置 cookie 之后, 浏览器每次请求时会在请求头中携带 cookie)

   `Cookie[] request.getCookies()`

4. 获取 cookie 中的 key 和 value

   `cookie.getName()`: 获取 key 值

   `cookie.getValue()`: 获取 value 值



cookie 使用细节:

1. 一次可不可以发送多个 cookie ?

   + Servlet 可以创建多个 Cookie 对象, 使用 response 调用多次 addCookie() 方法即可

2. cookie 在浏览器中保存多久 ? 

   + 默认情况下, 当浏览器关闭后, Cookie 数据被销毁.
   + 持久化存储: `setMaxAge(int seconds)`
     1. 正数: 将Cookie数据写到本地磁盘, seconds 是存活的时间 (s), 时间到达后, cookie 自动清除
     2. 负数: 默认值. (不用设置)
     3. 零: 手动删除 cookie 信息.

3. cookie 能不能存中文 ?

   + 在 tomcat 8 之前的版本, cookie 中不能直接存储中文数据. (需要将中文采用 URL 编码)
   + 在 8 版本之后, cookie 支持中文.

4. cookie 获取的范围 ?

   + 假设在一个 tomcat 服务器中, 部署了多个web项目, 那么在这些 web 项目中 cookie 能不能共享 ?

     1. 默认情况下, cookie 不是共享的.

     2. `setPath(String path)`: 设置cookie的获取范围, 默认情况下, 设置当前的虚拟目录.

        如果需要共享cookie, 那么可以将虚拟目录 path 设置为 "/"

   + 不同的 tomcat 服务器间 cookie 共享问题 ?

     1. `setDomain(String path)`: 如果设置一级域名相同, 那么多个服务器之间 cookie 可以共享.
     2. `setDomain(".baidu.com")`: 那么 tieba.baidu.com 和 news.baidu.com 中 cookie 可以共享.



##### cookie 的特点与作用

1. cookie 存储数据在浏览器中.
2. 浏览器对于单个 cookie 大小有限制(4KB) 以及对同一个域名下的cookie数量是有限制的 (20个)
3. cookie 一般用于存储少量的不太敏感的数据.
4. 在不登录的情况下, 完成服务器对浏览器的身份识别.





###### 完 !