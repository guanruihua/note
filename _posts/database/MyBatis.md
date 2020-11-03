---
title: MyBatis
date: 2020-09-17 22:11:02
tags: 
	- mybatis
---

# MyBatis

> OPMapping: Object Relationship Mapping 对象关系映射
>
> - 对象: 面向对象
> - 关系: 关系型数据库
>
> 开发者可以以面向对象的实现来管理数据库
>
> mybatis框架: 实体类, 自定义Mapper接口, Mapper.xml
>
> 项目环境 : idea2019.3, java1.8



## 初使用

新建Maven工程

### pom.xml

```xml
<dependencies>
  <dependency>
    <groupId>org.mybatis</groupId>
    <artifactId>mybatis</artifactId>
    <version>3.4.5</version>
  </dependency>
  <dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>8.0.11</version>
  </dependency>
  <dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.18.6</version>
    <scope>provided</scope>
  </dependency>
</dependencies>
<build>
  <resources>
    <resource>
      <directory>src/main/java</directory>
      <includes>
        <include>**/*.xml</include>
      </includes>
    </resource>
  </resources>
</build>
```



### 新建数据库表

```mysql
use mybatis;
create table t_account(
  id int primary key auto_increment,
  username varchar(11),
  password varchar(11),
  age int
)
```



### 创建数据表对应的实体类Account

```java
package com.southwind.entity.bean;
import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;
@Data
@AllArgsConstructor
@NoArgsConstructor
public class Account {
    private long id;
    private String username;
    private String password;
    private int age;
}
```



### 配置文件

```xml-dtd
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE configuration PUBLIC "-//mybatis.org//DTD Config 3.0//EN" 
"http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <!-- 配置MyBatis运行环境 -->
    <environments default="development">
        <environment id="development">
            <!-- 配置JDBC事务管理 -->
            <transactionManager type="JDBC"></transactionManager>
            <!-- POOLED配置JDBC数据源连接池 -->
            <dataSource type="POOLED">
                <property name="driver" value="com.mysql.cj.jdbc.Driver"></property>
                <property name="url" value="jdbc:mysql://localhost:3306/mybatis?serverTimezone=UTC&amp;useUnicode=true&amp;characterEncoding=UTF-8"></property>
                <property name="username" value="root"></property>
                <property name="password" value="root"></property>
            </dataSource>
        </environment>
    </environments>
  	<!-- 注册多个Mapper.xml-->
  	 <mappers>
        <mapper resource="com/southwind/entity/mapper/AccountMapper.xml"></mapper>
        <mapper resource="com/southwind/entity/mapper/AccountRepository.xml"></mapper>
    </mappers>
  
</configuration>
```



### 使用原生接口

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" 
"http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.southwind.mapper.AccoutMapper">
    <insert id="save" parameterType="com.southwind.entity.Account">
      insert into t_account(username,password,age) values(#{username},#
{password},#{age})
    </insert>
</mapper>
```

> 实际开发中, 每个实体都会创建对应的`Mapper.xml`, 定义管理该对象数据的sql
>
> - `namespace`:  通常设置为文件所在包+文件名的形式
> - `insert`: 执行添加操作
> - `select` : 执行查询操作
> - `update`: 执行更新操作
> - `delete`:执行删除操作
> - `id`是实际调用`MyBatis`方法是否需要用到的参数
> - `parameterType`是调研对应方法时的数据类型



### 使用MyBatis原生接口执行操作

```java
public class Test {
    public static void main(String[] args) {
        //加载MyBatis配置文件
        InputStream inputStream = Test.class.getClassLoader().getResourceAsStream("config.xml");
        SqlSessionFactoryBuilder sqlSessionFactoryBuilder = new SqlSessionFactoryBuilder();
        SqlSessionFactory sqlSessionFactory = sqlSessionFactoryBuilder.build(inputStream);
        SqlSession sqlSession = sqlSessionFactory.openSession();
        String statement = "com.southwind.mapper.AccoutMapper.save";
        Account account = new Account(1L,"grh","123123",22);
        sqlSession.insert(statement,account);
        sqlSession.commit();
    }
}
```

> 通过Mapper代理实现自定义接口





## 自定义接口

```java
public interface AccountRepository {
    public int save(Account account);
    public int update(Account account);
    public int deleteById(long id);
    public List<Account> findAll();
    public Account findById(long id);
}
```



创建对应的Mapper.xml, 定义接口方法对应的sql语句

> statement标签可根据sql执行的业务选择insert, delete, update, select
>
> mybatis框架会根据规则自动创建接口实现列的代理对象
>
> - 规则
>   - namespace: 为接口的全类名
>   - statement中的id为接口中对应的方法名
>   - statement中paramentType和接口分钟对应的方法的类型一致
>   - statement中resultTypehe和接口中对应方法的返回值类型一致





```xml-dtd
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">

<mapper namespace="com.southwind.entity.dao.AccountRepository">
    <insert id="save" parameterType="com.southwind.entity.bean.Account">
        insert into t_account(username,password,age) values(#{username},#
{password},#{age})
    </insert>
    <update id="update" parameterType="com.southwind.entity.bean.Account">
        update t_account set username = #{username},password = #{password},age
= #{age} where id = #{id}
    </update>
    <delete id="deleteById" parameterType="long">
        delete from t_account where id = #{id}
    </delete>
    <select id="findAll" resultType="com.southwind.entity.bean.Account">
        select * from t_account
    </select>
    <select id="findById" parameterType="long"
            resultType="com.southwind.entity.bean.Account">
        select * from t_account where id = #{id}
    </select>
</mapper>
```



在config.xml注册

```xml-dtd
<!-- 注册  -->
<mappers>
  <mapper resource="com/southwind/mapper/AccountMapper.xml"></mapper>
  <mapper resource="com/southwind/repository/AccountRepository.xml"></mapper>
</mappers>
```

```java
public class Test2 {
    public static void main(String[] args) {
        InputStream inputStream =
                ResolverUtil.Test.class.getClassLoader().getResourceAsStream("config.xml");
        SqlSessionFactoryBuilder sqlSessionFactoryBuilder = new
                SqlSessionFactoryBuilder();
        SqlSessionFactory sqlSessionFactory =
                sqlSessionFactoryBuilder.build(inputStream);
        SqlSession sqlSession = sqlSessionFactory.openSession();
        // 获取实现接口的代理对象
        AccountRepository accountRepository =
                sqlSession.getMapper(AccountRepository.class);
        // 添加对象
//        Account account = new Account(3L,"grh","111111",24);
//        int result = accountRepository.save(account);
//        sqlSession.commit();
        // 查询全部对象
//        List<Account> list = accountRepository.findAll();
//        for (Account account:list){
//            System.out.println(account);
//        }
//        sqlSession.close();
        // 通过id查询对象
//        Account account = accountRepository.findById(3L);
//        System.out.println(account);
//        sqlSession.close();
        // 修改对象
//        Account account = accountRepository.findById(3L);
//        account.setUsername("小明");
//        account.setPassword("000");
//        account.setAge(18);
//        int result = accountRepository.update(account);
//        sqlSession.commit();
//        System.out.println(result);
//        sqlSession.close();
        //通过id删除对象
        int result = accountRepository.deleteById(1L);
        System.out.println(result);
        sqlSession.commit();
        sqlSession.close();
    }
}
```



## 及联查询

### 一对多

```java
public class Student {
    private long id;
    private String name;
    private Classes classes;
}
```

```java
public class Classes {
    private long id;
    private String name;
    private List<Student> students;
}
```



```xml-dtd
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" 
"http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.southwind.repository.StudentRepository">
    <resultMap id="studentMap" type="com.southwind.entity.Student">
        <id column="id" property="id"></id>
        <result column="name" property="name"></result>
        <association property="classes" javaType="com.southwind.entity.Classes">
            <id column="cid" property="id"></id>
            <result column="cname" property="name"></result>
        </association>
    </resultMap>
    <select id="findById" parameterType="long" resultMap="studentMap">
        select s.id,s.name,c.id as cid,c.name as cname 
					from student s,classes c 
						where s.id = #{id} and s.cid = c.id
    </select>
</mapper>
```

> association : 涉及到两个表 , 表示一个复杂的关联, 可以将许多结果包装成这类型

```xml-dtd
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" 
"http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.southwind.repository.ClassesRepository">
    <resultMap id="classesMap" type="com.southwind.entity.Classes">
        <id column="cid" property="id"></id>
        <result column="cname" property="name"></result>
        <collection property="students" ofType="com.southwind.entity.Student">
            <id column="id" property="id"/>
            <result column="name" property="name"/>
        </collection>
    </resultMap>
    <select id="findById" parameterType="long" resultMap="classesMap">
        select s.id,s.name,c.id as cid,c.name as cname 
					from student s,classes c 
					where c.id = #{id} and s.cid = c.id
    </select>
</mapper>
```

> collection: 获取一个classes 和一个数组student

### 多对多



```xml-dtd
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" 
"http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.southwind.repository.CustomerRepository">
    <resultMap id="customerMap" type="com.southwind.entity.Customer">
        <id column="cid" property="id"></id>
        <result column="cname" property="name"></result>
        <collection property="goods" ofType="com.southwind.entity.Goods">
            <id column="gid" property="id"/>
            <result column="gname" property="name"/>
        </collection>
    </resultMap>
    <select id="findById" parameterType="long" resultMap="customerMap">
        select c.id cid,c.name cname,g.id gid,g.name gname from customer c,goods 
g,customer_goods cg where c.id = #{id} and cg.cid = c.id and cg.gid = g.id
    </select>
</mapper>
```



```xml-dtd
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" 
"http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.southwind.repository.GoodsRepository">
    <resultMap id="goodsMap" type="com.southwind.entity.Goods">
        <id column="gid" property="id"></id>
        <result column="gname" property="name"></result>
        <collection property="customers" ofType="com.southwind.entity.Customer">
            <id column="cid" property="id"/>
            <result column="cname" property="name"/>
        </collection>
    </resultMap>
    <select id="findById" parameterType="long" resultMap="goodsMap">
        select c.id cid,c.name cname,g.id gid,g.name gname from customer c,goods 
g,customer_goods cg where g.id = #{id} and cg.cid = c.id and cg.gid = g.id
    </select>
</mapper>
```



## MyBatis动态SQL

### if标签

```xml
<select id="findByAccount" parameterType="com.southwind.entity.Account" 
resultType="com.southwind.entity.Account">
    select * from t_account where
  		<if test="id!=0">
        id = #{id}
    </if>
    <if test="username!=null">
        and username = #{username}
    </if>
    <if test="password!=null">
        and password = #{password}
    </if>
    <if test="age!=0">
        and age = #{age}
    </if>
</select>
```



### where标签

```xml
<select id="findByAccount" parameterType="com.southwind.entity.Account" 
resultType="com.southwind.entity.Account">
    select * from t_account
    <where>
        <if test="id!=0">
            id = #{id}
        </if>
        <if test="username!=null">
            and username = #{username}
        </if>
        <if test="password!=null">
            and password = #{password}
        </if>
        <if test="age!=0">
            and age = #{age}
        </if>
    </where>
</select>
```



### choose, when, otherwise标签

> 类似switch,多个选项执行一个



```xml
<select id="findByAccount" parameterType="com.southwind.entity.Account" 
resultType="com.southwind.entity.Account">
    select * from t_account
    <where>
        <choose>
            <when test="id!=0">
             and  id = #{id}
            </when>
            <when test="username!=null">
               and  username = #{username}
            </when>
            <when test="password!=null">
               and  password = #{password}
            </when>
            <when test="age!=0">
            	 and age = #{age}
            </when>
          	 <otherwise>
            	 and age = 22  
            </otherwise>
        </choose>
    </where>
</select>
```



### trim标签



```xml
<select id="findByAccount" parameterType="com.southwind.entity.Account" 
resultType="com.southwind.entity.Account">
    select * from t_account
    <trim prefix="where" prefixOverrides="and">
        <if test="id!=0">
            id = #{id}
        </if>
        <if test="username!=null">
            and username = #{username}
        </if>
        <if test="password!=null">
            and password = #{password}
        </if>
        <if test="age!=0">
            and age = #{age}
        </if>
    </trim>
</select>
```





### set标签



```xml
<update id="update" parameterType="com.southwind.entity.Account">
    update t_account
    <set>
        <if test="username!=null">
            username = #{username},
        </if>
        <if test="password!=null">
            password = #{password},
        </if>
        <if test="age!=0">
            age = #{age}
        </if>
    </set>
    where id = #{id}
</update>
```





### foreach标签



```xml
<select id="findByIds" parameterType="com.southwind.entity.Account" 
resultType="com.southwind.entity.Account">
      select * from t_account
      <where>
          <foreach collection="ids" open="id in (" close=")" item="id"  separator=",">
              #{id}
          </foreach>
      </where>
</select>
```



## MyBatis延迟加载

> - 又名懒加载, 懒惰加载
>
> - 使用延迟加载可以提高程序的运行效率, 针对数据持久层的操作
>
> - 在某些特定的情况下去访问特定的数据库, 在其他秦阔可以不访问某些表, 一定程度上减少java应用与数据库的交互次数



在config.xml中开启延迟加载

```xml-dtd
<settings>
  <!-- 打印SQL-->
  <setting name="logImpl" value="STDOUT_LOGGING" />
  <!-- 开启延迟加载 -->
  <setting name="lazyLoadingEnabled" value="true"/>
</settings>
```



## MyBatis缓存

> - 减少java应用域数据库的交互次数, 提高程序的运行效率

### 缓存分类

#### 一级缓存

> - SqlSession级别, 默认开启, 并且不能关闭
> - 操作数据库时需要创建SqlSession对象, 在对象中有一个HashMap用于存储缓存数据, 不同的SqlSession之间缓存数据区域是互不影响
> - 两次执行相同的sql语句, 第一次若成功执行, 第二次执行就会从第一次缓存中获取

```java
public class Test4 {
    public static void main(String[] args) {
        InputStream inputStream = 
Test.class.getClassLoader().getResourceAsStream("config.xml");
        SqlSessionFactoryBuilder sqlSessionFactoryBuilder = new 
SqlSessionFactoryBuilder();
        SqlSessionFactory sqlSessionFactory = 
sqlSessionFactoryBuilder.build(inputStream);
      
        SqlSession sqlSession = sqlSessionFactory.openSession();
        AccountRepository accountRepository = 
sqlSession.getMapper(AccountRepository.class);
        Account account = accountRepository.findById(1L);
        System.out.println(account);
        sqlSession.close();
      
        sqlSession = sqlSessionFactory.openSession();
        accountRepository = sqlSession.getMapper(AccountRepository.class);
        Account account1 = accountRepository.findById(1L);
        System.out.println(account1);
    }
}
```







#### 二级缓存

> - Mapper级别, 默认关闭, 可以开启
> - 使用耳机缓存时, 多个SqlSession使用同一 个Mapper的SQL语句操作数据库, 得到的数据会存在耳机缓存, 同样是使用HashMap进行数据缓存, 相比较于一级缓存, 耳机缓存的范围更加大, 多个SqlSession可以共用二级缓存, 二级缓存时跨SqlSession的
> - 作用域: Mapper同一个namespace, 不同SqlSession两次执行相同的namespace下的sql语句, 参数也相同, 则会第一次执行成功之后交数据保存到二级缓存中, 第二次可以直接从二级缓存中去的数据



config.xml配置二级缓存

```xml-dtd
<settings>
    <!-- 打印SQL-->
    <setting name="logImpl" value="STDOUT_LOGGING" />
    <!-- 开启延迟加载 -->
    <setting name="lazyLoadingEnabled" value="true"/>
    <!-- 开启二级缓存 -->
    <setting name="cacheEnabled" value="true"/>
</settings>
```

Mapper.xml中配置缓存

```mxl
<cache></cache>
```



实体类实现序列化接口

```java
import java.io.Serializable;
@Data
@AllArgsConstructor
@NoArgsConstructor
public class Account implements Serializable {
    private long id;
    private String username;
    private String password;
    private int age;
}
```

ehcache二级缓存

> pom.xml 添加相关依赖

```xml
<dependency>
  <groupId>org.mybatis</groupId>
  <artifactId>mybatis-ehcache</artifactId>
  <version>1.0.0</version>
</dependency>
<dependency>
  <groupId>net.sf.ehcache</groupId>
  <artifactId>ehcache-core</artifactId>
  <version>2.4.3</version>
</dependency>
```



添加ehcahe.xml

```xml-dtd
<ehcache xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:noNamespaceSchemaLocation="../config/ehcache.xsd">
    <diskStore/>
    <defaultCache
            maxElementsInMemory="1000"
            maxElementsOnDisk="10000000"
            eternal="false"
            overflowToDisk="false"
            timeToIdleSeconds="120"
            timeToLiveSeconds="120"
            diskExpiryThreadIntervalSeconds="120"
            memoryStoreEvictionPolicy="LRU">
    </defaultCache>
</ehcache>
```



config.xml 开启二级缓存

```xml-dtd
<settings>
    <!-- 打印SQL-->
    <setting name="logImpl" value="STDOUT_LOGGING" />
    <!-- 开启延迟加载 -->
    <setting name="lazyLoadingEnabled" value="true"/>
    <!-- 开启二级缓存 -->
    <setting name="cacheEnabled" value="true"/>
</settings>
```

Mapper.xml 中配置二级缓存

```xml
<cache type="org.mybatis.caches.ehcache.EhcacheCache">
  <!-- 缓存创建之后, 最后一次访问的时间至缓存失效的时间间隔  -->
  <property name="timeToIdleSeconds" value="3600"/>
  <!-- 缓存自创建时间起至失效的时间间隔  -->
  <property name="timeToLiveSeconds" value="3600"/>
  <!-- 缓存回收策略, LRU表示移除近期使用最少的对象 -->
  <property name="memoryStoreEvictionPolicy" value="LRU"/>
</cache>
```

实体类不需要事先序列化接口

```java
@Data
@AllArgsConstructor
@NoArgsConstructor
public class Account {
    private long id;
    private String username;
    private String password;
    private int age;
}
```





## 问题

### 时区问题

报错

```verilog
### Error updating database.  Cause: java.sql.SQLException: The server time zone value '�й���׼ʱ��' is unrecognized or represents more than one time zone. You must configure either the server or JDBC driver (via the 'serverTimezone' configuration property) to use a more specifc time zone value if you want to utilize time zone support.
```



添加`serverTimezone=UTC`

```xml
 <property name="url" value="jdbc:mysql://localhost:3306/mybatis?serverTimezone=UTC&amp;useUnicode=true&amp;characterEncoding=UTF-8"></property>
```































































