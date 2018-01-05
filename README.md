# cloudgo-io

设计一个 web 小应用，展示静态文件服务、js 请求支持、模板输出、表单处理、Filter 中间件设计等方面的能力。（不需要数据库支持）

## 基本要求
1. 支持静态文件服务 
2. 支持简单 js 访问
3. 提交表单，并输出一个表格对 
4. /unknown 给出开发中的提示，返回码 5xx

## 支持静态文件服务
<li>访问localhost:8080就可以看到一个简单的登陆页面，输入并提交，会返回一个写着你的密码和用户名的表格。访问localhost:8080/unknown会返回一个501错误。   
 使用了Negroni的logging中间件，第一次访问是这样的：</li><code>[negroni] listening on :8080
[negroni] 2017-11-16T05:34:13-08:00 | 200 | 	 2.357753ms | localhost:8080 | GET / 
[negroni] 2017-11-16T05:34:13-08:00 | 200 | 	 56.266µs | localhost:8080 | GET /main.css 
[negroni] 2017-11-16T05:34:13-08:00 | 200 | 	 25.696µs | localhost:8080 | GET /test.js 
[negroni] 2017-11-16T05:34:13-08:00 | 404 | 	 36.723µs | localhost:8080 | GET /favicon.ico 
[negroni] 2017-11-16T05:34:13-08:00 | 404 | 	 37.846µs | localhost:8080 | GET /favicon.ico </code>
<li>程序相应了客户端的请求，返回了主页以及静态目录的css文件和js文件，显示其支持静态文件服务</li>

## 支持简单 js 访问
访问localhost:8080/api，则会返回一串JSON数据

## 提交表单，并输出一个表格对 
json数据可以在服务器端看到
<code>[negroni] 2017-11-16T06:49:38-08:00 | 200 | 	 113.166µs | localhost:8080 | GET /api </code>

## /unknown 给出开发中的提示，返回码 5xx
访问localhost:8080/unknown浏览器会看见501 not implement的字样
服务器端显示501错误
<code>[negroni] 2017-11-16T07:00:57-08:00 | 501 | 	 61.707µs | localhost:8080 | GET /unknown </code>
