---
title: notes笔记
date : 2017-08-07 17:41:06
---

append出来的节点需要重新绑定事件 


# react native的优点：
跨平台  低投入高回报
性能高  支持动态更新

好处：
一才两用 开发成本低
代码复用率高 支持动态更新

http://www.devio.org/ 贾鹏辉的技术博客

1. 安装nodejs 
  node -v 查看版本号
  设置镜像 加速下载过程
   npm config set registry https://registry.npm.taobao.org --global      
   npm config set disturl https://npm.taobao.org/dist --global
或者
   npm install -g yarn
   安装完yarn后同理也要设置镜像源：
   yarn config set registry https://registry.npm.taobao.org --global
    yarn config set disturl https://npm.taobao.org/dist --global

2. npm install -g react-native-cli   命令行工具（用于执行创建、初始化、更新项目、运行打包服务（packager）等任务）
  react-native --help 帮助命令

3. 安装android开发工具 Androidstudio （Android sdk）  
配置环境变量 （勾选所需要的项）1).下载 Androidstudio地址（国外无法打开） http://developer.android.com/ 2).Google下载地址: //developer.android.google.cn

4. react-native init 项目名  新建一个项目

5. 安装genymotion 模拟器    delete重启出现或是F2
bios虚拟化设置

6. 手机设备连接
1）adb devices               
2） adb reverse tcp:8081 tcp:8081 

7. 安卓运行  react-native run-android
 react-native start 启动项目
ios运行 react-native run-ios
入口文件 index.android.js 

## 运行方式 ：
1. 命令运行
安装的模型器 emulator -avd 5 -gpu off
react-native run-android
首先开始 js server服务器

2. android studio 开始
包有问题
项目根目录下 npm start启动
Ctrl+M 单击两次就可以启动模拟器的菜单
加载js代码

# python
https://www.liaoxuefeng.com/wiki/001374738125095c955c1e6d8bb493182103fac9270762a000/001407375700558864523211a5049c4983176de304549c8000
![react-native生命周期](https://img-blog.csdnimg.cn/d899f5fa88024345be9a4b5c18050748.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zOTA0NzE3OQ==,size_16,color_FFFFFF,t_70)


# ES6
1. class 
2. module模块（import和export） 
3. 箭头函数 
卸载监听器是的陷阱
保存this

4. 不支持Minxin

5. 不支持自动绑定 用bind
<div this.tick.bind(this)}></div>

6. static
默认属性 
static defaultProps = {
name:"小米"
}
static propTypes= {
name:react.propTypes.string.isRequired
}

# 布局
1. flexDirection：row（横向排列）、row-reverse（反横向排列）、column（纵向排列），column-reverse（反纵向排列）
2. flexwrap 溢出是否换行 nowrap（不换行）、wrap（换行）
3. justifyContent 对齐方式
 flex-start（default） 左对齐
flex-end 右对齐
center 居中 
space-between
space-around 相邻间距相同，首和尾是中间间距的一半
4. alignItems

子视图属性
alignSelf
flex

1.重新打开页面 target="_blank" 。
2.限制输入框的长度 maxlength="11" onkeyup="this.value=this.value.replace(/\D/g,'')"  onafterpaste="this.value=this.value.replace(/\D/g,'')"
3.用avalon时加载出来之前  class="ms-controller"
<style>  
  [ms-controller]{display:none}
  .ms-controller{visibility:hidden}
 </style>
4.截取上下文 location.pathname.split("/")[1]
5. ie版本判断
//ie版本提示
var browser = navigator.appName;
var b_version = navigator.appVersion;
var version = b_version.split(";");
var trim_Version;
var msie_Version;
if (version[1]) {
trim_Version = version[1].replace(/[ ]/g, "");
} else {
trim_Version = "";
}
msie_Version = trim_Version.split('MSIE')[1];
if (browser == "Microsoft Internet Explorer" && msie_Version >= 8.0) {
window.location.href = "index";
}

if (browser != "Microsoft Internet Explorer") {
window.location.href = "index";
}
6.$.ajax(
{
type	 : "post",
url	 : '/' + path + '/restservices/http/single/query',
data	 : JSON.stringify(data),
dataType	: "json",
success	 : function(data)
{
}
});
7.onchange
8.接口文档
9.密码加密（在前端加密）
md5	 : 'http://download.yxybb.com/test/lib/md5'
md5.hex_md5('123')

10.stateless = true 不需要鉴权
不写默认是false 需要鉴权（authorize=true）

11.把结果集累加到数组里面
var arr = [];
arr = arr.concat(result);
vm.newslist = arr;

12.安装webstorm需要安装的文件
----------------简介----------------
CMD/AMD规范简介

nodejs（搭建测试服务器）

express框架(路由)

json/jsonp请求

requirejs（前端模块儿化框架）

fis3（前端工程构建工具）
----------安装开发工具-----------------
		
--WebStorm
		
--node
		
--express
		
[npm install -g express express-generator]
		
--fis3
		
[npm install -g fis3 fis3-hook-amd fis3-postpackager-loader]


13.webstrom新建项目
输入命令express -e  文件名（test）
命令---生成node_modules ： npm install


14.新建项目
 复制完了之后 服务端可以什么都不要  客户端需要 .leap .project修改项目名字name  保留web-INF中lib和resourcelib、leap.xml 、License.lic、web.xml，修改leap.xml 

15.在js中加css样式的方式：
               $("#comment_content").css({border:'1px solid #FF0000'});
                document.getElementById( "ueditor_0" ).style.border = "1px solid #FF0000";
		$(".page02_main").css({"padding-bottom":"200px"});
		$(".page02_main").css("padding-bottom","200px");