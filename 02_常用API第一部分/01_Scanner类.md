## Scanner 类

Scanner类可以实现键盘输入数据, 到程序中.

Scanner类是引用数据类型.

导入Scanner( 为什么String类不需要导入？因为：只有 `java.lang` 包下的内容不需要导包，其它的包都需要手动导入 )

```java
import java.util.Scanner;

public class DemoScanner {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        int num = scanner.nextInt();
        String string = scanner.next();
        System.out.println(num);
        System.out.println(string);
    }
}
```



###### 完 !

