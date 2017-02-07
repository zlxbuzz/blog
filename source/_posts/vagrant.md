title: vagrant初探
date: 2015-11-23 14:30:35
tags: vagrant
---
  对于新的系统`Mac/Linux/Windows`来说,装开发环境是一件很痛苦的事,要根据不同的系统装不同的环境,非常凌乱。偶然听说有`Vagrant`,它可以通过`VirtualBox`来封装一个linux环境, 我们只需要在本地进行开发，代码就可以同步到环境中，非常方便。

##安装##
  只需要装两个：
  `VirtualBox` : https://www.virtualbox.org/wiki/Downloads
  `Vagrant`    : http://downloads.vagrantup.com/
 完成之后，可以通过`vagrant box add [box_name]`自动下载相关的`box`镜像，添加到`vagrant`中去。如果网速比较慢的话,可以通过url去下载相应的`box`文件,然后通过`vagrant box add [box_name]  [file]`,`box_name`可以自定义。
[相关的box列表](https://atlas.hashicorp.com/boxes/search)
## 初始化环境
   安装完之后可以通过 `vagrant box list`  查看所有的`box`。
```bash
~ >vagrant box list
laravel (virtualbox, 0) #有个name为laravel的环境
```
  现在可以创建开发目录
```bash
mkdir ~/code #新建开发目录
vagrant init laravel #相关环境的初始化，会生成`Vagrantfile`的配置文件
vagrant up #开启环境,如果每次修改配置文件后，可以通过vagrant reload 重置环境
```
 完成之后，如果不做配置修改，默认的开发目录就对应linux的`/vargrant`目录,linux环境就已经搭建好了，可以通过 `vagrant ssh` 直接连接到环境

## Vagrantfile文件配置
```
Vagrant.configure("2") do |config|
  #目前大多数都是版本2的配置
end
```

所对应的box名称，如果没有，则默认为`base`
```
config.vm.box = "laravel"
config.vm.host_name = "lln" ##主机名
```
网络的配置,本地的8080端口对应虚拟机的80端口，可以通过`localhost:8080`访问
```
config.vm.network :forwarded_port, guest: 80, host: 8080
config.vm.network :private_network, ip: "192.168.50.4" #通过固定的ip去访问，也可以通过本地域名绑定到这个ip
```
文件的同步，默认为本地的开发目录到 `/vagrant`
```
config.vm.synced_folder "code/", "/home/lln/code" #第一个为本地目录，第二个为虚拟机的挂载目录，会同步
```

修改完成之后可以随时`vagrant reload`重载配置

ps:有些环境可能`nginx`需要自己配置一下.
