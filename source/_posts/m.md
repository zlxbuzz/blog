title: 移动端收集
date: 2016-10-18 14:10:08
tags:
---

```


## flex相关

```js
flex布局下的img标签默认会撑满整个屏幕，需要设置百分比来限制高度


```

## 弹窗蒙层滚动遇到的坑

```js

移动端局部滚动我一般都用
overflow:auto;/*android*/
-webkit-overflow-scrolling:touch;/*iphone*/


但是`-webkit-overflow-scrolling`有比较多的坑，网上有很多介绍，我这里说下我遇到的问题的解决方案：
1.fixed元素不能放在有`-webkit-overflow-scrolling:touch`中的容器内，尽量放在和他同级的地方,或者将touch改成auto。
2.由于`fastclick`在部分手机内会有兼容问题，比如body为100%高度，内容却超出了这个高度，则这个内容超出的部分点击事件会有坑，所以建议所有的页面都放在100%高度的容器中，如果有弹出框等蒙层效果的dom，一律已fixed放在body下面即可。

或者所有的移动端滚动采用`better-scroll`等动画库
```

##  华为等部分android手机可能出现最终的font－size不一致的情况

```c
#默写华为手机 设置的fontSize，不等于最终编译得到的
getComputedStyle(html).fontSize 和 html.style.fontSize 不一致
所以可能会导致rem的计算有问题。

解决方法就是让计算出来的getComputedStyle(html).fontSize 的值等于html.style.fontSize

可以通过循环或者比例相除的方式计算

比如:
    做一个循环
    不断的获取parseInt(window.getComputedStyle(html).fontSize),如果返回值等于
    parseInt(html.style.fontSize),则html.setAttribute('style', 'font-size:'+font + 'px!important');
    否则parseInt(html.style.fontSize)＋＋
```


##  华为部分手机不支持jusify-content space-between

```
如题，采用autoprefixer也是无效，后来就用了子元素的flex属性，要实现两边排列的效果，
首先必须是块元素，左右的子元素flex设为1，右边不设置（默认为自身大小即可）

```



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




## padding控制图片自适应

```
//背景图,padding值为百分比
.banner {
    padding: 10% 0 0;
    background-size: cover;
}

//img
<div class="banner">
  <img src=""banner.jpg>
</div>

.banner {
    padding: 15.15% 0 0;
    position: relative;
}
.banner > img {
    position: absolute;
    width: 100%; height: 100%;
    left: 0; top: 0;
}


```
