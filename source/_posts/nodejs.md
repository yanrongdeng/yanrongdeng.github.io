---
title: nodejs
date: 2017-08-13 17:53:12
tags: nodejs
categories: 学习笔记
---

1.createServer
http.createServer(function(req,res){
   res.writeHead(200,{"Content-Type":"text/plain"});
   res.end("Hello world \n");
}).listen(3000,'127.0.0.1')

2.get 小爬虫
http.get(url,function(res){
  var html = "";
  res.on("data",function(data){
    html+=data;
  })
  res.on("end",function(){
    console.log(html);
  })
}).on("error",function(){
   console.log("获取课程信息失败~");
})
3.request
var req = http.request(options,function(res){
     console.log("Status: "+res.statusCode);
     console.log("headers: "+JSON.stringify(res.headers));
  res.on("data",function(chunk){
     console.log(Buffer.isBuffer(chunk));
     console.log(typeof chunk);
  })
  res.on("end",function(){
    console.log("评论完毕~");
  })
})
req.on("error",function(e){
   console.log("Error:"+e.message);
})
req.write(postData)
req.end()