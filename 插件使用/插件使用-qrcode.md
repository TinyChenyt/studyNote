# 插件使用-qrcode

**链接生成二维码插件**

[官网](https://github.com/soldair/node-qrcode)

## 使用

**导入**

```vue
<script setup>
import { onMounted, ref } from "vue";
import QRCode from 'qrcode';

const qrcodeUrl = ref('');

const getCode = () => {
  QRCode.toDataURL('https://juejin.cn/', {
    color: {
      dark: '#000000',
      light: '#ffffff'
    },
  }).then((url) => {
    qrcodeUrl.value = url;
  })

  // QRCode.toCanvas('https://www.baidu.com/', { errorCorrectionLevel: 'H' }, (err, canvas) => {
  //   if (err) {
  //     throw err
  //   }

  //   const container = document.getElementById('test');
  //   container.appendChild(canvas);
  // })
}

onMounted(() => {
  getCode()
});

const downloadQRCode = () => {
  const a = document.createElement('a');
  a.href = qrcodeUrl.value;
  a.download = 'qrcode.jpg';
  a.click();
};
</script>

<template>
  <div id="qrcode">
    <img class="qrcode__img" :src="qrcodeUrl" alt="" srcset="">
    <!-- <div id="test"></div> -->
    <button @click="downloadQRCode()">下载</button>
  </div>
</template>

<style scoped>
.qrcode {
  height: 100%;
}
</style>

```

