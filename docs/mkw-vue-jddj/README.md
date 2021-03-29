# 什么是闭包？
------

> 闭包：闭包就是访问另一个函数作用域变量的函数

> 闭包简单定义为在一个函数内部的函数

> 形成闭包的原因：存在上级作用域的引用

变量的作用域
------

变量的作用域分为两种：全局变量和局部变量

1.  javascript的特殊之处--函数内部可以直接读取全局变量

```js
    var a = 10; 
    function f1(){
    console.log(a);
    }
    f1();
```

> `f1()`是在全局下创建的，所以`a`的上级作用域就是`window`,输出的是`10`

2.  函数外部不能读取函数内的局部变量

```js
    function f2(){
        var  b = 1;
    }
     console.log(b); 
```

> `f2()`的`b`是函数内部的局部变量，函数外部不能读取，`console.log(b)`的`b`作用域是全局(window),然而全局中并未定义`b`,所以报错.

3.这里有一个地方需要注意，函数内部声明变量的时候，一定要使用var命令。如果不用的话，你实际上声明了一个全局变量！

```js
     function f2(){
        b = 1;
    }
      f2();
     console.log(b); 
```

```js
     function f2(){
      var b = 1;
      console.log(b);
    }
    f2();
    console.log(b);

```

[阮一峰的学习JavaScript闭包(Closure)](http://www.ruanyifeng.com/blog/2009/08/learning_javascript_closures.html)

初识闭包
----

```js
    function foo(){
        var a = 2;
        function bar(){
            console.log(a);
        }
        return bar;
    }
    var baz=foo();
    baz();
    
```

> `bar()`词法作用域能访问`foo()`的内部作用域，将`bar()`函数对象本身当作返回值。`foo()`执行后，其返回值（也就是内部的bar()函数）赋值给变量`baz`并调用`baz()`,实际上只是通过不同的标识符引用调用了内部的函数`bar()`.在`foo()`执行后，通常会期待`foo()`的整个内部作用域都被销毁，因为我们知道引擎有垃圾回收器用来释放不在使用的内存空间.由于看上去`foo()`内容不会再被使用，所以很自然地会考虑对其进行回收。

> 闭包的神奇之处正是可以阻止这件事情发生，事实上内部作用域依然存在，因此没有被回收。谁在使用这个内部作用域呢？原来是`bar()`本身在使用。`bar()`拥有涵盖`foo()`内部作用域的闭包，使得该作用域能够一直存活，以供`bar()`在之后任何时间进行引用。`bar()依然持有对该作用域的引用，而这个引用就叫做闭包。`

分析闭包经典使用场景
----------

### 1\. 使用return 返回函数

```js
function foo(){
    var a = 2;
    function bar(){
         console.log(a);
    }
    return bar;
}
var baz = foo();
baz(); 
```

**其实可以这样写，如下：** 

```js
function foo(){
    var a = 2;
    function bar(){
       console.log(a);
    }
    return bar;
}
foo()();
```

> `bar`函数是一个闭包,它在`foo`函数内部定义的函数

### 知识拓展--简化

*   f()执行f函数，返回子函数
*   f()()执行子函数，返回孙函数
*   f()()()执行孙函数，返回重孙函数

> 注意：但注意，如果想这样执行，函数结构必须是这样，f的函数体里要return 子函数，子函数里要return 孙函数，如果没有return关键字，是不能这样连续执行的，会报错的。

```js
    function fun(){
        return 5 
    }
    var a=fun
    var b=fun()
    console.log(a); 
    console.log(b);
```

```js
    function fun(){
        return k;
        function k(){
           return '555 '
        }

    }
    var a=fun;
    var b=fun();
    var kk=fun()();
    console.log(a); 
    console.log(b);
    console.log(kk); 
```

> 函数只要是要调用它进行执行的，都必须加括号。此时，函数实际上等于函数的返回值或者执行效果，当然，有些没有返回值，但已经执行了函数体内的行为，就是说，加括号的，就代表将会执行函数体代码。

### 2\. 函数作为参数

```js
var a = '函数外'
function fo(){
    var a = ' fo 函数内'
    function foo(){
        console.log(a)
    }
    return foo
}

function f(p){
    var a = 'f 函数内'
    p()
}
f(fo())
```

> 使用`retuen foo` 返回, `foo()`是一个闭包，f(fo())执行的参数就是函数`foo`,因为`foo()`中 `console.log(a)` 中的`a`的上级作用域是函数`fo`,所以输出的是`fo`函数内部定义的`a`的内容`fo 函数内`。

`思考`：如果将上面的f()函数改一下你是否能理解？如果你能理解那么上面的`补充知识`你也懂了。

```js
var a = '函数外'
function fo(){
    var a = ' fo 函数内'
    function foo(){
        console.log(a)
    }
    return foo
}

function f(p){
    var a = 'f 函数内'
    p()()
}
f(fo)
```

### 3.IIFE(自执行函数)

```js
    var a = 2;
    (function IIFE(){
        console.log(a);
    })() 
```

> 这样产生的是闭包`IIFE()`,但是严格来讲它并不是闭包，为什么？因为`IIFE()`并不是在它本身的词法作用域以外执行的。自执行函数本身是没有变量作用域的，因此会使用外层函数的变量作用域。所以输出为`2`.尽管`IIFE`本身并不是观察闭包的恰当例子，但它的确创建了闭包，并且也是最常用来创建可以被封闭起来的闭包的工具。因此`IIFE`的确同作用域息息相关，即使本身并不会真的创建作用域。

### 4\. 定时器setTimeout（回调函数都是闭包）

```js
    function wait(m){
        setTimeout(function timer(){
            console.log(m);
        },1000) 
    } 
    wait("Hello");
```

> 闭包`timer`传递给 `setTimeout()`。`timer()`具有涵盖`wait()`作用域的闭包，因此保存了对变量`m`的引用。`wait()`执行1000毫秒后，它的内部作用域并不会消失,`timer()`函数依然保有`wait()`作用域的闭包。

### 知识拓展-回调函数

> 一个函数被作为参数传递给另一个函数（在这里我们把另一个函数叫做“otherFunction”），回调函数在otherFunction中被调用。`注意回调函数都是闭包`

*   将回调函数的参数作为与回调函数同等级的参数进行传递

![](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/2911a14fc8f24ea3b16503facc7962fc~tplv-k3u1fbpfcp-watermark.jpg)

*   回调函数的参数在调用回调函数内部创建

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/b970620e70c64e4297dc01421ea23240~tplv-k3u1fbpfcp-watermark.jpg)

### 5.循环和闭包

`思考下面的代码:`

```js
for(var i = 1;i<=5;i++ ){
    (function(){
           setTimeout(function timer(){
            console.log(i);
            },i*1000)
     })();
    }

```

> 输出的答案是什么呢？`1，2，3，4，5？`错误正确输出是`6,6,6,6,6,6`。为什么呢？解析一下6是从哪来的？相信你和我一开始一样都是千百个`？？？`，而且循序的终止条件是`i`不在是`<=5`。条件首次成立时`i`的值为6，因此，输出显示的是循环结束`i`的最终值。延迟函数的回调会在循环结束时才会执行，不管定时器 `setTimeout`的时间是多少，所有的回调函数依然是在循环结束后才会被执行，因此每一次都是输出一个6来。

`想要输出1，2，3，，4，5的结果，那么要如何修改我们的代码呢？`

#### 方法一(传参)

```js
    for(var i = 1;i<=5;i++ ){
    (function(j){
           setTimeout(function timer(){
            console.log(j);
            },j*1000)
     })(i);
    }
    
```

> 通过传参的方法，将`i`传递进去，将变量名取为`j` 来获取`i`的值

#### 方法二(定义变量接收i的值)

```js
    for(var i = 1;i<=5;i++ ){
    (function(){
            var j=i;
           setTimeout(function timer(){
            console.log(j);
            },j*1000)
     })();
    }
    
```

> 通过定义变量的方法，将变量名取为`j`用来在每个迭代中存储i的值

#### 方法三(将var改为let)

```js
    for(let i = 1;i<=5;i++ ){
    (function(){
           setTimeout(function timer(){
            console.log(i);
            },i*1000)
     })();
    }
    
```

> `for`循环头部使用`let`声明，`let`具有块级作用域，`let`每次迭代都会声明，随后的每个迭代都是使上一个迭代结束时的值来初始化这个变量,迭代变量的作用域仅限于for循环块内部。`let可以在任意代码块中隐式的创建或是劫持块作用域`；`var`声明的其中块代码的作用域是全局的，所以当执行完循环之后运行`setTimeout`中闭包之后，其中引用的`i`就是全局作用域中的`i`，然而let就不会。

#### 知识拓展-- `let`和`var`的区别

```js
   for(let i = 0;i<=5;i++){
        console.log(i);
    }
    console.log(i,'----');
    
```

```js
    for(var i = 0;i<=5;i++){
        console.log(i);
    }
    console.log(i,'++++');
    
```

> `var`在`for循环`头部声明变量`i`,在`for循环`结束后`i`会被暴露在全局作用域中，然而`let`就不会，因为`let可以在任意代码块中隐式的创建或是劫持块作用域`

思考题
---

### 思考题1

```js
　var name = "The Window";
　　var object = {
　　　　name : "My Object",
　　　　getNameFunc : function(){
　　　　　　return function(){
            
　　　　　　　　return this.name;  
　　　　　　};
　　　　}
　　};
console.log( object.getNameFunc()());
```

> 输出的是`The Window`还是`"My Object`？首先我们需要了解`this.name`中`this`指向的到底是什么？

### 思考题1解答

> `this`指向的是全局(window)因为上一级`getNameFunc()`函数没有`name` 属性 ,因此就去找全局的`name`属性,所以输出`“The Window”`

### 思考题2

```js
  var name = "The Window";
　　var object = {
　　　　name : "My Object",
　　　　getNameFunc : function(){
　　　　　　var that = this;   
　　　　　　return function(){
　　　　　　　　return that.name;
　　　　　　};
　　　　}
　　};
　console.log(object.getNameFunc()());
```

> 输出的是`The Window`还是`"My Object`？首先我们需要了解`that = this`中`this`指向的到底是什么？

### 思考题2解答

> 将`this`赋值给一个变量，内部函数是可以访问外部函数变量的.所以`this`指向的是`object`,由于`this`关键字不是在包含的函数中引用的，而是通过`that=this`这个调用的，所以这个`this`不是在闭包内的，因此这个`this`就不能调用函数体内的全局对象，而是他的局部对象`object.name`，所以输出的是`"My Object"`

使用闭包注意点
-------

> 1）由于闭包会使得函数中的变量都被保存在内存中，内存消耗很大，所以不能滥用闭包，否则会造成网页的性能问题，在IE中可能导致内存泄露。解决方法是，在退出函数之前，将不使用的局部变量全部删除。

> 2）闭包会在父函数外部，改变父函数内部变量的值。所以，如果你把父函数当作对象（object）使用，把闭包当作它的公用方法（Public Method），把内部变量当作它的私有属性（private value），这时一定要小心，不要随便改变父函数内部变量的值。

总结
--

> 闭包第一次去认真了解，初识闭包发现里面涉及的知识很多，让我对于js的认识更加深刻了！如果有问题欢迎指出，谢谢您的阅读！本人大三，正在学习前端，欢迎大家一起学习探讨！

参考
--

[面试 | JS 闭包经典使用场景和含闭包必刷题](https://juejin.cn/post/6937469222251560990#heading-2)

[阮一峰的学习JavaScript闭包(Closure)](http://www.ruanyifeng.com/blog/2009/08/learning_javascript_closures.html)

[js 彻底理解回调函数](https://blog.csdn.net/baidu_32262373/article/details/54969696)