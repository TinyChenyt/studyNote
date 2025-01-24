# ==与对象的valueOf

```js
const obj = {
  n: 1,
  valueOf: function () {
    return this.n++;
  },
}

console.log(obj == 1, obj == 2, obj == 3);
```

obj在进行比较的时候，实际上是获取obj内部的valueOf属性的值来进行比较
