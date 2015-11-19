title: git  常用
date: 2014-12-08 18:23:40
categories: git
tags: git
---
经常遇到的git相关操作。

## git rebase
```c
git checkout bat
git rebase origin #把"bat"分支里的每个提交(commit)取消掉，并且把它们临时 #保存为补丁(patch)(这些补丁放到".git/rebase"目录中),然后把"bat"分支更新 
#为最新的"origin"分支，最后把保存的这些补丁应用到"mywork"分支上

git rebase和git merge的区别
merge相当于将双方的修改综合
rebase相当于将对方修改之后,在提交自己的修改,结果一样
```

## git clone 取回远程的所有分支

```c
git clone git@github.com:dolymood/angular-example.git #获取某个远程库
git fetch <远程主机名>  <分支名> #获取全部的分支 如果需要特定分支 可指定分支名
git branch -a #查看所有分支 git branch -a 查看所有分支
git checkout -b newBrach <远程分支> #创建并且切换到新的分支
```

## 返回某个文件的某个版本 

```c
git log 文件名 #查看某个文件的历史记录 可以加参数-p查看diff   获取commit id
git reset commitid 文件名 #返回该文件的当前的版本，会在缓存区
git checkout 文件名 #返回之前的版本

#可以用git reflog 查看所有的版本信息
#git log --pretty=oneline filename 通过一行查看单个文件的提交情况
#git show commitid 查看该提交id的修改情况
```

## 跳转到某个版本

```c
git reflog #查看所有版本信息
git reset --hard commitid #重置到某个特定的版本
```

## 删除文件

```c
git rm filename   直接删除文件
git rm --cached filename   删除文件暂存状态
```
 
## 创建分支

```c
git branch develop // 只创建分支
git checkout -b master develop // 创建并切换到 develop 分支
```

## 设置 commit 的用户和邮箱

```c
git config user.name "xx"
git config user.email "xx@xx.com"
```

## Git设置
```c
Git的全局设置在~/.gitconfig中，单独设置在project/.git/config下。

忽略设置全局在~/.gitignore_global中，单独设置在project/.gitignore下。
```
## git clean 指令
```c
git clean -f #删除未跟踪的文件
  参数n:查看删除哪些文件
  参数x:将gitignore的文件删除,一般不用
  参数d:删除未跟踪的目录

```


## gitignore生效
```c
#中途加进.gitignore的文件或文件夹不会生效
git rm -r --cached .#之前已经在版本管理中了，需要删除本地缓存，在提交
git add .
git commit -m"add"

``` 
