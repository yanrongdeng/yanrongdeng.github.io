---
title: webpack4快速入门指南
date: 2021-03-28 17:20:46
tags: webpack
categories: 学习笔记
---

>说明：此文档仅供自己记录学习的过程，由于webpack等版本更新，所以不兼容

# 安装webpack

1. **全局安装webpack：**  `npm install webpack webpack-cli  webpack-dev-server -g`
2. **新增项目目录：**  `mkdir  project`
3. **进入project文件：**  `cd  project`
4. **新建三个项目结构：** `mkdir dist src config`
5. **初始化本地仓库，生成  .git  文件夹：**  `git init .`
6. **生成依赖文件  packgae.json ：**  `npm init -y`
7. **生成 index.html 和 index.js 文件：**  `touch src/index.js dist/index.html`
8. **打开 vscode 代码工具：**  `code .`
9. **入口文件：**  `webpack.dev.js`
    >webpack4版本出现的方式：默认生成
    >>webpack --mode=development（本地环境）
    >>webpack --mode=production （生产环境）
    
10. **配置 webpack.dev.js 文件：**  `entry(入口)   mode(打包环境)    output(出口)`
11. **打包命令：**      `webpack --config=config/webpack.dev.js`
12. **配置公开路径：**  `publicPath`
13. **项目中安装本地服务器：**  `npm install webpack@4.3.0 webpack-cli@2.0.13 webpack-dev-server@3.1.1`
14. **启动本地服务器：**  `webpack-dev-server --config=config/webpack.dev.js`
	>如果报如下错误：
	![在这里插入图片描述](https://img-blog.csdnimg.cn/20210328110245292.png)
	解决方式：
		1). 卸载webpack-dev-server:	`npm uninstall webpack-dev-server`
		2). 重新安装低版本：`npm install webpack-dev-server@3.1.1`
		如果还没有解决，就删除node_modules文件夹，重新安装依赖：`npm install`	
		还是没有解决，就是webpack webpack-cli  web-dev-server版本不匹配、按我给的版本重新安装
		
15. **配置本地服务器：**  `devServer `

# 引入css

16. **新建 main.css 文件:**    `touch src/main.css`
17. **加载 css 文件，安装加载器（版本不对，服务启动不起来）：**  `npm install style-loader@0.20.3 css-loader@0.28.11`
18. **配置 css 加载器：** `module:{   rules: [  {test:/\.css$/,  use:[   {loader: style-loader },{loader:css-loader}]}]}` 
19. **只要改变了webpack.dev.js，就得重新启动服务：**  `webpack-dev-server --config=config/webpack.dev.js`
20. **修改服务启动项(package.json的scripts)：**   `	start(启动)   
	build(打包)`
	```js
	  "scripts": {
    	"start": "webpack-dev-server --config=config/webpack.dev.js",
    	"build": "webpack --config=config/webpack.dev.js"
 	 }
	```

# 引入html

21. **把 dist 中的 index.html 移动到src下面、并删除 main-bundle.js：**  
22. **加载 html 文件，安装加载器：**  `npm install html-loader@0.5.5 extract-loader@2.0.1 file-loader@1.1.11`
23. **配置 html 加载器：**   `rules:[ {  test:/\.html$/,  use:[  {  loader:"file-loader", options:{ name:"[name].html"  } }, {loader:"extract-loader" }, { loader:"html-loader"} ] } ]`   不加载到js中，单独存在
24. **启动服务器：**  `npm start`
25. **修改main.css文件、设置样式：**
	 ```css
	  h1{
		   height: 100vh;
		   display: flex;
		   align-items: center;
		   justify-content: center;
		   color: white;
		   text-shadow: 0 0 20px white;
		   font-size: 5rem;
		   font-family: sans-serif;
	  }
	```
    
# 引入图片

26. **新建 images 文件夹：**  `mkdir src/images`
27. **配置 img 加载器：**   `rules:[{  test:/\.(jpg|gif|jpeg|png)$/,  use:[  {  loader:"file-loader", options:{ name:"images/[name].[ext]"  } } ]} ]`
28. **在 index.html 中引入图片：** 
29. **修改 main.css 文件，设置图片样式**
	```css
	body{
	    margin: 0;
	    background: #444444;
	}
	.profile{
	    height: 100vh;
	    display: flex;
	    align-items: center;
	    justify-content: center;
	    flex-direction: column;
	}
	img{
	    border-radius: 100%;
	    width: 500px;
	    height: 500px;
	    object-position: 50% -20px;
	}
	h1{
	    color: white;
	    text-shadow: 0 0 20px white;
	    font-size: 5rem;
	    font-family: sans-serif;
	}
	```

# babel转换器的使用
es6—>es5

30. **安装 Babel：**  `npm install babel-core@6.26.0`
31. **新增 .babelrc 文件：**  `touch .babelrc`
32. **安装插件：** `npm install babel-plugin-transform-es2015-arrow-functions@6.22.0`
33. **配置 .babelrc 文件**
	```js
	{
		"plugins":[
	  		"transform-es2015-arrow-functions"
	  ]
	}
	```
34. **全局安装 babel-cli：**   `npm install babel-cli -g`
35. **安装加载器 babel-loader :** `npm install babel-loader@7.1.4`
36. **配置 babel-loader 加载器：** `rules: [  {test:'/\.js$/',  use:[   {loader: babel-loader }]}]` 
37. **打包：**  `npm run build`
38. **启动服务器：**  `npm start`

 # webpack.dev.js完整代码如下：
    
   ```js
const path = require("path");
const { resolveTxt } = require("dns");
module.exports={
		//entry 入口，可以有多个           
		entry:{ 
		     main:["./src/main.js"]
		 },
		 //mode 打包环境  开发(development) & 生成(production)    
		 mode : "development" ,
		 //output 出口，有且只有一个        
		 output :{
		     filename:"[name]-bundle.js",
		     path:path.resolve(__dirname,"../dist"),
		     //公开路径
		     publicPath:"/",
		 },
		//本地服务器
		devServer:{
		    contentBase:"dist",
		    //浏览器中也显示错误信息
		    overlay:true 
		},
		module:{
		    rules:[
		        {
		            //js  loaders
		            test:/\.js$/,
		            use:[
		                {
		                    loader:"babel-loader"
		                }
		            ]
		        },
		        {
		            //css  loaders
		            test:/\.css$/,
		            use:[
		                {
		                    loader:"style-loader"
		                },
		                {
		                    loader:"css-loader"
		                }
		            ]
		        },
		        {
		            //html loaders
		            test:/\.html$/,
		            use:[
		                {
		                    loader:"file-loader",
		                    options:{
		                        name:"[name].html" //输出的文件名
		                    }
		                },
		                {
		                    loader:"extract-loader"  //不会加载到js中，单独存在
		                },
		                {
		                    loader:"html-loader"
		                }
		            ]
		        },
		        {
		            // img  loaders
		            test:/\.(jpg|gif|jpeg|png)$/,
		            use:[
		                {
		                    loader:"file-loader",
		                    options:{
		                        name:"images/[name].[ext]"
                        	}
                    	}
               	]
              }
          ]
      }
}
 ```