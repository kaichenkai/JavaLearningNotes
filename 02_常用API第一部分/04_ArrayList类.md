## ArrayList 类

`ArrayList`集合的长度是可以随意变化的

对于`ArrayList`来说，有一个尖括号<E>代表泛型

泛型：就是装在集合中的元素的类型(统一)

注意事项：

- 泛型只能是引用类型，**不能是基本类型**
- 对于`ArrayList`集合来说，直接打印得到的不是地址值，而是存储的内容，如果内容为空，那么打印 `[]`

```java
import java.util.ArrayList;

public class DemoArrayList {
    public static void main(String[] args) {
        // 创建一个ArrayList
        ArrayList<String> arrayList = new ArrayList<>();

        arrayList.add("甲");
        // arrayList.add(10);   // 泛型已经指明是String类型，况且只能是引用类型
        System.out.println(arrayList);  // [甲]
    }
}
```



常用方法:

`public boolean add(E e)`：向集合中添加元素，元素的类型应与泛型一致，返回值是boolean类型

`public E get(int index)`：根据索引值从集合中获取元素，返回元素类型与泛型一致

`public E remove(int index)`：根据索引值从集合中删除元素，返回元素类型与泛型一致

`public int size()`：获取集合中元素的长度，返回int类型

```java
import java.util.ArrayList;

public class ArrayListMethod {
    public static void main(String[] args) {
        ArrayList<String> arrayList = new ArrayList();

        // 添加
        boolean bool = arrayList.add("甲");
        System.out.println(bool);  // true

        // 获取
        String str = arrayList.get(0);
        System.out.println(str);  // 甲

        // 获取大小
        int count = arrayList.size();
        System.out.println(count);  // 1

        // 删除
        String delete = arrayList.remove(0);
        System.out.println(delete);  // 甲
    }
}
```



如果需要往集合中存储基本数据类型，那么就必须使用基本数据类型对应的包装类

包装类与String类一样，都在java.long包下，所以可以直接使用

`Byte --> byte`

`Short --> short`

`Integer --> int`    // 特殊

`Long --> long`

`Float --> float`

`Double --> double`

`Character --> char `   // 特殊

`Boolean --> boolean`

从JDK 1.5开始，支持自动装箱，自动拆箱：基本类型  <----> 包装类型

```java
import java.util.ArrayList;

public class WrapperClass {
    public static void main(String[] args) {
        // 指定集合中的泛型是Integer
        ArrayList<Integer> arrayList = new ArrayList<>();

        arrayList.add(100);
        int num = arrayList.get(0);
        System.out.println(num);  // 100
    }
}
```



包装类成员方法: 

- valueOf() 装箱
- intValue() 拆箱

```java
public class Main {
    public static void main(String[] args) {
        // 装箱
        // Integer ig = new Integer("123456");
        Integer ig = Integer.valueOf("123456");
        // 拆箱
        int i = ig.intValue();
        System.out.println(i);   // 123456

        // 自动装箱, 拆箱
        Integer ig2 = 123456;
        int i2 = ig2;
    }
}
```



做一个小题目:

```java
// 定义以指定格式打印集合的方法，格式参照：{元素@元素@元素@元素}
import java.util.ArrayList;

public class ArrayListPrint {
    public static void main(String[] args) {
        ArrayList<String> arrayList = new ArrayList<>();

        arrayList.add("2019");
        arrayList.add("-02");
        arrayList.add("-14");
        System.out.println(arrayList);  // [2019, -02, -14]

        arrayListPrint(arrayList);
    }

    public static void arrayListPrint(ArrayList<String> arrayList){
        System.out.print("{");
        for (int i = 0; i < arrayList.size(); i++){
            String str = arrayList.get(i);
            System.out.print(str);
            if (i != arrayList.size() - 1){
                System.out.print("@");
            }
        }
        System.out.print("}"); // {2019@-02@-14}
    }
}
```



###### 完 !

