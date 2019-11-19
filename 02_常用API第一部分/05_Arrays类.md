## Arrays 工具类

`java.util.Arrays `: 是一个与数组相关的工具类, 里面提供了大量静态方法, 用来实现常见的数组操作

`public static String toString(参数数组)`: 将参数数组转换为字符串返回 (按照默认格式: [element1, element2, element3 ...] )

`public static void sort(参数数组)`: 将当前数组进行排序, 默认升序.

```java
import java.util.Arrays;

public class DemoArrays {
    public static void main(String[] args) {
        int[] arrayNum = {5, 1, 6, 3, 9};
        String[] arrayString = {"bbb", "ccc", "aaa"};

        // toString()
        System.out.println(Arrays.toString(arrayNum));  // [5, 1, 6, 3, 9]

        // sort()
        Arrays.sort(arrayNum);
        System.out.println(Arrays.toString(arrayNum));  // [1, 3, 5, 6, 9]
        Arrays.sort(arrayString);
        System.out.println(Arrays.toString(arrayString));  // [aaa, bbb, ccc]
    }
}
```





###### 完 !

