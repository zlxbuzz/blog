title: css权威指南笔记5
date: 2017-06-09 13:35:46
tags: css
---

## 字体


### 通用字体系列

```css
/* serif 字体:衬线字体，笔画开头和结尾有修饰，粗细不一。 */
/* sans-serif 字体：非衬线字体，没有上线短线 */
/* monospace 字符宽度完全相同。 */
/* cursive 可能有弯曲，或者由花体部分和小的弯曲部分组成。 */
/* fantasy 其他。 */

p {font-family:Times,TimesNR,'New York',serif;}
/*会按顺序查找，如果都不可用，则会简单的选择serif系列的可用字体*/
```

### 字体加粗

```css
font-weight:normal|bold|bolder|lighter|100|200|300|400|500|600|700|800|900|inherit

bolder|ligher 相对父元素字体加粗

```

### 字体大小

```css
font-size:xx-small|x-small|small|medium|large|x-large|xx-large|smaller|larger|<length>|<percentage>|inherit

smaller|larger 相对父元素字体变化

```


#### 字体大小和继承

```css
/* font-size 是可以继承的,只是继承计算值而不是百分比 ,代理浏览器会将小数取整，累积起来误差会大*/

```

#### 字体风格

```css
font-style:italic|oblique|normal|inherit

```

#### 字体变形

```css
font-variant:small-caps(小型大写字母文本)|normal|inherit
```

#### 字体的拉伸和调整

```css
font-stretch:nomal|wider|narrower|ultra-condensed|extra-condensed|condensed|semi-condensed|semi-expanded|expanded|extra-expanded|ultra-expanded|inherit
/* 让字体更胖或者更瘦,所有浏览器都不支持 ,包括font-size-adjust 也很少浏览器支持 */
```

#### font属性

```css
font: [[<font-style> || <font-variant> || <font-weight> ] ? <font-size> [/<line-height>] ? <font-family>]

caption:用操作系统的按钮字体
icon：用操作系统的图标
menu:采用操作系统菜单
message-box:采用操作系统对话框
small-caption:采用操作系统的小空间
status-bar :用于窗口状态条
```

#### font-face

```css
/* 下载远程字体 */
@font-face (font-family:"my";src:url(http://xxxxx.ttf));
```
