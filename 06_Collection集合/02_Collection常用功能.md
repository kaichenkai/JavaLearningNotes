## Collection常用功能

最顶层的接口, 里边定义了所有单列集合共性的方法

单列集合子类可使用共性方法:

+ `public boolean add(E e)`：  把给定的对象添加到当前集合中 。
+ `public void clear()` :清空集合中所有的元素。
+ `public boolean remove(E e)`: 把给定的对象在当前集合中删除。
+ `public boolean contains(E e)`: 判断当前集合中是否包含给定的对象。
+ `public boolean isEmpty()`: 判断当前集合是否为空。
+ `public int size()`: 返回集合中元素的个数。
+ `public Object[] toArray()`: 把集合中的元素，存储到数组中。

