## webjars & 静态资源映射

### WebMvcAutoConfiguration.java 源码

```java
public void addResourceHandlers(ResourceHandlerRegistry registry) {
    if (!this.resourceProperties.isAddMappings()) {
        logger.debug("Default resource handling disabled");
    } else {
        Duration cachePeriod = this.resourceProperties.getCache().getPeriod();
        CacheControl cacheControl = this.resourceProperties.getCache().getCachecontrol().toHttpCacheControl();
        if (!registry.hasMappingForPattern("/webjars/**")) {
            this.customizeResourceHandlerRegistration(registry.addResourceHandler(new String[]{"/webjars/**"}).addResourceLocations(new String[]{"classpath:/META-INF/resources/webjars/"}).setCachePeriod(this.getSeconds(cachePeriod)).setCacheControl(cacheControl));
        }

        String staticPathPattern = this.mvcProperties.getStaticPathPattern();
        if (!registry.hasMappingForPattern(staticPathPattern)) {
            this.customizeResourceHandlerRegistration(registry.addResourceHandler(new String[]{staticPathPattern}).addResourceLocations(WebMvcAutoConfiguration.getResourceLocations(this.resourceProperties.getStaticLocations())).setCachePeriod(this.getSeconds(cachePeriod)).setCacheControl(cacheControl));
        }

    }
}
```



### 公共的静态资源

1. 如果我们需要用到 bootstrap.js jquery.js 等公共的静态资源, 可以通过 webjars 的方式导入

   所有的 /webjars/**   都会从 classpath:/META-INF/resources/webjars/  路径下寻找资源

   webjars : 是指通过 jar 包的方式引入静态资源, 比如前端需要用到 jquery, 那么可以通过导入 jquery 的 jar包来导入 ([maven仓库](<https://mvnrepository.com/search> ))

```maven
<!-- https://mvnrepository.com/artifact/org.webjars.bower/jquery -->
<dependency>
    <groupId>org.webjars.bower</groupId>
    <artifactId>jquery</artifactId>
    <version>3.3.1</version>
</dependency>
```



### 私有的静态资源

1. 当我们想导入自己写的静态资源(html, css, js, img) , 那么静态资源该放在哪个目录呢 ?

   ```
   "classpath://META-INF/resources"
   "classpath:resources"
   "classpath:static"
   "classpath:public"
   "/": 当前项目的根路径
   ```

   classpath: maven工程的 resources目录下

2. 我们也可以自己指定静态资源的文件夹, 多个目录以 , (逗号) 分隔

   比如在全局配置文件中指定类路径下的 dist 文件夹 (一般前端项目打包会生成dist文件夹); **指定静态资源目录之后, 那么默认的静态资源路径则不再有效**

   ```yml
   spring:
     resources:
       static-locations: classpath:/dist/,classpath:/test
   ```

"/**" 访问当前项目classpath下的任何资源

当我们访问静态资源时, SpringBoot 会自动从以上几个目录下寻找, 没找到返回 404 

**注意: 新增加的静态资源需要重启项目才能访问到**\



### 欢迎页

1. 当我们在浏览器中访问根路径时, 我们想默认返回一个静态资源, 这个资源的文件名是 index.html, 也是被 "/**" 映射, 所以在 classpath 目录下放入我们写好 index.html 首页静态文件就好.



### 站点图标

1. 当我们想设置站点图标, 也是可以直接把 favicon.ico 文件直接放在 classpath 路径下.







###### 完 





