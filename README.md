# vue标签
- v-model="inputValue" //获取标签内容
- v-for="(item, key, index) of list" //遍历list的item，还可用in，推荐使用of。  
- v-on:click="" == @click="" //绑定点击事件 .native 代表原生组件  
- v-bind:Receive="afferent" == :Receive="afferent" //接收传入的值
- v-on:sendOut="implement" == @sendOut="implement" //监听函数，并执行"implement"
- v-text="content" == {{content}} //模板语法，content为js表达式  
- v-html="htmlContent" //转译输出  
- v-if="" //条件，false时DOM被注释  
- v-else="" //对应上层v-if，两者必须<b>紧贴</b>使用  
- v-else-if="" //v-if拓展  
- v-show="" //false时DOM；display="none"  
- v-once //组件创建时将组建缓存，无需每次调用重新创建，提高性能  
- :key="" //vue元素识别  
- is="" //引用
# vue方法
- vm.$destroy() //销毁vm实例
# vue实例
```
var vm = new ({ //创建vue实例，接管页面某部分的DOM的渲染，根实力  
    el: '#app', //定义vue实例接管的DOM的标签  
    components: { //定义新的子组件  
        item: item  
    },  
    data: { //存放数据  
        list: [], //遍历的list，调用方式v-for="item in list"  
        inputValue: '', //数据双向绑定，v-model=""  
    }
    template: "", //html标签  
    methods: { //定义函数  
        heanleItemClick: function () {  
            // alert("click");  
        }  
    },
    computed: { //计算属性，缓存机制，相比于方法性能更高  
        fullName: function () {  
            return this.firstName + " " + this.lastName  
        }  
        get:function () {}, //输出  
        set: function (value) {}, //获取  
    },   
    watch: {}, //侦听器   
})  

Vue.prototype.bus = new Vue() //给vue组件的prototype挂载bus属性，每一个vue实例被创建时都会存在bus属性  
//定义新组件，子组件不允许修改父组件传递的内容（单向数据流）  
<item content=""> //使用方式，content="" 传入字符串，:content="" 传入js表达式  
    <p slot="name">hello</p> //插槽  
    <template slot-scope="props"> //作用域插槽，必须用 template ，必须声明从子组件接收的数据存放位置 
        <li>{{props.item}}--hello</li> //子组件显示模板信息  
    </template>  
</item>  
//全局组件  
Vue.component('item',{ //创建模块实例  
    props: [""], //接收传入的值  
Or  props: {
        content: [ Number , String] //校验传入的参数类型  
Or      content: { //校验  
            type: String, //验证传入的参数类型  
            required: true, //必须有传入值  
            default: 'default value', //默认值  
            validator: function (value) { //校验器，校验传入值大于5  
                return (value.length > 5)  
            }  
        }  
    }  
    data: function () { //子组件data只能是函数形式  
        return {  
            content: "this is content"  
        }  
    },  
    methods: {  
        handleClick: function () {  
            this.$emit("sendOut", this.index);  //子组件向外部发送信息    
        }  
    }  
    template: `<div>  //定义实例模板
                Hello world  
                <slot name="name">默认内容</slot> //插槽的使用  
               </div>`,   
})  
//局部组件  
//定义子组件  
var item = {
    item: "<div></div>"
}
```
# vue css动画
```
//显示隐藏渐变  
<style type="text/css">  
    .fade-enter, .fade-leave-to { //fade-enter开始出现时 //fade-leave-to执行消失时  
        opacity: 0;  
    }  
    .fade-enter-active, .fade-leave-active { //全称存在监控opacity变化  
        transition: opacity 3s;  
    }  
Or    
    @keyframes bounce-in {
        0% {
            transform: scale(0);
        }
        50% {
            transform: scale(1.5);
        }
        100% {
            transform: scale(1);
        }
    }
    .active{
        transform-origin: left center;
        animation: bounce-in 1s;
    }
    .leave{
        transform-origin: left center;
        animation: bounce-in 1s reverse;
    }
    //animation-direction: reverse; //动画效果反向      
</style>  
//使用方式  
<transition name="fade"> //必须使用 transition 标签嵌套  
    <div v-if="">hello world</div>  
</transition>  
Or
<transition  
    type="transition" //自定义动画时长元素  
    :duration="5000" //自定义动画时长  
Or  :duration="{enter：5000, leave :10000}"  
    name="fade"  
    appear //刷新时的动画  
    appear-active-class="active"  
    enter-active-class="active"  
    leave-active-class="leave"  
> //自定义css命名规范  
    <div v-if="show">Hello world</div>  
</transition>

```

# vue数组方法
- pop() //删除数组最后一项  
- push() //向数组增加一条数据  
- shift() //删除数据第一项  
- unshift() //向数组第一项增加一条数据  
- splice() //截取数据  
- sort() //对数组进行排序  
- reverse() //对数组取反  
- set()  
# vue生命周期
- vue生命周期图
<div align="center">
    <img src="https://github.com/KLSOBIG/Vue-Learn/blob/master/imgs/vue生命周期.png" />
</div>

- vue生命周期钩子  
> beforeCreate //初始化之前  
> created //初始化完成  
> beforeMount //实例渲染之前  
> mounted //实例渲染完成，组件被挂载时执行  
> beforeDestroy //实例销毁之前  
> destroyed //实例销毁完成  
> beforeUpdate //实例更新之前  
> updated //实例更新完成

# 命令
- 引入fastclick包 //目前已知作用，去除click 300ms延时  
```
npm install fastclick --save
```
