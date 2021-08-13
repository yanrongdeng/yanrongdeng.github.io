---
title: Js获取当前日期时间及其它操作
date: 2017-06-11 18:18:16
tags: js
categories: 小知识
---

# 获取时间de方法
```js
var myDate = new Date();
myDate.getYear();        //获取当前年份(2位)
myDate.getFullYear();    //获取完整的年份(4位,1970-????)
myDate.getMonth();       //获取当前月份(0-11,0代表1月)
myDate.getDate();        //获取当前日(1-31)
myDate.getDay();         //获取当前星期X(0-6,0代表星期天)
myDate.getTime();        //获取当前时间(从1970.1.1开始的毫秒数)
myDate.getHours();       //获取当前小时数(0-23)
myDate.getMinutes();     //获取当前分钟数(0-59)
myDate.getSeconds();     //获取当前秒数(0-59)
myDate.getMilliseconds();       //获取当前毫秒数(0-999)
myDate.toLocaleDateString();    //获取当前日期(2021/8/12)
myDate.toLocaleTimeString();    //获取当前时间(下午1:10:14)
myDate.toLocaleString( );       //获取日期与时间(2021/8/12下午1:10:14)
```
# 日期时间脚本库方法列表
## isLeapYear 判断闰年
```js
Date.prototype.isLeapYear = function()   
{   
    return (0==this.getYear()%4&&((this.getYear()%100!=0)||(this.getYear()%400==0)));   
}   
myDate.isLeapYear() // false
```
## Format 日期格式化
``` js
/**
* 说明：YYYY/yyyy/YY/yy 表示年份  MM/M 月份  W/w 星期  dd/DD/d/D 日期 hh/HH/h/H 时间  mm/m 分钟  ss/SS/s/S 秒  
* @param {string} formatStr 日期格式
*/
Date.prototype.Format = function(formatStr)   
{   
    var str = formatStr;   
    var Week = ['日','一','二','三','四','五','六'];  
  
    str=str.replace(/yyyy|YYYY/,this.getFullYear());   
    str=str.replace(/yy|YY/,(this.getYear() % 100)>9?(this.getYear() % 100).toString():'0' + (this.getYear() % 100));   
  
    str=str.replace(/MM/,this.getMonth()+1>9?(this.getMonth()+1).toString():'0' + (this.getMonth()+1));   
    str=str.replace(/M/g,this.getMonth()+1);   
  
    str=str.replace(/w|W/g,Week[this.getDay()]);   
  
    str=str.replace(/dd|DD/,this.getDate()>9?this.getDate().toString():'0' + this.getDate());   
    str=str.replace(/d|D/g,this.getDate());   
  
    str=str.replace(/hh|HH/,this.getHours()>9?this.getHours().toString():'0' + this.getHours());   
    str=str.replace(/h|H/g,this.getHours()); 

    str=str.replace(/mm/,this.getMinutes()>9?this.getMinutes().toString():'0' + this.getMinutes());   
    str=str.replace(/m/g,this.getMinutes());   
  
    str=str.replace(/ss|SS/,this.getSeconds()>9?this.getSeconds().toString():'0' + this.getSeconds());   
    str=str.replace(/s|S/g,this.getSeconds());   
  
    return str;   
}
myDate.Format("YYYY/MM/dd HH:mm:SS")    //"2021/08/12 14:17:31"
myDate.Format("MM-dd-YYYY HH:mm:SS")    //"08-12-2021 14:17:31"
myDate.Format("MM/dd/YYYY HH:mm:SS")    //"08/12/2021 14:17:31"
myDate.Format("MM-dd-YYYY")     //"08-12-2021"
myDate.Format("MM-dd")          //"08-12"
myDate.Format("M-d")            //"8-12"
```
## format 日期格式化(yyyy-MM-dd hh:mm:ss.S)
```js
/**
* 说明：月(M)、日(d)、小时(H)、分(m)、秒(s)、季度(q) 可以用 1-2 个占位符，年(y)可以用 1-4 个占位符，毫秒(S)只能用 1 个占位符(是 1-3 位的数字)
* @param {string} fmt 日期格式  "yyyy-MM-dd hh:mm:ss.S"  "yyyy-M-d h:m:s.S"
*/
Date.prototype.format = function(fmt) { 
    var o = {
        "M+": this.getMonth() + 1, //月份
        "d+": this.getDate(), //日
        "h+": this.getHours(), //小时
        "m+": this.getMinutes(), //分
        "s+": this.getSeconds(), //秒
        "q+": Math.floor((this.getMonth() + 3) / 3), //季度
        "S": this.getMilliseconds() //毫秒
    };
    if (/(y+)/.test(fmt))
        fmt = fmt.replace(RegExp.$1, (this.getFullYear() + "").substr(4 - RegExp.$1.length));
    for (var k in o)
        if (new RegExp("(" + k + ")").test(fmt))
            fmt = fmt.replace(RegExp.$1, (RegExp.$1.length == 1) ? (o[k]) : (("00" + o[k]).substr(("" + o[k]).length)));
    return fmt;
} 
```
## DateAdd 日期计算
```js  
Date.prototype.DateAdd = function(strInterval, Number) {   
    var dtTmp = this;  
    switch (strInterval) {   
        case 's' :return new Date(Date.parse(dtTmp) + (1000 * Number));  
        case 'n' :return new Date(Date.parse(dtTmp) + (60000 * Number));  
        case 'h' :return new Date(Date.parse(dtTmp) + (3600000 * Number));  
        case 'd' :return new Date(Date.parse(dtTmp) + (86400000 * Number));  
        case 'w' :return new Date(Date.parse(dtTmp) + ((86400000 * 7) * Number));  
        case 'q' :return new Date(dtTmp.getFullYear(), (dtTmp.getMonth()) + Number*3, dtTmp.getDate(), dtTmp.getHours(), dtTmp.getMinutes(), dtTmp.getSeconds());  
        case 'm' :return new Date(dtTmp.getFullYear(), (dtTmp.getMonth()) + Number, dtTmp.getDate(), dtTmp.getHours(), dtTmp.getMinutes(), dtTmp.getSeconds());  
        case 'y' :return new Date((dtTmp.getFullYear() + Number), dtTmp.getMonth(), dtTmp.getDate(), dtTmp.getHours(), dtTmp.getMinutes(), dtTmp.getSeconds());  
    }  
}  
```
## DateDiff 比较日期差
```js  
//| 比较日期差 dtEnd 格式为日期型或者有效日期格式字符串  
Date.prototype.DateDiff = function(strInterval, dtEnd) {   
    var dtStart = this;  
    if (typeof dtEnd == 'string' )//如果是字符串转换为日期型  
    {   
        dtEnd = getStringToTime(dtEnd);  
    }  
    switch (strInterval) {   
        case 's' :return parseInt((dtEnd - dtStart) / 1000);  
        case 'n' :return parseInt((dtEnd - dtStart) / 60000);  
        case 'h' :return parseInt((dtEnd - dtStart) / 3600000);  
        case 'd' :return parseInt((dtEnd - dtStart) / 86400000);  
        case 'w' :return parseInt((dtEnd - dtStart) / (86400000 * 7));  
        case 'm' :return (dtEnd.getMonth()+1)+((dtEnd.getFullYear()-dtStart.getFullYear())*12) - (dtStart.getMonth()+1);  
        case 'y' :return dtEnd.getFullYear() - dtStart.getFullYear();  
    }  
}  
```
## toString 日期转字符串
```js  
//| 日期输出字符串，重载了系统的toString方法  
Date.prototype.toString = function(showWeek)  
{   
    var myDate= this;  
    var str = myDate.toLocaleDateString();  
    if (showWeek)  
    {   
        var Week = ['日','一','二','三','四','五','六'];  
        str += ' 星期' + Week[myDate.getDay()];  
    }  
    return str;  
}  
myDate.toString()       // "2021/8/12"
myDate.toString(true)   // "2021/8/12 星期四"
```
##  toArray 日期分割为数组
```js  
Date.prototype.toArray = function()  
{   
    var myDate = this;  
    var myArray = Array();  
    myArray[0] = myDate.getFullYear();  
    myArray[1] = myDate.getMonth();  
    myArray[2] = myDate.getDate();  
    myArray[3] = myDate.getHours();  
    myArray[4] = myDate.getMinutes();  
    myArray[5] = myDate.getSeconds();  
    return myArray;  
}  
myDate.toArray() //  [2021, 7, 12, 14, 36, 31]
```
## DatePart 取日期的部分信息
```js  
//| 取得日期数据信息  
//| 参数 interval 表示数据类型  
//| y 年 m月 d日 w星期 ww周 h时 n分 s秒  
Date.prototype.DatePart = function(interval)  
{   
    var myDate = this;  
    var partStr='';  
    var Week = ['日','一','二','三','四','五','六'];  
    switch (interval)  
    {   
        case 'y' :partStr = myDate.getFullYear();break;  
        case 'm' :partStr = myDate.getMonth()+1;break;  
        case 'd' :partStr = myDate.getDate();break;  
        case 'w' :partStr = Week[myDate.getDay()];break;  
        case 'ww' :partStr = myDate.WeekNumOfYear();break;  
        case 'h' :partStr = myDate.getHours();break;  
        case 'n' :partStr = myDate.getMinutes();break;  
        case 's' :partStr = myDate.getSeconds();break;  
    }  
    return partStr;  
}  
myDate.DatePart('y')  //2021
myDate.DatePart('w') //"四"
```
## MaxDayOfDate 取日期所在月的最大天数
```js  
Date.prototype.MaxDayOfDate = function()  
{   
    var myDate = this;  
    var ary = myDate.toArray();  
    var date1 = (new Date(ary[0],ary[1]+1,1));  
    var date2 = date1.dateAdd(1,'m',1);  
    var result = dateDiff(date1.Format('yyyy-MM-dd'),date2.Format('yyyy-MM-dd'));  
    return result;  
}  
```
## WeekNumOfYear 判断日期所在年的第几周
```js 
Date.prototype.WeekNumOfYear = function()  
{   
    var myDate = this;  
    var ary = myDate.toArray();  
    var year = ary[0];  
    var month = ary[1]+1;  
    var day = ary[2];  
    document.write('< script language=VBScript\> \n');  
    // document.write('myDate = Datue(''+month+'-'+day+'-'+year+'') \n');  
    document.write('result = DatePart('ww', myDate) \n');  
    document.write(' \n');  
    return result;  
}  
```
# IsValidDate 验证日期有效性
```js  
//| 日期合法性验证  
//| 格式为：YYYY-MM-DD或YYYY/MM/DD  
function IsValidDate(DateStr)   
{   
    var sDate=DateStr.replace(/(^\s+|\s+$)/g,''); //去两边空格;   
    if(sDate=='') return true;   
    //如果格式满足YYYY-(/)MM-(/)DD或YYYY-(/)M-(/)DD或YYYY-(/)M-(/)D或YYYY-(/)MM-(/)D就替换为''   
    //数据库中，合法日期可以是:YYYY-MM/DD(2003-3/21),数据库会自动转换为YYYY-MM-DD格式   
    var s = sDate.replace(/[\d]{ 4,4 }[\-/]{ 1 }[\d]{ 1,2 }[\-/]{ 1 }[\d]{ 1,2 }/g,'');   
    if (s=='') //说明格式满足YYYY-MM-DD或YYYY-M-DD或YYYY-M-D或YYYY-MM-D   
    {   
        var t=new Date(sDate.replace(/\-/g,'/'));   
        var ar = sDate.split(/[-/:]/);   
        if(ar[0] != t.getYear() || ar[1] != t.getMonth()+1 || ar[2] != t.getDate())   
        {   
            //alert('错误的日期格式！格式为：YYYY-MM-DD或YYYY/MM/DD。注意闰年。');   
            return false;   
        }   
    }   
    else   
    {   
        //alert('错误的日期格式！格式为：YYYY-MM-DD或YYYY/MM/DD。注意闰年。');   
        return false;   
    }   
    return true;   
}   
```
# CheckDateTime 完整日期时间检查
```js  
//| 日期时间检查  
//| 格式为：YYYY-MM-DD HH:MM:SS  
function CheckDateTime(str)  
{   
    var reg = /^(\d+)-(\d{ 1,2 })-(\d{ 1,2 }) (\d{ 1,2 }):(\d{ 1,2 }):(\d{ 1,2 })$/;   
    var r = str.match(reg);   
    if(r==null)return false;   
    r[2]=r[2]-1;   
    var d= new Date(r[1],r[2],r[3],r[4],r[5],r[6]);   
    if(d.getFullYear()!=r[1])return false;   
    if(d.getMonth()!=r[2])return false;   
    if(d.getDate()!=r[3])return false;   
    if(d.getHours()!=r[4])return false;   
    if(d.getMinutes()!=r[5])return false;   
    if(d.getSeconds()!=r[6])return false;   
    return true;   
}   
```
# daysBetween 日期天数差
```js  
//| 求两个时间的天数差 日期格式为 YYYY-MM-dd   
function daysBetween(DateOne,DateTwo)  
{   
    var OneMonth = DateOne.substring(5,DateOne.lastIndexOf ('-'));  
    var OneDay = DateOne.substring(DateOne.length,DateOne.lastIndexOf ('-')+1);  
    var OneYear = DateOne.substring(0,DateOne.indexOf ('-'));  
  
    var TwoMonth = DateTwo.substring(5,DateTwo.lastIndexOf ('-'));  
    var TwoDay = DateTwo.substring(DateTwo.length,DateTwo.lastIndexOf ('-')+1);  
    var TwoYear = DateTwo.substring(0,DateTwo.indexOf ('-'));  
  
    var cha=((Date.parse(OneMonth+'/'+OneDay+'/'+OneYear)- Date.parse(TwoMonth+'/'+TwoDay+'/'+TwoYear))/86400000);   
    return Math.abs(cha);  
}  
``` 
# getStringDate 获取字符串日期
```js
function getStringDate( time , format="yyyy.MM.dd" ){
    // 对time进行正则判断
    if(/^[0-9]{14,15}$/.test(time)){ 
        //"yyyyMMddhhmmss"
        time = `${time.substring(0, 4)}/${time.substring(4, 6)}/${time.substring(6, 8)} ${time.substring(8, 10)}:${time.substring(10,12)}:${time.substring(12, 14)}`;
    }
    else if(/^\d{8}$/.test(time)){  
        // "yyyyMMdd"
        time = `${time.substring(0, 4)}/${time.substring(4, 6)}/${time.substring(6, 8)}`;
    }
    else if(/^\d{8}\s{1}[0-9]{2}:[0-9]{2}:[0-9]{2}\.?[0-9]?$/.test(time)){  
        // "yyyyMMdd hh:mm:ss"
        time = `${time.substring(0, 4)}/${time.substring(4, 6)}/${time.substring(6, 8)} ${time.split(" ")[1]}`;
    }
    return new Date(time).Format(format);
}
//获取当前时间
getStringDate(myDate,"YYYY-MM-DD HH:mm:SS"); // "2021-08-13 14:50:26"
getStringDate(myDate,"yyyyMMddhhmmss") // "20210813145026"
getStringDate(myDate,"yyyyMMdd hh:mm:ss") // "20210813 14:50:26"
//yyyyMMddhhmmss 字符串日期格式化
getStringDate("20210812155004","yyyy-MM-dd hh:mm:ss.S") //"2021-08-12 15:50:04.0"
getStringDate("20210812155004") // "2021.08.12"
//yyyyMMdd hh:mm:ss 字符串日期格式化
getStringDate("20210813 14:50:26","yyyy-MM-dd hh:mm:ss") // "2021-08-13 14:50:26"
```
# getStringToTime 获取中国标准时间(日期)
```js  
//DateStr 格式
function getStringToTime(DateStr)  
{   
    DateStr = this.getStringDate(DateStr,"yyyy-MM-dd hh:mm:ss");
    var converted = Date.parse(DateStr);  
    var myDate = new Date(converted);  
    if (isNaN(myDate))  
    {   
        //var delimCahar = DateStr.indexOf('/')!=-1?'/':'-';  
        var arys= DateStr.split('-');  
        myDate = new Date(arys[0],--arys[1],arys[2]);  
    }  
    return myDate;  
}  
getStringToTime("2021-08-12 14:07") // Thu Aug 12 2021 14:07:00 GMT+0800 (中国标准时间)
getStringToTime("2021/08/12 14:07") // Thu Aug 12 2021 14:07:00 GMT+0800 (中国标准时间)
getStringToTime("08/12/2020 14:07") // Wed Aug 12 2020 14:07:00 GMT+0800 (中国标准时间)
getStringToTime("08-12-2020 14:07") // Wed Aug 12 2020 14:07:00 GMT+0800 (中国标准时间)
getStringToTime("08-12-2020")       // Wed Aug 12 2020 00:00:00 GMT+0800 (中国标准时间)
```
# getTimeStamp 获取时间戳
```js
/**
* @param dateStr 多类型
*/
function getTimeStamp(dateStr) {
    dateStr = this.getStringDate(dateStr,"yyyy-MM-dd hh:mm:ss");
    var arr = dateStr.split(/[- :]/);
    let nndate = new Date(arr[0], arr[1] - 1, arr[2], arr[3], arr[4], arr[5]);
    nndate = Date.parse(nndate);
    return nndate;
}
```
# getDayWeek 获取“周几”
```js
/**
* @param date 多类型
*/
function getDayWeek(date) {
    date = this.getStringDate(date,"yyyy-MM-dd");
    const weekDay = ["星期日", "星期一", "星期二", "星期三", "星期四", "星期五", "星期六"];
    let newDate = date.replace(/-/g, "/");
    let week = weekDay[new Date(newDate).getDay()];
    return week;
}
```
# getFormatSeconds 获取时、分、秒
```js
functin getFormatSeconds(value) {
    var secondTime = parseInt(value); // 秒
    var minuteTime = 0; // 分
    var hourTime = 0; // 小时
    if (secondTime > 60) { //如果秒数大于60，将秒数转换成整数
        //获取分钟，除以60取整数，得到整数分钟
        minuteTime = parseInt(secondTime / 60);
        //获取秒数，秒数取佘，得到整数秒数
        secondTime = parseInt(secondTime % 60);
        //如果分钟大于60，将分钟转换成小时
        if (minuteTime > 60) {
            //获取小时，获取分钟除以60，得到整数小时
            hourTime = parseInt(minuteTime / 60);
            //获取小时后取佘的分，获取分钟除以60取佘的分
            minuteTime = parseInt(minuteTime % 60);
        }
    }
    var result = "" + parseInt(secondTime) + "秒";

    if (minuteTime >= 0) {
        result = "" + parseInt(minuteTime) + "分" + result;
    }
    if (hourTime > 0) {
        result = "" + parseInt(hourTime) + "时" + result;
    }
    return result;
}
```
# getDay 获取天数
```js
/**
* @param {Date} itemDay 目标时间 
* @param {Date} today 今天时间
* @return 判断今天、明天、后天、周几
*/
function getDay(itemDay = new Date(), today = new Date()) {
    today = new Date(today.format("yyyy-MM-dd"));
    const everyDayTime = 24 * 60 * 60 * 1000; // 每天毫秒数
    let days = Math.ceil((itemDay.getTime() - today.getTime()) / everyDayTime); // 目标时间距离今天的天数
    const dayList = ["周日", "周一", "周二", "周三", "周四", "周五", "周六"]; // 对应周天数的map
    days < 0 && (days = 0); // 目标天在今天之前的当做今天
    let preStr = "";
    switch (days) {
        case 0:
            preStr = "今天";
            break;
        case 1:
            preStr = "明天";
            break;
        case 2:
            preStr = "后天";
            break;
        default:
            preStr = dayList[itemDay.getDay()];
            break;
    }
    return preStr;
}
```
# getDayDesc 获取明后天 本周下周
```js
/**
* 获取明后天 本周下周
* @param {Date} itemDay
* @param {Date} today
*/
function getDayDesc(itemDay = new Date(), today = new Date()) {
    today = new Date(today.format("yyyy/MM/dd")); // 今天的00:00国际标准时间  东八区按照08:00
    itemDay = new Date(itemDay.format("yyyy/MM/dd")); // 目标天的00:00国际标准时间  东八区按照08:00
    const everyDayTime = 24 * 60 * 60 * 1000; // 每天毫秒数
    let days = Math.ceil((itemDay.getTime() - today.getTime()) / everyDayTime); // 目标时间距离今天的天数
    const todayWeekDay = today.getDay() || 7; // 今天：每周第几天
    let itemWeekDay = itemDay.getDay() || 7; // 目标天：每周第几天
    const surDay = 7 - todayWeekDay; // 本周剩余天数
    const dayList = ["一", "二", "三", "四", "五", "六", "日"]; // 对应周天数的map
    let preStr = "";
    switch (days) {
        case 0:
            preStr = "今天 ";
            break;
        case 1:
            preStr = "明天 ";
            break;
        case 2:
            preStr = "后天 ";
            break;
        default:
            days < 0 && (days = 0); // 目标天在今天之前的当做今天
            const nextWeek = days - surDay; // 距离今天的天数是否在本周
            if (todayWeekDay == 7 && days <= 7) {
                // 今天为本周最后一天 相差天数 <=7
                preStr = `周${dayList[days - 1]} `;
            } else if (nextWeek <= 0) {
                // 剩余天数在本周范围内
                preStr = `周${dayList[itemWeekDay - 1]} `;
            } else if (nextWeek > 0 && nextWeek <= 7) {
                // 出了本周 但在下周范围内
                preStr = `周${dayList[nextWeek - 1]} `;
            }
            break;
    }
    return preStr;
}
```
# getCommentTime 处理评论的发布时间
```js
/**
* @param num 参数为时间戳，type参数为自定义时间格式，例如"YYYY-mm-dd"
* @return '刚刚'、'X分钟前'、'X小时前'、'1天前'、'2天前'、自定义格式
*/
function getCommentTime(num, timeType = "YYYY-MM-dd HH:mm:SS") {
    if (num) {
        num = parseInt(num);
        var now = new Date();
        var r = now.getTime() - num;
        if (r < 86400000) {
            //24小时内
            var h = Math.floor(r / 3600000);
            if (h > 0) {
                //超过1小时
                return h + "小时前";
            } else {
                //1小时内
                var m = Math.floor((r % 86400000) / 60000);
                return m > 0? m + "分钟前":"刚刚";
            }
        } else if (r <= 172800000) {
            return "1天前";
        } else if (r <= 259200000) {
            return "2天前";
        } else {
            //超过24小时
            return this.getStringDate(num,timeType);
        }
    } else {
        return "";
    }
}
```

# dateChange 字符串格式相互转换
```js
/**
* @param str 
* @param {string} suffix + - * "" /
* 这个方法有点好玩，返回的结果，再调用一次，又可以还原
* @return dateChange(myDate,'-')//"2021-08-13"
*/
function dateChange(str, suffix) {
    let date = new Date(str);
    const year = date.getFullYear();
    const month = date.getMonth() + 1;
    const day = date.getDate();
    const t1 = [year, month, day].map(this.formatNumber).join(suffix);
    return `${t1}`;
}
// 两位数前面补0
function formatNumber(n) {
    const str = n.toString();
    // return str[1] ? str : `0${str}`;
    return str.padStart(2,"0");
}
Number.prototype.padStart = function(...arr){
    return String.prototype.padStart.call(this,...arr);
}
```