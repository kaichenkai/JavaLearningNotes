## JDBC 控制事务

事务: 它是一个操作序列，这些操作要么都执行，要么都不执行，它是一个不可分割的操作单位.

使用 Connection 对象来管理事务

1. 开启事务: setAutoCommit(boolean autoCommit): 调用该方法设置参数为 false, 即开启事务

   执行 sql 前开启事务.

2. 提交事务: commit()

   所有 sql 都执行完提交事务.

3. 回滚事务: rollback()

   在 catch 中回滚事务.



demo:

```java
import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.SQLException;

/**
 *  JDBC 事务的应用, 模拟转账
 */
public class JdbcDemo02 {
    public static void main(String[] args) {
        Connection conn = null;
        PreparedStatement pstat1 = null;
        PreparedStatement pstat2 = null;

        try {
            // 获取数据库连接
            conn = JDBCUtils.getConnection();
            // 开启事务!!!
            conn.setAutoCommit(false);
            // 编写sql
            String sql1 = "update user set balance = balance - 500 where username = ?";
            String sql2 = "update user set balance = balance + 500 where username = ?";
            // 获取 preparedStatement 对象
            pstat1 = conn.prepareStatement(sql1);
            pstat2 = conn.prepareStatement(sql2);
            // 给 sql 赋值
            pstat1.setString(1, "xiaoming");
            pstat2.setString(1, "xiaohong");
            // 执行sql
            pstat1.executeUpdate();
            pstat2.executeUpdate();

            //手动抛出异常
            int a = 3 / 0;

            // 提交事务
            conn.commit();
            System.out.println("处理完成");
        } catch (Exception e) {
            e.printStackTrace();
            // 回滚事务, 数据库连接不为空的时候进行回滚  (不会滚也不会更新成功, 回滚是不是在释放资源 ?)
            if (conn != null) {
                try {
                    conn.rollback();
                } catch (SQLException e1) {
                    e1.printStackTrace();
                }
            }
        } finally {
            // 释放资源
            JDBCUtils.close(pstat1, conn);
            JDBCUtils.close(pstat2, null);
        }
    }
}
```





 

