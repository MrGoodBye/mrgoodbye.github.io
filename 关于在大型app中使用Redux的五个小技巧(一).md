---
categories:
    - 翻译
tags:
    - Redux
---
![Redux](redux.png)

# 前言
## 本文术语
> 在正文中如果不作翻译,请参考:

Redux,state,App,dispatch,action,reducer,interface,index

## 为什么要翻译
为了学英语(虽然大部分单词只记与开发相关的词义),为了测验自己能坚持多久.

# [正文](https://techblog.appnexus.com/five-tips-for-working-with-redux-in-large-applications-89452af4fdcb)
## Redux简介
Redux是一个管理App的状态非常棒的工具.数据的单向流动以及关注于不可变state
使得state的变化变得易于推理.每一次state的更新都是由dispatched action来完成,
这样使得reducer函数翻译一个新的并且携带了所需改变的state.
我们在AppNexus上用Redux创建的许多用户界面用来解决庞大数量的数据和非常负载的
用户界面例如客户管理广告或者在我们的平台上发布库存.在开发这些interfaces时,我们
总结出一些有用的规则和技巧来保证Redux可管理的.接下来讨论的药店应该能帮助每个用Redux开发
大型,数据密集的App.

## 存储data时给其一个索引.访问data时使用选择器方式.
选择正确的数据结构对App的阻止和性能有很大的影响.从一个API中获取可序列化的数据
,使用index的方式存储的话,能够受益良多.
index是一个javascript对象,键为正要存储的data的id,值就是实际要存储的对象data.
这种模式与使用hashmap存储data非常相似,在查找用时方面也是有所收益的.
对那些精通Redux的大牛来说可能不是很惊奇.确实,Redux的作者Dan在他的教程中是推荐使用这种数据结构的.

试想你从REST API中获取到了一个用户对象列表,假设
