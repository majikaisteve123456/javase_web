##使用Maven##

Maven 的主要作用：

* 统一开发规范与工具
* 统一管理jar包



使用Maven 构建的普通Java项目，对源代码、单元测试代码，资源乃至后续需要的问题都有专门的目录规划，使用maven，那么项目的目录结构必须符合Maven 的规范



Maven 的基本命令：

mvn -v   查询Maven版本

compile  将java源文件编译成class文件

test：执行test目录下的测试用例

package：将项目打包成jar包

clean：删除target文件夹

install：将当前项目放到Maven的本地仓库，供其他项目使用



本地仓库：Maven本地的Jar包仓库

中央仓库：Maven 官方提供的远程从仓库

当项目编译的时候，Maven首先从本地仓库寻找项目的jar包，若本地仓库没有，再到中央仓库中下载所需要的jar包



“坐标”是在maven 中的唯一标识，Maven通过坐标在仓库中找到项目

<dependency>

​     <groupId>xxxx </groupId>

​    <artifactId> xxxx </artifactId>

​      <version> xxxx </version>

</dependency>



pom.xml 这是maven的核心配置文件，用来描述maven项目

groupId 公司名和组织名，项目用途+公司名+项目名

artifactId 项目名



**Maven的目录结构：**

main目录下是项目的主要代码，test目录下存放测试相关的代码

编译输出后的代码会放在target目录下

src/main/java存放java代码，src/main/resources下存放配置文件

pom.xml是Maven项目的配置文件







**传递依赖和排除依赖**

**传递依赖** ：项目需要引用一个jar包，该jar包又引用另外一个jar包，那么默认情况下项目编译的时候，maven会直接引用和简洁的jar包都下载到本地

排除依赖：如果只想下载直接引用的jar包，那么需要在pom.xml中做如下配置

<exclusions>









## Spring的java配置方式##

java配置是spring4.x推荐的配置方式，可以完全替代xml配置

spring的java配置是通过@Configuration 和 @ Bean

1. @Configuration 作用于类上相当于xml配置文件
2. @Bean作用于方法上，相当于<bean>



使用eclipse创建 spring boot项目

直接new就行，不需要先创建maven项目



使用数据库连接池：

将实现网络协议的通信库称为数据库驱动程序，对于不同语言需要编写不同的数据库驱动程序，通过TCP与数据库建立连接是非常耗时的，TCP建立连接要三次握手，断开需要四次握手，使用连接池的方式。应用程序需要更低的响应时间，如果每次数据库都需要经过建立连接-通信-断开连接这个过程，那么势必导致响应延时的增加。避免数据库服务器的资源被耗尽。



当创建maven项目出现报错可以先清空用户目录下.m2本地仓库中的jar包，然后右击项目-》maven-》maven update



实例：通过java配置的方式进行配置spring，并实现spring IOC功能

在Service层中使用Dao组将，需要注入Spring容器中的对象。



package cn.itcast.springboot.javaconfig;

import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

@Service
public class userService {

	@Autowired
	private userDao dao;
	public List<user> queryUserList()
	{
		return dao.queryUserList();
	}
}



编写SpringConfig 用于实例化Spring容器

package cn.itcast.springboot.javaconfig;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;

@Configuration
@ComponentScan(basePackages="cn.itcast.springboot.javaconfig")//配置扫描包
public class springConfig {

	@Bean
	public userDao getuserDao()
	{
		return new userDao();
	}

}

编写main方法：

package cn.itcast.springboot.javaconfig;

import java.util.List;

import org.springframework.context.annotation.AnnotationConfigApplicationContext;

public class Main {
   public static void main(String[] args)
   {
	   
	   AnnotationConfigApplicationContext context=new AnnotationConfigApplicationContext(springConfig.class);
	   userService userservice=context.getBean(userService.class);
	   List<user> list=userservice.queryUserList();
	   for(user p:list)
	   {
		   System.out.println(p.getUsername()+p.getPassword()+p.getAge());
	   }
	   context.destroy();


​	   
​	   
   }
	
}



SpringBoot 的常用注解

@Service :用来标注业务层组件

@Autowired: 注入spring 容器中的bean对象

@Configuration：指出配置的信息源，相当于XML文件

@ComponentScan:组件扫描



## 读取外部的配置文件##

通过@PropertySource 可以指定读取的配置文件，通过@Value注解获取值

@PropertySource(value={"classpath:jdvc.properties"})

如果需要配置多个外部配置文件

则

@PropertySource(value={"classpath:jdvc.properties"，“xxxxx”,"xxxxx"})



@Value{"${jdbc.url}"}

private String jdbcUrl；



如果配置文件不存在

@PropertySource(value={"classpath:jdvc.properties"}，ignoreResourceNotFound=true)



写一个数据库连接池

@Value("${jdbc.driverClassName}")

private String driverClassName;

@Value("${jdbc.url}")

private String jdbcUrl;

@Value("$jdbc.username")

private String jdbcUsername;

@Value("$jdbc.password")

private String  jdbcPassword;



@Bean(destroyMethod="close")

public BoneCPDataSource boneCPDataSource(){

   BoneCPDataSource boneCPDataSource=new BoneCPDataSource();

   boneCPDataSource.setDriverClass(jdbcDriverClassName);

   boneCPDataSource.setJdbcUrl(jdbcUrl);

​    boneCPDataSource.setUsername(jdbcUsername);  

}

## Spring Boot##

java是静态语言，先编译后运行

**快速入门**

springboot 需要设定parent，设置spring boot 的parent

<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>2.0.4.RELEASE</version>
		<relativePath/> <!-- lookup parent from repository -->
	</parent>



spring boot的项目必须要将parent设置为spring boot的parent，该parent包含了大量的默认的配置，简化我们的开发



导入spring boot的web支持

​            <dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>



## 第一个SpringBoot 应用##

package com.example.demo;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.annotation.Configuration;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;

@Controller
@SpringBootApplication
@Configuration
public class HelloApplication {
                   @RequestMapping("hello")
		   @ResponseBody
		   public String hello()
		   {
			   return  "hello word";
		   }
   public static void main(String[] args)
   {
	   SpringApplication.run(HelloApplication.class,args);
   }
		  	
}

@responseBody注解的作用是将controller的方法返回的对象通过适当的转换器转换为指定的格式之后，写入到response对象的body区，通常用来返回JSON数据或者是XML 

@SpringBootApplication :SpringBoot项目的核心注解，主要目的是开启自动配置

@Configuration: 只是配置Spring的配置类



启动应用：

1. 直接run java Applica同
2. 通过Spring Boot的Maven 插件



当运行的时候，默认配置tomcat，servlet

当运行项目的时候，在浏览器的地址栏中输入127.0.0.1:8080/hello



**@RequestMapping的注解的使用**

将HTTP请求映射到控制器的处理方法上

@RestController
@RequestMapping("/home")
public class IndexController {
    @RequestMapping("/")
    String get() {
        //mapped to hostname:port/home/
        return "Hello from get";
    }
    @RequestMapping("/index")
    String index() {
        //mapped to hostname:port/home/index/
        return "Hello from index";
    }
}



可以将多个请求映射到一个方法上去，只需要添加一个带有请求路径值列表的 @RequestMapping 注解就行了。  

@RestController
@RequestMapping("/home")
public class IndexController {

    @RequestMapping(value = {
        "",
        "/page",
        "page*",
        "view/*,**/msg"
    })
    String indexMultipleMapping() {
        return "Hello from index multiple mapping.";
    }
}

如你在这段代码中所看到的，@RequestMapping 支持统配符以及ANT风格的路径。前面这段代码中，如下的这些 URL 都会由 indexMultipleMapping() 来处理： 

 

- localhost:8080/home
- localhost:8080/home/
- localhost:8080/home/page
- localhost:8080/home/pageabc
- localhost:8080/home/view/
- localhost:8080/home/view/view



**带有 @RequestParam 的 @RequestMapping**

 

 

 

@RequestParam 注解配合 @RequestMapping 一起使用，可以将请求的参数同处理方法的参数绑定在一起。 

@RequestParam 注解使用的时候可以有一个值，也可以没有值。这个值指定了需要被映射到处理方法参数的请求参数, 代码如下所示： 

代码 

1. @RestController  
2. @RequestMapping("/home")  
3. public class IndexController {  
4.   
5. ​    @RequestMapping(value = "/id")  
6. ​    String getIdByValue(@RequestParam("id") String personId) {  
7. ​        System.out.println("ID is " + personId);  
8. ​        return "Get ID from query string of URL with value element";  
9. ​    }  
10. ​    @RequestMapping(value = "/personId")  
11. ​    String getId(@RequestParam String personId) {  
12. ​        System.out.println("ID is " + personId);  
13. ​        return "Get ID from query string of URL without value element";  
14. ​    }  
15. }  

在代码的第6行，id 这个请求参数被映射到了 thegetIdByValue() 这个处理方法的参数 personId 上。

如果请求参数和处理方法参数的名称一样的话，@RequestParam 注解的 value 这个参数就可省掉了, 如代码的第11行所示。 

 

@RequestParam 注解的 required 这个参数定义了参数值是否是必须要传的。 

 

代码 

1. @RestController  
2. @RequestMapping("/home")  
3. public class IndexController {  
4. ​    @RequestMapping(value = "/name")  
5. ​    String getName(@RequestParam(value = "person", required = false) String personName) {  
6. ​        return "Required element of request param";  
7. ​    }  
8. }  

在这段代码中，因为 required 被指定为 false，所以 getName() 处理方法对于如下两个 URL 都会进行处理： 

- /home/name?person=xyz
- /home/name



## Spring Boot的核心##

入口类和@SpringBootApplication

项目有一个入口类，入口有一个main方法

@SpringBootApplication 是个组合注解

在SpringBoot 项目中推荐使用@SpringBootApplication来替代@Configuration

中间有 @EnableAutoConfiguration :启动自动配置，该注解使Spring Boot根据项目中依赖的jar包自动配置项目的配置项

@ComponentScan：默认扫描@SpringBootApplication 所在类的同级目录以及子目录



SpringBoot会自动配置，但是如果我们不需要SpringBoot自动配置，想关闭某一项的自动配置

@SpringBootApplication(exclude={RedisAuotConfiguration.class})





## 全局配置文件##

Spring Boot 项目使用一个全局配置文件application.properties,在resource下

1. 修改tomcat的端口为8088

   server.port=8088

   2.修改进入DispatcherServlet的规则为*.html

   server.servlet-path=*.html



## SpringBoot的自动配置##

Spring Boot 在进行SpringApplication对象实例化时会加载META-INF/spring.factories文件，将配置文件中的配置载入到Spring容器中



## Spring Boot的web 开发##

条件注解表明类初始化的条件

静态资源放在resource目录下

在全局配置文件中加上

spring.resource.static-location=classpath:/public/

指定静态资源的访问路径



**自定义消息转化器**

消息转化器@RequestBody 、@ResponseBody注解可以将输入解析成json,将输出解析成Json,li浏览器和服务器通过原始文本进行通信，这里是消息转换器发挥着作用

只需要在@Configuration的类中添加消息转化器的@bean加入到Spring容器

@Bean

public StringHttpMessageConverter stringHttpMessageConverter()

{

​    StringHttpMessageConverter converter=new      StringHttpMessageConverter(Charset.forName("UTF-8"))；

return converter；

}



springboot自动配置的utf-8的消息转换器，可以不用，如果自定义，则spring boot自定义的对象将不会实例化

所以在view层可以显示中文，没有乱码



**添加拦截器**

https://blog.csdn.net/htf2620032/article/details/79305208



## spring boot 项目

Spring Boot 没有web.xml

数据源写在*Application类中

设置Mybatis和Spring Boot整合

官方提供整合包

使用mybatis-spring整合方式



采用第二种方便后续修改

创建一个配置类 MyBatisConfig



@Configuration

public class MyBatisConfig

{

@AutoWired

   private  DataSource dataSource;



@Bean

public SqlSessionFactoryBean sqlSessionFactoryBean()

{

​      SqlSessionFactoryBean sqlSessionFactoryBean=new  SqlSessionFactoryBean();

​     sqlSessionFactoryBean.setDataSource(dataSource);

​     return sqlSessionFactoryBean;

}

}



创建Mapper接口的扫描类MapperScannerConfig

@Configuration

@AutoConfigurationAfter(MyBatisConfig.class)//保证MyBatisConfig实例化之后再实例化该类

public class MapperScannerConfi{





}













