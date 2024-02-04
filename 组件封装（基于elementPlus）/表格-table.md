```vue
<script setup>
import { useSlots } from 'vue';


const props = defineProps({
  tableConfig: {
    required: false,
    type: Array,
    default: () => []
  },
  tableData: {
    required: false,
    type: Array,
    default: () => []
  },
  height: {
    required: false,
    type: Number,
    default: 250
  },
  operationsWidth: {
    required: false,
    type: Number,
    default: 150
  },
  showDeleteBtn: {
    required: false,
    type: Boolean,
    default: false
  },
  showEditBtn: {
    required: false,
    type: Boolean,
    default: false
  },
});

const slots = useSlots();

const handleDelete = (data) => {
  emit('delete', data.row);
};

const handleEdit = (data) => {
  emit('edit', data.row);
};

const emit = defineEmits(['edit', 'delete']);
</script>

<template>
  <div>

    <el-table :data="props.tableData" border style="width: 100%" :height="height">
      <el-table-column v-for="item in props.tableConfig" :prop="item.key" :label="item.label" :key="item.key"
        :width="item.width">
        <template #default="scope">
          <slot v-if="slots[item.key]" :name="item.key" :data="scope.row"></slot>
          <span v-else>{{ scope.row[item.key] }}</span>
        </template>
      </el-table-column>
      <el-table-column fixed="right" label="操作栏" :width="operationsWidth" v-if="operationsWidth">
        <template #default="scope">
          <slot name="operations" :data="scope.row"></slot>
          <el-button v-if="props.showDeleteBtn" link type="danger" @click="handleDelete(scope)">删除</el-button>
          <el-button v-if="props.showEditBtn" link type="primary" @click="handleEdit(scope)">编辑</el-button>
        </template>
      </el-table-column>
    </el-table>

  </div>
</template>

<style scoped></style>
```

