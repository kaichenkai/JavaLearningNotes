## Spring - JDBC

Spring 框架对 JDBC 的简单封装, 提供了一个 JDBCTemplate 对象简化 JDBC 的开发.

步骤: 

1. 导入 jar 包

2. 创建 JdbcTemplate 对象, 依赖于数据源 DataSource

   JdbcTemplate template = new JdbcTemplate(ds)

3. 调用 JdbcTemplate 的方法来完成 CURD 的操作.

   + `update()`: 执行 DML 语句, 增, 删, 改 语句.

     

   + `queryForMap()`: 查询结果将结果集封装为 map 集合.

     + 将列名作为 key, 值作为 value, 这个方法查询的结果长度只能是 1 

       

   + `queryForList()`: 查询结果将结果集封装为 List 集合.

     + 将每一条记录封装为一个 map 集合, 再将 map 集合装载到 List 集合中.

       

   + `query()`: 查询结果, 将结果封装为 JavaBean 对象.

     + 对象的属性值类型必须是引用类型 (查询的值可能是 null ) (使用包装类)

     + query 的参数: RowMapper: 

       一般我们使用 BeanPropertyRowMapper 实现类, 可以完成数据到 JavaBean 的自动封装 ( 反序列化的概念 )

       ```java
       query(querySql, new BeanPropertyRowMapper<UserModule>(UserModule.class));
       ```

     

   + `queryForObject()`: 查询结果, 将结果封装为一些基本类型对象, (多用于 sql 聚合函数), 也可以用来查询单个的 JavaBean 对象




demo: ( 初步使用, 查询一条数据, 封装到不同的对象 )

```java
import com.company.JDBC.JDBCDruidUtils;
import org.springframework.jdbc.core.BeanPropertyRowMapper;
import org.springframework.jdbc.core.JdbcTemplate;
import java.util.List;
import java.util.Map;

/**
 * 使用 Spring JDBC 查询一条数据, 封装到不同的对象.
 */
public class Jdbc_07_使用SpringJDBC查询一条数据 {
    // 获取 JdbcTemplate 对象
    private JdbcTemplate template = new JdbcTemplate(JDBCDruidUtils.getDataSource());

    public static void main(String[] args) {
        Jdbc_07_使用SpringJDBC查询一条数据 obj = new Jdbc_07_使用SpringJDBC查询一条数据();
        // 更新一条记录
        obj.updateRecord();
        // 查询结果 Map
        obj.queryDataByMap();
        // 查询结果 List
        obj.queryDataByList();
        // 查询结果 Object  (常用!)
        obj.queryDataByObject();
        // 查询结果 返回基本数据类型, 聚合函数
        obj.queryDataByBasic();
    }

    // 更新一条数据
    public void updateRecord(){
        String updateSql = "update user set balance = 123456 where id = ?";
        int count = this.template.update(updateSql, 1);
        System.out.println("受影响的行数是: " + count);
    }

    // 查询结果, 将结果集封装为 map 集合
    public void queryDataByMap(){
        // 拼写 sql
        String querySql = "select * from user where id = ?";
        Map<String, Object> map = this.template.queryForMap(querySql, 1);
        System.out.println(map);
    }

    // 查询结果, 将结果集封装为 List 集合
    public void queryDataByList(){
        String querySql = "select * from user limit 0, 3";
        List<Map<String, Object>> list = this.template.queryForList(querySql);
        for (Map row:list) {
            System.out.println(row);
            System.out.println(row.get("username"));
        }
    }

    // 查询结果, 将结果集封装为 JavaBean 对象 (放在java实例属性值)
    public void queryDataByObject(){
        String querySql = "select * from user limit 0, 3";
        List<UserModule> objList = this.template.query(querySql, new BeanPropertyRowMapper<UserModule>(UserModule.class));
        for (UserModule user:objList) {
            System.out.println(user);
            System.out.println(user.getBalance());
        }
    }

    // 查询结果, 返回基本数据类型, 多用于 聚合函数
    public void queryDataByBasic(){
        String querySql = "select sum(balance) from user";
        Integer balanceTotal = this.template.queryForObject(querySql, Integer.class);
        System.out.println(balanceTotal);  // 125456
    }
}
```





