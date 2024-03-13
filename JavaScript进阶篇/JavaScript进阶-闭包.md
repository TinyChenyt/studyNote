# JavaScript进阶-闭包

**闭包，私有化变量**

函数可以访问函数外部的变量，但函数内部的变量无法被外部访问。

```js
var a = 10;

const fn = () => {
  console.log(a);
};

fn(); // 10
```

```js
const fn = () => {
  var a = 10;
}

fn();

console.log(a); // a is not defined
```

**对于需要仅通过方法进行改变，且不能被其他外部改变的变量，可以通过闭包实现**

```js
const add = () => {
  let count = 0;
  const fn = () => {
    return count += 1;
  };
  return fn;
}

let fn1 = add();

console.log(fn1()); // 1
```

**以上方法，除add方法外，无法通过其他途径获取到方法内的count进行改变**