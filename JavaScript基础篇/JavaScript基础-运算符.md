# JavaScript基础-运算符

## 算术运算符

### + 加

```javascript
let num = 10;

let str = 'abc';

let res = num + str // 10abc
```

### - 减

```javascript
let num = 10;

let str = 'abc';

let res = num - str // NaN
```

### * 乘

```javascript
let num = 10;

let str = 'abc';

let num2 = 100;

let res = num * num2 // 1000
```

### / 除

```javascript
let num = 1000;

let str = 'abc';

let num2 = 10;

let res = num / num2 // 100
```

### % 取余

```javascript
let num = 5;

let str = 'abc';

let num2 = 2;

let res = num % num2 // 1
```

### -- 自减

```javascript
let num = 5;

let str = 'abc';

let num2 = 2;

let res = --num + 1; // 5 先减再计算

let res2 = num2-- + 1; // 3 先计算再减
```

### ++ 自增（与自减同理）

```javascript
let num = 5;

let str = 'abc';

let num2 = 2;

let res = ++num + 1; // 7

let res2 = num2++ + 1; // 3
```

## 赋值运算符

### =

```javascript
let num = 10; // 10

let res = num // 10
```

### +=

```javascript
let num = 10; // 10

let res = num; // 10

res += num; // 20 --> res = res + num;
```

### -=

```javascript
let num = 10; // 10

let res = num; // 10

res -= num; // 0 --> res = res - num;
```

### *=

```javascript
let num = 10; // 10

let res = num; // 10

res *= num; // 100 --> res = res * num;
```

### /=

```javascript
let num = 10; // 10

let res = num; // 10

res /= num; // 1 --> res = res / num;
```

### %=

```javascript
let num = 10; // 10

let res = num; // 10

res %= num; // 0 --> res = res % num;
```

## 比较运算符

### == 等于，会进行类型转换

```javascript
let num = 10;

let str = '10'

let res = num == str // true
```

### === 恒等于，不会进行类型转换

```javascript
let num = 10;

let str = '10'

let res = num === str // false
```

### != 不等于

```javascript
let num = 10;

let str = '10'

let res = num != str // false
```

### !== 不等于

```javascript
let num = 10;

let str = '10'

let res = num !== str // true
```

### < 小于

```javascript
let num = 10;

let num2 = 100;

let str = 'af';

let str2 = 'bc';

let res = num < num2 // true

let res2 = str < str2 // true
```

数字根据大小来判断，字符串根据首字母大小来判断，**下面的小于等于，大于，大于等于同理。**

### <= 小于等于

```javascript
let num = 10;

let num2 = 100;

let str = 'af';

let str2 = 'af';

let res = num <= num2 // true

let res2 = str <= str2 // true
```

### > 大于

```javascript
let num = 10;

let num2 = 100;

let str = 'af';

let str2 = 'bc';

let res = num > num2 // false

let res2 = str > str2 // false
```

### >= 大于等于

```javascript
let num = 10;

let num2 = 100;

let str = 'af';

let str2 = 'bc';

let res = num >= num2 // false

let res2 = str >= str2 // false
```

## 条件运算符

### 三元运算符：条件 ? 真 : 假

```javascript
const trueFn = () => {
  console.log(true);
}

const falseFn = () => {
  console.log(false);
}

let num = 100;

num > 1000 ? trueFn() : falseFn(); // 输出false

let result = num > 10 ? 'yes' : 'no'; // yes
```

## 逻辑运算符

### || 或

```javascript
let num = 10;

let result = num > 5 || num++ > 10; // num = 10; result = true
```

或运算符，当有一个条件为真时，返回结果为真，当两个条件都为假时返回结果为假，**当第一个条件为真时，不执行第二个条件，直接返回结果。**

### && 与

```javascript
let num = 10;

let result = num > 50 && num++ > 10; // num = 10; result = false
```

与运算符，当有一个条件为假时，返回结果为假，只有当两个条件都为真返回结果为真，**当第一个条件为假时，不执行第二个条件。**

### ! 非

```javascript
let num = 10;

let result = !(num > 50) // true
```

## 位运算符

### & 位与

```javascript
let num = 10; // 1010
let num2 = 5; // 0101

let res = num & num2;// 1010 & 0101 --> 0000 res = 0
```

### | 位或

```javascript
let num = 10; // 1010
let num2 = 5; // 0101

let res = num | num2;// 1010 & 0101 --> 1111 res = 15
```

### ~

```javascript
let num = 10; // 1010
let num2 = 5; // 0101

// 0000 0000 0000 0000 0000 0000 0000 1010 --> 1111 1111 1111 111 1111 1111 1111 0101 --> 
// 1000 0000 0000 0000 0000 0000 0000 1010 --> 1000 0000 0000 0000 0000 0000 0000 1011
let res = ~num; // -11
```

### ^

```javascript
let num = 11; // 1011
let num2 = 5; // 0101

let res = num ^ num2; // 1110
```

**都为1或都为0时取0**

### << 左移

```javascript
let num = 11; // 1011
let num2 = 5; // 0101

let res = num2 << 2; // 0001 0100
```

### >> 右移

```javascript
let num = 11; // 1011
let num2 = 5; // 0101

let res = num2 >> 2; // 0001
```

## ES6拓展

### 指数运算符

```javascript
let num = 3;

let res = num ** 2; // 9 === 3的2次方

let res2 = 2 ** 3 ** 2; // 512
```

### 链判断运算符

```javascript
const obj = {
  name: 'foo',
  age: 18,
  children: {
    code: 'bar',
    self: true
  }
}

let res = obj.job.name; // 报错
let res2 = obj.job?.name // undefined
```

**判断当前属性是否存在，存在才往下访问属性**

### 逻辑赋值运算符
