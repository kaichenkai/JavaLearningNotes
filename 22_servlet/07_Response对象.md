## Response 对象

Response 对象是来设置响应消息



##### 设置响应体消息

1. 设置响应状态码

   `setStatus(int sc)`

2. 设置响应头

   `setHeader(String name, String value)`

3. 设置响应体

   1. 获取**输出**流
      + 字符输出流: `PrintWriter getWriter()`  

        中文乱码问题:

        1. 获取字符输出流之前需要修改默认编码 (默认是 ISO-8859-1 拉丁编码)  

        2. 然后告诉浏览器使用该编码解码.

           ```java
           // 获取流对象之前, 设置流的编码为 utf-8
           // response.setCharacterEncoding("utf-8");  // 设置流的编码可以省略
           // 告诉浏览器, 使用 utf-8 进行解码
           // response.setHeader("content-type", "text/html; charset=utf-8");
           // 设置编码 (简单方式)
           response.setContentType("text/html; charset=utf-8");
           // 写入字符数据
           response.getWriter().write("登录成功, 欢迎您, " + username);
           ```

        

      + 字节输出流: `ServletOutputStream getOutputStream`  (当做字节输出流来使用)

        ```java
        // 设置编码 (简单方式)
        response.setContentType("text/html; charset=utf-8");
        // 获取字节对象
        ServletOutputStream sos = response.getOutputStream();
        // 使用字节流对象输出内容
        sos.write("hello, world".getBytes());
        ```

        

      + 输出图片:

        ```java
        ImageIO.write(imageObj, "jpg", response.getOutputStream());
        ```

        

   2. 使用输出流, 将数据输出到客户端浏览器

      



##### 重定向 ( redirect )

`response.sendRedirect("/source/path");`





###### 完 !