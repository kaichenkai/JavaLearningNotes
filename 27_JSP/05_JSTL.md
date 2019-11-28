## JSTL

JSTL : jsp 标准标签库 ( JavaServer Pages Tag Library )

由 Apache 基金会提供的开源的免费的 jsp 标签



##### 作用

用于简化和替换 jsp 页面上的 java 代码

> 一般用于在 jsp 页面辅助 EL 表达式进行数据的展示,
>
> 例如: if 判断, swith 判断, for 循环,  foreach 循环



##### 使用步骤

1. 导入 JSTL 相关的包: 

   `javax.servlet.jsp.jstl.jar` 和 `jstl-impl.jar`

2. 引入标签库 : 

   `<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>`

3. 使用标签



##### 常用的 JSTL 标签

1. if else

   test 是必须的属性, 填写条件, 如果条件满足, 则显示标签体内容, 否则不显示. (一般结合EL表达式一起使用)

   if 标签没有 else 情况, 可以定义多个 c:if 标签以达到 if else 的效果.

   ```jsp
   <%@ page contentType="text/html;charset=UTF-8" language="java" %>
   <%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
   <html>
   <head>
       <title>if else 判断语句</title>
   </head>
   <body>
       <%
           request.setAttribute("a", 1);
       %>
       <c:if test="true">
           is ture
       </c:if>
   
       <br>
   
       <c:if test="${a  == 1}">
           is 1
       </c:if>
   
       <c:if test="${not empty list}">
           遍历集合...
       </c:if>
   </body>
   </html>
   ```

   

2. choose ( swith )

   ```jsp
   <%@ page contentType="text/html;charset=UTF-8" language="java" %>
   <%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
   <html>
   <head>
       <title>choose</title>
   </head>
   <body>
       <%
           request.setAttribute("number", 8);
       %>
   
       <c:choose>
           <c:when test="${number==1}">星期一</c:when>
           <c:when test="${number==2}">星期二</c:when>
           <c:when test="${number==3}">星期三</c:when>
           <c:when test="${number==4}">星期四</c:when>
           <c:when test="${number==5}">星期五</c:when>
           <c:when test="${number==6}">星期六</c:when>
           <c:when test="${number==7}">星期七</c:when>
           <c:otherwise>数字输入有误</c:otherwise>
       </c:choose>
   </body>
   </html>
   ```

   

3. forEach ( 常用, 完成数据的遍历 )

   1. 一般 for 循环的属性:

      1. begin : 开始值

      2. end : 结束值

      3. var : 临时变量

      4. step : 步长 , 1 (i = i+1) , 2 (i = i+2)

      5. varStatus : 循环状态对象, 可以获取 index(索引) 和 count(当前循环次数)

         index 和 count 的区别是 : index 从 0 开始, count 从 1 开始, index 更为通用.

      

   2. 遍历容器 ( foreach ) 的属性:

      1. items : 容器对象
      2. var : 临时变量
      3. varStatus : 循环状态对象, 可以获取 index(索引) 和 count(当前循环次数)

   ```jsp
   <%@ page import="java.util.ArrayList" %>
   <%@ page import="java.util.List" %>
   <%@ page contentType="text/html;charset=UTF-8" language="java" %>
   <%@taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
   <html>
   <head>
       <title>forEach 语句</title>
   </head>
   <body>
       <%--for 循环--%>
       <c:forEach begin="0" end="10" var="i" step="2" varStatus="s">
           ${i} ${s.index} ${s.count}
           <br>
       </c:forEach>
       <br>
   
       <%
           List list = new ArrayList<String>();
           list.add("johny");
           list.add("anson");
           list.add("skier");
           request.setAttribute("list", list);
       %>
       <%--遍历 List 集合--%>
       <c:forEach items="${list}" var="name" varStatus="s">
           ${name} ${s.index} ${s.count}
           <br>
       </c:forEach>
   </body>
   </html>
   ```






###### 完 !

