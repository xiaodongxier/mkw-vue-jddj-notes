# 第2章 Vue 基础语法

> 本章中，将会讲解生命周期函数，指令，模版，数据，侦听器，事件，循环渲染等基础语法知识点，帮助大家理解第一章重写过的代码，同时理解数据驱动的编程思想。


## 2-1 Vue 中应用和组件的基础概念 (09:32)


```html
<div id="root"></div>
<script>
    // createAppApp 表示创建一个Vue应用 (App为Applocation的缩写)，存储在app变量中
    // 传入的参数表示，这个应用最外层的组件应该如果展示
    // 面向数据编程参考 mvvm 设计模式  m-> model 数据，v-> view 视图，viewModel-> 视图数据连接层
    const app = Vue.createApp({
        data(){
            return {
                message: "hello world"
            }
        },
        template:"<div>{{message}}</div>"
    })

    // vm 代表的就是 vue 应用的跟组件
    const vm = app.mount('#root')
</script>
```

<output>
    <div id="list2-1-1"></div>
</output>
<script>
const app = Vue.createApp({
    data(){
        return {
            message: "hello world"
        }
    },
    template:"<div>{{message}}</div>"
})
const vm = app.mount('#list2-1-1')
</script>



##  2-2 理解 Vue 中的生命周期函数（1） (10:49)

![lifecycle](./media/lifecycle.png)


```html
<div id="root"></div>
<script>
    // 生命周期函数：在某一时刻自动执行的函数
    const app = Vue.createApp({
        data(){
            return {
                message: "hello world"
            }
        },
        // 实例创建之前自动执行的函数
        beforeCreate(){
            console.log("beforeCreate")  
        },
        // 初始化结束 事件 生命周期函数 依赖注入 双向绑定 实例创建完成 都分析结束后执行
        // --实例创建之后自动执行的函数--
        created(){
            console.log("created")  
        },
        // 判断实例是否存在templatr模版选项
        // yes 存在   模版变成一个函数(vue底层代码实现)  &  no 不存在
        // --在组件内容被渲染到页面之前立即执行的函数--
        beforeMount(){
            console.log("beforeMount")  
        },
        // 函数与数据进行一些结合
        // --在组件内容被渲染到页面之后自动执行的函数--
        mounted(){
            console.log("mounted")  
        },
        template:"<div>{{message}}</div>"
    })
    const vm = app.mount('#root')
</script>
```

## 2-3 理解 Vue 中的生命周期函数（2） (12:56)


```html
<div id="root"></div>
<script>
    // 生命周期函数：在某一时刻自动执行的函数
    const app = Vue.createApp({
        data(){
            return {
                message: "hello world"
            }
        },
        // 实例创建之前自动执行的函数
        beforeCreate(){
            console.log("beforeCreate")  
        },
        // 初始化结束 事件 生命周期函数 依赖注入 双向绑定 实例创建完成 都分析结束后执行
        // --实例创建之后自动执行的函数--
        created(){
            console.log("created")  
        },
        // 判断实例是否存在templatr模版选项
        // yes 存在   模版变成一个函数(vue底层代码实现)  &  no 不存在template 寻找dom节点里面的进行处理
        // --在组件内容被渲染到页面之前立即执行的函数--
        beforeMount(){
            console.log("beforeMount")  
            console.log(document.getElementById("root").innerHTML,"beforeMount")
        },
        // 函数与数据进行一些结合
        // --在组件内容被渲染到页面之后自动执行的函数--
        mounted(){
            console.log("mounted")  
            console.log(document.getElementById("root").innerHTML,"mounted")
        },
        // 当( date 中的)数据发生变化时会执行的函数
        beforeUpdate(){
            console.log("beforeUpdate")
            console.log(document.getElementById("root").innerHTML,"beforeUpdate")
        },
        // 当( date 中的)数据发生变化,同时页面完成更新后，会自动执行的函数
        updated(){
            console.log("updated")
            console.log(document.getElementById("root").innerHTML,"updated")
        },
        // 当vue应用失效时，自动执行的函数
        beforeUnmount(){
            console.log("beforeUnmount")
            console.log(document.getElementById("root").innerHTML,"beforeUnmount")
        },
        // 当vue应用失效时，且dom完全销毁之后，自动执行的函数
        unmounted(){
            console.log("unmounted")
            console.log(document.getElementById("root").innerHTML,"unmounted")
        },
        template:"<div>{{message}}</div>"
    })
    const vm = app.mount('#root')
</script>
```

## 2-4 常用模版语法讲解（1） (09:55)


> v-html

```html
<div id="demo2_2_1"></div>
<script>
    const app2_2_1 = Vue.createApp({
        data() {
            return {
                message: "<h1>hello world</h1>"
            }
        },
        template: "<div v-html='message'></div>"
    })

    const vm2_2_1 = app2_2_1.mount('#demo2_2_1')
</script>
```

<iframe height="300" style="width: 100%;" scrolling="no" title="Vue3系统入门与项目实战-常用模版语法" src="https://codepen.io/xiaodongxier/embed/zYNoXJX?height=265&theme-id=dark&default-tab=js,result" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/xiaodongxier/pen/zYNoXJX'>Vue3系统入门与项目实战-常用模版语法1</a> by 小东西儿
  (<a href='https://codepen.io/xiaodongxier'>@xiaodongxier</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>



> v-bind 

```html
<div id="demo2_2_2"></div>
<script>
    const app2_2_2 = Vue.createApp({
        data() {
            return {
                message: "hello world"
            }
        },
        template: "<div :title='message'>{{message}}</div>"
    })
    const vm2_2_2 = app2_2_2.mount('#demo2_2_2')
</script>
```

<iframe height="300" style="width: 100%;" scrolling="no" title="Vue3系统入门与项目实战-常用模版语法2" src="https://codepen.io/xiaodongxier/embed/NWdbmmy?height=265&theme-id=dark&default-tab=js,result" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/xiaodongxier/pen/NWdbmmy'>Vue3系统入门与项目实战-常用模版语法2</a> by 小东西儿
  (<a href='https://codepen.io/xiaodongxier'>@xiaodongxier</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>



> v-bind 可以与输入框的这些属性进行绑定

```html
<div id="demo2_2_3"></div>
<script>
    const app2_2_3 = Vue.createApp({
        data() {
            return {
                disable1: false,
                disable2: true
            }
        },
        template: 'false:<input type="text" :disabled="disable1"> <br> true:<input type="text" :disabled="disable2">'
    })

    const vm2_2_3 = app2_2_3.mount('#demo2_2_3')
</script>
```

<iframe height="300" style="width: 100%;" scrolling="no" title="Vue3系统入门与项目实战-常用模版语法3" src="https://codepen.io/xiaodongxier/embed/yLgVWBG?height=265&theme-id=dark&default-tab=js,result" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/xiaodongxier/pen/yLgVWBG'>Vue3系统入门与项目实战-常用模版语法3</a> by 小东西儿
  (<a href='https://codepen.io/xiaodongxier'>@xiaodongxier</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>



> 可以写一些全局的方法 & js语句是不行的 & 此处需要补充 js方法与语句的区别

```html
<div id="demo2_2_6"></div>
<script>
    const app2_2_6 = Vue.createApp({
        data() {
            return {
                message: "hello world"
            }
        },
        // 判断最大值
        template: "<div>{{Math.max(1,2,3,4)}}</div>"
    })
    const vm2_2_6 = app2_2_6.mount('#demo2_2_6')
</script>
```

<iframe height="300" style="width: 100%;" scrolling="no" title="Vue3系统入门与项目实战-常用模版语法5" src="https://codepen.io/xiaodongxier/embed/rNjWgyB?height=265&theme-id=dark&default-tab=js,result" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/xiaodongxier/pen/rNjWgyB'>Vue3系统入门与项目实战-常用模版语法4</a> by 小东西儿
  (<a href='https://codepen.io/xiaodongxier'>@xiaodongxier</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>



> v-once  变量只渲染一次

```html
<div id="demo2_2_7"></div>
<script>
    const app2_2_7 = Vue.createApp({
        data() {
            return {
                message: "hello world"
            }
        },
        template: "<div v-once>{{message}}</div>"
    })
    const vm2_2_7 = app2_2_7.mount('#demo2_2_7')
</script>
```


<iframe height="300" style="width: 100%;" scrolling="no" title="Vue3系统入门与项目实战-常用模版语法5" src="https://codepen.io/xiaodongxier/embed/VwPmOWb?height=265&theme-id=dark&default-tab=js,result" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/xiaodongxier/pen/VwPmOWb'>Vue3系统入门与项目实战-常用模版语法5</a> by 小东西儿
  (<a href='https://codepen.io/xiaodongxier'>@xiaodongxier</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>



> v-if  变量只渲染一次 & 如果是false 那么 dom节点被移除

```html
<div id="demo2_2_8"></div>
<script>
    const app2_2_8 = Vue.createApp({
        data() {
            return {
                message: "hello world",
                show: false
            }
        },
        template: "<div v-if='show'>{{message}}</div>"
    })
    const vm2_2_8 = app2_2_8.mount('#demo2_2_8')
</script>
```

<iframe class="wyj" height="350" style="width: 100%;" scrolling="no" title="Vue3系统入门与项目实战-常用模版语法6" src="https://codepen.io/xiaodongxier/embed/NWdbVaE?height=265&theme-id=dark&default-tab=js,result" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/xiaodongxier/pen/NWdbVaE'>Vue3系统入门与项目实战-常用模版语法6</a> by 小东西儿
  (<a href='https://codepen.io/xiaodongxier'>@xiaodongxier</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>


## 2-5 常用模版语法讲解（2） (08:46)


> 指令简写
> v-on:  简写 @   
> v-bind:  简写 :



> 动态属性 :[title]     :[event]


```html
<!-- 动态属性(动态参数) -->
<div id="demo2_2_9"></div>
<script>
    const app2_2_9 = Vue.createApp({
        data() {
            return {
                message: "hello world",
                name: "title",
                event: "mouseenter"
            }
        },
        methods: {
            handleBtnClick(){
                alert("click")
            }
        },
        // 模版事件绑定的时候，方法一定是写在 methods 对象里面的，否则是不生效的
        template: `<div 
                        @[event]='handleBtnClick'
                        :[name]='message'
                        >{{message}}</div>`
    })
    const vm2_2_9 = app2_2_9.mount('#demo2_2_9')
</script>
```

<iframe height="500" style="width: 100%;" scrolling="no" title="Vue3系统入门与项目实战-常用模版语法7-动态属性" src="https://codepen.io/xiaodongxier/embed/KKaWPXr?height=265&theme-id=dark&default-tab=js,result" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/xiaodongxier/pen/KKaWPXr'>Vue3系统入门与项目实战-常用模版语法7-动态属性</a> by 小东西儿
  (<a href='https://codepen.io/xiaodongxier'>@xiaodongxier</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>



> 修饰符 简化常用代码的缩写 

```html
<div id="demo2_2_10"></div>
<script>
    const app2_2_10 = Vue.createApp({
        data() {
            return {
                message: "hello world",
                name: "title",
                event: "mouseenter"
            }
        },
        methods: {
            handleClick(e){
                // e.preventDefault();
            }
        },
        // 模版事件绑定的时候，方法一定是写在 methods 对象里面的，否则是不生效的
        template: `<form action="https://www.baidu.com" @click.prevent="handleClick">
                        <button type="submit">提交</button>
                    </form>`
    })
    const vm2_2_10 = app2_2_10.mount('#demo2_2_10')
</script>   
```

<iframe height="500" style="width: 100%;" scrolling="no" title="Vue3系统入门与项目实战-常用模版语法8-修饰符" src="https://codepen.io/xiaodongxier/embed/GRrWKQM?height=265&theme-id=dark&default-tab=js,result" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/xiaodongxier/pen/GRrWKQM'>Vue3系统入门与项目实战-常用模版语法8-修饰符</a> by 小东西儿
  (<a href='https://codepen.io/xiaodongxier'>@xiaodongxier</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>


## 2-6 数据，方法，计算属性和侦听器（1） (15:47)

> vm_2_6_1.$data.message
> vm_2_6_1.message （第一层数据也可以这样获取）


```html
<div id="demo_2_6_1"></div>
<script>
    const app_2_6_1 = Vue.createApp({
        data() {
            return {
                message: "hello world"
            }
        },
        template: "<div>{{message}}</div>"
    })

    const vm_2_6_1 = app_2_6_1.mount("#demo_2_6_1")
</script>
```
























































## 2-7 数据，方法，计算属性和侦听器（2） (06:10)

















## 2-8 样式绑定语法 (12:48)

















## 2-9 条件渲染 (06:41)

















## 2-10 列表循环渲染（1） (11:38)

















## 2-11 列表循环渲染（2） (10:45)

















## 2-12 事件绑定（1） (13:28)

















## 2-13 事件绑定（2） (07:15)

















## 2-14 表单中双向绑定指令的使用（1） (07:54)

















## 2-15 表单中双向绑定指令的使用（2） (07:22)

















## 2-16 表单中双向绑定指令的使用（3） (08:51)






























