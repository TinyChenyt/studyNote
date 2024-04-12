# JavaScript基础-Array

## 创建数组

**1. 创建一个空数组**

```js
let arr = [];

let arr = new Array();
```
**2. 创建一个有初始长度的数组**
   ```js
const length = 5;
   
let arr = new Array(length);
   ```
**3. 创建一个有初始值的数组**
```js
const length = 5;

let arr = [1,2,3];

let arr = new Array(1,2,3);

let arr = new Array(length).fill(0);
```

## 数组方法
**1. toString() 将数组转换为用,分隔的字符串**

```js
let arr = ['a', 'b', 'c'];

let str = arr.toString();

console.log(str);
```
**2.join() 将数组转换为字符串，可以指定分隔符**

```js
let arr = ['a', 'b', 'c'];

let str = arr.join('#');

console.log(str);
```
**3. pop() 删除数组的最后一个元素，返回值为删除的元素**

```js
let arr = ['a', 'b', 'c'];

let index = arr.pop();

console.log(`index: ${index} --> arr: ${arr}`);
```
**4.push() 在数组尾部添加一个新的元素，返回值为新的数组长度**

```js
let arr = ['a', 'b', 'c'];

let index = arr.push('d');

console.log(`index: ${index} --> arr: ${arr}`);
```
**5. shift() 删除数组的首个元素，返回值为删除的元素**

```js
let arr = ['a', 'b', 'c'];

let index = arr.shift();

console.log(`index: ${index} --> arr: ${arr}`);
```
**5. unshift() 在数组的头部添加新的元素，返回值为新的数组长度**

```js
let arr = ['a', 'b', 'c'];

let index = arr.unshift('-1');

console.log(`index: ${index} --> arr: ${arr}`);
```
**6. splice() 删除/添加数组元素 在原数组在做修改 返回值为被删除的元素**

```js
let arr = ['a', 'b', 'c'];
// splice(被修改或删除的元素的起始位置, 删除的元素的个数, 新插入的元素（可选）)
// 删除
let delArr = arr.splice(0, 1);
// 修改
let changeArr = arr.splice(1, 1, 'change');

console.log(`arr: ${arr} ---> delArr: ${delArr} ---> changeArr: ${changeArr}`);
```
**7.slice() 数组裁剪，原数组不会被改变，返回裁剪之后的新数组**

```js
let arr = ['a', 'b', 'c'];

// slice(开始裁剪的位置, 结束裁剪的位置)
let changeArr = arr.slice(1,2);

console.log(`arr: ${arr} ---> changeArr: ${changeArr}`);
```
**8.concat() 数组合并，返回新数组**

```js
let arr = ['a', 'b', 'c'];

let arr2 = ['d', 'e', 'f'];
// concat(需要合并的数组，可多个，用,进行分隔)
let allArr = arr.concat(arr2);

console.log(`arr: ${arr} ---> allArr: ${allArr}`);
```
**9.sort() 数组排序**

```js
let strArr = ["Banana", "Orange", "Apple", "Mango"];
let numArr1 = [5,3,1,7,0];
let numArr2 = [5,4,6,1,3];
/**
 * 字符串数组根据首字母大小进行排序
 * 数字数组可定义升序或降序
 */
strArr.sort();
numArr1.sort((a, b) => {
    return a - b;
});
numArr2.sort((a, b) => {
    return b - a;
})

console.log(`strArr: ${strArr} ---> numArr1: ${numArr1} ---> numArr2: ${numArr2}`);
```
**10. reverse() 反转数组**

```js
let strArr = ["Banana", "Orange", "Apple", "Mango"];

// 可用于字符串数组经过sort排序之后再反转
strArr.reverse();

console.log(`strArr: ${strArr}`);
```
**11. forEach() 循环数组，为数组的每一个元素调用一次回调函数 用于遍历获取数组的值，不对原数组进行操作，不返回新数组**

**若数组值为对象，则可改变对象中属性的值**

```js
let arr = [10,5,4,1,23];

arr.forEach((item, index) => {
    console.log(item, index);
})

let arr = [
  {
    name: 'a',
    age: 1
  },
  {
    name: 'b',
    age: 2
  }
];

arr.forEach(item => {
  item.age = 'bc'
})

console.log(arr);
```
**12. map() 循环数组，为数组的每一个元素调动一次回调函数 用于遍历数组，不对原数组进行操作，返回新数组**

```js
let arr = [10,5,4,1,23];

let newArr = arr.map((item) => {
    return item * 2;
})
```
**13. filter() 过滤数组 返回通过测试条件的新数组，不改变原数组**

```js
let arr = [10,5,4,1,23];

let newArr = arr.filter((item ,index) => {
    return item > 10;
})
```
**14. reduce() 数组从左往右计算， 可用于计算数组总和，返回最终计算值，不改变原数组**

```js
let arr = [10,5,4,1,23];

// Array.reduce(回调函数(先前返回的值, 当前的item值, 索引, 数组本身), 初始值)
let total = arr.reduce((total, item) => {
    return total + item
})
console.log('total: ', total);
```
**15. reduceRight() 数组从右往左计算，可用于计算数组总和，返回最终计算值，不改变原数组**

```js
let arr = [10,5,4,1,23];

let total = arr.reduceRight((total, item) => {
    return total + item
},100)
console.log('total: ', total);
```
**16. every() 检测数组所有元素是否通过测试条件，返回一个布尔值，是为true，否为flase**

```js
let arr = [10,5,4,1,23];

let flag = arr.every((item) => {
    return item > 5;
})

console.log(flag);
```
**17. some() 检测数组是否有某些元素通过测试条件，返回一个布尔值，是为true，否为flase**

```js
let arr = [10,5,4,1,23];

let flag = arr.some((item) => {
    return item > 5;
})

console.log(flag);
```
**18. indexOf() 从头部搜索元素在数组中的位置，元素在数组中存在则返回第一个发现该元素的位置，不存在则返回 -1**

```js
let arr = [10,5,4,1,23,1];

// indexOf(搜索的数组, 开始搜索的位置)
let flag = arr.indexOf(1);

console.log(flag);
```
**19. lastIndexOf() 从头部搜索元素在数组中的位置，元素在数组中存在则返回第一个发现该元素的位置，不存在则返回 -1**

```js
let arr = [10,5,4,1,23,1];

// lastIndexOf(搜索的数组, 开始搜索的位置)
let flag = arr.lastIndexOf(1);

console.log(flag);
```
**20. find() 在数组中寻找通过测试条件的第一个元素， 返回第一个通过测试条件的元素的值**

```js
let arr = [10,5,4,1,23,1];

let flag = arr.find((item) => {
    return item % 2 !== 0;
})

console.log(flag);
```
**21. findIndex() 返回第一个通过测试条件的值的索引**

```js
let arr = [10,5,4,1,23,1];

let flag = arr.findIndex((item) => {
    return item % 2 !== 0;
})

console.log(flag);
```
**22. Array.from() 将类似数组的对象和可遍历的对象转为数组**

```js
let arrLike = {
    '0': '1',
    '1': '2',
    '2': '3',
    length: 3
}

let arr = Array.from(arrLike);
console.log('arr: ', arr);
```
**23. Array.of() 将一组值转为数组**

```js
let arr = Array.of(1,2,3);

console.log(arr);
```
**24. fill() 用于数组填充 可初始化数组**

```js
let arr = Array.of(1,2,3);

arr.fill(0);

console.log(arr);
```
**25. includes() 检测数组是否包含给定的数值 返回一个布尔值**

```js
let arr = [1,2,3,4,5];

let flag = arr.includes(1);

console.log('flag: ', flag);
```
**26. flat() 拉平数组，接收一个参数，为降维的参数，返回拉平后的新数组，不改变原数组**

```js
let arr = [1,2,3,4,5,[2,3,4,[2,4,5]]];

let newArr = arr.flat(2);

console.log('newArr: ', newArr);
```
**27. flatMap() 对拉平数组进行map操作，只能展开一层数组**