## Thread 类

`java.lang.Thread`

> java 虚拟机允许应用程序并发地运行多个线程(真的多线程)
>
> java 线程属于抢占式调度, 哪个线程的优先级高, 哪个线程优先执行, 同一个优先级, 随机执行
>
> 多个线程之间互不影响



创建线程的两种方法:

1. 创建 Thread 子类, 重写 run 方法
2. 实现 Runnable 接口的类,  然后实现 run 方法



```java
public class Main {
    public static void main(String[] args) {
        MyTread mt1 = new MyTread();
        mt1.start();

        for (int i=1; i<=20; i++) {
            System.out.println("main" + i);
        }
    }
}

class MyTread extends Thread {
    @Override
    public void run(){
        for (int i=0; i<20; i++) {
            System.out.println("run" + i);
        }
    }
}
```



运行效果:

```java
main1
run0
main2
run1
main3
main4
run2
main5
main6
main7
main8
main9
run3
main10
run4
main11
run5
run6
run7
run8
run9
run10
run11
run12
run13
run14
run15
run16
main12
main13
run17
run18
run19
main14
main15
main16
main17
main18
main19
main20
```

