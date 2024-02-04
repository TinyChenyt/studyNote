# JavaScript基础-Date

## 创建Date对象

```javascript
const date1 = new Date();

const date2 = new Date(79, 5, 24)

// const date3 = new Date(dateString);
const date3 = new Date("October 13, 1975 11:13:00");

// const date4 = new Date(year, month, day, hours, minutes, seconds, milliseconds);
const date4 = new Date(79, 5, 24, 11, 33, 0);
```

## Date对象方法

### getDate() 一个月的某一天

```javascript
const date = new Date();

const day = date.getDate();
```

### getDay() 一周的某一天

```javascript
const date = new Date();

const day = date.getDay();
```

### getFullYear() 返回年份

```javascript
const date = new Date();

const year = date.getFullYear();
```

### getMonth() 返回月份

```javascript
const date = new Date();

const month = date.getMonth();
```

### getHours() 返回小时

```javascript
const date = new Date();

const hour = date.getHours();
```

### getMinutes() 返回分钟
```javascript
const date = new Date();

const minutes = date.getMinutes();
```
### getSeconds() 返回秒
```javascript
const date = new Date();

const second = date.getSeconds();
```

### getMilliseconds() 返回毫秒

```javascript
const date = new Date();

const millisecond = date.getMilliseconds();
```