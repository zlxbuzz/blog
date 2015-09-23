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

rar:
        unrar x aaa.rar
```

##查看端口的占用情况
```c
lsof -i:80  #查看80端口 root下
lsof #查看本地网络服务活动状态
```
##修改主机名称
```c
vi /etc/hostname #主机名
vi /etc/hosts #域名解析
```

##apt操作
```c
apt-cache search package 搜索包    
apt-cache show package 获取包的相关信息，如说明、大小、版本等    
sudo apt-get install package 安装包    
sudo apt-get install package - - reinstall 重新安装包    
sudo apt-get -f install 修复安装"-f = ——fix-missing"    
sudo apt-get remove package 删除包    
sudo apt-get remove package - - purge 删除包，包括删除配置文件等    
sudo apt-get update 更新源    
sudo apt-get upgrade 更新已安装的包    
sudo apt-get dist-upgrade 升级系统    
sudo apt-get dselect-upgrade 使用 dselect 升级    
apt-cache depends package 了解使用依赖    
apt-cache rdepends package 是查看该包被哪些包依赖    
sudo apt-get build-dep package 安装相关的编译环境    
apt-get source package 下载该包的源代码    
sudo apt-get clean && sudo apt-get autoclean 清理无用的包    
sudo apt-get check 检查是否有损坏的依赖
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
#注销后保存在 ~/.bash_history中

使用上、下箭头调用以前的历史命令
使用"!n"重复执行第n条历史命令
使用"!!"重复执行上一条命令
使用"!字串"重复执行最后一条以该字串开头的命令
```


##重定向
```bash
标准输入输出 0 标准输入 1标准输出 2 标准错误输出
命令 > 文件（覆盖）,命令 >> 文件（追加） 都是正确语句的重定向,
命令 > 文件 2>&1 (覆盖)，命令 >> 文件 2>&1，正确错误信息输出都保存到同一个文件。
命令&>文件 （覆盖），命令&>>文件 (追加)，正确错误信息输出都保存到同一个文件。
命令 >> 文件1 2>>文件2 把正确的输出追加到文件1中，错误输出追加到文件2中。
/dev/null 是系统预留的用来接受垃圾的文件，即任何东西写到这个文件里面都会消失即不存在。

wc -c 统计字节数
wc -l 统计单词数
```

##变量操作
```bash
set 查看变量
set -u 调用未声明的变量时会报错
x=${x}111 变量叠加
unset x 删除变量x
env 查看环境变量
PS1变量：命令提示符设置
	\d #显示日期，格式为“星期 月 日”
	\H #显示完整的主机名，如默认的主机名“localhost.localdomain”
	\h #显示主机名，如localhost
	\t #显示24小时制时间，格式为“HH:MM:SS”
	\A #显示24小时制时间，格式为“HH:MM”
	\u #显示当前用户名
	\w #显示当前所在目录的最后一个目录
	\W #显示当前所在目录的最后一个目录
	\$ #提示符。如果是root用户会显示提示符为“#”，如果是普通用户会显示提示符为“$”

命令行位置变量:
	$n　 n为数字，$0代表命令本身，$1-$9代表第一到第九个参数，十以上的参数需要用大括号包含，如${10}
	$* 这个变量代表命令行中所有的参数，$*把所有的参数看成一个整体
	$@ 　这个变量也代表命令行中所有参数，不过$@把每个参数区分对待
	$# 　这个变量代表命令行所有参数的个数

预定义变量:
	$? ：最后一次执行命令的返回状态，如果正确执行，则返回0；
	$$：返回当前进程的PID号；
	
	$!：返回后台的进程PID号；
read -n
read -p "please input name " name #-p表示输出提示信息 read [选项] 变量名
read -t 30 #-t 表示等待时间单位为秒 -t 30 表示30秒，若30秒后没有输入数据终止执行脚本
read -s #隐藏信息

变量声明:
	declare声明变量类型
	declare [+/-] [选项] 变量名 -设定类型 +取消类型
	declare -p 变量名 显示变量类型
	declare -i 变量名 声明为整形
	declare -a 声明为数组
	declare -x 变量 相当于 export export其实是调用了declare -x
	declare -r 变量 将变量变为只读属性 改为只读属性后，无法进行操作了。
	
数值计算 dd=$(expr $aa + $bb)
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


##系统服务管理
```bash
#systemctl命令将service和chkconfig命令结合在了一起
systemctl enable nginx.service #使nginx自动启动
systemctl disable nginx.service #取消nginx自动启动
检查服务状态 systemctl status httpd.service （服务详细信息） systemctl is-active httpd.service （仅显示是否 Active)
显示所有已启动的服务	systemctl list-units --type=service
启动某服务	systemctl start nginx.service
停止某服务	systemctl stop nginx.service
重启某服务	systemctl restart nginx.service
```

##数据同步
```bash
rsync [option] 源路径 目标路径
	a, –archive 归档模式，表示以递归方式传输文件，并保持所有文件属性
	b, –backup 创建备份，也就是对于目的已经存在有同样的文件名时，将老的文件重新命名为~filename。可以使用–suffix选项来指定不同的备份文件前缀。
	–backup-dir 将备份文件(如~filename)存放在在目录下。
	-suffix=SUFFIX 定义备份文件前缀
	–delete 删除那些DST中SRC没有的文件
	–bwlimit=KBPS 限制I/O带宽
	
#将本机/tmp/a文件夹 同步至/tmp/b
rsync -avzP --delete /tmp/a /tmp/b
#将远程主机x中/tmp/a下的文件下载至本机 /tmp/b
rsync -avz -e ssh root@192.168.0.1:/tmp/a /tmp/b
```

##采集
```bash
wget [options] [URL]
	-o:记录log信息，用法-ofilename
	-a:追加log信息
	-O:将文件保存到文件 -Ofilename
	-c:断点续传
	–referer,referer值，采集必用
	–load-cookies=FILE 在开始会话前从文件 FILE中加载cookie
	–save-cookies=FILE 在会话结束后将 cookies保存到 FILE文件中
	-nc, –no-clobber 不要覆盖已经存在的文件
	-T,–timeout=SECONDS 设置超时时间
	-x,强制建立目录(保持目标网站的目录结构)
	-r,递归下载整个网站
curl [option] [url]
	-c:断点续传
	-o:文件名，要自己写
	-O:文件名，自动(和服务器上的名字一样)
	-D:保存cookie,curl -D cookie.txt URL
	-b:使用cookie,curl -b cookie.txt URL
	-A:发送浏览器信息，伪装成浏览器。curl -A “Mozilla/5.0 (Macintosh; Intel Mac OS X 10_8_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/31.0.1626.0″ URL,这样对方服务器会认为我们是一个在macos上跑的chrom浏览器。
	-e:填写referer值。
	-d:post模式，以application/x-www-url-encoded发送请求。d后面填写要提交的参数即可 curl -d”a=xx&b=xx&c=xx”。
	-F模拟 multipart/form-data 形式的 form 上传文件。curl -F “action=upload” -F”filename=@file.gz;type=application/octet-stream” URL

```


##ssh

```bash
 ssh user@host #远程登陆
 ssh -p port user@host #远程登陆某个端口
 ssh-keygen #在～/.ssh/下生成自己的公钥和私钥
 ssh-copy-id user@host #将自己的公钥copy到远程 免登陆，也可以直接$ ssh user@host 'mkdir -p .ssh && cat >> .ssh/authorized_keys' < ~/.ssh/id_rsa.pub
 如果不行，远传配置/etc/ssh/sshd_config 
 　RSAAuthentication yes
　　PubkeyAuthentication yes
　　AuthorizedKeysFile .ssh/authorized_keys
 
 　$ ssh -L 本地端口:目标主机:目标主机端口 #本地端口转发
 　$ ssh -R 远程主机端口:目标主机:目标主机端口 #远程端口转发
```
