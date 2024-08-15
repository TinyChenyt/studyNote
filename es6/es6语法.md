# es6语法 #

- let const
```js
let a = 1;
const b = 2;
```
- 模板字符串
```js
`a = ${a}`
```

- 解构赋值
```js
let [a, b] = [1, 2];
let {a, b} = {a: 1, b: 2};
```

- 箭头函数
```js
let a = (a, b) => a + b;
```
- 函数参数默认值
```js
let a = (a = 1, b = 2) => a + b;
```
- 函数参数解构
```js
let a = ({a = 1, b = 2}) => a + b;
```
- promise
```js
let a = new Promise((resolve, reject) => {
    resolve(1);
    reject(2);
}).then(res => {}).catch(err => {});
```
- class
```js
class A {
    constructor(a, b) {
        super(a, b);
    }
}
```
- 模块化
```js
import a from './a';

export default a;
```
- 迭代器
```js
for (let i of [1, 2, 3]) {
    console.log(i);
    yield i;
    throw new Error('error');
}
```
- 生成器
```js
for (let i of [1, 2, 3]) {
    console.log(i);
    yield i;
    throw new Error('error');
}
```
- Map Set
```js
let a = new Map([[1, 2], [3, 4]]);
let b = new Set([1, 2, 3]);
```
- Symbol
```js
let a = Symbol('a');
```
- Proxy
```js
let a = new Proxy({}, {});
```
- Reflect
```js
let a = Reflect.get(obj, 'a');
```
- Promise.all Promise.race
```js
Promise.all([1, 2, 3]).then(res => {}).catch(err => {});
```
- async await
```js
async function a() {
    let a = await fetch('a');
};
```
- URLSearchParams
```js
let a = new URLSearchParams('a=1&b=2');
```
- fetch
```js
fetch('a').then(res => {}).catch(err => {});
```

- 拓展运算符
