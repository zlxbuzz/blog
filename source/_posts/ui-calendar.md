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
```js
var  myAppModule= angular.module('MyApp', ['ui.calendar']);
myAppModule.controller('myappController',function($scope){
	$scope.eventSources = [];
	 $scope.uiConfig = {
		  calendar:{
			height: 450,
			editable: true,
			header:{
			  left: 'month basicWeek basicDay agendaWeek agendaDay',
			  center: 'title',
			  right: 'today prev,next'
			},
			dayClick: $scope.alertEventOnClick,
			eventDrop: $scope.alertOnDrop,
			eventResize: $scope.alertOnResize
		  }
		};
});
```
