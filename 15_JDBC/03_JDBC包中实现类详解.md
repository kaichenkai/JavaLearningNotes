## JDBC 包中各个实现类的详解

### DriverManager: 驱动管理对象

1. 导入 mysql jar 包, 注册驱动

   `Class.forName("com.mysql.jdbc.Driver");`

   通过查看源码发现, 在 com.mysql.jdbc.Driver 类中存在静态代码块:

   ```java
   static {
       try {
           java.sql.DriverManager.registerDriver(new Dirver());
       } catch (SQLException E) {
           throw new RuntimeException("Can't register driver!");
       }
   }
   ```

   提示: mysql 1.5版本之后的 jar 包可以省略注册驱动的步骤 (会根据配置文件自动导入)

   

2. 获取数据库连接

   ```java
   public static Connection getConnection(String url, String user, String password)
   ```

   url: jdbc:mysql://IP:PORT/DataBaseName

   

### Connection: 数据库连接对象

1. 获取执行 sql 的cursor 对象

   `Statement  createStatement();`

   `PreparedStatement prepareStatement(String sql);`

   

2. 管理事务

   开启事务: `void setAutoCommit(boolean autoCommit);`

   提交事务: `commit()`

   回滚事务: `rollback()`



### Statement: 执行 sql 的对象

1. 执行sql

   `int executeUpdate(String sql)`: 执行 DML (insert, update, delete) ,  DDL (create, alter, drop) 

   `ResultSet executeQuery(String sql)`: 执行DQL (select)

   `boolean execute(String sql)`: 可以执行任意的sql (不常用)



### ResultSet: 结果集对象

封装查询结果

常用方法: 

1. `boolean next()`: 游标向下移动一行
2. `int getInt(int columnIndex)`: 获取一个 int 类型的值 (传编号[编号从1开始] 或 列名)
3. `int getInt(String columnLabel)`
4. `String getString(int columnIndex)`: 获取一个 String 类型的值 (传编号 或 列名)
5. `String getString(String columnLabel)`



### PreparedStatement: 执行 sql 的对象

使用 PreparedStatement 对象能解决 sql 注入的问题, 

