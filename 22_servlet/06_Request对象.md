## Request 对象

##### 原理

1. request 对象和 response 对象是由服务器创建的, 用来封装请求消息与响应消息.
2. request 对象是来获取请求消息, response 对象是来设置响应消息.



##### Request 继承体系结构

> ServletRequest (接口) <-- HttpServletRequest (接口) <-- org.apache.catalina.connector.RequestFacade ( 类, 由 tomcat 实现)



##### Request 获取请求消息

1. 获取请求行消息:

   + 获取 get 请求参数 (url 后边的查询字符串 ) :  `String getQueryStrng()` 
   + 获取虚拟目录: `String getContextPath()`
   + 获取请求URI:
     + `String getRequestURI()`:  /resouce/1
     + `StringBuffer getRequestURL()`:  http://localhost:8080/resouce/1

   ```java
   @WebServlet("/demo3")
   public class Servlet_04_HttpServlet拿请求头消息 extends HttpServlet {
       @Override
       protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
           System.out.println(req.getContextPath());  // 获取虚拟目录
           System.out.println(req.getRequestURI());  // /demo3
           System.out.println(req.getRequestURL());  // http://localhost:8080/demo3
       }
   }
   ```

   

2. 获取请求头数据:

   + 通过请求头的名称获取值: `String getHeader(String name)`

     请求头名称不区分大小写

   ```java
   @WebServlet("/demo4")
   public class Servlet_04_HttpServlet拿请求头消息 extends HttpServlet {
       @Override
       protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
           // User-Agent
           String userAgent = req.getHeader("User-Agent");
           System.out.println(userAgent);  // Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/71.0.3578.98 Safari/537.36
           // Referer
           String referer = req.getHeader("Referer");
           System.out.println(referer);  // null
       }
   }
   ```

   

3. 获取请求体数据:

   只有 POST 方法才有请求体

   步骤:  获取流对象, 再从流对象中拿数据

   + 字符流: `BufferedReader br = req.getReader()`

     ```java
     @WebServlet("/demo5")
     public class Servlet_05_HttpServlet拿请求体参数 extends HttpServlet {
         protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
             // 读取字符流
             BufferedReader br = request.getReader();
             // 读取一行
             System.out.println(br.readLine());
             // 读取所有
             String line;
             while ((line = br.readLine()) != null) {
                 System.out.println(line);  // username=johny&passwd=123123
             }
         }
     }
     ```

     

   + 字节流:  

   

4. 获取请求参数通用方式:

   根据参数名称获取参数值: `String getParameter(String name)`

   根据参数名称获取参数值的数组: `String[] getParameterValues(String name)`

   获取所有参数的 map 集合: `Map<String, String[]> getParameterMap()`

   ```java
   @WebServlet("/demo6")
   public class Servlet_06_HttpServlet拿请求参数通用方式 extends HttpServlet {
       protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
           // 1. 根据参数名称获取参数值
           System.out.println(request.getParameter("username"));  //
           // 2. 根据参数名称获取参数值的数组
           System.out.println(Arrays.toString(request.getParameterValues("hobby")));  //
           // 3. 获取所有参数的map集合
           Map<String, String[]> map = request.getParameterMap();
           for (String key : map.keySet()) {
               System.out.println("key: " + key);
               String[] values = map.get(key);
               for (String value : values) {
                   System.out.println("value: " + value);
               }
               System.out.println(" --- ");
           }
       }
   
       protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
   
       }
   }
   
   // 运行结果
   johny
   [game, study]
   key: username
   value: johny
    --- 
   key: passwd
   value: 123123
    --- 
   key: hobby
   value: game
   value: study
    --- 
   ```

   

5. post 中文乱码问题

   原因: post 中是通过字符流获取的参数

   解决: 设置流的编码

   `request.setCharacterEncoding("utf-8");`





###### 完 !

