## Iterator 接口

`java.util.Iterator`

获取迭代器对象: 调用集合实现类的 iterator() 方法

Java访问集合**总是通过统一的方式**——迭代器（Iterator）来实现，它最明显的好处在于无需知道集合内部元素是按什么方式存储的。 



常用成员方法:

1. `boolean hasNext()`: 判读是否有元素可以迭代
2. `E next()`: 返回迭代的下一个元素



```java
import java.util.ArrayList;
import java.util.Collection;
import java.util.Iterator;

public class Main {
    public static void main(String[] args) {
        Collection<String> coll = new  ArrayList<>();
        coll.add("johny");
        coll.add("anson");

        // 获取迭代器对象, 接口Iterator也是有泛型的
        Iterator<String> it = coll.iterator();
        while (it.hasNext()) {
            String s = it.next();
            System.out.println(s);
        }
    }
}
```



###### 完 !