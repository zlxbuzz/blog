title: css权威指南笔记4
date: 2017-06-09 13:35:46
tags: css
---

## 长度单位

```css
/* 绝对长度单位 */
英寸(in)
厘米(cm):1英寸 = 2.54厘米
毫米(mm):1英寸 = 25.4毫米
点(pt) : 1英寸 = 72点
派卡(pc) : 12点 = 1派

ppi 每英寸实际像素


/* 相对长度单位 */
em: 1em (em 是相对于自身的font-size,如果没有设置，则为父级，依次向上级，最后为浏览器默认font-size)
ex: ex 代表所用字体中小写x的高度(大多数字体的小写字母都是相应大写字母高度的一般所以一般1ex = 0.5em)
px:像素
```

## url

```css
url(pathname)  /*会从文档开始的位置加上pathname  http://www.index.com/pathname*/
@import url(special/toppings.css) /*会基于当前css所在的目前后面去找对应的css http://www.index.com/style/special/toppings.css*/

```

## 关键字

```css
normal
inherit /*继承*/

```
