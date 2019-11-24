## BeanUtils jar 包

apache 开源免费的 jar 包: `commons-beanutils-1.8.0.jar`

> ```
> import org.apache.commons.beanutils.BeanUtils;
> ```



作用: 简化数据的封装, 不用一个一个参数的去获取, 类似于反序列化. 



demo: 将用户的登录信息封装到 javabean 中:

```java
// 使用 BeanUtils 工具包将参数封装到 javabean 中 (像反序列化)
// 1. 先获取参数, 放到 Map 集合中
Map<String, String[]> map = request.getParameterMap();
// 2. 放入到对应的 javabean 中
User loginUser = new User();

try {
    BeanUtils.populate(loginUser, map);
} catch (IllegalAccessException e) {
    e.printStackTrace();
} catch (InvocationTargetException e) {
    e.printStackTrace();
}
```



问题: 有其它类型的值有什么好的方式处理 ?



###### 完 !