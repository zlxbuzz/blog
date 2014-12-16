title: postgresql
date: 2014-12-08 15:55:19
categories: postgresql
tags: postgresql
---

最近在用`PostgreSQL`，`PostgreSQL`的七个常用命令，和`MySQL`数据库相比，常用命令的关键词大体一致，不过在细节上还是有很多的不同。
##(1)用户实用程序

`createdb` 创建一个新的`PostgreSQL`的数据库（和SQL语句：`CREATE DATABASE` 相同） 
`createuser` 创建一个新的`PostgreSQL`的用户（和SQL语句：`CREATE USER` 相同） 
`dropdb` 删除数据库 
`dropuser` 删除用户 
`pg_dump` 将`PostgreSQL`数据库导出到一个脚本文件 
`pg_dumpall` 将所有的`PostgreSQL`数据库导出到一个脚本文件 
`pg_restore` 从一个由`pg_dump`或`pg_dumpall`程序导出的脚本文件中恢复`PostgreSQL`数据库 
`psql` 一个基于命令行的`PostgreSQL`交互式客户端程序 
`vacuumdb` 清理和分析一个`PostgreSQL`数据库，它是客户端程序`psql`环境下`SQL`语句`VACUUM`的`shell`脚本封装，二者功能完全相同
##(2)系统实用程序

    1. `pg_ctl` 启动、停止、重启`PostgreSQL`服务（比如：`pg_ctl start` 启动`PostgreSQL`服务，它和`service postgresql start`相同） 
    2. `pg_controldata` 显示`PostgreSQL`服务的内部控制信息 
    3. `psql` 切换到`PostgreSQL`预定义的数据库超级用户`postgres`，启用客户端程序`psql`，并连接到自己想要的数据库，比如说： 
    `psql template1 `
    出现以下界面，说明已经进入到想要的数据库，可以进行想要的操作了。 
```c
    template1=#
```
##(3)在数据库中的一些命令
```c
template1=# \l 查看系统中现存的数据库 
template1=# \q 退出客户端程序psql 
template1=# \c 从一个数据库中转到另一个数据库中，如template1=# \c sales 从template1转到sales 
template1=# \dt 查看表 
template1=# \d 查看表结构 
template1=# \di 查看索引
```
###[基本数据库操作]
1. 创建数据库： `create database` [数据库名]; 
2. 查看数据库列表：` \d `
3. 删除数据库： .` drop database `[数据库名]; 
创建表： create table ([字段名1] [类型1] <references 关联表名(关联的字段名)>;,[字段名2] [类型2],......<,primary key (字段名m,字段名n,...)>;); 
查看表名列表： \d 
查看某个表的状况： \d [表名] 
重命名一个表： alter table [表名A] rename to [表名B]; 
删除一个表： drop table [表名]; ========================================

###[表内基本操作] 
在已有的表里添加字段： `alter table [表名] add column [字段名] [类型]`; 
删除表中的字段：` alter table [表名] drop column [字段名]`; 
重命名一个字段： `alter table [表名] rename column [字段名A] to [字段名B]`; 
给一个字段设置缺省值： `alter table [表名] alter column [字段名] set default [新的默认值]`; 
去除缺省值： `alter table [表名] alter column [字段名] drop default`; 
在表中插入数据： `insert into 表名 ([字段名m],[字段名n],......) values ([列m的值],[列n的值],......)`; 
修改表中的某行某列的数据： `update [表名] set [目标字段名]=[目标值] where [该行特征]`; 
删除表中某行数据： `delete from [表名] where [该行特征]`; 
`delete from [表名];删空整个表 ========================== ==========================`

##(4)PostgreSQL用户认证

`PostgreSQL`数据目录中的pg_hba.conf的作用就是用户认证，可以在`/usr/local/pgsql/data`中找到。 
有以下几个例子可以看看： 
(1)允许在本机上的任何身份连接任何数据库 
`TYPE DATABASE USER IP-ADDRESS IP-MASK METHOD` 
`local all all trust(`无条件进行连接) 
(2)允许IP地址为192.168.1.x的任何主机与数据库sales连接 
`TYPE DATABASE USER IP-ADDRESS IP-MASK METHOD `
`host sales all 192.168.1.0 255.255.255.0 ident sameuser`(表明任何操作系统用户都能够以同名数据库用户进行连接)
##(5)看了那么多，来一个完整的创建`PostgreSQL`数据库用户的示例吧

(1)进入`PostgreSQL`高级用户 
(2)启用客户端程序，并进入`template1`数据库 
`psql template1 `
(3)创建用户 
`template1=# CREATE USER hellen WITH ENCRYPED PASSWORD'zhenzhen' `
(4)因为设置了密码，所以要编辑pg_hba.conf，使用户和配置文件同步。 
在原有记录上面添加md5 
`local all hellen md5 `
(4)使用新用户登录数据库 
```
template1=# \q 
psql -U hellen -d template1 
```
PS：在一个数据库中如果要切换用户，要使用如下命令： 
```
template1=# \!psql -U tk -d template1
```
##(6).设定用户特定的权限

还是要用例子来说明： 
创建一个用户组： 
```
sales=# CREATE GROUP sale; 
```
添加几个用户进入该组 
```
sales=# ALTER GROUP sale ADD USER sale1,sale2,sale3; 
```
授予用户级sale针对表employee和products的SELECT权限 
```
sales=# GRANT SELECT ON employee,products TO GROUP sale; 
```
在sale中将用户user2删除 
```
sales=# ALTER GROUP sale DROP USER sale2;
```
##(7).备份数据库

可以使用pg_dump和pg_dumpall来完成。比如备份sales数据库：
```c
pg_dump sales>/home/tk/pgsql/backup/1.bak
```
备份数据表
```c
pg_dump -h主机 -d数据库名 -t 你的表名 > 你的文件名
```

##(8).复制数据库
```c
CREATE TABLE test_1 AS (SELECT * FROM test_2)
```
由于复制的表没有主键，则需要额外增加主键
```c
ALTER TABLE test_1 ADD CONSTRAINT test_1_pkey PRIMARY KEY (id)
```
说明：复制表(只复制结构,源表名：a 新表名：b)
```c
select * into b from a where 1<>1
```
说明：拷贝表(拷贝数据,源表名：a 目标表名：b)
```c
insert into b(a, b, c) select d,e,f from b;
```
说明：显示文章、提交人和最后回复时间
```c
select a.title,a.username,b.adddate from table a,(select
max(adddate) adddate from table where table.title=a.title) b
```
说明：外连接查询(表名1：a 表名2：b)
```c
select a.a, a.b, a.c, b.c, b.d, b.f from a LEFT OUT JOIN b ON a.a =b.c
```
说明：日程安排提前五分钟提醒
```c
select * from 日程安排 where
datediff('minute',f开始时间,getdate())>5
说明：两张关联表，删除主表中已经在副表中没有的信息
delete from info where not exists ( select * from infobz where
info.infid=infobz.infid )
```

cmd 下postgresql 导入sql数据文件

> psql -h localhost  -d databaseName  -U username -f  filename


##tips
如果用到空间函数
```c
su -postgres
 ``` 
切换到postgres用户下
```c
pg_ctl -D /data/pgsql/ -l /data/pgsql/pgsql.log start 
```
启动数据库
```c
createdb template_postgis
```
创建数据库,此时，该数据库还没有具备空间特性
```c
psql -f /usr/local/pgsql/share/contrib/postgis-1.5/postgis.sql -d template_postgis 
```
执行postgis.sql脚本，创建相关空间数据库相关的函数，类型，操作符等 执行完这个脚本，该数据库就具有了空间特性了
```c    
psql template_postgis
```
连接到创建的空间数据库
```c    
select postgis_full_version(); 
```
查询postgis的版本信息，包含用到的三个库信息
```c
POSTGIS="1.5.4" GEOS="3.3.3-CAPI-1.7.4" PROJ="Rel. 4.8.0, 6 March 2012" LIBXML="2.6.26" USE_STATS
createdb [-U username] -T template_postgis my_spatial_db
```
下次再创建数据库，只要以这个模板就可以了
