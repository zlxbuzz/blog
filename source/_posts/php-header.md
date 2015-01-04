title: php header函数的详解
date: 2014-12-08 18:30:44
categories: php
tags: [php,header]
---
####发送一个原始 HTTP 标头[Http Header]到客户端。标头 (header) 是服务器以 HTTP 协义传 HTML 资料到浏览器前所送出的字串，在标头与 HTML 文件之间尚需空一行分隔
```php
Header(“Location: http://www.php100.com”;);
exit; //在每个重定向之后都必须加上“exit”,避免发生错误后，继续执行。
?>
```

####禁止页面在IE中缓存
```php
header( ‘Expires: Mon, 26 Jul 1997 05:00:00 GMT’ );
header( ‘Last-Modified: ‘ . gmdate( ‘D, d M Y H:i:s’ ) . ‘ GMT’ );
header( ‘Cache-Control: no-store, no-cache, must-revalidate’ );
header( ‘Cache-Control: post-check=0, pre-check=0′, false );
header( ‘Pragma: no-cache’ ); //兼容http1.0和https
?>
CacheControl = no-cache
Pragma=no-cache
Expires = -1
```
####实现文件下载
```php
header('Content-Type: application/octet-stream');//设置内容类型
header('Content-Disposition: attachment; filename="example.zip"'); //设置MIME用户作为附件下载 如果将attachment换成inline意思为在线打开
header('Content-Transfer-Encoding: binary');//设置传输方式
header('Content-Length: '.filesize('example.zip'));//设置内容长度
　　// load the file to send:
readfile('example.zip');//读取需要下载的文件
```
####向浏览器发送Status标头，
```php
// ok
header(‘HTTP/1.1 200 OK’);

//设置一个404头:
header(‘HTTP/1.1 404 Not Found’);

//设置地址被永久的重定向
header(‘HTTP/1.1 301 Moved Permanently’);


HTTP/1.x 200 OK
Date: Thu, 03 Aug 2006 07:49:11 GMT
Server: Apache/2.0.55 (Win32) PHP/5.0.5
X-Powered-By: PHP/5.0.5
Status: 404 Not Found
Content-Length: 0
Keep-Alive: timeout=15, max=98
Connection: Keep-Alive
Content-Type: text/html
```

####注意
•Location和":"之间不能有空格，否则会出现错误（注释：我刚测试了，在我本地环境下，没有跳转页面，但是也没有报错，不清楚什么原因）；
•在用header前不能有任何的输出（注释：这点大家都知道的，如果header之前有任何的输出，包括空白，就会出现header already sent by xxx的错误）；
•header 后面的东西还会执行的；
