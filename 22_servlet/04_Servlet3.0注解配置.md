## Servlet3.0 注解配置

好处: 支持注解配置, 不再需要web目录下的 web.xml 文件了, 使用更方便

使用步骤: 

1. 创建 JavaEE 项目, 选择 Servlet 的版本 3.0 以上, 不创建 web.xml
2. src 目录下实现代码, 定义一个类, 实现 Servlet 接口, 覆写所有抽象方法
3. jar 包放在 web/WEB-INF/lib 目录下
4. 在类名上方, 使用注解: `@WebServlet(" uri ")`



urlpartten 的配置: 

1. 一个 Servlet 实现类可以定义多个访问路径: `@WebServlet({"/d4", "/dd4"})`
2. 路径定义规则:
   + /xxx
   + /xxx/xxx:  多层路径
   + *.do: 支持通配符



demo: 

```java
import javax.servlet.*;
import javax.servlet.annotation.WebServlet;
import java.io.IOException;


/**
 * 用注解的方式使用 Servlet
 */
@WebServlet(urlPatterns = "/demo")
public class Servlet_01_使用注解 implements Servlet {

    @Override
    public void init(ServletConfig servletConfig) throws ServletException {
        System.out.println("init ...........servlet");
    }

    @Override
    public ServletConfig getServletConfig() {
        return null;
    }

    @Override
    public void service(ServletRequest servletRequest, ServletResponse servletResponse) throws ServletException, IOException {
        System.out.println("Servlet 3.0 !!!");
    }

    @Override
    public String getServletInfo() {
        return null;
    }

    @Override
    public void destroy() {

    }
}
```



###### 完 !

