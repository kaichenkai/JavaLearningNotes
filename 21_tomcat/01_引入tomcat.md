## tomcat

web 服务器软件

1. 服务器: 安装了服务器软件的计算机.

2. 服务器软件: 接收用户的请求, 处理请求, 做出响应.

3. web 服务器软件: 接收用户的请求, 处理请求, 做出响应.

   **在web服务器软件中, 可以部署 web 项目, 让用户通过浏览器来访问这些项目. ( web容器 )**

显然, tomcat 是一款web服务器软件



常见的java相关的web服务器软件: 

1. webLogic: oracle 公司, 大型 JavaEE 服务器, 支持所有的 JavaEE 规范, 收费.
2. webSphere: IBM 公司, 大型 JavaEE 服务器, 支持所有的 JavaEE 规范, 收费.
3. JBOSS: JBOSS公司, 大型 JavaEE 服务器, 支持所有的 JavaEE 规范, 收费.
4. Tomcat: Apache基金组织, 中小型的 JavaEE 服务器, 仅仅支持少量的 JavaEE 规范, servlet / jsp, 开源的, 免费的.

remark: JavaEE: Java语言在企业级开发中使用的技术规范的总和, 一共规定了13项大的规范.



tomcat 下载, 安装, 运行

**下载** ( 根据系统版本选择 ):

+ http://tomcat.apache.org

**安装:** 

+ 解压压缩包即可

**启动:** 

+ bin/startup.bat  ( windows 双击运行)
+ 修改配置文件: conf/server.xml
+ 启动报错问题排查:
  + 黑窗口一闪而过: 没有正确配置 JAVA_HOME 环境变量

**访问:** 

http://IP:8080



**关闭:**

1. 正常关闭: 
   + bin/shutdown.bat
   + ctrl + c
2. 强制关闭: 
   + 点击启动窗口的 'x'



##### 部署项目的方式: 

1. 开发者 ( 直接将项目放到 webapps 目录下即可 )

   + /hello: 项目的访问路径 --> 虚拟目录
   + 简化部署: 将项目打包成一个 war 包, 再将 war 包放置到 webapps 目录下

2. 配置 conf/server.xml 文件  ( **不推荐使用** )

   + 在 <Host> 标签体中配置

     <Context docBase="D:\hello" path="/hehe" />

     docBase: 项目存放的路径  ( 一定得先创建这个路径, 不然 tomcat 启动不了 )

     path: 虚拟目录

3. 项目热部署

    在 conf\Catalina\localhost 创建任意名称的 xml 文件, 在文件中编写:

   <Context docBase="D:\hello" />

   docBase: 项目存放的路径

   path 虚拟目录: 是文件名





###### 完 !

