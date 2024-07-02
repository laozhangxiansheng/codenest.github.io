---
title: CSS
banner_img: https://cdn.houdemingxin.com/image/default/B380716569044A5DA885EAFA36EE4FAF-6-2.png
date: 2024-06-14 16:22:40
tags: CSS
---

## CSS

### 选择器

- 基本选择器
  - 标签选择器
  - 类选择器
  - id 选择器
  - 通配符选择器
  - 属性选择器
  - 伪类选择器
  - 伪元素选择器
- 组合选择器
  - 后代选择器
  - 子元素选择器
  - 相邻兄弟选择器
  - 通用兄弟选择器
- 伪类选择器
  - 动态伪类选择器

### 重绘重排

- 重绘
  - 元素的外观发生改变时会触发重绘，例如：修改元素的颜色或者背景色时会导致页面重新绘制
- 重排
  - 指页面重新排列，dom 的变化影响了元素的布局，例如：页面初始化时，对 dom 节点进行增删改时，浏览器窗口的 resize 发生改变时都会触发重排
- 重排必然会导致重绘，重绘不一定导致重排

- display:none; (隐藏元素不占位) 会导致重排和重绘

- visibility:hidden; (隐藏元素占位) 只会导致重绘，不会导致重排

### 响应式布局

- 媒体查询
  - 媒体查询是 CSS3 引入的，通过媒体查询可以针对不同的媒体类型定义不同的样式
  - 媒体查询可以针对不同的屏幕尺寸、不同的设备类型、不同的设备方向进行响应式布局
  - 媒体查询的语法格式如下：

```css
@media mediatype and|not|only (media feature) {
  CSS代码;
}
```

- 媒体查询的 mediatype 属性
  - all: 用于所有设备
  - print: 用于打印机和打印预览
  - screen: 用于电脑屏幕、平板电脑、智能手机等
  - speech: 用于屏幕阅读器等发声设备
- 媒体查询的 media feature 属性
  - width: 定义视口的宽度
  - height: 定义视口的高度
  - max-width: 定义视口的最大宽度
  - min-width: 定义视口的最小宽度
  - max-height: 定义视口的最大高度
  - min-height: 定义视口的最小高度
  - orientation: 定义视口的横纵比例
  - aspect-ratio: 定义视口的宽高比例
  - color: 定义视口的颜色深度
  - color-index: 定义视口的颜色索引值
  - resolution: 定义视口的分辨率
  - scan: 定义视口的扫描方式
  - grid: 定义视口的栅格是否为网格
  - pointer: 定义视口的指针类型
  - hover: 定义视口的鼠标悬停状态
