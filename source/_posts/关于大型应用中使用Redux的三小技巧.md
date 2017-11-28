---
title: 关于在大型应用中使用Redux的五个小技巧
categories:
    - 翻译
tags:
    - Redux
---

# 前言
开始试着翻译一些文章,希望大家多多指正.
<!--more-->


# [正文](https://techblog.appnexus.com/five-tips-for-working-with-redux-in-large-applications-89452af4fdcb)
## 存储数据使用索引对象.读取时使用选择器
### 索引对象存储数据

> 将数据的id作为键,数据本身作为值组合成一个对象

模拟一个从服务端请求到的用户数据
```js
[
    { id:'123',name:'MrGoodBye' },
    { id:'456',name:'MrsHello'}
]
```
使用索引对象存储在state中像这样:

```js
usersById: {
    '123':{ id:'123',name:'MrGoodBye' },
    '456':{ id:'456',name:'MrsHello'}
}
```
### 选择器读取

好处非常明显,当想要通过id获取数据时,用**选择器**来获取数据.非常便捷:
```js
const user = state.usersById[userId];
```
而如果未使用索引对象存储,就需要遍历用户列表,**性能开销**相对而言就大很多.

## 单独保存原始数据
原始数据就是在数据库中存放的数据,未经任何加工(前端没加工,服务端加工不算).将原始数据单独保存,如果需要修改应该创建一个副本(例如创建一个索引对象),在副本上修改.

比如编辑功能,在编辑时可能会修改原有的属性以及添加新的属性;保存到服务器,有些新创建的属性可能不会保存,那么服务器返回保存后的数据;如果直接替换原有的对象的话,一些新添加的属性就会丢失;再比如取消编辑,如果新创建了一个副本数据对象,取消就直接干掉这个对象就好了.

### 我的思考
编辑功能时我的做法是:将要编辑的数据与**当前组件的state**关联起来,保存或取消之前都不会dispatch给store;这样在保存后数据的重新赋值以及取消编辑上也能达到以上效果.

## 提取公用的reducer
例如每个应用中都会有大量的切换loading状态的场景,可以提取出来:
```js
// 各种loading状态的初始数据
// 格式一致,只有前缀不同
const initialLoadingState = {
  usersLoading: false,
  domainsLoading: false,
  subDomainsLoading: false,
  settingsLoading: false,
};

// action就可以这样写,type是一样的,根据不同的前缀来dispatch不同的action
// @param scope:不同的前缀
const setLoading = (scope, loading) => {
  return {
    type: SET_LOADING,
    payload: {
      scope,
      loading,
    },
  };
}

// 在reducer中就根据不同前缀进行state的修改
const loadingReducer = (state = initialLoadingState, action) => {
  const { type, payload } = action;
  if (type === SET_LOADING) {
    return Object.assign({}, state, {
      // 根据payload判断不同的loading状态.
      [`${payload.scope}Loading`]: payload.loading,
    });
  } else {
    return state;
  }
}

```


# 结语
这篇译文本来是打算作五次翻译的,但是译着译着,就发现译不下去了.原文的废话太多,逐句翻译真的是折磨人啊.还是提取出一些重点出来吧,有点像是做笔记的味道.以后得风格也会是**精简**突出的.

# Done