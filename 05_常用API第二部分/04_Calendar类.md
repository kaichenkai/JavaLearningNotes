## Calenda 类

Calendar 是抽象类

常用成员方法:

1. 返回当前的日期时间的Date对象: 

   `public Date getTime()`

2. 将给定的日期时间字段设置为给定值:

   `public void set(int field, int value)`

3. 根据日历的规则, 为给定的日历字段添加或者减去指定的时间量(例如获取前N天的时间, 前N秒的日期时间, 非常方便) (正数为加, 负数为减)

   `public abstract void add(int field, int amount)`

4. 获取日历字段的值

   `public int get(int field)`



```java
import java.util.Calendar;
import java.util.Date;

public class Main {
    public static void main(String[] args) {
        Calendar c = Calendar.getInstance();  // 直接获取对象, 多态写法

        // 获取当前时间
        Date currentTime = c.getTime();

        // 设置年份
        c.set(Calendar.YEAR, 9999);

        // 获取年份
        int year = c.get(Calendar.YEAR);
        System.out.println(year);  // 9999

        // 更改月份
        c.add(Calendar.MONTH, 2);
        // 查看更改的月份
        System.out.println(c.get(Calendar.MONTH));  // 西方月份是 0-11, 中国是 1-12
    }
}
```

