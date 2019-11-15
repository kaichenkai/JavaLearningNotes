## File 类

`java.io.File`

文件和目录路径名的抽象表示形式, 对文件或目录进行操作

构造方法:

1. `File(File parent, String child)`:  根据 parent 抽象路径名和 child 路径名称字符串创建一个新的实例
2. `File(String parent, String child)`:
3. `File(String,  pathname)`: 
4. `File(URI uri)`:



获取功能的方法:

1. `public String getAbsolutePath()`: 返回此 File 的绝对路径

2. `public String getPath()`:  将此 File 转换为路径 (构造方法中的路径)

3. `public String getName()`:  返回由此 File 表示的文件或目录的名称

4. `public long  length`: 返回由此 File  表示的文件长度 (字节长度, Unicode, 中文占两个字节)

5. `toString`: 

   ```java
   public String toString() {
       return getPath();
   }
   ```



判断的方法: 

1. `public boolean exists()`: 判断此 File 表示的文件或路径是否存在
2. `public boolean isDirectory()`: 判断构造方法中的路径是否以目录结尾
3. `public boolean isFile()`: 判断构造方法中的路径是否以文件结尾



创建\删除

1. `public boolean createNewFile()`: 当且仅当该名称的文件不存在时, 才创建新文件 (路径错误会报错)

2. `public boolean delete()`: 删除由此 File 表示的文件或目录 (文件或目录不存在时返回 false)

   **直接在硬盘上刷数据, 不走回收站, 谨慎删除**

3. `public boolean mkdir()`: 创建由此 File 表示的目录 (父目录不存在返回 false)

4. `public boolean mkdirs()`: 递归创建