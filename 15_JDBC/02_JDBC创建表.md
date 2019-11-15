## JDBC 创建表

使用 mysql jar 包操作数据库的步骤:

首先需在 mysql 上创建数据库

1. 在项目里边导入 mysql jar 包, 注册驱动
2. 获取数据库连接对象, 获取游标对象 cursor
3. 组织 sql 语句
4. 使用 cursor 执行 sql
5. 处理结果
6. 释放资源



demo:

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.Statement;

/**
 * JDBC 初步使用
 */
public class ConnectDataBase {
    public static void main(String[] args) throws Exception {
        // 导入 mysql jar 包, 注册驱动
        Class.forName("com.mysql.jdbc.Driver");
        // 获取数据库连接对象, 获取 cursor
        Connection conn = DriverManager.getConnection("jdbc:mysql://192.168.0.115/JDBC", "username", "passwd");
        Statement st = conn.createStatement();
        // 写 sql
        String sql = "create table student(id int unsigned primary key auto_increment not null, name varchar(150))";
        // 执行 sql
        int num = st.executeUpdate(sql);
        // 处理结果
        // 执行成功返回 0, 再次执行: Exception in thread "main" com.mysql.jdbc.exceptions.jdbc4.MySQLSyntaxErrorException: Table 'student' already exists
        System.out.println(num);
        // 释放资源
        st.close();
        conn.close();
    }
}
```

