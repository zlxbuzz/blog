title: php常用笔记
date: 2014-12-10 15:07:16
categories: php
tags: [php,命令行,参数]
---
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
