# mockjs

安装

> **pnpm install --save-dev mockjs**

## 定义

在src下新建一个mock文件夹用于存放mock文件，在mock文件夹下新建一个mock.js文件，用于统一导出mock。

新建一个user.js文件，用于用户信息的模拟接口

```js
import Mock from 'mockjs';

Mock.mock('/user/info', 'get', () => {
  return {
    code: 200,
    success: true,
    message: '请求成功',
    data: {
      id: '0000000001',
      username: 'admin',
      sex: 'male',
      age: 18,
      address: '北京市',
      phone: '12345678901'
    }
  };
});
```

在mock.js中导入user.js文件

```js
import './user.js';
```

在main.js中导入mock文件

```js
import './mock/mock.js';
```

## 语法