## 用户登录案例

需求: 

1. 编写 login.html 登录页面

   username  &  passwd 两个输入框

2. 使用 Druid 数据库连接池技术, 并使用Spring  JDBCTemplate 对象封装连接池, 操作数据库.

3. 获取用户提交的 form 表单数据, 查询数据库

4. 登录成功转发到成功的 Servlet 进行处理, 返回 登录成功, 欢迎 xxx

5. 登录失败转发到失败的 Servlet 处理, 返回登录失败.



注意: 

1. jar 包的路径: web/WEB-INF/lib

2. druid.properties 配置文件的位置

3. 返回内容需要设置内容的格式与编码

   `response.setContentType("text/html; charset=utf-8");`



login.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>UserLogin</title>
</head>
<body>
    <form action="/login" method="post">
        用户名: <input type="text" name="username"> <br>
        密码:    <input type="password" name="passwd"> <br>
        <input type="submit" value="login">
    </form>
</body>
</html>
```



用户模型类

```java
package com.web.Servlet_01_UserLogin.domain;

public class User {
    private Integer id;
    private String username;
    private String passwd;
    private Integer balance;

	getter and  setter 
    ...
}

```



用户模型 dao

```java
import com.web.Servlet_01_UserLogin.domain.User;
import com.web.Servlet_01_UserLogin.util.JDBCDruidUtils;
import org.springframework.dao.DataAccessException;
import org.springframework.jdbc.core.BeanPropertyRowMapper;
import org.springframework.jdbc.core.JdbcTemplate;

public class UserDao {
    // 获取连接池
        private JdbcTemplate template = new JdbcTemplate(JDBCDruidUtils.getDataSource());

    public User login(String username, String passwd) {

        try {
            // 拼写 sql
            String querySql = "select * from user where username = ? and passwd = ?";
            User user = template.queryForObject(querySql, new BeanPropertyRowMapper<User>(User.class),
                username, passwd);
            return user;
        } catch (DataAccessException e) {
//            e.printStackTrace();
            return null;
        }
    }
}
```



JDBCDruidUtils

```java
import com.alibaba.druid.pool.DruidDataSourceFactory;
import org.springframework.jdbc.core.JdbcTemplate;
import javax.sql.DataSource;
import java.io.InputStream;
import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.util.Properties;

/**
 * JDBCDruidUtils 工具类
 */
public class JDBCDruidUtils {
    private static DataSource ds = null;

    static {
        try {
            // 加载配置文件
            Properties pro = new Properties();
            // 获取 src 路径下的文件 --> ClassLoader
            ClassLoader cl = JDBCDruidUtils.class.getClassLoader();
            InputStream is = cl.getResourceAsStream("druid.properties");
            pro.load(is);
            // 通过工厂函数 获取 数据库连接池 (传入配置文件)
            ds = DruidDataSourceFactory.createDataSource(pro);

        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    // 获取连接池对象
    public static DataSource getDataSource(){
        return ds;
    }

    // 获取连接对象
    public static Connection getConnection() throws SQLException {
        return ds.getConnection();
    }

    // 资源回收
    public static void close(ResultSet ret, PreparedStatement pstat, Connection conn){
        if (ret != null) {
            try {
                ret.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }

        if (pstat != null) {
            try {
                ret.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }

        if (conn != null) {
            try {
                ret.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }

    public static void main(String[] args) {
        JdbcTemplate template = new JdbcTemplate(JDBCDruidUtils.getDataSource());
        System.out.println(template);
    }
}

```



LoginServlet

```java
import com.web.Servlet_01_UserLogin.dao.UserDao;
import com.web.Servlet_01_UserLogin.domain.User;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

@WebServlet("/login")
public class LoginServlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        // 获取用户提交的参数
        String username = request.getParameter("username");
        String passwd = request.getParameter("passwd");
        if (username == null || passwd == null) {
            // 返回参数错误
            response.getWriter().write("参数缺失");
        }
        User user = new UserDao().login(username, passwd);

        if ( user != null ) {
            // 登录成功
            request.setAttribute("username", username);
            // 转发到登录成功的页面
            request.getRequestDispatcher("/success").forward(request, response);
        } else {
            // 登录失败
            request.getRequestDispatcher("/failed").forward(request, response);
        }
    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

    }
}
```



LoginSuccess

```java
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

/**
 * 登录成功
 */
@WebServlet("/success")
public class LoginSuccess extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        // 设置编码
        response.setContentType("text/html; charset=utf-8");
        // 获取 request 域中的共享数据
        Object username = request.getAttribute("username");
        response.getWriter().write("登录成功, 欢迎您, " + username);

    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

    }
}
```



LoginFailed

```java
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

/**
 * 登录失败
 */
@WebServlet("/failed")
public class LoginFailed extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        // 设置编码
        response.setContentType("text/html; charset=utf-8");
        response.getWriter().write("登录失败!");
    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

    }
}
```



###### 完 !

