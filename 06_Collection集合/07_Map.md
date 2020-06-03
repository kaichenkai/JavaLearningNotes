## Map

### 定义

1. Map也是一个接口, 最常用的实现类是 HashMap
2. Map<K, V> 是一种键值映射表, 可以通过key快速查找value, 调用 put(K key, V value) 方法时, 就把 key 和 value 做了映射并放入 Map, 调用 V get(K key) 时, 就可以通过 key 获取到对应的 value, 如果 key 不存在,则返回null
3. Map 中不存在重复的 key, 因为放入了相同的 key, 会把原有的 key-value 替换掉, 虽然 key 不能重复, 但 value 可以
4. Map 中 key-value 是无序的



### 遍历Map

1. 可以通过`for each`遍历`keySet()`，也可以通过`for each`遍历`entrySet()`，直接获取`key-value`

   ```java
   public static void main(String[] args) {
       //定义Map
       Map<String, Student> studentMap = new HashMap<>();
       //定义学生
       Student s1 = new Student("xiaohong", 19);
       Student s2 = new Student("xiaogang", 20);
       //添加到 Map中
       studentMap.put("xiaohong", s1);
       studentMap.put("xiaogang", s2);
       // foreach 遍历 Map (keySet() 获取 key 的集合)
       for (String key : studentMap.keySet()) {
           System.out.println(studentMap.get(key).getName());
       }
   }
   ```



### EnumMap

1. 使用`EnumMap`的时候，我们总是用`Map`接口来引用它，因此，实际上把`HashMap`和`EnumMap`互换，在客户端看来没有任何区别。
2. 如果`Map`的key是`enum`类型，推荐使用`EnumMap`，既保证速度，也不浪费空间。
3. 使用`EnumMap`的时候，根据面向抽象编程的原则，应持有`Map`接口。

### TreeMap

1. `SortedMap` 内部会对Key进行排序, 注意到`SortedMap`是接口，它的实现类是`TreeMap`

   ```text
          ┌───┐
          │Map│
          └───┘
            ▲
       ┌────┴─────┐
       │          │
   ┌───────┐ ┌─────────┐
   │HashMap│ │SortedMap│
   └───────┘ └─────────┘
                  ▲
                  │
             ┌─────────┐
             │ TreeMap │
             └─────────┘
   ```

2. 作为`SortedMap`的Key必须实现`Comparable`接口，或者传入`Comparator`；

3. 要严格按照`compare()`规范实现比较逻辑，否则，`TreeMap`将不能正常工作。



###### 完 !

