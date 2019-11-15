## Random 类

Random类可以生成一个随机数:

`import  java.util.Random;` 

`Random r = new Random();`



获取一个随机 int 数字 ( 范围是 int 所有范围，有正负两种 ) : `int num = random.nextInt()`

获取一个随机 int 数字 ( 参数代表了范围，顾前不顾尾 ):

`int num = random.nextInt(100)`    取值的范围是[0, 99)

```java
// 猜数字小游戏
import java.util.Scanner;
import java.util.Random;

public class RandomGame {
    public static void main(String[] args) {
        int random = new Random().nextInt(100);
        System.out.println(random);

        while (true) {
            int num = new Scanner(System.in).nextInt();
            if (num > random){
                System.out.println("greater than");
            } else if (num < random){
                System.out.println("less than");
            } else {
                System.out.println("bingo");
                break;
            }
        }
    }
}
```



###### 完 ! 



