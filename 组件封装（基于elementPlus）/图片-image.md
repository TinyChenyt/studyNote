```vue
<script setup>
import { nextTick, ref } from "vue";


const props = defineProps({
  path: {
    required: false,
    type: String,
    default: 'https://fuss10.elemecdn.com/e/5d/4a731a90594a4af544c0c25941171jpeg.jpeg'
  },
  lazy: {
    required: false,
    type: Boolean,
    default: true
  },
  preview: {
    required: false,
    type: Boolean,
    default: false
  },
  height: {
    required: false,
    type: Number,
    default: 150
  },
  width: {
    required: false,
    type: Number,
    default: 150
  }
});

const minHeight = 150;
const minWidth = 150;

const lazyLoad = () => {
  const io = new IntersectionObserver((entries) => {
    entries.forEach(item => {
      // 当前元素可见时
      if (item.isIntersecting) {
        // 替换src
        item.target.src = item.target.dataset.src;
        // 停止观察当前元素，避免不可见时再次调用 callback 函数
        io.unobserve(item.target);
      }
    });
  });

  const imgs = document.querySelectorAll('.demo-image-img');

  imgs.forEach(item => {
    io.observe(item);
  });
};

nextTick(() => {

  if (props.lazy) {
    lazyLoad();
  }
});

// 占位图片，可换成加载的图片路径
const lazyUrl = ref('');

</script>

<template>
  <div class="demo-image"
    :style="{ width: `${width > minWidth ? width : minWidth}px`, height: `${height > minHeight ? height : minHeight}px` }">
    <img id="imageId" :src="lazyUrl" :data-src="props.path" alt="" class="demo-image-img"
      :class="{ 'demo-image-img-pointer': preview }">
  </div>
</template>

<style scoped>
.demo-image-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.demo-image-img-pointer {
  cursor: pointer;
}
</style>
```

