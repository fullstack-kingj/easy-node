**在本节课中，我们将学习如何接收客户端发送的请求，并且如何处理这些请求数据。**

在官方示例中，我们可以掌握了通过 HTTP 模块的 `createServer()` 方法创建服务器，并且掌握了其回调函数中的 `res` 参数，该参数表示响应对象。

但，在其回调函数还包含了另一个参数 `req`，表示客户端请求的对象。

```javascript
const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello World\n');
});
```

## Request 请求对象

作为 `http.createServer()` 方法的回调函数的第一个参数 `req` 是 `http.IncomingMessage` 对象，它可用于访问响应状态、标题和数据。

### 1. `http.IncomingMessage` 对象的常用属性

`http.IncomingMessage` 对象用于读取客户端请求流中的数据，该对象提供一系列属性:

| 属性名称 | 描述 |
| --- | --- |
| url | 请求的 URL 字符串 |
| method | 请求方法，例如 GET 等|
| headers | 请求头信息 |
| httpVersion | HTTP 版本 |

通过如下示例代码测试 `IncomingMessage` 对象的上述属性内容:

```javascript
const http = require('http');

const server = http.createServer(function(req, res){
    if (req.url != '/favicon.ico'){
        console.log('message.url: '+req.url);
        console.log('message.method: '+req.method);
        console.log('message.headers: '+JSON.stringify(req.headers));
        console.log('message.httpVersion: '+req.httpVersion);
        res.end();
    }
});
server.listen('3000', '127.0.0.1', function(){
    console.log('Server is running.');
});
```

上述示例代码，运行后的结果如下图所示:

![](images/Snip20161211_22.png)
￼
### 2. `stream.Readable` 接口的事件

`IncomingMessage` 对象还实现了 `stream.Readable` 接口，`stream.Readable` 接口提供了 data 和 end 事件。

* data 事件会在从客户端请求流中读取到新数据时触发。
* end 事件会在客户端请求流中的数据读取完毕时触发。

```javascript
const http = require('http');

const server = http.createServer(function(req, res){
    if (req.url != '/favicon.ico') {
        req.on('data', function (data) {
            console.log('Data of the client: ' + decodeURIComponent(data));
        });
        req.on('end', function () {
            console.log('Data stream is readed.');
        });
        res.end();
    }
});
server.listen('3000', '127.0.0.1', function(){
    console.log('Server is running.');
});
```

上述示例代码，运行后的结果如下图所示:

![](images/Snip20161211_23.png)
￼
如果我们创建一个 HTML 页面，并且请求上述服务器，情况会有所不同。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>IncomingMessage</title>
</head>
<body>
    <form action="http://127.0.0.1:3000/" method="post">
        Username: <input type="text" name="username"><br>
        Password: <input type="text" name="password"><br>
        <input type="submit">
    </form>
</body>
</html>
```

通过浏览器访问上述 HTML 页面:

![](images/Snip20161211_24.png)
￼
输入数据后，点击【提交】按钮，效果如下图所示：
￼
![](images/Snip20161211_25.png)

## URL 模块

通过 `http.IncomingMessage` 对象的 url 属性可以得到客户端的请求流中的 URL 字符串。而 URL 模块是包含了专门用于分析和解析 URL 字符串的工具。

想要掌握 URL 模块的内容，首先需要先对 URL 有个基本的了解。

### 1. URL 格式

完整的 URL 语法格式如下:

```
protocol :// [username:password @] hostname[:port] / path / [;parameters][?query]#fragment
```

| 语法内容 | 描述 |
| --- | --- |
| protocol | 协议名称，例如 HTTP 等 |
| username | 登录名称，用于登录认证 |
| password | 登录密码，用于登录认证 |
| hostname | 服务器地址，可以是 IP 地址或者域名 |
| port | 端口号 |
| path | 文件的路径，可以是相对路径或绝对路径 |
| parameters | 请求参数，用于指定特殊参数 |
| query | 查询字符串，用于发送给服务器的数据 |
| fragment | 片段标示符，多指锚点等 |

完成的 URL 内容，例如如下示例:

```
http://user:pass@host.com:8080/p/a/t/h?query=string#hash
```

在了解了 URL 的完整格式后，再来看看 Node.js 的 URL 模块所提供的方法。

### 2. url.parse() 方法

`url.parse()` 方法的具体语法结构如下:

```javascript
url.parse(urlStr[, parseQueryString][, slashesDenoteHost])
```

- urlStr 参数: 必要参数，指定需要转换的 URL 字符串。
- parseQueryString 参数: 可选参数，是否使用 Query Strings 模块转换查询字符串。默认为 false，表示不使用 Query Strings 模块转换。
- slashesDenoteHost 参数: 可选参数，是否将 hostname 单独解析。默认为 false，不解析。

具体用法可参考如下示例代码:

```javascript
const url = require('url');

console.log(url.parse('http://user:pwd@127.0.0.1:8888/users/user.html?username=jinyunlong&pwd=12345#age'));
```

上述代码示例，运行结果如下:

```
Url {
  protocol: 'http:',
  slashes: true,
  auth: 'user:pwd',
  host: '127.0.0.1:8888',
  port: '8888',
  hostname: '127.0.0.1',
  hash: '#age',
  search: '?username=jinyunlong&pwd=12345',
  query: 'username=jinyunlong&pwd=12345',
  pathname: '/users/user.html',
  path: '/users/user.html?username=jinyunlong&pwd=12345',
  href: 'http://user:pwd@127.0.0.1:8888/users/user.html?username=jinyunlong&pwd=12345#age' 
}
```

如果指定使用 Query Strings 模块对查询字符串进行解析，调用 `url.parse()` 方法时的第二个参数设置为 true。如下代码所示:

```javascript
const url = require('url');

console.log(url.parse('http://user:pwd@127.0.0.1:8888/users/user.html?username=jinyunlong&pwd=12345#age', true));
```

输出的内容则如下所示:

```
Url {
  protocol: 'http:',
  slashes: true,
  auth: 'user:pwd',
  host: '127.0.0.1:8888',
  port: '8888',
  hostname: '127.0.0.1',
  hash: '#age',
  search: '?username=jinyunlong&pwd=12345',
  query: { username: 'jinyunlong', pwd: '12345' },
  pathname: '/users/user.html',
  path: '/users/user.html?username=jinyunlong&pwd=12345',
  href: 'http://user:pwd@127.0.0.1:8888/users/user.html?username=jinyunlong&pwd=12345#age' 
}
```

上述两个示例之间的区别仅在于 query 字段的值。

### 3. url.format() 方法

`url.formate()` 方法的具体语法结构如下:

```javascript
url.format(urlObj)
```

如上述语法格式，urlObj 参数表示一个解析过的并需要还原的 URL 对象。该方法返回一个还原后的 URL 字符串。如下述示例代码:

```javascript
const url = require('url');

const urlObj = url.parse('http://user:pwd@127.0.0.1:8888/users/user.html?username=jinyunlong&pwd=12345#age',true)

console.log(url.format(urlObj));
```

上述示例代码运行后，最终会得到一个被还原的 URL 字符串:

```
http://user:pwd@127.0.0.1:8888/users/user.html?username=jinyunlong&pwd=12345#age
```

### 4. url.resolve() 方法

`url.resolve()` 方法的具体语法结构如下:

```javascript
url.resolve(from, to)
```

该方法表示将两个路径结合成为一个路径。第一个参数表示起点路径字符串，第二个参数表示参考路径字符串。

*这两个路径既可以是相对路径，也可以是绝对路径。*

## Query Strings 模块

Node.js 的 Query Strings 模块提供用于处理查询字符串的实用工具。

### 1. querystring.parse() 方法

`querystring.parse()` 方法的具体语法结构如下:

```javascript
querystring.parse(str[, sep][, eq][, options])
```

- str 参数: 表示需要转换的查询字符串。
- sep 参数: 表示分隔符`&`。
- eq 参数: 表示分隔符`=`。
- options 参数: maxKeys 属性用来限制处理过的健值。默认值为 1000，如果为 0 的话可以去掉键值的数量限制。decodeURIComponent 属性用来设置解析编码格式。

`querystring.parse()` 方法具体的用法如下:

```javascript
> querystring.parse('foo=bar&baz=qux&baz=quux&corge')
{ foo: 'bar', baz: [ 'qux', 'quux' ], corge: '' }
```

### 2. querystring.stringify() 方法

`querystring.stringify()` 方法的具体语法结构如下:

```javascript
querystring.stringify(obj[, sep][, eq][, options])
```

- obj 参数: 表示需要转换的对象。
- sep 参数: 表示分隔符`&`。
- eq 参数: 表示分隔符`=`。
- options 参数: maxKeys 属性用来限制处理过的健值。默认值为 1000，如果为 0 的话可以去掉键值的数量限制。decodeURIComponent 属性用来设置解析编码格式。

`querystring.stringify()` 方法具体的用法如下:

```javascript
> querystring.stringify({ foo: 'bar', baz: ['qux', 'quux'], corge: '' })
'foo=bar&baz=qux&baz=quux&corge='
> querystring.stringify({foo: 'bar', baz: 'qux'}, ';', ':')
'foo:bar;baz:qux'
```