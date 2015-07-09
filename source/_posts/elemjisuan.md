title: ele.me外卖平分算钱
date: 2015-06-11 14:54:18
categories: 其他
tags: 其他
---
最近一直在吃`ele.me`外卖，有很大的优惠，比如点50减20，点30减18等等，由于人多，最终每个人点了多少不好算出来，就用`bash`写了一个简单的算钱的公式,由于`bash`对于计算比较`low`,凑合着来用吧～
```bash
#!/bin/bash
price=0;
read -p "请输入总人数:" num
read -p "请输入实际付的总价钱:" all
for ((i=1;i<=$num;i++ ))
do
    declare -a array
    read -p "请输入第"$i"个人的原始价钱:" array[$i]
    price=$(($price+array[$i]))
done
arrnum=${#array[@]}
for ((count =1;count<=arrnum;count++)) 
do
        nowprice=`echo "scale=2;${array[$count]}/$price"|bc`
        nowprice=0$nowprice
        echo  $nowprice*$all|bc
done
```
直接在命令行执行该脚本就可以～
