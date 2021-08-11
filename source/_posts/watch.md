---
title: js实现input/textarea监听事件
date: 2017-10-18 16:25:21
tags: js jQuery
categories: 小知识
---

要求： 评论框，输入字数限制为200(不包含空格)，超过200字后，不允许用户输入，并且要求兼容IE8浏览器(~~当时avalon不支持~~)
```js
$('.sug_textarea').bind('input propertychange', function() { 
    //limit事件 
    var  $this  = $(this), 
    _val  = $this.val(); 
    if(_val) 
    { 
        var  s  = _val.replace(/[\t\r\n]+/g, '').replace(/\s+/g,"");//去掉所有空格 
        if(s.length  >= 200) 
        { 
            for(var  i  = 200;i< _val.length;i++){ 
                var  a  = _val.substring(0,i); 
                var  b  = a.replace(/[\t\r\n]+/g, '').replace(/\s+/g,""); 
                if(b.length  == 200){ 
                    $this.val(a); 
                } 
            } 
        }else{ 
            $this.val(_val); 
        } 
    } 
    //watch事件 
    var  txtVal  = $(this).val().trim();
    if(!txtVal==''){
        areaVal  = txtVal; 
    }else{ 
        areaVal  = ""; 
    } 
    btnClass(); 
});

```