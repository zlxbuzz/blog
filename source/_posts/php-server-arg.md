title: 如何正确实现PHP命令行读取参数
date: 2014-12-10 15:07:16
categories: php
tags: [php,命令行,参数]
---
PHP在参数的读取上可以用多种方法来实现,如果想实现PHP命令行读取参数，CLI可以从$_SERVER['argc']和$_SERVER['argv'']取得参数的个数和值

比如创建一个`test.php`的文件
```php
#!/usr/local/bin/php
echo $_SERVER["argc"]."\n"; 
echo $_SERVER["argv"][1]."\n";  
echo $_SERVER["argv"][2]."\n";  
```
运行 php test.php a b
结果为:
```c
2
a
b
```
$_SERVER["argc"]数组返回一个整型的数，代表从命令行上回车后一共输入了几个参数。
从PHP命令行读取参数范例中的结果已经看出，要访问已经传入的参数值，需要从索引1开始。因为脚本本身的文件已经占用了索引0，即$_SERVER["argv"][0]
