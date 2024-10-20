
--- 
title:  【微信小程序】WXSS模板样式 
tags: []
categories: [] 

---
>  
 ✅作者简介：CSDN内容合伙人、阿里云专家博主、51CTO专家博主🏆 📃个人主页： 🔥系列专栏：🥇 💬个人格言：不断的翻越一座又一座的高山，那样的人生才是我想要的。这一马平川，一眼见底的活，我不想要,我的人生，我自己书写，余生很长，请多关照，我的人生，敬请期待💖💖💖 


<img src="https://img-blog.csdnimg.cn/75860e007264416dbfd5fc8c6f545ed3.gif#pic_center" alt="在这里插入图片描述"> 

#### WXSS模板样式
- - - - <ul><li>- - - - - - 


## 什么是WXSS

WXSS（WeiXin Style Sheets）是一套样式语言，用于美化WXML的组件样式，类似于网页开发中的CSS。

## WXSS和CSS的关系

WXSS具有CSS大部分特性，同时，WXSS还对CSS进行了扩充以及修改，以适应微信小程序的开发。与CSS相比，WXSS扩展的特性有： ①rpx尺寸单位 ②@import样式导入

## rpx

### 什么是rpx尺寸单位

rpx（responsive pixel）是微信小程序独有的，用来解决适配的尺寸单位。

### rpx的实现原理

rpx的实现原理非常简单：鉴于不同设备屏幕的大小不同，为了实现屏幕的自动适配，rpx把所有设备的屏幕，在宽度上等分为750份（即：当前屏幕的总宽度为750rpx）。 ①在较小的设备上，1rpx所代表的宽度较小 ②在较大的设备上，1rpx所代表的宽度较大 小程序在不同设备上运行的时候，会自动把rpx的样式单位换算成对应的像素单位来渲染，从而实现屏幕适配。

### rpx与px之间的单位换算

在iphone6中，屏幕宽度为375px,共有750个物理像素，等分为750rpx，则：**750rpx=375px=750物理像素 1rpx=0.5px=1物理像素**

|设备|rpx换算px（屏幕宽度/750）|px换算rpx（750/屏幕宽度）
|------
|iphone5|1rpx=0.42px|1px=2.34rpx
|iphone6|1rpx=0.5px|1px=2rpx
|iphone6 plus|1rpx=0.552px|1px=1.81rpx

🐱‍🏍官方建议：开发微信小程序时，设计师可以用iphone6作为视觉稿的标准。

## 样式导入

### 什么是样式导入

使用WXSS提供的@import语法，可以导入外联的样式表。

### @import的语法样式

@import后跟需要导入的外联样式表的相对路径，用；表示语句结束。示例如下：

**common.wxss**

```
.small-p{<!-- -->
    padding:5px;
}

```

**app.wxss**

```
@import "common.wxss";
.middle-p{<!-- -->
	padding;15px;
	}

```

## 全局样式和局部样式

### 全局样式

定义在app.wxss中的样式为全局样式，作用于每一个页面

### 局部样式

在页面的.wxss文件中定义的样式为局部样式，只作用于当前页面 ✅注意： ①当局部样式和全局样式冲突时，根据就近原则，局部样式会覆盖全局样式。 ②当局部样式的权重大于或等于全局样式的权重时，才会覆盖全局的样式

## 结束语🥇

以上就是微信小程序之wxss模板样式 持续更新微信小程序教程，欢迎大家订阅系列专栏 你们的支持就是hacker创作的动力💖💖💖

<img src="https://img-blog.csdnimg.cn/5b80ea7dab574ae5bb3fda934fe3f872.gif#pic_center" alt="在这里插入图片描述">
