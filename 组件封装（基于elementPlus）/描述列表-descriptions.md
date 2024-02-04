```vue
<script setup>
import { useSlots } from 'vue';

const props = defineProps({
  descriptionsData: {
    required: false,
    type: Object,
    default: () => { }
  },
  descriptionsConfig: {
    required: false,
    type: Array,
    default: () => []
  },
  descriptionsTitle: {
    required: false,
    type: String,
    default: ''
  },
  descriptionsColumn: {
    required: false,
    type: Number,
    default: 2
  },
  showExtraBtn: {
    required: false,
    type: Boolean,
    default: false
  },
  showExtraBtnText: {
    required: false,
    type: String,
    default: ''
  }
});

const slots = useSlots();

const openDetail = () => {
  emit('openDetail');
};

const emit = defineEmits(['openDetail']);

</script>

<template>
  <div>
    <el-descriptions class="margin-top" :title="props.descriptionsTitle" :column="descriptionsColumn" border size="large">
      <template #extra v-if="showExtraBtn">
        <el-button type="primary" @click="openDetail()">{{ props.showExtraBtnText }}</el-button>
      </template>
      <el-descriptions-item v-for="item in props.descriptionsConfig" :key="item.key" :span="item.span"
        label-align="center" :label="item.label">
        <slot v-if="slots[item.key]" :name="item.key" :value="descriptionsData[item.key]"></slot>
        <div v-else>
          {{ descriptionsData[item.key] }}
        </div>
      </el-descriptions-item>
    </el-descriptions>
  </div>
</template>

<style scoped></style>
```

