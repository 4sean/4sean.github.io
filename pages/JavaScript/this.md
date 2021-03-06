# this 的指向

在ES5中，其实this的指向，始终坚持一个道理：**this永远指向最后调用它的那个对象**。

下面举个例子：

例1：

```
var name = 'windowName';
funciton a(){
    var name = 'Cherry';
    console.log(this.name); //windowName
    console.log('inner:' + this); //inder :window
}
a();
console.log('outer:' + this) // outer:window
```

根据'**this永远指向最后调用它的那个对象**',最后调用==a== 的地方 ==a();==,前面没有调用的对象，那么就是全局对象window，这就相当于是==window.a()==;注意，这里我们没有使用严格木事，如果使用严格模式的话，全局对象就是==undifined==，那么就会报错==Uncaught TypeError: Cannot read property 'name' of undefined==。

再看下这个例子：

例 2：

```
 var name = "windowsName";
    var a = {
        name: "Cherry",
        fn : function () {
            console.log(this.name);      // Cherry
        }
    }
    a.fn();

```

在这个例子中，函数 fn 是对象 a 调用的，所以打印的值就是 a 中的 name 的值。

我们做一个小小的改动：

例 3：

```
var name = "windowsName";
    var a = {
        name: "Cherry",
        fn : function () {
            console.log(this.name);      // Cherry
        }
    }
    window.a.fn();

```
这里打印 Cherry 的原因也是因为刚刚那句话“**this 永远指向最后调用它的那个对象**”，最后调用它的对象仍然是对象 a。

我们再来看一下这个例子：

例 4：


```
 var name = "windowsName";
    var a = {
        // name: "Cherry",
        fn : function () {
            console.log(this.name);      // undefined
        }
    }
    window.a.fn();

```
这里为什么会打印 undefined 呢？这是因为正如刚刚所描述的那样，调用 fn 的是 a 对象，也就是说 fn 的内部的 this 是对象 a，而对象 a 中并没有对 name 进行定义，所以 log 的 this.name 的值是 undefined。
这个例子还是说明了：this 永远指向最后调用它的那个对象，因为最后调用 fn 的对象是 a，所以就算 a 中没有 name 这个属性，也不会继续向上一个对象寻找 this.name，而是直接输出 undefined。

再来看一个比较坑的例子：

例 5：

```
 var name = "windowsName";
    var a = {
        name : null,
        // name: "Cherry",
        fn : function () {
            console.log(this.name);      // windowsName
        }
    }

    var f = a.fn;
    f();

```
这里你可能会有疑问，为什么不是 ==Cherry==，这是因为虽然将 a 对象的 fn 方法赋值给变量 f 了，但是没有调用，再接着跟我念这一句话：“**this 永远指向最后调用它的那个对象**”，由于刚刚的 f 并没有调用，所以 ==fn()== 最后仍然是被 window 调用的。所以 this 指向的也就是 window。

由以上五个例子我们可以看出，this 的指向并不是在创建的时候就可以确定的，在 es5 中，永远是**this 永远指向最后调用它的那个对象**。

再来看一个例子：

例 6：


```
  var name = "windowsName";

    function fn() {
        var name = 'Cherry';
        innerFunction();
        function innerFunction() {
            console.log(this.name);      // windowsName
        }
    }

    fn()

```


# **怎么改变 this 的指向**

```
- 使用 ES6 的箭头函数
- 在函数内部使用 _this = this
- 使用 apply、call、bind
- new 实例化一个对象
```

例 7：


```
var name = "windowsName";

    var a = {
        name : "Cherry",

        func1: function () {
            console.log(this.name)     
        },

        func2: function () {
            setTimeout(  function () {
                this.func1()
            },100);
        }

    };

    a.func2()     // this.func1 is not a function

```
在不使用箭头函数的情况下，是会报错的，因为最后调用 setTimeout 的对象是 window，但是在 window 中并没有 func1 函数。

我们在改变 this 指向这一节将把这个例子作为 demo 进行改造。


### **箭头函数**
众所周知，ES6 的箭头函数是可以避免 ES5 中使用 this 的坑的。箭头函数的 this 始终指向函数定义时的 this，而非执行时。，箭头函数需要记着这句话：“箭头函数中没有 this 绑定，必须通过查找作用域链来决定其值，如果箭头函数被非箭头函数包含，则 this 绑定的是最近一层非箭头函数的 this，否则，this 为 undefined”。


例 8 ：

```
  var name = "windowsName";

    var a = {
        name : "Cherry",

        func1: function () {
            console.log(this.name)     
        },

        func2: function () {
            setTimeout( () => {
                this.func1()
            },100);
        }

    };

    a.func2()     // Cherry

```

## 在函数内部使用 ==_this = this==

如果不使用 ES6，那么这种方式应该是最简单的不会出错的方式了，我们是先将调用这个函数的对象保存在变量 _this 中，然后在函数中都使用这个 _this，这样 _this 就不会改变了。

例 9：
```
  var name = "windowsName";

    var a = {

        name : "Cherry",

        func1: function () {
            console.log(this.name)     
        },

        func2: function () {
            var _this = this;
            setTimeout( function() {
                _this.func1()
            },100);
        }

    };

    a.func2()       // Cherry

```

这个例子中，在 func2 中，首先设置 var _this = this;，这里的 this 是调用 func2 的对象 a，为了防止在 func2 中的 setTimeout 被 window 调用而导致的在 setTimeout 中的 this 为 window。我们将 this(指向变量 a) 赋值给一个变量 _this，这样，在 func2 中我们使用 _this 就是指向对象 a 了。


### 使用 apply、call、bind

例 10：

```
  var a = {
        name : "Cherry",

        func1: function () {
            console.log(this.name)
        },

        func2: function () {
            setTimeout(  function () {
                this.func1()
            }.apply(a),100);
        }

    };

    a.func2()            // Cherry

```
### 使用 call

例 11：

```
 var a = {
        name : "Cherry",

        func1: function () {
            console.log(this.name)
        },

        func2: function () {
            setTimeout(  function () {
                this.func1()
            }.call(a),100);
        }

    };

    a.func2()            // Cherry

```


引用：https://juejin.im/post/59bfe84351882531b730bac2

