---
title: Spring学习(二)
tags: [Spring,JavaWeb]
---
## spring整合JDBC
spring中提供了一个可以操作数据库的对象，对象封装了jdbc技术。
JDBCTemplate模板对象
与DBUtils中的queryRunner非常相似
准备工作
1、导包
* 4+2
* spring-test、spring-aop、junit4类库
* c3p0连接池+DBC驱动
* spring-jdbc+spring-tx事物

2、准备数据库
public class Demo {

	@Test
	public void fun1() throws PropertyVetoException{
		//0\准备连接池
		ComboPooledDataSource dataSource = new ComboPooledDataSource();
		dataSource.setDriverClass("com.mysql.jdbc.Driver");
		dataSource.setJdbcUrl("jdbc:mysql:///sun");
		dataSource.setUser("root");
		dataSource.setPassword("root");

		//1\创建jdbc模板对象
		JdbcTemplate jt = new JdbcTemplate();
		jt.setDataSource(dataSource);

		//2\书写sql，并执行
		String sql="insert into t_user values(null,'Rose')";

		jt.update(sql);

	}
增删改查中的查
@Override
	public User getById(Integer id) {
		// TODO Auto-generated method stub
		String sql = "select * from t_user where id = ?";
		return jt.queryForObject(sql,new RowMapper<User>(){

			@Override
			public User mapRow(ResultSet rs, int arg1) throws SQLException {

				User u = new User();
				u.setId(rs.getInt("id"));
				u.setName(rs.getString("name"));
				return u;
			}},id);
	}

applicationContext.xml配置

	<!-- 1、将连接池放入spring容器 -->
	<bean name = "dataSource" class="com.mchange.v2.c3p0.ComboPooledDataSource">
		<property name="jdbcUrl" value="jdbc:mysql:///sun"></property>
		<property name="driverClass" value="com.mysql.jdbc.Driver"></property>
		<property name="user" value="root"></property>
		<property name="password" value="root"></property>
	</bean>
	<!-- 2、将JDBCTemplate放入spring容器 -->
	<bean name="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate">
		<property name="dataSource" ref="dataSource"></property>
	</bean>
	<!-- 3、将UserDao放入spring容器 -->
	<bean name="userDao" class="com.a_jdbctemplate.UserDaoImpl">
		<property name = "jt" ref="jdbcTemplate"></property>
	</bean>
## spring中aop事物
### 事务
#### 事务特性：acid
> ACID，指数据库事务正确执行的四个基本要素的缩写。包含：原子性（Atomicity）、一致性（Consistency）、隔离性（Isolation）、持久性（Durability）。一个支持事务（Transaction）的数据库，必需要具有这四种特性，否则在事务过程（Transaction processing）当中无法保证数据的正确性，交易过程极可能达不到交易方的要求。

#### 事务并发问题

1、赃读
> 一个事务读取了另一个事务未提交的数据。事务A：张三妻子给张三转账100元。事务B：张三查询余额。事务A转账后（还未提交），事务B查询多了100元。事务A由于某种问题，比如超时，进行回滚。事务B查询到的数据是假数据。脏读本质上是读写操作的冲突，解决办法是写完之后再读。

2、不可重复读
> 一个事务两次读取同一个数据，两次读取的数据不一致。事务A：张三妻子给张三转账100元。事务B：张三两次查询余额。事务B第一次查询余额，事务A还没有转账，第二次查询余额，事务A已经转账了，导致一个事务中，两次读取同一个数据，读取的数据不一致。不可重复读本质上是读写操作的冲突，解决办法是读完再写。

3、幻读
> 一个事务两次读取一个范围的记录，两次读取的记录数不一致。事务A：张三妻子两次查询张三有几张银行卡。事务B：张三新办一张银行卡。事务A第一次查询银行卡数的时候，张三还没有新办银行卡，第二次查询银行卡数的时候，张三已经新办了一张银行卡，导致两次读取的银行卡数不一样。幻象读本质上是读写操作的冲突，解决办法是读完再写。

#### 事务的隔离级别
1、读未提交
2、读已提交
4、可重复读
8、串行化

### spring封装了事务管理代码
#### 事务操作
* 打开事务
* 提交事务
* 回滚事务

#### 实务操作对象
1、因为在不同平台，操作事务的代码各不相同，因此spring提供了一个接口
2、PlatformTransactionManager接口（spring中事务管理最为核心的的对象就是TransactionManager对象）
* DataSourceCTransactionManager
* HibernateTransactionManager
3、spring管理事务的属性介绍
事务的隔离级别
1、读未提交
2、读已提交
4、可重复读
8、串行化
是否只读 ：true只读，false可操作
事务的传播行为：决定业务方法之间调用，事务如何处理
PROPAGION_XXX :事务的传播行为
* 保证同一个事务中
PROPAGATION_REQUIRED 支持当前事务，如果不存在 就新建一个(默认)
PROPAGATION_SUPPORTS 支持当前事务，如果不存在，就不使用事务
PROPAGATION_MANDATORY 支持当前事务，如果不存在，抛出异常
* 保证没有在同一个事务中
PROPAGATION_REQUIRES_NEW 如果有事务存在，挂起当前事务，创建一个新的事务
PROPAGATION_NOT_SUPPORTED 以非事务方式运行，如果有事务存在，挂起当前事务
PROPAGATION_NEVER 以非事务方式运行，如果有事务存在，抛出异常
PROPAGATION_NESTED 如果当前事务存在，则嵌套事务执行
### spring管理事务方式
* 编码式
1、将核心事务管理其配置到spring容器
* xml配置（aop）（重要）
* 注解配置（aop）（重要）
