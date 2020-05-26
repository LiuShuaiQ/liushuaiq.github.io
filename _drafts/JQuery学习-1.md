# JQuery学习 - 01

## 简介  

jQuery库包含以下功能:

- HTML元素选取
- HTML元素操作
- CSS操作
- HTML事件函数
- JavaScript特效和动画
- HTML DOM遍历和修改
- AJAX
- Utilities

除此之外,jQuery还提供大量的插件.


## 安装  

- 下载 [jquery.com](https://jquery.com/download/) 放到项目中

- 从CDN载入jQuery,如从Google中加载jQuery

## 语法

通过jQuery,可以选取HTML元素,并对他们执行“操作”(actions).

基础语法: `$(selector).action()`

- 美元符号定义jQuery
- 选择符`(selector)`查询和查找HTML元素
- jQuery的`action()`执行对元素的操作

实例: 

- `$(this).hide()` - 隐藏当前元素
- `$("p").hide()` - 隐藏所有的`<p>`元素
- `$("p.test").hide() ` - 隐藏所有`class="test"`的`<p>`元素
- `$("#test").hide() ` - 隐藏`id="test" ` 的元素
- 文档就绪事件, DOM 加载完成后执行:
``` javascript
$(document).ready(function(){
 
   // 开始写 jQuery 代码...
 
});
```
简洁语法:
```javascript
$(function(){
 
   // 开始写 jQuery 代码...
 
});
```

## jQuery选择器

jQuery 选择器允许您对 HTML 元素组或单个元素进行操作。


jQuery 选择器基于元素的 id、类、类型、属性、属性值等"查找"（或选择）HTML 元素。 它基于已经存在的 CSS 选择器，除此之外，它还有一些自定义的选择器。

jQuery 中所有选择器都以美元符号开头：$()。

### 常用选择器

- 元素选择器
    jQuery 元素选择器基于元素名选取元素。
    在页面中选取所有 <p> 元素: `$("p")`

- #id 选择器
    jQuery #id 选择器通过 HTML 元素的 id 属性选取指定的元素。
    `$("#test")`

- .class选择器
    jQuery 类选择器可以通过指定的 class 查找元素。
    `$(".test")`


## jQuery事件

jQuery 是为事件处理特别设计的。

事件处理程序指的是当 HTML 中发生某些事件时所调用的方法。

在 jQuery 中，大多数 DOM 事件都有一个等效的 jQuery 方法。


### 常用的jQuery事件方法

- $(document).ready()
- click()
- dblclick()
- mouseenter()
- mouseleave()
- mousedown()
- mouseup()
- hover()
- focus()
- blur()
