---
title: 处理Array的函数
date: 2018-08-12 15:26:44
tags: js
---

```js
/**
 * 清除数组中的空格元素:
 */
function removeTrim(arr) {
    let newArr = new Array();
    if (Array.isArray(arr)) {
        for (let i = 0; i < arr.length; i++) {
            if (arr[i] != "" && arr[i] != " ") {
                newArr.push(arr[i]);
            }
        }
        return newArr;
    } else {
        return "";
    }
},
/**
 * 处理数组为字符串
 */
function arrayToStr(arr) {
    if (arr) {
        if (arr.length > 1) {
            return arr.join("/");
        } else {
            return arr[0];
        }
    } else {
        return "";
    }
}
```