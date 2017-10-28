# ajax

## XHR
XHR是负责ajax运作的核心对象。XHR定义了一个用脚本操纵HTTP的API，能以多种形式返回服务器的响应 (XML/文本)。
1. 创建XMLHttpRequest对象
	var req = new XMLHttpRequest();
2. open方法启动请求
	req.open(http-method，url，async);
	* URL使用相对路径，绝对路径会报错（同源策略）
	* async值为true 或 false
 	* async为false发送同步请求，js会等待请求返回，获取status。异步则需要onreadystatechange事件处理，当readystate=4响应完成。须在调用open()前指定onreadystatechange事件处理才能确保跨浏览器兼容性。 
3. send方法发送请求
	req.send()；参数为请求主体entity-body。GET无主体。
	
当收到服务器响应后，响应数据会自动填充XHR对象的属性：
* responseText：作为响应主体返回文本；
* responseXML：响应内容类型为”text/xml”或”application/xml”，则保存包含响应数据的XML文档；
* status和statusText；
___
## CORS跨域
* IE8通过XDomainRequest对象支持CORS，其他通过XHR对象支持CORS。CORS稳定，但不兼容低版本IE。
* 当JavaScript向外域（如sina.com）发起请求后，浏览器收到响应后，首先检查Access-Control-Allow-Origin是否包含本域，如果不是，则请求失败，js无法获取到响应的任何数据。
* 假设本域是my.com，外域是sina.com，只要响应头Access-Control-Allow-Origin为http://my.com，或者是*，本次请求就可以成功。
* 跨域能否成功，取决于对方服务器是否愿意给你设置一个正确的Access-Control-Allow-Origin，决定权始终在对方手中。

## JSONP跨域
JSONP把JSON包裹在函数里面发送HTTP请求，通过设置<script>的URL来发送跨域HTTP请求
* 通过script的src请求资源,浏览器允许跨域引用js,不受同源策略约束。
* 请求的资源中用回调函数的将数据进行包裹
* 调用方要定义回调函数

