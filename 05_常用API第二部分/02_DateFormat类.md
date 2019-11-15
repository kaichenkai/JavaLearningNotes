## DateFormat  类

DateFormat 是一个抽象类

`import java.text.DateFormat;`

SimpleDateFormat 是实现的非抽象子类

`import java.text.SimpleDateFormat`



作用: 

+ 将Date类型格式化为指定模式的字符串

  ```java
  import java.text.SimpleDateFormat;
  import java.util.Date;
  
  public class Main {
      public static void main(String[] args) {
          SimpleDateFormat sd =  new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
          String dateStr = sd.format(new Date());
          System.out.println(dateStr);  // 2019-10-24 22:37:28
      }
  }
  ```

+ 将字符串解析为Date类型

  ```java
  import java.text.ParseException;
  import java.text.SimpleDateFormat;
  import java.util.Date;
  
  public class Main {
      public static void main(String[] args) throws ParseException {  // 解析可能会发生异常
          SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
          Date d = sdf.parse("2019-10-24 22:37:28");
          System.out.println(d);  // Thu Oct 24 22:37:28 CST 2019
      }
  }
  ```

  

  

