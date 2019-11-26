## JSP

jsp: Java服务器端页面 ( Java Server Pages )

可以理解为: 一个特殊的页面, 其中既可以定义 html 页面, 又可以定义 java 代码.

> 前后端不分离的一种响应方式,
>
> 因为后端要返回 html 页面, 同时想在 html 中插入后端的响应内容,
>
> 在 jsp 页面中既能渲染 html 页面, 又可以展示后端逻辑处理的结果.



##### jsp 原理

jsp本质上就是一个 Servlet, 怎么说 ?

当用户请求 http://localhost/8080/index.jsp 的时候: 

1. 服务端解析请求信息, 寻找 index.jsp 文件,
2. 找到 jsp 文件之后, 会将 index.jsp 转换为 .java 文件,
3. 服务端编译 .java 文件, 生成 .class 字节码文件,
4. 然后由 .class 文件创建 Servlet 给客户端返回响应.

所以说, jsp 是一个 Servlet.



##### jsp 脚本

jsp 定义 java 代码的方式:

1. <% 代码块 %>: 定义的 java 代码, 在 service 方法中, service 方法中可以定义什么, 该代码块就可以定义什么.
2. <%= 代码块 %>: 加 = 表示定义输出内容, 例如: <%= "hello world" ( 可以放变量 ) %>
3. <%! 代码块 %>: 加 ! 表示定义 java 类的成员变量或成员方法. ( 一般不建议, 会引发线程安全问题 )



##### jsp 注释

`<!--  html标签内容  -->`:  注释 html 标签

`<%--   ava代码块  --%>`:  注释 java 代码



##### jsp 内置对象

jsp 语法部分, 理解为在 jsp 页面中不需要获取和创建, 可以直接使用的对象.

jsp 一共有 9 个内置对象, 下边介绍最简单的 3 个: 

1. request

2. response

3. out: 字符输出流对象, 可以输出字符到页面上, 和 response.getWriter() 类似

   ~~out 对象是 jsp 产生的, 而 response.getWriter() 是由首次处理浏览器请求的 Servlet 产生.~~

   建议统一使用 **out 对象**输出字符到页面上.





###### 完 !