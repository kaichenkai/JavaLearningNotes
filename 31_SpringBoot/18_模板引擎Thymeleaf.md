## 模板引擎Thymeleaf

### 引入thymeleaf

```maven
<!-- https://mvnrepository.com/artifact/org.springframework.boot/spring-boot-starter-thymeleaf -->
    <dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-thymeleaf</artifactId>
    <version>2.3.0.RELEASE</version>
</dependency>
```



### 使用thymeleaf

ThymeleafProperties.class 源码

```java
@ConfigurationProperties(prefix = "spring.thymeleaf")
public class ThymeleafProperties {
    private static final Charset DEFAULT_ENCODING;
    public static final String DEFAULT_PREFIX = "classpath:/templates/";
    public static final String DEFAULT_SUFFIX = ".html";
    private boolean checkTemplate = true;
    private boolean checkTemplateLocation = true;
    //默认在类路径下的 templates 目录下查找模板
    private String prefix = "classpath:/templates/";
    private String suffix = ".html";
    private String mode = "HTML";
```

1. 模板放置路径

   `classpath:/templates/`

2. 导入 thymeleaf 的命名空间

   ```xml
   <html lang="en" xmlns:th="http://www.thymeleaf.org">
   ```

3. 使用 thymeleaf 语法, 编写模板页面

   ```xml
   <!DOCTYPE html>
   <html lang="en" xmlns:th="http://www.thymeleaf.org">
   <head>
       <meta charset="UTF-8">
       <title>Title</title>
   </head>
   <body>
       <h3>thymeleaf 模板测试</h3>
       <div th:text="${test}"></div>
   </body>
   </html>
   ```

4. 编写控制层

   ```java
   package com.atguigu.restfulcurd.demo.controller;
   
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   import org.springframework.stereotype.Controller;
   import org.springframework.web.bind.annotation.*;
   import java.util.HashMap;
   import java.util.Map;
   
   //@RestController
   @Controller
   @RequestMapping("/main")
   public class HelloController {
       Logger logger = LoggerFactory.getLogger(HelloController.class);
   
       @GetMapping("thymeleaf")
       public String thymeleaf(Map<String, Object> map){
           map.put("test", "test data ...");
           return "/thymeleafTest.html";
       }
   }
   
   ```

   坑: 不能使用 RestController 注解, 否则无法渲染模板



thymeleaf 更多语法可以去网上查找







###### 完