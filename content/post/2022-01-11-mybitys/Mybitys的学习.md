---
title: Mybitys的学习
author: txz
date: '2022-01-11'
slug: mybitys
categories:
  - Example
tags:
  - Markdown
---
# Mybatis学习

## 环境

- JDK1.8
- Mysql5.7
- maven 3.6.3
- IDEA

## 回顾

- JDBC

- Mysql

- Java基础

- Maven

- Junit

  

## SSM框架：配置文件的最好的方式：看官网文档

# 2 Mybatis

## 1、Mybatis简介（2020-10-21）

### 1.1 什么是Mybatis

​	是一款优秀的持久层框架

​	避免了几乎所有的 JDBC 代码和手动设置参数以及获取结果集的过程

​	 可以使用简单的 XML 或注解来配置和映射原生信息，将接口和 Java 的 实体类 【Plain Old Java Objects,普通的 Java对象】映射成数据库中的记录。



Mybatis官方文档 : http://www.mybatis.org/mybatis-3/zh/index.html

GitHub : https://github.com/mybatis/mybatis-3

如何获得Mybatis

- maven仓库：

  ```
  <!-- https://mvnrepository.com/artifact/org.mybatis/mybatis -->
          <dependency>
              <groupId>org.mybatis</groupId>
              <artifactId>mybatis</artifactId>
              <version>3.5.6</version>
          </dependency>
  ```

- 中文文档：https://mybatis.org/mybatis-3/zh/index.html

- Github:https://github.com/mybatis/mybatis-3

### 1.2 持久化

数据持久化

- 持久化就是将程序的数据在持久状态和瞬时状态转化的过程
- 内存：**断电即失**
- 数据库（JDBC）,io文件持久化

**为什么需要持久化**

- 不想丢掉一些对象
- 内存太贵

### 1.3 持久层

Dao层，Service层，Controller层

- 完成持久化工作的代码块
- 层界限十分明显

### 1.4 为什么需要Mybatis

- 帮助程序员将数据存入到数据库中
- 方便
- 传统的JDBC代码太复杂，简化->框架->自动化
- 不用Mybatis也可以。更容易上手。
- 优点：
  - 简单易学：本身就很小且简单。没有任何第三方依赖，最简单安装只要两个jar文件+配置几个sql映射文件就可以了，易于学习，易于使用，通过文档和源代码，可以比较完全的掌握它的设计思路和实现。
  - 灵活：mybatis不会对应用程序或者数据库的现有设计强加任何影响。sql写在xml里，便于统一管理和优化。通过sql语句可以满足操作数据库的所有需求。
  - 解除sql与程序代码的耦合：通过提供DAO层，将业务逻辑和数据访问逻辑分离，使系统的设计更清晰，更易维护，更易单元测试。sql和代码的分离，提高了可维护性。
  - 提供xml标签，支持编写动态sql。

## 2、第一个Mybatis程序

思路流程：搭建环境-->导入Mybatis--->编写代码--->测试

### 2.1 搭建环境

搭建数据库

```sql
CREATE DATABASE `mybatis`;

USE `mybatis`;

DROP TABLE IF EXISTS `user`;

CREATE TABLE `user` (
`id` int(20) NOT NULL,
`name` varchar(30) DEFAULT NULL,
`pwd` varchar(30) DEFAULT NULL,
PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

insert  into `user`(`id`,`name`,`pwd`) values (1,'上岸秋槐','123456'),(2,'张三','abcdef'),(3,'李四','987654');
```

新建项目

- 新建一个普通maven项目
- 删除src目录
- 导入maven依赖

```xml
<!--import dependencies-->
    <dependencies>
        <!--mysql driver-->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>5.1.47</version>
        </dependency>
        <!--mybatis-->
        <!-- https://mvnrepository.com/artifact/org.mybatis/mybatis -->
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis</artifactId>
            <version>3.5.6</version>
        </dependency>
        <!--junit-->
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
        </dependency>
    </dependencies>
```

## 2.2 创建一个模块

编写MyBatis核心配置文件

查看帮助文档

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
       PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
       "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
   <environments default="development">
       <environment id="development">
           <transactionManager type="JDBC"/>
           <dataSource type="POOLED">
               <property name="driver" value="com.mysql.jdbc.Driver"/>
               <property name="url" value="jdbc:mysql://localhost:3306/mybatis?useSSL=true&amp;useUnicode=true&amp;characterEncoding=utf8"/>
               <property name="username" value="root"/>
               <property name="password" value="123456"/>
           </dataSource>
       </environment>
   </environments>
   <mappers>
       <mapper resource="com/kuang/dao/userMapper.xml"/>
   </mappers>
</configuration>
```

编写mybatis工具类

```java
package com.kuang.utils;

import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;

import java.io.InputStream;

//SqlSessionFactory -->SqlSession
public class MybatisUtils {

    private static SqlSessionFactory sqlSessionFactory;
    static {

        try {
            //使用Mybaties第一步：获取sqlSessionFactory对象
            String resource = "mybatis-config.xml";
            InputStream inputStream = Resources.getResourceAsStream(resource);
            sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    //既然有了 SqlSessionFactory，顾名思义，我们可以从中获得 SqlSession 的实例。
    // SqlSession 提供了在数据库执行 SQL 命令所需的所有方法。你可以通过 SqlSession 实例来直接执行已映射的 SQL 语句。
    public static SqlSession getSqlSession(){
//        SqlSession sqlSession =  sqlSessionFactory.openSession();
//        return sqlSession;

        return sqlSessionFactory.openSession();
    }

}
```

## 2.3 编写代码

- 实体类

```java
//实体类
public class User {
    private int id;
    private String name;
    private String pwd;

    public User() {
    }

    public User(int id, String name, String pwd) {
        this.id = id;
        this.name = name;
        this.pwd = pwd;
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getPwd() {
        return pwd;
    }

    public void setPwd(String pwd) {
        this.pwd = pwd;
    }

    @Override
    public String toString() {
        return "User{" +
                "id=" + id +
                ", name='" + name + '\'' +
                ", pwd='" + pwd + '\'' +
                '}';
    }
}
```

- Dao接口

```java
public interface UserDao {
    List<User> getUserList();
}
```

- 接口实现类由原来的UserDaoImpl转变成一个Mapper配置文件。

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<!--namespace=绑定一个对应的Dao/Mapper窗口-->
<mapper namespace="com.kuang.dao.UserMapper">
    <!--select查询语句-->
    <select id="selectUser" resultType="com.kuang.pojo.User">
  		select * from user
 	</select>
</mapper>
```

## 2.4 注意点：

- org.apache.ibatis.binding.BindingException: Type interface com.kuang.dao.UserDao is not known to the MapperRegistry.

**MapperRegistry是什么？**

核心配置文件中注册mappers

```xml
<!--    每一个Mapper.xml文件都需要在Mybatis核心配置文件中注册-->
    <mappers>
        <mapper resource="com/kuang/dao/userMapper.xml"/>
    </mappers>
```

- junit测试

```java
public class UserDaoTest {

    @Test
    public void test() {

        // 第一步：获得SqlSession对象
        SqlSession sqlSession = MybatisUtils.getSqlSession();

        //方式一：getMapper
        UserDao userDao = sqlSession.getMapper(UserDao.class);
        List<User> userList = userDao.getUserList();

        for (User user : userList) {
            System.out.println(user);
        }

        //关闭SqlSession
        sqlSession.close();
    }
}
```

可能遇到的问题：

1. 配置文件没有注册；
2. 绑定接口错误；
3. 方法名不对；
4. 返回类型不对；
5. Maven导出资源问题。

## 问题说明

可能出现问题说明：Maven静态资源过滤问题

```xml
<resources>
   <resource>
       <directory>src/main/java</directory>
       <includes>
           <include>**/*.properties</include>
           <include>**/*.xml</include>
       </includes>
       <filtering>false</filtering>
   </resource>
   <resource>
       <directory>src/main/resources</directory>
       <includes>
           <include>**/*.properties</include>
           <include>**/*.xml</include>
       </includes>
       <filtering>false</filtering>
   </resource>
</resources>
```

# 3、CRUD以及配置解析

### 3.1 namespace

namespace中的包名要和Dao/Mapper接口的包名一致！

### 3.2 select

选择，查询语句；

- id:就是对应的namespace中的方法名；
- resultType:Sql语句执行的返回值！
- parameterType:参数类型！

1、编写接口

```java
//根据id查询用户
    User getUserById(int id);
```

2、编写对应mapper中的sql语句

```xml
	<select id="getUserById" parameterType="int" resultType="com.kuang.pojo.User">
        select * from mybatis.user where id = #{id}
	</select>
```

3、测试

```java
@Test
    public void getUserById(){
        SqlSession sqlSession = MybatisUtils.getSqlSession();

        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        User user = mapper.getUserById(1);
        System.out.println(user);

        //关闭SqlSession
        sqlSession.close();
    }
```

### 3.3 insert

我们一般使用insert标签进行插入操作，它的配置和select标签差不多！

需求：给数据库增加一个用户

1、在UserMapper接口中添加对应的方法

```java
//添加一个用户
int addUser(User user);
```

2、在UserMapper.xml中添加insert语句

```xml
<insert id="addUser" parameterType="com.kuang.pojo.User">
    insert into user (id,name,pwd) values (#{id},#{name},#{pwd})
</insert>
```

3、测试

```java
@Test
public void testAddUser() {
   SqlSession session = MybatisUtils.getSession();
   UserMapper mapper = session.getMapper(UserMapper.class);
   User user = new User(5,"王五","zxcvbn");
   int i = mapper.addUser(user);
   System.out.println(i);
   session.commit(); //提交事务,重点!不写的话不会提交到数据库
   session.close();
}
```

注意点：**增、删、改操作需要提交事务！**

### 3.4 upadte

我们一般使用update标签进行更新操作，它的配置和select标签差不多！

需求：修改用户的信息

1、同理，编写接口方法

```java
//修改一个用户
int updateUser(User user);
```

2、编写对应的配置文件SQL

```xml
<update id="updateUser" parameterType="com.kuang.pojo.User">
  update user set name=#{name},pwd=#{pwd} where id = #{id}
</update>
```

3、测试

```java
@Test
public void testUpdateUser() {
   SqlSession session = MybatisUtils.getSession();
   UserMapper mapper = session.getMapper(UserMapper.class);
   User user = mapper.selectUserById(1);
   user.setPwd("asdfgh");
   int i = mapper.updateUser(user);
   System.out.println(i);
   session.commit(); //提交事务,重点!不写的话不会提交到数据库
   session.close();
}
```

### 3.5 delete

我们一般使用delete标签进行删除操作，它的配置和select标签差不多！

需求：根据id删除一个用户

1、同理，编写接口方法

```java
//根据id删除用户
int deleteUser(int id);
```

2、编写对应的配置文件SQL

```xml
<delete id="deleteUser" parameterType="int">
  delete from user where id = #{id}
</delete>
```

3、测试

```java
@Test
public void testDeleteUser() {
   SqlSession session = MybatisUtils.getSession();
   UserMapper mapper = session.getMapper(UserMapper.class);
   int i = mapper.deleteUser(5);
   System.out.println(i);
   session.commit(); //提交事务,重点!不写的话不会提交到数据库
   session.close();
}
```

### 小结：

- 所有的增删改操作都需要提交事务！
- 接口所有的普通参数，尽量都写上@Param参数，尤其是多个参数时，必须写上！
- 有时候根据业务的需求，可以考虑使用map传递参数！
- 为了规范操作，在SQL的配置文件中，我们尽量将Parameter参数和resultType都写上！

### 3.6 分析错误

1. xml文件中注释不能出现中文报错，查看自己的是UTF-8还是GBK编码，改成为相应的就行。

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<?xml version="1.0" encoding="GBK" ?>
```

即可成功测试。

1. 标签不要匹配错！
2. resource绑定mapper，需要使用路径！
3. 程序配置文件必须符合规范！
4. NullPointerException，没有注册到资源！
5. maven资源没有导出问题！

### 3.7 万能Map

假设，我们的实体类，或者数据库中的表，字段或者参数过多，我们应当考虑使用Map！

```java
//万能的Map
    int addUser2(Map<String,Object> map);
<!--对象中的属性，可以直接取出来  传递map的key-->
    <insert id="addUser2" parameterType="map">
        insert into mybatis.user (id,pwd) values (#{userid},#{password})
    </insert>
@Test
     public void addUser2(){
         SqlSession sqlSession = MybatisUtils.getSqlSession();

         UserMapper mapper = sqlSession.getMapper(UserMapper.class);
         Map<String,Object> map = new HashMap<String, Object>();
         map.put("userid",qiuhuai);
         map.put("password","15963257");

         mapper.addUser2(map);


         sqlSession.commit();
         sqlSession.close();
     }
```

Map传递参数，直接在sql中取出key即可！【parameterType=“map”】
对象传递参数，直接在sql中取对象的属性即可！【parameterType=“Object”】
只有一个基本类型参数的情况下，可以直接在sql中取到！
多个参数用Map，**或者注解！**



> 模糊查询like语句该怎么写?

第1种：在Java代码中添加sql通配符。

```java
string wildcardname = “%smi%”;
list<name> names = mapper.selectlike(wildcardname);

<select id=”selectlike”>
select * from foo where bar like #{value}
</select>
```

第2种：在sql语句中拼接通配符，会引起sql注入

```java
string wildcardname = “smi”;
list<name> names = mapper.selectlike(wildcardname);

<select id=”selectlike”>
    select * from foo where bar like "%"#{value}"%"
</select>
```

# 4 配置解析

### 1. 核心配置文件

- mybatis-config.xml
- Mybatis的配置文件包含了会深深影响MyBatis行为的设置和属性信息。

```java
configuration（配置）
    properties（属性）
    settings（设置）
    typeAliases（类型别名）
    typeHandlers（类型处理器）
    objectFactory（对象工厂）
    plugins（插件）
        environments（环境配置）
            environment（环境变量）
            transactionManager（事务管理器）
    dataSource（数据源）
    databaseIdProvider（数据库厂商标识）
    mappers（映射器）
```

### 2. 环境配置（environments）

MyBatis 可以配置成适应多种环境

**不过要记住：尽管可以配置多个环境，但每个 SqlSessionFactory 实例只能选择一种环境。**

Mybatis 默认的事务管理器是JDBC，连接池：POOLED

### 3. 属性

我们可以通过properties属性来引用配置文件

这些属性可以在外部进行配置，并可以进行动态替换。你既可以在典型的 Java 属性文件中配置这些属性，也可以在 properties 元素的子元素中设置。 （db.properties）

编写一个配置文件

```java
driver = com.mysql.jdbc.Driver
url = "jdbc:mysql://localhost:3306/mybatis?useSSL=true&amp;useUnicode=true&amp;characterEncoding=utf8""
username = root 
password = root
```

在核心配置文件中引入

mybatis-config.xml (同时有的话，优先走外面properties)

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <!--引入外部配置文件-->
    <!--<properties resource="db.properties">-->

    <properties resource="db.properties">
        <property name="username" value="root"/>
        <property name="password" value="root"/>
    </properties>
    
    <environments default="development">
        <environment id="development">
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">
                <property name="driver" value="com.mysql.jdbc.Driver"/>
                <property name="url" value="jdbc:mysql://localhost:3306/mybatis?useSSL=true&amp;useUnicode=true&amp;characterEncoding=utf8"/>
                <property name="username" value="root"/>
                <property name="password" value="root"/>
            </dataSource>
        </environment>
    </environments>

    <!--每一个Mapper.xml文件都需要在Mybatis核心配置文件中注册-->
    <mappers>
        <mapper resource="com/kuang/dao/UserMapper.xml"/>
    </mappers>

</configuration>
```

1. 可以直接引入外部文件
2. 可以在其中增加一些属性配置
3. 如果两个文件有同一个字段，优先使用外部配置文件的

### 4. 类型别名 typeAliases

- 类型别名可为 Java 类型设置一个缩写名字。 它仅用于 XML 配置.
- 意在降低冗余的全限定类名书写。

```java
<!--可以给实体类起别名-->
<typeAliases>
    <typeAlias type="com.kuang.pojo.User" alias="User"/>
</typeAliases>
```

也可以指定一个包，每一个在包 `domain.blog` 中的 Java Bean，在没有注解的情况下，会使用 Bean 的首字母小写的非限定类名来作为它的别名。 比如 `domain.blog.Author` 的别名为 `author`,；若有注解，则别名为其注解值。见下面的例子：

```java
<typeAliases>
    <package name="com.kuang.pojo"/>
</typeAliases>
```

在实体类比较少的时候，使用第一种方式。

如果实体类十分多，建议用第二种扫描包的方式。

第一种可以DIY别名，第二种不行，如果非要改，需要在实体上增加注解。

```java
@Alias("author")
public class Author {
    ...
}
```

### 5.设置

| 设置名             | 描述                                                         | 有效值                                                       | 默认   |
| :----------------- | :----------------------------------------------------------- | :----------------------------------------------------------- | :----- |
| cacheEnabled       | 全局性地开启或关闭所有映射器配置文件中已配置的任何缓存。     | true \| false                                                | true   |
| lazyLoadingEnabled | 延迟加载的全局开关。当开启时，所有关联对象都会延迟加载。 特定关联关系中可通过设置 `fetchType` 属性来覆盖该项的开关状态。 | true \| false                                                | false  |
| logImpl            | 指定 MyBatis 所用日志的具体实现，未指定时将自动查找。        | SLF4J \| LOG4J \| LOG4J2 \| JDK_LOGGING \| COMMONS_LOGGING \| STDOUT_LOGGING \| NO_LOGGING | 未设置 |

### 6. 其他

- [typeHandlers（类型处理器）](https://mybatis.org/mybatis-3/zh/configuration.html#typeHandlers)
- [objectFactory（对象工厂）](https://mybatis.org/mybatis-3/zh/configuration.html#objectFactory)
- plugins（插件）
  - mybatis-generator-core
  - mybatis-plus
  - 通用mapper

### 7. 映射器 mappers

MapperRegistry：注册绑定我们的Mapper文件；

方式一: [推荐使用]

```xml
<mappers>
    <mapper resource="com/hou/dao/UserMapper.xml"/>
</mappers>
```

方式二：

```xml
<mappers>
    <mapper class="com.hou.dao.UserMapper" />
</mappers>
```

- 接口和它的Mapper必须同名
- 接口和他的Mapper必须在同一包下

方式三：

```xml
<mappers>
    <!--<mapper resource="com/hou/dao/UserMapper.xml"/>-->
    <!--<mapper class="com.hou.dao.UserMapper" />-->
    <package name="com.hou.dao" />
</mappers>
```

- 接口和它的Mapper必须同名
- 接口和他的Mapper必须在同一包下



### 借鉴以下文章：

[1]: https://blog.csdn.net/qq_45304571/article/details/122219273
[2]: https://blog.csdn.net/li643937579/article/details/109194467

