---
title: Spring学习(一)
date: 2017-09-05 23:12:05
tags: [Spring,JavaWeb]
---
## 如何学习
  * 掌握用法、
  * 深入理解、
  * 不断实践、
  * 反复总结、
  * 再次深入理解与实践

  学习资源：

  [Spring.io](http://spring.io/)

  [spring-framework](http://projects.spring.io/spring-framework)

## Spring简介(对象的容器)
  Spring是一个开源框架，为了解决企业应用开发的复杂性而创建的，但现在已经不只应用于企业应用。
  是一个轻量级的控制反转（IoC）和面向切面（AOP）的容器框架。
  * 从大小与开销两方面而言Spring都是轻量型的
  * 通过控制反转（IoC）的技术达到松耦合的目的
  * 提供了面向切面编程的丰富支持，允许通过分离应用的业务逻辑与系统及服务进行内聚性的开发。
  * 包含并管理应用对象的配置和生命周期，这个意义上是一种容器。
  * 将煎蛋的组件配置，组合成为复杂的应用，这个意义上是框架。

### 在Spring上开发
      简单、方便、快捷

### Spring作用（负责管理项目中的所有对象）
* 一站式框架（正是因为spring框架性质是属于容器性质的，容器中装什么对象就有什么功能）
* 看做是项目中对象的管家
* 不仅不排斥其他框架，还能帮助其他框架管理对象
* aop支持
* ioc思想
* spring jdbc
* aop事物
* junit测试支持

### 框架
#### 什么是（软件）框架
简单来说，框架就是制定一套规范或者规则，是用别人的舞台表演。
#### 框架的特点
* 半成品
* 封装了特定的处理流程和控制逻辑
* 成熟的，不断升级改进的软件

#### 框架和类库的区别
* 框架一般是封装了逻辑、高内聚的，类库则是松散的工具组合
* 框架专注于某一领域，库类则是更通用的。

#### 为什么使用（软件）框架
* 软件系统日趋复杂
* 重用度高，开发效率和质量提高
* 软件设计人员要专注于对领域的了解，使需求分析更充分。

## spring搭建

### 导包&创建一个对象
使用spring要导入的最基础的包：
* Beans
* Core
* Context
* Expression
还有日志包org.apach.commots.logging.jar

### 约束引入
新建一个xml文件（位置任意（建议放到src下），配置文件名任意（建议applicationContext））
XML Catalog中，导入约束schema/beans

key type更改为 Schema location

在xml文件中写入根元素<beans></beans>，然后切换到设计视图（Design）

右键beans,更改命名空间
### 注册对象到容器&测试
#### 将User对象交给spring容器管理
``<bean name = "user" class = "com.bean.User"></bean>``
#### 测试
* 创建容器对象

``ApplicationContext ac  = new ClassPathXmlApplicationContext("applicationContext.xml");``
* 向容器“要”user对象

``User u  = (User) ac.getBean("user");``
* 打印user对象

``System.out.println(u);``
## Spring概念
### 思想

#### 什么是IOC(Inverse Of Control)
将我们创建对象的方式反转了，以前对象的创建是由我们开发人员自己维护，包括依赖关系也是自己注入。

使用了spring之后，对象的创建以及依赖关系可以由spring完成创建以及注入。

反转控制就是反转了对象的创建方式，从我们自己创建反转给了程序（Spring）。

> 控制反转，控制权的转移，需要对象时，申请一个对象。

> 获得依赖对象的过程被反转。

#### DI（Dependency Injection依赖注入）
需要IOC的环境，是实现IOC思想的方式(技术)。

注入方式：
* set方法注入
* 构造方法注入
* 字段注入（不推荐）

注入类型：
* 值类注入 #八大基本数据类型
* 引用类注入 #将依赖对象注入


目的：创建对象并且组装对象之间的关系。
### applicationContext&BeanFactory
#### BeanFactory借口
* spring原始接口，针对原始接口的实现类功能较为单一
* BeanFactory借口实现类的容器，特点是每次在获得对象时才会创建对象

#### ApplicationContext
* 每次容器启动时创建容器中配制的所有对象。提供给更多功能
* 从类路径下加载配置文件：ClassPathXmlApplicationContext
* 从硬盘绝对路径下架在配置文件：FileSystemXmlApplicationContext("d://xxx/xxx")

结论：web开发中使用applicationContext,在资源匮乏的环境可以使用BeanFactory。

## spring配置详解
### Bean元素
使用该元素描述需要spring容器管理的对象
* class属性：被管理对象的完整类名。
* name属性：给呗管理的对象起个名字，获得对象是根据该名称获得对象。
> 可以重复，可以使用特殊字符
* id属性：与name属性相同，
> 名称不能重复，不能使用特殊字符。

  结论：尽量使用name属性

### spring创建对象的三种方式
* 创建方式1：空参构造创建
* 创建方式2：静态工厂（了解）
* 创建方式3：实例工厂（了解）

### Bean元素进阶

#### scope属性
* singleton(默认值)：单例对象，被表示为单例的对象，在spring容器中只会存在一个实例。
* prototype（多例原型）：被标志为多例子的对象，每次在获得时才会创建，每次创建都是新的对象。
整合struts2时，ActionBean必须配置为多例的。
* request(了解)：web环境下，对象与request生命周期一致
* session（了解）：web环境下，对象与session生命周期一致

#### 生命周期属性（了解）
* init-method（配置一个方法作为生命周期初始化方法，spring会在对象创建之后立即调用）
* destroy-method（配置一个方法作为生命周期的销毁方法，spring容器在关闭并销毁所有容器中的对象之前调用）

### spring的分模块配置
导入其他spring配置文件
``<import resource=""/>``

## spring属性注入
### 注入方式
#### set方法注入（重点）
set方式注入：
``<bean name = "user" class = "com.bean.User">``
> 值类型注入：为User对象中名为name的属性注入tom为值

``<property name = "name" value="tom"></property>``

``<property name = "age" value="18"></property>``
> 引用类型注入：为car属性注入下方配置的car对象

``<property name = "car" ref="car"></property>``

``</bean>``
> 将car对象配置到容器中

``<bean name = "car" class = "com.bean.Car">``

``<property name = "name" value="兰博基尼"></property>``

``<property name = "color" value="黄色"></property>``

``</bean>``
#### 构造方法注入
> 构造函数注入

``<bean name = "user" class="com.bean.User">``

若指定构造函数中name在前，car在后，则设置index属性为0；
若构造函数有多个，有构造函数中name的值为integer，应设置type属性为某数据类型完整类名。
> name属性：构造函数的参数名

> index属性：构造函数的参数索引

> type属性：构造函数的参数类型

``<construct-arg name ="name" index="0" type =“java.lang.String” value="jerry" ></construct-arg>``

``<construct-arg name ="car" ref="car" inedx="1"></construct-arg>``

``</bean>``
#### p名称空间注入（了解）
* 导入p名称空间 xmlns:p="http://www.springframework.org/schema/p"
* 使用p:属性完成注入
            |--值类型：P：属性名= "值"
            |--对象类型： p:属性名-ref="bean名称"
> 实际上还是set方法

``<bean name = "user" class = "com.bean.User" p:name="jack" p:age="16" p:car-ref="兰博基尼"></bean>``

#### spel注入（了解）
  spel注入：spring Expression language spring表达式语言

  ``<bean name = "user" class = "com.bean.User">

  <property name = "name" value="#{user.name}"><property>

  <property name = "age" value="#{user.age}"><property>

  <property name = "car" ref="car"><property>

  </bean>``

### 复杂类型注入

#### array注入

  ``<bean name = "cb" class = "com.bean.CollectionBean">``

> 如果数组中只准备注入一个值（对象），直接使用value和ref即可

//  ``<property name="arr" value></property>``
> 多元素array注入，多个元素注入

  ``<property name="arr" >``

    ``<array>``

      ``<value>tom</value>``

      ``<value>jerry</value>``

      ``<ref bean = "user4"/>``

    ``</array>``

  ``</property>``
#### List注入
  > 如果LIST中只准备注入一个值（对象），直接使用value和ref即可

//  ``<property name= "list" balue="jack">``

``<property name = "list">``

    ``<list>``

      ``<value>jack</value>``

      ``<value>rose</value>``

      ``<ref bean="user4"/>``

    ``</list>``

``</property>``

#### map注入

``<property name = "map">``

    ``<map>``

      ``<entry key="url" value="jdbc:mysql:///crm"></entry>``

      ``<entry key="user" value-ref="user4"></entry>``

      ``<entry key-ref="user3" value-ref="user2"></entry>``

    ``</map>``

``</property>``

#### properties类型注入
``<property name = "prop">``

    ``<props>``

      ``<prop key="diverClass">com.jdbc.mysql.Driver</prop>``

      ``<prop key="userName">root</prop>``

      ``<prop key="password">1234</prop>``

    ``</props>``

``</property>``

  ``</bean>``

## 使用注解配置spring
### 步骤

导包4+2+spring-aop
* 为主配置文件引入新的命名空间（约束）
* 开启使用注解代替配置文件

指定扫描com.bean包下的所有类中的注解

注意：扫描包时，会扫描指定包下的所有子包

``<context:component-scan base-package="com.bean"></context:component-scan>``

* 在类中使用注解

``@Component("user")``

就相当于在xml文件中的

``<bean name = "user" class = "com.bean.User">``
其余一些注解，为了区分对象

### 将对象注册到容器

``@Service("user")`` //Service层

``@Control("user")`` //Web层

``@Ropositor("user")`` //dao层

作用与Component相同，只是为了区分

### 修改对象的作用范围

``@Scope(scopeName="singleton|property")``

//制定对象的作用返回

### 值类型注入

``@value("tom")``

* 将注解放在变量上（通过反射的Field字段赋值）（破坏了对象的封装性）
* 将注解放在set方法上（通过set方法赋值）（推荐使用）

### 引用类型注入
  Car对象 @Component("Car")
  注入给User，将注解放在private Car car上

  * ``@Autowired``

  //自动装配，若有多个类型一致的对象，将无法选择具体注入哪个对象
  * ``@Qualifier("car2")``

  //使用Qualifier注解告诉spring容器自动装配哪个名称的对象
  * ``@resource(name="car2")``

  //手动注入，指定注入哪个名称的对象（推荐）

### 初始化|销毁方法
  ``@PostConstruct``

  //在对象被创建后调用，相当于init-method

  ``@PreDestroy``

  //在对象销毁之前调用，相当于destory-method

## STS插件
## spring与Junit整合测试
### 导包4+2+aop+test
### 配置注解
* @RunWith(SpringJunit4ClassRunner.class)//帮我们创建容器
* @ContextConfiguration（"classpath:applicationContext.xml"）//指定创建容器时使用哪个配置文件
* 获得User
      //将名为User的对象注入到u变量中
    ``@Resource(name="user")``

    ``private User u；``

### 测试
## AOP（Aspect Oriented Programming，面向切面编程）
### AOP思想
横向重复代码，纵向抽取
### 动态代理
动态代理：对目标对象中的方法进行增强
通过动态代理可以体现AOP思想，仅仅是AOP的一个体现形式
### Spring中的AOP
spring能够为容器中管理的对象生成动态代理对象
spring封装了动态代理代码，就不需要手写动态代理代码；还封装了cglib代理；-->可以对任何类进行代理增强
以前我们要使用动态代理，我们需要自己调用下面这个方法。
``Proxy.newProxyInstance(xx,xx,xx)``

spring能帮我们生成代理对象
### spring实现aop的原理
#### 动态代理（优先）
被代理对象必须要实现接口，才能产生代理对象。若果没有借口则不能使用动态代理技术。
#### cglib代理（没有接口）
第三方代理技术，可以对任何类生成代理，代理的原理是对目标对象进行继承代理，如果目标对象被final修饰，那么该类无法被cglib代理。
#### AOP名词学习
* Joinpoint(连接点): 目标对象中，所有可（用代理技术）增强的方法。
* Pointcut(切入点):  目标对象，需要|已经要增强的方法。
* Advice(通知/增强): 增强的代码
* Target(目标对象):  被代理对象
* Weaving(织入):（v.）将通知应用到切入点    
* Proxy（代理）:将通知织入到目标对象后，形成代理对象
* aspect（切面）:切入点+通知

#### Spring中的AOP演示
##### 步骤（XML配置）
* 导包4+2+2+2
* 准备目标对象
* 准备通知
通知种类：

前置通知-->目标方法运行之前调用

``public void before(){System.out.println("前置通知");}``

后置通知（若出现异常则不会调用）-->目标方法运行之后通知

``public void afterReturning(){System.out.println("后置通知（出现异常不调用）");}``

环绕通知-->目标方法运行之前和之后都通知

public Object around(ProceedingJoinPoint pjp) throws Throwable{

    System.out.println("环绕通知之前的部分");

		Object proceed = pjp.proceed();//调用目标方法

		System.out.println("环绕通知之后的部分");

    return proceed;

	}

异常拦截通知-->若出现异常，就会调用

``public void afterException(){System.out.println("出现异常");}``

后置通知（无论是否出现异常都会调用）-->目标方法运行之后通知

``public void after(){System.out.println("后置通知(出现异常也会调用)");}``

* 配置进行织入，将通知织入目标对象

准备工作：导入AOP（约束）命名空间
=
1、配置目标对象
``<bean name="userServiceTarget" class="com.service.UserServicelmpl"></bean>``

2、配置通知对象
``<bean name="myAdvice" class="com.b_springaop.MyAdvice"></bean>``

3、配置将通知织入目标对象

  <aop:config>

    //配置切入点
    ``public void com.service.UserServicelmpl.save()``

    //省略public
    ``void com.service.UserServicelmpl.save()``

    //简化
    ``* com.service.UserServicelmpl.save()``

    //简化
    ``* com.service.UserServicelmpl.*()``

    //简化
    ``* com.service.UserServicelmpl.*(..)``

    //简化
    ``* com.service.*Servicelmpl.*(..)``

		<aop:pointcut expression="executiion(* executiion(com.service.*Servicelmpl.*(..))" id="pc"/>

		<aop:aspect ref="myAdvice">

    <aop:before method="before" pointcut-ref="pc"/>//指定名为before的前置方法作为前置通知

    <aop:after-returning method="afterReturning" pointcut-ref="pc"/>//后置

    <aop:around method="around" pointcut-ref="pc"/>//环绕

    <aop:after-throwing method="afterException" pointcut-ref="pc"/>//异常拦截通知

    <aop:after method="after" pointcut-ref="pc"/>//后置
		</aop:aspect>

##### 步骤（注解配置）
  * 导包4+2
  * 准备目标对象
  * 准备通知对象
  * 开启使用注解完成织入
  @Aspect //表示该类是一个通知
  @Before("executiion(* com.service.*Servicelmpl.*(..))") //指定该方法为前置通知，并指定切入点

	</aop:config>
