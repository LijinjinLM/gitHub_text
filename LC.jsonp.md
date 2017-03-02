
[slide]
##ajax-jsonp
[slide]
#同源策略
同源策略就是规定了javascript*可以操作*那些web内容的一个完整的安全限制。

[slide]
#什么是同源？
同源就是规定多个*web*资源的*url*中`scheme(协议)`、`hostname(域名或IP)`、`port(端口)`必须相同，只要有一项不同那么这个`web`资源就不是同源的。

[slide]
#什么是跨域？
当请求的资源的*URL*与**当前页面**的*URL*中的`scheme(协议)`、`hostname(域名或IP)`、`port(端口)`有一个不同的时候就算是跨域操作。

[slide]
#JSONP
* *script*元素可以作为一种*Ajax*传输协议
* 只需设置*script*元素的`src`属性并且插入到*DOM*中，浏览器就会发出一个*HTTP*请求到*src*属性所指向的*URL*。
* script不受*同源策略*的影响
* script元素会*自动下载*并**执行**下载的数据
* 使用这种script元素来进行*Ajax*数据的传输的技术就叫做*JSONP*,也就是`JSON－Padding`.
```
//服务器不可以返回这样的数据
["baidu","telnet","alibaba"]
//服务器会返回一个这样的响应
functionName(["baidu","telnet","alibaba"])
```
> 其中的*functionName*必须是在*window*下可以访问的名称


[slide]
#JSONP 的实现步骤  客户端
* 在页面中加入```<script>```标签 其src属性设置为 服务器的数据请求地址
* 示例
```
<script type="text/javascript"
src=http://matchweb.sports.qq.com/kbs/calendar?columnId=100000">
```
* 第2步  在你页面中的js代码中定义一个函数，函数名随便，要有一个参数，名字随便，这个函数用来接收服务器端返回的数据，并完成接收数据后的后续操作，类似于AJAX中的onreadystatechange事件的回调函数
```
     function getInfo(data) {

        console.log(data);

    }
```
[slide]
#JSONP 的实现步骤  客户端(2)
*  在刚才添加的script标签的src的地址中加入一个参数，参数名一般叫做callback(cb),参数的值就是你刚才定义的函数的名字
```<script type="text/javascript" src="http://matchweb.sports.qq.com/kbs/calendar?callback=getInfo&columnId=100000">
```
* 你所添加的这个函数，会在服务器端数据返回后自动执行，不需要你去调用
* 所有的JSONP请求必须是get请求  不能是post
[slide]
#JSONP 的实现步骤  服务器端
* 服务器端首先从客户端请求中获取callback参数的值 fn
* 服务器端返回给客户端的数据不再是json格式 而是一个字符串
  这个字符串的组成是: fn(数据);
* 服务器端其实并不是直接返回的数据，而是返回的是一段js代码
  ,这个js代码的内容是: fn(数据).其中的fn是客户端通过callback参数传给服务器的函数名，
  所以客户端收到 fn(数据) 这段字符串后，就会将其视作可执行的js代码直接调用执行。
* 前提是服务器端在设置响应头时 要设置为Content-Type:text/javascript


[slide]
#示例
```
function search(){
  var script = document.createElement('script');
  var keyword = document.getElementById('keyword').value;
  script.src = 'http://suggestion.baidu.com/su?wd=a&cb=show';
  script.src = 'http://localhost/search?keyword='+keyword+'&callback=show';
  document.body.appendChild(script);
}
```
