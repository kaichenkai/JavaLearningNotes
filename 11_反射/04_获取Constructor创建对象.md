## 获取 Constructor 创建对象

+ `Constructor<?>[] getConstructors()`

+ `Constructor<T> getConstructor(Class<?>... parameterTypes)`

  

+ `Constructor<?>[] getDeclaredConstructor()`

+ `Constructor<T> getDeclaredConstructor(Class<?>... parameterTypes)`



```java
import java.lang.reflect.Constructor;

public class Main {
    public static void main(String[] args) throws Exception {
        // .class
        Class pc = Person.class;
        // 获取构造器
        Constructor c = pc.getConstructor(String.class, String.class);
        // 创建对象
        Object person = c.newInstance("johny", "my hobby");
        System.out.println(person);  // Person{name='johny', hobby='my hobby'}

        // 空参构造
        Object person2 = pc.newInstance();
        System.out.println(person2);  // Person{name='null', hobby='null'}
    }
}


class Person {
    public String name;
    private String hobby;

    public Person(String name, String hobby) {
        this.name = name;
        this.hobby = hobby;
    }

    public Person() {
    }

    @Override
    public String toString() {
        return "Person{" +
                "name='" + name + '\'' +
                ", hobby='" + hobby + '\'' +
                '}';
    }
}
```

