title: postgresql copy指令及相关函数
date: 2014-12-08 17:59:40
categories: postgresql
tags: [postgresql]
---
##关于postgresql的其他函数 
<!--more-->
#####查询获取在相关图形区间内的数据

```c
select * from shuibiaowgs where ST_Within(ST_GeomFromText(st_astext(geom)),ST_GeomFromText('MULTIPOLYGON(((116.46599813867363 39.80381050387473,116.49573847223077 39.80743703396794,116.50436445642275 39.792914248486795,116.47277876306339 39.78803384212833,116.46599813867363 39.80381050387473)))')) 
```

#####导出相关查询的结果(注意目录权限的问题,可以设定分隔符，默认为 \t)
```c
copy (select * from celiudianwgs where ST_Within(ST_GeomFromText(st_astext(geom)),ST_GeomFromText('MULTIPOLYGON(((116.46599813867363 39.80381050387473,116.49573847223077 39.80743703396794,116.47277876306339 39.78803384212833,116.50436445642275 39.792914248486795,116.46599813867363 39.80381050387473)))'))) to '/tmp/celiudianwgs.sql [DELIMTER '|']';         
```

#####导入之前导出的文件(注意表要优先建立，并且字段要匹配)
```c
copy table form 'filename'
```
