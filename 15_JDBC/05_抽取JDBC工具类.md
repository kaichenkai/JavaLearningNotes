## 抽取 JDBC 工具类

步骤:

1. 封装 JDBCUtils 工具类
2. 通过 properties 配置文件来读取数据库连接信息
3. 通过静态代码块来初始化, 连接到数据库
4. 封装释放资源的静态方法



jdbc.properties:

```properties
ipaddr=192.168.0.115
port=3306
dbname=JDBC
username=chenkai
passwd=chenkai
```



JDBCUtils: 

```java
import java.sql.*;
import java.util.Properties;
import java.io.IOException;
import java.io.FileReader;
import java.net.URL;


/**
 * 封装 JDBC 的工具类
 */
public class JDBCUtils {
    private static String ipaddr;
    private static String port;
    private static String dbname;
    private static String username;
    private static String passwd;

    static {
        try {
            // 读取配置文件, 初始化连接数据库
            Properties pro = new Properties();
            // 获取 src 路径下的文件 --> ClassLoader
            ClassLoader cl = JDBCUtils.class.getClassLoader();
            URL url = cl.getResource("jdbc.properties");
            String path = url.getPath();  // 配置文件的绝对路径
            // 加载配置文件
            pro.load(new FileReader(path));
            // 获取配置文件中的参数
            ipaddr = pro.getProperty("ipaddr");
            port = pro.getProperty("port");
            dbname = pro.getProperty("dbname");
            username = pro.getProperty("username");
            passwd = pro.getProperty("passwd");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    // 获取连接
    public static Connection getConnection(){
        try {
            // 注册驱动
            Class.forName("com.mysql.jdbc.Driver");
            // 获取连接
            Connection conn = DriverManager.getConnection(String.format("jdbc:mysql://%s:%s/%s", ipaddr, port, dbname), username, passwd);
            return conn;
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        } catch (SQLException e) {
            e.printStackTrace();
        }
        //
        return null;
    }

    public static void close(ResultSet ret, Statement statement, Connection conn){
        if (ret!=null) {
            try {
                ret.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }

        if (statement!=null) {
            try {
                ret.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }

        if (conn!=null) {
            try {
                ret.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }

    public static void close(PreparedStatement pstatement, Connection conn){
        if (pstatement!=null) {
            try {
                pstatement.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }

        if (conn!=null) {
            try {
                conn.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }
}
```



client:

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
            // 1.获取数据库连接
            conn = JDBCUtils.getConnection();
            // 2.编写sql
            String sql = "select * from student";
            // 4.获取statement操作对象
            st = conn.createStatement();
            // 5.执行sql
            ret = st.executeQuery(sql);
            // 6.处理sql执行结果
            ret.next();
            int id = ret.getInt(1);
            String name = ret.getString("name");
            System.out.println(String.format("id: %s， name: %s", id, name));

        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            // 7.释放资源
            JDBCUtils.close(ret, st, conn);
        }
    }
}

```

