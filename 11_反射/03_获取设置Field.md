## 通过反射对象获取设置Field

+ `Field[] getFields()`: 获取所有 public 修饰的成员变量  

+ `Field getField(String name)`

  

+ `Field[] getDeclaredFields()`: 获取所有的成员变量 (不考虑修饰符)

+ `Field getDeclaredField(String name)`



Field 对象操作成员变量: 

1. 获取值:

   `void get(Object obj)`

2. 设置值:

   `void set(Object obj, Object value)`

3. 忽略访问修饰符的安全检查:

   `setAccessible(true)`

   


```java
import java.lang.reflect.Field;

public class Main {
    public static void main(String[] args) throws Exception {
        // .class
        Class pc = Person.class;
        // 获取所有的字段 (忽略修饰符)
        Field[] farray = pc.getDeclaredFields();
        for (Field field:farray) {
            System.out.println(field.getName());  //name hobby
        }

        // 获取指定名称的字段, 并修改值
        Field fh = pc.getDeclaredField("hobby");
        Field fn = pc.getDeclaredField("name");
        Person p = new Person();
        fn.set(p, "johny");
        System.out.println(fn.get(p));  // johny
        // 私有字段需要暴力反射
        fh.setAccessible(true);
        fh.set(p, "我的爱好");
        System.out.println(fh.get(p));  // 我的爱好
        System.out.println(p.toString());  // Person{name='johny', hobby='我的爱好'}
    }
}

class Person {
    public String name;
    private String hobby;

    @Override
    public String toString() {
        return "Person{" +
                "name='" + name + '\'' +
                ", hobby='" + hobby + '\'' +
                '}';
    }
}

运行结果:
name
hobby
johny
我的爱好
Person{name='johny', hobby='我的爱好'}
```

