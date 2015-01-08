title: npm package.json dependecies 和 devDependecies区别
date: 2014-12-02 10:43:01
categories: node
tags: nodejs
---
####dependencies
        有package.json的目录下 npm install安装
        任意目录下 npm install $package 安装到当前目录

####devDependencies
        有package.json的目录下 npm install安装
        任意目录下 npm install $package --dev 才能进行安装
