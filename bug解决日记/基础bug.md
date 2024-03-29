# 基础bug

## 编辑数据之后重新获取数据，但图片没有刷新问题

**解决方案：给图片标签添加key值（确保唯一性）**

## 隐藏el-select的弹出层

**通过popper-class属性给el-select添加类名，然后在没有scoped的style标签中通过设置display:none来进行隐藏。**