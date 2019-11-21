## Thread 和 Runnable 接口的区别

实现 Runnable 接口, 开启多线程:

```java
public class Main {
    public static void main(String[] args) {
        // 创建一个 Runnable 接口的实现类对象
        RunnableImpl run = new RunnableImpl();
        // 创建 Thread 类对象, 构造方法中传入 Runnable 实现类对象
        Thread mt = new Thread(run);
        mt.start();
    }
}


class RunnableImpl implements Runnable{
    @Override
    public void run(){
        System.out.println(Thread.currentThread().getName());
    }
}
```



实现 Runnable 接口创建多线程的优点:

1. 一个类只能继承一个类, 而一个类可以实现多个接口(实现了 Runnable 接口, 还能实现其它的接口 ,  继承其它的类)

2. 增强程序的扩展性, 降低耦合性(解耦合)

   实现 Runnable 接口的方式, 把设置线程任务和开启新线程进行了分离

   实现类中, 重写了 run 方法:  用来设置线程任务

   创建 Thread 类对象, 传入 run 方法,  开启线程





###### 完 !

