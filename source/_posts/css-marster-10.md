title: css权威指南笔记10
date: 2017-06-09 13:36:48
tags: css
---

## 浮动

```
float:
  值：left | right | none |inherit
  默认值：none
  应用：所有元素
  继承：无

浮动外边距不会合并。
浮动元素的包含块是其最近的块级祖先元素
两个浮动元素不会彼此覆盖
一个浮动元素的顶端不能比其父元素的内顶端或者之前出现的浮动元素的顶端高
```


```
定位：
position:
  值: static|relative|absolute|fixed|inherit
  应用于： 所有元素
  继承性：无

偏移属性: top,right,bottom,left
  值:<length> | <percenter> | auto | inherit
  初始值: auto
  应用于：定位元素(postion不是static的元素)
  百分数：top和bottom相对于包含块的高度，right和left相对于包含块的宽度

内容溢出
  overflow：visible | hidden | scroll | auto | inherit
  初始值：visible
  应用于：块级元素和替换元素
  继承性：无
剪裁
  clip: rect(top,right,bottom,left) (代表距离左上角的距离)| auto | inherit
  应用于：绝对定位元素

z-index: <integer>(整数包括负数) | auto| inherit
    初始值：auto
    应用于: 定位元素
    继承性: 无
    如果一个元素指定了z-index的值（非auto），该元素就会建立自己的局部叠放上下文，所有该元素的后代相对于该祖先元素都有其自己的叠放顺序

```
