[TOC]

xml
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

work:供web应用使用 ，tomcat生成的



tomcat可以执行对多个项目。



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
*  address 



**Web应用**

静态网站

* 在webapps目录下创建一个目录（命名必须不包含中文和空格），该目录称之为项目目录
* 在项目目录下创建一个html文件



动态网站

* 在webapps 目录下创建一个项目目录

* 在项目目录下创建如下内容

  1. WEB-INF目录

       在WEB-INF目录下创建创建web.xml文件（web.xml决定是否动静态），向其他项目借

     2. 动态或静态页面



动态页面在项目目录下加入jsp 页面，jsp页面可以加入变量



如果WEB-INF下可以建一个lib文件夹，中间放着jar包

新建一个文件夹命名为classes，放java类编译出的class文件  

网页可以分目录存储。

WEB-INF下的东西是浏览器不能访问的 ，是安全的



## 创建Java Web项目##

---

使用eclipse，创建webproject

运行仍然通过tomcat。不需要将整个eclipse中的项目放到tomcat下的webapps下

只需要将页面和编译后字节码文件放在webapps

防火墙允许应用

##JSP##

---

什么是jsp？

html+java 代码

本质就是 servlet ，画了浓妆的servlet



servlet：

缺点：不适合设置html响应体，需要使用大量的response.getWriter().print("<html>");

缺点：动态资源，可以编程



html:

缺点：html是静态页面内，不能包含动态信息

优点：本身就是html标签



jsp 和servlet的区别：

jsp:作为请求发起的页面

​     作为请求结束的页面

servlet:作为请求过程中处理数据的环节

jsp是服务员

servlet是后厨的厨师



jsp无需无需创建即可使用的对象一共有9个，被称为9大内置对象，例如request对象，out对象

3种java脚本：

<%...%>java 代码片段（常用），用于定义0-N条java语句，方法能放什么它就能放什么。

<%=...%>java表达式，用于输出，用于输出 一条表达式的结果

<%!...%> 用来创建输出类的成员和成员方法（基本不用，但容易被考到）



演示jsp中的java脚本

获取项目名

String path=request.getContextPath();

获取协议+主机名+服务端口号+项目名

String basePath=request.getScheme()+"://"+request.getServerName()+":"+request.getServerPort()+path+"/"；



在头部中使用 <base href="<%=basePath%>">

那么下body中的超链接指向的页面 都是在base下的，相当于在链接的href之前加上

<%

int a=10;

%>

 <%

  out.println(a);

%>

<%=a%>



html 的表格显示

<table border=“1”  align="center" width="60%">

​      <tr>

​             <td>姓名</td>

​             <td>年龄</td>

​    </tr>

<%  for(int i=0;i<10;i++){

%>

​      <tr>

​             <td>张三</td>

​             <td>14</td>

​    </tr>

<%}%>

</table>

JSP是JAVA Web 服务器的服务页,经过tomcat解析后生成html页面



form.jsp 

整数1:加框

整数2：加框

提交

result.jsp

结果是：



AServelet

1. 获取表单数据
2. 把字符串转换成整数
3. 进行加运算得到结果
4. 保存结果到request域中
5. 转发到result.jsp



action写上servlet的名字

<form action="/web/AServelet" method="post">

​    整数1：<input type="text" name="num1"/>

  <br/> <br/>
   整数2:<input type="text" name="num2"/>
   <br/> <br/>
   <input type="submit" value="提交">





## JSP的原理##

---

jsp 是一种特殊的Servlet

* 当jsp页面第一 次被法访问，服务器会把jsp编译成java文件（这个java其实是一个servlet类）

* 然后把java文件编译成.class

* 然后创建该类对象

* 然后调用它的service（）方法完成响应

* 第二次请求同一jsp时，直接调用service()方法

  在tomcat中的work目录下可以找到jsp对应的.java源代码  



"第一次惩罚"

abcdefg

<%

int a=100

System.out.println(a);

out.print(a);

%>

a

<%=a%>

--------

out.write(“abcdefg”);

int a=100;

System.out.println(a);

out.print(a);

out.write("a");

out.print(a);



## jsp的注释##

<%--....--%>当服务器把jsp 编译成java<u>文件时忽略</u>









## 什么是servlet##

每个servelet都是唯一，处理的请求是不同  

tomcat负责将浏览器的请求发送给不同的servlet  

异步



接收请求数据

处理请求

完成响应



每个Servlet必须实现javax.servlet.Servlet接口



## 实现Servlet的方式

1. 实现javax.servlet.
2. 继承javax.servlet.GenericServlet
3. 继承javax.servlet.http.HttpServlet



Servlet接口（IDE中可以帮助添加）

方法有tomcat来调用，并且对象不由我们来创建

声明周期方法(有tomcat来调用)：

destroy（）在销毁之前调用，只会调用一次

init() 在Servlet对象创建之后马上执行，并只执行一次（出生之后）

service()会被调用多次,每一次访问都会使用



getServletConfig() 获取配置信息

getServletInfo() 获取Servlet信息 自己调用，没用



void init(ServletConfig):出生之后

void service(ServiceRequest request,ServiceResponse  response)

void destroy():临时之前



单例，一个类只有一个对象，当然可能存在多个Servlet类

线程不安全的，所以效率是高的



Servlet类由我们来写，但独享有服务器来创建，并且有服务器来调用响应的方法。



## 浏览器访问Servlet##

1. 给Servlet指定一个Servlet路径（让Servlet与一个路径绑定在一起）
2. 浏览器访问Servlet路径

给Servlet 配置路径：需要在web.xml对Servlet进行配置

xxx 是给servlet取的名字



web.xml

<?xml version="1.0" encoding="UTF-8"?>
<web-app version="2.5" xmlns="http://java.sun.com/xml/ns/javaee"  
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  
    xsi:schemaLocation="http://java.sun.com/xml/ns/javaee   
    http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd">  

<servlet>
<servlet-name>XXX</servlet-name>
<servlet-class>comxidian.fengbushi.AServlet</servlet-class>
</servlet>

   <servlet-mapping>
      <servlet-name>XXX</servlet-name>
      <url-pattern>/AServlet</url-pattern>
   </servlet-mapping>

</web-app> 



servlet是单例执行



## Cookie##

会话跟踪技术，客户端对服务器的多次访问，一连贯访问 。

服务器保存到客户端

由服务器创建  

* Cookie 是HTTP协议制定的：先由服务器保存到Cookie.在下次浏览器请求是服务器把上一次请求到的Cookie再归还给服务器。（不是java独有的）

* 由服务器创建保存到客户端的一个键值对，服务器保存到Cookie的响应头

  repsonse.addHeader("Set-Cookie","aaa-AAA");

  值也是一个键值对

* 当浏览器请求服务器时，浏览器归还给服务器请求头 Cookie: aaa=AAA;bbb=BBB



一个Cookie最大4KB（一些浏览器会违反）

1个服务器最多向1个浏览器保存20个cookie(浏览器保存的Cookie最终是保存到硬盘上的，另外数量太多，归还给服务器时处理的数量太多)

1个浏览器最多可以保存300个Cookie(大部分的违反)



Cookie的用途：

* 服务器使用Cookie来跟踪客户端状态。
* 显示上次登录名



便捷方式：

服务器向浏览器保存Cookie:       response.addCookie()  需要提供一个Cookie类

获取浏览器归还的Cookie:            request.getCookies()   得到的是一个Cookie数组，得到后需要判断是否是null



Cookie是不能够跨浏览器的

在jsp中

Cookie cookie=new Cookie("aaa","AAA");

response.addCookie(cookie);



获取Cookie对象

Cookie[] cooikes=request.getCookie();

if(cookies!=null)

{

  for(Cookie c:cookies)

{

   out.print(c.getName()+"="+c.getValue()+<br/>;);

}

}



除了写在jsp中的Cookie 外还有tomcat也会发送Cookie 



## Cookie的生命周期##

Cookie不只有name 和value 两个属性

maxAge:Cookie的最大生命周期，即Cookie可保存的最大时长，以秒为单位，例如，cookie。setMaxAge(60)  如果不设置这个值，那么一般默认为关掉浏览器，释放掉进程所占用的内存，那么Cookie就不存在，但是如果设置最大生命周期，那么将放置在浏览器主机上的主机硬盘上



maxAge>0 浏览器会把Cookie保存到客户端硬盘上，即Cookie可保存的最大时长，以秒为单位

maxAge<0 只在浏览器的内存中存在，当用户关闭浏览器是，浏览器进程结束，同时Cookie也就死亡

maxAge=0 浏览器会马上删除这个Cookie，通过设置为0 ,将同名cookie删除掉



## JSP页面之间##

页面之间进行通信：

由于HTTP是无状态的，web页面无法向下一个页面传递信息

1. URL传值































 





















