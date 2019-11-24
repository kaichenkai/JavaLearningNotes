## cookie 案例

##### 需求

1. 访问一个 servlet, 如果是第一次访问, 那么提示: 您好, 欢迎首次登陆!
2. 如果不是第一次访问, 则提示: 欢迎回来, 您上次访问时间为: 年月日, 时分秒.



##### 分析

1. 可以采用 cookie 来完成.
2. 在服务器中的 Servlet 判断是否有一个名为 lastTime 的cookie
   1. 没有: 第一次访问, 设置 cookie, 返回欢迎信息.
   2. 有: 返回上次访问的日期时间.





##### 实现

```java
/**
 * cookie 访问案例
 */
@WebServlet("/cookie")
public class CookieDemo extends HttpServlet {
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        // 尝试获取浏览器中的     cookie
        Cookie[] cookies = request.getCookies();
        // 设置字符流的编码
        response.setContentType("text/html; charset=utf-8");

        // 考虑有其它的 cookie 但没有 lastTime 这个 cookie
        boolean flag = false;
        //
        if (cookies != null && cookies.length > 0) {

            for (Cookie cookie : cookies) {
                if ("lastTime".equals(cookie.getName())){
                    // 获取 cookie 中上次访问的时间日期
                    String lastTimeStr = cookie.getValue();
                    response.getWriter().write("<h1>您上次登录访问时间: " + lastTimeStr + "</h1>");
                    // 重新设置 cookie
                    this.setCookie(response);
                    // 已经找到 cookie 的值
                    flag = true;
                    break;
                }
            }
        }

        if ( cookies == null || cookies.length < 1 || flag == false) {
            // 第一次访问, 设置 cookie
            this.setCookie(response);
            // 返回欢迎信息
            response.getWriter().write("<h1>您好, 欢迎登陆首页</h1>");
        }
    }

    /**
     * 设置 cookie
     * @param response
     */
    public void setCookie(HttpServletResponse response){
        LocalDateTime ldt = LocalDateTime.now(); // 获取当前日期时间对象
        DateTimeFormatter dtf = DateTimeFormatter.ofPattern("yyy-MM-dd HH:mm:ss");
        String lastTimeStr = dtf.format(LocalDateTime.now());
        response.addCookie(new Cookie("lastTime", lastTimeStr));
    }
}
```



###### 完 !