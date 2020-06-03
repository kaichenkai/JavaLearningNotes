## Deque

### 定义

1. Queue 队列只能一头进, 另一头出, 如果把条件放松一下, 允许两头都进元素, 两头都出元素, 这种队列叫双端队列 (Double Ended Queue), 学名叫做: Deque
2. Deque 也是一个接口



### 操作Deque

1. 接口`Deque`来实现一个双端队列，它的功能是：

   - 既可以添加到队尾，也可以添加到队首；
   - 既可以从队首获取，又可以从队尾获取。
   - 避免把`null`添加到队列

2. 比较一下`Queue`和`Deque`出队和入队的方法：

   |                    | Queue                  | Deque                           |
   | :----------------- | :--------------------- | :------------------------------ |
   | 添加元素到队尾     | add(E e) / offer(E e)  | addLast(E e) / offerLast(E e)   |
   | 取队首元素并删除   | E remove() / E poll()  | E removeFirst() / E pollFirst() |
   | 取队首元素但不删除 | E element() / E peek() | E getFirst() / E peekFirst()    |
   | 添加元素到队首     | 无                     | addFirst(E e) / offerFirst(E e) |
   | 取队尾元素并删除   | 无                     | E removeLast() / E pollLast()   |
   | 取队尾元素但不删除 | 无                     | E getLast() / E peekLast()      |



### 实现Deque接口

1. Deque 的实现类有: ArrayDeque 和 LinkedList

2. 发现 LinkedList 真是一个全能选手, 它既是List, 又是Queue, 还是Deque, 但是我们在使用的时候, 总是用特定的接口来引用它, 这是应为持有接口 说明代码的抽象层次更高, 而且接口本身定义的方法代表了特定的用途.

   ```java
   // 不推荐的写法:
   LinkedList<String> d1 = new LinkedList<>();
   d1.offerLast("z");
   // 推荐的写法：
   Deque<String> d2 = new LinkedList<>();
   d2.offerLast("z");
   ```

**面向抽象编程的一个原则就是: 尽量持有接口, 而不是具体的实现类**





###### 完