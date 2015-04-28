title: linux常用笔记
date: 2014-12-10 15:07:16
categories: linux
tags: linux
---
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
```bash
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
