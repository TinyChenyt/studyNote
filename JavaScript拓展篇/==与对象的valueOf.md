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

