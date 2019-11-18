## HttpServlet 类

Servlet 的体系结构:

Servlet 接口 --> GenericServlet 抽象类 --> HttpServlet 抽象类



GenericServlet 抽象类: 

将 Servlet 接口中其它抽象方法做了默认实现, 只将 service() 方法作为抽象方法

使用: 

1. 继承 GenericServlet 抽象类, 实现 service() 方法即可.



HttpServlet 抽象类: 

对 http 协议的一种封装, 简化了操作.

使用: 

1. 继承 HttpServlet, 覆写 doGet / doPost 方法



demo: 

```java
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;


/**
 * HttpServlet 初步使用
 */
@WebServlet("/demo1")
public class Servlet_02_HttpServlet初步使用 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        // System.out.println("doGet");
        System.out.println("doGet");
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        // super.doPost(req, resp);
        System.out.println("doPost");
    }
}
```









###### 完 !















