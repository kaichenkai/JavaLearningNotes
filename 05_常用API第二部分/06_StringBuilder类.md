## StringBuilder 类

`java.lang.StringBuilder`

StringBuilder 是一个字符串缓冲区

在内存中始终是一个byte[]数组, 占用空间少, 操作效率高

StringBuilde  是可变对象，用来高效拼接字符串；

StringBuilder 可以支持链式操作，实现链式操作的关键是返回实例本身；



常用成员方法:

1. append (可添加任意类型数据的字符串形式)
2. delete: 相当于 subString
3. insert: 插入字符或字符串
4. reverse: 反转
5. toString (StringBuilder 和 String  可以互相转换)



```java
//  字符串的高效拼接
public class Main {
    public static void main(String[] args) {
        StringBuilder bu = new StringBuilder();
        // 链式调用
        bu.append("abc")
                .append(123)
                .append(true)
                .append(0.999)
                .append('a');
        System.out.println(bu.toString();
    }
}
```



```java
// StringBuilder 和 String 之间的相互转换
public class Main {
    public static void main(String[] args) {
        StringBuilder bu = new StringBuilder("abc");  // 使用不同的构造方法
        System.out.println(bu.getClass());  // class java.lang.StringBuilder
        //
        String str = bu.toString();
        System.out.println(str.getClass());  // class java.lang.String
    }
}
```

