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

















## 2-5 常用模版语法讲解（2） (08:46)

















## 2-6 数据，方法，计算属性和侦听器（1） (15:47)

















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






























