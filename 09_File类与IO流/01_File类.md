## File 类

`java.io.File`

文件和目录路径名的抽象表示形式, 对**文件或目录**进行操作

构造方法:

1. `File(File parent, String child)`:  根据 parent 抽象路径名和 child 路径名称字符串创建一个新的实例
2. `File(String parent, String child)`:
3. `File(String,  pathname)`: 
4. `File(URI uri)`:

**因为 Windows 和 Linux 的路径分隔符不同, File 对象有一个静态变量用于表示当前平台的系统分割符**

`System.out.println(File.separator)`



获取功能的方法:

1. `public String getAbsolutePath()`: 返回此 File 的绝对路径

2. `public String getPath()`:  将此 File 转换为路径 (构造方法中的路径)

3. `public String getName()`:  返回由此 File 表示的文件或目录的名称

4. `public long  length`: 返回由此 File  表示的文件长度 (字节长度, Unicode, 中文占两个字节)

5. `public long lastModified()`: 返回文件的最后修改时间

6. `toString`: 

   ```java
   public String toString() {
       return getPath();
   }
   ```

**注意:** **需要在 file 对象的确实存在的情况下, 才可以看到对应的文件长度、修改时间等信息**; 否则返回 0



判断的方法: 

1. `public boolean exists()`: 判断此 File 表示的文件或路径是否存在
2. `public boolean isDirectory()`: 判断构造方法中的路径是否以目录结尾
3. `public boolean isFile()`: 判断构造方法中的路径是否以文件结尾



创建\删除

1. `public boolean createNewFile()`: 当且仅当该名称的文件不存在时, 才创建新文件 (路径错误会报错)

2. `public boolean delete()`: 删除由此 File 表示的文件或目录 (文件或目录不存在时返回 false, 当前目录必须为空才能删除成功)

   **直接在硬盘上刷数据, 不走回收站, 谨慎删除**

3. `public boolean mkdir()`: 创建由此 File 表示的目录 (父目录不存在返回 false)

4. `public boolean mkdirs()`: 递归创建





###### 完

