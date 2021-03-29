# 目录

* [Vue3 系统入门与项目实战](mkw-vue-jddj/README)



<output>
<div id="root"></div>
</output>

<script>
    // Vue.createApp 创建vue实例
    Vue.createApp({
        data(){
            return {
                content: 1
            }
        },
        // 页面加载完成执行的函数
        mounted(){
            setInterval(()=>{
                this.content += 1
            },1000)
        },
        template: '<div>{{content}}</div>'
    }).mount('#root')
</script>
