---
title: mongoose
date: 2020-09-05 13:44:02
tags: 
 - javascript
 - mongoose
 - mongodb
 - node
 - database
---


# mongoose

> - [官方api](http://mongoosejs.net/docs/guide.html)
> - 用于编写mongodb相关验证, 转换和逻辑

## 环境搭建

```js
npm init
npm i express --save
npm install mongoose --save
```



## 使用

```js
var express = require("express");
var db = require("mongoose");
var app = express();


//跨域问题处理
app.all('*', function(req, res, next) {
    console.log(req.method);
    res.header("Access-Control-Allow-Origin", "*");
    res.header('Access-Control-Allow-Headers', 'Content-type');
    res.header("Access-Control-Allow-Methods", "PUT,POST,GET,DELETE,OPTIONS,PATCH");
    res.header('Access-Control-Max-Age',1728000);//预请求缓存20天
    next();
});


//链接数据库
var link = db.createConnection("mongodb://localhost:27017/Test");
link.on("open", function (err) {
    if (!err) {
        console.log("数据库连接成功！")
    } else {
        console.log(err);
    }
});

//构建信息数据表
var modelSchema = new db.Schema({
    cont: {type: String},
}, {collection: "msg"});
//绑定表
var model = link.model("msg", modelSchema);

//接口
app.get("/index", function (req, res) {//增
    var count = req.query.cont;
    model.create({cont:count},function (err,doc) {
        res.send("成功")
    })
});
app.listen(8084);
```

### understand mongoose

| Oracle                        | MongoDB          | Mongoose                 |
| ----------------------------- | ---------------- | ------------------------ |
| 数据库实例(database instance) | MongDB实例       | Mongoose                 |
| 模式(schema)                  | 数据库(database) | mongoose                 |
| 表(table)                     | 集合(collection) | 模板(Schema)+模型(Model) |
| 行(row)                       | 文档(document)   | 实例(instance)           |
| rowId                         | _id(document)    | _id                      |
| Join                          | DBRef            | DBRef                    |



## schama

> - 每一个schema都会映射到MongoDb collection
> - 用来定义documents的基本字段和集合

```js
// demo
var mongoose = require('mongoose');
var Schema = mongoose.Schema;
mongoose.connect('mongodb://localhost:27017/test')//连接test数据库

// 给连接绑定成功或失败的提醒
var db = mongoose.connection;
db.on('error', console.error.bind(console, 'connection error'));
db.once('open', function() {
  // connected 成功连接
  
  // 定义schema (colection里面的结构)
  var blogSchema = new Schema({
    title:  String,
    author: String
  });
  
  blogSchema.methods.say = function(){
    console.log(this.title);
	}

  // 继承一个schema
  let Model = mongoose.model('Blog',blogSchema);
  
  // 生成 一个document
  let blog = new Model({
    title : 'mybolg',
    author: 'grh'
	})
	
	// 存放数据
	blog.save((err,apple)=>{
		if(err) return console.log(err);
		blog.say();
		Model.find({author: 'grh'},(err, data) => {
			console.log(data)
		})
	});
})
```



### 模式类型(SchemaType)

> - schamaTypes: String, Number, Date, Buffer, Boolean, Mixed

```js
var schema = new Schema({
  name:    String,
  binary:  Buffer,
  living:  Boolean,
  updated: { type: Date, default: Date.now },
  age:     { type: Number, min: 18, max: 65 },
  mixed:   Schema.Types.Mixed,
  _someId: Schema.Types.ObjectId,
  decimal: Schema.Types.Decimal128,
  array:      [],
  ofString:   [String],
  ofNumber:   [Number],
  ofDates:    [Date],
  ofBuffer:   [Buffer],
  ofBoolean:  [Boolean],
  ofMixed:    [Schema.Types.Mixed],
  ofObjectId: [Schema.Types.ObjectId],
  ofArrays:   [[]],
  ofArrayOfNumbers: [[Number]],
  nested: {
    stuff: { type: String, lowercase: true, trim: true }
  }
})

// example use

var Thing = mongoose.model('Thing', schema);

var m = new Thing;
m.name = 'Statue of Liberty';
m.age = 125;
m.updated = new Date;
m.binary = new Buffer(0);
m.living = false;
m.mixed = { any: { thing: 'i want' } };
m.markModified('mixed');
m._someId = new mongoose.Types.ObjectId;
m.array.push(1);
m.ofString.push("strings!");
m.ofNumber.unshift(1,2,3,4);
m.ofDates.addToSet(new Date);
m.ofBuffer.pop();
m.ofMixed = [1, [], 'three', { four: 5 }];
m.nested.stuff = 'good';
m.save(callback);
```

#### SchemaType选项

> - 全部都可以使用
>   - required : true, 添加required 验证器
>   - default:  任何值或函数 设置此路径默认值。如果是函数，函数返回值为默认值
>   - select: 布尔值, 指定query的默认 projections
>   - validate: 函数 添加一个validator function
>   - get : 使用`Object.defineProperty()` 定义 getter
>   - set : 使用`Object.defineProperty() `定义 setter
>   - alias(mongoose$\leq$4.10.0):定义虚拟值gets/sets 
> - 索引
>   - index : boolean 是否创建索引
>   - unique: boolean 是否创建唯一索引
>   - sparse: boolean 是否创建稀疏属性
> - String 
>   - lowercase: boolean 保存前调用`.toLowerCase()`
>   - uppercase: boolean 保存前调用`.toUpperCase()`
>   - trim: boolean 保存前调用`.trim()`
>   - match : 正则表达式 创建验证器检查值 
>   - enum :  数组 创建验证器检查这个值是否含于给定数组
> - Number:
>   - min : 数值 
>   - max : 数值
>     - 创建验证器检查属性
> - Date
>   - min: Date
>   - max: Date 

```js
var schema1 = new Schema ({
  test: String,
});

var schema2 = new Schema({
  test: { type: String }
})

var schema3 = new Schema({
  test:{
		 type: String,
    lowercase: true,// 保存前全部变成小写
   }
})
```





### 连接(Connections)

> - 连接数据库的方式
>   - `mongoose.connect('mongodb://localhost/myapp');`
>   - `mongoose.connect('mongodb://username:password@host:port/database?options...');`	

#### 操作缓存

> - 不用等待连接建立成功就可以使用Mongoose models

```js
mongoose.connect('mongodb://localhost/myapp')
var MyModel = mongoose.model('test', new Schema({ name: String }))
MyModel.findOne(function(err, result) {/*...*/})

// 禁用缓存 
mongoose.set('bufferCommands', false );
```



#### 连接字符串选项

```javascript
mongoose.connect('mongodb://localhost:27017/test?connectTimeoutMS=1000&bufferCommands=false');
// The above is equivalent to:
mongoose.connect('mongodb://localhost:27017/test', {
  connectTimeoutMS: 1000
  // Note that mongoose will **not** pull `bufferCommands` from the query string
});
```

#### 回调

>  `connect()`接受回调函数, 或返回一个`promise`

```js
mongoose.connect(uri, options, function(error) {
  // Check error in initial connection. There is no 2nd param to the callback.
});

// Or using promises
mongoose.connect(uri, options).then(
  () => { /** ready to use. The `mongoose.connect()` promise resolves to undefined. */ },
  err => { /** handle initial connection error */ }
);
```

#### 多mongos支持

```javascript
// Connect to 2 mongos servers
mongoose.connect('mongodb://mongosA:27501,mongosB:27501', cb);
```

#### 多个连接

```javascript
const conn = mongoose.createConnection('mongodb://[username:password@]host1[:port1][,host2[:port2],...[,hostN[:portN]]][/[database][?options]]', options);

// mongoose.connect() , 可以通过mongoose.connection访问连接
```

### 模型(Models)

> - Models是从Schema编一个来的构造函数
> - 主要用户数据库保存和读取的documnets

```js
var schema = new mongoose.Shema({ name: String })
var Tank = mongoose.model('Tank', schema);
```
#### 保存到数据库

```js
var small = new Tank({ size: 'small' })
small.save((err)=>{
	if(err) return console.log(err)
})

// or

Tank.create({ size: 'small' }, function (err, small) {
  if (err) return handleError(err);
  // saved!
})

// 查询
Tank.find({size: 'small'}).where('createDate').gt(oneYearAgo).exec(callback);
// 删除
Tank.remove({size: 'large'}, function(err) {
	if(err) return console.log(err)
})
```

### 查询

```js
var Person = mongoose.model('Person', yourSchema);

// 查询每个 last name 是 'Ghost' 的 person， select `name` 和 `occupation` 字段
Person.findOne({ 'name.last': 'Ghost' }, 'name occupation', function (err, person) {
  if (err) return handleError(err);
  // Prints "Space Ghost is a talk show host".
  console.log('%s %s is a %s.', person.name.first, person.name.last,
    person.occupation);
});

// 查询每个 last name 是 'Ghost' 的 person
var query = Person.findOne({ 'name.last': 'Ghost' });

// select `name` 和 `occupation` 字段
query.select('name occupation');

// 然后执行查询
query.exec(function (err, person) {
  if (err) return handleError(err);
  // Prints "Space Ghost is a talk show host."
  console.log('%s %s is a %s.', person.name.first, person.name.last,
    person.occupation);
});
```



```javascript
// With a JSON doc
Person.
  find({
    occupation: /host/,
    'name.last': 'Ghost',
    age: { $gt: 17, $lt: 66 },
    likes: { $in: ['vaporizing', 'talking'] }
  }).
  limit(10).
  sort({ occupation: -1 }).
  select({ name: 1, occupation: 1 }).
  exec(callback);

// Using query builder
Person.
  find({ occupation: /host/ }).
  where('name.last').equals('Ghost').
  where('age').gt(17).lt(66).
  where('likes').in(['vaporizing', 'talking']).
  limit(10).
  sort('-occupation').
  select('name occupation').
  exec(callback);
```



### 验证



```javscript
var userSchema = new Schema({
      phone: {
        type: String,
        validate: {
          validator: function(v) {
            return /\d{3}-\d{3}-\d{4}/.test(v);
          },
          message: '{VALUE} is not a valid phone number!'
        },
        required: [true, 'User phone number required']
      }
    });

    var User = db.model('user', userSchema);
    var user = new User();
    var error;

    user.phone = '555.0123';
    error = user.validateSync();
    assert.equal(error.errors['phone'].message,
      '555.0123 is not a valid phone number!');

    user.phone = '';
    error = user.validateSync();
    assert.equal(error.errors['phone'].message,
      'User phone number required');

    user.phone = '201-555-0123';
    // Validation succeeds! Phone number is defined
    // and fits `DDD-DDD-DDDD`
    error = user.validateSync();
    assert.equal(error, null);
```

### 中间件(Middleware)

> - 支持Documnet中间件: 
>
>   - init
>   - validate
>   - save
>   - remove
>
> - 支持query中间件
>
>   - count 
>   - find
>   - findOne
>   - findOneRemove
>   - findOneUpdate
>   - update
>
> - ###### model中间件
>
>   - insertMany
>
> - Aggregate中间件
>   - aggregate

#### Pre

> pre分为串行和并行







### 填充(Populate)

### 鉴别器(Discriminators)

