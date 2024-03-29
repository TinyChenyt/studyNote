# axios封装

## 创建axiso

```javascript
const axiosInstance = axios.create({});
```

## 设置请求时长

```javascript
const axiosInstance = axios.create({
    baseURL: '/',
    timeout: 10000,
})
```

## 设置请求路径

```javascript
if (process.env.NODE_ENV === 'development') {
  instance.defaults.baseURL = '/';
} else if (process.env.NODE_ENV === 'production') {
  instance.defaults.baseURL = '/';
}
```

## 请求拦截

## 响应拦截
