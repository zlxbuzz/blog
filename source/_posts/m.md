title: 移动端收集
date: 2016-10-18 14:10:08
tags:
---


## 滚动
```c
  问题:
      ios4 和 android2.2 以下不支持 position:fixed
      ios 和 android2.3 以下不支持 overflow:auto
      ios4 和 android 不支持 overflow-scrolling
  # 滚动穿透问题解决:
  # 在列表容器的父元素上设置样式overflow:hidden来禁用滚动
  #切换弹窗时候切换类名
  $('html').addClass('noscroll');$('html').removeClass('noscroll');
```
## 垂直居中
```c
  margin: auto;
  position: absolute;
  top: 0; left: 0; bottom: 0; right: 0;
```
先将div left，top分别50%，则div的上边和左边分别定位到了中间，之后再用margin进行width/2的left和height/2的top位移，正好就定位到了中间


```js

    position: relative;
    left: 50%; //相对于父级
    transform: translate(-50%);//translate如果是％，则基于自身的高度和宽度
```


```c
    position:absolute;
    top:50%;
    left:50%;
    border:1px solid #eee;
    margin-left:-330px;
    margin-top:-165px;
    width:660px;
    height:331px;
```

## placeholder 颜色

```css
    :-moz-placeholder { /* Mozilla Firefox 4 to 18 */
        color: #f00;
    }

    ::-moz-placeholder { /* Mozilla Firefox 19+ */
        color: #f00;
    }

    input:-ms-input-placeholder,
    textarea:-ms-input-placeholder {
        color: #f00;
    }

    input::-webkit-input-placeholder,
    textarea::-webkit-input-placeholder {
        color: #f00;
    }
```

## input 相关
 如果给一个input设置了readonly属性，为了防止光标出现，可以采用onfocus="this.blur()"属性。

 禁止表单自动填充，在前面加一个 <input type="password"/> 并设置css让不在页面中出现即可。

```html
<input type="password" style={{position: 'absolute', top: '-999px'}}/>
<input type="text" name="username"/>
```


## background-image 比img 更加节省资源

##  line-height相关
字体有个默认高度，如果希望外部块级元素自适应字体的高度，需要设置line-height=1;



##  移动端1px问题
当采用lib-flex的时候，android中经常会遇到border 1px问题。其实这和border没有关系，只要是1px，2px这种比较小的高度或者长度，在一些机型中都会出现问题，
当采用rem作为单位的时候，当最终计算出来的px小于1px时候，就会出现线条粗细不一，甚至消失的情况，这里我设置了min-height:1px这个属性，同时设置height:xxrem
左右高清适配方案，目前解决了大部分问题.

```js
http://www.cnblogs.com/surfaces/p/5158582.html
/* //采用背景图的方式，webkit内核方向和w3c方向相反。有点问题,暂时不用。 */
/* //分别生成bottom和right */
/* background-image:-webkit-linear-gradient(90deg, #e0e0e0, #e0e0e0 50% ,transparent 50%),-webkit-linear-gradient(270deg, #e0e0e0, #e0e0e0 50% ,transparent 50%); */
/* background-image:linear-gradient(0, #e0e0e0, #e0e0e0 50% ,transparent 50%),linear-gradient(90deg, #e0e0e0, #e0e0e0 50% ,transparent 50%); */
/* background-position:bottom,right; */
/* background-size:100% 1px,1px 100%;/*!no*/ */
/* background-repeat:no-repeat; */


//由于lib-flex 对未对android做dpr的处理，所以导致android上的线条过粗，这里采用transform的方式将border缩放，形成1px的效果，目前缩放.5就可以满足视觉，主要用了一个less的mixin.
//设置下边线
.setBottomLine(@c: #C7C7C7) {
  & {
    position: relative;
  }
  &:after {
    content: " ";
    position: absolute;
    left: 0;
    bottom:0;
    width: 100%;
    height:1px;
    border-bottom: 1px solid @c;
  }

  [data-dpr="1"] &:after{
    transform-origin: 0 0;
    transform: scaleY(0.5);
  }
}
//设置下右边线
setBRLine(@c: #C7C7C7) {
  & {
    position: relative;
  }

  &:after {
    content: " ";
    position: absolute;
    top: 0;
    right:0;
    width:100%;
    height: 100%;
    border-right: 1px solid @c;
    border-bottom: 1px solid @c;
  }

  [data-dpr="1"] &:after {
    width:200%;
    height: 200%;
    transform-origin: 0 0;
    transform: scale(0.5);
  }
}
```



## font
css定义了5种字体：
1.serif 上下有短线进行装饰。
2.sans-serif 没有上下短线。
3.monospace 字符宽度完全相同。
4.cursive 可能有弯曲，或者由花体部分和小的弯曲部分组成。
5.fantasy 其他。


## line-height
假如font-size为14px，line-height设置为18px，其差除以2，得到的2分别到内容区
的顶部和地步，则会获得一个18px的行内框(inline box).

## float相关

```
float 具有包裹性和破坏性
float 几乎等同于display:inline-block（没有多个inline-block中间有空格的bug）,
```

## android 点击输入框上移

```js
if(/Android [4-6]/.test(navigator.appVersion)) {
   window.addEventListener("resize", function() {
        if(document.activeElement.tagName=="INPUT" || document.activeElement.tagName=="TEXTAREA") {
            window.setTimeout(function() {
                document.activeElement.scrollIntoViewIfNeeded();
            },0);
        }
    })
}
```


##  倒计时

```js
//倒计时一般采用setTimeout，来解决误差
/**
 * @brief 倒计时
 *
 * @param cb 每 interval 触发的回调函数
 * @param interval 事件间隔(毫秒)
 * @param ms 倒计时时间差，默认为当前时间(毫秒)
 */
const countDown = (cb,interval,ms) =>{

  var interval  = interval || 1000;
  var ms        = ms || new Date().getTime();
  cb(ms);
  //当前时间戳，用来计算时间误差
  var startTime = new Date().getTime();
  var count     = 0;
  if(ms > 0){
    var watcher = setTimeout(__countDown,interval);
  }

  function __countDown(){
    count++;
    var offset = new Date().getTime() - (startTime + count * interval);
    var nextTime = interval - offset ;
    if(nextTime < 0 ){
      nextTime = 0;
    }
    ms-=interval;
    if(ms < 0){
      clearTimeout(watcher);
    }else{
      cb(ms);
      watcher = setTimeout(__countDown,nextTime);
    }
  }
}

```


## 图片

```js
background-size  有cover和contain，如果比原图片大 则cover会往外放大，反之会往内缩小，
img则设置100%即可.


```


## axios

如果是android 4.4.4以下不支持promise，需要 `require('es6-promise').polyfill();`
不支持ios7



