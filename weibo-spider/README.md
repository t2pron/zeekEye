# weibo-Spider
##-- Programmable spidering of web sites with Java
weibo-spider
============

新浪微博爬虫，采用Java语言开发，使用hetrix爬虫架构，基于HTTPClient 4.0和Apache4.0网络包，采用SQLServer存储爬取数据，支持多进程并发执行。
功能包括：模拟微博登录、爬取微博用户信息、用户评论、提取数据、建立数据表、互粉推荐。待更新...
欢迎Fork!!!


## 安装

使用以下代码:

<pre>
  git clone git@github.com:crazyacking/Spider--Java.git
  cd Spider--Java
  npm link ../Spider--Java
</pre>

## API(如何使用)

### Creating a Spider
<pre>
  var spider = require('spider');
  var s = spider();
</pre>

#### weibo-Spider(选项)

"选项"包含一下字段：
* `maxSockets` - 线程池中最大并行线程数. 默认为 `4`.
* `userAgent` - 发送到远程服务器的用户代理请求. 默认为 `Mozilla/5.0 (Macintosh; U; Intel Mac OS X 10_6_4; en-US) AppleWebKit/534.7 (KHTML, like Gecko) Chrome/7.0.517.41 Safari/534.7` (firefox userAgent String).
* `cache` -  用作缓存的缓存对象。默认为非缓存，看最新代码缓存对象的实现细节。
* `pool` - 一个包含该请求代理的哈希对象。如果省略，将使用全局设置的maxsockets。

### 添加路由处理程序

#### spider.route(主机，模式)
其中参数如下 :

* `hosts` - A string -- or an array of string -- representing the `host` part of the targeted URL(s).
* `pattern` - The pattern against which spider tries to match the remaining (`pathname` + `search` + `hash`) of the URL(s).
* `cb` - A function of the form `function(window, $)` where
  * `this` - Will be a variable referencing the `Routes.match` return object/value with some other goodies added from spider. For more info see https://github.com/aaronblohowiak/routes.js
  * `window` - Will be a variable referencing the document's window.
  * `$` - Will be the variable referencing the jQuery Object.

### 爬虫抓取网址队列.

`spider.get(url)`其中'url'是要抓取的网络url.

### 拓宽 / 更新缓存

目前更新缓存提供了以下方法:

* `get(url, cb)` - Returns `url`'s `body` field via the `cb` callback/continuation if it exists. Returns `null` otherwise.
  * `cb` - Must be of the form `function(retval) {...}`
* `getHeaders(url, cb)` - Returns `url`'s `headers` field via the `cb` callback/continuation if it exists. Returns `null` otherwise.
  * `cb` - Must be of the form `function(retval) {...}`
* `set(url, headers, body)` - Sets/Saves `url`'s `headers` and `body` in the cache.

### 设置冗余/日志级别
`spider.log(level)` - Where `level` is a string that can be any of `"debug"`, `"info"`, `"error"`