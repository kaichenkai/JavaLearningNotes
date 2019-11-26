## jsp 指令

##### 作用 

用于配置 jsp 页面, 导入资源文件



##### 格式

`<%@ 指令名称 属性名1=属性值1  属性名2=属性值2  ...%>`

例如 jsp 文件的第一行: 

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
```



##### 分类

1. page: 配置 jsp 页面的属性, 如上边所示.

   + `contentType`: 等同于 response.setContentType(), 设置响应体的 mime 类型和字符集

   + `import`: 导包  (在 jsp 页面写 java 代码, 导 jar 包一样, 感觉有点乱....)

     ```java
     <%@ page import="java.util.List" %>
     <%@ page import="java.util.ArrayList" %>
     <%@ page contentType="text/html;charset=UTF-8" language="java" %>
     <html>
       <head>
         <title>$Title$</title>
       </head>
       <body>
           <% List<String> list = new ArrayList(); %>
       </body>
     </html>
     ```

   + `errorPage`: 当前页面发生异常 (内部错误) 后, 会自动跳转到 errorPage="error.jsp" 的页面 ( 提升用户体验 )

   + `isErrorPage`: 标识当前 jsp 页面是否是错误页面

     false: 默认不是, 不能使用 exception 内置对象

     true: 是, 可以使用 exception 对象, 将错误信息输出到日志中. 

   

2. include: 导入其它页面的资源, 

   > 像是模板的继承, 和 python flask 里边的模板继承是一样的道理
   >
   > 比如一个新闻的网站, 好多地方的显示内容都是一样的, 没必要在每个 jsp 里边都写一遍
   >
   > 把那些共同的地方抽取出来, 生成通用的模板 jsp, 其它的页面包含即可
   >
   > 同样的代码就应该抽取出来, 可维护性更高.

   

3. taglib: 导入 jsp 其它的标签库

   > jsp 第三方库里边, 还包含有 html 没有的标签, 花里花哨的, 了解一下即可.





###### 完 !