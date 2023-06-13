---
layout: post
title: wx-02，数据属性，函数事件，if-for，text，image，样式
date: 2023-06-13 22:15 +0800
categories: [实训-微信小程序]
tags: [课程,微信小程序]     # TAG 名称应始终小写
author: master
---
1，基础功能
1，数据绑定
js的data中声明变量，页面{{}}调用
//wxml部分
<view>{{age}}</view>
<view>{{arr[1]}}</view>
<view>{{cat.num}}</view>
//js部分
Page({
data:{
age:90，
arr:[55,77,99]，
cat:{
num:3
　　　　}
}
})
2，属性绑定
直接在属性中写{{变量名}}
<view id="{{age}}"></view>
data:{
　age:5
}
//渲染结果：
<view id=”k5m”></view>
3，小程序的函数
小程序的函数，直接在Page里写即可
Page({
data:{
age:89
},
//函数
x1(){
　　},
　　x2:function(){
　　}
})
2，触摸事件
1，单击事件
bindtap，手指触摸后马上离开，函数名后不可带小括号。
//语法
<view bindtap=”函数名”>111</view>

例如：
<view bindtap=”x1”>111</view>
3，事件传参
小程序事件传递参数，不同于前端开发，它采用事件对象的自定义属性的方式，所有参数，以事件对象形式，都放在事件发生者的dataset里。

例如：
//参数写死：
<view data-参数1=”77” data-参数2=”66” bindtap=”x1”>按钮11</view>
//参数为变量
<view data-参数1=”{{age}}” data-参数2=”66” bindtap=”x1”>按钮11</view>
x1(e){
var target = e.currentTarget.dataset;
}
3，操作data
data中的数据可读可写。

例如：
//定义data中的数据
Page({
age:7,
　　arr:[5,2],
　　obj:{
　　a:6,
　　b:7
　　}
})
//函数读取data中的数据
console.log(this.data.age);
console.log(this.data.arr);
console.log(this.data.obj);
//修改、添加数据
this.setData({
age:88,//写单个变量
　　“arr[0]”:89,//写数组第一个
})
//修改数组
this.setData({
　　"arr[0]":89,//修改数组中的元素
})
//向数组中添加数据
this.data.arr.push("鲁迅");
//更新数组
this.setData({
arr:this.data.arr
})
小程序data中的对象，追加的属性，天生具有响应式，不需要类似vue中$set的设置
4，基础语法
1，wx:if条件渲染
使用 wx:if="" 来判断是否需要渲染该代码块，配合wx:else使用，可实现互斥效果

例如：
//字面量
<view wx:if=”{{true}}”>牛顿</view>
//变量
<view wx:if=”{{abc}}”>牛顿</view>
//else
<view wx:else>鲁迅</view>
ps：对比和hidden属性的区别
2，wx:for列表渲染
wx:for 控制属性绑定一个数组，把数组渲染到页面上。

例如：
<view wx:for=”{{arr}}”> {{index}} - {{item}}</view>
参数解释：
index，默认下标
item，默认元素
通过wx:for-index，wx:for-item可修改默认下表和元素
<view wx:for=”{{arr}}” wx:for-index=”index1” wx:for-item=”item1”>
{{index1}} - {{item1}}
</view>
参数解释：
index1，修改后的下标
item1，修改后的元素
3，wx:key唯一标识
和vue类似，若以后要动态修改此数组，需要提供wx：key

<view wx:for=”{{arr}}” wx:key="id"></view>
arr:[
{id:1:name:”wsc1”},
{id:2:name:”wsc2”},
{id:3:name:”wsc3”}
]
5，组件
1，text - 文本
text类似html中的span，重要属性如下：

1，space，是否显示连续空格
2，user-select，节点是否可选择
3，decode，是否解码（&nbsp; &lt; &gt; &amp; &apos; &ensp; &emsp;）

<text class="x1"
user-select="{{true}}"
decode="{{true}}"
space="nbsp">年&lt;圣诞节手动滑    稽后</text>
2，image图片
通过image，可以显示本地或者网路上的图片，若是本地图片，可以放在项目的任意目录下，路径写对即可。（行内块级元素）

常用属性：
1，src，图片路径
2，mode，图片裁剪、缩放的模式
1）scaleToFill（默认值），图片变形充满整个容器
2）aspectFit，图片完全居中显示，上下，左右会有白边
3）aspectFill，图片尽量全部显示，过长的部分将被裁切
4）center，图片上下左右居中，不缩放，自动裁切
6，控制样式
1，class控制
可以在{{}}中写入变量，或者三目运算符表达式，结果就是待渲染的class类名

例如：
//变量渲染
<view class=”c1 {{xx}}”>
data:{
xx:’c2’
}
//渲染结果
<view class=”c1 c2”>
//表达式渲染
<view class=”c1 {{xx?’c2’:’c3’}}”>
data:{
xx:true
}
//渲染结果
<view class=”c1 c2”>
2，rpx尺寸单位
rpx是小程序推荐的长度尺寸单位，英文全称（responsive pixel），它规定小程序中，界面宽度为750rpx。

可以理解为把屏幕横向分成了750份，不必关心屏幕分辨率的大小。

