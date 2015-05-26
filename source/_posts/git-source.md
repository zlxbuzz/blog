title: git  常用
date: 2014-12-08 18:23:40
categories: git
tags: git
---
经常遇到的git相关操作。

##git clone 取回远程的所有分支

```c
git clone git@github.com:dolymood/angular-example.git #获取某个远程库
git fetch <远程主机名>  <分支名> #获取全部的分支 如果需要特定分支 可指定分支名
git branch -a #查看所有分支 git branch -a 查看所有分支
git checkout -b newBrach <远程分支> #创建并且切换到新的分支
```

##返回某个文件的某个版本 

```c
git log 文件名 #查看某个文件的历史记录 可以加参数-p查看diff   获取commit id
git reset commitid 文件名 #返回该文件的当前的版本，会在缓存区
git checkout 文件名 #返回之前的版本

#可以用git reflog 查看所有的版本信息
#git log --pretty=oneline filename 通过一行查看单个文件的提交情况
#git show commitid 查看该提交id的修改情况
```

##跳转到某个版本

```c
git reflog #查看所有版本信息
git reset --hard commitid #重置到某个特定的版本
```

##删除文件

```c
git rm filename   直接删除文件
git rm --cached filename   删除文件暂存状态
```
 
##创建分支

```c
git branch develop // 只创建分支
git checkout -b master develop // 创建并切换到 develop 分支
```

##设置 commit 的用户和邮箱

```c
git config user.name "xx"
git config user.email "xx@xx.com"
```

##Git设置

Git的全局设置在~/.gitconfig中，单独设置在project/.git/config下。

忽略设置全局在~/.gitignore_global中，单独设置在project/.gitignore下。

