---
title: Vue的学习笔记
date: 2021-06-25 20:08:57
tags: Vue
categories: 学习笔记
---
## Vue基本指令

`v-cloak` 能够解决插值表达式闪烁的问题
style中设置` [v-cloak]{display：none;}`
`v-text` 文本
`v-html `解析标签
`v-bind: ` 是vue中，绑定属性的指令
`v-on /@click`   绑定事件的指令
`@click.stop `  阻止事件冒泡
`@click.prevent ` 阻止默认事件
`@click.capture` 实现捕获事件处理机制
`@click.self ` 只有点击当前元素，才会触发事件
`@click.prevent.once`  默认事件只触发一次 

### Stop和self的区别？
* stop 阻止冒泡，也就是不触发父级的事件
* self 只有点击自身的时候，才会触发事件
	
`:class` 的使用 
* 直接传一个数组 (类名) `:class="['red','thin']"`
*  数组中使用三元表达式  `:class="['red',active?'thin':'']"`
* 在数组中使用 对象来代替三元表达式  `:class="['red',{'thin':true}]"`
* 在为class使用v-bind绑定 对象 的时候，对象的属性是类名 `:class="{'red':false,'thin':true}"`

`:style` 的使用 :   一个就直接写，多个就是数组形式
`v-model`  双向绑定
`v-for` 循环展示 i    普通数组、对象数组、对象、迭代数字
```javascript
   v-for = "count in 10"
```
* 注意：
	>key属性只能使用number获取string
    >Key在使用的时候，必须用v-bind属性绑定的形式，指定key的值
  
### v-if和v-show 的区别？
* 都有隐藏和显示dom元素的功能
* v-show 类似于display:none的用法，只会预编译一次
* v-if  不停的创建和销毁dom元素，很消耗性能

`Vue.filter`  全局定义过滤器
`Vue.directive`  全局定义指令
>钩子函数：bind    inserted  update
>一般情况下，通常把bind和update写在一起

`filters`  定义私有过滤器
`directives`  定义私有指令
## Vue的生命周期
```js
	//创建前后、载入前后、更新前后、销毁前后
	beforeCreate(){},	//data 未初始化
	created(){},  		//data初始化好了
	beforeMount(){},	//页面未渲染
	mounted(){}, 		//页面渲染好了
	beforeUpdate(){},	//data数据更新了，但页面未改变
	updated(){},		//页面上已修改
	beforeDestroy(){},
	destroyed(){},
```

## Vue的异步调用请求
引入 `vue-resource.js` 文件
Get、post、jsonp
```js
 // 发起get请求
 this.$http.get('http://www.phonegap100.com/appapi.php?a=getPortalList&catid=20&page=1').then(function (result) {  console.log(result.body) // 通过 result.body 拿到服务器返回的成功的数据
 })
 //  通过 post 方法的第三个参数， { emulateJSON: true } 设置 提交的内容类型 为 普通表单数据格式
 this.$http.post('http://www.phonegap100.com/appapi.php?a=getPortalList&catid=20&page=1', {}, { emulateJSON: true }).then(result => { console.log(result.body) })
// 发起JSONP 请求
 this.$http.jsonp('http://www.phonegap100.com/appapi.php?a=getPortalList&catid=20&page=1').then(result => { console.log(result.body) })
```
## Vue的动画transition
```html
<style>
   .v-enter,.v-leave-to{
       opacity: 0;
       transform: translateX(150px);
   }
   .v-enter-active,.v-leave-active{
       transition: all 0.8s ease;
   }
</style>
<transition>
     <h3 v-if="flag">这是一个H3</h3>
</transition>
```
## vue组件的定义方式
1. extend 或是 省略extend，直接用一个对象:   `Vue.compontent("login",Vue.extend({template:"<h1>这是个h1标签</h1>"})) `
2. template 放在HTML中，加一个id:    `Vue.component("mycom4",{template:"#com4"})`
3. 字面量形式:   `var helloLogin = { template:"<h3>这是一个h3标签，字面量形式</h3>"}`

### 组件的data和methods 的使用
data  必须是  一个  函数，且返回的是  一个  对象
### 组件切换  
1. 使用`v-if  v-else`，来切换
2. `component `组件的  `:is`  属性，指定组件的名称
### 组件切换动画
在transition标签上加  `mode = " out-in "`,定义为先出后进


## vue父--子组件的通信
`props`  		父----->子
`this.$emit()`   子---->父
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210414104020156.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zOTA0NzE3OQ==,size_16,color_FFFFFF,t_70)
`ref`  获取dom元素 和  组件
this.$refs.name

## vue路由创建方式
```html
<!-- 切换路由 -->
<router-link to="/login?id=10&name=dyr">登录</router-link>
<router-link to="/register/20/ywb">注册</router-link>
<!--展示路由组件 -->
<router-view></router-view>
```
```js
var routerObj = new VueRouter({
	routes:[
		{path:'/',redirect:'/login'}, //重定向
		{path:'/login',component:login}
		{path:'/register/:id/:name',component:register}
	]
})
let vm = new Vue({
     el:"#app",
     router:routerObj
})
```
### 传参方式 
```js
/login?id=10&name=dyr      		this.$route.query.id
/register/20/ywb  /:id/:name    this.$route.params.id
```
### 嵌套  
```js
children:[
	{ path:'/login',component:login }
]
```
### 命名视图实现经典布局
```js
//指定name
components:{
     default:header,
     left:leftBox,
     main:mainBox
 }
```
## watch监听属性 和 computed 计算属性
```js
  watch:{
    'firstname':function(){
       this.funllname = this.firstname + '-' + this.lastname;
    }
  },
  computed:{
   'firstname':function(){
       this.funllname = this.firstname + '-' + this.lastname;
    }
  }
```


## 新建vue项目
1、全局安装vue-cli：`npm install --global vue-cli`
2、新建项目：`vue init webpack my-project`
3、进入项目目录：`cd my-project`
4、运行项目：`npm run dev`

#### 用vue实现一个表的增删改查

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>vue实现表的增删改查</title>
    <script src="./vue.js"></script>
    <style>
        body{margin: 0;padding: 0;}
        .flex{ width: 100%;height: 100%;margin: 0 auto;}
        .header{height: 100px;background-color: aqua;text-align: center;margin: 0 auto;}
        .Lheader{padding: 30px 0;}
        .Lheader span{color:cornflowerblue;padding-right: 5px;}
        .Lheader input{ padding: 5px 10px;border-radius: 5px;margin-right: 40px;}
        .content{background-color: bisque;height: 800px;padding-top: 20px;text-align: center;}
        input[type='button']{    cursor: pointer;}
        ul{margin: 0;}
        ul li{border: 1px solid red;list-style: none;width: 100%;}
        ul li:hover{
            transition: all 0.6s ease;
            background-color: rgb(144, 223, 247);
        }
        [v-cloak]{
            display: none;
        }
        ul li p {display:inline-block;padding: 5px 20px;width: 200px;}
        p input{ background-color:orange;color:white;padding: 5px 10px;border-radius: 5px; border:orange;}
        p input:visited, p input:focus, p input:active{border:orange;outline: 0;}
        .v-enter,.v-leave-to{
            opacity: 0;
            transform: translateY(80px);
        }
        .v-enter-active,.v-leave-active{
            transition: all 0.6s ease;
        }
        .v-move{
            transition: all 0.6s ease;
        }
        .v-leave-active{
            position:absolute;
        }
    </style>
</head>
<body>
    <div class="flex" id="app">
        <div class="header">
            <div class="Lheader">
                <span>id: </span> <input type="text" oninput="value=value.replace(/[^\d]/g,'')" name="idcard" id="id" v-model="id"> 
                <span>name: </span> <input type="text" name="name" id="name" v-model="name">
                <input type="button" value="添加" @click="add">
                <span>搜索：</span> 
                <input type="search" name="search" id="search" v-model="keywords" v-focus v-color="{ color: 'green', backgroundColor: 'aqua' }"> 
            </div>
        </div>
        <div class="content">
            <transition>
                <ul>
                <li>
                    <p>id</p>
                    <p>name</p>
                    <p>creattime</p>
                    <p>opration</p>
                </li>
                </ul>
        </transition>
            <transition-group appear tag="ul" v-cloak>
                <li v-for="(item,index) in oklist" :key="item.id">
                    <p>{{item.id}}</p>
                    <p>{{item.name}}</p>
                    <p>{{item.creattime | subTime }}</p>
                    <p class="delete"><input type="button" value="修改" @click="update(item.id,index)"> <input type="button" value="删除" @click="deleted(index)"></p>
                </li>
            </transition-group>
        </div>
    </div>
</body>
</html>
<script>
    Number.prototype.padStart = function(...arr){
        return  String.prototype.padStart.call(this,...arr);
    }
    //Vue.filter 全局自定义过滤器
    Vue.filter("subTime",function(str,pre=''){
        if(!str){return '';}
        const time = new Date(str);
        const year = time.getFullYear();
        let month = time.getMonth() + 1;
        let day = time.getDate();
        let hour = time.getHours();
        let min = time.getMinutes();
        let sec  = time.getSeconds();
        if(pre&&pre==='yyyy-mm-dd'){
            return `${year}-${month.padStart(2,'0')}-${day.padStart(2,'0')}`;
        }else{
             return `${year}-${month.padStart(2,'0')}-${day.padStart(2,'0')} ${hour.padStart(2,'0')}:${min.padStart(2,'0')}:${sec.padStart(2,'0')}`;
        }
    })
    //Vue.directive 全局自定义指令 `v-focus`
    //第一个参数是指令的名称 不需要v-
    // 第二个参数是一个对象，有一些函数，可以执行相关的操作
    Vue.directive('focus', {
        bind: function(el,binding,vnode){
        },
        // 当被绑定的元素插入到 DOM 中时……
        inserted: function (el) {
            el.focus()
        },
        update:function(el){
            // console.log(el.value)
        }
    })
    //在bind和update触发相同行为，函数简写如下
    Vue.directive('color',function(el,binding){
        //对象字面量的形式
        el.style.color = binding.value.color;
        el.style.backgroundColor = binding.value.backgroundColor;
    })
    let vue = new Vue({
        el:"#app",
        data:{
            id:"",
            name:"",
            keywords:"",
            list:[
                {id:'1',name:"马云",creattime:'2021-3-19 15:28:26'},
                {id:'2',name:"张三",creattime:'2021-3-19 17:28:29'},
                {id:'3',name:"李四",creattime:'2021-3-19 13:20:35'}
            ]
        },
        methods:{
            add:function(){
                if(this.id){
                    this.id = this.id;
                }else{
                    this.id = Math.random().toString(36).substring(2,10);
                }
                if(!this.name){
                    this.name = Math.random().toString(8).substring(2,6)
                }
                const arr = this.list.findIndex((v)=>v.id===this.id);
                if(arr===-1){
                    this.list.push({id:this.id ,name:this.name,creattime:new Date()});
                    this.name = this.id = "";
                }else{
                    alert(`新增失败！id=${this.id}已存在`);
                }
                
            },
            deleted:function(i){
                this.list.splice(i,1);
            },
           search:function(keywords){
            //    数组的新方法   indexOf  forEach  filter  find  findIndex  
                if(keywords){
                    let newList = this.list.filter((item)=>item.name.includes(keywords)); //filter的用法  表达式为true   就返回当前项
                    return newList;
                }else{
                    return this.list;
                }
           },
           update:function(id,index){}
        },
        computed:{
            oklist :function(){
                if(this.keywords){
                    let newList = this.list.filter((item)=>item.name.includes(this.keywords)); //filter的用法  表达式为true   就返回当前项
                    return newList;
                }else{
                    return this.list;
                }
            }
        },
        //定义私有过滤器
        filters:{
            subTime2:function(str,pre=""){}    
        },
        directives:{
             'fontweight':{
                bind:function(el,binding){
                    el.style.fontWeight = binding.value;
                }
             }
        }

    })
</script>
```
