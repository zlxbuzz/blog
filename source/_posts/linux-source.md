title: linux常用笔记
date: 2014-12-10 15:07:16
categories: linux
tags: linux
---
##压缩命令
```c
tar zxvf aaa.tar.gz #解压
tar zcvf aaa.tar.gz aaa #压缩
```

##查看端口的占用情况
```c
lsof -i:80  #查看80端口
lsof #查看本地网络服务活动状态
```

##查看Linux内核版本或发布版本
```c
lsb_release -a
uname -a
```

##查看端口
```c
netstat –tlnp
netstat -an
```
