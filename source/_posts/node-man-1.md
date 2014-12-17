title: Node.js 核心模块方法
date: 2014-12-15 11:52:34
categories: node
tags: [node]
---
##模块
####核心模块

核心模块是被编译成二进制代码，引用的时候只需require表示符即可
####os 系统基本信息

os模块可提供操作系统的一些基本信息

1.返回系统临时目录
```js
    os.tmpdir() 
    结果如: C:\Users\ADMINI~1\AppData\Local\Temp
```

2.返回 CPU 的字节序，可能的是 “BE” 或 “LE”
```js
    os.endianness()
    结果如: LE (inter i3)
```
3.返回操作系统的主机名
```js
    os.hostname()
    结果如: QH-20141006HJKT
```
4.返回操作系统名称
```js
    os.type()
    结果如: Windows_NT
```
5.返回操作系统平台
```js
    os.platform()
    结果如: win32
```
6.返回操作系统 CPU 架构，可能的值有 “x64"、"arm” 和 “ia32”
```js
    os.arch()
    结果如: x64
```
7.返回操作系统的发行版本
```js
    os.release()
    结果如: 6.1.7601
```
8.返回操作系统运行的时间，以秒为单位
```js
    os.uptime()
    结果如: 7847.6797442
```
9.返回一个包含 1、5、15 分钟平均负载的数组
```js
    os.loadavg()
    结果如: 6.1.7601
```
10.返回系统内存总量，单位为字节
```js
    os.totalmem()
    结果如: 3931602944
```
11.返回操作系统空闲内存量，单位是字节
```js
    os.freemem()
    结果如: 1307422720
```
12.返回一个对象数组，包含所安装的每个 CPU/内核的信息：型号、速度（单位 MHz）、时间（一个包含 user、nice、sys、idle 和 irq 所使用 CPU/内核毫秒数的对象）
```js
    os.cpus()
```
13.获取网络接口的一个列表信息
```js
    os.networkInterfaces() 结果如: 1307422720
```
14.一个定义了操作系统的一行结束的标识的常量
```js
    os.EOL
```

####process 进程管理

process 是一个全局变量.无需 require;

1.返回应用程序当前目录
```js
    process.cwd() 结果如: c:\Users\Administrator\MongoDb_Test
```
2.改变应用程序目录
```js
    process.chdir(“目录”)
```
3.标准输出流.将内容打印到输出设备上.console.log就是封装了它
```js
    process.stdout.write(‘aa\n’) 结果如: aa
```
4.标准错误流
```js
    process.stderr.write(‘aa\n’) 结果如: aa
```
5.进程的输入流. 通过注册事件的方式来获取输入的内容
```js
    process.stdin.on('readable’, function() { var chunk = process.stdin.read(); if (chunk !== null) { process.stdout.write('data: ' + chunk); } });
```
6.结束进程
```js
    process.exit(code);
```
参数code为退出后返回的代码，如果省略则默认返回0

7.注册事件
```js
    process.stdout.on('data’,function(data){ console.log(data); });
```
8.为事件循环设置一项任务,Node.js 会在下次事件循环调响应时调用 callback
```js
    process.nextTick(callback)
```
9.设置编码, 默认 utf8. node.js编码格式只支持UTF8、ascii、base64，暂时不支持GBK、gb2312
```js
    process.stdin.setEncoding(编码); process.stdout.setEncoding(编码); process.stderr.setEncoding(编码);
```
####fs 文件管理

fs 模块提供了异步和同步2个版本 fs.readFile() fs.readFileSync()

1.写入文件内容
```js
    fs.writeFile('test.txt’, ‘Hello Node’ , [encoding], [callback]);
```
2.追加写入
```js
    fs.appendFile('test.txt’,’Hello Node’,[encoding],[callback]);
```
3.文件是否存在
```js
    fs.exists('test.txt’,[callback]);
```
4.修改文件名
```js
    fs.rename(旧文件,新文件,[callback]);
```
5.移动文件. 没有专门函数,通过修改文件名可以达到目的
```js
    fs.rename(oldPath,newPath,[callback]);
```
6.读取文件内容
```js
    fs.readFile('test.txt’, [encoding], [callback]);
```
7.删除文件
```js
    fs.unlink('test.txt’, [callback]);
```
8.创建目录
```js
    fs.mkdir(路径, 权限, [callback]); 路径：新创建的目录。 权限：可选参数，只在linux下有效，表示目录的权限，默认为0777，表示文件所有者、文件所有者所在的组的用户、所有用户，都有权限进行读、写、执行的操作。
```
9.删除目录
```js
    fs.rmdir(path, [callback]);
```
10.读取目录. 读取到指定目录下所有的文件
```js
    fs.readdir(path, [callback]);
```
11.打开文件
```js
    fs.open(path,flags, [mode], [callback(err,fd)])
```
12.关闭文件
```js
    fs.close(fd, [callback(err)]) fd 是打开文件后的标示符
```
13.读取文件
```js
    fs.read(fd,buffer,offset,length,position,[callback(err, bytesRead, buffer)])
```
14.写入文件
```js
    fs.writeFile(filename, data,[encoding],[callback(err)])
```
15.获取真实路径
```js
    fs.realpath(path, [callback(err,resolvedPath)])
```
16.更改所有权
```js
    fs.chown(path, uid, gid, [callback(err)])
```
17.更改权限
```js
    fs.fchmod(fd, mode, [callback(err)])
```
18.获取文件信息
```js
    fs.stat(path, [callback(err, stats)])
```
19.创建硬链接
```js
    fs.link(srcpath, dstpath, [callback(err)])
```
20.读取链接
```js
    fs.readlink(path, [callback(err,linkString)])
```
21.修改文件时间戳
```js
    fs.utimes(path, atime, mtime, [callback(err)])
```
22.同步磁盘缓存
```js
    fs.fsync(fd, [callback(err)])
```
####url 文件管理

1.解析url，返回一个json格式的数组
```js
    url.parse(‘http://www.baidu.com’);

结果如: { protocol: 'http:’, slashes: null, auth: null, host: null, port: null, hostname: null, hash: null, search: null, query: null, pathname: 'www.baidu.com’, path: 'www.baidu.com’, href: ‘http://www.baidu.com’ }
```
2.解析url - 条件解析
```js
    url.parse('http://www.baidu.com?page=1’,true); 结果如: { protocol: 'http:’, slashes: true, auth: null, host: 'www.baidu.com’, port: null, hostname: 'www.baidu.com’, hash: null, search: '?page=1’,

query: { page: ‘1’ }, pathname: '/’, path: '/?page=1’, href: ‘http://www.baidu.com/?page=1’ }
```
3.解析主机
```js
    url.parse('http://www.baidu.com/news’,false,true); 结果如:{ protocol: 'http:’, slashes: true, auth: null, host: 'www.baidu.com’, port: null, hostname: 'www.baidu.com’, hash: null, search: null, query: null, pathname: '/news’, path: '/news’, href: ‘http://www.baidu.com/news’ }
```
4.格式化为url. 将json数组逆向成url
```js
    url.format({ protocol: 'http:’, hostname:’www.baidu.com’, port:’80’, pathname :’/news’, query:{page:1} }); 结果如: http://www.baidu.com/news?page=1
```
5.封装路径
```js
    url.resolve('http://example.com/’, ‘/one’) // ‘http://example.com/one’ url.resolve('http://example.com/one’, ‘/two’) // ‘http://example.com/two’
```
####path 路径管理

用于处理和转换文件路径的工具集,用于处理目录的对象

1.格式化路径. 将不符合规范的路径经过格式化转换为标准路径,解析路径中的.与…外，还能去掉多余的斜杠
```js
    path.normalize(‘/path///normalize/hi/…’); 结果如: ‘/path/normalize/’ 标准化之后的路径里的斜杠在Windows系统下是，而在Linux系统下是/
```
2.组合路径
```js
    path.join('///you’, '/are’, ‘//beautiful’); 结果如: ‘/you/are/beautiful’
```
3.返回路径中的目录名
```js
    path.dirname(‘/foo/strong/cool/nice’); 结果如: ‘/foo/strong/cool’
```
4.返回路径最后一部分,还可以排除指定字符串
```js
    path.basename(‘/foo/strong/basename/index.html’); path.basename(‘/foo/strong/basename/index.html’,’.html’); 结果如: index.html 和 index
```
5.返回路径后缀
```js
    path.extname(‘index.html’); 结果如: .html
```
####Query String 字符串转换

用于实现URL参数字符串与参数对象之间的互相转换

1.序列化对象.将对象类型转换成一个字符串类型（默认的分割符（“&”）和分配符（“=”））
```js
    querystring.stringify({foo:’bar’,cool:['xux’, ‘yys’]}); 结果如: foo=bar&cool=xux&cool=yys

    重载1: querystring.stringify({foo:’bar’,cool:[‘xux’, ‘yys’]},’*’,’$’); 结果如: foo$bar*cool$xux*cool$yys
```
2.反序列化
```js
    querystring.parse('foo@bar$cool@xux$cool@yys‘,’@’,’$’); 结果如: { foo: ‘bar’ , cool: ['xux’, ‘yys’] }
```

####util 使用工具

提供常用函数的集合，用于弥补核心JavaScript的一些功能过于精简的不足。并且还提供了一系列常用工具，用来对数据的输出和验证

1.任意对象转化为字符串,用于调试输出
```js
    util.inspect(object,[showHidden],[depth],[colors])
```
2.格式化字符串. 就像c语言的 printf函数 支持的占位符有：“%s(字符串)”、“%d(数字<整型和浮点型>)”、“%j(JSON)”、“%(单独一个百分号则不作为一个参数)”
```js
    util.format('%s:%s’, ‘foo’); 结果如: foo:%s

    util.format('%s:%s’, 'foo’, 'bar’, ‘baz’); 结果如: foo:bar baz 额外的参数将会调用util.inspect()转换为字符串连接在一起

    util.format(1, 2, 3); 结果如: 1 2 3 , 第一个参数是一个非格式化字符串，则会把所有的参数转成字符串并以空格隔开拼接在一块
```
3.验证函数
```js
    util.isArray(object); 判断对象是否为数组类型，是则返回ture,否则为false

    util.isDate(object); 判断对象是否为日期类型，是则返回ture,否则返回false

    util.isRegExp(object); 判断对象是否为正则类型，是则返回ture,否则返回false ,util.isArray()、util.isRegExp()、util.isDate()、util.isError() util.format()、util. debug()
```
4.继承
```js
    util.inherits( 子类, 基类) 实现对象间原型继承
```
child_process 子进程

node.js是基于单线程模型架构，这样的设计可以带来高效的CPU利用率，但是无法却利用多个核心的CPU，为了解决这个问题，node.js提供了child_process模块，通过多进程来实现对多核CPU的利用. child_process模块提供了四个创建子进程的函数，分别是spawn，exec，execFile和fork

1.用给定的命令发布一个子进程，带有‘args’命令行参数

    child_process.spawn(command, [args], [options]) command {String}要运行的命令行 args {Array} 字符串参数列表 options {Object} cwd {String} 子进程的当前的工作目录 stdio {Array|String} 子进程 stdio 配置. (参阅下文) customFds {Array} Deprecated 作为子进程 stdio 使用的 文件标示符. (参阅下文) env {Object} 环境变量的键值对 detached {Boolean} 子进程将会变成一个进程组的领导者. (参阅下文) uid {Number} 设置用户进程的ID. (See setuid(2).) gid {Number} 设置进程组的ID. (See setgid(2).) 返回: {ChildProcess object}

2.创建子进程

    child_process.exec(command, [options], callback)

3.创建进程 - 直接运行指定文件

    child_process.execFile( file);

4.直接运行Node.js模块

    child_process.fork( modulePath ); fork函数只支持运行JavaScript代码

http HTTP

2个方法

    http.createServer([requestListener]) 创建HTTP服务器 http.createClient([port], [host]) 创建HTTP客户端

http.Server

由 http.createServer 创建所返回的实例

http.Server 事件

    request 客户端请求到来 提供2个参数: req, res 分别是http.ServerRequest 和 http.ServerResponse 的实例.表示请求和响应消息

    connection TCP建立连接时触发 提供1个 socket 参数 net.Socket 实例

    close 服务器关闭时触发 无参数

    还有checkContinue 、 upgrade 、 clientError 等事件. request 经常使用,所以包含在了 createServer函数中

http.ServerRequest 对象 HTTP请求的消息, 一般由 http.Server的 request 事件发送

属性: complete 客户端请求是否已经发送完成 httpVersion HTTP 协议版本，通常是 1.0 或 1.1 method HTTP 请求方法，如 GET、POST、PUT、DELETE 等 url 原始的请求路径，例如 /static/image/x.jpg 或 /user?name=byvoid headers HTTP 请求头 trailers HTTP 请求尾（不常见） connection 当前 HTTP 连接套接字，为 net.Socket 的实例 socket connection 属性的别名 client client 属性的别名

GET: 的请求是直接嵌入路径中的. 解析?后面的路径就行了. url 模块中 parse 函数提供了这个功能

POST:

**HTTP 请求分: 请求头.  请求体**
http.ServerRequest 提供3个事件控制请求体传输
data:   请求体数据来到时. 参数 chunk 表示接收到的数据
end:    请求体数据传输完成时
close   用户当前请求结束时

    var post = '';
    req.on('data', function(chunk) {    post += chunk;  });
    req.on('end', function() {  post = querystring.parse(post);
    res.end(util.inspect(post));});

http.ServerResponse 对象 http.ServerResponse是返回给客户端的信息,决定了用户最终看到的结果. 有3个重要的成员函数. 用于响应头,响应内容以及结束请求

1.向客户端发送响应头

    res.writeHead(statusCode, [headers]) statusCode, 是HTTP状态码. 如200,404.
    headers 类似数组的对象,表示响应头的每个属性 { "Content-Type": "text/html", "Connection": “keep-alive” }

2.发送响应内容, 如果是字符串,需要制定编码方式, 默认 utf-8

    res.write(data, [encoding])

3.结束响应,告知客户端所有响应完成. 此函数必须调用一次

    res.end([data] , [encoding] )

文件模块

文件模块，则是指js文件、json文件或者是.node文件
无
核心
事件

挂接模块

    var EventEmitter = require(‘events’).EventEmitter;

1.实例化一个EventEmitter对象

    var event = new EventEmitter();

2.注册事件

    emitter.on( ‘Event_Name’ , callBack_Fun ) emitter.once( ‘Event_Name’ , callBack_Fun ) //注册一个单次监听器,触发一次后立刻解除

3.发射事件

    event.emit(‘Event_Name’ , 参数1,参数2);

4.移除事件

    emitter…removeListener(‘Event_Name’ , callBack_Fun) emitter.removeAllListeners( [‘Event_Name’] ) //如果指定了事件名,就移除指定的,否则移除所有事件

模块和包

Node.js 的模块和包机制的实现参照了 CommonJS 的标准，但并未完全遵循。

#### 包
包是在模块基础上更深一步的抽象, 类似于 c/c++ 的函数库.
Node.js 包是一个目录. 其中包含一个JSON格式的说明文件 package.json
CommonJS 规范特征:
->   package.json 必须在包的顶层目录下
->   二进制文件在bin目录下
->   JavaScript代码在lib目录下
->   文档应该在doc目录下
->   单元测试在test目录下




#### require('Modile_Name')     
功能: 加载其他模块
说明: 不会重复加载以加载的模块


#### exports.setName
功能: 公开一个模块中的函数或对象
说明: exports 本身仅仅是一个普通的空对象，即 {}. 所以 exports.函数  就是给它加了函数
    module.exports  则是用一个对象取代 exports  对象. (不可以对 exports 直接赋值替代此功能)

方式1:
    //使用
    exports.SayName = function(thyName) {console.log(thyName)}; 
    //调用
    var test = require('./fileName');
    test.SayName('XueYou');

方式2:
    //使用
    function hello(){
        var name;
        this.setNam(){};
        this.SayName(){};
    }
    module.exports = hello;
    //调用
    var test = require('./fileName');
    test = new test();  //注意因为是对象,所以要new
    test.SayName();

其他
express 与 webstorm 配置

Node interpreter : node.exe 路径 Node parameters : ./bin/www Working directory : 工作目录 JavaScript file : app.js





MongoDb

标签（空格分隔）： 数据库 MongoDb
安装

当前版本 2.X
解压至任意目录,最好不要是c盘. 在根目录下建立一个文件夹用来存储工程
我的例子:
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

Node.js 中使用

1. package.json dependencies对象中加入  "mongodb": "*"
2. 在工程目录下运行 npm install  更新依赖文件
3. 引入

    var Db = require(‘mongodb’).Db; var Connection = require(‘mongodb’).Connection; var Server = require(‘mongodb’).Server; // ‘blog’ 数据库名称 mongodb就是一个Db实例 var mongodb = new Db('blog’, new Server('localhost’, Connection.DEFAULT_PORT, {}));

Db API

属性: serverConfig 拓扑结构, 比如上面实例的 new Server(‘localhost’, Connection.DEFAULT_PORT, {}) bufferMaxEntries 数据库当前缓冲区值
databaseName 当前数据库名称, 比如上面实例的’blog’

API: //将用户添加到该数据库 Db.addUser(username, password, options, callback) //删除用户 Db.removeUser(username, callback) //返回管理员数据库实例 Db.admin() //验证用户 Db.authenticate(username, password, options, callback) //关闭连接 force布尔值,是否强制关闭 Db.close(force, callback) //取一个特定集合 Db.collection(name, options, callback) //获取所有集合 Db.collections(callback) //创建一个集合 Db.createCollection(name, options, callback) //创建索引 Db.createIndex(name, fieldOrSpec, options, callback) //删除集合 Db.dropCollection(name, callback) //删除数据库 Db.dropDatabase(callback) //获取集合中的信息 Db.listCollections(name, options, callback) //打开数据库 Db.open(callback) //登出数据库 Db.logout(options, callback) //统计所有数据 Db.stats(options, callback)

一般使用流程: //打开数据库 Db.open(function(err,db){ //读取集合 db.collection(name,function(err,collection){ //在集合中插入数据 collection.insert({’age’:21,’email’:’xxxx’}, {safe: true}, function(err, user){Db.close();}) })

})

collection API

API: //查询匹配文档的数目 count(query, options, callback) //创建索引 createIndex(fieldOrSpec, options, callback) //删除多个文档 deleteMany(filter, options, callback) //删除一个文档 deleteOne(filter, options, callback) //删除集合 drop(callback) //删除集合中的索引 dropAllIndexes(callback) //删除指定索引 dropIndex(indexName, options, callback) //是否存在索引,不存在就创建 ensureIndex(fieldOrSpec, options, callback) //查询 find(query) //查询第一个 findOne(query, options, callback) //查找和替换文档 findAndModify(query, sort, doc, options, callback) //查找并删除 findAndRemove(query, sort, options, callback) //找到一个文件并删除 findOneAndDelete(filter, options, callback) //找到一个文件并替换 findOneAndReplace(filter, replacement, options, callback) //找到一个文件并更新 findOneAndUpdate(filter, update, options, callback) //所有索引集合 indexes(callback) //检查集合中是否存在索引 indexExists(indexes, callback) //获取此集合的索引信息 indexInformation(options, callback) //批量写 initializeOrderedBulkOp(options, callback)

//插入文档到数据库中 docs 对象或数组, 
insert(docs, options, callback)
实例
inset({'a':1}, {w:1},function(err,data){})

//插入数组
insertMany(docs, options, callback)
//插入一个单个文件
insertOne(doc, options, callback)
//重建索引
reIndex(callback)
//删除文件
remove(selector, options, callback)
//重命名集合
rename(newName, options, callback)
//保存
save(doc, options, callback)
//统计所有数据
stats(options, callback)
//更新集合
update(selector, document, options, callback)

基础
文档

    多个键和值有序的放置在一起便是文档,基本数据单元
    javascript 中,文档表示为对象.
    每个文档都有一个 _id 的键,值在所处集合中是唯一的
    
    有序的:   (下面2个文档完全不同)
    {'title':'xueyou', 'Age':21}
    {'Age':21, 'title':'xueyou'}
    
    语法:
    键不能包含 \0 空字符, 这个字符表示键的结尾
    . 和 $ 有特殊含义,通常保留
    _ 开头的键通常也要保留,虽然不强制
    MongoDb区分类型也区分大小写
    文档不能有重复的键

集合

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

shell

    MongoDb 自带javascript shell;
    可以运行任何javascript程序, DOM和浏览器模型不算
    启动数据库, 进入bin 运行mongo 启动shell
    当前版本 2.6.5
    默认连接 test 数据库, 并将这个数据库赋值给全局变量 db

API helo 获取帮助 exit 退出shell

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

其他

mongod.exe   启动数据库,没参数的时候默认数据目录在 c:\data\dbm
使用27017端口, 同时还会启动一个HTTP服务器,监听比端口号大1000的端口
28017端口. 访问:  http://localhost:28017 可以获取数据库的管理信息





Mongoose 参考手册

标签（空格分隔）： MongoDB
Mongoose 是什么?

一般我们不直接用MongoDB的函数来操作MongoDB数据库 Mongose就是一套操作MongoDB数据库的接口.
Schema

一种以文件形式存储的数据库模型骨架，无法直接通往数据库端，也就是说它不具备对数据库的操作能力.可以说是数据属性模型(传统意义的表结构)，又或着是“集合”的模型骨架

/* 定义一个 Schema */
var mongoose = require("mongoose");

var TestSchema = new mongoose.Schema({
    name : { type:String },//属性name,类型为String
    age  : { type:Number, default:0 },//属性age,类型为Number,默认为0
    time : { type:Date, default:Date.now },
    email: { type:String,default:''}
});

上面这个 TestSchema包含4个属性 [name, age, time, email]
Model

由Schema构造生成的模型，除了Schema定义的数据库骨架以外，还具有数据库操作的行为，类似于管理数据库属性、行为的类

var db = mongoose.connect("mongodb://127.0.0.1:27017/test");

// 创建Model
var TestModel = db.model("test1", TestSchema);

test1 数据库中的集合名称, 不存在会创建.
Entity

由Model创建的实体，使用save方法保存数据，Model和Entity都有能影响数据库的操作，但Model比Entity更具操作性

var TestEntity = new TestModel({
       name : "Lenka",
       age  : 36,
       email: "lenka@qq.com"
});
console.log(TestEntity.name); // Lenka
console.log(TestEntity.age); // 36

游标

MongoDB 使用游标返回find的执行结果.客户端对游标的实现通常能够对最终结果进行有效的控制。可以限制结果的数量，略过部分结果，根据任意键按任意顺序的组合对结果进行各种排序，或者是执行其他一些强的操作。
ObjectId

存储在mongodb集合中的每个文档（document）都有一个默认的主键_id，这个主键名称是固定的，它可以是mongodb支持的任何数据类型，默认是ObjectId。

ObjectId是一个12字节的 BSON 类型字符串。按照字节顺序，依次代表： 4字节：UNIX时间戳 3字节：表示运行MongoDB的机器 2字节：表示生成此_id的进程 3字节：由一个随机数开始的计数器生成的值
Node.js 中

package.json 中加入"mongoose": “*” 字段 npm install 安装依赖.

var mongoose = require("mongoose");
var db = mongoose.connect("mongodb://localhost:27017/test");

然后引用
API

var mongoose = require("mongoose");
var db = mongoose.connect("mongodb://localhost:27017/test");

db - 数据库操作

1.挂接数据库连接事件,参数1: 也可以是error.

    db.connection.on('open’, callback);

Schema - 表结构

1.构造函数

    new mongoose.Schema( { name:{type:String}, age:{type:Number, default:10} } )

2.添加属性

    Schema.add( { name: 'String’, email: 'String’, age: ‘Number’ } )

3.有时候Schema不仅要为后面的Model和Entity提供公共的属性，还要提供公共的方法

    Schema.method( 'say’, function(){console.log(‘hello’);} ) //这样Model和Entity的实例就能使用这个方法了

4.添加静态方法

    Schema.static( 'say’, function(){console.log(‘hello’);} ) //静态方法，只限于在Model层就能使用

5.追加方法

    Schema.methods.say = function(){console.log(‘hello’);}; //静态方法，只限于在Model层就能使用

model - 文档操作

1.构造函数, 参数1:集合名称, 参数2:Schema实例

    db.model("test1", TestSchema );

2.查询, 参数1忽略,或为空对象则返回所有集合文档

    model.find({}, callback);

    model.find({},field,callback); 过滤查询,参数2: {’name’:1, 'age’:0} 查询文档的返回结果包含name , 不包含age.(_id默认是1)

    model.find({},null,{limit:20}); 过滤查询,参数3: 游标操作 limit限制返回结果数量为20个,如不足20个则返回所有.

    model.findOne({}, callback); 查询找到的第一个文档

    model.findById('obj._id’, callback); 查询找到的第一个文档,同上. 但是只接受 __id 的值查询

3.创建, 在集合中创建一个文档

    Model.create(文档数据, callback))

4.更新,参数1:查询条件, 参数2:更新对象,可以使用MondoDB的更新修改器

    Model.update(conditions, update, function(error)

5.删除, 参数1:查询条件

    Model.remove(conditions,callback);

Entity - 文档操作

1.构造函数, 其实就是model的实例

    new TestModel( { name:’xueyou’, age:21 } );

2.创建, 在集合中创建一个文档.

    Entity.save(callback);

修改器和更新器
更新修改器:

‘$inc’ 增减修改器,只对数字有效.下面的实例: 找到 age=22的文档,修改文档的age值自增1

    Model.update({’age’:22}, {’$inc’:{’age’:1} } ); 执行后: age=23

‘$set’ 指定一个键的值,这个键不存在就创建它.可以是任何MondoDB支持的类型.

    Model.update({’age’:22}, {’$set’:{’age’:’haha’} } ); 执行后: age=’haha’

‘$unset’ 同上取反,删除一个键

    Model.update({’age’:22}, {’$unset’:{’age’:’haha’} } ); 执行后: age键不存在

数组修改器:

‘$push’ 给一个键push一个数组成员,键不存在会创建

    Model.update({’age’:22}, {’$push’:{’array’:10} } ); 执行后: 增加一个 array 键,类型为数组, 有一个成员 10

‘$addToSet’ 向数组中添加一个元素,如果存在就不添加

    Model.update({’age’:22}, {’$addToSet’:{’array’:10} } ); 执行后: array中有10所以不会添加

‘$each’ 遍历数组, 和 $push 修改器配合可以插入多个值

    Model.update({’age’:22}, {’$push’:{’array’:{’$each’: [1,2,3,4,5]}} } ); 执行后: array : [10,1,2,3,4,5]

‘$pop’ 向数组中尾部删除一个元素

    Model.update({’age’:22}, {’$pop’:{’array’:1} } ); 执行后: array : [10,1,2,3,4] tips: 将1改成-1可以删除数组首部元素

‘$pull’ 向数组中删除指定元素

    Model.update({’age’:22}, {’$pull’:{’array’:10} } ); 执行后: array : [1,2,3,4] 匹配到array中的10后将其删除

条件查询:

    “$lt” 小于
    “$lte” 小于等于
    “$gt” 大于
    “$gte” 大于等于
    “$ne” 不等于

    Model.find({"age":{ "$get":18 , "$lte":30 } } );

查询 age 大于等于18并小于等于30的文档
或查询 OR:

    ‘$in’ 一个键对应多个值
    ‘$nin’ 同上取反, 一个键不对应指定值
    “$or” 多个条件匹配, 可以嵌套 $in 使用
    “$not” 同上取反, 查询与特定模式不匹配的文档

    Model.find({"age":{ "$in":[20,21,22.’haha’]} } );

查询 age等于20或21或21或’haha’的文档

    Model.find({"$or" : [ {’age’:18} , {’name’:’xueyou’} ] }); 查询 age等于18 或 name等于’xueyou’ 的文档

类型查询:

null 能匹配自身和不存在的值, 想要匹配键的值 为null, 就要通过 “$exists” 条件判定键值已经存在 “$exists” (表示是否存在的意思)

    Model.find(“age” : { “$in” : [null] , “exists” : true } ); 查询 age值为null的文档

Model.find({name: {$exists: true}},function(error,docs){
  //查询所有存在name属性的文档
});

Model.find({telephone: {$exists: false}},function(error,docs){
  //查询所有不存在telephone属性的文档
});

正则表达式:

MongoDb 使用 Prel兼容的正则表达式库来匹配正则表达式

    find( {"name" : /joe/i } )
    查询name为 joe 的文档, 并忽略大小写

    find( {"name" : /joe?/i } ) 查询匹配各种大小写组合

查询数组:

    Model.find({"array":10} ); 查询 array(数组类型)键中有10的文档, array : [1,2,3,4,5,10] 会匹配到

    Model.find({"array[5]":10} ); 查询 array(数组类型)键中下标5对应的值是10, array : [1,2,3,4,5,10] 会匹配到

‘$all’ 匹配数组中多个元素

    Model.find({"array":[5,10]} ); 查询 匹配array数组中 既有5又有10的文档

‘$size’ 匹配数组长度

    Model.find({"array":{"$size" : 3} } ); 查询 匹配array数组长度为3 的文档

‘$slice’ 查询子集合返回

    Model.find({"array":{"$skice" : 10} } ); 查询 匹配array数组的前10个元素

    Model.find({"array":{"$skice" : [5,10] } } ); 查询 匹配array数组的第5个到第10个元素

where

用它可以执行任意javacript语句作为查询的一部分,如果回调函数返回 true 文档就作为结果的一部分返回

    find( {"$where" : function(){
        for( var x in this ){
         //这个函数中的 this 就是文档
        }
        
        if(this.x !== null && this.y !== null){
            return this.x + this.y === 10 ? true : false;
        }else{
            return true;
        }
        
        
}  }  )

简化版本

    find( {"$where" :  "this.x + this.y === 10" } )
    find( {"$where" : " function(){ return this.x + this.y ===10; } " } )

游标:

    limit(3) 限制返回结果的数量,
    skip(3) 跳过前3个文档,返回其余的
    sort( {"username":1 , "age":-1 } ) 排序 键对应文档的键名, 值代表排序方向, 1 升序, -1降序




express

标签（空格分隔）： node.js express [TOC]

安装:

新版本中命令行工具分家了

npm install -g express  //安装 express

然后

npm install -g express-generator    //安装 express 命令行工具

express -V 我现在查看到的版本是 4.9.0 npm start 代替 node app.js 启动
http.Server

    var http = require(‘http’); var server = http.createServer(callback); 返回一个http.Server实例

属性:

    server.maxHeadersCount 最大请求头数目限制, 默认 1000 个. 如果设置为0, 则代表不做任何限制

方法:

    server.listnen(prot) 监听一个端口 server.close(callback) 禁止服务端接收新的连接 server.setTimeout(msecs_Time, callback) 设置套接字的超时值

事件:

    ‘request’ 每收到一个HTTP请求时触发, http.createServer的参数默认就是此事件的处理程序. 提供2个参数: req, res 分别是http.ServerRequest 和 http.ServerResponse 的实例. 表示请求和响应消息
    ‘connection’ 新的TCP建立时触发. 提供1个 socket 参数 net.Socket 实例
    ‘close’ 服务器关闭时触发 无参

http.ServerRequest

HTTP请求的消息, 一般由 http.Server的 request 事件发送. HTTP 请求分: 请求头. 请求体
事件:

    ‘data’ 请求体数据来到时. 参数 chunk 表示接收到的数据 ‘end’ 请求体数据传输完成时 ‘close’ 用户当前请求结束时

属性:

    complete 客户端请求是否已经发送完成 httpVersion HTTP 协议版本，通常是 1.0 或 1.1 method HTTP 请求方法，如 GET、POST、PUT、DELETE 等 url 原始的请求路径，例如 /static/image/x.jpg 或 /user?name=byvoid headers HTTP 请求头 trailers HTTP 请求尾（不常见） connection 当前 HTTP 连接套接字，为 net.Socket 的实例 socket connection 属性的别名 client client 属性的别名 params 多路由控制时的对象

http.ServerResponse

HTTP响应消息是返回给客户端的信息,决定了用户最终看到的结果
函数

    res.writeHead(statusCode, [headers]) 该函数在一次请求中最多调用一次. statusCode, 是HTTP状态码. 如200,404. headers 类似数组的对象,表示响应头的每个属性 res.write(data, [encoding]) 发送响应内容, 如果是字符串,需要制定编码方式, 默认 utf-8 res.end(data, data, [encoding]) 结束响应,告知客户端所有响应完成. 此函数必须调用一次

API

HTTP动词都是Express的方法. post 改、put 增、delete 删、get 查
GET

    GET 根据请求路径来处理客户端发出的GET请求

    app.get(path, [callback(request, response)])

ALL

    ALL 以匹配所有的HTTP动词，也就是说它可以过滤所有路径的请求

    app.all(path, [callback(request, response, next)])

USE

    USE express调用中间件的方法，它返回一个函数. path默认为"/"

    app.use([path], [callback(request, response, next)])

    USE 不仅可以调用中间件,还可以根据请求的网址，返回不同的网页内容

app.use(function(request, response, next) {
   if(request.url == "/") {
      response.send("Welcome to the homepage!");
   }else {
      next();
   }
});

app.use(function(request, response, next) {
   if(request.url == "/about") {
     response.send("Welcome to the about page!");
   }else {
     next();
   }
});
        
app.use(function(request, response) {
  response.send("404 error!");
});

post

    处理指定页面的post请求

    app.post(path,function(req, res));

想要使用 body 需要安装中间件 npm install body-parser npm install multer

调用 var bodyParser = require(‘body-parser’); var multer = require(‘multer’); … app.use(bodyParser.json()); app.use(bodyParser.urlencoded({ extended: true })); app.use(multer());

    req.body 解析客户端的post请求参数
    格式：req.body.参数名；

注意: 表单所发送的 post请求 Accept 和 ajax 的不一样 服务器 send 发回来的数据,ajax是数据, 表单会反映称网页
param/query/params

    获取主机名、路径名.[这里的req就是回调函数中的第一个参数]

    req.host 返回请求头里取的主机名(不包含端口号); req.path 返回请求的URL的路径名 req.query 是一个对象,存储着get请求路径参数的对象属性 www.***.com/shoes?order=desc&shoe[color]=blue&shoe[type]=converse 网址 得到: { order: 'desc’, shoe: { color: 'blue’, type: ‘converse’ } } req.param() 功能同上,不过是函数形式 req.param(‘order’) 返回 desc

// req.param('name') 还可以获取具有相应路由规则的请求对象
app.get("/user/:name/", function(req, res) {
    console.log(req.param("name")); 
    res.send("使用req.param属性获取具有路由规则的参数对象值!");
});

// req.params 同上,但可以匹配复杂命名路由规则的请求
app.get("/user/:name/:id", function(req, res) {
    console.log(req.params.id); 
});

send

    send 方法向浏览器发送一个响应信息，并可以智能处理不同类型的数据 send方法在输出响应时会自动进行一些设置，比如HEAD信息、HTTP缓存支持等等 类型可以是: String, Array, Object, Number. 当参数为一个String时，Content-Type默认设置为"text/html" 当参数为Array或Object时，Express会返回一个JSON 当参数为一个NumberExpress会帮你设置一个响应体，比如：200

set

    app.set('view engine’, ‘ejs’); 设置默认模板引擎 app.engine( '.html’, require( ‘ejs’ ).__express ); 修改模板引擎 "__express"，ejs模块的一个公共属性，表示要渲染的文件扩展名

    app.set('views’, __dirname); 设定views变量，意为视图存放的目录

express.static —— 指定静态文件的查找目录 app.use(express.static(require(‘path’).join(__dirname, ‘public’)));

模板操作: app.set('views’, path.join(__dirname, ‘views’)); app.set('view engine’, ‘html’); app.engine('.html’, require(‘ejs’).__express); 这样模板后缀可以使 .html 但模板代码是ejs代码
render

何对网页模板进行访问. res对象的render函数

    res.render(view, [locals], callback); view 视图名, locals 为模板传入变量

redirect

允许网址的重定向，跳转到指定的url并且可以指定status，默认为302方式 根据指定url来重定向，可以域内路径、网页间跳转也可以跳转至不同域名

    res.redirect([status], url); res.redirect(“login”);

Middleware<中间件>

中间件(middleware)就是处理HTTP请求的函数，用来完成各种特定的任务，比如检查用户是否登录、分析数据、以及其他在需要最终将数据发送给用户之前完成的任务。 它最大的特点就是，一个中间件处理完，可以把相应数据再传递给下一个中间件。

//连续调用2个中间件
app.use(function(request, response, next){
    console.log("method："+request.method+" ==== "+"url："+request.url);
    next();
});

app.use(function(request, response){
    response.writeHead(200, { "Content-Type": "text/html;charset=utf-8" });
    response.end('示例：连续调用两个中间件');
});

由于这种原因,所以调用中间件的顺序非常重要

    设定静态文件目录的访问路径

    express.static(path.join(__dirname, ‘/public’))

    express-session

var session = require('express-session');
app.use(session({
    secret:'secret',
    resave:true,
    saveUninitialized:false,
    cookie:{
        maxAge:1000*60*10  //过期时间设置(单位毫秒)
    }
}));


//新增中间件并设置模板变量值

app.use(function(req, res, next){
    res.locals.user = req.session.user;
    var err = req.session.error;
    res.locals.message = '';
    if (err) res.locals.message = '<div style="margin-bottom: 20px;color:red;">' + err + '</div>';
    next();
});

    body-parser

npm install body-parser
npm install multer

调用
var bodyParser = require('body-parser');
var multer = require('multer');
   ......
app.use(bodyParser.json());
app.use(bodyParser.urlencoded({ extended: true }));
app.use(multer());






ejs 手册

标签（空格分隔）： ejs
express 中使用

//设置模板目录
app.set('views', path.join(__dirname, 'views'));    

//设置模板引擎
app.set('view engine', 'html');

//设置引擎后缀.  index.html 中的内容可以是 ejs 代码
app.engine('.html', require('ejs').__express);

ejs的特性： 1、缓存功能，能够缓存已经解析好的html模版； 2、<% code %>用于执行其中javascript代码； 3、<%= code %>会对code进行html转义； 4、<%- code %>将不会进行转义； 5、支持自定义标签，比如’<%’可以使用’{{’，’%>’用’}}’代替； 6、提供一些辅助函数，用于模版中使用 7、利用<%- include filename %>加载其他页面模版；
ejs 函数/运算符

    引入模板 不指定后缀就寻找 layout.ejs. (注意:如果没有定义模板目录,则 include无效)

    <% include layout.html%> <%- include layout.html%>

    静态编译模板,没有 IO 操作，会非常快，而且可以公用本地变量. <ul>
    <% users.forEach(function(user){ %>
    <% include user/show %>
    <% }) %>
    </ul>
    意思就是模板名是动态的

    自定义 闭合标签. 厌倦了 <% %> ?

//设置闭合标签
var ejs = require('ejs');  
ejs.open = '{{';  
ejs.close = '}}';  

express中全局设定

app.set("view options",{                                                                                  
   "open":"{{",                                                                                  
   "close":"}}"
});

    变量

//传递 index 模板引擎参数
res.render('index',{'title':'haha');

//使用参数
<title><%= title %></title>

    运行js代码

<%for(var i=p.length-1; i>=0; i--){%>
<input type="button" value=<%=p[i]%>>
<%}%>

    选项 express中 通过 res.redirect('login’, [options]); 来对模板进行访问,options就可以设置模板引擎的一些选项 其中options的一些参数为： 1、cache：是否缓存解析后的模版，需要filename作为key； 2、filename：模版文件名； 3、scope：complile后的Function执行所在的上下文环境； 4、debug：标识是否是debeg状态，debug为true则会输出生成的Function内容； 5、compileDebug：标识是否是编译debug，为true则会生成解析过程中的跟踪信息，用于调试； 6、client，标识是否用于浏览器客户端运行，为true则返回解析后的可以单独运行的Function函数； 7、open，代码开头标记，默认为’<%’； 8、close，代码结束标记，默认为’%>’； 9、其他的一些用于解析模版时提供的变量。 在express中使用时，options参数将由response.render进行传入，其中包含了一些express中的设置，以及用户提供的变量值。

    f辅助函数 此外ejs还提供了一些辅助函数，用于代替使用javascript代码，使得更加方便的操纵数据。 1、first，返回数组的第一个元素； 2、last，返回数组的最后一个元素； 3、capitalize，返回首字母大写的字符串； 4、downcase，返回字符串的小写； 5、upcase，返回字符串的大写； 6、sort，排序（Object.create(obj).sort()？）； 7、sort_by:’prop’，按照指定的prop属性进行升序排序； 8、size，返回长度，即length属性，不一定非是数组才行； 9、plus:n，加上n，将转化为Number进行运算； 10、minus:n，减去n，将转化为Number进行运算； 11、times:n，乘以n，将转化为Number进行运算； 12、divided_by:n，除以n，将转化为Number进行运算； 13、join:’val’，将数组用’val’最为分隔符，进行合并成一个字符串； 14、truncate:n，截取前n个字符，超过长度时，将返回一个副本 15、truncate_words:n，取得字符串中的前n个word，word以空格进行分割； 16、replace:pattern,substitution，字符串替换，substitution不提供将删除匹配的子串； 17、prepend:val，如果操作数为数组，则进行合并；为字符串则添加val在前面； 18、append:val，如果操作数为数组，则进行合并；为字符串则添加val在后面； 19、map:’prop’，返回对象数组中属性为prop的值组成的数组； 20、reverse，翻转数组或字符串； 21、get:’prop’，取得属性为’prop’的值； 22、json，转化为json格式字符串

辅助函数使用

//注意闭合标签  <%=:  %>
<input type="button" value=<%=:p|first%>>

    给模板添加方法

    app.locals[‘say’] = function(){ return 'hello’; }; 在 app.locals 中定义的方法都可以在模板中引用 <input type="button" value=<%=say()%>>







