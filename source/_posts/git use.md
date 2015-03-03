title: git  常用
date: 2014-12-08 18:23:40
categories: git
tags: git
---
经常遇到的git相关操作。
####返回某个文件的某个版本 

```c
git log 文件名 #查看某个文件的历史记录 可以加参数-p查看diff   获取commit id
git reset commitid 文件名 #返回该文件的当前的版本，会在缓存区
git checkout 文件名 #返回之前的版本

#可以用git reflog 查看所有的版本信息
```

####跳转到某个版本

```c
git reflog #查看所有版本信息
git reset --hard commitid #重置到某个特定的版本
```
