title: php常用笔记
date: 2014-12-10 15:07:16
categories: php
tags: [php,命令行,参数]
---

##PHP内置小型web server
```php
php -S localhost:8080 -t /www #-t 用来指定相关的目录,如果有apache 或  nginx 的重写则失效 支持远程
```

##PHP命令行参数

```php
#!/usr/local/bin/php
echo $_SERVER["argc"]."\n"; #2，为参数的个数
echo $_SERVER["argv"][1]."\n";#a  输入的第一个参数
echo $_SERVER["argv"][2]."\n"; #b 输入的第二个参数
#$_SERVER["argc"]数组返回一个整型的数，代表从命令行上回车后一共输入了几个参数。
#从PHP命令行读取参数范例中的结果已经看出，要访问已经传入的参数值，需要从索引1开始。
#因为脚本本身的文件已经占用了索引0，即$_SERVER["argv"][0]
```
##PHP类型判断

```
+--------------+-----------+---------+-----------+---------+--------+
| 真值表        | gettype() | empty() | is_null() | isset() | (bool) |
+--------------+-----------+---------+-----------+---------+--------+
| $x = ""      | string    | true    | false     | true    | false  |
| $x=null      | NULL      | true    | true      | false   | false  |
| var $x       | NULL      | true    | true      | false   | false  |
| $x = array() | array     | true    | false     | true    | false  |
| $x = false   | boolean   | true    | false     | true    | false  |
| $x = 15      | integer   | false   | false     | true    | true   |
| $x = 1       | integer   | false   | false     | true    | true   |
| $x = 0       | integer   | true    | false     | true    | false  |
| $x = -1      | integer   | false   | false     | true    | true   |
| $x = '15'    | string    | false   | false     | true    | true   |
| $x = '1'     | string    | false   | false     | true    | true   |
| $x = '0'     | string    | true    | false     | true    | false  |
| $x = '-1'    | string    | false   | false     | true    | true   |
| $x = 'foo'   | string    | false   | false     | true    | true   |
| $x = 'true'  | string    | false   | false     | true    | true   |
| $x = 'false' | string    | false   | false     | true    | true   |
+--------------+-----------+---------+-----------+---------+--------+
empty() 和 bool 不可能相等
```

##修改phpunit内存限制
```
phpunit -d memory_limit=512M
```


##php下载远程文件到本地
```php
$url = 'http://picturescdn.qiniudn.com/93aa93787ae02be68192b3533d3e76b0';
$remote_fp = fopen($url,'rb');#指定fopen的打开模式为b(二进制模式)
$local_fp = fopen(date('YmdHis'),'wb');
while(!feof($remote_fp)){
    fwrite($local_fp,fread($remote_fp,128));
}
fclose($remote_fp);
fclose($local_fp);
```

##cURL 常用函数
```php
//初始化
$curlobj=curl_init('http://www.baidu.com');//初始化culr
$curlobj = curl_init();			
curl_setopt($curlobj, CURLOPT_URL, "http://www.baidu.com");// 初始化，两种

//相关常用的option
curl_setopt($curlobj, CURLOPT_RETURNTRANSFER, true);	// 执行之后不直接打印出来，否则会直接输出
$output=curl_exec($curlobj);	// 执行

// 如果模拟cookie登录 要先设置cookie
date_default_timezone_set('PRC'); // 使用Cookie时，必须先设置时区
curl_setopt($curlobj, CURLOPT_COOKIESESSION, 1); 
curl_setopt($curlobj, CURLOPT_HEADER, 0); 
curl_setopt($curlobj, CURLOPT_FOLLOWLOCATION, 1); // 支持页面链接跳转  这个设置必须关闭安全模式 
//以及关闭open_basedir，金额贝尔不过对服务器安全不利

//将数据post
$postdata='username=buzzmjx@126.com&password=123456';
curl_setopt($curlobj, CURLOPT_POST, 1);  //允许post
curl_setopt($curlobj, CURLOPT_POSTFIELDS, $postdata);  //post 数据
curl_setopt($curlobj, CURLOPT_HTTPHEADER, array("application/x-www-form-urlencoded; charset=utf-8",
 "Content-length: ".strlen($postdata))); 

//从ftp下载
curl_setopt($curlobj, CURLOPT_TIMEOUT, 300); // times out after 300s
curl_setopt($curlobj, CURLOPT_USERPWD, "buzzmjx:123456");//FTP用户名：密码
$outfile = fopen('dest.txt', 'wb');//保存到本地的文件名
curl_setopt($curlobj, CURLOPT_FILE, $outfile);

//上传ftp
$fp = fopen('test.php', 'r');
curl_setopt($curlobj, CURLOPT_UPLOAD, 1);
curl_setopt($curlobj, CURLOPT_INFILE, $fp);
curl_setopt($curlobj, CURLOPT_INFILESIZE, filesize($localfile));
$rtn = curl_exec($curlobj);  
 
// 设置HTTPS支持
date_default_timezone_set('PRC'); // 使用Cookie时，必须先设置时区
curl_setopt($curlobj, CURLOPT_SSL_VERIFYPEER, 0); // 对认证证书来源的检查从证书中检查
//SSL加密算法是否存在
curl_setopt($curlobj, CURLOPT_SSL_VERIFYHOST, 2); // 
//webservice
curl_setopt($curlobj, CURLOPT_POSTFIELDS, $data); //data为soapxml 
curl_setopt($curlobj, CURLOPT_HTTPHEADER, array("Content-Type: application/soap+xml; charset=utf-8", 
	"Content-length: ".strlen($data),
"SOAPAction:\"http://WebXml.com.cn/getWeatherbyCityName\"")); 

//关闭
curl_close($curlobj);
```
