---
title: npm 命令参数--save，--save-dev，-g 的区别
date: 2021-09-06 20:08:08
tags:
---

**常用命令：**

`npm init -y` : 创建 package.json 这个文件

`npm run dev` : 执行 npm script 中的命令
&nbsp;
 
**一、npm install 安装模块的时候 ，一般会使用下面这几种命令形式：**
 
1. `npm install moduleName`
安装模块到项目目录下

2. `npm install moduleName -g`
&nbsp;-g 将模块安装到全局，具体安装到磁盘哪个位置，要看 `npm config prefix` 的位置
查看：`npm config ls` 
修改：`npm config set prefix`

3.  `npm install moduleName --save`
(简写：-S) 
&nbsp;-save 将模块安装到项目目录下，并在 package 文件的 dependencies 属性写入依赖

4. `npm install moduleName --save-dev` 
(简写：-D) 
&nbsp;-save-dev 将模块安装到项目目录下，并在 package 文件的 devDependencies 属性写入依赖

**二、命令的区别**
 
`npm install moduleName` 命令
1. 安装模块到项目 node_modules 目录下。
2. 不会修改 package.json 文件。
3. 运行 npm install 初始化项目时不会下载模块。


`npm install moduleName -g` 命令
1. 安装模块到全局，不会在项目 node_modules 目录中保存模块包。
2. 不会修改 package.json 文件。
3. 运行 npm install 初始化项目时不会下载模块。

`npm install moduleName --save` 命令
1. 安装模块到项目 node_modules 目录下。
2. 会在 package.json 文件的 dependencies 属性将模块依赖写入。
3. 运行 npm install 初始化项目时，会将模块下载到项目目录下。
4. 运行 npm install --production 或者注明 NODE_ENV 变量值为 production 时，会自动下载模块到 node_modules 目录中。

`npm install  moduleName --save-dev` 命令
1. 安装模块到项目 node_modules 目录下。
2. 会在 package.json 文件的 devDependencies 属性将模块依赖写入。
3. 运行 npm install 初始化项目时，会将模块下载到项目目录下。
4. 运行 npm install --production 或者注明 NODE_ENV 变量值为 production 时，不会自动下载模块到 node_modules 目录中。

**三、总结**

**使用原则**: 运行时需要用到的包使用 --save ，否则使用 --save-dev。

1. –g: 全局安装，三不原则

2. –save (-S)：将保存配置信息到 pacjage.json 的 dependencies 节点中。
运行时的依赖，发布后，即生产环境下还需要用的模块 
eg: vue、vue-router、vuex、jquery、express

3. –save-dev (-D)：将保存配置信息到 pacjage.json 的 devDependencies 节点中。
开发时的依赖，里面的模块是开发时用的，发布时用不到它。 
eg: babel、gulp、webpack、

4. devDependencies 和 dependencies 可以同时存在同一个包的依赖。