# JavaScript基础-Math

**使用math对象前不需要定义**

## Math常用方法

### 圆周率

```javascript
const pi = Math.PI;

console.log(pi); // 3.141592653589793
```

### abs()， 返回绝对值

```javascript
const num = -10;

console.log(Math.abs(num)); // 10
```

### acos()，返回反余弦值

```javascript
const num = 1 / 2;

console.log(Math.acos(num)); // 1.0471975511965979
```

### asin()，返回反正弦值

```javascript
const num = 1 / 2;

console.log(Math.asin(num)); // 0.5235987755982989
```

### atan()，返回反正切值

```javascript
const num = 1 / 2;

console.log(Math.atan(num)); // 0.4636476090008061
```

### ceil()，向上取整

```javascript
const num = 1.2;

console.log(Math.ceil(num)); // 2
```

### exp()，返回e的指数

```javascript
const num = 2;

console.log(Math.exp(num)); // 7.38905609893065
```

### floor()，向下取整

```javascript
const num = 2.6;

console.log(Math.floor(num)); // 2
```

### log()，返回数的自然对数（e为底）

```javascript
const num = 7.38905609893065;

console.log(Math.log(num)); // 2
```

### pow(x,y)，返回x的y次幂

```JavaScript
const x = 2;
const y = 3;

console.log(Math.pow(x, y)); // 8
```

### round()，四舍五入

```javascript
const num = 5.4;

console.log(Math.round(num)); // 5
```

### random()，返回0-1之间的随机数

```JavaScript
// 0 - 1
console.log(Math.random()); 

// 1 - 10
console.log((Math.floor(Math.random() * 10) + 1));
```

### sin()，返回正弦

```javascript
const x = 2;

console.log(Math.sin(x)); // 0.9092974268256817
```

### tan()，返回正切

```javascript
const x = 2;

console.log(Math.tan(x)); // -2.185039863261519
```

### cos()，返回余弦值

```javascript
const num = 1 / 2;

console.log(Math.cos(num)); // 0.8775825618903728
```

### sqrt()，返回平方根

```JavaScript
const x = 9;

console.log(Math.sqrt(x)); // 3
```

### max()，返回最大值

```javascript
const arr = [10, 2, 3, 4, 1]

console.log(Math.max(...arr)); // 10
```

### min()，返回最小值

```JavaScript
const arr = [10, 2, 3, 4, 1]

console.log(Math.min(...arr)); // 1
```

## ES6拓展

### Math.trunc()，去掉小数部分，自动将参数类型转为number

```javascript
const str = '123.78'

console.log(Math.trunc(str)); // 123
```

###  Math.sign()，判断一个数是正数，负数，0以及非数值，会将参数进行类型转换

```javascript
Math.sign(5) // 1
Math.sign(-5) // -1
Math.sign(0) // 0
Math.sign(-0) // -0
Math.sign(NaN) // NaN
Math.sign(false) // 0
Math.sign(true) // 1
Math.sign('123') // 1
Math.sign('123a') // NaN
```

### Math.cbrt()，计算立方根

```javascript
const num = -1;

Math.cbrt(num); // -1
```
