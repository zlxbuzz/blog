title: angulajs的ui日历插件--ui-calendar
date: 2015-04-07 17:35:57
categories: angularjs
tags: [angularjs,angular-ui]
---
最近在做一个基于angularjs的项目，需要用到日历插件，基于jquery有一款插件[FullCalendar](http://fullcalendar.io/docs)。为了减少jquery的依赖性，还是采用一款基于angular的日历插件[ui-calendar](https://github.com/angular-ui/ui-calendar)，记录下使用方法。

##引入对应的js和css
[fullcalendar.css](https://raw.githubusercontent.com/buzzmjx/lib/master/fullcalendar/dist/fullcalendar.css) --fullcalendar的样式
[jquery.js](https://raw.githubusercontent.com/buzzmjx/lib/master/jquery.js) --jQuery插件
[angular.js](https://raw.githubusercontent.com/buzzmjx/lib/master/angular/angular.js) --angularjs插件
[calendar.js](https://raw.githubusercontent.com/buzzmjx/lib/master/fullcalendar/dist/calendar.min.js),[moment.js](https://raw.githubusercontent.com/buzzmjx/lib/master/moment/moment.js),[fullcalendar.js](https://raw.githubusercontent.com/buzzmjx/lib/master/fullcalendar/dist/fullcalendar.js),[gcal.js](https://raw.githubusercontent.com/buzzmjx/lib/master/fullcalendar/dist/gcal.js) --必要的js包
> **注意：**需要下载到本地使用。

```html
<link rel="stylesheet" href=" fullcalendar/dist/fullcalendar.css"/>
<script type="text/javascript" src=" jquery.js"></script>
<script type="text/javascript" src=" angular/angular.js"></script>
<script type="text/javascript" src=" moment/moment.js"></script>
<script type="text/javascript" src=" fullcalendar/dist/calendar.min.js"></script>
<script type="text/javascript" src=" fullcalendar/dist/fullcalendar.js"></script>
<script type="text/javascript" src=" fullcalendar/dist/gcal.js"></script>
```

##js初始化

####1.依赖注入
```js
var  myAppModule= angular.module('MyApp', ['ui.calendar']);

```

####2.简单配置
```js
myAppModule.controller('myappController',function($scope){
$scope.eventSources = [];//事件源

```

##### 根据api一共有多种数据的导入
	```js
		$scope.eventSource = {
				url: "http://www.google.com/calendar/feeds/usa__en%40holiday.calendar.google.com/public/basic",
				className: 'gcal-event',           // an option!
				currentTimezone: 'America/Chicago' // an option!
		};
	```
	
```js
$scope.events = [
  {title: 'All Day Event',start: new Date(y, m, 1)},
  {title: 'Long Event',start: new Date(y, m, d - 5),end: new Date(y, m, d - 2)},
  {id: 999,title: 'Repeating Event',start: new Date(y, m, d - 3, 16, 0),allDay: false},
  {id: 999,title: 'Repeating Event',start: new Date(y, m, d + 4, 16, 0),allDay: false},
  {title: 'Birthday Party',start: new Date(y, m, d + 1, 19, 0),end: new Date(y, m, d + 1, 22, 30),allDay: false},
  {title: 'Click for Google',start: new Date(y, m, 28),end: new Date(y, m, 29),url: 'http://google.com/'}
];
如果allDay 为 true 则时间块可以在日历中进行拖动
```

```js
$scope.eventsF = function (start, end, timezone, callback) {
  var s = new Date(start).getTime() / 1000;
  var e = new Date(end).getTime() / 1000;
  var m = new Date(start).getMonth();
  var events = [{title: 'Feed Me ' + m,start: s + (50000),end: s + (100000),allDay: false, className: ['customFeed']}];
  callback(events);
};
```

```js
$scope.calEventsExt = {
   color: '#f00',
   textColor: 'yellow',
   events: [ 
	  {type:'party',title: 'Lunch',start: new Date(y, m, d, 12, 0),end: new Date(y, m, d, 14, 0),allDay: false},
	  {type:'party',title: 'Lunch 2',start: new Date(y, m, d, 12, 0),end: new Date(y, m, d, 14, 0),allDay: false},
	  {type:'party',title: 'Click for Google',start: new Date(y, m, 28),end: new Date(y, m, 29),url: 'http://google.com/'}
	]
};
```

####3.对插件的参数配置
```js
$scope.uiConfig = {
	  calendar:{
		height: 450,//宽度
		editable: true,//可编辑
		header:{//各个部位的需要显示的内容
		  left: 'month basicWeek basicDay agendaWeek agendaDay',
		  center: 'title',
		  right: 'today prev,next'
		},
		dayClick: $scope.alertEventOnClick,//日期点击触发函数
		eventDrop: $scope.alertOnDrop,//日期拖拽出发函数
		eventResize: $scope.alertOnResize，
		eventResize //日期拉伸出发函数 这些函数写在配置的前面～
	  }
	};
});
```


####相关参数的中文
```js
$scope.uiConfig.calendar.dayNames = ["星期日", "星期一", "星期二", "星期三", "星期四", "星期五", "星期六"];
    $scope.uiConfig.calendar.dayNamesShort = ["星期日", "星期一", "星期二", "星期三", "星期四", "星期五", "星期六"];
    $scope.uiConfig.calendar.monthNamesShort = ["一月", "二月", "三月", "四月", "五月", "六月", "七月","八月","九月","十月","十一月","十二月"];
    $scope.uiConfig.calendar.monthNames = ["一月", "二月", "三月", "四月", "五月", "六月", "七月","八月","九月","十月","十一月","十二月"];
```


####常见的问题
```js
//由于ui-calendar的ng-model会生成标志_d等参数,如果进行ajax 清空重复赋值可能会出现数据无法重新加载的问题
//当点击下个月的按钮时可以采用slice方法将数组清空后重新赋值
$scope.uiConfig 下的calendar参数可以
viewRender:function(view){
	var date =new Date(view.intervalStart._d).getMonth()+1;
		workorderService.get({type:4,pid:$stateParams.sid,m:date},function(data){
		$scope.eventSources.splice(0,1);
		$scope.events=[];
		var result=datas.handle(data);
		if(result){
			$scope.workorders=result.workorders;
			for(var i in $scope.workorders){
				$scope.events.push({
					'title':'<i class="ace-icon fa fa-barcode" style="color:'+$scope.workorders[i].color+'"></i> '+$scope.workorders[i].wkname,
					'start':$scope.workorders[i].jihua_date,
					'allDay':true,
					'backgroundColor':'white',
					'textColor':'black',
					'borderColor':'white',
					'wkid':$scope.workorders[i].wkid
				});			
			}
			$scope.eventSources.push($scope.events);
		}
	});
}
```
