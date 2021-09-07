---
title: ESLint 使用指南
date: 2021-09-03 11:28:05
tags:
---

## 简介
eslint 检查我们写的 JavaScript 代码是否满足指定规则的**静态代码检查工具**。

- **JSHint** 和 **JSLint** 也是静态代码检查工具，但伴随着发展，他们已经无法满足需求，于是 **ESlint** 诞生了，因次 ESlint 比它们功能更强大也更灵活。
- ESLint 是用 Node.js 写的，可以通过 npm 来安装。
- ESLint 也可以在 webpack( eslint-loader ) 和 Gulp.js( gulp-eslint ) 中使用。
- ESLint 使用 Espree 解析 JavaScript。
- ESLint 使用 AST 去分析代码中的模式。
- ESLint 是完全插件化的。每一个规则都是一个插件, 并且你可以在运行时添加更多的规则。

## 特点
- 内置规则和自定义规则共用一套规则 API。
- 内置的格式化方法和自定义的格式化方法共用一套格式化 API。
- 额外的规则和格式化方法能够在运行时指定。
- 规则和对应的格式化方法并不强制捆绑使用。
- 每条规则都是各自独立的，可以根据项目情况选择开启或关闭。
- 用户可以将结果设置成警告或者错误。
- ESLint 并不推荐任何编码风格，规则是自由的。
- 所有内置规则都是泛化的。

## 作用
ESlint作为代码检查工具，其作用主要有以下几点：

- **统一代码风格规则**，如：缩进用几个空格；是否用驼峰命名法来命名变量和函数名等。
- **减少错误**， 如：相等比较必须用 ===，变量在使用前必须被声明，在条件语句中不能使用赋值语句等。
- **提高代码质量**，如：函数最多有多少条件分支；最多有几个参数，代码块最多能嵌套多少层等。
- **其他**。如： 禁用alert。这可以提高用户体验，因为 alert 框的外观不是那么好看，而且往往与网站的风格不搭，一般都会自定义 alert 框。

## 安装&配置
eslint 可以用 npm 安装依赖

**全局安装：**`npm install -g eslint`
**局部安装（推荐）：**`npm i -D eslint`
**自动生成配置：**`eslint --init`
或者可以在 `.eslintrc.js`(优先级：.eslintrc.js > .eslintrc.yaml > .eslintrc.yml > .eslintrc.json > .eslintrc > package.json) 的文件进行配置:
- **env**: 指定代码的运行环境（如：nodejs，browser，commonjs等）
- **globals**：额外的全局变量
- **parserOptions**: 指定 JavaScript 相关的选项。ecmaVersion 指定用哪个ECMAScript 的版本，默认是 3 和 5。
- **rules**: 具体检查的规则，不设置则不会检查
>这些规则的等级有三种：
>1、 "off" 或者 0：关闭规则。
>2、 "warn" 或者 1：打开规则，并且作为一个警告（不影响exit code）。
>3、 "error" 或者 2：打开规则，并且作为一个错误（exit code将会是1）。


```js
{
  "env": {
    "browser": true,
    "commonjs": true,
    "es6": true
  },
  "parserOptions": {
    "ecmaVersion": 6
  },
  "rules": {
    "indent": ["error", 2],
    "no-mixed-spaces-and-tabs": "error"
    "camelcase": "error",
    "eqeqeq": "warn",
    "curly": "error",
    "no-undef": "error",
    "no-unused-vars": "warn",
    "max-params": "warn"
  }
}
```