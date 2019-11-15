## System类

`java.lang.System`

提供了很多的静态方法, 使用类名直接调用

1. 返回当前时间的unix时间戳 (可用于统计程序运行耗时)

2. arraycopy

   ```java
   public static native void arraycopy(Object src,  int  srcPos, Object dest, int destPos,
                                       int length);
   ```

   



```java
// 统计程序运行耗时
public class Main {
    public static void main(String[] args) throws InterruptedException {
        long startTime = System.currentTimeMillis();
        Thread.sleep(1000);
        long endTime = System.currentTimeMillis();
        System.out.println(endTime - startTime);  // 1001
    }
}
```



```java
// arraycopy
import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        int[] src = {1,2,3,4};
        int[] dest = {5,6,7,8};

        System.arraycopy(src, 0, dest,0, 3);  //  替换3个, 元素少于3个报错
        System.out.println(Arrays.toString(dest)); // [1, 2, 3, 8]
    }
}
```





