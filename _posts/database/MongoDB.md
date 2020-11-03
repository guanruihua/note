---
title: mongodb
layout: about
date: 2020-09-05 13:44:02
tags: 
 - javascript
 - mongodb
 - node
 - Robo 3T
 - database
---

# MongoDB

> [ 安装过程](https://blog.csdn.net/qq_41127332/article/details/80755595)
>
> [可视化工具 Robo 3T](https://robomongo.org/)
>
> [mongoDB](https://www.mongodb.com/)
>
> - `mongod` 启动数据库
> - [使用文档](http://mongoosejs.net/docs/guide.html)

**MongoDB**是一个开源、高性能、无模式的文档型数据库，当初的设计就是用于简化开发和方便扩展，是NoSQL数据库产品中的一种。是最像关系型数据库（MySQL）的非关系型数据库。

它支持的数据结构非常松散，是一种类似于 JSON 的 格式叫**BSON**，所以它既可以存储比较复杂的数据类型，又相当的灵活。

MongoDB中的记录是一个文档，它是一个由字段和值对（fifield:value）组成的数据结构。MongoDB文档类似于JSON对象，即一个文档认 为就是一个对象。字段的数据类型是字符型，它的值除了使用基本的一些类型外，还可以包括其他文档、普通数组和文档数组

## 体系结构

MySQL和MongoDB对比

<img src="https://gitee.com/heguangchuan/rainmeter/raw/master/img/mongo/txjg.png" alt="image" style="zoom:50%;" />

## 术语

相关术语对比

![image](https://gitee.com/heguangchuan/rainmeter/raw/master/img/mongo/shuyu.png)

## 数据模型

MongoDB的最小存储单位就是文档(document)对象。文档(document)对象对应于关系型数据库的行。数据在MongoDB中以 BSON（Binary-JSON）文档的格式存储在磁盘上。

BSON（Binary Serialized Document Format）是一种类json的一种二进制形式的存储格式，简称Binary JSON。BSON和JSON一样，支持 内嵌的文档对象和数组对象，但是BSON有JSON没有的一些数据类型，如Date和BinData类型。

BSON采用了类似于 C 语言结构体的名称、对表示方法，支持内嵌的文档对象和数组对象，具有轻量性、可遍历性、高效性的三个特点，可 以有效描述非结构化数据和结构化数据。这种格式的优点是灵活性高，但它的缺点是空间利用率不是很理想。

Bson中，除了基本的JSON类型：string,integer,boolean,double,null,array和object，mongo还使用了特殊的数据类型。这些类型包括 date,object id,binary data,regular expression 和code。每一个驱动都以特定语言的方式实现了这些类型，查看你的驱动的文档来获取详 细信息。

BSON数据类型参考列表：

![image](https://gitee.com/heguangchuan/rainmeter/raw/master/img/mongo/sjlx.png)

## [安装和使用](https://segmentfault.com/a/1190000008387379)

### 启动mongodb

```cmd
D:\software\MongoDB\server\bin>mongod --dbpath D:\software\MongoDB\server\data\db
```

然后通过cmd命令界面输入指令`mongod`



### 浏览器打开查看

[http://127.0.0.1:27017](http://127.0.0.1:27017/)



## mongdb使用

### 常用指令

| 指令                   | 作用                     |
| :--------------------- | ------------------------ |
| db                     | 查看当前使用使用的数据库 |
| show dbs               | 查看全部数据库           |
| show tables/collection | 查看已有集合             |
| db.col.find()          | 查看col集合已经插入文档  |



### 创建数据库use

```
语法:use DATABASE_NAME`

eg: use mydb//没有就创建,有就切换到该数据库
```

### 删除数据库dropDatabase()

```shell
语法:db.dropDatabase()
> use mydb//先切换到改数据库
> db.dropDatabase()//再删除
```

### 创建集合Collection

```shell
语法:db.createCollection(name[集合名], options[指定内存大小,索引选项等])

//1.创建aa集合
> use test 
> db.createCollection("aa"){"ok":1}

//2.带有参数创建集合mycol		[整个集合空间大小 6142800 KB, 文档最大个数为 10000 个]
> use test
> db.createCollection("mycol", { capped : true, autoIndexId : true, size : 6142800, max : 10000 } ){ "ok" : 1 }

//3.不用创建集合,插入一些文档时，MongoDB 会自动创建集合。
> use test
> db.mycol2.insert({"name": "grh"});
```

#### options参数

| 字段        | 类型 | 描述                                                         |
| :---------- | :--- | :----------------------------------------------------------- |
| capped      | 布尔 | （可选）如果为 true，则创建固定集合。固定集合是指有着固定大小的集合，当达到最大值时，它会自动覆盖最早的文档。 **当该值为 true 时，必须指定 size 参数。** |
| autoIndexId | 布尔 | （可选）如为 true，自动在 _id 字段创建索引。默认为 false。   |
| size        | 数值 | （可选）为固定集合指定一个最大值，以千字节计（KB）。 **如果 capped 为 true，也需要指定该字段。** |
| max         | 数值 | （可选）指定固定集合中包含文档的最大数量。                   |

### 删除集合drop

```\
语法: db.collection.drop()
>	use mydb
	switched to db mydb
>	show collections
  mycol
  mycol2
  system.indexes
>	db.mycol2.drop()
  true
```

### 插入文档

```shell
语法: 	db.COLLECTION_NAME.insert(document) 或 db.COLLECTION_NAME.save(document)
				db.collection.insertOne()		[插入一条] 和 db.collection.insertMany()		[插入多条]
				
        db.collection.insertOne(
           <document>,
           {
              writeConcern: <document>
           }
        )

        db.collection.insertMany(
           [ <document 1> , <document 2>, ... ],
           {
              writeConcern: <document>,
              ordered: <boolean>
           }
        )


```

### 更新文档

```
update()  和  save() 方法
语法:
	db.collection.update(
   <query>,
   <update>,
   {
     upsert: <boolean>,
     multi: <boolean>,
     writeConcern: <document>
   }
	)
	
	db.collection.save(
   <document>,
   {
     writeConcern: <document>//可选,抛出异常的级别
   }
	)

//update()
>db.col.update({'title':'MongoDB 教程'},{$set:{'title':'MongoDB'}})//更新一条文档
WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 })   # 输出信息
>>db.col.update({'title':'MongoDB 教程'},{$set:{'title':'MongoDB'}},{multi:true})//加这个属性可以更新多条相同的文档


//save()
>db.col.save({
    "_id" : ObjectId("56064f89ade2f21f36b03136"),
    "title" : "MongoDB",
    "description" : "MongoDB 是一个 Nosql 数据库",
    "by" : "Runoob",
    "url" : "http://www.runoob.com",
    "tags" : [
            "mongodb",
            "NoSQL"
    ],
    "likes" : 110
})//替换了_id为56064f89ade2f21f36b03136的数据

>db.col.find().pretty()查看替换后的数据
```



### 删除文档

```json
语法:
//remove()已经过时了
db.collection.remove(
   <query>,//可选）删除的文档的条件。
   {
     justOne: <boolean>,//（可选）如果设为 true 或 1，则只删除一个文档，如果不设置该参数，或使用默认值 false，则删除所有匹配条件的文档。
     writeConcern: <document>//（可选）抛出异常的级别。
   }
)

>db.col.remove({'title':'MongoDB'})//删除文档
> db.repairDatabase()
或者
> db.runCommand({ repairDatabase: 1 })才会释放磁盘空间

//deleteMany() 和 deleteOne()
>db.inventory.deleteMany({ status : "A" })//删除多个
>db.inventory.deleteOne( { status: "D" } )//删除一个
```



### 查询文档



```json
语法： db.collection.find(query, projection)
qurey：可选, 使用操作符指定查询条件
projection: 可选, 查询文档中所有键值,
pretty()方法:易读方式读取数据

> db.col.find().pretty()
{
        "_id" : ObjectId("56063f17ade2f21f36b03133"),
        "title" : "MongoDB 教程",
        "description" : "MongoDB 是一个 Nosql 数据库",
        "by" : "grh",
        "url" : "http://www.runoob.com",
        "tags" : [
                "mongodb",
                "database",
                "NoSQL"
        ],
        "likes" : 100
}



```

| 操作       | 格式         | 范例                                        | RDBMS中的类似语句       |
| :--------- | :----------- | :------------------------------------------ | :---------------------- |
| 等于       | `{:`}        | `db.col.find({"by":"菜鸟教程"}).pretty()`   | `where by = '菜鸟教程'` |
| 小于       | `{:{$lt:}}`  | `db.col.find({"likes":{$lt:50}}).pretty()`  | `where likes < 50`      |
| 小于或等于 | `{:{$lte:}}` | `db.col.find({"likes":{$lte:50}}).pretty()` | `where likes <= 50`     |
| 大于       | `{:{$gt:}}`  | `db.col.find({"likes":{$gt:50}}).pretty()`  | `where likes > 50`      |
| 大于或等于 | `{:{$gte:}}` | `db.col.find({"likes":{$gte:50}}).pretty()` | `where likes >= 50`     |
| 不等于     | `{:{$ne:}}`  | `db.col.find({"likes":{$ne:50}}).pretty()`  | `where likes != 50`     |

#### and条件

```json
>db.col.find({key1:value1, key2:value2}).pretty()
> db.col.find({"by":"菜鸟教程", "title":"MongoDB 教程"}).pretty()
//相当于WHERE by='菜鸟教程' AND title='MongoDB 教程'
```

#### or条件

```json
关键字：$or
>db.col.find(
   {
      $or: [
         {key1: value1}, {key2:value2}
      ]
   }
).pretty()
```



#### AND 和 OR 联合使用

```shell
>db.col.find({
	"likes": {$gt:50}, 
		$or: [
			{"by": "菜鸟教程"},
			{"title": "MongoDB 教程"}
			]}).pretty()
```

### 条件控制符

```shell
$gt -------- greater than  >
$gte --------- gt equal  >=
$lt -------- less than  <
$lte --------- lt equal  <=
$ne ----------- not equal  !=
$eq  --------  equal  =

用法:db.col.find({likes : {$gt : 100}})等同于Select * from col where likes > 100;
```

### 模糊查询

```shell
查询 title 包含"教"字的文档：
	db.col.find({title:/教/})
查询 title 字段以"教"字开头的文档：
	db.col.find({title:/^教/})
查询 titl e字段以"教"字结尾的文档：
	db.col.find({title:/教$/})
```



### $type操作符

| **类型**                | **数字**              |
| :---------------------- | :-------------------- |
| Double                  | 1                     |
| String                  | 2                     |
| Object                  | 3                     |
| Array                   | 4                     |
| Binary data             | 5                     |
| Undefined(已废弃)       | 6                     |
| Object id               | 7                     |
| Boolean                 | 8                     |
| Date                    | 9                     |
| Null                    | 10                    |
| Regular Expression      | 11                    |
| JavaScript              | 13                    |
| Symbol                  | 14                    |
| JavaScript (with scope) | 15                    |
| 32-bit integer          | 16                    |
| Timestamp               | 17                    |
| 64-bit integer          | 18                    |
| Min key                 | 255(Query with `-1`.) |
| Max key                 | 127                   |

```shell
db.col.find({"title" : {$type : 2}})
或
db.col.find({"title" : {$type : 'string'}})
```

### Limit与Skip方法

#### Limit

> 指定返回数据的组数

```
>db.COLLECTION_NAME.find().limit(NUMBER)
> db.col.find({},{"title":1,_id:0}).limit(2)//显示两条数据
```

#### Skip

> 跳过数据

```shell
>db.COLLECTION_NAME.find().limit(NUMBER).skip(NUMBER)
>db.col.find({},{"title":1,_id:0}).limit(1).skip(1)//显示第二条数据
```



### 排序

#### sort()方法

> 1:	升序
>
> -1:	降序

```shell
>db.COLLECTION_NAME.find().sort({KEY:1})

>db.col.find({},{"title":1,_id:0}).sort({"likes":-1})
```

### 索引

> 索引可以提高查询的效率

#### createIndex()方法

```shell
>db.collection.createIndex(keys, options)

>db.col.createIndex({"title":1})
>db.col.createIndex({"title":1,"description":-1})//复合索引
```



### 索引操作

```
查看集合索引:db.col.getIndexes();
查看集合索引大小:db.col.totalIndexSize()
删除所有的索引:db.col.dropIndexes()
删除指定索引:db.col.dropIndex("索引名称")
```









##### createIndex() 接收可选参数

| Parameter          | Type          | Description                                                  |
| :----------------- | :------------ | :----------------------------------------------------------- |
| background         | Boolean       | 建索引过程会阻塞其它数据库操作，background可指定以后台方式创建索引，即增加 "background" 可选参数。 "background" 默认值为**false**。 |
| unique             | Boolean       | 建立的索引是否唯一。指定为true创建唯一索引。默认值为**false**. |
| name               | string        | 索引的名称。如果未指定，MongoDB的通过连接索引的字段名和排序顺序生成一个索引名称。 |
| dropDups           | Boolean       | **3.0+版本已废弃。**在建立唯一索引时是否删除重复记录,指定 true 创建唯一索引。默认值为 **false**. |
| sparse             | Boolean       | 对文档中不存在的字段数据不启用索引；这个参数需要特别注意，如果设置为true的话，在索引字段中不会查询出不包含对应字段的文档.。默认值为 **false**. |
| expireAfterSeconds | integer       | 指定一个以秒为单位的数值，完成 TTL设定，设定集合的生存时间。 |
| v                  | index version | 索引的版本号。默认的索引版本取决于mongod创建索引时运行的版本。 |
| weights            | document      | 索引权重值，数值在 1 到 99,999 之间，表示该索引相对于其他索引字段的得分权重。 |
| default_language   | string        | 对于文本索引，该参数决定了停用词及词干和词器的规则的列表。 默认为英语 |
| language_override  | string        | 对于文本索引，该参数指定了包含在文档中的字段名，语言覆盖默认的language，默认值为 language. |



### 聚合

#### aggregate()方法

> 计算数量

```shell
>db.COLLECTION_NAME.aggregate(AGGREGATE_OPERATION)
> db.mycol.aggregate([{$group : {_id : "$by_user", num_tutorial : {$sum : 1}}}])
```

| 表达式    | 描述                                           | 实例                                                         |
| :-------- | :--------------------------------------------- | :----------------------------------------------------------- |
| $sum      | 计算总和。                                     | db.mycol.aggregate([{$group : {_id : "$by_user", num_tutorial : {$sum : "$likes"}}}]) |
| $avg      | 计算平均值                                     | db.mycol.aggregate([{$group : {_id : "$by_user", num_tutorial : {$avg : "$likes"}}}]) |
| $min      | 获取集合中所有文档对应值得最小值。             | db.mycol.aggregate([{$group : {_id : "$by_user", num_tutorial : {$min : "$likes"}}}]) |
| $max      | 获取集合中所有文档对应值得最大值。             | db.mycol.aggregate([{$group : {_id : "$by_user", num_tutorial : {$max : "$likes"}}}]) |
| $push     | 在结果文档中插入值到一个数组中。               | db.mycol.aggregate([{$group : {_id : "$by_user", url : {$push: "$url"}}}]) |
| $addToSet | 在结果文档中插入值到一个数组中，但不创建副本。 | db.mycol.aggregate([{$group : {_id : "$by_user", url : {$addToSet : "$url"}}}]) |
| $first    | 根据资源文档的排序获取第一个文档数据。         | db.mycol.aggregate([{$group : {_id : "$by_user", first_url : {$first : "$url"}}}]) |
| $last     | 根据资源文档的排序获取最后一个文档数据         | db.mycol.aggregate([{$group : {_id : "$by_user", last_url : {$last : "$url"}}}]) |



> - $project：修改输入文档的结构。可以用来重命名、增加或删除域，也可以用于创建计算结果以及嵌套文档。
> - $match：用于过滤数据，只输出符合条件的文档。$match使用MongoDB的标准查询操作。
> - $limit：用来限制MongoDB聚合管道返回的文档数。
> - $skip：在聚合管道中跳过指定数量的文档，并返回余下的文档。
> - $unwind：将文档中的某一个数组类型字段拆分成多条，每条包含数组中的一个值。
> - $group：将集合中的文档分组，可用于统计结果。
> - $sort：将输入文档排序后输出。
> - $geoNear：输出接近某一地理位置的有序文档。
>
> eg:
>
> ```
> db.article.aggregate(
>     { $project : {
>         title : 1 ,
>         author : 1 ,
>     }}
>  );
> ```

### 分片

> 存储海量的数据时，一台机器可能不足以存储数据，也可能不足以提供可接受的读写吞吐量。这时，我们就可以通过在多台机器上分割数据，使得数据库系统能存储和处理更多的数据。
>
> 为什么使用分片
>
> - 复制所有的写入操作到主节点
> - 延迟的敏感数据会在主节点查询
> - 单个副本集限制在12个节点
> - 当请求量巨大时会出现内存不足。
> - 本地磁盘不足
> - 垂直扩展价格昂贵

实例:

```
接口结构
Shard Server 1：27020
Shard Server 2：27021
Shard Server 3：27022
Shard Server 4：27023
Config Server ：27100
Route Process：40000
```

#### 步骤一:	启动Shard Server

```shell
[root@100 /]# mkdir -p /www/mongoDB/shard/s0
[root@100 /]# mkdir -p /www/mongoDB/shard/s1
[root@100 /]# mkdir -p /www/mongoDB/shard/s2
[root@100 /]# mkdir -p /www/mongoDB/shard/s3
[root@100 /]# mkdir -p /www/mongoDB/shard/log
[root@100 /]# /usr/local/mongoDB/bin/mongod --port 27020 --dbpath=/www/mongoDB/shard/s0 --logpath=/www/mongoDB/shard/log/s0.log --logappend --fork
....
[root@100 /]# /usr/local/mongoDB/bin/mongod --port 27023 --dbpath=/www/mongoDB/shard/s3 --logpath=/www/mongoDB/shard/log/s3.log --logappend --fork
```

#### 步骤二:	启动Config Server

```shell
[root@100 /]# mkdir -p /www/mongoDB/shard/config
[root@100 /]# /usr/local/mongoDB/bin/mongod --port 27100 --dbpath=/www/mongoDB/shard/config --logpath=/www/mongoDB/shard/log/config.log --logappend --fork
```

**注意：**这里我们完全可以像启动普通mongodb服务一样启动，不需要添加—shardsvr和configsvr参数。因为这两个参数的作用就是改变启动端口的，所以我们自行指定了端口就可以。

#### 步骤三:	启动Route Process

```shell
/usr/local/mongoDB/bin/mongos --port 40000 --configdb localhost:27100 --fork --logpath=/www/mongoDB/shard/log/route.log --chunkSize 500
```

mongos启动参数中，chunkSize这一项是用来指定chunk的大小的，单位是MB，默认大小为200MB.

#### 步骤四:	配置Sharding

使用MongoDB Shell登录到mongos，添加Shard节点

```
[root@100 shard]# /usr/local/mongoDB/bin/mongo admin --port 40000
MongoDB shell version: 2.0.7
connecting to: 127.0.0.1:40000/admin
mongos> db.runCommand({ addshard:"localhost:27020" })
{ "shardAdded" : "shard0000", "ok" : 1 }
......
mongos> db.runCommand({ addshard:"localhost:27029" })
{ "shardAdded" : "shard0009", "ok" : 1 }
mongos> db.runCommand({ enablesharding:"test" }) #设置分片存储的数据库
{ "ok" : 1 }
mongos> db.runCommand({ shardcollection: "test.log", key: { id:1,time:1}})
{ "collectionsharded" : "test.log", "ok" : 1 }
```

#### 步骤五： 程序代码内无需太大更改，直接按照连接普通的mongo数据库那样，将数据库连接接入接口40000

----



### 备份(mongodump)和恢复(mongorestore)

#### 数据备份

```
>mongodump -h dbhost -d dbname -o dbdirectory
```

| 操作符 | 解释                                                         |
| ------ | ------------------------------------------------------------ |
| -h     | MongDB所在服务器地址，例如：127.0.0.1，当然也可以指定端口号：127.0.0.1:27017 |
| -d     | 需要备份的数据库实例，例如：test                             |
| -0     | 备份的数据存放位置，例如：c:\data\dump，当然该目录需要提前建立，在备份完成后，系统自动在dump目录下建立一个test目录，这个目录里面存放该数据库实例的备份数据。 |

>  接到ip为 127.0.0.1 端口号为 27017 的MongoDB服务上，并备份所有数据到 bin/dump/ 目录中

<img src="https://images.gitee.com/uploads/images/2020/0531/225458_3729a629_6545143.png" style="zoom: 67%;" />

| 语法                                              | 描述                           | 实例                                             |
| :------------------------------------------------ | :----------------------------- | :----------------------------------------------- |
| mongodump --host HOST_NAME --port PORT_NUMBER     | 该命令将备份所有MongoDB数据    | mongodump --host runoob.com --port 27017         |
| mongodump --dbpath DB_PATH --out BACKUP_DIRECTORY |                                | mongodump --dbpath /data/db/ --out /data/backup/ |
| mongodump --collection COLLECTION --db DB_NAME    | 该命令将备份指定数据库的集合。 | mongodump --collection mycol --db test           |

#### 数据恢复

```
>mongorestore -h <hostname><:port> -d dbname <path>
```

> - --host <:port>, -h <:port>：
>
>   MongoDB所在服务器地址，默认为： localhost:27017
>
> - --db , -d ：
>
>   需要恢复的数据库实例，例如：test，当然这个名称也可以和备份时候的不一样，比如test2
>
> - --drop：
>
>   恢复的时候，先删除当前数据，然后恢复备份的数据。就是说，恢复后，备份后添加修改的数据都会被删除，慎用哦！
>
> - <path>：
>
>   mongorestore 最后的一个参数，设置备份数据所在位置，例如：c:\data\dump\test。
>
>   你不能同时指定 <path> 和 --dir 选项，--dir也可以设置备份目录。
>
> - --dir：
>
>   指定备份的目录
>
>   你不能同时指定 <path> 和 --dir 选项。

<img src="https://images.gitee.com/uploads/images/2020/0531/225514_d8ccbb6e_6545143.png" style="zoom:50%;" />

----



### Node.js

#### 安装MongoDB模块

```cmd
npm install mongoose --save
```

#### 创建数据库

```js
var MongoClient = require('mongodb').MongoClient;
var url = "mongodb://localhost:27017/runoob";
 
MongoClient.connect(url, { useNewUrlParser: true }, function(err, db) {
  if (err) throw err;
  console.log("数据库已创建!");
  db.close();
});
```

#### 创建集合

```js
var MongoClient = require('mongodb').MongoClient;
var url = 'mongodb://localhost:27017/runoob';
MongoClient.connect(url, { useNewUrlParser: true }, function (err, db) {
    if (err) throw err;
    console.log('数据库已创建');
    var dbase = db.db("runoob");
    dbase.createCollection('site', function (err, res) {
        if (err) throw err;
        console.log("创建集合!");
        db.close();
    });
});
```

#### 数据库操作CURD

##### 插入一条数据

```js
var MongoClient = require('mongodb').MongoClient;
var url = "mongodb://localhost:27017/";
 
MongoClient.connect(url, { useNewUrlParser: true }, function(err, db) {
    if (err) throw err;
    var dbo = db.db("runoob");
    var myobj = { name: "菜鸟教程", url: "www.runoob" };
    dbo.collection("site").insertOne(myobj, function(err, res) {
        if (err) throw err;
        console.log("文档插入成功");
        db.close();
    });
});
```

##### 插入多条数据

```js
var MongoClient = require('mongodb').MongoClient;
var url = "mongodb://localhost:27017/";
 
MongoClient.connect(url, { useNewUrlParser: true }, function(err, db) {
    if (err) throw err;
    var dbo = db.db("runoob");
    var myobj =  [
        { name: '菜鸟工具', url: 'https://c.runoob.com', type: 'cn'},
        { name: 'Google', url: 'https://www.google.com', type: 'en'},
        { name: 'Facebook', url: 'https://www.google.com', type: 'en'}
       ];
    dbo.collection("site").insertMany(myobj, function(err, res) {
        if (err) throw err;
        console.log("插入的文档数量为: " + res.insertedCount);
        db.close();
    });
});
```

##### 查询数据

```js
var MongoClient = require('mongodb').MongoClient;
var url = "mongodb://localhost:27017/";
 
MongoClient.connect(url, { useNewUrlParser: true }, function(err, db) {
    if (err) throw err;
    var dbo = db.db("runoob");
    dbo.collection("site"). find({}).toArray(function(err, result) { // 返回集合中所有数据
        if (err) throw err;
        console.log(result);
        db.close();
    });
});
```



##### 查询指定条件数据

```js
var MongoClient = require('mongodb').MongoClient;
var url = "mongodb://localhost:27017/";
 
MongoClient.connect(url, { useNewUrlParser: true }, function(err, db) {
    if (err) throw err;
    var dbo = db.db("runoob");
     var whereStr = {"name":'菜鸟教程'};  // 查询条件
    dbo.collection("site").find(whereStr).toArray(function(err, result) {
        if (err) throw err;
        console.log(result);
        db.close();
    });
});
```



##### 更新数据

```js
var MongoClient = require('mongodb').MongoClient;
var url = "mongodb://localhost:27017/";
 
MongoClient.connect(url, { useNewUrlParser: true }, function(err, db) {
    if (err) throw err;
    var dbo = db.db("runoob");
    var whereStr = {"name":'菜鸟教程'};  // 查询条件
    var updateStr = {$set: { "url" : "https://www.runoob.com" }};
    dbo.collection("site").updateOne(whereStr, updateStr, function(err, res) {
        if (err) throw err;
        console.log("文档更新成功");
        db.close();
    });
});
```



##### 更新多条数据

```js
var MongoClient = require('mongodb').MongoClient;
var url = "mongodb://localhost:27017/";
 
MongoClient.connect(url, { useNewUrlParser: true }, function(err, db) {
    if (err) throw err;
    var dbo = db.db("runoob");
    var whereStr = {"type":'en'};  // 查询条件
    var updateStr = {$set: { "url" : "https://www.runoob.com" }};
    dbo.collection("site").updateMany(whereStr, updateStr, function(err, res) {
        if (err) throw err;
         console.log(res.result.nModified + " 条文档被更新");
        db.close();
    });
});
```





##### 删除数据

```js
var MongoClient = require('mongodb').MongoClient;
var url = "mongodb://localhost:27017/";
 
MongoClient.connect(url, { useNewUrlParser: true }, function(err, db) {
    if (err) throw err;
    var dbo = db.db("runoob");
    var whereStr = {"name":'菜鸟教程'};  // 查询条件
    dbo.collection("site").deleteOne(whereStr, function(err, obj) {
        if (err) throw err;
        console.log("文档删除成功");
        db.close();
    });
});
```



##### 删除多条数据

```js
var MongoClient = require('mongodb').MongoClient;
var url = "mongodb://localhost:27017/";
 
MongoClient.connect(url, { useNewUrlParser: true }, function(err, db) {
    if (err) throw err;
    var dbo = db.db("runoob");
    var whereStr = { type: "en" };  // 查询条件
    dbo.collection("site").deleteMany(whereStr, function(err, obj) {
        if (err) throw err;
        console.log(obj.result.n + " 条文档被删除");//obj.result.n 删除的条数
        db.close();
    });
});
```

##### 排序

> ```js
> { type: 1 }  // 按 type 字段升序
> { type: -1 } // 按 type 字段降序
> ```

```js
var MongoClient = require('mongodb').MongoClient;
var url = "mongodb://localhost:27017/";
 
MongoClient.connect(url, { useNewUrlParser: true }, function(err, db) {
    if (err) throw err;
    var dbo = db.db("runoob");
    var mysort = { type: 1 };
    dbo.collection("site").find().sort(mysort).toArray(function(err, result) {
        if (err) throw err;
        console.log(result);
        db.close();
    });
});
```



##### 查询分页

###### limit():读取两条数据

```js

var MongoClient = require('mongodb').MongoClient;
var url = "mongodb://localhost:27017/";
 
MongoClient.connect(url, { useNewUrlParser: true }, function(err, db) {
    if (err) throw err;
    var dbo = db.db("runoob");
    dbo.collection("site").find().limit(2).toArray(function(err, result) {
        if (err) throw err;
        console.log(result);
        db.close();
  });
});
```

###### skip():跳过前两条数据,读取两条数据

```js
var MongoClient = require('mongodb').MongoClient;
var url = "mongodb://localhost:27017/";
 
MongoClient.connect(url, { useNewUrlParser: true }, function(err, db) {
    if (err) throw err;
    var dbo = db.db("runoob");
    dbo.collection("site").find().skip(2).limit(2).toArray(function(err, result) {
        if (err) throw err;
        console.log(result);
        db.close();
  });
});
```



#### 连接操作:$lookup左连接

集合1:orders

```js
[
  { _id: 1, product_id: 154, status: 1 }
]
```

集合2:products

```js
[
  { _id: 154, name: '笔记本电脑' },
  { _id: 155, name: '耳机' },
  { _id: 156, name: '台式电脑' }
]
```

左连接:

```js
var MongoClient = require('mongodb').MongoClient;
var url = "mongodb://127.0.0.1:27017/";
 
MongoClient.connect(url, { useNewUrlParser: true }, function(err, db) {
  if (err) throw err;
  var dbo = db.db("runoob");
  dbo.collection('orders').aggregate([
    { $lookup:
       {
         from: 'products',            // 右集合
         localField: 'product_id',    // 左集合 join 字段
         foreignField: '_id',         // 右集合 join 字段
         as: 'orderdetails'           // 新生成字段（类型array）
       }
     }
    ]).toArray(function(err, res) {
    if (err) throw err;
    console.log(JSON.stringify(res));
    db.close();
  });
});
```



#### 删除集合

```js
var MongoClient = require('mongodb').MongoClient;
var url = "mongodb://localhost:27017/";
 
MongoClient.connect(url, { useNewUrlParser: true }, function(err, db) {
    if (err) throw err;
    var dbo = db.db("runoob");
    // 删除 test 集合
    dbo.collection("test").drop(function(err, delOK) {  // 执行成功 delOK 返回 true，否则返回 false
        if (err) throw err;
        if (delOK) console.log("集合已删除");
        db.close();
    });
});
```

















连接

app.js

```javascript
var mongoose = require('mongoose');            
mongoose.connect('mongodb://localhost/blog')     //连接本地数据库blog 
var db = mongoose.connection;
// 连接成功
db.on('open', function(){
    console.log('MongoDB Connection Successed');
});
// 连接失败
db.on('error', function(){
    console.log('MongoDB Connection Error');
});
```

