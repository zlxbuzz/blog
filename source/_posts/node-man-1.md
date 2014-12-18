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


####child_process 子进程

node.js是基于单线程模型架构，这样的设计可以带来高效的CPU利用率，但是无法却利用多个核心的CPU，为了解决这个问题，node.js提供了child_process模块，通过多进程来实现对多核CPU的利用. child_process模块提供了四个创建子进程的函数，分别是spawn，exec，execFile和fork

1.用给定的命令发布一个子进程，带有‘args’命令行参数
```js
    child_process.spawn(command, [args], [options]) command {String}要运行的命令行 args {Array} 字符串参数列表 options {Object} cwd {String} 子进程的当前的工作目录 stdio {Array|String} 子进程 stdio 配置. (参阅下文) customFds {Array} Deprecated 作为子进程 stdio 使用的 文件标示符. (参阅下文) env {Object} 环境变量的键值对 detached {Boolean} 子进程将会变成一个进程组的领导者. (参阅下文) uid {Number} 设置用户进程的ID. (See setuid(2).) gid {Number} 设置进程组的ID. (See setgid(2).) 返回: {ChildProcess object}
```
2.创建子进程
```js
    child_process.exec(command, [options], callback)
```
3.创建进程 - 直接运行指定文件
```js
    child_process.execFile( file);
```
4.直接运行Node.js模块
```js
    child_process.fork( modulePath ); fork函数只支持运行JavaScript代码
```
####http HTTP

2个方法
```js
    http.createServer([requestListener]) 创建HTTP服务器 http.createClient([port], [host]) 创建HTTP客户端
```
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
```js
    var post = '';
    req.on('data', function(chunk) {    post += chunk;  });
    req.on('end', function() {  post = querystring.parse(post);
    res.end(util.inspect(post));});
```
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

####挂接模块
```js
    var EventEmitter = require(‘events’).EventEmitter;
```
1.实例化一个EventEmitter对象
```js
    var event = new EventEmitter();
```
2.注册事件
```js
    emitter.on( ‘Event_Name’ , callBack_Fun ) emitter.once( ‘Event_Name’ , callBack_Fun ) //注册一个单次监听器,触发一次后立刻解除
```
3.发射事件
```js
    event.emit(‘Event_Name’ , 参数1,参数2);
```
4.移除事件
```js
    emitter…removeListener(‘Event_Name’ , callBack_Fun) emitter.removeAllListeners( [‘Event_Name’] ) //如果指定了事件名,就移除指定的,否则移除所有事件
```
##模块和包

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
```js
    exports.SayName = function(thyName) {console.log(thyName)}; 
```
    //调用
    
```js
    var test = require('./fileName');
    test.SayName('XueYou');
```
方式2:
    //使用
```js
    function hello(){
        var name;
        this.setNam(){};
        this.SayName(){};
    }
    module.exports = hello;
```
    //调用
```js
    var test = require('./fileName');
    test = new test();  //注意因为是对象,所以要new
    test.SayName();
```
其他
express 与 webstorm 配置

Node interpreter : node.exe 路径 Node parameters : ./bin/www Working directory : 工作目录 JavaScript file : app.js





