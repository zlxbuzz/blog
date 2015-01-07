title: nodejs-lesson4 的挑战功能
date: 2014-12-18 10:52:52
categories: nodejs
tags: [node]
---
##Node.js 包教不包会的lession4的挑战功能
https://github.com/buzzmjx/node-lessons/tree/master/lesson4
主要思路是在每次并发请求每条文章的时候，获取作者名，同时访问到作者的页面抓取作者的积分信息
```js
var eventproxy = require('eventproxy');
var superagent = require('superagent');
var cheerio = require('cheerio');
var url = require('url');

var cnodeUrl = 'https://cnodejs.org/';
var userUrl='https://cnodejs.org/user/';
superagent.get(cnodeUrl)
  .end(function (err, res) {
    if (err) {
      return console.error(err);
    }
    var topicUrls = [];
    var $ = cheerio.load(res.text);
    $('#topic_list .topic_title').each(function (idx, element) {
      var $element = $(element);
      var href = url.resolve(cnodeUrl, $element.attr('href'));
      topicUrls.push(href);
    });

    var ep = new eventproxy();

    ep.after('topic_html', topicUrls.length, function (topics) {
      topics = topics.map(function (topicPair) {
        var topicUrl = topicPair[0];
        var topicHtml = topicPair[1];
        var $ = cheerio.load(topicHtml);
        return ({
          title: $('.topic_full_title').text().trim(),
          href: topicUrl,
          comment1: $('.reply_content').eq(0).text().trim(),
          author:topicPair[2],
          score:topicPair[3]
        });
      });
	console.log(topics);
    
    });

    topicUrls.forEach(function (topicUrl) {
      superagent.get(topicUrl)
        .end(function (err, res) {
		var $=cheerio.load(res.text);
		var author=$('.changes').find("a").text();
		superagent.get(url.resolve(userUrl,author)).end(function(err,res1){
			var $ =cheerio.load(res1.text);
			var score=$('.user_profile .big').text();
			ep.emit('topic_html', [topicUrl, res.text,author,score]);
			})
          
        });
    });
  });


```
