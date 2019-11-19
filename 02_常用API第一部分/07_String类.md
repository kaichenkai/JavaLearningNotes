## String 类

##### 程序中所有的双引号字符串, 都是 String 类的对象

字符串的特点: 

1. 字符串的内容永不可变 ( final 修饰 )
2. 字符串效果上相当于 char[] 数组, 但是底层原理是 byte[] 字节数组.



[廖雪峰谈字符串与编码](https://www.liaoxuefeng.com/wiki/1252599548343744/1260469698963456)

> 较新的JDK版本的`String`则以`byte[]`存储：如果`String`仅包含ASCII字符, 则每个`byte`存储一个字符, 否则, 每两个`byte`存储一个字符, 这样做的目的是为了节省内存, 因为大量的长度较短的`String`通常仅包含ASCII字符:
>
> ```java
> public final class String {
>     private final byte[] value;
>     private final byte coder; // 0 = LATIN1, 1 = UTF16
> ```
>
> 对于使用者来说, `String`内部的优化不影响任何已有代码, 因为它的`public`方法签名是不变的。 



字符串的常见 3+1 种创建方式:

```java
public class DemoString {
    public static void main(String[] args) {
        // 最简单的方式创建一个字符串
        String str = "johny";

        // 使用空参构建
        String str1 = new String();
        System.out.println(str1);  // ""
        
        // 根据字符数组的内容, 来创建对应的字符串
        char[] charArray = {'A', 'B', 'C'};
        String str2 = new String(charArray);
        System.out.println(str2);  // "ABC"

        // 根据字节数组的内容, 来创建对应的字符串
        byte[] byteArray = {97, 98, 99};
        String str3 = new String(byteArray);
        System.out.println(str3);  // "abc"
    }
}
```



字符串常量池:

![1574060066268](07_String类.assets\1574060066268.png)



字符串的比较:

== 运算符是进行对象的地址值比较, 如果需要比较字符串的内容, 那么可以使用 equals() 方法.

注意事项: 

1. `equals()`具有对称性, 也就是 a.equals(b) 和 b.equals(a) 是一样的.
2. 如果比较双方中一个常量和一个变量, 推荐把常量写在前面：`"abc".equals(a)`, 因为前面的字符串不能是null, 否则会出现`NullPointerException`
3. `equalsIgnoreCase()`在比较时忽略大小写.

```java
public class StringEquals {
    public static void main(String[] args) {
        String strA = "abc";
        String strB = "abc";

        char[] arrayChar = {'a', 'b', 'c'};
        String strC = new String(arrayChar);

        System.out.println(strA.equals(strB));  // true
        System.out.println(strA.equals(strC));  // true

        // 推荐写法
        System.out.println("abc".equals(strA));  // true

        // 空指针异常
        String strD = null;
        // System.out.println(strD.equals(strA));  // NullPointerException

        // equalsIgnoreCase()
        System.out.println("ABC".equalsIgnoreCase(strA));  // true
    }
}
```



字符串常用方法: 

`int length()`：获取字符串当中含有的字符个数, 就是字符串长度

`String concat(String str)`：将当前字符串和参数字符串进行拼接

`char charAt(int index)`：获取指定索引值位置的字符

`int indexOf(String/char args)`：查找参数字符串/字符在当前字符串中的第一次索引位置, 如果没有找到就返回 -1

```java
public class StringGet {
    public static void main(String[] args) {
        String strA = "abc";

        char[] arrayChar = {'A', 'B', 'C'};
        String strB = "ABC";

        // 返回字符串长度
        System.out.println(strA.length());  // 3

        // 字符串拼接
        System.out.println(strA.concat(strB));  // abcABC

        // 返回指定索引值位置上的字符
        System.out.println(strA.charAt(1));  // b

        // 查找参数字符串在当前字符串中的第一次索引位置, 没有找到就返回-1
        System.out.println(strA.indexOf("bc"));  // 1
        System.out.println(strA.indexOf("d"));  // -1
    }
}
```



字符串切片: 

`String substring(int index)`：截取从参数位置一直到字符串末尾, 返回新字符串.

`String substring(int begin, int end)`：截取从begin开始, 到end结束, 顾前不复尾.

```java
public class StringSubstring{
    public static void main(String[] args){
        String strA = "hello, world!";
        
        // 截取
        System.out.println(strA.substring(0, 5));  // hello
    }
}
```



字符串中关于转换的方法:

`char[] toCharArray()`: 将当前字符串拆分成为字符数组作为返回值, 返回字符数组.

`byte[] getBytes(): `获取当前字符串底层的字节数组, 返回的是字节数组的**地址值**(引用).

`String replace(CharSequence oldString, CharSequence newString) `: 将出现的所有老字符串替换成新字符串, 返回替换之后的结果字符串.

```java
public class StringConvert{
    public static void main(String[] args){
        String strA = "中国";

        // 返回字符数组
        System.out.println(strA.toCharArray());  // 中国

        // 返回字节数组(返回的是对象的引用)
        byte[] byteArray1 = strA.getBytes();
        System.out.println(byteArray1);  // [B@1e643faf
        for (int i = 0; i < strA.length(); i++){
            System.out.print(byteArray1[i]);  // -28-72
            if (i == strA.length() - 1){
                System.out.println();
            }
        }

        byte[] byteArray2 = "abc".getBytes();
        System.out.println(byteArray2);  // [B@6e8dacdf
        for (int i = 0; i < "abc".length(); i++){
            System.out.print(byteArray2[i]);  // 979899
            if (i == "abc".length() - 1){
                System.out.println();
            }
        }

        // 字符串替换
        System.out.println(strA.replace("中", "爱"));  // 爱国
    }
}
```



字符串的切割:

`String[] split(String regex)`: 按照参数的规则, 将当前字符串分割为多个部分, 返回字符串数组的地址值(引用)

注意事项：

1. split方法的参数其实是一个正则表达式，如果按照英文句点 `.` 进行切分，必须写 `\\.`

```java
public class StringSplit{
    public static void main(String[] args){
        String strA = "my name is johny";

        String[] strArray = strA.split(" ");  // {"my", "name", "is", "johny"}
        System.out.println(strArray);  // [Ljava.lang.String;@6e8dacdf
       	// 遍历打印
        for (int i = 0; i < strArray.length; i++){
            System.out.print(strArray[i]);  // mynameisjohny
        }
        
        // 特殊写法
        String strB = "a.b.c";
        System.out.println(strB.split("\\."));  // [Ljava.lang.String;@7a79be86
        for (int i = 0; i < strB.split("\\.").length; i++){
            System.out.print(strArray[i]);  // mynameisjohny
        }
        
    }
}
```



###### 完 !

