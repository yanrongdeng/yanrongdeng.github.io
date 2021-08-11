---
title: jquery归纳总结
date: 2017-04-08 09:33:34
tags: jQuery
categories: 学习笔记
---
​
1 网页中引入jquery
从jquery.com 下载jquery库
从页面上面引用 <script src='jquery.js'></script>
2 就绪函数
$(document).ready(function(){    })
简写:$(function(){  }) 

3 操作类名
addClass("类名")         //给元素增加类名 
removeClass("类名")     //删除元素类名 
toggleClass（"类名"）  //添加或删除一个或多个类（切换）

4 设置内容
html()            //无参数 读---获取元素的里的内容   
html("内容")     //有参数 写---设置元素的内容
text( )         //文本操作
val()          //无参—获取值 
val("内容")   //有参—设置值

5 绑定事件
on("click",fn1)   //绑定事件    
off("click", fn1)   //解除绑定 

6 改变样式
css("属性名","值")  // css({“属性1” : ”值1” , ”属性2” : ”值2”})
font-size           //  fontSize  
7 元素显示和隐藏
show()        //显示   
hide()        //隐藏   
toggle()      //显示/隐藏切换
8 元素淡入淡出
fadeIn()          //淡入  
fadeout()        //淡出  
fadeToggle()    //切换
9 滑动展开/卷起
slideUp()      //卷起    
slideDown()    //展开    
slideToggle()  //切换 
10 动画
animate({ 属性1:值1, 属性2,值2}, 时间, 类型, 回调函数 )      
     //属性1: [“值1”, “linear”]  
     //属性2: [“值2”, “easeInOutExpo”]
11 设置/删除属性
attr("属性名")          //读--获取元素属性值;
attr("属性名","值")    //写--设置元素属性值;
removeAttr()          //移除属性
12 获取兄弟的方法
prev()          //上一个兄弟元素
next()          //下一个
siblings( )     //所有的兄弟元素
first()         //第一个节点
last()          //最后一个节点
eq(n)           //第n个节点
13 DOM对象与jquery对象相互转换
js对象转jq对象 增加$() document–$(document)
jq对象转js对象 增加[0] $(“#box”)[0]

14 ajax请求
$.ajax({  
    type:”GET”,   // 请求类型 GET  POST  
    url:”data/product.json”   // 请求的url资源  
    dataType:”json”  // 期望返回数据类型, 默认自动判断  
    success: function( data){ }  //回调函数,处理服务器的请求内容
           // function(data,status,xhr){}  
                                // data  返回的数据,
                                //status  描述状态字符串
                                // xhr – 原始的XMLHttpRequest对象  
    error:function(xhr,status,exception){ }  // 请求失败的回调函数  
    catch:true //默认true , 是否缓存数据;
}) 
简写 :
(1)  $.getJSON( url,dataObj,function(data) { 回调函数 })
(2)  $.get(url,  dataObj , callback )
(3)  $.post(url,  dataObj, callback ) //参数设置$.ajaxSetup({dataType:”json”}) 
(4)  load()   $(“#result”).load(url)  //将url请求的内容插入目标盒 
15 字符串和对象的转换
JSON.stringify (json对象)  //转换对象为字符串 
JSON.parse(字符串)        //字符串转成对象
16 find(）
$("父元素").find("后辈元素")   //父元素中查找后辈元素
17 stop()//停止当前正在运行的所有动画
18 remove()
$("要被删除的元素").remove()    //删除指定元素
19 blur()
on("blur",fn )   //失去焦点事件
20 empty()
$("#res").empty()   //清空元素的内容
21 change()//当表单控件值变化时
22 prop() //获取属性值
23 slideUp( 时间, 类型, 回调函数 )
动画类型: swing 平滑(默认) | linear 匀速 easeOutElastic 弹性easeInBounce 反弹

24 width()//获取元素的宽高
25 height() //获取元素的高
26 each()
$("元素组").each(function(index,element){ 代码 })  
27 stop()//立刻停止之前的所有动画
28 finish() //立刻完成之前的所有动画
29 hover()
hover(function(){ 鼠标移入效果 } , function(){ 鼠标移出效果 })   //鼠标移入移除函数 
30 $.trim()
var newStr=$.trim(oldStr) //去除字符串两端的空格
31 追加
append(son)         //后追加
prepend(son)        //前追加
son.appendTo()      //追加到
before(son)         //在”我”前面追加
after(son)          //在”我”后面追加
son.insertBefore()  //追加到…前面
son.insertAfter()   //追加到…后面
32 index()
$("子元素").index() //获取一组元素中某个元素的索引值 
33 e.preventDefault()//阻止默认事件
34 e.stopPropagation() //阻止事件冒泡
35 scrollTop
$("窗口").scrollTop( h ) //窗口向上滚动指定的距离h
$(document).scrollT()  //浏览器窗口滚动的距离
36 $(“窗口”).prop(“scrollHeight”) //获取窗口滚动内容高度
37 $.map()
var newArr=$.map(oldArr,function(val){  代码  }) //将数组中的元素逐个处理形成一个新数组  
38 $(“按钮”).trigger(“click”) //代码模拟事件点击
39 parents()
$("子元素").parents("选择器")  //查找指定的父辈元素;
40 is()
$("A").is( $("B") )//判断两个元素是否为同一元素;
41 e.type //获取事件类型
42 scroll//窗体滚动事件
43 鼠标事件
mouseover mouout //进入或离开被选中元素或子元素; 鼠标悬停事件
mouseenter mouselve //进入或离开被选中元素;

44 事件委托
给li绑定的事件,对于静态li生效
为了对于动态li也生效, 使用事件委托
把事件监听委托给li的父级ul

$("ul").on("click","li",function(){ 代码 })
45 keyup
//键盘按键弹起事件
e.keyCode //获取键码

46 headers: {“apikey”:”XXX”} //头文件信息设置
47 相对绝对定位
var p=$("元素").position() 
p.left  p.p   //绝对坐标 
Var q=$("元素").offset()
q.left   qop  //相对于浏览器偏移 
48 $.isArray( ) //判断变量是否是数组
49 $.type() //获取对象类型
50 $.isEmptyObject()//判断变量是否是空对象
51 $.parseJSON() //将json字符串转换为js对象
52 $.each()
//遍历js对象集合
$.each(obj,function(prop,val){ 代码})
//prop 属性名  
//val – 属性值
选择器
1 基本选择器

选择器	中文名称	举例
*	所有选择器	$(“*”).
id	ID选择器	$(“#id”)
class	类选择器	$(“.class”)
element	元素选择器	$(“p”)
逗号隔开	组合选择器	$(“#id，.class”)
2 层级选择器

选择器	中文名称	举例
>	子集选择器	$(“#box>p”) #box盒内儿子辈的p
+	相邻选择器	$(“p.pc +p”) 紧邻的下一个p元素
~	兄弟选择器	$(“p.pc ~p”) 后面所有的兄弟p元素
3 位置选择器

选择器	中文名称
:first	第一个元素
:last	最后一个元素
:eq(n)	第n个元素
:gt(n)	大于n的元素
:lt(n)	小于n的元素
:even	偶数元素（下标为0开始）
:odd	奇数元素（下标为0开始）
:header	标题元素 h1 h2…
li:first-child	每个ul里的第一个li
li:last-child	每个ul里的最后一个
li:nth-child(n)	每个ul中第第n个元素;
li:nth-child(even)	even 偶数 odd 奇数
li:nth-child(3n+1)	n=0 1 2
li:only-child	只有一个子集
4 内容选择器

选择器	中文名称
:contains(“text”)	包含文本
:has(“选择器”)	至少包含
:empty	空元素
:parent	有文本子节点
5 表单对象筛选

选择器	中文名称
:enabled	可点
:disabled	不可点
:checked	选择
:selected	
6 可见性筛选

选择器	中文名称
:visible	显示元素
:hidden	隐藏元素
7 属性选择器

选择器	中文名称
$(“a[href]”)	包含href属性的所有a标签;
$(“a[href=’#’]”)	空链接;
$(“a[href^=’http’]”)	链接以“http”开始
$(“a[href$=’.html’]”)	链接以“.html”结束
$(“a[title*=’data’]”)	内容中包含”data”;
$(“a[title~=’data’]”)	内容中包含”data’”单词
$('a[href!="#"]')	href值不是”#’或者没有href属性或者
下次整理：
:read-only
:read-write
:before
:after
:root
:not 除*之外
:nth-last-child(n) 倒数第n行
:first-of-type 父元素中的某个类型的第一个
:last-of-type
:nth-of-type
:only-of-type 只有一个元素
$.data(ele,key,value)

​