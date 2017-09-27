title: css权威指南笔记8
date: 2017-06-09 13:35:46
tags: css
---

## 基本元素框（element box）


```
width

值: <length>|<percentage>|auto|inherit
初始值: auto
应用: 块级元素和替换元素（行内非替换元素不生效）
百分比: 对于包含块的宽度

height

值: <length>|<percentage>|auto|inherit
初始值: auto
应用: 块级元素和替换元素（行内非替换元素不生效）
百分比: 对于包含块的高度

margin

值: <length>|<percentage>|auto|inherit
初始值: 无
应用:所有
百分比: 对于包含块的width

```

## 外边距和行内元素

```
行内非替换元素 上下外边距不影响行高,左右外边距可以。
```

## 内边距和行内元素

```
行内非替换元素 左右内边距可以扩展，上下内边距也可以，但是不影响行高。
```

```
全局边框

border:[<border-width> || <border-style> || border-color] | inherit

内边距padding

值: [<length> | <percentage>] | inherit
初始值: 未定义
应用于：所有元素
百分比： 相对于包含块的width
说明： 内边距绝对不能为负
```
