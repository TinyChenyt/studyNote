# JavaScript基础-类型判断

## 1.通用用法

### 1.1typeof

```javascript
const str = '123';

const arr = [123,123];

typeof str; // string
typeof arr; // object
```

**typeof只能判断基`number` ，`string`， `object`， `boolean`， `function`， `undefined`， `symbol`，引用数据类型都会返回object**

### 1.2instanceof

```javascript
let str = '123';

str instanceof Number; // false
```

**instanceof用于判断，但无法知道参数具体属于什么类型**

### 1.3Object.prototype.toString.call()

```javascript
let str = '123';

let arr = [1, 2, 3, 4, 5];

Object.prototype.toString.call(arr); // [object Array]
```

**可以获取到参数的详细类型**

### 1.4constructor

```javascript
let arr = [1, 2, 3, 4, 5];

arr.constructor // [Function: Array]
```

**获取参数类型，也可以访问构造函数**

## 2.判断数组

### 2.1Array.isArray()

```javascript
let arr = [1, 2, 3, 4, 5];

let res = Array.isArray(arr); // true
```

### 2.2arr.\__proto__ === Array.prototype

```javascript
let arr = [1, 2, 3, 4, 5];

let res = arr.__proto__ === Array.prototype // true
```

**原理参考JavaScript进阶-原型与原型链**

### 2.3Array.prototype.isPrototypeOf

```javascript
let arr = [1, 2, 3, 4, 5];

let res = Array.prototype.isPrototypeOf(arr) // true
```

## 3.判断null和undefined

**null是定义了一个参数，参数的值为null**

**undefined是已声明未定义（但在对象中，反问不存在的属性的返回值也是undefined）**

```javascript
let data1 = null;

let data2;

console.log(data1, data2);
```



```javascript
const obj = {
  data1: null,
}

console.log(obj.data1, obj.data2) // null undefined
```

**使用typeof进行判断**

```javascript
let data1 = null;

let data2;

console.log(typeof data1, typeof data2); // object undefined
```

**typeof null为object的原因**

JavaScripts使用32位储存值，通过值的低1位或3位来进行类型标记，object和null的低三位都是000，所以typeof识别为object

```javascript
let data1 = null;

console.log(Object.prototype.toString.call(data1)); // [object Null]
```

## 4.判断NaN
