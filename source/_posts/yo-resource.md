title: yeoman使用心得
date: 2015-05-01 15:27:59
categories: js
tags: Yoeman
---
最近在用前端的项目构建工具`yeoman`，在此记录下心得。
##`Yeoman`介绍
通常在开发新项目时我们都需要配置工程环境，开发目录，需要下载一些库、框架文件（如 `jQuery`、`Backbone` 等），配置编译环境（`Less`、`Sass`、`Coffeescript`等），甚至还要配置单元测试框架，过程非常繁琐，还没开始编码时间就耗了大半天。为了解决这个问题 Paul Irish、Addy Osmani、Sindre Sorhus、Mickael Daniel、Eric Bidelman 和 Yeoman 社区共同开发的一个项目——`Yeoman`。

`YO`：`Yeoman`核心工具，项目工程依赖目录和文件生成工具，项目生产环境和编译环境生成工具。
`GRUNT`：前端构建工具。
`BOWER`：`Web` 开发的包管理器，概念上类似 `npm`，`npm` 专注于`NodeJs` 模块，而 `bower` 专注于 `CSS`、`JavaScrip`t、图像等前端相关内容的管理。
##`yo`的安装
```bash
npm install -g yo #yo作为全局的安装
```
由于`yo`需要各种不一样的模具`generator`，以`angular`为例子
```bash
npm install -g generator-angular #以-隔开
```
在项目目录下创建目录

```bash
zhonglingxiao@anheng:~/angular$  yo angular learnyo #第二个为模具名 第三个为项目名称
#之后会有选项，确认即可。如果报错 则需要 npm install && bower install

```
##`bower`的安装
全局安装
```bash
npm install -g bower
```
bower的安装web包一共有4中方式
```bash
#对于常见的组件
bower install bootstrap #可以加 `#` 后面跟版本
#通过github的短语
bower install jquery/jquery 
#通过github完整的连接
#支持直接的url连接
```
bower 有2个配置文件，可以通过`bower init` 或者直接手动创建
```bash
bower.json － bower install读取json文件，下载公共库和组件
.bowerrc 如何生成：bower init －> 配置bower.json的items
.bowerrc
{
	“directory” : "bower_components", #是bower安装依赖文件的目录路径
	"proxy" : "http://proxy.tencent.com:8080", #使用代理 
	"https-proxy":"https://proxy.tencent.com:8080", #使用https代理
	"timeout" : 60000 #失效时间 ms

}
```

##常见经验
####package.json
```bash
package.json //nodejs的 配置文件
#name 项目名
#version 版本

#dependencies 生产中的依赖包 --就是发布后 别人运行的npm install的依赖包
#devDependencies 开发过程中的依赖包
#在使用install命令时  如果加上--save 或者 --save-dev 则会分别存入json文件 对于bower.json也一样


npm update或npm install 会自动更新一下：
^主版本号锁定
~次版本号锁定
啥都不加，末版本号锁定
```

