## Druid 

使用步骤: 

1. 导入 jar 包 druid-1.0.9.jar
2. 定义配置文件
   + 是 properties 形式
   + 文件可以放在任意目录下, 通过路径加载配置文件
3. 加载配置文件
4. 获取数据库连接池对象: 通过工厂函数来获取: DruidDataSourceFactory.createDataSource()
5. 获取连接 --> 获取执行对象 --> 处理结果集 --> 资源回收



JDBCDruidUtils 工具类: 

```java
import com.alibaba.druid.pool.DruidDataSourceFactory;
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
}

```



druid.properties:

```properties
driverClassName=com.mysql.jdbc.Driver
url=jdbc:mysql://192.168.0.115:3306/JDBC
username=username
password=passwd
initialSize=5
maxActive=10
maxWait=3000
```



demo: 

```java
import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;


public class JdbcDruid {
    public static void main(String[] args) {

        Connection conn = null;
        PreparedStatement pstat = null;
        ResultSet ret = null;

        try {
            // 获取数据库连接
            conn = JDBCDruidUtils.getConnection();
            // 编写sql
            String sql = "select * from user where username = ?;";
            // 获取执行 sql 对象
            pstat = conn.prepareStatement(sql);
            // 给 sql 赋值
            pstat.setString(1, "xiaoming");
            // 执行sql
            ret = pstat.executeQuery();
            // 读取一条记录
            ret.next();
            // 处理结果 ResultSet
            String passwd = ret.getString("passwd");
            System.out.println(passwd);  // 123

        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            JDBCDruidUtils.close(ret, pstat, conn);
        }
    }
}

```



