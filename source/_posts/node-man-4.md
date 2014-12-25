title: Node.js Express 方法 
date: 2014-12-15 11:52:34
categories: node
tags: [node,express]
---

##express


安装:

新版本中命令行工具分家了

    npm install -g express  //安装 express

然后

    npm install -g express-generator    //安装 express 命令行工具

express -V 我现在查看到的版本是 4.9.0 
npm start 代替 node app.js 启动
##http.Server

    var http = require(‘http’); 
    var server = http.createServer(callback); 返回一个http.Server实例

####属性:

    server.maxHeadersCount 最大请求头数目限制, 默认 1000 个. 如果设置为0, 则代表不做任何限制

####方法:

    server.listnen(prot) 监听一个端口
    server.close(callback) 禁止服务端接收新的连接 
    server.setTimeout(msecs_Time, callback) 设置套接字的超时值

####事件:

    ‘request’ 每收到一个HTTP请求时触发, http.createServer的参数默认就是此事件的处理程序. 提供2个参数: req, res 分别是http.ServerRequest 和 http.ServerResponse 的实例. 表示请求和响应消息
    ‘connection’ 新的TCP建立时触发. 提供1个 socket 参数 net.Socket 实例
    ‘close’ 服务器关闭时触发 无参

##http.ServerRequest
```c
HTTP请求的消息, 一般由 http.Server的 request 事件发送. 
HTTP 请求分: 请求头. 请求体
```    
####事件:

    ‘data’ 请求体数据来到时. 参数 chunk 表示接收到的数据 
    ‘end’ 请求体数据传输完成时 
    ‘close’ 用户当前请求结束时

####属性:

    complete 客户端请求是否已经发送完成
    httpVersion HTTP 协议版本，通常是 1.0 或 1.1
    method HTTP 请求方法，如 GET、POST、PUT、DELETE 等
    url 原始的请求路径，例如 /static/image/x.jpg 或 /user?name=byvoid 
    headers HTTP 请求头
    trailers HTTP 请求尾（不常见） 
    connection 当前 HTTP 连接套接字，为 net.Socket 的实例 
    socket connection 属性的别名 
    client client 属性的别名
    params 多路由控制时的对象

##http.ServerResponse

HTTP响应消息是返回给客户端的信息,决定了用户最终看到的结果
####函数

    res.writeHead(statusCode, [headers]) 该函数在一次请求中最多调用一次. statusCode, 是HTTP状态码. 如200,404. 
    headers 类似数组的对象,表示响应头的每个属性
    res.write(data, [encoding]) 发送响应内容, 如果是字符串,需要制定编码方式, 默认 utf-8
    res.end(data, data, [encoding]) 结束响应,告知客户端所有响应完成. 此函数必须调用一次

##API

HTTP动词都是Express的方法. post 改、put 增、delete 删、get 查
####GET

    GET 根据请求路径来处理客户端发出的GET请求

    app.get(path, [callback(request, response)])

####ALL

    ALL 以匹配所有的HTTP动词，也就是说它可以过滤所有路径的请求

    app.all(path, [callback(request, response, next)])

####USE
 USE express调用中间件的方法，它返回一个函数. path默认为"/"

    app.use([path], [callback(request, response, next)])
USE 不仅可以调用中间件,还可以根据请求的网址，返回不同的网页内容
```js
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
```
####post
处理指定页面的post请求

    app.post(path,function(req, res));

想要使用 body 需要安装中间件 

    npm install body-parser 
    npm install multer

调用

    var bodyParser = require(‘body-parser’); 
    var multer = require(‘multer’);
    … 
    app.use(bodyParser.json());
    app.use(bodyParser.urlencoded({ extended: true })); 
    app.use(multer());

    req.body 解析客户端的post请求参数
    格式：req.body.参数名；

注意: 表单所发送的 post请求 Accept 和 ajax 的不一样 
服务器 send 发回来的数据,ajax是数据, 表单会反映称网页
####param/query/params

    获取主机名、路径名.[这里的req就是回调函数中的第一个参数]

    req.host 返回请求头里取的主机名(不包含端口号); 
    req.path 返回请求的URL的路径名 
    req.query 是一个对象,存储着get请求路径参数的对象属性
    www.***.com/shoes?order=desc&shoe[color]=blue&shoe[type]=converse 网址 
    得到: { order: 'desc’, shoe: { color: 'blue’, type: ‘converse’ } } 
    req.param() 功能同上,不过是函数形式 req.param(‘order’) 返回 desc
```js
// req.param('name') 还可以获取具有相应路由规则的请求对象
app.get("/user/:name/", function(req, res) {
    console.log(req.param("name")); 
    res.send("使用req.param属性获取具有路由规则的参数对象值!");
});

// req.params 同上,但可以匹配复杂命名路由规则的请求
app.get("/user/:name/:id", function(req, res) {
    console.log(req.params.id); 
});
```
####send

    send 方法向浏览器发送一个响应信息，并可以智能处理不同类型的数据 send方法在输出响应时会自动进行一些设置，比如HEAD信息、HTTP缓存支持等等 类型可以是: String, Array, Object, Number. 当参数为一个String时，Content-Type默认设置为"text/html" 当参数为Array或Object时，Express会返回一个JSON 当参数为一个NumberExpress会帮你设置一个响应体，比如：200

####set
```js
app.set('view engine’, ‘ejs’); 设置默认模板引擎 
app.engine( '.html’, require( ‘ejs’ ).__express ); 
修改模板引擎 "__express"，ejs模块的一个公共属性，表示要渲染的文件扩展名

app.set('views’, __dirname); 设定views变量，意为视图存放的目录

express.static —— 指定静态文件的查找目录 app.use(express.static(require(‘path’).join(__dirname, ‘public’)));

模板操作: 
app.set('views’, path.join(__dirname, ‘views’)); 
app.set('view engine’, ‘html’); 
app.engine('.html’, require(‘ejs’).__express); 
这样模板后缀可以使 .html 但模板代码是ejs代码
```
####render

何对网页模板进行访问. res对象的render函数
```js
    res.render(view, [locals], callback); view 视图名, locals 为模板传入变量
```
####redirect

允许网址的重定向，跳转到指定的url并且可以指定status，默认为302方式 根据指定url来重定向，可以域内路径、网页间跳转也可以跳转至不同域名

    res.redirect([status], url); res.redirect(“login”);

####Middleware<中间件>

中间件(middleware)就是处理HTTP请求的函数，用来完成各种特定的任务，比如检查用户是否登录、分析数据、以及其他在需要最终将数据发送给用户之前完成的任务。 它最大的特点就是，一个中间件处理完，可以把相应数据再传递给下一个中间件。
```js
//连续调用2个中间件
app.use(function(request, response, next){
    console.log("method："+request.method+" ==== "+"url："+request.url);
    next();
});

app.use(function(request, response){
    response.writeHead(200, { "Content-Type": "text/html;charset=utf-8" });
    response.end('示例：连续调用两个中间件');
});
```
#####由于这种原因,所以调用中间件的顺序非常重要

设定静态文件目录的访问路径
```js
    express.static(path.join(__dirname, ‘/public’))
```
    express-session
```js
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
```
body-parser
```js
npm install body-parser
npm install multer

调用
var bodyParser = require('body-parser');
var multer = require('multer');
   ......
app.use(bodyParser.json());
app.use(bodyParser.urlencoded({ extended: true }));
app.use(multer());
```
