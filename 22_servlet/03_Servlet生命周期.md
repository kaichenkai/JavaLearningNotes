## Servlet 生命周期

分为三个部分: 

1. 被创建 ( init )

   什么时候被创建?

   + Servlet 的 init 方法, 只执行一次, 说明一个 Servlet 在内存中只存在一个对象 ( 单例模式 )

     + 竟然 Servlet 对象是单例的, 那么多用户访问时, 就会存在线程安全问题 ( 尽量不要在 Servlet 接口实现类中定义成员变量, 即使定义了成员变量, 也不要修改值 )

   + 默认情况下: 第一次被访问时, Servlet 对象被创建 ( 可配置 Servlet 对象创建的时机 )

   + 在 web.xml 文件中指定创建时机

     ```xml
     <!--配置 Servlet-->
     <servlet>
         <servlet-name>demo1</servlet-name>
         <servlet-class>com.web.Servlet_01_快速使用servlet</servlet-class>
         <!--指定 Servlet 对象创建的时机
             1. 默认第一次访问时创建 (配置负数也行)
             2. 在 tomcat 服务启动时创建 (配置 0 或 正整数)
             -->
         <load-on-startup>0</load-on-startup>
     </servlet>
     ```

2. 提供服务 ( service )

   + 每次访问 Servlet 时, service 方法都会被调用一次.

3. 被销毁 ( destroy )

   + Servlet 对象被销毁时, 执行 ( 服务器正常关闭情况下才执行, 一般用于释放资源 )







###### 完 !