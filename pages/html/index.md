<!-- ![这是html基础思维导图](https://github.com/4sean/4sean.github.io/tree/master/pages/images/html.png "这是html基础思维导图") -->

## 你不知道的HTML
### 一、开发工具
推荐 Sublime Text （最主要的优点：轻量、性能高）

插件推荐： Emmet 概括地说，Emmet（译者注：前身就是以前大名鼎鼎的Zen Coding，这个如果你没听说和使用过，就悲哀了）是一个可以让你更快更高效地编写HTML和CSS，节省你大量时间的插件。怎么使用？你只需按约定的缩写形式书写而不用写整个代码，然后按“扩展”键，这些缩写就会自动扩展为对应的代码内容。

Material Theme 主题插件，界面看起来清爽优化。

Comic Sans MS 这个是英文字体，一个看起来舒服的英文字体，能够让开发在写代码时，心情更加愉悦。比如说，后面这段调皮的代码： console.info("Hello World");

备注：统一编辑器的好处

1).作为团队开发，统一的编辑器可以尽量减少团队的沟通的成本 2).好的编辑器能够提高团队的开发效率，无论从写代码的角度，还是审美的角度。

---

### 二、前端跨域请求解决方案
1. 什么是同源
2. 同源策略限制的对象（跨域）
3. 如何设置同源策略（hosts）
4. 怎么突破同源策略

#### 1.同源策略
先来说说什么是源？
源（origin）就是协议、域名和端口号。

同源策略是浏览器的一个安全功能，不同源的客户端脚本在没有明确授权的情况下，不能读写对方资源。所以a.com下的js脚本采用ajax读取b.com里面的文件数据是会报错的。

同源就是：
```
- 协议相同
- 域名相同
- 端口号相同
```

举例来说，==http://www.example.com/dir/page.html==这个网址，协议是==http://==，域名是==www.example.com==，端口是==80==（默认端口可以省略）。它的同源情况如下。
```
http://www.a.com/dir/page.html ----成功
http://www.child.a.com/test/index.html ----失败，域名不同
https://www.a.com/test/index.html ----失败，协议不同
http://www.a.com:8080/test/index.html ----失败，端口号不同
```

#### 2.同源策略限制的对象（跨域）
```
1. Cookie、LocalSotrage和IndexDB无法读取
2. DOM无法获得
3. AJAX请求不能发送
```

#### 3. 如何设置同源策略（hosts）


不受同源策略限制的：
浏览器不同的域名不能访问对应的cookie但是内部的表单没有限制
页面中的链接，重定向以及表单提交是不会受到同源策略限制的。


跨域资源的引入是可以的。但是js不能读写加载的内容。如嵌入到页面中的<script src="..."></script>，<img>，<link>，<iframe>等。

### 跨域
  1. 概念：受到浏览器同源策略的影响，要操作其他源下面的脚本，就需要跨域。
### Ajax跨域的解决方案
  1. JSONP：网页添加一个`<script>`元素，向服务器请求jsON数据。服务器收到请求后，将数据放在一个指定名字的回调函数里传回来。
  - 缺点只支持get请求
  - 优点简单方便，易理解，兼容性良好
  - 如下示例代码
  ```
    //动态创建script，用于跨越操作
    function creatScriptTag(src) {
      var script = document.createElement('script');
      script.setAttribute("type","text/javascript");
      script.src = src;
      document.body.appendChild(script);
    }
    // 调用creatScriptTag函数
    window.onload = function () {
      var url = '/index.php?jsoncallback=result';
      creatScriptTag(url);
    }
    // 定义回调函数
    function result (data) {
      console.log(data);
    } 
  ```
  ```
    // index.php 
    <?php
    header('Content-type: application/json');
    //获取回调函数名
    $jsoncallback = htmlspecialchars($_REQUEST ['jsoncallback']);
    //取数据
    $data = [
      'data'=>'123',
    ];
    $json_data = json_encode(array('code'=>'200','msg'=>'请求成功','data' => $data),jsON_UNESCAPED_UNICODE);
    //输出jsonp格式的数据
    echo $jsoncallback ."(" . $json_data . ")";
    ?>
  ```
  2. WebSocket:是一种通信协议，使用ws://（非加密）和wss://（加密）作为协议前缀。该协议不实行同源政策，只要服务器设置利用origin字段设置白名单，就可以通过它进行跨源通信。
  3. CORS（Cross-Origin Resource Sharing）
   - 在请求头信息中增加Origin字段，用来说明此次请求来自那个源（协议+域名+端口），此字段可以设置相应白名单
   - 必须设置`Access-Control-Allow-Origin`字段，值要求是`Origin`字段的值或者是*，*的意思是接受任意域名的请求
   - CORS请求默认不发送cookie和http认证信息，如果要发送，要在服务器端指`Access-Control-Allow-Credentials: true`,并且ajax请求必须打开withCredentials属性
   ```
   var xhr = new XMLHttpRequest();
   xhr.withCredentials = true;
   ```
   - 如果选择发送cookie,`Access-Control-Allow-Origin`字段不能设为*，必须指定明确的，与当前网页一致的域名
