# Pinia

## **安装pinia**

```shell
yarn add pinia
# 或者
npm install pinia
```

## **mian.js引入**

```js
import { createPinia } from 'pinia';

const pinia = createPinia();

app.use(pinia);
```

## defineStroe的配置属性

- state ---> 数据仓库
- actions ---> 修改state的方法
- getter ---> 返回state的计算结果，但不影响state的数据

## **src下新建stores文件**

**分模块导出**

在stores下新建modules文件夹和index.js文件

在modules下新建一个useMyPinia.js文件

```js
// useMyPinia.js
import { defineStore } from 'pinia';

const useMyPiniaStore = defineStore('myPinia', {
  // state:数据仓库
  state: () => ({
    count: 0
  }),
  // 或者写为
  // state: () => {
  //   return {
  //     count: 0
  //   }
  // }
  actions: {
    // actions:修改state
    increment() {
      this.count++;
    }
  },
  // getters:计算属性,获取到计算之后的state，但是不修改state的数据
  getters: {
    doubleCount: (state) => {
      return state.count * 2;
    }
  }
})

export default useMyPiniaStore;
```

```js
// index.js
import useMyPiniaStore from "./modules/useMyPinia";

export {
  useMyPiniaStore
}
```

**使用**

```vue
<script setup>
import { useMyPiniaStore } from '../../stores';

const store = useMyPiniaStore();

console.log(store);
</script>

<template>
  <div>{{ store.count }}</div>
  <div>{{ store.doubleCount }}</div>
  <button @click="store.increment">+</button>
</template>

<style scoped></style>
```

