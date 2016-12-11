# 乱码问题

重要提示：如果你遇到的是代码第一行提示非法字符 65279   那么   
这是因为你的文件头有BOM码，至于什么是BOM码自行百度   
请用notepad++一类工具去除即可  

关于gradle编译乱码主要是由于 编译使用的字符集编码与代码文件使用的字符集编码不一致   
 
安装系统之后，一般中文系统默认字符集是GBK。我们安装的软件一般都继承使用操作系统的默认字符集。  

# 解决方法

方法1-3: [garbled.gradle](https://github.com/benjaminwhx/gradle-example/blob/master/02-garbled/garbled.gradle)
方法4: [gradle.properties](https://github.com/benjaminwhx/gradle-example/blob/master/02-garbled/gradle.properties)