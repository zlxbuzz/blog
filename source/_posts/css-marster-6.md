title: css权威指南笔记6
date: 2017-06-09 13:35:46
tags: css
---

## 文本属性

```css

/* 缩进 */
text-indent: 3em;/*应用于块级元素,不应用于行内元素或者替换元素*/
/* 百分比相当于父元素的宽度 ,可以继承,2.1之前继承计算值，之后继承申明值*/

/* 水平对齐 */
/* 应用于块级元素 */
text-align:center|left|right|justify|inherit


/* 垂直对齐 */
line-height:<length>|<percentage>|<number>|normal|inherit /*代表文本行基线之间的最小距离*/
/* 百分比相当于元素的字体大小 */


/* 定义: */
/* 文本行中每个元素都会生成一个内容区，内容区会生成一个行内框(inline box),由line-height产生的行间距 */
/* 就是增加或者减少各个行内框高度的原因之一。将line－height的计算值减去font－size的计算值就是总的行 */
/* 间距，然后除以2 将一半分别应用到内容区的顶部和底部，结果就是行内框。 */

/* 继承： */
/*   1.如果为一个数字1（缩放因子），则继承申明值。 */
/*   2.如果为其他，则继承计算值。 */


/* 垂直对齐文本 */
/* 只能应用到行内元素和替换元素,并且不能继承 */
/* 百分比相对于元素的line-height值 */
/*inline-block依赖型元素(只有inline或者inline-block才起作用)*/
vertical-align:baseline|sub|super|top|text-top|middle|bottom|text-bottom|<percentage>|<length>|inherit

vertical-align:baseline;/*默认值，一个元素的基线和其父元素的基线对齐,如果该元素没有基线，比如为图像或者表单数据元素，则底端(实际上是下外边距)与父元素的基线对齐*/

vertical-align:5px;/*元素相当于基线向上偏移5像素,同时提升其内容区和行内框*/
vertical-align:-5px;/*元素相当于基线向下偏移5像素*/

vertical-align:text-bottom;/*基线与父元素的行内文本底端对齐(将元素行内框的底端与父元素的内容区的底端对齐)*/
vertical-align:bottom;/*基线与父元素的下行框底端对齐(将元素行内框的底端与包含该元素的行框的底端对齐)*/

vertical-align:text-top;/*基线与父元素的行内文本顶端对齐(将元素行内框的底端与父元素的内容区的顶端对齐)*/
vertical-align:top;/*基线与父元素的行框顶端对齐(将元素行内框的顶端与包含该元素的行框的顶端对齐)*/

vertical-align:middle;/*一般用于图片,将元素行内框的的垂直中点和父元素基线上方0.5ex（一般为0.25em）出的点对齐*/

```

## 字间隔和字母间隔

```css
/*单词间隔*/
word-spacing:<length>|normal|inherit
/*字母 隔*/
letter-spacing:<length>|normal|inherit
```

## 文本

```css
/* 文本转换 */
text-transform:uppercase|lowercase|capitalize|none|inherit;
/* 分别为大写，小写，首字母大写 */

/* 文本装饰*/
/* 无继承 */
text-decoration:underline|overline|line-through|blink|none|inherit;
/*下划线，上划线，贯穿线，闪烁*/

/* 文本阴影 */
text-shadow:green 5px 0.5em 1px;
/*颜色 向右偏移5px 向下偏移0.5em 模糊半径1px*/

/* 处理空白符 */
white-space:normal|nowrap|pre|pre-wrap|pre-line|inherit
/* normal:一行中多个空格的序列会转换为一个空格 */
/* pre:空白符不会忽略 */
/* nowrap:防止文本换行 */

/* 文本方向 */
direction:ltr|rtl|inherit

```



