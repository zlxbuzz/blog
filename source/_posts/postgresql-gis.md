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

##几何对象关系函数 ：
获取两个几何对象间的距离 ST_Distance(geometry, geometry)
如果两个几何对象间距离在给定值范围内，则返回TRUE ST_DWithin(geometry, geometry, float)
判断两个几何对象是否相等（比如LINESTRING(0 0, 2 2)和LINESTRING(0 0, 1 1, 2 2)是相同的几何对象） ST_Equals(geometry, geometry)
判断两个几何对象是否分离 ST_Disjoint(geometry, geometry)
判断两个几何对象是否相交 ST_Intersects(geometry, geometry)
判断两个几何对象的边缘是否接触 ST_Touches(geometry, geometry)
判断两个几何对象是否互相穿过 ST_Crosses(geometry, geometry)
判断A是否被B包含 ST_Within(geometry A, geometry B)
判断两个几何对象是否是重叠 ST_Overlaps(geometry, geometry)
判断A是否包含B ST_Contains(geometry A, geometry B)
判断A是否覆盖 B ST_Covers(geometry A, geometry B)
判断A是否被B所覆盖 ST_CoveredBy(geometry A, geometry B)
通过DE-9IM 矩阵判断两个几何对象的关系是否成立 ST_Relate(geometry, geometry, intersectionPatternMatrix)
获得两个几何对象的关系（DE-9IM矩阵） ST_Relate(geometry, geometry)

##几何对象处理函数：
获取几何对象的中心 ST_Centroid(geometry)
面积量测 ST_Area(geometry)
长度量测 ST_Length(geometry)
返回曲面上的一个点 ST_PointOnSurface(geometry)
获取边界 ST_Boundary(geometry)
获取缓冲后的几何对象 ST_Buffer(geometry, double, [integer])
获取多几何对象的外接对象 ST_ConvexHull(geometry)
获取两个几何对象相交的部分 ST_Intersection(geometry, geometry)
将经度小于0的值加360使所有经度值在0-360间 ST_Shift_Longitude(geometry)
获取两个几何对象不相交的部分（A、B可互换） ST_SymDifference(geometry A, geometry B)
从A去除和B相交的部分后返回 ST_Difference(geometry A, geometry B)
返回两个几何对象的合并结果 ST_Union(geometry, geometry)
返回一系列几何对象的合并结果 ST_Union(geometry set)
用较少的内存和较长的时间完成合并操作，结果和ST_Union相同 ST_MemUnion(geometry set)

##几何对象存取函数：
获取几何对象的WKT描述 ST_AsText(geometry)
获取几何对象的WKB描述 ST_AsBinary(geometry)
获取几何对象的空间参考ID ST_SRID(geometry)
获取几何对象的维数 ST_Dimension(geometry)
获取几何对象的边界范围 ST_Envelope(geometry)
判断几何对象是否为空 ST_IsEmpty(geometry)
判断几何对象是否不包含特殊点（比如自相交） ST_IsSimple(geometry)
判断几何对象是否闭合 ST_IsClosed(geometry)
判断曲线是否闭合并且不包含特殊点 ST_IsRing(geometry)
获取多几何对象中的对象个数 ST_NumGeometries(geometry)
获取多几何对象中第N个对象 ST_GeometryN(geometry,int)
获取几何对象中的点个数 ST_NumPoints(geometry)
获取几何对象的第N个点 ST_PointN(geometry,integer)
获取多边形的外边缘 ST_ExteriorRing(geometry)
获取多边形内边界个数 ST_NumInteriorRings(geometry)
同上 ST_NumInteriorRing(geometry)
获取多边形的第N个内边界 ST_InteriorRingN(geometry,integer)
获取线的终点 ST_EndPoint(geometry)
获取线的起始点 ST_StartPoint(geometry)
获取几何对象的类型 GeometryType(geometry)
类似上，但是不检查M值，即POINTM对象会被判断为point ST_GeometryType(geometry)
获取点的X坐标 ST_X(geometry)
获取点的Y坐标 ST_Y(geometry)
获取点的Z坐标 ST_Z(geometry)
获取点的M值 ST_M(geometry)



####在SQL语句中，用以下的方式可以使用WKT格式定义几何对象：
POINT(0 0) ——点
LINESTRING(0 0,1 1,1 2) ——线
POLYGON((0 0,4 0,4 4,0 4,0 0),(1 1, 2 1, 2 2, 1 2,1 1)) ——面
MULTIPOINT(0 0,1 2) ——多点
MULTILINESTRING((0 0,1 1,1 2),(2 3,3 2,5 4)) ——多线
MULTIPOLYGON(((0 0,4 0,4 4,0 4,0 0),(1 1,2 1,2 2,1 2,1 1)), ((-1 -1,-1 -2,-2 -2,-2 -1,-1 -1))) ——多面
GEOMETRYCOLLECTION(POINT(2 3),LINESTRING((2 3,3 4))) ——几何集合

####查询区域 面内的线
```c
select * from shuibiaowgs where ST_Within(ST_GeomFromText(st_astext(geom)),ST_GeomFromText('MULTIPOLYGON(((116.479776207058 39.7959679679374,116.481032007188 39.7963947089671,116.482239191711 39.7968431557598,116.483222850071 39.7951851880901,116.480750730424 39.7942829597482,116.479776207058 39.7959679679374)))')) 
```
