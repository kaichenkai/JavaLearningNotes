## HelloWorld 探究

### 父项目

Spring Boot 的版本仲裁中心

```xml
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>1.5.9.RELEASE</version>
</parent>

<!--
它的父项目是 spring-boot-dependencies
它来真正管理 Spring Boot 应用里边的所有依赖版本
-->
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-dependencies</artifactId>
    <version>1.5.9.RELEASE</version>
    <relativePath>../../spring-boot-dependencies</relativePath>
</parent>
```

以后我们导入依赖默认是不需要写版本的; (没有在 dependencies 里边管理的依赖自然需要声明版本号)



### 导入的依赖

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

**spring-boot-starter** - **web**

spring-boot-starter: 场景启动器;

starter-web: 帮我们导入了 web 模块正常运行所依赖的组件;

Spring Boot 将所有的功能场景都抽取出来, 做成一个个的 starters (启动器), 只需要在项目里边引入这些 starter, 相关场景的所有依赖都会导入进来. 要用什么功能就导入什么场景的启动器.





