## ServletContext 对象

概念: 代表整个 web 应用, 可以和程序的服务器进行通信 ( 全局的上下文管理器? )



获取: 

1. 通过 request 对象获取: `request.getServletContext();`
2. 通过 HttpServlet 对象获取:  `this.getServletContext();`

无论通过哪种方式获取, 返回的是同一个对象.



功能: 

1. 获取 MIME 类型: 

   MIME类型: 在互联网通信过程中定义的一种文件数据类型.

   + 格式: 大类型/小类型, 例如: text/html  image/jpeg

   获取的方法:

   + `String mimeType = context.getMimeType(filename)` 

   

2. 域对象: 共享数据

   ServletContext 域: 所有用户, 所有请求的数据.

   方法: 

   1. `void setAttribute(String name, Object obj)`
   2. `object getAttribute(String name)`: 通过 key 来获取值
   3. `void removeAttribute(String name)`: 通过 key 来删除数据

   

3. 获取文件的真实路径. ( 服务器路径 )

   获取文件的服务器路径方法: `context.getRealPath()`

   1. web 目录下的资源访问: `String realPath = context.getRealPath("/b.txt");`

   2. WEB-INF 目录下: `String realPath = context.getRealPath("/WEB-INF/c.txt");`

   3. src 目录下: `String realPath = context.getRealPath("/WEB-INF/classes/a.txt");`

      



###### 完 !