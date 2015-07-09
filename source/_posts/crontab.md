title: crontab记录
date: 2015-06-03 11:37:40
categories: linux
tags: linux
---
`crontab`是一个定时执行脚本的命令,类似于`windows`中的计划任务(最小执行单位为`分钟`).
####常见的指令
`crontab -e` – 编辑该用户的` crontab`。
`crontab -l `– 列出该用户的 `crontab`。
`crontab -r `– 删除该用户的 `crontab`。
`crontab -u <username>` – 指定要设定 `crontab `的用户名称。
`crontab <file>` – 表示将`file`做为`crontab`的任务列表文件并载入`crontab`。
####主要的参数
| 字段      |    描述 |  值  |
| :-------- | --------:| :--: |
| 分钟  | 一小时的第几分 |  0-59   |
| 小时  | 一天的第几小时 |  0-23   |
| 日期  | 一个月的的第几天 | 1-31   |
| 月份 | 一年的第几个月 |  1-12  |
| 周几  | 一周的第几天 | 0-6   |
| 命令  | 命令 |  可以被执行的任何命令   |

>关键词替换

| 字段      |    描述 | 
| :-------- | --------:| 
| @yearly  | 0 0 1 1 * | 
| @daily  |0 0 * * * |  
| @hourly  | 0 * * * * |
| @reboot | 重启时运行 |  

每天执行`test.php`
```bash
@daily php -f /home/zhonglingxiao/test/test.php>/dev/null 2>&1
```

`星号（*）`：代表所有可能的值，例如month字段如果是星号，则表示在满足其它字段的制约条件后每月都执行该命令操作。
`逗号（,）`：可以用逗号隔开的值指定一个列表范围，例如，“1,2,5,7,8,9”
`中杠（-）`：可以用整数之间的中杠表示一个整数范围，例如“2-6”表示“2,3,4,5,6”
`正斜线（/）`：可以用正斜线指定时间的间隔频率，例如“0-23/2”表示每两小时执行一次。同时正斜线可以和星号一起使用，例如*/10，如果用在minute字段，表示每十分钟执行一次。
####常见的例子
6月3日20点执行`test.php`
```bash
00 20 03 06 * php -f /home/zhonglingxiao/test/test.php>/dev/null 2>&1
```
6月3日20点,21点执行`test.php`
```bash
00 20,21 03 06 * php -f /home/zhonglingxiao/test/test.php>/dev/null 2>&1
```
每隔5分钟执行`test.php`
```bash
*/5 * * * * php -f /home/zhonglingxiao/test/test.php>/dev/null 2>&1
```
周1到周5 早上6点到12点 每隔一小时 执行`test.php`
```bash
00 06-12 * * 1-5 php -f /home/zhonglingxiao/test/test.php>/dev/null 2>&1
```

##常见问题
1.新创建的`cron job`想要立即生效,需要`/etc/init.d/crond restart`.
2.尽量不用`crontab -r`,它会删了该用户的所有crontab.
3.在`crontab`中`%`是有特殊含义的，表示换行的意思。如果要用的话必须进行转义`\%`，如经常用的`date ‘+%Y%m%d’`在`crontab`里是不会执行的，应该换成`date ‘+\%Y\%m\%d’`
4.周与日月不可同时并存,`30 12 11 9 5 root echo "just test"   <==这是错误的写法`
