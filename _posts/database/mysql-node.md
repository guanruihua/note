---
title: mysql-node
date: 
tags: 
	- mysql
	- node
	- javascript
	- database
---



# Mysql-node

Node.js 连接 MySQL

介绍如何使用 Node.js 来连接 MySQL，并对数据库进行操作。

### 安装驱动

```
$ npm install mysql
```

### 连接数据库

在以下实例中根据你的实际配置修改数据库用户名、及密码及数据库名：

## test.js 文件代码：

```javascript
var mysql      = require('mysql');
var connection = mysql.createConnection({
  host     : 'localhost',
  user     : 'root',
  password : '123456',
  database : 'test'
});
 
connection.connect();
 
connection.query('SELECT 1 + 1 AS solution', function (error, results, fields) {
  if (error) throw error;
  console.log('The solution is: ', results[0].solution);
});
```

执行以下命令输出结果为：

$ node test.js
The solution is: 2



## 数据库操作( CURD )

在进行数据库操作前，你需要将本站提供的 Websites 表 SQL 文件[websites.sql](https://static.runoob.com/download/websites.sql) 导入到你的 MySQL 数据库中。

本教程测试的 MySQL 用户名为 root，密码为 123456，数据库为 test，你需要根据自己配置情况修改。

### 查询数据

将上面我们提供的 SQL 文件导入数据库后，执行以下代码即可查询出数据：

## 查询数据

```javascript
var mysql  = require('mysql');  
 
var connection = mysql.createConnection({     
  host     : 'localhost',       
  user     : 'root',              
  password : '123456',       
  port: '3306',                   
  database: 'test' 
}); 
 
connection.connect();
 
var  sql = 'SELECT * FROM websites';
//查
connection.query(sql,function (err, result) {
        if(err){
          console.log('[SELECT ERROR] - ',err.message);
          return;
        }
 
       console.log('------SELECT------');
       console.log(result);
       console.log('------------------');  
});
 
connection.end();
```

执行以下命令输出就结果为：

```
$ node test.js
--------------------------SELECT----------------------------
[ RowDataPacket {
    id: 1,
    name: 'Google',
    url: 'https://www.google.cm/',
    alexa: 1,
    country: 'USA' },
  RowDataPacket {
    id: 2,
    name: '淘宝',
    url: 'https://www.taobao.com/',
    alexa: 13,
    country: 'CN' }
]
------------------------------------------------------------
```

### 插入数据

我们可以向数据表 websties 插入数据：

## 插入数据

```javascript
var mysql  = require('mysql');  
 
var connection = mysql.createConnection({     
  host     : 'localhost',       
  user     : 'root',              
  password : '123456',       
  port: '3306',                   
  database: 'test' 
}); 
 
connection.connect();
 
var  addSql = 'INSERT INTO websites(Id,name,url,alexa,country) VALUES(0,?,?,?,?)';
var  addSqlParams = ['工具', 'https://c.sxb.com','23453', 'CN'];
//增
connection.query(addSql,addSqlParams,function (err, result) {
        if(err){
         console.log('[INSERT ERROR] - ',err.message);
         return;
        }        
 
       console.log('------INSERT------');
       //console.log('INSERT ID:',result.insertId);        
       console.log('INSERT ID:',result);        
       console.log('--------------\n\n');  
});
 
connection.end();
```

执行以下命令输出就结果为：

```
$ node test.js
--------------------------INSERT----------------------------
INSERT ID: OkPacket {
  fieldCount: 0,
  affectedRows: 1,
  insertId: 6,
  serverStatus: 2,
  warningCount: 0,
  message: '',
  protocol41: true,
  changedRows: 0 }
-----------------------------------------------------------------
```

执行成功后，查看数据表，即可以看到添加的数据

### 更新数据

我们也可以对数据库的数据进行修改：

## 更新数据

```javascript
var mysql  = require('mysql');  
 
var connection = mysql.createConnection({     
  host     : 'localhost',       
  user     : 'root',              
  password : '123456',       
  port: '3306',                   
  database: 'test' 
}); 
 
connection.connect();
 
var modSql = 'UPDATE websites SET name = ?,url = ? WHERE Id = ?';
var modSqlParams = ['移动站', 'https://m.sxt.com',6];
//改
connection.query(modSql,modSqlParams,function (err, result) {
   if(err){
         console.log('[UPDATE ERROR] - ',err.message);
         return;
   }        
  console.log('--------UPDATE--------');
  console.log('UPDATE affectedRows',result.affectedRows);
  console.log('----------\n\n');
});
 
connection.end();
```

执行以下命令输出就结果为：

```
--------------------------UPDATE----------------------------
UPDATE affectedRows 1
-----------------------------------------------------------------
```

执行成功后，查看数据表

### 删除数据

我们可以使用以下代码来删除 id 为 6 的数据:

## 删除数据

```javascript
var mysql  = require('mysql');  
 
var connection = mysql.createConnection({     
  host     : 'localhost',       
  user     : 'root',              
  password : '123456',       
  port: '3306',                   
  database: 'test' 
}); 
 
connection.connect();
 
var delSql = 'DELETE FROM websites where id=6';
//删
connection.query(delSql,function (err, result) {
        if(err){
          console.log('[DELETE ERROR] - ',err.message);
          return;
        }        
 
       console.log('-----DELETE-------');
       console.log('DELETE affectedRows',result.affectedRows);
       console.log('----------------\n\n');  
});
 
connection.end();
```

执行以下命令输出就结果为：

```
--------------------------DELETE----------------------------
DELETE affectedRows 1
-----------------------------------------------------------------
```

执行成功后，查看数据表

## 排序

- 为了方便查看数据，可以对数据进行排序
- 语法：

```
select * from 表名
order by 列1 asc|desc,列2 asc|desc,...
```

- 将行数据按照列1进行排序，如果某些行列1的值相同时，则按照列2排序，以此类推
- 默认按照列值从小到大排列
- asc从小到大排列，即升序
- desc从大到小排序，即降序
- 查询未删除男生学生信息，按学号降序

```
select * from students
where gender=1 and isdelete=0
order by id desc;
```

- 查询未删除科目信息，按名称升序

```
select * from subject
where isdelete=0
order by stitle;
```

## 聚合

- 为了快速得到统计数据，提供了5个聚合函数
- count(*)表示计算总行数，括号中写星与列名，结果是相同的
- 查询学生总数

```
select count(*) from students;
```

- max(列)表示求此列的最大值
- 查询女生的编号最大值

```
select max(id) from students where gender=0;
```

- min(列)表示求此列的最小值
- 查询未删除的学生最小编号

```
select min(id) from students where isdelete=0;
```

- sum(列)表示求此列的和
- 查询男生的编号之后

```
select sum(id) from students where gender=1;
```

- avg(列)表示求此列的平均值
- 查询未删除女生的编号平均值

```
select avg(id) from students where isdelete=0 and gender=0;
```

## 分组

- 按照字段分组，表示此字段相同的数据会被放到一个组中
- 分组后，只能查询出相同的数据列，对于有差异的数据列无法出现在结果集中
- 可以对分组后的数据进行统计，做聚合运算
- 语法：

```
select 列1,列2,聚合... from 表名 group by 列1,列2,列3...
```

- 查询男女生总数

```
select gender as 性别,count(*)
from students
group by gender;
```

- 查询各城市人数

```
select hometown as 家乡,count(*)
from students
group by hometown;
```

#### 分组后的数据筛选

- 语法：

```
select 列1,列2,聚合... from 表名
group by 列1,列2,列3...
having 列1,...聚合...
```

- having后面的条件运算符与where的相同
- 查询男生总人数

```
方案一
select count(*)
from students
where gender=1;
-----------------------------------
方案二：
select gender as 性别,count(*)
from students
group by gender
having gender=1;
```

#### 对比where与having

- where是对from后面指定的表进行数据筛选，属于对原始数据的筛选
- having是对group by的结果进行筛选

 获取部分行

- 当数据量过大时，在一页中查看数据是一件非常麻烦的事情
- 语法

```
select * from 表名
limit start,count
```

- 从start开始，获取count条数据
- start索引从0开始

#### 示例：分页

- 已知：每页显示m条数据，当前显示第n页
- 求总页数：此段逻辑后面会在python中实现
  - 查询总条数p1
  - 使用p1除以m得到p2
  - 如果整除则p2为总数页
  - 如果不整除则p2+1为总页数
- 求第n页的数据

```
select * from students
where isdelete=0
limit (n-1)*m,m
```

## 范式

### 示例表数据

假设有一个名为`employee`的员工表，它有九个属性：`id`(员工编号)、`name`(员工名称)、`mobile`(电话)、`zip`(邮编)、`province`(省份)、`city`(城市)、`district`(区县)、`deptNo`(所属部门编号)、`deptName`(所属部门名称)、表总数据如下：

| id   | name | mobile                  | zip    | province | city | district | deptNo | deptName |
| ---- | ---- | ----------------------- | ------ | -------- | ---- | -------- | ------ | -------- |
| 101  | 张三 | 13910000001 13910000002 | 100001 | 北京     | 北京 | 海淀区   | D1     | 部门1    |
| 101  | 张三 | 13910000001 13910000002 | 100001 | 北京     | 北京 | 海淀区   | D2     | 部门2    |
| 102  | 李四 | 13910000003             | 200001 | 上海     | 上海 | 静安区   | D3     | 部门3    |
| 103  | 王五 | 13910000004             | 510001 | 广东省   | 广州 | 白云区   | D4     | 部门4    |
| 103  | 王五 | 13910000004             | 510001 | 广东省   | 广州 | 白云区   | D5     | 部门 5   |

由于此员工表是非规范化的，我们将面对如下的问题。

> - **修改异常**：上表中张三有两条记录，因为他隶属于两个部门。如果我们要修改张三的地址，必修修改两行记录。假如一个部门得到了张三的新地址并进行了更新，而另一个部门没有，那么此时张三在表中会存在两个不同的地址，导致了数据不一致
> - **新增异常：**假如一个新员工假如公司，他正处于入职培训阶段，还没有被正式分配到某个部门，如果`deptNo`字段不允许为空，我们就无法向`employee`表中新增该员工的数据。
> - **删除异常：**假设公司撤销了D3部门，那么在删除`deptNo`为D3的行时，会将李四的信息也一并删除。因为他隶属于D3这一部门。

### 第一范式(1NF)

> **表中的列只能含有原子性(不可再分)的值。**

表中的张三有两个手机号存储在mobile列中，违反了 1NF 规则。为了使表满足 1NF，数据应该修改如下：

| id   | name | mobile      | zip    | province | city | district | deptNo | deptName |
| ---- | ---- | ----------- | ------ | -------- | ---- | -------- | ------ | -------- |
| 101  | 张三 | 13910000001 | 100001 | 北京     | 北京 | 海淀区   | D1     | 部门1    |
| 101  | 张三 | 13910000002 | 100001 | 北京     | 北京 | 海淀区   | D1     | 部门1    |
| 101  | 张三 | 13910000001 | 100001 | 北京     | 北京 | 海淀区   | D2     | 部门2    |
| 101  | 张三 | 13910000002 | 100001 | 北京     | 北京 | 海淀区   | D2     | 部门2    |
| 102  | 李四 | 13910000003 | 200001 | 上海     | 上海 | 静安区   | D3     | 部门3    |
| 103  | 王五 | 13910000004 | 510001 | 广东省   | 广州 | 白云区   | D4     | 部门4    |
| 103  | 王五 | 13910000004 | 510001 | 广东省   | 广州 | 白云区   | D5     | 部门 5   |

### 第二范式(2NF)

第二范式要同时满足下面两个条件

> - **满足第一范式**
> - **没有部分依赖**

例如，员工表的一个候选键是{id，mobile，deptNo}，而deptName依赖于deptNo，同样 name 依赖于 id，因此不是 2NF的。为了满足第二范式的条件，需要将这个表拆分成employee、dept、employee_dept、employee_mobile四个表。如下：

**员工表 employee**

| id   | name | zip    | province | city | district |
| ---- | ---- | ------ | -------- | ---- | -------- |
| 101  | 张三 | 100001 | 北京     | 北京 | 海淀区   |
| 102  | 李四 | 200001 | 上海     | 上海 | 静安区   |
| 103  | 王五 | 510001 | 广东省   | 广州 | 白云区   |

**部门表 dept**

| deptNo | deptName |
| ------ | -------- |
| D1     | 部门1    |
| D2     | 部门2    |
| D3     | 部门3    |
| D4     | 部门4    |
| D5     | 部门5    |

**员工部门关系表 employee_dept**

| id   | deptNo |
| ---- | ------ |
| 101  | D1     |
| 101  | D2     |
| 102  | D3     |
| 103  | D4     |
| 104  | D5     |

**员工电话表 employee_mobile**

| id   | mobile      |
| ---- | ----------- |
| 101  | 13910000001 |
| 101  | 13910000002 |
| 102  | 13910000003 |
| 103  | 13910000004 |

### 第三范式(3NF)

第三范式要同时满足下面两个条件

> - **满足第二范式**
> - **没有传递依赖**

例如，员工表的province、city、district依赖于zip，而zip依赖于id，换句话说，province、city、district传递依赖于id，违反了 3NF 规则。为了满足第三范式的条件，可以将这个表拆分成employee和zip两个表，如下

**employee**

| id   | name | zip    |
| ---- | ---- | ------ |
| 101  | 张三 | 100001 |
| 102  | 李四 | 200001 |
| 103  | 王五 | 510001 |

**地区表area**

| zip    | province | city | district |
| ------ | -------- | ---- | -------- |
| 100001 | 北京     | 北京 | 海淀区   |
| 200001 | 上海     | 上海 | 静安区   |
| 51000  | 广东省   | 广州 | 白云区   |

在关系数据库模型设计中，一般需要满足第三范式的要求。如果一个表具有良好的主外键设计，就应该是满足3NF的表。规范化带来的好处是通过减少数据冗余提高更新数据的效率，同时保证数据完整性。然而，我们在实际应用中也要防止过度规范化的问题。规范化程度越高，划分的表就越多，在查询数据时越有可能使用表连接操作。而如果连接的表过多，会影响查询性能。关键的问题是要依据业务需求，仔细权衡数据查询和数据更新关系，指定最合适的规范化程度。不要为了遵循严格的规范化规则而修改业务需求

## 数据库一对一、一对多、多对多设计

------

数据库实体间有三种对应关系：一对一、一对多、多对多

一对一关系示例：

一个学生对应一个学生档案材料 每个人都有唯一的身份证号

一对多关系示例：

一个学生只属于一个班，但这个班有多名学生

多对多关系示例：

一个学生可以选择多门课，一门课也可以有多名学生

一个人可以有多个角色，一个角色可以有多个人

 

一、一对多关系处理

![img](https:////upload-images.jianshu.io/upload_images/3781695-ad93b299b2fc9c2a.png?imageMogr2/auto-orient/strip|imageView2/2/w/517/format/webp)

设计数据库表：只需在 学生表 中多添加一个班级号的ID即可

二、多对多关系处理

![img](https:////upload-images.jianshu.io/upload_images/3781695-5dbc50523244885e.png?imageMogr2/auto-orient/strip|imageView2/2/w/866/format/webp)

![img](https:////upload-images.jianshu.io/upload_images/3781695-9ff016c8cea50772.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/webp)

 

### 关系

- 创建成绩表scores，结构如下
  - id
  - 学生
  - 科目
  - 成绩
- 
- 思考：学生列应该存什么信息呢？
- 答：学生列的数据不是在这里新建的，而应该从学生表引用过来，关系也是一条数据；根据范式要求应该存储学生的编号，而不是学生的姓名等其它信息
- 同理，科目表也是关系列，引用科目表中的数据

![关系](D:/note/Front-end/node/images/r.png)

- 创建表的语句如下

```
create table scores(
id int primary key auto_increment,
stuid int,
subid int,
score decimal(5,2)
);
```

### 外键

- 思考：怎么保证关系列数据的有效性呢？任何整数都可以吗？
- 答：必须是学生表中id列存在的数据，可以通过外键约束进行数据的有效性验证
- 为stuid添加外键约束

```
alter table scores add constraint stu_sco foreign key(stuid) references students(id);
```

- 此时插入或者修改数据时，如果stuid的值在students表中不存在则会报错
- 在创建表时可以直接创建约束

```
create table scores(
id int primary key auto_increment,
stuid int,
subid int,
score decimal(5,2),
foreign key(stuid) references students(id),
foreign key(subid) references subjects(id)
);
```

#### 外键的级联操作

- 在删除students表的数据时，如果这个id值在scores中已经存在，则会抛异常
- 推荐使用逻辑删除，还可以解决这个问题
- 可以创建表时指定级联操作，也可以在创建表后再修改外键的级联操作
- 语法

```
alter table scores add constraint stu_sco foreign key(stuid) references students(id) on delete cascade;
```

- 级联操作的类型包括：
  - restrict（限制）：默认值，抛异常
  - cascade（级联）：如果主表的记录删掉，则从表中相关联的记录都将被删除
  - set null：将外键设置为空
  - no action：什么都不做

## 连接查询

### 先看个问题

- 问：查询每个学生每个科目的分数
- 分析：学生姓名来源于students表，科目名称来源于subjects，分数来源于scores表，怎么将3个表放到一起查询，并将结果显示在同一个结果集中呢？
- 答：当查询结果来源于多张表时，需要使用连接查询
- 关键：找到表间的关系，当前的关系是
  - students表的id---scores表的stuid
  - subjects表的id---scores表的subid
- 则上面问题的答案是：

```
select students.sname,subjects.stitle,scores.score
from scores
inner join students on scores.stuid=students.id
inner join subjects on scores.subid=subjects.id;
```

- 结论：当需要对有关系的多张表进行查询时，需要使用连接join

### 连接查询

- 连接查询分类如下：
  - 表A inner join 表B：表A与表B匹配的行会出现在结果中
  - 表A left join 表B：表A与表B匹配的行会出现在结果中，外加表A中独有的数据，未对应的数据使用null填充
  - 表A right join 表B：表A与表B匹配的行会出现在结果中，外加表B中独有的数据，未对应的数据使用null填充
- 在查询或条件中推荐使用“表名.列名”的语法
- 如果多个表中列名不重复可以省略“表名.”部分
- 如果表的名称太长，可以在表名后面使用' as 简写名'或' 简写名'，为表起个临时的简写名称

### 练习

- 查询学生的姓名、平均分

```
select students.sname,avg(scores.score)
from scores
inner join students on scores.stuid=students.id
group by students.sname;
```

- 查询男生的姓名、总分

```
select students.sname,avg(scores.score)
from scores
inner join students on scores.stuid=students.id
where students.gender=1
group by students.sname;
```

- 查询科目的名称、平均分

```
select subjects.stitle,avg(scores.score)
from scores
inner join subjects on scores.subid=subjects.id
group by subjects.stitle;
```

- 查询未删除科目的名称、最高分、平均分

```
select subjects.stitle,avg(scores.score),max(scores.score)
from scores
inner join subjects on scores.subid=subjects.id
where subjects.isdelete=0
group by subjects.stitle;
```

## 子查询



- 查询支持嵌套使用
- 查询各学生的语文、数学、英语的成绩

### 什么是子查询

 当一个查询是另一个查询的条件时,这个查询称之为子查询(内层查询)

 什么时候用？

 当查询需求比较复杂，一次性查询无法得到结果，需要多次查询时，

 例如：给出一个部门名称，需要获得该部门所有的员工信息

 分析：

 1.需要先确定部门的id

 2.然后才能通过id确定员工

 解决问题的方式是把一个复杂的问题拆分为若干个简单的问题

###### 2. 如何使用？

首先明确子查询就是一个普通的查询,当一个查询需要作为子查询使用时,用括号包裹即可

###### 3. 需要注意

 in中的子查询只能包含一个列

 例如：查询财务部有哪些人

 正确的写法：select name from emp where dept_id in (select id from dept where name = "财务");

 错误的写法：select name from emp where dept_id in (select * from dept where name = "财务");

#### 关键字：exists

exists后跟子查询，子查询有结果是为True，没有结果时为False。为True时外层执行，为False外层不执行

##### 如何使用？

select *from emp where exists (select* from emp where salary > 1000);

前面 exists 后面 如果 *后面* 查询有结果时，*前面* 才会执行



## 视图

- 对于复杂的查询，在多次使用后，维护是一件非常麻烦的事情
- 解决：定义视图
- 视图本质就是对查询的一个封装
- 定义视图

```
create view stuscore as 
select students.*,scores.score from scores
inner join students on scores.stuid=students.id;
```

- 视图的用途就是查询

```
select * from stuscore;
```

### 操作

```
-- 查询视图内容等同于查询表操作
SELECT * from bookallinfo where cataory = '历史传记';
-- 视图实现模糊查找
SELECT * from bookallinfo where bookname like "%小%";

-- 更新多字段
UPDATE booktable SET bookname = "小时代1",authorid=0,score = NULL  where id = 2;

-- 删除
-- 逻辑删除和物理删除

-- 逻辑删除小时代书
UPDATE booktable set isdelete = "true" where id = 2

-- 物理删除
-- DELETE from booktable WHERE bookname = "鬼吹灯"
DELETE from booktable
```

##  子查询

- 查询支持嵌套使用
- 查询各学生的语文、数学、英语的成绩

### 什么是子查询

 当一个查询是另一个查询的条件时,这个查询称之为子查询(内层查询)

 什么时候用？

 当查询需求比较复杂，一次性查询无法得到结果，需要多次查询时，

 例如：给出一个部门名称，需要获得该部门所有的员工信息

 分析：

 1.需要先确定部门的id

 2.然后才能通过id确定员工

 解决问题的方式是把一个复杂的问题拆分为若干个简单的问题

###### 2. 如何使用？

首先明确子查询就是一个普通的查询,当一个查询需要作为子查询使用时,用括号包裹即可

###### 3. 需要注意

 in中的子查询只能包含一个列

 例如：查询财务部有哪些人

 正确的写法：select name from emp where dept_id in (select id from dept where name = "财务");

 错误的写法：select name from emp where dept_id in (select * from dept where name = "财务");

#### 关键字：exists

exists后跟子查询，子查询有结果是为True，没有结果时为False。为True时外层执行，为False外层不执行

##### 如何使用？

select *from emp where exists (select* from emp where salary > 1000);

前面 exists 后面 如果 *后面* 查询有结果时，*前面* 才会执行