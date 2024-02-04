# JavaScript进阶-事件冒泡与事件捕获

## 事件冒泡

**子组件事件触发父组件事件（先触发子组件事件，然后触发父组件事件）**

**点击loader__bar**

![image-20240108094035322](https://tiny-blog.oss-cn-guangzhou.aliyuncs.com/blog/202401080940348.png)

## 事件捕获

**先触发父组件事件，然后触发子组件事件**

**addEventListener接收三个参数，第三个参数为是否开启事件捕获，默认为false**

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <style>
    #container {
      width: 400px;
      height: 400px;
      background-color: #333;
    }

    #loader {
      width: 200px;
      height: 200px;
      background-color: #444;
    }

    #loader__bar {
      width: 100px;
      height: 100px;
      background-color: #aaa;
    }
  </style>
</head>

<body>
  <div id="container">
    <div id="loader">
      <div id="loader__bar"></div>
    </div>
  </div>
</body>

<script>
  let container = document.getElementById('container');
  let loader = document.getElementById('loader');
  let bar = document.getElementById('loader__bar');

  container.addEventListener('click', (e) => {
    console.log('container');
  }, true)

  loader.addEventListener('click', (e) => {
    console.log('loader');
  }, true)

  bar.addEventListener('click', (e) => {
    console.log('bar');
  }, true)
</script>

</html>
```

**点击loader__bar**

![image-20240108093944123](https://tiny-blog.oss-cn-guangzhou.aliyuncs.com/blog/202401080939224.png)

## 阻止事件冒泡

**stopPropagation()和stopImmediatePropagation（）**

stopPropagation：阻止事件向父组件冒泡，stopImmediatePropagation阻止除当前事件外的事件

**stopImmediatePropagation()**

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <style>
    #container {
      width: 400px;
      height: 400px;
      background-color: #333;
    }

    #loader {
      width: 200px;
      height: 200px;
      background-color: #444;
    }

    #loader__bar {
      width: 100px;
      height: 100px;
      background-color: #aaa;
    }
  </style>
</head>

<body>
  <div id="container">
    <div id="loader">
      <div id="loader__bar"></div>
    </div>
  </div>
</body>

<script>
  let container = document.getElementById('container');
  let loader = document.getElementById('loader');
  let bar = document.getElementById('loader__bar');

  container.addEventListener('click', (e) => {
    console.log('container');
  })

  loader.addEventListener('click', (e) => {
    console.log('loader');
  })

  bar.addEventListener('click', (e) => {
    console.log('bar click');
    e.stopImmediatePropagation();
    // e.stopPropagation();
  })

  bar.addEventListener('click', (e) => {
    console.log('bar');
  })
</script>

</html>
```

![image-20240108095017422](https://tiny-blog.oss-cn-guangzhou.aliyuncs.com/blog/202401080950449.png)

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <style>
    #container {
      width: 400px;
      height: 400px;
      background-color: #333;
    }

    #loader {
      width: 200px;
      height: 200px;
      background-color: #444;
    }

    #loader__bar {
      width: 100px;
      height: 100px;
      background-color: #aaa;
    }
  </style>
</head>

<body>
  <div id="container">
    <div id="loader">
      <div id="loader__bar"></div>
    </div>
  </div>
</body>

<script>
  let container = document.getElementById('container');
  let loader = document.getElementById('loader');
  let bar = document.getElementById('loader__bar');

  container.addEventListener('click', (e) => {
    console.log('container');
  })

  loader.addEventListener('click', (e) => {
    console.log('loader');
  })

  bar.addEventListener('click', (e) => {
    console.log('bar click');
    // e.stopImmediatePropagation();
    e.stopPropagation();
  })

  bar.addEventListener('click', (e) => {
    console.log('bar');
  })
</script>

</html>
```

![image-20240108095126972](https://tiny-blog.oss-cn-guangzhou.aliyuncs.com/blog/202401080951997.png)

## 事件委托

借助冒泡机制，将需要绑定的多个子元素的方法绑定到父元素中做统一处理。