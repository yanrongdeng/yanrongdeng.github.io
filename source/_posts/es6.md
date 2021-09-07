---
title: ES6 学习记录
date: 2021-08-31 20:20:56
tags: js
---

# ES6 模块化

## 什么是 ES6 模块化

ES6出现的原因 取代 AMD CMD  common.js

AMD CMD 适用于 浏览器端 的 JavaScript 模块化
common.js 适用于 服务器端 的 JavaScript 模块化

**ES6模块化规范中定义：**
1. 每个js文件都是一个独立的模块
2. 导入其他模块成员使用 import 关键字
3. 导出共享模块成员使用 export 关键字


## 在node中体验ES6模块化

node.js 中默认仅支持 common.js 模块规范， 若想基于 node.js 体验和学习 es6 的模块化语法，可以按照下面的两个步骤：
1. node.js 版本要  >14.15.1 ( `node -v` )
2. 在 package.json ( 快速生成 `npm init -y` )文件中，添加 `"type":"module"` 节点，默认值为`commonjs`


## 默认导出和默认导入

**1、默认导出 `export default`**

**注意事项**：每个模块中，只允许唯一一次 export default ，否则会报错

**2、默认导入 `import`**

**注意事项**：默认导入时的接收名称可以任意名称，只要是合法的成员名称即可，不能以数字开头

## 按需导出和按需导入

**1、 按需导出 `exprot` 按需导出的成员**

**2、 按需导入 `import {s1} from '模块标识符'`**

**注意事项**：
1. 每个模块中可以使用多次按需导出
2. 按需导入的成员名称必须和按需导出的名称保持一致
3. 按需导入时，可以使用 `as` 关键字进行重命名
4. 按需导入可以和默认导入一起使用 `import info,{s1} from '模块标识符'`

## 直接导入并执行模块中的代码
`import '路径'`

# promise 详解

## 回调地狱

![在这里插入图片描述](https://img-blog.csdnimg.cn/95010614ad3a4e3489e1770e22ffdd08.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA54eV5a2Q6bG855qE55y85rOq,size_11,color_FFFFFF,t_70,g_se,x_16)

## promise 的基本概念

![在这里插入图片描述](https://img-blog.csdnimg.cn/8ee42d0bb1314fb7af9d9cc3d2805dd0.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA54eV5a2Q6bG855qE55y85rOq,size_15,color_FFFFFF,t_70,g_se,x_16)

## 基于回调函数按顺序读取文件内容

![在这里插入图片描述](https://img-blog.csdnimg.cn/c8419d34fc4c404cb241eca85106e5a8.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA54eV5a2Q6bG855qE55y85rOq,size_14,color_FFFFFF,t_70,g_se,x_16)可以实现功能，但是却形成了回调地狱的问题。

## 基于 then-fs 异步的读取文件内容

由于 node.js 官方提供的 fs 模块 仅支持 以回调的方式 读取文件，不支持 Promise 的调用方式。因此，需要先运行如下的命令，安装 then-fs 这个第三方包，从而支持我们基于promise的方式读取文件的内容：

安装 `npm install then-fs`

### then-fs 的基本使用

![在这里插入图片描述](https://img-blog.csdnimg.cn/ac84fcd75c1340b7a85a16ddf7a867a2.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA54eV5a2Q6bG855qE55y85rOq,size_18,color_FFFFFF,t_70,g_se,x_16)

### .then() 方法的特性

![在这里插入图片描述](https://img-blog.csdnimg.cn/1510cfd9409b4f69a991f6a075c0fc0b.png)

## 基于 Promise 异步按顺序读取文件内容

![在这里插入图片描述](https://img-blog.csdnimg.cn/aa6be6176cf24e69a40a109f43c2c1c8.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA54eV5a2Q6bG855qE55y85rOq,size_20,color_FFFFFF,t_70,g_se,x_16)

## 通过 .catch 捕获错误

![在这里插入图片描述](https://img-blog.csdnimg.cn/d681d3b635ac4326b185342706d27c61.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA54eV5a2Q6bG855qE55y85rOq,size_20,color_FFFFFF,t_70,g_se,x_16)![在这里插入图片描述](https://img-blog.csdnimg.cn/849383474a854420a18dbba12d598af5.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA54eV5a2Q6bG855qE55y85rOq,size_20,color_FFFFFF,t_70,g_se,x_16)

## promise.all() 方法

![在这里插入图片描述](https://img-blog.csdnimg.cn/80e5968b5f754d428c5e41c11a319a66.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA54eV5a2Q6bG855qE55y85rOq,size_18,color_FFFFFF,t_70,g_se,x_16)


## promise.race() 方法

![在这里插入图片描述](https://img-blog.csdnimg.cn/fd4ff541249f44a986927a6e8fef31d5.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA54eV5a2Q6bG855qE55y85rOq,size_19,color_FFFFFF,t_70,g_se,x_16)

## 基于 promise 封装读文件的方法

**1、方法名称 getFile**
**2、形参 fpath ，读取的文件路径**
**3、返回promise实例对象(形式上的异步)**![在这里插入图片描述](https://img-blog.csdnimg.cn/6340af4e4e8f48168bc4d552dbb49185.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA54eV5a2Q6bG855qE55y85rOq,size_20,color_FFFFFF,t_70,g_se,x_16)**4、获取 .then 的两个实参**![在这里插入图片描述](https://img-blog.csdnimg.cn/4101082f26eb4a989884f7773053f466.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA54eV5a2Q6bG855qE55y85rOq,size_19,color_FFFFFF,t_70,g_se,x_16)**5、调用 resolve 和 reject 回调函数**![在这里插入图片描述](https://img-blog.csdnimg.cn/e58218af37044e628a2b11805c3ecdb8.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA54eV5a2Q6bG855qE55y85rOq,size_18,color_FFFFFF,t_70,g_se,x_16)

# async/await

## 什么是 async/await

![在这里插入图片描述](https://img-blog.csdnimg.cn/56d2ab384b16423ca509e55f1c8dcb41.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA54eV5a2Q6bG855qE55y85rOq,size_20,color_FFFFFF,t_70,g_se,x_16)

## async/await 的基本用法

![在这里插入图片描述](https://img-blog.csdnimg.cn/2f2e0db4552a4efdb16735dd81ec9ca8.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA54eV5a2Q6bG855qE55y85rOq,size_17,color_FFFFFF,t_70,g_se,x_16)

## async/await 使用注意事项

1. 如果在 function 中使用了await，则function 必须被 async 修饰
2. 在 async 方法中，第一个 await 之前的代码会同步执行， await之后的代码会异步执行。

![在这里插入图片描述](https://img-blog.csdnimg.cn/d63710a3b2e54ce78b37de3515765101.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA54eV5a2Q6bG855qE55y85rOq,size_20,color_FFFFFF,t_70,g_se,x_16)


# EventLoop

## js 是单线程的语言

如果一个任务很耗时，会出现假死的问题

## 同步任务和异步任务

把 js 放在浏览器中执行，浏览器就是宿主环境 

把 js 放在 node 中执行，node 就是宿主环境

![在这里插入图片描述](https://img-blog.csdnimg.cn/108478cb5870419986db5fcc5636fcce.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA54eV5a2Q6bG855qE55y85rOq,size_20,color_FFFFFF,t_70,g_se,x_16)

## 同步任务和异步任务的执行过程

![在这里插入图片描述](https://img-blog.csdnimg.cn/ac1ec1da99554da7878b854245ba0bbb.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA54eV5a2Q6bG855qE55y85rOq,size_20,color_FFFFFF,t_70,g_se,x_16)

## EventLoop 的基本概念

![在这里插入图片描述](https://img-blog.csdnimg.cn/00b2b07288e44b638f0f914be27c4239.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA54eV5a2Q6bG855qE55y85rOq,size_20,color_FFFFFF,t_70,g_se,x_16)

## 结合 EventLoop 分析输出的顺序

![在这里插入图片描述](https://img-blog.csdnimg.cn/1bbd7c25221c46b6a0e1dffac77f143c.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA54eV5a2Q6bG855qE55y85rOq,size_20,color_FFFFFF,t_70,g_se,x_16)

# 宏任务和微任务

## 什么是宏任务和微任务

![在这里插入图片描述](https://img-blog.csdnimg.cn/75b29d4eb4364d13b8c51078f08f0799.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA54eV5a2Q6bG855qE55y85rOq,size_20,color_FFFFFF,t_70,g_se,x_16)

## 宏任务和微任务的执行顺序

![在这里插入图片描述](https://img-blog.csdnimg.cn/da093f9e4a9d4b4f89801b564911dec9.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA54eV5a2Q6bG855qE55y85rOq,size_20,color_FFFFFF,t_70,g_se,x_16)

## 去银行办业务的场景

![在这里插入图片描述](https://img-blog.csdnimg.cn/591368559d2f4f3e9e4f0b0dbfbc5813.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA54eV5a2Q6bG855qE55y85rOq,size_20,color_FFFFFF,t_70,g_se,x_16)

## 分析以下代码输出的顺序

![在这里插入图片描述](https://img-blog.csdnimg.cn/f0abeaa2ba124df49e21d386e5108168.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA54eV5a2Q6bG855qE55y85rOq,size_20,color_FFFFFF,t_70,g_se,x_16)

## 经典面试题

![在这里插入图片描述](https://img-blog.csdnimg.cn/90ee6e7b2c7b4a408172e1d778f01a9d.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA54eV5a2Q6bG855qE55y85rOq,size_20,color_FFFFFF,t_70,g_se,x_16)

# API接口案例

搭建 MySQL2 + express 的项目

## 技术

- 第三方包 express + mysql2
- ES6 模块化
- promise
- async/await

## 主要的实现步骤

- 搭建项目的基本结构
- 创建基本的服务器
- 创建 db 数据库操作模块
- 创建 user_ctrl 业务模块
- 创建 user_router 路由模块

##  项目的基本结构

- 新建文件 project，用 vsCode 打开，输入命令：`npm init -y`
- package.json 设置 ES6 模块化 `"type":"module"`
- 安装第三方包 `npm i express@4.17.1  mysql@2.2.5`

##  创建基本的服务器

创建 app.js 
通过命令 `nodemon app.js` 启用服务器

![在这里插入图片描述](https://img-blog.csdnimg.cn/52108ad6916840b49c6e49b247945d0e.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA54eV5a2Q6bG855qE55y85rOq,size_18,color_FFFFFF,t_70,g_se,x_16)

##  创建 db 数据库操作模块

创建 db/index.js 
调用 mysql 的 createPool() 方法，设置 主机 端口号 数据库名 用户 密码等
默认导出的是 promise() 的返回值，可以通过 promise 的方式操作

![在这里插入图片描述](https://img-blog.csdnimg.cn/685a2a70a415482c9e6cfba1b7c64a17.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA54eV5a2Q6bG855qE55y85rOq,size_17,color_FFFFFF,t_70,g_se,x_16)


##  创建 user_ctrl 业务模块

创建 controller/user_ctrl.js 
设置 getAllUser() 方法，用 async/await 的方式简化 promise 操作
用 send() 把请求的结果发送给客户端

![在这里插入图片描述](https://img-blog.csdnimg.cn/cb9c3f69eae54ecb92b251069524c819.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA54eV5a2Q6bG855qE55y85rOq,size_20,color_FFFFFF,t_70,g_se,x_16)


##  创建 user_router 路由模块

新建 router/user_router.js 
创建路由 `const router = new express.Router()` 
通过 get() 方法去监听 get 请求 `router.get('/user',getAllUser)`  挂载路由规则

![在这里插入图片描述](https://img-blog.csdnimg.cn/8c0e439a6f9948a5b01f2e0292ddbd5d.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA54eV5a2Q6bG855qE55y85rOq,size_18,color_FFFFFF,t_70,g_se,x_16)

##  导入并挂载路由模块

在 app.js 文件中 导入 路由模块
添加 `app.use('/api',userRouter)` 
重新启动服务器 `nodemon app.js `

![在这里插入图片描述](https://img-blog.csdnimg.cn/eefb6f2c7b72464db68dde15f3df4ed8.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA54eV5a2Q6bG855qE55y85rOq,size_20,color_FFFFFF,t_70,g_se,x_16)![在这里插入图片描述](https://img-blog.csdnimg.cn/daa078b0797742b5b68740c42791ee36.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA54eV5a2Q6bG855qE55y85rOq,size_20,color_FFFFFF,t_70,g_se,x_16)


##  使用 try...catch 捕获异常

![在这里插入图片描述](https://img-blog.csdnimg.cn/e1734938be2f4c7e8c7766d38dc8f140.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA54eV5a2Q6bG855qE55y85rOq,size_20,color_FFFFFF,t_70,g_se,x_16)

# 总结
![在这里插入图片描述](https://img-blog.csdnimg.cn/77c8ebccf6ac4b42bfbf903b86b9b129.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA54eV5a2Q6bG855qE55y85rOq,size_20,color_FFFFFF,t_70,g_se,x_16)
