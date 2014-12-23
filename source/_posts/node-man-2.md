title: Node.js MongoDB数据库方法 
date: 2014-12-15 11:52:34
categories: node
tags: [node,mongodb]
---

##MongoDb

####安装

当前版本 2.X
解压至任意目录,最好不要是c盘. 在根目录下建立一个文件夹用来存储工程
    
    安装至:
    d:\mongodb
    建立存储目录
    d:\mongodb\blog
    运行CMD,切入bin目录
    cd  d:\mongodb\bin
    启用数据库
    mongod -dbpath “d:\mongodb\blog”
    这样就完毕了,如果关闭CMD,数据库就会关闭.
    
    建立一个快速启动的bat文件,因为每次启动服务器都是这样的命令
    启动mongodb.bat:
        d:\mongodb\bin\mongod.exe -dbpath d:\mongodb\blog

####Node.js 中使用

1. package.json dependencies对象中加入  "mongodb": "*"
2. 在工程目录下运行 npm install  更新依赖文件
3. 引入
```js
var Db = require(‘mongodb’).Db;
var Connection = require(‘mongodb’).Connection;
var Server = require(‘mongodb’).Server; 
// ‘blog’ 数据库名称 mongodb就是一个Db实例 
var mongodb = new Db('blog’, new Server('localhost’, Connection.DEFAULT_PORT, {}));
```

###Db API

属性: 
`serverConfig`  拓扑结构, 比如上面实例的 new Server(‘localhost’, Connection.DEFAULT_PORT, {}) 
`bufferMaxEntries` 数据库当前缓冲区值
`databaseName `当前数据库名称, 比如上面实例的’blog’

`API:`
//将用户添加到该数据库 
```js
Db.addUser(username, password, options, callback) 
```
//删除用户 
```js
Db.removeUser(username, callback)
```
//返回管理员数据库实例 
```js
Db.admin() 
```
//验证用户 
```js
Db.authenticate(username, password, options, callback)
```
//关闭连接 force布尔值,是否强制关闭
```js
Db.close(force, callback)
```
//取一个特定集合
```js
Db.collection(name, options, callback)
```
//获取所有集合 
```js
Db.collections(callback) 
```
//创建一个集合 
```js
Db.createCollection(name, options, callback) 
```
//创建索引 
```js
Db.createIndex(name, fieldOrSpec, options, callback)
```
//删除集合 
```js
Db.dropCollection(name, callback) 
```
//删除数据库
```js
Db.dropDatabase(callback) 
```
//获取集合中的信息 
```js
Db.listCollections(name, options, callback) 
```
//打开数据库
```js
Db.open(callback)
```
//登出数据库 
```js
Db.logout(options, callback) 
```
//统计所有数据 
```js
Db.stats(options, callback)
```
######一般使用流程:
//打开数据库 
```js
Db.open(function(err,db){
//读取集合 
db.collection(name,function(err,collection){ 
//在集合中插入数据 
collection.insert({’age’:21,’email’:’xxxx’}, {safe: true}, function(err, user){Db.close();}) })
})
```
####collection API

`API: `
//查询匹配文档的数目 
```js
count(query, options, callback) 
```
//创建索引 
```js
createIndex(fieldOrSpec, options, callback) 
```
//删除多个文档
```js
deleteMany(filter, options, callback)
```
//删除一个文档
```js
deleteOne(filter, options, callback) 
```
//删除集合 
```js
drop(callback)
```
//删除集合中的索引
```js
dropAllIndexes(callback)
```
//删除指定索引 
```js
dropIndex(indexName, options, callback)
```
//是否存在索引,不存在就创建 
```js
ensureIndex(fieldOrSpec, options, callback)
```
//查询 
```js
find(query)
```
//查询第一个
```js
findOne(query, options, callback)
```
//查找和替换文档 
```js
findAndModify(query, sort, doc, options, callback)
```
//查找并删除
```js
findAndRemove(query, sort, options, callback)
```
//找到一个文件并删除 
```js
findOneAndDelete(filter, options, callback) 
```
//找到一个文件并替换 
```js
findOneAndReplace(filter, replacement, options, callback)
```
//找到一个文件并更新
```js
findOneAndUpdate(filter, update, options, callback) 
```

//所有索引集合
```js
indexes(callback) 
```
//检查集合中是否存在索引 
```js
indexExists(indexes, callback) 
```
//获取此集合的索引信息 
```js
indexInformation(options, callback) 
```
//批量写 
```js
initializeOrderedBulkOp(options, callback)
```
//插入文档到数据库中 docs 对象或数组, 
```js
insert(docs, options, callback)
实例
inset({'a':1}, {w:1},function(err,data){})
```
//插入数组
```js
insertMany(docs, options, callback)
```
//插入一个单个文件
```js
insertOne(doc, options, callback)
```
//重建索引
```js
reIndex(callback)
```
//删除文件
```js
remove(selector, options, callback)
```
//重命名集合
```js
rename(newName, options, callback)
```
//保存
```js
save(doc, options, callback)
```
//统计所有数据
```js
stats(options, callback)
```
//更新集合
```js
update(selector, document, options, callback)
```
##基础
####文档

    多个键和值有序的放置在一起便是文档,基本数据单元
    javascript 中,文档表示为对象.
    每个文档都有一个 _id 的键,值在所处集合中是唯一的
    
    有序的:   (下面2个文档完全不同)
    {'title':'xueyou', 'Age':21}
    {'Age':21, 'title':'xueyou'}
    
   #### 语法:
    键不能包含 \0 空字符, 这个字符表示键的结尾
    . 和 $ 有特殊含义,通常保留
    _ 开头的键通常也要保留,虽然不强制
    MongoDb区分类型也区分大小写
    文档不能有重复的键

####集合

    看做是表,多个文档组成集合
    
    语法:
    不能包含 \0 空字符
    不能使空串 ""
    不能包含 $
    不能 system 开头.系统保留   
    system.users存储着数据库内用户的信息
    system.namespaces 存储着所有数据库集合的信息

数据库

    多个集合组成数据库. 一个MongoDB实例可以承载多个数据库,每个数据库有独立的权限
    语法:
    不能空串,全部小写,最多64字节,不能特殊字符
    因为数据库名称会变成系统的文件
    数据库保留名称:
    admin -   local   -  config

####shell

    MongoDb 自带javascript shell;
    可以运行任何javascript程序, DOM和浏览器模型不算
    启动数据库, 进入bin 运行mongo 启动shell
    当前版本 2.6.5
    默认连接 test 数据库, 并将这个数据库赋值给全局变量 db

#####API 
`helo` 获取帮助
`exit` 退出shell
```js
db.help() 查看数据库的API
db.foo.help() 查看集合的API

//获取集合
db.getCollection('集合名')


//切换到 foobar数据库,这个时候全局变量 db 就是foobar数据库
switched to db foobar




//插入一个文档到集合中, db.集合名.insert
db.blog.insert(对象)

**查询时shell默认最多显示20个匹配文档**

//返回集合里所有文档
db.blog.find()
//查看集合里的一个文档
db.blog.findOne()
//更新文档
db/blog.update({title:'aa'},文档对象)
//从数据库永久删除文档,无参时删除集合内所有文档
db.blog.remove();
```
####其他

    mongod.exe   启动数据库,没参数的时候默认数据目录在 c:\data\dbm
    使用27017端口, 同时还会启动一个HTTP服务器,监听比端口号大1000的端口
    28017端口. 访问:  http://localhost:28017 可以获取数据库的管理信息

