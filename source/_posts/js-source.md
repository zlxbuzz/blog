title: js常用笔记
date: 2015-03-11 17:20:11
categories: js
tags: js
---
####将时间戳转换成日期格式：
```js
var date = new Date(时间戳);
Y = date.getFullYear() + '-';
M = (date.getMonth()+1 < 10 ? '0'+(date.getMonth()+1) : date.getMonth()+1) + '-';
D = date.getDate() <10 ? '0'+date.getDate() : date.getDate() + ' ';
h = date.getHours() + ':';
m = date.getMinutes() + ':';
s = date.getSeconds(); 
console.log(Y+M+D+h+m+s);
```

####将日期格式转换成时间戳：
```js
date = new Date('2014-04-23 18:55:49:123');
// 有三种方式获取
time1 = date.getTime()
time2 = date.valueOf()
time3 = Date.parse(date)

// 三种获取的区别
//第一、第二种：会精确到毫秒
//第三种：只能精确到秒，毫秒将用0来代替
// 比如上面代码输出的结果(一眼就能看出区别)：
//    1398250549123
//    1398250549123
//    1398250549000 
```


####字符串截取

```js
substr(start [, length ])
返回一个从指定位置开始的指定长度的子字符串
substring(start, end)
返回位于 String 对象中指定位置的子字符串。
```

####页面跳转
```js
window.navigate("top.jsp");
window.history.back(-1);
window.location.href="login.jsp?backurl="+window.location.href; 
self.location='top.htm';
top.location='xx.jsp';
```

####加载完成
```js
window.onload 
必须等页面内包括图片的所有元素加载完成后才能执行。
不能同时编写多个，只执行一个
$(document).ready()
是DOM结构绘制完毕后就可以执行
可以编写多个
简写$(function(){});
$(window).load()等同与window.onload
```

####刷新页面
```js
history.go(0) 
location.reload() 
location=location 
location.assign(location) 
document.execCommand('Refresh') 
window.navigate(location) 
location.replace(location) 
document.URL=location.href 
```

####json转化和解析
```js
JSON.parse("{a:'111',b:'ccc'}");  //解析
eval("("+""+")"); //解析
```

####URI编码转换
```js
var a="':'";
en = encodeURI(a);    //编码
a = decodeURI(en);    //解码
```

####HTML编码转换
```js
function htmlEncode(value){
  return $('<div/>').text(value).html();
}

function htmlDecode(value){
  return $('<div/>').html(value).text();
}
```
