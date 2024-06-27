# jq入门语法 #


## 入口函数  ##
```js
// 文档就绪事件
$(document).ready(function(){
    // 代码
});

// 或者

$(function(){
    // 代码
});
```

## 选择器 ##

jq可以通过$符号获取元素，获取元素的选择器与css选择器一样。
```js
// 标签选择器
$('button').click(function() {
    // 代码
});

// 类选择器
$('.btn').click(function() {
    // 代码
});

// id选择器
$('#btn').click(function() {
    // 代码
});

// 属性选择器
$('[type="button"]').click(function() {
    // 代码
});

// 选择所有元素
$('*').click(function() {
    // 代码
});

// 选择当前html
$('this').click(function() {
    // 代码
});

```

## 事件 ##

```javascript
// 点击
$('button').click(function() {});

// 双击
$('button').dblclick(function() {});

// 鼠标移入
$('button').mouseenter(function() {});

// 鼠标移出
$('button').mouseleave(function() {});

// 鼠标指针移动到元素上方，并按下鼠标按键时
$('button').mousedown(function() {});

// 在元素上松开鼠标按钮时
$('button').mouseup(function() {});

// 光标悬停
$('button').hover(function() {}, function() {});

// 获取焦点
$('button').focus(function() {});

// 失去焦点
$('button').blur(function() {});
```
