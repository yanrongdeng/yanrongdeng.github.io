---
title: process.env.NODE_ENV详解
date: 2021-08-09 14:43:21
tags:
---


# 一、 process.env.NODE_ENV是什么？
在node中，有全局变量process表示的是当前的node进程。
process.env包含着关于系统环境的信息，但是process.env中并不存在NODE_ENV这个东西。

## process.env.NODE_ENV的作用
- NODE_ENV这个变量不是process.env本来就有的，是通过设置得到的。
- 在webpack中它的用途是判断生产环境或开发环境。

为了查看 process的基本信息，我们可以在文件夹中 新建一个process.js文件，在里面加一句代码console.log(process);  然后进入该文件夹，执行node process.js可以在命令行中打印如下信息：

``` bash
$ node process.js
process {
  title: 'node',
  version: 'v4.4.4',
  moduleLoadList: 
   [....],
  versions: 
   { http_parser: '2.5.2',
     node: '4.4.4',
     v8: '4.5.103.35',
     uv: '1.8.0',
     zlib: '1.2.8',
     ares: '1.10.1-DEV',
     icu: '56.1',
     modules: '46',
     openssl: '1.0.2h' },
  arch: 'x64',
  platform: 'darwin',
  release: 
   { name: 'node',
     lts: 'Argon',
     sourceUrl: 'https://nodejs.org/download/release/v4.4.4/node-v4.4.4.tar.gz',
     headersUrl: 'https://nodejs.org/download/release/v4.4.4/node-v4.4.4-headers.tar.gz' },
  argv: 
   [ '/Users/tugenhua/.nvm/versions/node/v4.4.4/bin/node',
     '/Users/tugenhua/个人demo/process.js' ],
  execArgv: [],
  env: 
   { TERM_PROGRAM: 'Apple_Terminal',
     SHELL: '/bin/zsh',
     TERM: 'xterm-256color',
     TMPDIR: '/var/folders/l7/zndlx1qs05v29pjhvkgpmhjm0000gn/T/',
     Apple_PubSub_Socket_Render: '/private/tmp/com.apple.launchd.7Ax4C1EWMx/Render',
     TERM_PROGRAM_VERSION: '404',
     TERM_SESSION_ID: '82E05668-442D-4180-ADA3-8CF64D85E5A9',
     USER: 'tugenhua',
     SSH_AUTH_SOCK: '/private/tmp/com.apple.launchd.MYOMheYcL3/Listeners',
     PATH: '/Users/tugenhua/.nvm/versions/node/v4.4.4/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin',
     PWD: '/Users/tugenhua/个人demo',
     LANG: 'zh_CN.UTF-8',
     XPC_FLAGS: '0x0',
     XPC_SERVICE_NAME: '0',
     SHLVL: '1',
     HOME: '/Users/tugenhua',
     LOGNAME: 'tugenhua',
     SECURITYSESSIONID: '186a8',
     OLDPWD: '/Users/tugenhua/工作文档/sns_pc',
     ZSH: '/Users/tugenhua/.oh-my-zsh',
     PAGER: 'less',
     LESS: '-R',
     LC_CTYPE: 'zh_CN.UTF-8',
     LSCOLORS: 'Gxfxcxdxbxegedabagacad',
     NVM_DIR: '/Users/tugenhua/.nvm',
     NVM_NODEJS_ORG_MIRROR: 'https://nodejs.org/dist',
     NVM_IOJS_ORG_MIRROR: 'https://iojs.org/dist',
     NVM_RC_VERSION: '',
     MANPATH: '/Users/tugenhua/.nvm/versions/node/v4.4.4/share/man:/usr/local/share/man:/usr/share/man:/Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.13.sdk/usr/share/man:/Applications/Xcode.app/Contents/Developer/usr/share/man:/Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/share/man',
     NVM_PATH: '/Users/tugenhua/.nvm/versions/node/v4.4.4/lib/node',
     NVM_BIN: '/Users/tugenhua/.nvm/versions/node/v4.4.4/bin',
     _: '/Users/tugenhua/.nvm/versions/node/v4.4.4/bin/node',
     __CF_USER_TEXT_ENCODING: '0x1F5:0x19:0x34' },
  pid: 14034,
  features: 
   { debug: false,
     uv: true,
     ipv6: true,
     tls_npn: true,
     tls_sni: true,
     tls_ocsp: true,
     tls: true },
  _needImmediateCallback: false,
  config: {},
  nextTick: [Function: nextTick],
  _tickCallback: [Function: _tickCallback],
  _tickDomainCallback: [Function: _tickDomainCallback],
  stdout: [Getter],
  stderr: [Getter],
  stdin: [Getter],
  openStdin: [Function],
  exit: [Function],
  kill: [Function],
  mainModule: 
   Module {
     id: '.',
     exports: {},
     parent: null,
     filename: '/Users/tugenhua/个人demo/process.js',
     loaded: false,
     children: [],
     paths: 
      [ '/Users/tugenhua/个人demo/node_modules',
        '/Users/tugenhua/node_modules',
        '/Users/node_modules',
        '/node_modules' ] } }
```
如上就可以看到 process是node的全局变量，并且process有env这个属性，但是没有NODE_ENV这个属性。

# 二、process.env.NODE_ENV该如何配置？
process.env属性返回的是一个包含用户环境信息的对象，它可以区分开发环境或正式环境的依据，那么我们如何配置它呢？

## 方法1：配置环境变量

**windows环境配置如下：**
``` bash
#node中常用的到的环境变量是NODE_ENV，首先查看是否存在 
set NODE_ENV 

#如果不存在则添加环境变量 
set NODE_ENV=production 

#环境变量追加值 set 变量名=%变量名%;变量内容 
set path=%path%;C:\web;C:\Tools 

#某些时候需要删除环境变量 
set NODE_ENV=
```

**Linux配置(mac系统环境也属于这个)如下：**

``` bash
#node中常用的到的环境变量是NODE_ENV，首先查看是否存在
echo $NODE_ENV

#如果不存在则添加环境变量
export NODE_ENV=production

#环境变量追加值
export path=$path:/home/download:/usr/local/

#某些时候需要删除环境变量
unset NODE_ENV

#某些时候需要显示所有的环境变量
env
```

注意：如果NODE_ENV设置为production后，所有的项目都会处于正式环境中。
此时使用命令`npm install`下载依赖包时，只会把package.json中的dependencies依赖项下载下来，对于devDependencies中的依赖包是下载不下来的。因此需要使用上面的命令`unset NODE_ENV`删除刚刚设置的环境变量。

## 方法2：使用mode
在webpack4中可以通过mode来配置。

- **开发环境development**：`mode:"development"`
- **正式环境production**: `mode:"production"`
- 默认情况下webpack会将production作为mode的默认值。

我们可以在webpack.config.js中添加如下代码配置全局变量信息，因为当webpack进行编译的时候会全局设置变量，如下代码：
```js
let config = {
    devtool: "source-map",
    mode : "development",
    output: {
        path: resolve('../dist'),
        filename: '[name].js',
        chunkFilename: '[name].js',
        publicPath: './'
    }
}
```

## 方法3：使用DefinePlugin
在webpack3或者以下，就需要使用插件webpack自带插件DefinePlugin来配置。

> [DefinePlugin](https://webpack.js.org/plugins/define-plugin/#usage)官网的解释是：DefinePlugin允许我们创建全局变量，可以在编译时进行设置。

因此可以使用该属性来设置全局变量来区分开发环境和正式环境，这就是DefinePlugin的基本功能。

我们可以在webpack.config.js中添加如下代码配置全局变量信息，因为当webpack进行编译的时候会全局设置变量，如下代码：
``` js
module.exports = {
  plugins: [
    // 设置环境变量信息
    new webpack.DefinePlugin({
      'process.env': {
        NODE_ENV: JSON.stringify(process.env.NODE_ENV)
      }
    })
  ]
}
```
package.json中的打包配置如下：
``` json
"scripts": {
  "dev": "NODE_ENV=development webpack-dev-server --progress --colors --devtool cheap-module-eval-source-map --hot --inline",
  "build": "NODE_ENV=production webpack --progress --colors --devtool cheap-module-source-map",
  "build:dll": "webpack --config webpack.dll.config.js"
},
```
这样配置完成后，为了验证一下是否是全局变量，运行 `npm run dev` 打包后，在我们项目入口js文件中打印下即可：
```js
console.log(process.env.NODE_ENV); // 打印结果为 'development' 
```
发现process.env.NODE_ENV已经被作为全局变量打印出来了，因此在项目打包中为了区分开发环境和正式环境我们可以使用这种方法。

### 关于cross-env
#### 什么是cross-env呢？
它是运行跨平台设置和使用环境变量的脚本。

#### 它的作用是啥？
当我们使用DefinePlugin这种方法设置NODE_ENV时，大多数windows命令会提示将会阻塞或者异常，或者windows不支持NODE_ENV=development的这样的设置方式，会报错。因此cross-env出现了。我们可以使用cross-env命令来实现全开发平台的兼容。
要使用该命令的话，我们首先需要在我们的项目中安装该命令：

``` bash
npm install --save-dev cross-env
``` 

在package.json中的scripts命令如下：

``` json
"scripts": {
  "dev": "cross-env NODE_ENV=development webpack-dev-server --progress --colors --devtool cheap-module-eval-source-map --hot --inline",
  "build": "cross-env NODE_ENV=production webpack --progress --colors --devtool cheap-module-source-map",
  "build:dll": "webpack --config webpack.dll.config.js"
}
```
# 三、vue-cli3.0中的process.env.NODE_ENV
使用vue-cli3构建的项目就简单多了，因为vue-cli3使用上述的DefinePlugin方式帮你把process.env.NODE_ENV配置好了，我们不需要再自己去配置。
它自带了三种模式：

> **development**：在vue-cli-service serve下，即开发环境使用
**production**：在vue-cli-service build和vue-cli-service test:e2e下，即正式环境使用
**test**： 在vue-cli-service test:unit下使用

在package.json中的scripts命令如下
```json
{
  "name": "",
  "version": "0.1.0",
  "private": true,
  "scripts": {
    "dev": "vue-cli-service serve", //本地开发运行，会把process.env.NODE_ENV设置为'development'
    "build": "vue-cli-service build", //默认打包模式，会把process.env.NODE_ENV设置为'production'
  },
  "dependencies": {
  }
}
```