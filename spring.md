# spring框架#

## MVC思想##

model1 -->model2 

在model1的模式下来了，整个web应用全部是JSP页面组成，JSP页面接收处理客户端请求，对请求处理后直接作出响应。

使用的少量的javabean来处理数据库连接、数据库访问等操作。

局限性：JSP页面身兼View和Controller两种角色，讲稿控制逻辑和表现逻辑混杂在一起，从而导致代码的重用性降低。



model2：基于MVC架构的设计模式，servlet作为前端控制器，负责接收客户端的请求，只包含控制逻辑和简单的前端处理，然后调用后端的javabean来完成实际的逻辑处理，将其转发到相应的jsp处理显示逻辑。



model2具有组件化的特点



## spring boot 入门##

spring是什么？

struts是web框架（jsp/aciton/actionform）

hibernate是orm框架  对象关系映射框架 处于持久层

spring 是框架，容器框架，用于配置bean并维护bean之间关系的框架

bean 是java中的任何一种对象 javabean/servlet/action/数据源/dao 

ioc 控制反转 

di 依赖注入



spring 层次图

| login.jsp        Action.java   ActionForm.java    ok.jsp     |
| ------------------------------------------------------------ |
| UserService.java(业务层)   Users.java[domain对象、javabean、pojo]    web层 struct |
| dao(Userdao/HibernateUtil.java)                              |
| hibernate(orm 框架) 持久层                                   |
| 数据库                                                       |

 spring横跨除了数据库外的所有层，可以管理web层、业务层、dao层、持久层，不需要用new，该框架可以配置各个层的组件（bean）并且维护各个bean之间的关系



快速入门 

开发一个spring项目

1. 需要引入spring的开发包（最小配置spring.jar 该包把常用的jar都包括了，还要写日志包common-logging.jar）

    需要创建一个lib文件夹，将jar包放入其中，build路径

   下载spring开发插件和开发包

2.创建spring的一个核心文件 applicationContext.xml

   该文件一般都放在 src目录下，该文件中引入xsd文件

可以从给出的案例中拷贝一份

3.配置bean   在容器文件中配置bean(service/dao/domain/action/数据源)

bean标签的作用是spring框架加载的时候，spring就会自动创建一个bean ，相当于使用new操作

<bean id="userService" class=“com.service.UserService”>

​     <property name="name">

​                    <value>韩顺平</value>

​      </proprerty>

</bean>

id号相当于生成对象的对象名

UserService userService =new UserService();

userService.setName("韩顺平")

set方法必须给否则无法将bean注入



在eclipse 平台上开发spring 项目

spring tool suite是一个eclipse插件，利用该插件可以方便在eclipse平台上开发基于spring的应用

安装插件

重启之后在window中preference 中能找到spring就说明安装成功。

创建项目

为项目木添加jar包 一共需要5个文件：

commons-logging.jar

spring-beans.jar

spring -context.jar

spring-core.jar

spring-expression.jar

(现在spring旨在引导大家使用Maven方式来管理jar包)

在src目录下创建applicationConetext 文件 创建applicationContext.xml 文件



写测试函数

注意引包

 ApplicationContext ac=new ClassPathXmlApplicationContext("applicationContext.xml");
	    hello hello=(hello)ac.getBean("helloworld");
	    hello.sayHello();



getBean中是xml文件的id,注意不要写错



使用spring来完成任务：

1. 得到spring的applicationContext对象（容器对象）

   ApplicationContext ac=new ClassPathXmlApplicationContext("applicationContext.xml");

​     UserService us=ac.getBean("userService");//可以取出对象

​     us.sayHello();

将属性的值



**什么是ioc  什么是di**

---

传统的方法和使用spring的方法

1. 使用spring,没有new对象，我们把创建对象的任务交给了spring 框架  bean的id必须是唯一的

   从ac(代表applicationContext容器中)得到bean需要使用强制转换

   ac.getBean("");

   

   对于在eclipse中对属性自动生成set get方法

   source >> generate setters and getters 

   

   维护bean 与bean 的关系：如果在一个bean中使用另外一个bean的方法，如果没有配置的话会直接报错，需要进行配置，否则没有注入

   配置文件中加入

   <property  name="byeService" ref="byeService"/>

   byeService  是属性

   byeService 是另外一个配置的bean

   

   2. spring框架原理图（spring框架什么时候被加载，spring中配置的bean怎样被创建，bean与bean之间的关系怎样被维护）

   ApplicationContext ac=new ClassPathXmlApplicationContext("applicationContext.xml");

   执行的似乎，我们的spring容器被创建，同时applicationContext.xml配置，bean就会被创建（内存），java反射机制,结构类似HashMap

   内存

   id                   对象

   userService   UserService[name,byeService]

   byeService     ByService[name]

   

   ac.getBean("");

   

   深入了解反射机制：dom4j+java 反射机制

   dom4j 是一个java的Xml api ，用来读写XML文件

   userService=Class.forName("com.service.UserService");

   userService.setName("韩顺平")；

   

   bybService=Class.forName("com.service.BybService");

   bybService.setName("小明")；

   userService.setByeService(bybService);

   applicationContext=new HashMap();

   applicationContext.put("userService",userService);

   applicationContext.put("byeService",bybService);

   

   3. ioc 和 di的定义

      对上面案例总结：

      spring是容器框架，可以配置各种bean（各个层）,并且可以维护各种bean与bean之间的关系，当我们需要使用某个bean的时候，可以getBean(id) 使用即可

   

   **IOC是什么**

   答：inverse of control 控制反转 ，所谓控制反转就是将创建对象任务和维护对象之间关系的权利从程序中转移到spring容器中（applicationContext.xml），而程序本身不在维护

   反转指的是控制权交给spring容器中

   

   学框架就是在学习配置

   

   **di是什么**

   答：dependency injection 依赖注入  实际上IOC和di 是同一个概念 

   

   ## applicationContext只能有一个,做成单例，做成一个工具类##

   final public class ApplicationContextUtil

   {

      private static ApplicationContext ac=null;

   ​    private ApplicationContextUtil(){

   ​      

   }

   static

   {

   ​    ac=new ClassPathXmlApplication("application.xml");

   }

   public static AppliationContext getApplication()

   {

   ​    return ac;

   }

   

   

   

   }

   

   

   

   

   

   

   

   