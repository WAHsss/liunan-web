## 过滤器
> 概念：Vue.js允许你自定义过滤器，**可被用作一些常见的文本格式化**。过滤器可以用在两个地方：**mustache插值和v-bind表达式**。过滤器应该被添加在JavaScript表达式的尾部，由"管道"符指示

语法：
> {{ msg | filterName }}
- Vue.filter('过滤器的名称',function(data){})
- 过滤器中的function ，第一个参数已经被规定死了，永远都是过滤器 管道符前面传递过来的数据。

## 定义Vue全局的过滤器
```
<!-- 把 "单纯" 换成 "可爱" 再输出 -->
<div id="app">
    <p>{{ msg | msgFormat | test }}</p>
    <p>{{ msg | msgFormat1('可爱！！') }}</p>
</div>
<script>
    // 定义一个 Vue全局的过滤器，叫做 msgFormat
    Vue.filter('msgFormat',function(msg){
        // 字符串的 replace 方法，第一个参数，除了可写一个 字符串之外，还可以定义一个正则
        return msg.replace(/单纯/g,'可爱~')
    })
    // 也可以给过滤器传递参数
    Vue.filter('msgFormat1',function(msg,arg){
        return msg.replace(/单纯/g,arg)
    })
    // 可以调用多个过滤器
    Vue.filter('test',function(msg){
        return msg+'======'
    })

    var app = new Vue({
        el:"#app",
        data:{
            msg:'曾经，我也是个单纯的少年，单纯的我，问谁是这个世界上最单纯的女孩'
        }
    })

</script>
```
>使用ES6中字符串新方法 
>
>**String.prototype.padStart(maxLength,fillString='')** 或 
>
>**String.prototype.padEnd(maxLength,fillString='')** 来填充字符串
```
var m = (dt.getMonth()+1).toString().padStart(2,'0')
var d = (dt.getDate()).toString().padStart(2,'0')
```

## 如何自定义一个私有的过滤器
```
// 如何自定义一个私有的过滤器
var app2 = new Vue({
    el:"#app2",
    filters:{  //定义私有过滤器
        filterName(..){

        }
    }
})
```
- 定义私有过滤器，过滤器两个条件 **【过滤器名称 和 处理函数】**
- 过滤器调用 采用 **就近原则**，如果私有过滤器和全局过滤器名称一致，这时优先调用私有过滤器

自定义一个私有的过滤器
```
var app2 = new Vue({
el:"#app2",
data:{
    dt:new Date()
}，
filters:{  
    dateFormat:function(dateStr,pattern){
        // 根据给定的时间字符串，得到特定的时间
        var dt = new Date()
        // yyyy-mm-dd
        var y = dt.getFullYear() 
        var m = dt.getMonth()+1
        var d = dt.getDate()

        if(pattern.toLowerCase() === 'yyyy-mm-dd'){
            // return y + '-' + m + '-' + d
            return `====${y}-${m}-${d}`
        }else{
            var hh = dt.getHours()
            var mm = dt.getMinutes()
            var ss = dt.getSeconds()
            return `====${y}-${m}-${d} ${hh}:${mm}：${ss}`
        }
    }
}
```