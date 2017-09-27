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
#git log --stat 很好用，只看每次提交的增减
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
git config --global color.ui true #git 显示颜色
```

## Git设置
```c
Git的全局设置在~/.gitconfig中，单独设置在project/.git/config下。

忽略设置全局在~/.gitignore_global中，单独设置在project/.gitignore下。

//设置提交的时候是否转换换行符号
git config [--global] core.autocrlf = [true|false|input]
true  : 将crlf转换为lf，而在检出时将crlf转换为lf.
false : 不转换.
input : 提交时将crlf转换成lf，检出时不转换.

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


##  git add submodule
```c
git submodule add git@github.com:zlxbuzz/gulp.git ./gulp

##删除模块
1 .gitmodules的模块信息
2 git rm –cached gulp

```

## git 更新submodule
```c
#可以写一个submoduleupdate.sh 的脚本
git submodule init
git submodule update
git submodule foreach --recursive 'branch="$(git config -f $toplevel/.gitmodules submodule.$name.branch)"; git checkout $branch'
git submodule foreach --recursive "git submodule update"

echo "Pulling all git submodules..."
git submodule foreach --recursive 'branch="$(git config -f $toplevel/.gitmodules submodule.$name.branch)"; git pull origin $branch'
```
## git blame 查看每行提交
```c
git blame [选项] [版本选项] [版本] [--] 文件
    --incremental         增量式地显示发现的 blame 条目
    -b                    边界提交显示空的 SHA-1（默认：关闭）
    --root                不把根提交作为边界（默认：关闭）
    --show-stats          显示命令消耗统计
    --score-debug         显示判断 blame 条目位移的得分诊断信息
    -f, --show-name       显示原始文件名（默认：自动）
    -n, --show-number     显示原始的行号（默认：关闭）
    -p, --porcelain       显示为一个适合机器读取的格式
    --line-porcelain      为每一行显示机器适用的提交信息
    -c                    使用和 git-annotate 相同的输出模式（默认：关闭）
    -t                    显示原始时间戳（默认：关闭）
    -l                    显示长的SHA1提交号（默认：关闭）
    -s                    隐藏作者名字和时间戳（默认：关闭）
    -e, --show-email      显示作者的邮箱而不是名字（默认：关闭）
    -w                    忽略空白差异
    --minimal             花费额外的循环来找到更好的匹配
    -S <文件>             使用来自 <file> 的修订集而不是调用 git-rev-list
    --contents <文件>     使用 <file> 的内容作为最终的图片
    -C[<得分>]            找到文件内及跨文件的行拷贝
    -M[<得分>]            找到文件内及跨文件的行移动
    -L <n,m>              只处理行范围在 n 和 m 之间的，从 1 开始
    --abbrev[=<n>]        用 <n> 位数字显示 SHA-1 哈希值
```

## git add
```c
用法：git add [选项] [--] <路径规则>...

    -n, --dry-run         演习
    -v, --verbose         冗长输出

    -i, --interactive     交互式拣选
    -p, --patch           交互式挑选数据块
    -e, --edit            编辑当前差异并应用
    -f, --force           允许添加忽略的文件
    -u, --update          更新已跟踪的文件
    -N, --intent-to-add   只记录，该路径稍后再添加
    -A, --all             添加所有改变的已跟踪文件和未跟踪文件
    --ignore-removal      忽略工作区中移除的路径（和 --no-all 相同）
    --refresh             不添加，只刷新索引
    --ignore-errors       跳过因出错不能添加的文件
    --ignore-missing      检查在演习模式下文件（即使不存在）是否被忽略

    git  add .  #新文件＋修改的文件
    git  add -u #修改的文件或删除的文件
    git  add -A # 所有新文件和修改的文件，删除的文件
```


## git push
```c
git push origin --delete dev #删除远程分支
```



## git flow

```c
分支使用
master
与线上版本保持同步，代码和功能质量满足实际发布环境需要
不直接接收任何代码commit。
接收来自release、hotfix分支的merge。
版本的tag也在此分支进行定义
develop
接收来自其他功能、特性开发分支（feature）的merge。
feature
具体功能、特性的工作分支族，大部分的commit在此类分支上完成。
完成开发后，分支merge到develop分支，具体feature分支删除。
release
用于版本发布的分支，在确定版本计划后从develop分支建立。
用于版本的测试、问题修复工作，接收bug修复的commit。
完成测试和开发后，分支merge到develop和master分支。
hotfix
用于在master分支发现实际环境中问题进行修复，接收修复commit。
完成后merge回master分支并且merge到develop分支。
master分支需要进行修复版本tag的定义。
```

## git 对比两个tag，并且排除某些目录

```c
 git diff 1.1.1.179...1.1.1.182 -- . ':!dist' ':!lib'
```


## git diff 三个点

```c
//两个点 直接就是2个分支(tag)的差别
//三个点相当于A和B的公共祖先与B的差异
git diff $(git-merge-base A B) B

```
