title: phalcon框架的nginx配置
date: 2015-06-10 13:04:01
categories: php
tags: php
---
`phalcon`是由`C`编写的php框架，通过扩展的形式加载，所以速度非常快。这里我记录下遇到的一些问题，以便大家学习和自己的提高。
##安装phalcon
由于我是`debian`系统，所以首先`https://phalconphp.com/en/download`下载,通过编译成`so`扩展：
```bash
git clone --depth=1 git://github.com/phalcon/cphalcon.git
cd cphalcon/build
sudo ./install
```
之后会生成在php的扩展目录`extension-dir`（可以通过命令 `php-config` 查看具体的路径），之后将`phalcon.so`引入到`php.ini`中。
引入的方法有很多，这里由于`debian`按照不同的运行模式配置`php`，我就写一下到`nginx`的配置:
```bash
sudo touch /etc/php5/mod-available/phalcon.ini
```

之后写上`extension=phalcon.so`,然后
```bash
cd /etc/php5/fpm/conf.d/ #nginx 的php配置环境fpm
sudo ln -s /etc/php5/mod-available/phalcon.ini phalcon.ini #设置软连接
sudo systemctl restart php5-fpm.service #重启php-fpm
```
最后可以在`phpinfo()`中看到`phalcon`信息，则说明加载成功

##安装Phalcon Developer Tools工具
`Phalcon Developer Tools`是phalcon的一款自动生成目录结构的工具，理论上`phalcon`没有固定的目录结构，可以随时使用。
安装`Phalcon Developer Tools`的方法有很多`http://phalcon.5iunix.net/reference/tools.html`，我介绍下最方便的。
通过`Composer`或者`PEAR`的方式由于国内的原因，不一定能成功。所以我这边通过`git`直接下载：
```bash
git clone https://github.com/phalcon/phalcon-devtools.git #git上下载
cd phalcon-devtools 
ln -s ~/phalcon-devtools/phalcon.php /usr/bin/phalcon #设置全局的环境变量
chmod ugo+x /usr/bin/phalcon #给所有`u：自己 g：同组 o：其他`人都有有执行的权限
```
如果没问题，之后就可以用了
```bash
zhonglingxiao@aa:/etc/php5/apache2$ phalcon

Phalcon DevTools (2.0.3)

Available commands:
  commands (alias of: list, enumerate)
  controller (alias of: create-controller)
  model (alias of: create-model)
  all-models (alias of: create-all-models)
  project (alias of: create-project)
  scaffold (alias of: create-scaffold)
  migration (alias of: create-migration)
  webtools (alias of: create-webtools)

```


##生成结构并且配置 
```bash
phalcon create-project store #生成目录
```
在`nginx`中进行配置
```
cd /etc/nginx/site-available/ #进入配置目录
sudo vi phalcon-hosts.conf #创建配置文件
```
在`phalcon-hosts.conf`添加
```bash
server {
       listen 80;#80端口
       listen [::]:80;
       server_name phalcon.com;
       root /home/zhonglingxiao/learnphp/phalcon/store;
       index index.php index.html;
       location ~ \.php$ {
               
               include snippets/fastcgi-php.conf;
              fastcgi_pass unix:/var/run/php5-fpm.sock;
              fastcgi_param SCRIPT_FILENAME /home/zhonglingxiao/learnphp/phalcon/store$fastcgi_script_name;
              include fastcgi_params;
        }
         location /{
                  rewrite ^$ public/ last;
                  rewrite ^(.*)$  /public/index.php?_url=$1 last;#重写的规则

        }
}

```
之后：
```
cd /etc/nginx/site-enable/ 
sudo ln -s /etc/nginx/site-available/phalcon-hosts.conf phalcon-hosts.conf
```

然后修改host，`127.0.0.1 phalcon.com`；
之后重启`nginx`就好了 `sudo systemctl restart nginx.service`;
如果没问题的话，输入`phalcon.com`，就ok了～
![描述](/选区_057.png)
