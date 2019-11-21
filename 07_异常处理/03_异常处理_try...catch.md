## 异常处理

> try {
>
> ​	尝试执行的代码
>
> } catch (Exception e) {
>
> ​	处理异常的代码
>
> }  finally {
>
> ​	最后一定会执行的代码
>
> }



```java
public class Main {
    public static void main(String[] args) {
        try {
            int i = 1 / 0;
        } catch (Exception e) {
            System.out.println("系统出错了, 请联系管理员");
        } finally {
            System.out.println("一定会执行的部分");
        }
    }
}
```



