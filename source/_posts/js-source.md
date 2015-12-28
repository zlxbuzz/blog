title: js常用笔记
date: 2015-03-11 17:20:11
categories: js
tags: js
---
## 将时间戳转换成日期格式：
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

## 将日期格式转换成时间戳：
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

## js数组去重
```js
Array.prototype.unique3 = function(){
	var res = [];
	var json = {};
	for(var i = 0; i < this.length; i++){
		if(!json[this[i]]){
			res.push(this[i]);
			json[this[i]] = true;
		}
	}
	return res;
}
```

## 字符串截取

```js
substr(start [, length ])
返回一个从指定位置开始的指定长度的子字符串
substring(start, end)
返回位于 String 对象中指定位置的子字符串。
```

## 页面跳转
```js
window.navigate("top.jsp");
window.history.back(-1);
window.location.href="login.jsp?backurl="+window.location.href;
self.location='top.htm';
top.location='xx.jsp';
```

## 加载完成
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

## 刷新页面
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

## json转化和解析
```js
JSON.parse("{a:'111',b:'ccc'}");  //解析
eval("("+""+")"); //解析
```

## URI编码转换
```js
var a="':'";
en = encodeURI(a);    //编码
a = decodeURI(en);    //解码
```

## HTML编码转换
```js
function htmlEncode(value){
  return $('<div/>').text(value).html();
}

function htmlDecode(value){
  return $('<div/>').html(value).text();
}
```


## 当属性名是另一个表达式时候
```js
a.b[c] // (a.b)[c]
a[b] //而不用 a.b
```

## js转义字符实体
```js
function htmlEscape(s) {
	return (s + '').replace(/&/g, '&amp;')
		.replace(/</g, '&lt;')
		.replace(/>/g, '&gt;')
		.replace(/'/g, '&#039;')
		.replace(/"/g, '&quot;')
		.replace(/\n/g, '<br />');
}
```

## 判断number
```js
var isNumber = function(n) {
    return !isNaN(parseFloat(n)) && isFinite(n);
};
```

## js原型
```js
//每一个构造函数都有一个prototype属性，指向另一个对象。这个对象的所有属性和方法，都会被构造函数的实例继承
//任何一个prototype对象都有一个constructor属性，指向它的构造函数

//如果替换了prototype对象
　　o.prototype = {};
//下一步必然是为新的prototype对象加上constructor属性，并将这个属性指回原来的构造函数
o.prototype.constructor = o;
//Object和Function都是构造函数，所有的构造函数的都是Function的实例对象,Object是Function的实例对象
//Function.prototype是Object的实例对象
Object.__proto__ === Function.prototype
Function.__proto__ === Function.prototype
Function.prototype.__proto__ === Object.prototype
//instanceof的结果不要仅是: 如果右侧构造函数的prototype属性能在左侧的对象的原型链中找到,
// 那么就返回true, 否则就返回false
Object intanceof Function: Object.__proto__ === Function.prototype  //true
Function instanceof Object: Function.__proto__.__proto__ === Object.prototype //true
//实例对象的constructor属性指向其构造函数
Object.constructor === Function
Function.constructor === Function
```
## js继承
```js
　function extend(Child, Parent) {
　　　　var F = function(){};
　　　　F.prototype = Parent.prototype;
　　　　Child.prototype = new F();//空对象实例化几乎不占内存
　　　　Child.prototype.constructor = Child;
　　　　Child.uber = Parent.prototype;
　　}
```

## js判断是否存在
```js
if (typeof myObj == "undefined") {
　　　var myObj = { };
}
```

## 修正js默认验证信息
```js
<input type="text" ng-model="data.IDcard" class="form-control" required  pattern="\d{6}[12]\d{3}[01]\d{6}\w{1}" oninput="disValidate(this,'请输入18位身份证号码') "/>

<script>
    function disValidate(self,mes){
        self.validity.patternMismatch ? self.setCustomValidity(mes) : self.setCustomValidity('');
    }
</script>
## obj 转 arr
```js
function(obj){
  if(!obj){
	return [];
}
var keys = Object.keys(obj);

return keys.filter(function(key){
	return obj[key];
});
}
```

## js 操作cookie
```js
 getCookie:function(name){
        var arr,reg=new RegExp("(^| )"+name+"=([^;]*)(;|$)");
        if(arr=document.cookie.match(reg))
            return unescape(arr[2]);
        else
            return null;
       },
setCookie:function(name,value){
        var Days = 30;
        var exp = new Date();
        exp.setTime(exp.getTime() + Days*24*60*60*1000);
        document.cookie = name + "="+ escape (value) + ";expires=" + exp.toGMTString();
       }
```
