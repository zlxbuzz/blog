title: linux常用笔记
date: 2014-12-10 15:07:16
categories: linux
tags: linux
---
##网络状态
```c
netstat -an |grep ESTABLISHED |wc -l #查看网络连接状态
```
##压缩命令
```c
支持tar,tar.gz：
	tar zxvf aaa.tar.gz #解压
	tar zcvf aaa.tar.gz aaa #压缩
	-c:建立新的存档
	-x:解压
	-v:详细内容
	-f:指定存档或设备	
zip:
	unzip FileName.zip
	zip FileName.zip DirName
	
.gz
gzip 源文件（压缩成.gz的压缩文件，源文件会消失）
gzip -c 源文件 > 压缩文件（压缩为.gz格式，源文件保留）
gzip -r 目录(压缩目录下所有的子文件，但是不能压缩目录)
```

##查看端口的占用情况
```c
lsof -i:80  #查看80端口 root下
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

##debian 安装软件
```c
dpkg -i <file.deb>#安装指定的deb包
dpkg -R <dir> #安装目录下的所有deb包
dpkg -r <file.deb>#删除指定的deb包
dpkg -L apache2 #查看指定软件的目录
```

##grep 搜索
```c
grep -c aaa file #显示 file中包含aaa内容的行数是几
grep -n aaa flie #列出所有的匹配行，并在最前面添加行的序列数
grep -v aaa file #显示文件中不包含所搜索内容的行数，这个和-c的参数正好相反
grep -i aaa file #列出所搜索内容的匹配行，搜索过程中不区分大小写
grep -l aaa * #列出所有包含aaa内容的文件的名
grep -r aaa #对当前目录和所有的子目录进行搜索
grep -w aaa file：#精确搜索，可以说准确性搜索，比如：grep -w b* a.txt：
						#此命令执行时，*不会默认为任何字符，只表示字面意思，就是一个*字符.
grep -x aaa file #完全匹配输出，比如：grep -x hello a.txt，只会输出某一行存在hello字符串，
#并且此行仅包含hello的内容。假设a.txt中有一行“hello all”，执行上述命令，此行不会被搜索到。
```

##自启动
**运行级别(Runlevel)**指的是Unix或者Linux等类Unix操作系统下不同的运行模式。运行级别通常分为7等，分别是从0到6.
```c
**0** 停机
**1** 单用户，Does not configure network interfaces, start daemons, or allow non-root logins
**2** 多用户，无网络连接 Does not configure network interfaces or start daemons
**3** 多用户，启动网络连接 Starts the system normally.
**4** 用户自定义
**5** 多用户带图形界面
**6** 重启

#在/etc下,根据不同的运行级别,通过脚本来启动服务
/etc/rc0.d Run level 0
/etc/rc1.d Run level 1
/etc/rc2.d Run level 2
/etc/rc3.d Run level 3
/etc/rc4.d Run level 4
/etc/rc5.d Run level 5
/etc/rc6.d Run level 6
#可能会有:
K01apache2与S91apache2

K:终止,S:启动

#修改常用的工具: sysv-rc-conf
sudo apt-get install sysv-rc-conf
```
##设置软链接
```bash
ls -n file1 file2 #创建file1的软链接file2,最好用绝对路径,否则可能会造成目录错误
```

##安全关机 
```bash
shutdown -r now #安全重启服务器
shutdown -h #关机
```

##历史命令
```bash
history 查看用户所有使用过的历史命令
history -w更新历史命令保存文件
history -c清空历史命令（错误信息及他人入侵的参考）

使用上、下箭头调用以前的历史命令
使用"!n"重复执行第n条历史命令
使用"!!"重复执行上一条命令
使用"!字串"重复执行最后一条以该字串开头的命令
```

##磁盘管理
```bash
分区类型：
	主分区最多只能分4个
扩展分区：
	最多只能有1个
	主分区加扩展分区最多有4个
	不能写入数据，只能包含逻辑分区
逻辑分区


df：查看磁盘分区使用状况
	-l：仅显示本地默认磁盘（默认）
	-a：显示所有文件系统的磁盘使用情况
	-h以1024进制计算最合适的单位显示磁盘容量
	-H：显示以1000进制计算最合适的单位显示磁盘容量
	-T显示磁盘分区类型
	-t显示指定类型文件系统的磁盘分区
	-x不显示指定类型文件系统的磁盘分区
du:统计磁盘上的文件大小
	-b 以byte为单位统计文件
	-k 以KB为单位统计文件
	-m 以MB为单位统计文件
	-h 按照1024进制以最适合的单位统计文件
	-H 按照1000进制以最适合的单位统计文件
	-s 指定统计目标
du -sh *.zip #以1024进制查看zip文件的大小
1.创建分区:
一:MBR分区模式:
 -主分区不超过4个
 -单个分区最大2TB
#磁盘分区工具fdisk
fdisk -l #查看分区设备
fdisk /dev/sdb #进入分区的模式,m查看help,n添加新的分区,w保存,q改变分区类型
二:GPT分区模式:(不适合安装32位的系统)
 -主分区最多有128个
 -单个分区几乎没有限制(18EB=18874368TB)
 -可以说没有逻辑,扩展等说法,只是为了兼容MBR
#磁盘分区工具parted
print #查看分区信息
malabel gpt #创建GPT分区(默认msdos为MBR分区模式)
rm 1 #删除1号分区
mkpart #创建分区
	-Partition name #名称(类似windows卷标)
	-File system type
	-start #从第几M开始    一般会让0-1M之间的一点点数据取消掉,使得数据对齐,从第1M开始 
	-end  #2000   2G
mkpart name start end #也可以一句话 
quit #退出 parted为立即生效
2.分区格式化:
#分区格式化工具 mkfs
mkfs -t ext4 /dev/sda1 #将第一块硬盘的1分区格式化为ext4文件系统
#MBR扩展分区不能格式化
#GPT分区 通过fdisk不能查看文件类型,只能通过parted
3.挂载分区
#挂载配置文件 /etc/fstab
mount /dev/sdb1 /mnt/zlx #临时挂载分区,重启失效
4.添加swap分区
通过fdisk工具,先通过t选择分区 ,然后L显示类型,选择82的swap id.
mkswap /dev/sdb8 #创建交换分区
swapon /dev/sdb8 #启用交换分区
free #查看交换分区
swapoff /devsdb8 #停用交换分区
```

##用户管理
```bash
/etc/group
组名:组密码占位符:组编号:组中用户名列表(相同则省略)
组编号0-499 为系统的组
/etc/gshadow #存储当前系统中用户组的密码信息
组名:组密码(*,!均为没有密码):组管理者:组中用户名列表
/etc/passwd #所有用户
用户名:密码占位符:用户编号:用户组编号:用户注释信息:用户主目录:shell类型
/etc/shadow #所有用户密码
```
