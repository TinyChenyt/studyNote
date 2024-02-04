# JavaScript进阶-原型与原型链

**对象的原型**是它的构造函数的prototype所指向的原型对象

![image-20231227173711123](https://tiny-blog.oss-cn-guangzhou.aliyuncs.com/blog/202312271737191.png)

```javascript
let str = '123';

str.__proto__ === String.prototype // true
```

