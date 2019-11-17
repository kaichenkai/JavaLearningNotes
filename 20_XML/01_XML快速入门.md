## XML快速入门

xml: Extensible Markup Language (可扩展标记语言)

**可扩展: 标签都是自定义**

功能: 存储数据 (配置文件, 网络传输等)



xml 与 html 的区别: 

1. xml 标签都是自定义, html 标签是预定义.
2. xml 语法非常严格, html 语法松散.
3. xml 是存储数据 ( 常用于配置文件, 比 properties 可扩展性, 易读性更高 ), html 是展示数据.



基本语法: 

1. xml 文档的后缀  .xml

2. xml 第一行必须定义为文档声明 (第一行不能空行)

3. xml 文档中有且仅有一个跟标签

4. 属性值必须使用引号引起来 (单双都行)

5. xml 标签名称区分大小写

   ```xml
   <?xml version="1.0" encoding="utf-8" ?>
   <users>
       <user id="1">
           <name>johny</name>
           <age>12</age>
           <hobby>badminton</hobby>
       </user>
       <user id="2">
           <name>anson</name>
           <age>10</age>
           <hobby>badminton</hobby>
       </user>
   </users>
   ```

   

组成部分: 

1. 文档声明:

   + 格式: <? xml 属性列表 >

     + version: 版本号

     + encoding: 编码方式 ( 编码方式必须和文件当前的编码方式一致 )

     + standalong: 是否独立 ( yes: 不依赖其它文件, no: 依赖其它文件)  ( 了解 )

       

2. 指令: 

   + 结合 css 的 ( 了解 )

   

3. 标签:

   + 规则 (注意下就好 ):

     + 名称由字母, 数字与其它字符组成.
     + 不能以数字或者符号开头.
     + 不能以 xml, XML 等字母开头.
     + 不能包含空格

     

4. 文本: 

   + CDATA区: 在区域中的数据会被原样展示

     格式: `<![CDATA[ 需要展示的数据 ]]>`



###### 完 ! 





