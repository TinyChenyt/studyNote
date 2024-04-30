# axios

```js
'use strict'

import axios from 'axios';
import localStorage from './localStorage';

const axiosInstance = axios.create({
  baseURL: '/',
  timeout: 60 * 1000
});

if (process.env.NODE_ENV === 'development') {
  axiosInstance.baseURL = '';
} else if (process.env.NODE_ENV === 'production') {
  axiosInstance.baseURL = '';
}

// 请求拦截器
axiosInstance.interceptors.request.use(
  config => {
    // 添加token
    if (localStorage.get('token')) {
      config.headers.Authorization = `Bearer ${localStorage.get('token')}`;
    }

    return config;
  },
);

// 响应拦截器
axiosInstance.interceptors.response.use(
  response => {
    return response.data;
  },
  error => {
    return Promise.reject(error);
  }
);

// 基础请求
const baseRequest = (config) => {
  return axiosInstance(config);
};

// get请求
const get = (url, params = {}) => {
  return baseRequest({
    method: 'get',
    url,
    params
  });
};

// post请求
const post = (url, data = {}) => {
  return baseRequest({
    method: 'post',
    url,
    data
  });
};

// put请求
const put = (url, data = {}) => {
  return baseRequest({
    method: 'put',
    url,
    data
  });
};

// delete请求
const del = (url, params = {}) => {
  return baseRequest({
    method: 'delete',
    url,
    params
  });
};

export default {
  axiosInstance,
  get,
  post,
  put,
  del
};


```

