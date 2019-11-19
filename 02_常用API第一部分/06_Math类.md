## Math 类

`java.util.Math` 类是数学相关的工具类, 里面提供了大量的静态方法, 完成数学运算相关的操作

1. `public static double abs(double num)`：获取绝对值
2. `public static double ceil(double num)`：向上取整
3. `public static double floor(doubel num)`：向下取整
4. `public static long round(double num)`：四舍五入



```java
public class DemoMath {
    public static void main(String[] args) {
        double num = -12.24;

        // 绝对值
        System.out.println(Math.abs(num));  // 12.24  double

        // 向上取整
        System.out.println(Math.ceil(num));  // 12.0  double

        // 向下取整
        System.out.println(Math.floor(num));  // 13.0  double

        // 四舍五入
        System.out.println(Math.round(num));  // 12  long
    }  
}
```



###### 完 !

