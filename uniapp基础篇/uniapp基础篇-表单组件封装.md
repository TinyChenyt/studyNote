# uniapp基础篇-表单组件封装

```vue
<script setup>
import { ref, reactive, useSlots, toRefs } from 'vue';
import UseImage from '@/hooks/useImage';

const useImage = UseImage();

const uploadConfig = useImage.getUploadConfig();

const props = defineProps({
  formData: {
    required: false,
    type: Object,
    default: () => {}
  },
  formRules: {
    require: false,
    type: Array,
    default: () => []
  },
  formConfig: {
    require: false,
    type: Array,
    default: () => []
  },
  showSubmitBtn: {
    required: false,
    type: Boolean,
    default: true
  },
  submitBtnText: {
    required: false,
    type: String,
    default: '提交'
  }
});

const emit = defineEmits(['submit']);

// 插槽对象
const slots = useSlots();

const rules = reactive({});

const formProRef = ref();

const { formData, formConfig } = toRefs(props);

const getPlaceholder = (data) => {
  let placeholder = `请选择${data.label}`;

  const arr = ['input', 'password', 'textarea', 'number'];

  if (arr.indexOf(data.type) !== -1) {
    placeholder = `请填写${data.label}`;
  }

  return {
    rule: {
      rules: [
        {
          required: true,
          errorMessage: placeholder
        }
      ],
      validateTrigger: 'submit'
    },
    placeholder
  };
};

formConfig.value.forEach((item) => {
  const placeholderData = getPlaceholder(item);

  const { placeholder, rule } = placeholderData;

  if (item.required) {
    rules[item.key] = item.rule || rule;
  }

  if (!item.placeholder) {
    item.placeholder = placeholder;
  }
});

const validate = () => {
  formProRef.value.validate((valid) => {
    if (!valid) {
      submit();
    } else {
      console.warn('[表单封装](校验错误)', valid);
    }
  });
};

const clearValidate = (data) => {
  formProRef.value.clearValidate(data);
};

const submit = () => {
  emit('submit', JSON.parse(JSON.stringify(formData.value)));
};

// 暴露函数
defineExpose({
  validate,
  submit,
  clearValidate
});

// 开关选择
const switchChange = (e) => {
  if (e.checked) {
    props.formData[e.key] = true;
  }
  props.formData[e.key] = !props.formData[e.key];
};

// 选择文件
const selectFile = async(e, item) => {

  const res = await fileUpload(e);
  const extname = e.tempFiles[0].extname;
  const { path: url, ...rest } = res;
  const newRes = Object.assign({}, { extname, url: useImage.getAuthUrl(url), path: url, ...rest });
  
  props.formData[item.key] = newRes;
  
};

// 文件上传
const fileUpload = (e) => {
  return new Promise((resolve, reject) => {
    const { tempFilePaths } = e;

    const imageUrl = tempFilePaths[0];

    uni.uploadFile({
      url: uploadConfig.url,
      filePath: imageUrl,
      name: 'file',
      header: uploadConfig.headers,
      success: (res) => {
        resolve(JSON.parse(res.data).data);
      },
      fail(err) {
        reject(err);
      }
    });
  });
};

// 上传失败
const uploadFail = (e) => {
  console.log(e);
};
</script>

<template>
	<view class="form-pro">
		<uni-forms v-model="formData" :rules="rules" :label-width="120" ref="formProRef">
			<template v-for="item in props.formConfig" :key="item.key">
				<uni-forms-item :label="item.label" :name="item.key" :required="item.required">
					<!-- 预留自定义表单 -->
					<slot v-if="slots[item.key]" :name="item.key" :value="formData[item.key]"></slot>
					<!-- 输入框 -->
					<uni-easyinput v-else-if="item.type === 'input'" v-model="formData[item.key]" :placeholder="item.placeholder" :disabled="item.disabled" clearable />
					<!-- 密码框 -->
					<uni-easyinput
						v-else-if="item.type === 'password'"
						v-model="formData[item.key]"
						type="password"
						:placeholder="item.placeholder"
						:disabled="item.disabled"
						show-password
					/>
					<!-- 文本框 -->
					<uni-easyinput
						v-else-if="item.type === 'textarea'"
						v-model="formData[item.key]"
						type="textarea"
						autoHeight
						:placeholder="item.placeholder"
						:disabled="item.disabled"
						clearable
					/>
					<!-- 数字输入框 -->
					<uni-number-box
						v-else-if="item.type === 'number'"
						v-model="formData[item.key]"
						:disabled="item.disabled"
						:min="item.props?.min"
						:max="item.props?.max"
						:step="item.props.step"
					/>
					<!-- 单选 -->
					<uni-data-checkbox v-else-if="item.type === 'radio'" v-model="formData[item.key]" :localdata="item.options" />
					<!-- 多选框 -->
					<uni-data-checkbox
						v-else-if="item.type === 'checkbox'"
						v-model="formData[item.key]"
						:localdata="item.options"
						:min="item.props?.min"
						:max="item.props?.max"
						multiple
					/>
					<!-- 下拉单选 -->
					<uni-data-select
						v-else-if="item.type === 'select'"
						v-model="formData[item.key]"
						:placeholder="item.placeholder"
						:disabled="item.disabled"
						:localdata="item.options"
						clear
					/>
					<!-- 联级单选 -->
					<uni-data-picker
						v-else-if="item.type === 'cascader'"
						v-model="formData[item.key]"
						:localdata="item.options"
						:placeholder="item.placeholder"
						:readonly="item.disabled"
						clearable
					/>
					<!-- 开关 -->
					<switch v-else-if="item.type === 'switch'" :checked="item.checked" :disabled="item.disabled" @change="switchChange(item)" />
					<!-- 日期 -->
					<uni-datetime-picker v-else-if="item.type === 'date'" v-model="formData[item.key]" type="date" :placeholder="item.placeholder" :disabled="item.disabled" />
					<!-- 日期时间 -->
					<uni-datetime-picker
						v-else-if="item.type === 'datetime'"
						v-model="formData[item.key]"
						type="datetime"
						:placeholder="item.placeholder"
						:disabled="item.disabled"
					/>
					<!-- 日期区间 -->
					<uni-datetime-picker
						v-else-if="item.type === 'daterange'"
						v-model="formData[item.key]"
						type="daterange"
						:start-placeholder="item.startPlaceholder"
						:end-placeholder="item.endPlaceholder"
						:disabled="item.disabled"
					/>
					<!-- 日期时间区间 -->
					<uni-datetime-picker
						v-else-if="item.type === 'datetimerange'"
						v-model="formData[item.key]"
						type="datetimerange"
						:start-placeholder="item.startPlaceholder"
						:end-placeholder="item.endPlaceholder"
						:disabled="item.disabled"
					/>
					<!-- 文件上传 -->
					<uni-file-picker
						v-else-if="item.type === 'upload'"
						v-model="formData[item.key]"
						:limit="item.props.limit || 1"
						:disabled="item.disabled"
						:file-extname="item.props.fileExtname"
						:mode="item.props.mode"
						@select="selectFile($event, item)"
						@fail="uploadFail"
					/>

					<view v-if="item.tips" class="w-100">
						<view class="tips" v-for="tip in item.tips" :key="tip">
							{{ tip }}
						</view>
					</view>
				</uni-forms-item>
			</template>
		</uni-forms>

		<button type="primary" @click="validate()" v-if="props.showSubmitBtn">{{ props.submitBtnText }}</button>
	</view>
</template>

<style scoped>
.form-pro {
	padding: 15px;
}

.tips {
	color: #909399;
	font-size: 28rpx;
	margin: 10rpx 0;
	font-weight: 400;
}
</style>

```

