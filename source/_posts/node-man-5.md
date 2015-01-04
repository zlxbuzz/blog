title: Node.js Ejs 方法 
date: 2014-12-15 11:52:34
categories: node
tags: [node,ejs]
---
##express 中使用
```js
//设置模板目录
app.set('views', path.join(__dirname, 'views'));    

//设置模板引擎
app.set('view engine', 'html');

//设置引擎后缀.  index.html 中的内容可以是 ejs 代码
app.engine('.html', require('ejs').__express);
```
```js
	ejs的特性： 
	1、缓存功能，能够缓存已经解析好的html模版；
	2、<% code %>用于执行其中javascript代码；
	3、<%= code %>会对code进行html转义； 
	4、<%- code %>将不会进行转义； 
	5、支持自定义标签，比如’<%’可以使用’左括号 左括号’，’%>’用’右括号 右括号’代替； 
	6、提供一些辅助函数，用于模版中使用 
	7、利用<%- include filename %>加载其他页面模版；
```
##ejs 函数/运算符
####1.引入模板 不指定后缀就寻找 layout.ejs. (注意:如果没有定义模板目录,则 include无效)
```js
<% include layout.html%>
<%- include layout.html%>
```
####2.静态编译模板,没有 IO 操作，会非常快，而且可以公用本地变量.
```js
<ul>
    <% users.forEach(function(user){ %>
    <% include user/show %>
    <% }) %>
</ul>
```
意思就是模板名是动态的
####3.自定义 闭合标签. 
厌倦了` <% %> ?`
```js
//设置闭合标签
var ejs = require('ejs');  
ejs.open = '左括号 左括号';  
ejs.close = '右括号 右括号';  
```
express中全局设定
```js
app.set("view options",{                                                                                  
   "open":"左括号 左括号",                                                                                  
   "close":"右括号 右括号"
});
```
####4.变量
```js
//传递 index 模板引擎参数
res.render('index',{'title':'haha');

//使用参数
<title><%= title %></title>
```
####5.运行js代码

```js
<%for(var i=p.length-1; i>=0; i--){%>
<input type="button" value=<%=p[i]%>>
<%右括号%>
```
####6.选项 express中 通过 res.redirect('login’, [options]); 来对模板进行访问,options就可以设置模板引擎的一些选项 其中options的一些参数为：
```js
1、cache：是否缓存解析后的模版，需要filename作为key； 
2、filename：模版文件名； 
3、scope：complile后的Function执行所在的上下文环境； 
4、debug：标识是否是debeg状态，debug为true则会输出生成的Function内容；
5、compileDebug：标识是否是编译debug，为true则会生成解析过程中的跟踪信息，用于调试； 
6、client，标识是否用于浏览器客户端运行，为true则返回解析后的可以单独运行的Function函数； 
7、open，代码开头标记，默认为’<%’； 
8、close，代码结束标记，默认为’%>’； 
9、其他的一些用于解析模版时提供的变量。 在express中使用时，options参数将由response.render进行传入，其中包含了一些express中的设置，以及用户提供的变量值。
```
####7.f辅助函数 此外ejs还提供了一些辅助函数，用于代替使用javascript代码，使得更加方便的操纵数据。
```js
1、first，返回数组的第一个元素； 
2、last，返回数组的最后一个元素； 
3、capitalize，返回首字母大写的字符串； 
4、downcase，返回字符串的小写； 
5、upcase，返回字符串的大写； 
6、sort，排序（Object.create(obj).sort()？）；
7、sort_by:’prop’，按照指定的prop属性进行升序排序； 
8、size，返回长度，即length属性，不一定非是数组才行； 
9、plus:n，加上n，将转化为Number进行运算； 
10、minus:n，减去n，将转化为Number进行运算； 
11、times:n，乘以n，将转化为Number进行运算；
12、divided_by:n，除以n，将转化为Number进行运算； 
13、join:’val’，将数组用’val’最为分隔符，进行合并成一个字符串； 
14、truncate:n，截取前n个字符，超过长度时，将返回一个副本 
15、truncate_words:n，取得字符串中的前n个word，word以空格进行分割； 
16、replace:pattern,substitution，字符串替换，substitution不提供将删除匹配的子串；17、prepend:val，如果操作数为数组，则进行合并；为字符串则添加val在前面； 
18、append:val，如果操作数为数组，则进行合并；为字符串则添加val在后面； 
19、map:’prop’，返回对象数组中属性为prop的值组成的数组； 
20、reverse，翻转数组或字符串；
21、get:’prop’，取得属性为’prop’的值； 
22、json，转化为json格式字符串
```
辅助函数使用
```js
//注意闭合标签  <%=:  %>
<input type="button" value=<%=:p|first%>>
```
####8.给模板添加方法

    app.locals[‘say’] = function(){ return 'hello’; };
    在 app.locals 中定义的方法都可以在模板中引用
    <input type="button" value=<%=say()%>>
