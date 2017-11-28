---
title: Cannot read property 'xxx' of undefined
categories: 
    - 常见错误
tags: 
     - js
---

开发时常见的一个报错:
```js
Cannot read property 'id' of undefined
Cannot set property 'id' of undefined
```
<!--more-->
### 正文
```js
let obj; // undefined
obj.id;// Uncaught TypeError: Cannot read property 'id' of undefined
obj.id = 1;// Uncaught TypeError: Cannot set property 'id' of undefined
```
用英文翻译如下:
> 不能读取`undefined`的属性`id`
> 不能给`undefined`设置属性`id`

所以当看到这种**报错**时,错误的触发点在调用者`obj`.
### 我的思考
刚开始学习js时看到这个报错第一反应就是id为undefined.自己工作了一段时间也是如此.
能够发现是因为有一次连续出现很多次这种报错,总感觉哪里不对劲.结合我那蹩脚的英文好好翻译了一下.
终于找到了问题所在.

我也不记得我是从哪个**教程**中学到的.**教程**中也没直接说`属性id`为`undefined`.
而在报错的第一时间去调试`id`,也怪我当时没有**深究**,导致很长一段时间都是在**东施效颦**.
可能教程中的教师也是在学习阶段这样"被学习"的,就造成了一个恶性循环.所以引起了我**一个大胆的想法**:
> 第一个在教学中这么调试的人**英文水准**肯定不咋地.

哈哈,想法够不够大胆!
### Done
