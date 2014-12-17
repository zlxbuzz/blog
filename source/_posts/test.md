title: test
date: 2014-12-17 18:47:25
categories:
tags:
---
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
                                                                                                                                superagent.get(url.resolve(userUrl,author)).end(function(err,res){
                                                                                                                                                                var $ =cheerio.load(res.text);
                                                                                                                                                                                        var score=$('.user_profile .big').text();
                                                                                                                                                                                                                ep.emit('topic_html', [topicUrl, res.text,author,score]);
                                                                                                                                                                                                                                        })
                                                                                                                                          
                                                                                                                                                  });
                                                                                  });
                                                          });


