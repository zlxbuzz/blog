title: css权威指南笔记2
date: 2017-06-09 13:35:46
tags: css
---

## 元素选择器

html {color:black;}
p {color:gray;}
h2 {color:red}

## 分组

### 选择器分组

h2,p {color:gray;}

### 声明分组

//推荐分号隔开每个声明
h1 {font: 18px;color: purple;}

### 选择器和声明综合分组

h1,h2,h3 {color:gray;background:white;}


## 类选择器和ID选择器

### 多类选择器

```css
.warning.urgent {background:red;}//class="urgent warning"

```
注意：浏览器通常不检查id的唯一性，但是还是不要多个元素设置一个id,现代浏览器选择器区分大小写（很老的浏览器不区分）.

## 属性选择器

```css
h1[class] {color:red}
a[href][title] {font-weight: bold;}

a[href="http://baidu.com"] {font-weight:bold}
a[href="http://baidu.com"][title="aaa"] {font-weight:bold}

/* 需要全局匹配 */
planet[type="barren rocky"] {font-weigth:bold}
```

### 部分属性选择器

```css
p[class~="warning"] {font-weight:bold;}/*属性值中的一个用空格来分隔的词 等价于 p.warning*/

p[class^="bar"]  /*全部属性值以bar开头*/
p[class$="bar"]  /*全部属性值以bar结尾*/
p[class*="bar"]  /*全部属性值包含bar字符串*/
```

### 特定属性选择器


```css
*[lang|="en"] {color:red}/*lang属性值等于en或en-开头的所有元素*/
```


### 后代选择器

```css
ul ol ul em {color:gray};/*后代所有元素，不管嵌套多深*/

h1 > strong {color:red};/*仅仅是子元素,可以理解为选择作为h1子元素的所有strong元素*/

h1 + p {maring-top:0};/*选择紧接在一个h1元素后出现的所有段落*/
```

## 伪类和伪元素

### 伪类

```css
/*链接伪类*/

:link /*超链接，带有href属性*/
:visited /*已访问的超链接*/

/*动态伪类*/
:focus /*获取焦点*/
:hover /*鼠标停留*/
:active /*用户输入激活，比如鼠标点击*/

/*静态伪类*/
:first-child /*第一个子元素*/
:lang(fr) /*语言选择*/

```

### 伪元素选择器

```css
:first-letter {color:red}/*一个块级元素的首字母*/
:first-line {color:purple} /*块级元素每一段的第一行文本*/

:befor{content:"]]";color:silver;} /*在元素前面插入*/
:after{content:"]]";color:silver;} /*在元素后面插入*/

```


