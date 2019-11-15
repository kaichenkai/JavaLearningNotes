## Date 类

`import java.util.Date;`



时间原点: 1970-01-01  00:00:00(英国格林威治)  

中国属于东八区, 会把时间增加 8 个小时: 1970-01-01  08:00:00

unix 时间戳是指离时间原点的毫秒值



获取当前日期时间的unix时间戳:

把毫秒值转换为 Date 日期



```java
// 获取当前unix时间戳
import java.util.Date;

public class Main {
    public static void main(String[] args){
        Date d = new Date();
        long i = d.getTime();
        System.out.println(i);  // 1571926743797
    }
}
```



```java
// 把时间戳转换为日期时间
import java.util.Date;

public class Main {
    public static void main(String[] args){
        Date d = new Date(1571926743797L);
        System.out.println(d); // Thu Oct 24 22:19:03 CST 2019
    }
}
```

