## profile多环境配置文件支持

### 概述

1. profile 是 Spring 对不同环境提供不同配置功能的支持, 可以通过激活, 指定参数, 命令行参数等方式快速切换环境

   

2. 使用形式:

   + 多 profile 文件形式 (**推荐使用**):

     1. 主配置文件名可以是 application-{profile}.properties/yml

        application-dev.properties,    application-prod.properties

     2. 默认使用 application.properties 的配置

   + yml 支持多文档快模式:

     ```yml
     server:
       port: 8081
     spring:
       profiles:
         active: prod
     
     ---
     
     server:
       port: 8082
     spring:
       profiles:
         active: dev
     
     ---
     
     server:
       port: 8083
     spring:
       profiles:
         active: test
     ```

   

3. 激活指定 profile

   + 命令行 

     在打包完成之后, 在命令行运行时传入profile参数

     `--spring.profiles.active=dev`

   + 配置文件

     在 application.properties/yml 主配置文件中指定当前环境的另一个配置文件

     `spring.profiles.active=dev`

   + jvm参数

     -D是固定写法

     `-Dspring.profiles.active=dev`



###### 完 