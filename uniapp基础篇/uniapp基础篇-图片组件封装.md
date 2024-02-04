# uniapp基础篇-图片组件封装

```vue
<script setup>
// import { ref } from 'vue';
const props = defineProps({
  path: {
    require: false,
    type: String,
    default: ''
  },
  mode: {
    require: false,
    type: String,
    default: 'top'
  },
  lazy: {
    require: false,
    type: Boolean,
    default: true
  },
  preview: {
    require: false,
    type: Boolean,
    default: false
  }
});

const handleClickImage = () => {
  if (props.preview) {
    uni.previewImage({
      current: props.path,
      urls: [props.path]
    });
  }
};
</script>

<template>
	<image :src="props.path" :mode="props.mode" :lazy-load="props.lazy" :lazy-load-margin="0" @tap.stop="handleClickImage()"></image>
</template>

<style scoped></style>

```

