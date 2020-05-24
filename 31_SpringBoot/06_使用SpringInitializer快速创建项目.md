## 使用SpringInitializer快速创建项目

IDE 都支持使用 Spring 的项目创建向导快速创建一个 Spring Boot 的项目;

选择我们需要的模块, 向导会联网创建 Spring Boot 项目;

默认生成 Spring Boot 项目:

1. 主程序已经生成好了, 我们只需要写我们自己的逻辑
2. resources 文件夹中目录结构
   + static: 保存所有的静态资源: js, css, images
   + templates: 保存所有的模板页面: 
     + Spring Boot 默认jar包使用嵌入式的 Tomcat, 默认不支持 JSP 页面, 也可以使用模板引擎 (freemarker, thymeleaf)
     + application.properties: Spring Boot应用的配置文件, 可以修改一些默认配置(例如修改端口号: server.port=8081)





