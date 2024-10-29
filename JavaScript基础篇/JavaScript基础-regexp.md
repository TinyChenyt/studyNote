# JavaScript基础-regexp

## 符号所表示的意义
符号 | 含义
--- | :---:
^ | 匹配字符串的开始位置
$ | 匹配字符串的结束位置
\d | 匹配一个数字
\D | 匹配一个非数字
\s | 匹配一个空白字符
\S | 匹配一个非空白字符
\w | 匹配一个字母、数字、下划线
\* | 匹配前面的字符零次或多次
\+ | 匹配前面的字符一次或多次
? | 匹配前面的字符零次或一次
{n} | 匹配前面的字符n次
{n,} | 匹配前面的字符至少n次
{n,m} | 匹配前面的字符至少n次，至多m次
[abc] | 匹配a、b、c中的任意一个
[^abc] | 匹配除了a、b、c之外的任意字符
. | 匹配任意一个字符
(xyt) | 匹配xyt，将xyt作为一个整体
\| | 匹配前面的表达式或后面的表达式
\ | 转义字符

**[练习链接](https://regex101.com/r/wL3xtE/1)**


## js中使用正则
### 使用new RegExp()创建
```js
var reg = new RegExp('abc');
console.log(reg); // /abc/

var reg2 = new RegExp('abc', 'g');
console.log(reg2); // /abc/g

var reg3 = new RegExp('abc', 'ig');
console.log(reg3); // /abc/gi

var reg4 = new RegExp('abc', 'i');
console.log(reg4); // /abc/i

var reg5 = new RegExp('abc', '');
console.log(reg5); // /abc/
```

### 直接创建
```js
var reg = /abc/;
var reg2 = /abc/g;
var reg3 = /abc/ig;
var reg4 = /abc/i;
```

### 匹配
```js
var reg = /abc/;
var str = 'abc';
// test()，字符串中是否有匹配的字符串，有则返回true，否则返回false
console.log(reg.test(str)); // true
// match()，返回匹配的字符串(数组)，如果没有匹配的字符串，则返回null
console.log(str.match(reg)); // ['abc']
// search()，返回匹配的字符串的索引(第一个)，如果没有匹配的字符串，则返回-1
console.log(str.search(reg)); // 0
console.log(str.replace(reg, 'def')); // def
console.log(str.split(reg)); // ['', '']
```
