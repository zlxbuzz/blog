title: npm常用包
date: 2016-01-27 14:22:12
tags: js
---
## 使用scp2进行ssh传输
```bash
#下载nodejs
#通过npm 下载全局命令scp2
npm i -g scp2
#直接使用
scp2 img/ zhonglingxiao:123456@10.172.225.119:/home/zhonglingxiao/img/ #复制目录的内容到某个目录
scp2 a.jpg zhonglingxiao:123456@10.172.225.119:/home/zhonglingxiao/img/

```
