title: postgresql-gis
date: 2014-12-08 18:23:40
categories: postgresql
tags: gis
---
//ST_AsText 获取区域中心坐标。
```c
select *,ST_AsText(ST_Centroid("geom")) from "dmaguihua"
```
##ST_Geometry 类型

ST_Geometry 类型是几何类型层次中的最大超类型。
主要用到两个函数
ST_GeomFromText
ST_AsText
http://dcx.sap.com/1201/zh/dbspatial/pg-api-spatial-st-geometry-type.html
