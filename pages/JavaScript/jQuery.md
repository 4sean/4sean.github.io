jQuery无new 构造
```
// 无 new 构造
$('#test').text('Test');
 
// 当然也可以使用 new
var test = new $('#test');
test.text('Test');
```

```
(function(window, undefined) {
    var
    // ...
    jQuery = function(selector, context) {
        // The jQuery object is actually just the init constructor 'enhanced'
        // 看这里，实例化方法 jQuery() 实际上是调用了其拓展的原型方法 jQuery.fn.init
        return new jQuery.fn.init(selector, context, rootjQuery);
    },
 
    // jQuery.prototype 即是 jQuery 的原型，挂载在上面的方法，即可让所有生成的 jQuery 对象使用
    jQuery.fn = jQuery.prototype = {
        // 实例化化方法，这个方法可以称作 jQuery 对象构造器
        init: function(selector, context, rootjQuery) {
            // ...
        }
    }
    // 这一句很关键，也很绕
    // jQuery 没有使用 new 运算符将 jQuery 实例化，而是直接调用其函数
    // 要实现这样,那么 jQuery 就要看成一个类，且返回一个正确的实例
    // 且实例还要能正确访问 jQuery 类原型上的属性与方法
    // jQuery 的方式是通过原型传递解决问题，把 jQuery 的原型传递给jQuery.prototype.init.prototype
    // 所以通过这个方法生成的实例 this 所指向的仍然是 jQuery.fn，所以能正确访问 jQuery 类原型上的属性与方法
    jQuery.fn.init.prototype = jQuery.fn;
 
})(window);
```

大部分人初看 jQuery.fn.init.prototype = jQuery.fn 这一句都会被卡主，很是不解。但是这句真的算是 jQuery 的绝妙之处。理解这几句很重要，分点解析一下：

1）首先要明确，使用 $('xxx') 这种实例化方式，其内部调用的是 return new jQuery.fn.init(selector, context, rootjQuery) 这一句话，也就是构造实例是交给了 jQuery.fn.init() 方法去完成。

2）将 jQuery.fn.init 的 prototype 属性设置为 jQuery.fn，那么使用 new jQuery.fn.init() 生成的对象的原型对象就是 jQuery.fn ，所以挂载到 jQuery.fn 上面的函数就相当于挂载到 jQuery.fn.init() 生成的 jQuery 对象上，所有使用 new jQuery.fn.init() 生成的对象也能够访问到 jQuery.fn 上的所有原型方法。

3）也就是实例化方法存在这么一个关系链  

jQuery.fn.init.prototype = jQuery.fn = jQuery.prototype ;
new jQuery.fn.init() 相当于 new jQuery() ;
jQuery() 返回的是 new jQuery.fn.init()，而 var obj = new jQuery()，所以这 2 者是相当的，所以我们可以无 new 实例化 jQuery 对象。