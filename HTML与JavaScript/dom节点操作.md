# DOM节点操作

## 1、js获取DOM节点

**JavaScript一般通过节点的类名、id、标签名获取节点**

注意：由于js要操作页面节点，所有对应的js执行需要在页面渲染结束之后才能进行，否则会出现报错。页面大致渲染过程为：

html和css合成renderTree渲染，js则在另一个线程进行渲染，js渲染时不会停止renderTree的加载。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div class="container">
        <div class="wrapper">
            <div class="box" id="box1">
                <p>test1</p>
            </div>
            <div class="box" id="box2">
                <p>test2</p>
            </div>
            <div class="box" id="box3">
                <p>test3</p>
            </div>
            <p>test4</p>
        </div>
    </div>
</body>

<script>
// 通过类名获取节点
var box = document.getElementsByClassName('box');
console.log('box: ', box);

// 通过标签名获取节点
var p = document.getElementsByTagName('p');
console.log('p: ', p);

// 通过id获取节点
var box1 = document.getElementById('box1');
console.log('box1: ', box1);

// 通过选择器获取节点
var selectorBox = document.querySelectorAll('.box');
console.log('selectorBox: ', selectorBox);
</script>
</html>
```
![20250124142345](https://tiny-blog.oss-cn-guangzhou.aliyuncs.com/blog/20250124142345.png)


## 2、事件监听

## 3、样式修改

## 4、数据渲染