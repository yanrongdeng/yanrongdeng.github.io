---
title: 学习JavaScript的过程
date: 2016-11-11 09:49:41
tags: js
categories: 学习笔记
---
​
# 变量的类型是由变量来决定的
**类型有**：String  Boolean  Number  object  null  undefined  数组  比较运算符 symbol

JavaScript把null、undefined、0、NaN和空字符串' ' 视为false，其他值一概视为true

# 处理数组de函数​​
![](https://img-blog.csdnimg.cn/20210328102026707.png#pic_left)

**请注意 :**  for ... in对 Array的循环得到的是 String而不是Number。

1. valueOf   ——> 返回的是数组本身的形式

2. toString   ——> 返回的是数组的字符串形式(  打印数组时，默认调用了toString方法  )

3. join   ——> 针对数组，加入到数组中，合并，变成字符串
![](https://img-blog.csdnimg.cn/20210328102057345.png)
补充：通过 call()，您能够使用属于另一个对象的方法。
A.call(B,x,y)  
1`改变函数A的this指向，使之指向B;
2` 把A函数放到B中运行，x和y是A函数的参数。
扩展：用原型对象来把字符串进行拼接
![](https://img-blog.csdnimg.cn/20210328102026707.png)

4. split   ——> 针对字符串，把字符串切割成数组
![](https://img-blog.csdnimg.cn/20210328102144235.png)

5. slice   ——> 截取数组的一部分,返回一个新的Array(引用类型)
![](https://img-blog.csdnimg.cn/2021032810215124.png)

6. splice  ——>  从指定的索引开始删除若干元素，然后再从该位置开始添加若干元素，返回删除的元素的数组
![](https://img-blog.csdnimg.cn/20210328102200651.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zOTA0NzE3OQ==,size_16,color_FFFFFF,t_70)

7. sort  ——> 默认以字母顺序对数组进行排序
按数字大小排序，需要加条件(大于0的时候，移动位置)
![](https://img-blog.csdnimg.cn/20210328102211730.png)
对字符串排序，用toLowerCase()函数，转化为小写，再比较

8. concat   ——> 连接（合并）数组

9. reverse ——> 把数组反转

10. unshift ——> 往Array头部添加元素，返回新数组长度lengt

11. shift  ——> 把Array的第一个元素干掉，返回删除的元素

12. push  ——> 向Array的末尾添加元素，返回新数组长度length

13. pop    ——> 把Array的最后一个元素删除掉，返回删除的元素

14. indexOf   ——> 搜索一个指定的元素的位置（返回的是数组的下标），没有就返回-1

15. reduce((total,value,index,arr) => { return total+value;})    ——>累加，从前往后 ( 每次运算后的值赋给total ) 返回一个值
![](https://img-blog.csdnimg.cn/20210328102445153.png)
![](https://img-blog.csdnimg.cn/20210328102449865.png)
![](https://img-blog.csdnimg.cn/20210328102455246.png)

16. reduceRight  ——> 从右到左执行

17. forEach((value, i, arr) => { })  ——> 数组循环，没有返回值，原数组不变

18. lastIndexoOf—返回元素首次出现的位置，不存在返回-1
注：使用严格相等运算符===进行比较，因此[NaN].indexOf(NaN)返回-1

19. map((value, i, arr) => { })      ——>返回新数组，原数组不变

20. every((value, i, arr) => { }) ——>返回布尔值，所有成员满足条件才返回true

21. some((value, i, arr) => { }) ——>返回布尔值，一个成员满足条件即返回true

22. filter((value, i, arr) => { })  ——> 返回满足条件的元素构成的数组

23. find((value, i, arr) => { })  ——>  找到满足条件的第一个元素

24. findIndex((value, i, arr) => { })  ——>  找到满足条件的第一个元素的索引

25. Math.max.apply(null,arr);

26. Math.min.apply(null,arr);

**补充：**
由于 JavaScript 数组没有 max() 方法，因此您可以应用 Math.max() 方法。
![](https://img-blog.csdnimg.cn/2021032810253168.png)
Math.max(...[1,2,3])

# 处理字符串de函数
1. toUpperCase  ——> 小写转成大写

2. toLowerCase ——> 大写转小写

3. indexOf ——> 搜索指定字符串出现的位置

4. substring  ——> 指定索引区间的子串

5. concat ——> 在字符串后面添加字符串

# 处理对象de函数
1. in    ——> 判断属性是否存在，包括继承的
![](https://img-blog.csdnimg.cn/20210328102546797.png)

2. hasOwnProperty ——>  判断一个属性是否自身拥有的，不是通过继承来的
![](https://img-blog.csdnimg.cn/20210328102553369.png)

# 面向对象编程
变量提升 （词法解释）

## 变量声明：

javascript程序并不全是一行一行往下执行的

1. 词法解释（预解析）
在整个文件中，查找带var声明的变量，如果有var声明的，把声明提前到当前作用域的最前面

2. 运行阶段（把代码从上往下 按顺序执行）
举例如下：
![](https://img-blog.csdnimg.cn/20210328102605327.png)

## 函数声明：

1）、函数声明会提升到当前作用域的最前面                      
![](https://img-blog.csdnimg.cn/2021032810261482.png)

2）、函数表达式不会提升
![](https://img-blog.csdnimg.cn/20210328102627549.png)

**当碰到函数表达式，函数声明，变量声明存在同名情况时：**

函数声明会被优先提升

变量声明会被忽略

表达式不会提升

如果出现多个同名的函数声明，怎么提升？   后面的会把前面的覆盖

不带var关键字的，变量不会提升
![](https://img-blog.csdnimg.cn/20210328102648357.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zOTA0NzE3OQ==,size_16,color_FFFFFF,t_70)
![](https://img-blog.csdnimg.cn/20210328102654734.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zOTA0NzE3OQ==,size_16,color_FFFFFF,t_70)

# this的指向
![](https://img-blog.csdnimg.cn/20210328102708466.png)
![](https://img-blog.csdnimg.cn/20210328102712842.png)
![](https://img-blog.csdnimg.cn/20210328102723277.png)
![](https://img-blog.csdnimg.cn/20210328102726959.png)
谁调用它，它就指向谁；

当不带拥有者对象调用对象时，this 的值成为全局对象。

如果一个函数不是 JavaScript 对象的方法，那么它就是全局对象的函数。

# 对象在内存中de表现形式：
笔记：js的三种引用类型：数组、函数、对象

当碰到引用类型‘赋值’’，其实是两个引用类型的变量指向的是同一个内存地址

# 封装
1. 没有名字的函数，叫匿名函数
 ![](https://img-blog.csdnimg.cn/20210328102744651.png)     

2. 不能直接写没有名字的函数(报错)

3.  立即表达式，函数自调用（自执行）
![](https://img-blog.csdnimg.cn/20210328102808155.png)

# 闭包
1、函数嵌套函数，一般把里面的函数用 返回值的方式  返回出来

2、闭包的作用域 形成于  定义时
![](https://img-blog.csdnimg.cn/20210328102816985.png)


# 原型对象
注意：

1、每个函数上面都有属性（prototype）指向了 函数的原型对象（CreateObj.prototype）

2、每个实例（构造函数的原型对象）上面都有一个隐式原型（_proto_）指向了 函数的原型对象

3、实例访问属性或者方法的问题，遵循以下原则：

如果实例上面存在，就用实例本身的属性和方法

如果实例上面不存在，就会顺着_proto_的指向一直往上查找，查找到就停止

4、每个函数的原型对象上面都有一个constructor属性 指向了构造函数本身
![](https://img-blog.csdnimg.cn/20210328102826184.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zOTA0NzE3OQ==,size_16,color_FFFFFF,t_70)
## 原型链
CreateObj.prototype._proto_===Object.prototype

Object.prototype._proto_为null
![](https://img-blog.csdnimg.cn/20210328102843266.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zOTA0NzE3OQ==,size_16,color_FFFFFF,t_70)


继承

# Js总共有9种数据类型
6种基本数据类型：string，number，boolean，null，undefined，symbol

3种引用数据类型：数组array，对象object，函数function

typeof下的数据类型有7种：string、number、boolean、symbol、undefined、function、object

# 2.设计模式

工厂模式

单例模式

迭代模式

订阅，发布者模式（观察者模式）

# 3.开源框架（gdom）的编写

v1.0.0版本

600行代码

目前支持的功能：

强大的选择器，事件绑定、Dom操作，动画，工具方法，插件扩展

# 4.插件开发

原生javascript

jquery插件

gdom扩展插件

​
​