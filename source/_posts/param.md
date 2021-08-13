---
title: 在链接URL上获取param
date: 2015-07-12 15:18:52
tags: RegExp
categories: 小知识
---

```js
/**
 * 传入要的key 返回 value
 */
function getUrlParam(name) {
    let r,
        reg = new RegExp("(^|\\?|&|#)" + name + "=([^&#]*)(&|#|$)", "i");
    try {
        r = top.location.href.match(reg);
    } catch (e) {
        r = window.location.href.match(reg);
    }
    if (r != null) return decodeURIComponent(r[2]);
    return null;
}
```