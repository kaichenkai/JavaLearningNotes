## SLE4j 使用原理

### 如何在系统中使用 SLF4j + logback

1. 开发的时候, 日志记录方法的调用, 不应该来直接调用日志的实现类, 而是调用日志抽象层里面的方法;
2. 在系统里导入 SLF4j.jar(抽象层) 和 logback.jar(实现类)

```java
package com.company.controller;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;


@RestController
public class HelloController {
    static Logger logger = LoggerFactory.getLogger(HelloController.class);

    @RequestMapping("/hello")
    public String hello(){
        logger.info("hello world");
        return String.format("Hello World, %s", name);
    }
}
```



**每一个日志的实现框架都有自己的配置文件, 使用 SLF4j 之后, 配置文件还是做成日志实现类的配置**



### 遗留问题

1. 在开发 SpringBoot (SLF4j+logback)的项目时, 依赖 Spring (commons-logging) hibernate (jboss-logging), Mybatis 等框架, 怎么统一日志记录呢 ? (即使集成了别的框架, 也和 SpringBoot 使用同一个日志框架)
2. 如何让系统中所有的日志抽象层
   1. 将系统中其它日志框架先排除出去;
   2. 用中间包来替换原有的日志框架;
   3. 最后导入 SLF4j 的实现类, 例如 logback.



###### 完