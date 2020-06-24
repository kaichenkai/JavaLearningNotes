## Arrays 工具类

`java.util.Arrays `: 是一个与数组相关的工具类, 里面提供了大量静态方法, 用来实现常见的数组操作

`public static String toString(参数数组)`: 将参数数组转换为字符串返回 (按照默认格式: [element1, element2, element3 ...] )

`public static void sort(参数数组)`: 将当前数组进行排序, 默认升序.

```java
import java.util.Arrays;

public class DemoArrays {
    public static void main(String[] args) {
        int[] arrayNum = {5, 1, 6, 3, 9, 3};
        int[] arrayNum2 = {5, 1, 6, 3, 9, 3};
        int[] arrayNum3 = {5, 1, 6, 3, 9, 3};
        String[] arrayString = {"bbb", "ccc", "aaa"};

        // toString()
        System.out.println(Arrays.toString(arrayNum));  // [5, 1, 6, 3, 9]

        // sort()
        Arrays.sort(arrayNum);
        System.out.println(Arrays.toString(arrayNum));  // [1, 3, 5, 6, 9]
        Arrays.sort(arrayString);
        System.out.println(Arrays.toString(arrayString));  // [aaa, bbb, ccc]

        //查询元素出现的位置（如果数组中有多个相同的元素，查找结果是不确定的）
        System.out.println(Arrays.binarySearch(arrayNum, 3));//返回元素所在的索引值
        System.out.println(Arrays.binarySearch(arrayNum, 999));//没有找到返回负的整数

        // 判断两个数组是否相同
        System.out.println(Arrays.equals(arrayNum, arrayNum2));//false
        System.out.println(Arrays.equals(arrayNum2, arrayNum3));//true
    }
}
```





###### 完 !

