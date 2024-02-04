# uniapp基础篇-常用API写法

## 路由跳转

**传递方**

```javascript
uni.navigateTo({
   url: `/pages/home/components/Detail/index?title=${title}`
});
```

**接收方**

```javascript
import { onLoad } from '@dcloudio/uni-app';
import { ref } from 'vue';


const title = ref('');

onLoad((e) => {
  title.value = e.title;
});
```

## 返回上一级

```javascript
uni.navigateBack({
  delta: 1
});
```

通过delta设置返回的层级。最多返回到首页

## 动态设置标题

```javascript
uni.setNavigationBarTitle({
  title: title.value
});
```

## 获取当前屏幕信息

```javascript
const info = uni.getWindowInfo();
info.screenHeight(); // 高度
```

## 获取节点信息

```javascript
// id获取
uni.createSelectorQuery().select('#imageId').boundingClientRect((data) => {
    imageHeight.value = data.height;
  }).exec();
```

```javascript
// class获取
  uni.createSelectorQuery().selectAll('.imageClass').boundingClientRect((data) => {
    console.log(data);
  }).exec();
```

## 触底加载

```javascript
import { onReachBottom } from '@dcloudio/uni-app';


onReachBottom(() => {});
```

**当onReachBottom位于子组件时，需要在父子组件中同时导入，否则h5端无法触发事件**
