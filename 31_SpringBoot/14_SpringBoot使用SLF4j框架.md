## SpringBoot使用SLF4j框架

### 底层依赖关系

idea 里边点击鼠标右键, 选择 Diagrams --> 查看

![1591889620108](assets/1591889620108.png)

![1591889332171](assets/1591889332171.png)

```xml
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-core</artifactId>
    <exclusions>
        <exclusion>
            <groupId>commons-logging</groupId>
            <artifactId>commons-logging</artifactId>
        </exclusion>
    </exclusions>
</dependency>
```

总结: 

+ SpringBoot 底层是 slf4j + logback 的方式进行日志记录
+ 排除了 commons-logging 日志框架 (Spring 默认日志框架)
+ SpringBoot也把其它的日志都替换成了 slf4j (导入了中间替换包, 覆盖包)



### 其他问题

1. 如果我们要引入其他框架, 一定要把这个框架的默认日志依赖移除掉; 

```xml
<exclusions>
    <exclusion>
        <groupId>commons-logging</groupId>
        <artifactId>commons-logging</artifactId>
    </exclusion>
</exclusions>
```





###### 完