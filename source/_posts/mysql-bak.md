title: mysql数据库迁移
date: 2015-04-26 09:59:38
categories: [mysql,数据库]
tags: [mysql,数据库] 
---

##数据迁移前停止mysql服务
```bash
sudi service mysql stop
```                                              
##将目标目录的所属用户组和用户和文件夹权限修改为mysql:mysql  0700
```bash
sudo chown -R mysql:mysql /var/data
sudo chmod -R 700 /var/data
```                                              
##为了防止意外，把现有数据复制(cp)到新目录，而不是移动(mv)，为保证文件的权限和属性一致，复制过程一定要添加 -a 参数，由于数据量比较大添加 –v 参数可查看复制的过程
```bash
cp -av /var/lib/mysql/* var/data
```                                                                                        
##修改my.cnf文件中的datadir参数值
datadir=/var/lib/mysql/ 修改为  /var/data                        
##编辑apparmor关于mysql的权限配置文件
```bash
datadir=/var/lib/mysql/ 修改为 datadir=/var/data
```                                             
##修改usr.sbin.mysqld文件中的数据存储目录的相关权限
```bash
vi /etc/apparmor.d/usr.sbin.mysqld
```
/var/lib/mysql/ r 修改为       	 /var/data/ r                         
/var/lib/mysql/** rwk 修改为    /var/data/** rwk                 
##保存退出后重启apparmor服务
```bash
service apparmor reload
```                                           
##重启apparmor权限服务进程和mysql进程
                                             
