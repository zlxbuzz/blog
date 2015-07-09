title: HTTP Basic Authentication
date: 2015-06-11 17:34:58
categories: php
tags: php
---
类似于路由器登陆的弹出框，打开地址就是一个对话框，可以输入用户名和密码。主要是在访问一个需要`HTTP Basic Authentication`的`URL`的时候，如果没有提供用户名和密码，服务器就会返回`401`。如果直接在浏览器中打开此`URL`，服务器可以通过向客户端浏览器发送`Authentication Required`信息，使其弹出一个用户名／密码输入窗口。
server端
```php
if (!isset($_SERVER['PHP_AUTH_USER'])) {
    header('WWW-Authenticate: Basic realm="haha"');
    header('HTTP/1.0 401 Unauthorized');
    echo 'Text to send if user hits Cancel button';
    exit;
} 
else {
    if($_SERVER['PHP_AUTH_USER'] === '123' && $_SERVER['PHP_AUTH_PW'] === '321') {
        echo "hello world"; 
    }else{

    header('WWW-Authenticate: Basic realm="My Realm"');
    header('HTTP/1.0 401 Unauthorized');
    echo 'Text to send if user hits Cancel button';
    exit;
    }
}

```

客户端可以通过`curl`，`fsocket`等测试，这里采用简单的`curl`测试

```bash
curl -s http://123:321@localhost  //返回 hello world

```

以下为转载
```php
$fp = fsockopen("www.example.com", 80, $errno, $errstr, 30);
$out = "GET / HTTP/1.1\r\n";
$out .= "Host: www.example.com\r\n";
$out .= "Authorization: Basic " . base64_encode("user:pass") . "\r\n";
fwrite($fp, $out);
while (!feof($fp)) {
    echo fgets($fp, 128);
}
fclose($fp);

/*AJAX的话可以用setRequestHeader,注意这里要写到open()的后面。不然chrome下会报错

xhr.setRequestHeader("Authorization", "Basic base64加密的字符串");//字符串格式："用户名:密码
*/

```
