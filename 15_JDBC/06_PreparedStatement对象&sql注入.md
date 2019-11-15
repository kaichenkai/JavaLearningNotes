## PreparedStatement & sql注入

使用 PreparedStatement 对象执行sql的步骤: 

1. 导入驱动包

2. 获取数据库连接对象

3. 定义 sql (使用 ? 作为占位符)

4. 获取sql执行对象 (PreparedStatement)

5. ##### 给 ? 赋值(setInt, setString...   传递两个参数, 位置和值, 位置从 1 开始)

6. 执行sql (不需要再传递 sql 语句)

7. 处理结果

8. 释放资源



后边操作数据库都用 PreparedStatement 对象来完成增删改查的所有操作



demo:

```java
import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.util.Scanner;

/**
 * 模拟用户登录, 处理sql注入问题
 */
public class UserLogin {
    public Connection conn = null;
    public PreparedStatement pstat = null;
    public ResultSet ret = null;


    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("请输入用户名:");
        String username = sc.nextLine();
        System.out.print("请输入密码:");
        String passwd = sc.nextLine();

        boolean ret = new UserLogin().login(username, passwd);
        if (ret) {
            System.out.println("登录成功");
        } else {
            System.out.println("用户名或密码输入错误!");
        }
    }

    public boolean login(String username, String passwd){
        if (username == null | passwd == null) {
            return false;
        }

        try{
            // 通过 JDBCUtils 获取数据库连接
            conn = JDBCUtils.getConnection();
            // 拼写sql
            String sql = "select * from user where username = ? and passwd = ?";
            // 获取 PreparedStatement 对象
            pstat = conn.prepareStatement(sql);
            // 给 sql 赋值
            pstat.setString(1, username);
            pstat.setString(2, passwd);
            // 执行 sql
            ret = pstat.executeQuery();
            // 处理结果
            return ret.next();
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            JDBCUtils.close(ret, pstat, conn);
        }
        return false;
    }
}
```

