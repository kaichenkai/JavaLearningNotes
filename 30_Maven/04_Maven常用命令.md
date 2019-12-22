## Maven 常用命令

### mvn clean

清除编译文件, 项目中 target 目录会被删除 (target 目录是编译后的文件存放目录)



### mvn compile (编译核心代码)

编译 src/main/java 目录下的文件



### mvn test (编译测试代码)

编译 src/test/java 目录下的文件 (它会将 src/main/java 目录下的代码也进行编译, 相当于说执行 mvn test 的时候, 也会执行 mvn compile)



### mvn package (打包)

打包代码 (它会将 src/main/java 和 src/test/java 目录下的代码都进行编译)

打包文件的类型可以在项目中 pom.xml 中进行配置

```xml
<packaging>war</packaging>
```



### mvn install 

他会执行 mvn compile, mvn test, mvn package 的操作, 最后将打包代码放入本地仓库





###### 完 ~



