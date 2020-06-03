## Set

### 定义

1. `Map`用于存储key-value的映射，对于充当key的对象，是不能重复的，并且，不但需要正确覆写`equals()`方法，还要正确覆写`hashCode()`方法。如果我们只需要存储不重复的key，并不需要存储映射的value，那么就可以使用`Set`。
2. `Set`实际上相当于只存储key、不存储value的`Map`
3. 因为放入`Set`的元素和`Map`的key类似，都要正确实现`equals()`和`hashCode()`方法，否则该元素无法正确地放入`Set`。
4. 最常用的`Set`实现类是`HashSet`，实际上，`HashSet`仅仅是对`HashMap`的一个简单封装



### 操作Set

`Set`用于存储不重复的元素集合，它主要提供以下几个方法：

- 将元素添加进`Set<E>`：`boolean add(E e)`
- 将元素从`Set<E>`删除：`boolean remove(Object e)`
- 判断是否包含元素：`boolean contains(Object e)`
- 返回 Set 长度： `int size();`

```java
public static void main(String[] args) {
    Set<String> set = new HashSet<>();
    //添加元素
    System.out.println(set.add("xiaohong"));//添加成功返回true
    System.out.println(set.add("aaa"));//添加成功返回true
    System.out.println(set.add("bbb"));//添加成功返回true
    //删除元素
    System.out.println(set.remove("xiaohong"));//删除成功返回true
    System.out.println(set.remove("test"));//删除失败返回false, py中删除失败报错
    //输出Set长度
    System.out.println(set.size());//2
}
```



### SortedSet

`Set`接口并不保证有序，而`SortedSet`接口则保证元素是有序的：

- `HashSet`是无序的，因为它实现了`Set`接口，并没有实现`SortedSet`接口；
- `TreeSet`是有序的，因为它实现了`SortedSet`接口。
- 使用`TreeSet`和使用`TreeMap`的要求一样，添加的元素必须正确实现`Comparable`接口，如果没有实现`Comparable`接口，那么创建`TreeSet`时必须传入一个`Comparator`对象。

```text
       ┌───┐
       │Set│
       └───┘
         ▲
    ┌────┴─────┐
    │          │
┌───────┐ ┌─────────┐
│HashSet│ │SortedSet│
└───────┘ └─────────┘
               ▲
               │
          ┌─────────┐
          │ TreeSet │
          └─────────┘
```



###### 完 ~

