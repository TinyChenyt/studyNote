# JavaScript基础-Object

## 1.创建对象

### 1.1直接定义

```js
const obj = {
  name: 'foo',
  age: 36,
  sex: 'male'
}

console.log(obj.name); // foo
console.log(obj['age']); // 36
```
### 1.2使用{}写入变量和函数

```js
const str = 'string';

const obj = { str };

console.log(obj); // { str: 'string' }
```

**重命名属性**

```js
const str = 'string';

const obj = { objStr: str };

console.log(obj); // { objStr: 'string' }
```

## 2.对象的方法
### 2.1.constructor 返回创建对象原型的函数

```js
const obj = {
  name: 'foo',
  age: 36,
  sex: 'male'
}

console.log(obj.constructor); // [Function: Object]
```

### 2.2.Object.keys() 返回带有对象键的数组迭代器对象（属性的键名） 可用于检测对象是否为空对象

```js
const obj = {
  name: 'foo',
  age: 36,
  sex: 'male'
}

const nullObj = {};

console.log(Object.keys(obj)); // [ 'name', 'age', 'sex' ]

console.log(Object.keys(nullObj)); // []
```

### 2.3.toString 将对象作为字符串返回 不能返回字符串，则返回 [object Object] `Object.toString()` 总是返回对象构造函数


```js
const obj = {
  name: 'foo',
  age: 36,
  sex: 'male'
}


console.log(obj.toString()); // [object Object]

console.log(Object.toString(obj)); // function Object() { [native code] }
```
### 2.4.Object.values() 显示对象的值（属性的键值）

```js
const obj = {
  name: 'foo',
  age: 36,
  sex: 'male',
}


console.log(Object.values(obj)); // [ 'foo', 36, 'male' ]
```

### 2.5.Object.is() 用于比较两个值是否相等

**特殊：NaN与NaN比较相等， -0与+0不相等**

```js
console.log(Object.is(NaN, NaN)); // true

console.log(NaN === NaN); // false

console.log(Object.is(-0, +0)); // false

console.log(-0 === +0); // true
```

### 2.6.Object.assign() 合并对象 可用于浅拷贝
**后面的参数与前面的同名，则后面的覆盖前面的， undefined和null不能作为参数。 合并数组时，会把数组当做对象处理**

```js
const person = {
  name: 'person',
  age: 36,
  sex: 'male'
}

const obj = Object.assign({}, person, {job: 'job', name: 'bar'}); 

console.log(obj); // { name: 'bar', age: 36, sex: 'male', job: 'job' }

console.log(Object.assign([1,2,3], [4,5])); // [ 4, 5, 3 ]
```

### 2.7.Object.getOwnPropertyDescriptors() 返回指定对象所有自身属性（非继承属性）的描述对象
**Object.getOwnPropertyDescriptor() 返回某个对象属性的描述对象**

```js
const person = {
  name: 'person',
  age: 36,
  sex: 'male'
}

/**
{
  name: {
    value: 'person',
    writable: true,
    enumerable: true,
    configurable: true
  },
  age: { value: 36, writable: true, enumerable: true, configurable: true },
  sex: {
    value: 'male',
    writable: true,
    enumerable: true,
    configurable: true
  }
}
 */
console.log(Object.getOwnPropertyDescriptors(person));
```
### 2.8.Object.entries() 参数对象自身的（不含继承的）所有可遍历（enumerable）属性的键值对数组


```js
const person = {
  name: 'person',
  age: 36,
  sex: 'male'
}

console.log(Object.entries(person)); // [ [ 'name', 'person' ], [ 'age', 36 ], [ 'sex', 'male' ] ]
```

### 2.9.Object.fromEntries() 是`Object.entries()`的逆操作

```js
const person = {
  name: 'person',
  age: 36,
  sex: 'male'
}

const entriesObj = Object.entries(person)
console.log(Object.fromEntries(entriesObj));  // { name: 'person', age: 36, sex: 'male' }
```
### 2.10.Object.create(), 传入一个目标参数，返回一个新对象，新对象的__proto__来自于目标参数

```js
const foo = Object.create({ a: 1 })

console.log(foo); // {}
console.log(foo.a); // 1
console.log(foo.__proto__); // { a: 1 }
```

### 2.11.Object.hasOwn()判断属性是否为自身的属性

```js
const foo = Object.create({ a: 123 });
foo.b = 456;

console.log(Object.hasOwn(foo, 'a')); // false
console.log(Object.hasOwn(foo, 'b')); // true
```
## 3.属性的可枚举性和遍历

### 3.1.枚举

Object.getOwnPropertyDescriptor可以获取对象的描述对象，其中有**enumerable**，当enumerable为true即是可枚举，当属性为不可枚举时，则会有一些操作会忽略该属性，如：
- for...in
- Object.keys()
- JSON.stringfiy()
- Object.assign()

### 3.2.遍历

```js
const person = {
  name: 'person',
  age: 36,
  sex: 'male'
}

for(item in person) {
  console.log(item); // name age sex
}

// 转为数组进行遍历
Object.keys(person) // [ 'name', 'age', 'sex' ]

// 转为数组进行遍历
Object.getOwnPropertyNames(person); // [ 'name', 'age', 'sex' ]

// 转为数组进行遍历
Reflect.ownKeys(person); // [ 'name', 'age', 'sex' ]
```