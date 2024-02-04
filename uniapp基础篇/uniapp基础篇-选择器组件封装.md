# uniapp基础篇-选择器组件封装

```vue
<script setup>
import { ref } from 'vue';

const props = defineProps({
  value: {
    require: false,
    type: Array,
    default: [0]
  },
  options: {
    require: false,
    type: Array,
    default: () => []
  }
});

const emit = defineEmits(['confirm']);

const popup = ref();

const open = () => {
  popup.value.open();
};

const cancel = () => {
  data.value = [0];
  popup.value.close();
};

const data = ref([0]);

const confirm = () => {
  emit('confirm', data.value);
  data.value = [0];
  popup.value.close();
};

const handleChange = (e) => {
  data.value = e.detail.value;
};

defineExpose({
  open,
  confirm
});
</script>

<template>
	<view class="pickerPro">
		<uni-popup ref="popup" type="bottom" background-color="#fff">
			<picker-view :indicator-style="'height: 110rpx'" :value="props.value" class="picker-view" @change="handleChange">
				<picker-view-column>
					<slot name="options"></slot>
					<view class="item" v-for="(item, index) in props.options" :key="index">{{ item.label }}</view>
				</picker-view-column>
			</picker-view>
			<view class="pickerPro__bottom">
				<slot name="operations"></slot>
				<view class="pickerPro__bottom__cancel" type="primary" @click="cancel()">取消</view>
				<view class="pickerPro__bottom__confirm" type="primary" @click="confirm()">确认</view>
			</view>
		</uni-popup>
	</view>
</template>

<style scoped>
.pickerPro {
	font-size: 36rpx;
	color: #333333;
}

.picker-view {
	height: 300rpx;
}

.item {
	display: flex;
	justify-content: center;
	align-items: center;
}

.pickerPro__bottom {
	display: flex;
	margin-top: 104rpx;
	margin-bottom: 126rpx;
	justify-content: center;
}

.pickerPro__bottom__cancel {
	width: 232rpx;
	height: 78rpx;
	background-color: #f2f2f2;
	color: #029cfb;
	border-radius: 12rpx;
	display: flex;
	justify-content: center;
	align-items: center;
	margin-right: 30rpx;
}

.pickerPro__bottom__confirm {
	width: 232rpx;
	height: 78rpx;
	background-color: #029cfb;
	color: #ffffff;
	border-radius: 12rpx;
	display: flex;
	justify-content: center;
	align-items: center;
}

.uni-picker-view-indicator:after,
.uni-picker-view-indicator:before {
	color: #f8f8f8;
	height: 2rpx;
	width: 650rpx;
	text-align: center;
	margin-left: 50rpx;
}
</style>

```

