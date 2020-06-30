## List

`java.util.List`

在集合类中, List 是最基础的一种集合: 它是一种有序链表. (有索引), 例如: 按照索引排列的 Student 的 List.

`List`的行为和数组几乎完全相同：`List`内部按照放入元素的先后顺序存放，每个元素都可以通过索引确定自己的位置，`List`的索引和数组一样，从`0`开始



### List  的实现类

ArrayList 和 LinkedList

List 是按索引顺序访问的长度可变的有序链表, 优先使用 **ArrayList** 而不是 LinkedList.

|                     | ArrayList    | LinkedList           |
| :------------------ | :----------- | :------------------- |
| 获取指定元素        | 速度很快     | 需要从头开始查找元素 |
| 添加元素到末尾      | 速度很快     | 速度很快             |
| 在指定位置添加/删除 | 需要移动元素 | 不需要移动元素       |
| 内存占用            | 少           | 较大                 |



### 创建List的两种方式

1. 使用 ArrayList 创建

   ```java
   List<String> list = new ArrayList<>();
   ```

2. 调用 List 接口的 of() 

   ```java
   List<Integer> list = List.of(1, 2, 5);  //java9 版本支持
   ```



### 遍历List 对象

可以直接使用 for each 遍历 List.



### 操作List对象

考察`List<E>`接口，可以看到几个主要的接口方法：

- 在末尾添加一个元素：`void add(E e)`
- 在指定索引添加一个元素：`void add(int index, E e)`
- 删除指定索引的元素：`int remove(int index)`
- 删除某个元素：`int remove(Object e)`
- 替换某个元素(索引不能越界)：`E set(int index, E e)`
- 获取指定索引的元素：`E get(int index)`
- 获取链表大小（包含元素的个数）：`int size()`

索引超出异常

```java
List<String> list = new ArrayList<>();
System.out.println(list.get(0));  //java.lang.IndexOutOfBoundsException: Index: 0, Size: 0
```



### List 可以和 Array 相互转换

1. List --> Array

   ```java
   list.add("xiaoming");
   list.add("xiaohong");
   String[] array = list.toArray(new String[list.size()]); //将 List --> Array
   System.out.println(Arrays.toString(array)); //[xiaoming, xiaohong]
   ```

2. Array --> List  (使用 Arrays 工具类)

   ```java
   String[] arr = new String[] {"1", "2", "3"};
   List<String> list = Arrays.asList(arr);
   for (String s : list) {
       System.out.println(s);
   }
   ```
   
   不过，这样做有些坑要注意：
   
   - 这样做生成的list，是定长的。也就是说，如果你对它做add或者remove，都会抛UnsupportedOperationException。
   
   - 如果修改数组的值，list中的对应值也会改变！
   
     **Arrays.asList() 返回的是Arrays内部静态类，而不是Java.util.ArrayList的类。****这个java.util.Arrays.ArrayList有set(),get(),contains()方法，但是没有任何add() 方法，所以它是固定大小的**
   
   如果希望避免这两个坑，请改用这个方式
   
   ```java
   Hero[] heroes = new Hero[]{new Hero("one"), new Hero("two"), new Hero("three")};
   List<Hero> list = new ArrayList<>();
   Collections.addAll(list, heroes);
   list.add(new Hero("four"));
   System.out.println(list);
   ```



### 把另一个容器的所有对象都加进来 (addAll)

```java
List list1 = new ArrayList();
list1.add(new Person("test", 10));
list1.addAll(list);
System.out.println(list1);
```



### 清空 

```java
arrayList.clear();
```



### List 特点

1. List对象内部的元素**可以重复**
2. List对象内部的元素**可以是 null**