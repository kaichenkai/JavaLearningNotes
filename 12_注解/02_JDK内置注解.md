## JDK 内置注解

jdk 中预定义的一些注解: 

1. `@Overrride`: 检测被注解标注的方法是否是继承父类(接口)的
2. `@Deprecated`: 该注解标注的内容, 表示已过时
3. `@SuppressWarnings`: 压制警告 @SuppressWarnings("all")



```java
@SuppressWarnings("all")  // 压制警告
interface MyInterface{
    public void test();
}

public class Main implements MyInterface {
    public static void main(String[] args) {
        Main m = new Main();
        m.show1();   // 不推荐使用过时的方法, 但也可以调用
        m.show2();
    }

    @Override
    public void test() {

    }

    @Deprecated
    public void show1(){
        System.out.println("old");
    }

    public void show2(){
        System.out.println("new");
    }
}
```







