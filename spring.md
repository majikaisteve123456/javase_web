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

   

   在整个web系统来说，web层中，structs接管jsp/action/表单，主要体现出mvc的数据输入、数据处理、数据显示分离

   

   mvc 模式中：view：jsp 

   ​                        controller:action.java

   ​                         model(业务层+dao+持久层（主要解决关系模型和对象模型的阻抗）)

   

   配置各种bean:  web层 action

   ​                            业务层 service/domain/dao

   ​                            持久层：数据源

   

   ## 理解IOC##

   spring开发提倡接口编程，配合di技术，可以得到层与层的解耦

   举例说明

   体验spring的di配合接口编程，完成一个字母大小写的案例

   1. 创建一个接口 ChangeLetter
   2. 两个类实现接口
   3. 把对象配置到spring容器中
   4. 使用

   

   applicationConetext.xml文件的名字不一定叫这名

   还有常见的叫法叫做beans.xml

   如果xml文件不是在src目录下的话，在包下的话，路径名需要将点.转换为斜杆/

   在xml文件配置bean的时候属性 class不能为接口，必须为类

   

   使用spring   action.java 和service层之间有接口

   

   继承同一接口的类使用相同的id ,在实际的工程中使用多选一

   

   好处：业务层的内容没有发生变化，只需要改变xml文件

   使用接口来访问bean：ChangeLetter changeLetter=（ChangeLetter）ac.getBean("changeLette");

   

   ## Bean 工厂和ApplicaitonContext##

   bean工厂：最简单的容器，提供基础的依赖注入支持，创建各种类型的Bean

   应用上下文(ApplicationContext):建立在工厂的基础之上，提供系统架构服务

   

   从ApplicationContext容器中获取bean 和bean工厂获取bean的区别：

   当加载配置文件的时候，在应用上下文容中bean已经被实例化，已被创建了

   

   **bean工厂的介绍**

   工厂设计模式，创建分发各种bean,配置好他们之间的协作关系，参与bean的生命周期

   Beanfactory factory=new XmlBeanFactory(new ClassPathResource("applicationContext.xml"));

   bean工厂只把bean的定义信息加载进来，getBean用到的时候才实例化

   

   Bean作用域

   | 作用域          | 描述                                                         |
   | --------------- | ------------------------------------------------------------ |
   | singleton       | 在Spring Ioc容器中一个bean定义对应一个对象实例               |
   | prototype       | 一个bean定义对应多个对象实例                                 |
   | request         | 在一次HTTP请求中，一个bean定义对应一个实例，即每次HTTP请求都会有各自的bean实例，他们依据某个bean定义创建而成，该作用域仅在基于web的Spring ApplicationContext情形下有效 |
   | session         | 在一个HTTP Session中，一个bean定义对应一个实例，该作用域仅在基于web的Spring Application情形下有效 |
   | global  session | 在一个全局的HTTP Session中，一个bean定义对应一个实例，当容器没关闭情况bean的实例就存在 |

   

   后三个配置只有在web开发中才有意义

   

   具体案例：

   移动设备的话使用bean工厂，不能占用太多的内存

   大部分应用系统使用应用上下文

   

   结论是：如果使用ApplicationContext,则配置的bean如果是singleton不管你用不用，都被实例化（好处就是预先加载，缺点就是耗内存）

   如果是BeanFactory,则当你实例化该对象时候，配置的bean不会被马上实例化，当你使用的时候才被实例化，节约内存，缺点就是速度有点慢

   规定：一般没有特殊要求，应当使用ApplicationContext完成

   

   singleton:单例，默认值

   prototype:原型

   request:一次请求有效

   session：session级有效

   global-session:在web中spring容器ApplicationContext一样

   

   <bean id ="student"  scope="singleton"></bean>

   Student s1=(Student)  ac.getBean("student");

   Student s2=(Student)   ac.getBean("student");

   System.out.println(s1+" "+s2);

   可以得到两个对象的内存地址相同

   

   <bean id ="student"  scope="prototype"></bean>

   可以得到两个对象的内存地址不相同，每次获取都会得到全新的对象

   

   singleton和global-session是等价的，global-session 是web开发中的singleton,只要spring容器没有关闭，对象就存在

   

   使用应用上下文：

   三种经常用到的实现：

   1. ClassPathXmlApplicationContext:从类路径中加载
   2. FileSystemXmlApplicationContext:从文件系统中加载，需要写全文件的路径，路径中双斜杠\\,需要使用绝对路径，不能使用相对路径
   3. XmlWebApplicationContext：从web系统中加载，当tomcat启动的时候后才加载。

   

   

   ## bean的生命周期##

   1. 实例化（当我们的程序加载beans.xml文件），把我们的bean（前提是scope=singleton）实例到内存中，默认情况下是找无参的构造方法

   如果有多个构造方法可以在配置文件中指定构造方法 

   2. 设置属性     注入属性 前提是有方法对应 setName才能ok

   3. 调用BeanNameAware的setBeanName（）方法

      eg:

      public class personService implements BeanNameAware

      {

      ​     //该方法可以给arg0表示正在被实例化得bean

      ​      public void setBeanName(String arg0)

      ​      {

      

      

      ​         }

      }

   

   4.如果有实现bean工厂接口，则可以获取bean工厂，调用BeanFactoryAware 的setBeanFactory()方法 ,该方法可以传递beanFactory,arg0就是bean工厂

   public void setBeanFacotry(BeanFactory arg0) throws BeansException

   {

   

   }

   5.该方法传递上下文

   如果实现ApplicationContextAware 中的setApplicationContext方法，该方法可以得到ApplicationContext

   

   6.如果一个bean与一个后置处理器相关联

   调用BeanPostProcesser  bean的后置处理器

   创建自己的bean后置处理器 MyBeanPostProcessor

   public class MyBeanPostProcessor implements BeanPostProcessor

   {

   }

   需要实现两种方法  postProcessAfterInitialization

   ​                                postProcessBeforeInitialization

   

   在beans.xml 文件中进行配置后置处理器，有点类似于过滤器

   给bean配置id， class

   

   有两个方法被调用：顺序是：before（） after（） 

   **中间还有可能其他的方法** 

   理解一下后置处理器：

   每当实例化一个bean后如果配置了后置处理器，那么每次都会调用before（）、after（）

   

   需求：

   1. 记录每个对象被实例化的时间
   2. 过滤每个调用对象的ip
   3. 给所有对象添加属性，或者函数=》aop() 面向切面编程,针对所有对象编程。

   

   相当于有一道门对所有对象进行编程，这道门就是MyBeanProcessor.对一波对象编程，是门产生作用的是xml文件。

   

   

   

   如果实现了InitializingBean的afterPropertieSet()方法：则在后置处理器的before方法后面调用该方法

   如果调用定制的初始化方法则在InitializingBean中的方法使用后使用

   

   

   

   

   

   

   