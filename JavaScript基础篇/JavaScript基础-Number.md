# JavaScript基础-Number

## 定义number类型

1. ### 赋值定义

   ```javascript
   const num = 10;
   ```

2. ### 科学计数法

   ```javascript
   const y = 123e5; // 12300000
   ```

   

3. ### 使用Number定义

   ```javascript
   const num = new Number(123);
   ```

使用Number进行定义的参数是一个对象。

number除了常用的10进制，还可以定义为8进制，16进制等。



## number的方法

### Number.parseFloat()，将字符串转为浮点数

```javascript
let str = '10.09';

console.log(Number.parseFloat(str)); // 10.09
```

### Number.parseInt()，将字符串转为整数

```javascript
let str = '10.09';

console.log(Number.parseInt(str)); // 10
```

### Number.isFinite()，判断传递的参数是否为有限数字

```javascript
console.log(Number.isFinite(4 / 2)); // true
console.log(Number.isFinite(Infinity)); // false
```

**Infinity为无穷大**

### Number.isInteger()，传递的参数是否为整数

```javascript
let num = 10.09

console.log(Number.isInteger(num)); // false
console.log(Number.isInteger(4 / 2)); // true
```

### Number.isNaN()，判断传递的参数是否为isNaN

```javascript
let num = 10.09

console.log(Number.isNaN(num)); // false
console.log(Number.isNaN(4 / 'a')); // true
```

### isNaN() 

- 函数 isNaN 接收参数后，**会尝试将这个参数转换为数值**，任何不能被转换为数值的的值（非数字值）都会返回 true，会影响 NaN 的判断。
- 函数 Number.isNaN 会首先判断传入参数是否为数字，如果是数字再继续判断是否为 NaN ，**不会进行数据类型的转换**，这种方法对于 NaN 的判断更为准确。

```javascript
console.log(Number.isNaN('a')); // false
console.log(isNaN('a')); // true
```



## ES6拓展

### 数值分隔符

```javascript
const num = 1_000_000;

console.log(num === 1000000); // true
```

**数字前后，小数点前后不能使用分隔符，两个或两个以上的分隔符不能连着使用。**