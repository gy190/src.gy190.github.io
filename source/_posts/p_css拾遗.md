---
title: css知识点拾遗
date: 2014-08-20 18:25:19
categories:
- 编程
tags:
- css
---

1. css3动画会影响页面的gif动画，可能导致gif动画静止  

2. margin-top取百分比在手机端不兼容，考虑用top  

3. 如果想让height取100%有效果，必须要在body和html上加上高度。 如果有滚动条，只要去掉目标容器的height使用min-height:100%即可 

4. css3 渐变translate是相对于元素本身的宽度（取100%则移动一个自身元素宽度的距离）。 position的元素（除fixed），left是相对于父容器的 

5. css3 box-sizing 

6. css3 display:box 控制子容器的呈现方式 box-flex 

7. img会有透明边距，只能用display:block可去除。 注意给width:100%，否则图片大小不会按照父元素的宽度去渲染。