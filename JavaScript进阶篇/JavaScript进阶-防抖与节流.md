# JavaScript进阶-防抖与节流

## 概念

- 函数防抖：事件触发n秒后执行回调，在执行回调之前，若事件再次被触发，则重新计时。可用于按钮点击事件（场景理解：电梯关门。自动关门前每次进来一个人都会重新打开计时）
- 函数节流：事件触发n秒后执行回调，在执行回调之前，若事件再次被触发，不进行处理，只有第一次触发生效。

## 节流函数

```javascript
const throttled = (fn, delay) => {
  let timer = null;

  // 获取第一次进来的事件
  let starttime = Date.now();

  return function () {
    // 获取当前事件时间
    let curTime = Date.now();
    // 计算剩余时间
    let remaining = delay - (curTime - starttime);
    let args = arguments;
    let context = this;
    // 如果timer存在，说明之前有事件触发，需要清除定时器
    if (timer) {
      clearTimeout(timer);
    }
    // 如果剩余时间小于等于0，说明已经到事件触发的时间了，需要立即触发事件
    if (remaining <= 0) {
      fn.apply(context, args);
      starttime = Date.now();
    } else {
      // 设置定时器
      timer = setTimeout(fn, remaining);
    }
  }
}
```



## 防抖函数

```javascript
const debounce = (fn, wait, immediate) => {
  // 定义定时器
  let timeout;

  return function () {
    let args = arguments;
    let context = this;

    // 如果定时器存在，说明之前有事件触发，需要清除定时器
    if (timeout) {
      clearTimeout(timeout);
    }

    // 如果是立即执行，则需要立即执行
    if (immediate) {
      // 第一次会立即执行，以后只有事件执行后才会再次触发
      let callNow = !timeout;
      // 设置定时器
      timeout = setTimeout(() => {
        timeout = null;
      }, wait);

      // 执行函数
      if (callNow) {
        fn.apply(context, args);
      }
    } else {
      // 定时器不存在，说明是事件触发后才会执行
      timeout = setTimeout(() => {
        fn.apply(context, args);
      }, wait);
    }
  }
};
```

