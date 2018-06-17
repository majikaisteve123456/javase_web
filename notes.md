<h1>xml</h1>
----
指可扩展标记型语言  
标记性语言，使用标签进行操作  
html里面的标签是固定，每个标签都有特定的含义  
xml的标签是可以自定义，标签可以写入中文  
html 主要用于显示数据，xml也可以用于显示数据（非主要功能）  
xml主要功能，为了存储数据   
xml有两个版本1.0 1.1  
使用1.0版本，1.1版本不能向下兼容  


**xml的应用**
---
<?xml version="1.0" encoding="UTF-8"?>  
1.不同的系统之间传输数据   
  传输的数据格式适应xml   
  比如： qq消息直接的传输数据
  早期的时候，使用字符串拼接  
   string str="qq1:qq2:hello"  
  程序的可维护性差，不利于程序的维护  

  现在使用的方式：
  string str="XXXX" XXXX为xml  

2.用来表示生活中有关系的数据  
     
3.经常用在配置文件    
    比如现在连接数据库，肯定知道数据的用户名和密码，数据名称    
如果需要修改数据库的信息，不需要修改源代码，只要修改配置文件就可以，源代码只需要编译一次  

<h1>xml的语法</h1>
---  
xml的文档声明   
创建文件，后缀名是.xml
如果xml,第一步必须要有个文档声明（写了文档声明之后，表示写xml文件的内容）  

<?xml version="1.0" encoding="gbk"?>   
文档声明必须写在第一行第一列 不能空格不能空行  

属性   
     -version:1.0(使用),1.1  
     -encoding:xml gdk uff-8,iso8859-1(不包含中文)  
     -standalone:xml文件是否可以独立存在，是否依赖于其他文件 yes/no
    

定义元素（标签） 

其实就是标签的定义  
标签有开始必须要有结束  
不包含标签主题，没有内容，在标签内结束<a/>  
标签可以嵌套，但是要合理嵌套  
在一个xml中只能有一个根标签   

第一段：
<网址>www.baidu.com</网址>  
第二段：  
<网址>  
&emsp; www.baidu.com  
</网址>  
解析的内容不一样
xml把空格和换行都当做空格来处理  
**xml中标签的名称规则**  
（1）xml代码区分大小写   
（2）xml的标签不能以数字和下划线（-）开头  
（3）不能以xml,XML,Xml等开头  
（4）xml标签不能包含空格和冒号  
（5）xml标签可以是中文


**定义属性**
xml可以有属性  
一个标签上可以有多个熟悉  
属性名称不同相同  
属性值可以用单引号或者双引号括起来  
属性名称和属性值之间使用=  

**xml的注释**   
xml注释的语法  
<!--注释--> 
注释不能嵌套  




特殊字符  
CDATA区（了解）  
PI指令（了解） 

xml的中文乱码问题  
保存文件时系统默认是格式是gbk 
而xml文档声明中的utf-8不一致
在保存时应该使用与文档声明一致  
当文件存储到本地硬盘是，使用gbk编码保存，存储在计算机中是以二进制形式，在gbk码表里面查找。打开xml,使用设置编码utf-8    
不出现乱码，设置保存时候的编码需要一致  




tomcat安装与运行  
web应用服务器会完成底层的网络处理，包括HTTP协议报文格式的编解码，管理具体文本请求处理线程等这些操作  
源代码用java写的，运行tomcat需要依赖java运行环境，就是需要依赖java虚拟机  
**tomcat安装**
需要配置环境变量CATALIANA_HOME(环境变量是给操作系统或应用程序设置的一些参数，这些参数可以控制操作系统或应用程序的行为，应用系统依赖这些参数才能够正常运行)     
CATALINA本身是Tomcat的一个组成部分  
CATALINA这个组件会掉调用用户的Java代码  

windows平台  使用bat脚本就是批处理  
%CATALINA_HOME%\bin\startup.bat  
%CATALINA_HOME%\bin\catalina.bat start  



**tomcat的组成**

bin:可执行文件（执行脚本），脚本执行时所依赖的jar包都放在bin目录下

conf:配置文件

lib:tomcat的依赖库，tomcat自身需要用到jar包

logs:日志，放日志文件，tomcat的活动被记录

temp:临时文件  

webapps:默认的应用部署目录  ，所写的web应用程序放这

work:供web应用使用  



JVM启动参数配置：

（1）环境变量 JAVA_OPTS  

 -server 告诉JVM 这是一个服务器应用  

 -Xms512m 调试JVM初始堆大小的参数  

 -Xmx512m 调试JVM最大堆的参数，m是兆    



windows下修改catalina.bat文件   

set JAVA_OPTS=-server -Xms1024m  -Xmx1024m   



conf 下最重要的配置文件 server.xml

Server 下可以有多个Service

Connector 用来接收用户请求

一个Service下只有一个Engine ，处理Connector所接收的请求

一个Engine可以有多个Host

Host是虚拟主机的概念，一个ip+一个端口组成一个 队为多个域名提供服务

一个Context就是一个web应用



Container由Catalina组成，根据请求生成相应的响应



Connector 参数配置：

*  port（不超过65535）
* address 













