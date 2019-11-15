## JDBC 操作数据库练习

插入一条数据:

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;

/**
 * 使用 JDBC 插入一条数据
 */
public class JdbcDemo01 {
    public static void main(String[] args) {
        Connection conn = null;
        Statement st = null;
        try {
            // 1.注册驱动
            Class.forName("com.mysql.jdbc.Driver");
            // 2.编写sql
            String sql = "insert into student values(null, 'johny')";
            // 3.获取数据库连接
            conn = DriverManager.getConnection("jdbc:mysql://192.168.0.115:3306/JDBC", "username", "passwd");
            // 4.获取statement操作对象
            st = conn.createStatement();
            // 5.执行sql
            int num = st.executeUpdate(sql);
            // 6.处理sql执行结果
            System.out.println(num);  // 1
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            // 7.释放资源
            try {
                st.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }

            try {
                conn.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }
}

```



查询一条数据: 

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;
import java.sql.ResultSet;

/**
 * 使用 JDBC 查询一条数据
 */
public class JdbcDemo01 {
    public static void main(String[] args) {
        Connection conn = null;
        Statement st = null;
        ResultSet ret = null;
        try {
            // 1.注册驱动
            Class.forName("com.mysql.jdbc.Driver");
            // 2.编写sql
            String sql = "select * from student";
            // 3.获取数据库连接
            conn = DriverManager.getConnection("jdbc:mysql://192.168.0.115:3306/JDBC", "username", "passwd");
            // 4.获取statement操作对象
            st = conn.createStatement();
            // 5.执行sql
            ret = st.executeQuery(sql);
            // 6.处理sql执行结果
            ret.next();
            int id = ret.getInt(1);
            String name = ret.getString("name");
            System.out.println(String.format("id: %s， name: %s", id, name));   // id: 1， name: johny

        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            // 7.释放资源
            try {
                ret.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }

            try {
                st.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }

            try {
                conn.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }
}
```









