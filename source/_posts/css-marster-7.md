title: css权威指南笔记7
date: 2017-06-09 13:35:46
tags: css
---

## 基本框

```css

/* 每个元素都会生成一个或者多个矩形框,称为元素框 */
/* 内边距不能为负，外边距可以 */

```

## 包含块

包含块由最近的块级祖先框，表单元格，行内祖先框的内容边界构成
height百分比相当于包含块高度的百分比，其余大多数都是相当于包含块的宽度

## 水平格式化

```css
7大属性:margin-left,border-left,padding-left,width,padding-right,border-right,margin-right
7个水平属性的总和要等于父元素的width（包括外边距为负的情况）

/*
margin-left,width,margin-right 三个属性可以设置为auto
如果没有显示申明，外边距默认为0，width默认为auto
如果3个属性都设置为某个值，会导致过分受限，一般会强制把margin-right转为auto

水平外边距不会合并

如果是替换元素，width如果为auto，则默认为元素内容的固有宽度
*/
```

## 垂直格式化

```css
7个属性:margin-top,border-top,padding-top,height,padding-bottom,border-bottom,margin-bottom.
7大属性的值等于包含块的height


/*
margin-top,height,margin-bottom 三个属性可以设置为auto
在正常流中，如果设置margin-top或者margin-bottom 为auto，则会计算为0,从而不能垂直居中

如果没有直接指定包含块的height,百分比高度会重置为auto

auto高度：
  如果高度为auto（默认），只有块级子元素，其默认的高度是从最高块级子元素的外边框边界到最低子元素外边框边界之间的距离，
  相当于自元素的外边距会超出包含块。但是如果包含块有padding或者border，则高度是从最高子元素的上外边距到最低子元素的下外边距
  之间的距离.

合并垂直外边距：
  相邻外边距会沿竖轴合并，会被较大的外边距合并,
  如果父元素有border或者padding包裹了外边距，则不合并

负外边距：
  都设置负值，浏览器会取绝对值大的值
  一正一负，浏览器会取相减值
*/

```


## 行内元素

### 行布局

```css
匿名文本:未包含在行内元素中的字符串,空格也是
em框:字符框,就是font-size的值来决定
内容区:非替换元素中就是各自的em框串在一起构成的框。替换元素中就是元素中固有高度再加上可能存在的外边距，边框，内边距
行间距：line-height和font-size之间的差，分成两半，只应用于非替换元素.
行内框: 非替换元素行内框等于line-height。替换元素行内框的高度等于内容区的高度
行框：包含该行中出现的行内框的最高点和最低点的最小框

非替换元素的内边距，边距和外边距对行内元素或其生成的框没有垂直效果，不会影响元素行内框的高度（行框的高度也不会）
替换元素的外边距和边框会影响行内框的高度（行框）

得到行内各元素行内框的高度:
  1: 得到行内“非替换元素”及不属于后代行内元素的所有文本的font-size值和line-height值，再将line-height减去font-size，得到
框的行间距，将这个行间距除以2，将其一半分别应用到em框的顶部和底部。
  2: 得到行内“替换元素”的height，margin，padding，border的值，把他们加载一起。

```


### 行内格式化


#### 行内非替换元素

```css
建立框：
  首先行内非替换元素或者匿名文本，font-size决定了内容区的高度，比如font-size为15px，则em框高度即15px;
  再考虑line-height的值，如果line-height为21px，则相减，得到6 在除以2，将一半3px分别应用到内容区的顶部和底部，这就得到了行内框;
  如果是line－height小于font-size的情况，则行内框可能小于内容区。
```
