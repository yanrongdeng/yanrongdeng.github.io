---
title: web预览PDF
date: 2018-07-11 10:11:08
tags: PDF
categories: 小知识
---

参考：https://mozilla.github.io/pdf.js/web/viewer.html

1. 下载文件 viewer.html 和 viewer.css
2. 下载 js
compatibility.js、l10n.js、pdf.js、debugger.js 、viewer.js

3. 获取 PDF 的路径
```js
function getUrlParam(name) {
    var reg = new RegExp("(^|&)" + name + "=([^&]*)(&|$)");
    var r = window.location.search.substr(1).match(reg);
    if (r != null) return r[2];
    return null;
}
var confir_url = getUrlParam("name") || "a.pdf";
```

4. 在 html 里面引用 pdf.js
```html
<script src="./js/pdf.js"></script>

<!-- 方式一：新打开页面，跳转链接 -->
<a class="see_det" target="_blank" href="viewer.html?name=a.pdf" id="imgView">图片预览</a>

<!-- 方式二：当前页面展示（iframe ） -->
<a class="see_det" target="pdfContainer" href="viewer.html?name=a.pdf" id="imgView">图片预览</a>
<div class="lightbox" id="lightbox"></div>
<div id="pop" class="pop" style="display: none;">
    <iframe src="" frameborder="0" id="pdfContainer" name="pdfContainer"></iframe>
</div>

<style>
.lightbox{
    position: fixed;
    top: 0px;
    left: 0px;
    height: 100%;
    width: 100%;
    z-index: 11;
    opacity: 0.3;
    background-color: rgb(0, 0, 0);
    display: none;
}
.pop,iframe{
    position: absolute;
    left: 50%;
    top:0;
    width: 7.5rem;
    height: 100%;
    margin-left: -3.75rem;
    z-index: 12;
}
</style>
```