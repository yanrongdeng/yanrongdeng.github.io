---
title: StyleLint 使用指南
date: 2021-09-03 13:18:02
tags:
---
## 简介

StyleLint 是『一个强大的、现代化的 CSS 检测工具』, 与 ESLint 类似, 是通过定义一系列的编码风格规则帮助我们避免在样式表中出现错误。

- stylelint：兼容多种格式的css代码规范工具(运行工具)
- stylelint-config-standard：标准配置规则
- stylelint-order：CSS属性排序插件(先写定位，再写盒模型，再写内容区样式，最后写 CSS3 相关属性)
- stylelint-scss：解析scss规范
- stylelint-webpack-plugin：通过webpack启动

## 特性 

- 了解**最新的 CSS 语法**，包括自定义属性和 4 级选择器
- 从 HTML、markdown 和 CSS-in-JS 对象和模板文本中**提取嵌入的样式**
- 解析**类似 CSS 的语法**，如 SCSS、Sass、Less 和 SugarSS
- 有超过**170 个内置规则**来捕获错误、应用限制和强制执行风格约定
- **支持插件**，因此您可以创建自己的规则或使用社区编写的插件
- **自动修复**大多数风格违规
- 是**很好的测试**超过15000的单元测试
- 支持您可以扩展或创建的**可共享配置**
- 没有意见，因此您可以根据您的确切需求对其进行自定义
- 拥有**不断增长的社区**，并被Facebook、GitHub和WordPress 使用

## 安装

`npm install -d -save-dev stylelint`
`npm install stylelint-config-standard stylelint-order --save-dev`

## 相关文件

.stylelintrc、stylelint.config.js：配置文件
.stylelintignore：忽略规则
.stylelintcache：缓存文件

## 配置

stylelint 使用cosmiconfig来完成查找和加载你的配置对象。从当前工作目录开始，它将按以下顺序查找尽可能的来源：

- 在 package.json 中的 stylelint 属性指定规则

- 在 .stylelintrc 文件中指定，文件格式可以是 JSON 或者 YAML 。也可以给该文件加后缀，像这样： .stylelintrc.json , .stylelintrc.yaml , .stylelintrc.yml , .stylelintrc.js 

- stylelint.config.js 文件，该文件 exports 一个配置对象

**语法格式**：rules 优先级大于extends，建议采用 extends 方式统一管理

```js
module.exports = {
  processors: [],
  plugins: [],
  extends:"stylelint-config-standard", // 这是官方推荐的方式
  rules: {
    "at-rule-empty-line-before": "always"|"never",
    "at-rule-name-case": "lower"|"upper",
    "block-no-empty": true,
  }
};
```
**配置项解析**
1. **rules**

rules 是一个对象，属性名为规则名称，属性值为规则取值，它告诉stylelint该检查什么，该怎么报错。所有规则默认都是关闭的。
每个规则配置符合以下形式之一：

- 一个值 (主要选项)
- 包含两个值的数组 ([primary option, secondary options])
- null(关闭规则)

2. **extends 扩展插件**

stylelint 的配置可以 extend 一个已存在的配置文件(无论是你自己的还是第三方的配置)。当一个配置继承了里一个配置，它将会添加自己的属性并覆盖原有的属性。

你也可以将 `extends` 设置为一个数组，每一项都是一个独立的 stylelint 配置项，后一项将会覆盖前一项，而接下来你自己书写的 rules 规则可以覆盖他们所有。

`extends` 的值实际上一个`定位器`（或者一个包含若干定位器的数组），所有可以通过 `require` 来使用的资源都可以作为 `extends` 的值。因此，可以使用 `Node` 的 `require.resolve()` 算法适应任何格式。这意味着一个“定位器”可以是：

- `node_modules` 中的某个模块名称 ，该模块的主文件需要返回一个配置对象 
(比如，stylelint-config-standard；模块的 main 文件必须是一个有效的 JSON 配置)
- 一个带有 `.js` 或 `.json` 扩展名的文件的绝对路径。
(which makes sense 如果你在 Node 上下文中创建了一个 JS 对象，并将它传入也是有效的)
- 一个带有 `.js` 或 `.json` 扩展名的文件的相对路径，相对于引用的配置 
(例如，如果 configA 是 extends: "../configB"，我们将查找 configB 相对于 configA)
- 正因为extends，你可以创建和使用可分享的 stylelint 配置。 如果你要发布你的配置到 npm，在你的 package.json 文件中使用 stylelint-config 关键字。

3. **plugins 插件列表**

插件一般是由社区提供的，对 stylelint 已有规则进行扩展，一般可以支持一些非标准的 css 语法检查或者其他特殊用途。一个插件会提供一个或者多个检查规则。

plugins 是一个数组，包含一组插件的定位器，这些定位器的取值跟 extends 一致。

plugins 声明后还需要在 rules 中使用它，具体规则名称以及可能的取值需要去查看每个插件的文档。
```json
{
  "plugins": [
    "../some-rule-set.js"
  ],
  "rules": {
    "some-rule-set/first-rule": "everything",
    "some-rule-set/second-rule": "nothing",
    "some-rule-set/third-rule": "everything"
  }
}
```

4. **processors 处理器列表：**

你还可以在 stylelint 的处理流中加入自己的处理函数，就是这里的 processors 。

processors 只能作为  命令行  和  Node API  使用，PostCss 的插件会忽略它们。

通过 processors，我们可以让 styleline 去处理 html 中 style 标签里面的 css 代码，MarkDown 里面的 css 代码块或者 js 里面一段包含 css 的字符串。

使用方法如下：
```json
{
  "processors": [
    "stylelint-html-processor",
    [ "some-other-processor", { "optionOne": true, "optionTwo": false } ]
  ],
  "rules": {..}
}
``` 
processors 的每一项也是一个定位器，需要额外的参数时，可以传递一个数组，第一项是定位器，第二项是需要的参数。

5. **defaultSeverity**

所有在第二个选项中没有指定严重级别的规则的默认严重级别。severity 可用的值为：
- "warning"
- "error"
 
6. **ignoreFiles**

一个文件匹配规则，或者一组文件匹配规则，来指定需要忽略的文件。

更高效的忽略文件的方法是通过 .stylelintignore 文件或者调整一下你的文件匹配规则。

 
ignoreFiles方式
```
// .stylelintignore
*.js
*.png
*.eot
*.ttf
*.woff
```
片段禁用规则
```
/* stylelint-disable */
/* （请说明禁止检测的理由）前端组件限制类名 */
  .cropper_topContainer .img-preview {
    border: 0 none;
  }
/* stylelint-enable */
```

## fix方式
stylelint --fix 就能搞定 更多语法规则

### 一键fix
在 package.json 中的 scripts 添加指令，然后 npm run lintcss 即可
```
{
  "scripts": {
    "lintcss": "stylelint 'src/**/*.css' --fix",
  }
}
``` 

### 手动fix
不放心的话，就针对指定文件自己执行， 文件一定要用""括起来
```
stylelint "src/less/bulma-cloud.less" --fix
```

 

问题排除： 
 

 

 

错误提示：

```
Unexpected unknown at-rule "@function" (at-rule-no-unknown) 

Unexpected unknown at-rule "@each" (at-rule-no-unknown) 

Unexpected unknown at-rule "@if" (at-rule-no-unknown) 

Unexpected unknown at-rule "@return" (at-rule-no-unknown)
```
 

 

 最开始只安装了官方推荐的定义规则"stylelint-config-standard",我想是不是我缺少插件的问题，所以我就多安装了一个"stylelint-scss"插件，错误已然存在，最后通过"stylelint-scss"的github找到了答案，就是需要添加排除规则。具体内容请点击访问

添加排除规则之后就好了。

```
{
  "extends": [
    "stylelint-config-standard",
    "stylelint-config-css-modules"
  ],
  "plugins": [
    "stylelint-scss"
  ],
  "rules": {
    "at-rule-no-unknown": [ true, {
      ignoreAtRules: ['extend', 'at-root', 'debug', 'warn', 'error', 'if', 'else', 'for', 'each', 'while', 'mixin', 'include', 'content', 'return', 'function']
    }]
  }
}
```

[参考文档](https://www.kancloud.cn/surahe/front-end-notebook/1153178)
[参考文档](https://cloud.tencent.com/developer/section/1489623)
[参考文档](https://www.cnblogs.com/jiaoshou/p/11284204.html)