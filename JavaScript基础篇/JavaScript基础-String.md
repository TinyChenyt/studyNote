# JavaScript基础-String

## 1.普通字符串与模板字符串
### 1.1.单行模板字符串

```js
const str = 'string';

const templateStr = `template ${str}`;

console.log(str, templateStr); // string template string
```
### 1.2.多行模板字符串

```js
const templateStr = `one row
tow end`

/**
 one row
 tow end
 */
console.log(templateStr);
```
### 1.3.模板标签

```js
console.log`string`; // [ 'string' ] 等同于 console.log(['string']);
```
## 2.字符串方法
### charAt() 返回在指定位置的字符

```js
let str = 'abc';

console.log(str.charAt(0) === str[0]); // a === a
```

### charCodeAt() 返回在指定的位置的字符的 Unicode 编码。

```js
let str = 'abc';

console.log(str.charCodeAt(0)); // 97
```

### concat() 连接多个字符串

```js
let str = 'abc';

let s = '123';

console.log(str.concat(s)); // abc123
```
### endsWith() 检查是否以指定字符串为结尾

```js
let str = 'abcbb';

console.log(str.endsWith('bb')); // true
```
### indexOf() 返回指定字符串第一次返回的位置，不存在则返回-1

```js
let str = 'abcbb';

console.log(str.indexOf('bbb')); // -1
```

### includes() 检查指定字符串是否存在，存在返回true，否则返回false

```js
let str = 'abcbb';

console.log(str.includes('bb')); // true
```

### lastIndexOf() 从后向前搜索

```js
let str = 'abcbb';

console.log(str.lastIndexOf('bb')); // 3
```

### repeat() 复制指定次数的字符串
```js
let str = 'abcbb';

console.log(str.repeat(2)); // abcbbabcbb
```

### replace() 查找匹配的子串，并替换与正则表达式匹配的子串
```js
let str = 'abcbb';

console.log(str.replace('bb', 'de')); // abcde
```

### replaceAll 查找匹配的子串，并替换与正则表达式匹配的所有子串
```js
let str = 'abcbb';

console.log(str.replaceAll('b', 'de')); // adecdede
```

### search() 查找与正则表达式相匹配的值。返回下标
```js
let str = 'abcbb';

console.log(str.search('b')); // 1
```

### slice(start, end) 取字符串的某个部分，并以新的字符串返回被提取的部分
```js
let str = 'abcbb';

console.log(str.slice(0, 2)); // ab
```

### split() 字符串分割为字符串数组
```js
let str = 'abcbb';

console.log(str.split('')); // [ 'a', 'b', 'c', 'b', 'b' ]
```

### startsWith() 查看字符串是否以指定的子字符串开头
```js
let str = 'abcbb';

console.log(str.startsWith('cc')); // false
```

### substr(from, len) 从起始索引号提取字符串中指定数目的字符
```js
let str = 'abcbb';

console.log(str.substr(0, 3)); // abc
```

### substring(from, to) 提取字符串中两个指定的索引号之间的字符
```js
let str = 'abcbb';

console.log(str.substring(0, 3)); // abc
```

### toLowerCase() 字符串转换为小写
```js
let str = 'abcbb';

console.log(str.toLowerCase()); // abcbb
```

### toUpperCase() 字符串转换为大写
```js
let str = 'abcbb';

console.log(str.toUpperCase()); // ABCBB
```

### trim() 去除两边的空白
```js
let str = '  abcbb  ';

console.log(str.trim()); // abcbb
```