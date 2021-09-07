---
title: 工作中遇到的css问题
date: 2018-12-13 15:35:37
tags: CSS
---
### 一个长的英文字段截断
`word-break: break-all;` //不留空白
`word-wrap: break-word;` //留空白
`word-break: break-word;` //留空白
`word-wrap` 强调的是是否允许单词内断句，而 `word-break` 强调的则是怎么样来进行单词内的断句。![在这里插入图片描述](https://img-blog.csdnimg.cn/13687dea827c4d669c3e56cd158253eb.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zOTA0NzE3OQ==,size_16,color_FFFFFF,t_70)
### HTML的源代码排版方式
`white-space` -- 通过HTML文档的源代码的排版方式控制页面显示文本的排版方式 
取值: `normal | pre | nowrap | pre-wrap | pre-line | inherit` 
`normal`: 正常无变化(默认处理方式.文本自动处理换行.假如抵达容器边界内容会转到下一行) 
`pre`: 保持HTML源代码的空格与换行,等同与pre标签 
`nowrap`: 强制文本在一行,除非遇到br换行标签 
`pre-wrap`: 同pre属性,但是遇到超出容器范围的时候会自动换行 
`pre-line`: 同pre属性,但是遇到连续空格会被看作一个空格 
`inherit`: 继承 
初始值: `normal `
继承性: 是 
适用于: 所有元素 
white:白色.space:间隔,距离

实例如下：
1. span 文本内容超过宽度自动换行
```css
span{
    word-break: normal; 
    width: auto; 
    display: block; 
    white-space: pre-wrap;
    word-wrap: break-word;
    overflow: hidden ;
}
```
2. 自动变省略号...
```css
.ells{
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
}
```
3. vue v-html解析不了\r\n的解决办法
实现方式有三种：
1、 修改数据，将数据中所有的\r\n转换成
`.replace(/\r\n/g,"<br/>")`
2、 修改css，添加样式
`<p style="white-space: pre-wrap;" v-html="data"></p>`
3、 修改dom，添加pre标签
`<pre><p v-html="data"></p></pre>`

4.同一行显示，一部分完全显示，剩下按比例显示
![在这里插入图片描述](https://img-blog.csdnimg.cn/7f86b0a4f8854751956f38d82ea50022.png)

5.左右固定高度，中间自适应，不能用浮动（用absolute和margin）
.left{position:absolute;left:0;top:0;width:200px;}
.middle{margin:0 300px 0 200px;}
.right{position:absolute;top:0;left:0;width:300px;}

6.-webkit-tap-highlight-color: rgba(0,0,0,0);

7.
display: flex;
display: -webkit-flex;
height: 0.5rem;
justify-content: center;
-webkit-justify-content: center;
align-items: center;

8.设置虚线的两种方式
.line{width: 1px;position: absolute;right: 200px;top:44px;bottom: 44px; 
    background-image: url("./line.png");
    background: linear-gradient(to bottom, #979797, #979797 5px, transparent 5px, transparent);background-size: 100% 10px;
 } 

 ![在这里插入图片描述](https://img-blog.csdnimg.cn/eaca1bdc84554fee89dcb52335f0f88c.png)