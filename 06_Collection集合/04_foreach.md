## 增强for循环(foreach)

### 定义

Java的集合类都可以使用`for each`循环，`List`、`Set`和`Queue`会迭代每个元素，`Map`会迭代每个key。



简化迭代器的编写(JDK1.5之后特性)

> for  (元素类型  变量名 : 集合/数组) {
>
> ​	System.out.println(变量名)
>
> }



**IDEA 快捷键: iter + Enter**

```java
import java.util.ArrayList;

public class Main {
    public static void main(String[] args) {
        ArrayList<String> arrL = new ArrayList<>();
        arrL.add("johny");
        arrL.add("anson");

        // foreach
        for (String element : arrL){
            System.out.println(element);
        }
    }
}
```





###### 完 !



