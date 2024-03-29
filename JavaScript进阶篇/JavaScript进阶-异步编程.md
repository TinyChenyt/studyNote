# JavaScript进阶-异步编程

## Promise

promise对象代表一种异步操作，存在三种对象，pending，fulfilled和rejected

**注意点：对象状态不受外界影响（只有异步操作的结果，可以决定当前是哪一种状态）；一旦状态改变就不会再变；一旦新建就立即执行**

- 无法取消Promise，一旦新建它就会立即执行，无法中途取消。
- 如果不设置回调函数，Promise内部抛出的错误，不会反应到外部。
- 当处于pending状态时，无法得知目前进展到哪一个阶段（刚刚开始还是即将完成）。

```js
new Promise((resolve, reject) => {
  console.log(0);
  resolve();
}).then(() => {
  console.log(1);
})

console.log(2);
// 0 2 1
```

promise构造函数接收一个函数作为参数，函数存在两个参数resolve函数和reject函数，resolve函数将promise状态修改为成功，reject函数将promise状态修改为失败

调用resolve和reject函数是带有参数，参数会被传递给回调函数

```js
new Promise((resolve, reject) => {
  resolve(1);
  reject(2)
}).then((res) => {
  console.log(res); // 1
}).catch((err) => {
  console.log(err); // 2
})
```

如果传递的参数为一个promise对象p1，则p1的状态会传递给p2，p1决定了p2的状态

```js
let p1 = new Promise((resolve, reject) => {
  resolve();
  reject();
})

p1.then((res) => {
  console.log(1);
}).catch(() => {
  console.log(2);
})

let p2 = new Promise((resolve, reject) => {
  resolve(p1)
  reject(() => {
    console.log(3);
  })
})

p2.then(() => {
  console.log(4);
}).catch(() => {
  console.log(5);
})

```

此时p1的状态为resolve，所以输出14

如果p1状态为reject时，则输出25

resolve和reject的调用不会终结promise的参数函数的执行，并且resolve和reject还在本本轮事件循环的末尾执行，总是晚于本轮循环的同步任务

```js
new Promise((resolve, reject) => {
  resolve();
  new Promise((resolve, reject) => {
    resolve(1);
    console.log(2);
  }).then(res => {
    console.log(res);
  })
  console.log(3);
}).then(() => {
  console.log(4);
})

// 2 3 1 4
```

### then

### catch

### all

### race

### finally

## async/await

`async`表示函数里有异步操作，`await`表示紧跟在后面的表达式需要等待结果

当函数执行的时候，一旦遇到`await`就会先返回，等到异步操作完成，再接着执行函数体内后面的语句。

```js
async function async1() {
  console.log(1);
  await async2();
  console.log(2);
}

async function async2() {
  console.log(3);
}

console.log(4);
async1();
console.log(5);

// 4 1 3 5 2
```

```js
const fn = async () => {
  async function async1() {
    console.log(1);
    await async2();
    console.log(2);
  }

  async function async2() {
    console.log(3);
  }

  console.log(4);
  await async1();
  console.log(5);
  // 4 1 3 2 5
}

fn();
```

