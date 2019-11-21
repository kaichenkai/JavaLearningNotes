## 异常处理

throws 表示方法**准备**要扔出来一个异常

产生的错误尽可能的自己处理, 少向外边抛出异常



throw 表示主动抛出异常(类似于 python 中的  raise)



```java
public class Main {
    public static void division (int a, int b) throws Exception {
        if (b==0) {
            // 主动抛出异常
            throw new Exception("除数是 0");  // 匿名对象的写法
        } else {
            System.out.println(a / b);
        }
    }

    public static void main(String[] args) throws Exception {
        division(2, 3);
    }
}
```

