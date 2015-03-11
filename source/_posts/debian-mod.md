title: debian下启动apache的相应模块
date: 2015-03-04 17:20:33
categories: [debian,linux,apache]
tags: [debian,linux]
---
####在apache的配置目录里，有两个文件夹

```c
/etc/apache2/mods-enabled/ #已经被启用的模块

/etc/apache2/mods-available/ #当前系统中可用的模块 
```
通过以下两个指令来启动或者停用

```c
a2enmod 模块名

a2dismod 模块名 
```
