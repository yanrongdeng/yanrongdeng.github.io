---
title: vue基本知识掌握
date: 2021-04-25 20:08:57
tags: Vue
categories: 学习笔记
---

# vue学习
![在这里插入图片描述](https://img-blog.csdnimg.cn/7dcb802800b9404591f2e9383f1f8fc1.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA54eV5a2Q6bG855qE55y85rOq,size_20,color_FFFFFF,t_70,g_se,x_16)
![在这里插入图片描述](https://img-blog.csdnimg.cn/963c243fb533449e8a4f136072600c49.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA54eV5a2Q6bG855qE55y85rOq,size_18,color_FFFFFF,t_70,g_se,x_16)
![在这里插入图片描述](https://img-blog.csdnimg.cn/d404affbfd2847409834fc4bbeb27d12.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA54eV5a2Q6bG855qE55y85rOq,size_20,color_FFFFFF,t_70,g_se,x_16)
![在这里插入图片描述](https://img-blog.csdnimg.cn/f4953b8f695c4cc2b7b2f647ca70b5b1.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA54eV5a2Q6bG855qE55y85rOq,size_18,color_FFFFFF,t_70,g_se,x_16)
![在这里插入图片描述](https://img-blog.csdnimg.cn/1aa8f7405315411198676bdf2f687a8a.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA54eV5a2Q6bG855qE55y85rOq,size_19,color_FFFFFF,t_70,g_se,x_16)
![在这里插入图片描述](https://img-blog.csdnimg.cn/37aaf20db44c4b9fa13c76cbeadf09d9.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA54eV5a2Q6bG855qE55y85rOq,size_20,color_FFFFFF,t_70,g_se,x_16)
![在这里插入图片描述](https://img-blog.csdnimg.cn/2940328820e44388acb65f709a50a0d3.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA54eV5a2Q6bG855qE55y85rOq,size_18,color_FFFFFF,t_70,g_se,x_16)
![在这里插入图片描述](https://img-blog.csdnimg.cn/c8b44a43e89f41a4bce67a020447b721.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA54eV5a2Q6bG855qE55y85rOq,size_18,color_FFFFFF,t_70,g_se,x_16)
# vue2.0 结构图
![学习vue2.0](https://img-blog.csdnimg.cn/f07e6473a74248c89a80e8cfd3e7949f.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zOTA0NzE3OQ==,size_16,color_FFFFFF,t_70)

## 2.x 数据劫持
vue 实现响应式 基于 Object.defineProperty() 的 get set  数据劫持
defineReactive()  //提供一个闭包环境，避免环境污染
```js
let obj = {
    a:1
}
function defineRactive(obj,key,val){
    Object.definePorperty(obj,key,{
        get(){
            return val;
        }
        set(newVal){
            val = newVal;
        }
    })
}
defineRactive(obj,"a",10)
console.log(obj.a)

Observe类 本质 核心功能：  正常 obj -- 属性 加工 响应式 obj
observe(obj) 由此触发，所有的开始 ——>  判断obj身上是否有__ob__   ——>   new Observe() 
 
//__ob__ 唯一的标识  存在不需要再次劫持
// 设置 __ob__ 不能被枚举
```

## vue 基本指令

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
`Vue.set(obj, obj.length, value);`  对数组或对象赋值
### Stop 和 self 的区别？
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
  
### v-if 和 v-show 的区别？
* 都有隐藏和显示dom元素的功能
* v-show 类似于display:none的用法，只会预编译一次
* v-if  不停的创建和销毁dom元素，很消耗性能

`Vue.filter`  全局定义过滤器
`Vue.directive`  全局定义指令
>钩子函数：bind    inserted  update
>一般情况下，通常把bind和update写在一起

`filters`  定义私有过滤器
`directives`  定义私有指令
## vue 的生命周期
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

## vue-resource 异步调用请求 
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
## transition 动画
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
<html>
<body>
<transition>
     <h3 v-if="flag">这是一个H3</h3>
</transition>
</body>
</html>
```
## vue 组件的定义方式
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


## vue组件的通信
### props
`props`  		父----->子
### $emit 
`this.$emit()`   子---->父
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210414104020156.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zOTA0NzE3OQ==,size_16,color_FFFFFF,t_70)
### ref
`ref`  获取dom元素 和  组件
this.$refs.name

## vue-router 路由创建方式
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
## watch 监听属性
```js
  watch:{
    'firstname':function(){
       this.funllname = this.firstname + '-' + this.lastname;
    }
  }
```
##  computed 计算属性
```js
  computed:{
   'firstname':function(){
       return this.funllname = this.firstname + '-' + this.lastname;
    }
  }
```
## nvm(node version manager) node 版本控制工具
![nvm](https://img-blog.csdnimg.cn/c3cf82afcf734e5f95430f7c4542fd20.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zOTA0NzE3OQ==,size_16,color_FFFFFF,t_70)

## vue-devtools 调试工具
参考链接: [vue调试工具vue-devtools安装及使用](https://www.cnblogs.com/yuqing6/p/7440549.html)

1. 下载：`git clone https://github.com/vuejs/vue-devtools`
2. 在 vue-devtools 目录下安装依赖包
`cd vue-devtools`
`npm install`
3. 修改 manifest.json 文件里的 "persistent":false 改成 true
![在这里插入图片描述](https://img-blog.csdnimg.cn/70ef62cec75a47c1b27ae57f6b89c3e5.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zOTA0NzE3OQ==,size_16,color_FFFFFF,t_70)
4. 编译代码： `npm run build`
>命令行安装npm淘宝镜像：
$ `npm install -g cnpm --registry=https://registry.npm.taobao.org`
安装之后就可以用cnpm代替npm安装依赖包
`cnpm install `
`cnpm run build`
5. 打开 chrome 的扩展程序，开发者模式，加载已经解压的扩展程序，放入 shell > chrome
Chrome浏览器 >  更多程序 > 拓展程序 
点击加载已解压程序按钮, 选择 vue-devtools > shells > chrome 放入, 安装成功如下图
![在这里插入图片描述](https://img-blog.csdnimg.cn/b578449e5aad491c88641acc52c0cb93.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zOTA0NzE3OQ==,size_16,color_FFFFFF,t_70)

6. vue-devtools 使用
vue 项目, 打开 f12 , 选择 vue 就可以使用了.
vue 是数据驱动的, 这样就能看到对应数据了, 方便我们进行调试
>**温情提示**: 
>> 1.vue 必须引入开发版, 使用 min 压缩版是不能使用 devtools 进行调试的
>> 2.安装后, 需要关闭浏览器, 再重新打开, 才能使用

## ESLint 写代码的规则，使代码更优美
## vuex 状态控制
## 新建vue项目
1、全局安装vue-cli：`npm install --global vue-cli`
2、新建项目：`vue init webpack my-project`
3、进入项目目录：`cd my-project`
4、安装依赖：`npm install`
5、启动服务：`npm run dev`

方式一：
vue create hello-world
cd hello-world
npm run serve

方式二：vue ui
### 用vue实现一个表的增删改查

```html
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
