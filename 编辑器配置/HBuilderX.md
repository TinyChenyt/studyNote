# HBuilderX配置

## 设置代码块（以设置vue文件中的代码块快捷输入为例）

![image-20240111145523717](https://tiny-blog.oss-cn-guangzhou.aliyuncs.com/blog/202401111455783.png)

点击进入编辑页

![image-20240111145614126](https://tiny-blog.oss-cn-guangzhou.aliyuncs.com/blog/202401111456186.png)

```json
{
	// 例子:
	"vue3": {
		"prefix": "vue3",
		"body": [
			"<script setup>",
			"",
			"</script>",
			"",
			"<template>",
			"\t<${0:div}></${0:div}>",
			"</template>",
			"",
			"<style scoped>",
			"",
			"</style>"
		],
		"triggerAssist": false,
		"description": "Log output to console twice"
	},
	"u3": {
		"prefix": "u3",
		"body": [
			"<script setup>",
			"",
			"</script>",
			"",
			"<template>",
			"\t<${0:view}></${0:view}>",
			"</template>",
			"",
			"<style scoped>",
			"",
			"</style>"
		],
		"triggerAssist": false,
		"description": "Log output to console twice"
	}
}
```

在左侧自定义代码中添加对应格式的代码块，配置快捷输入

新建一个vue文件，输入u3，获得代码提示，回车确认即可输入

![image-20240111151612438](https://tiny-blog.oss-cn-guangzhou.aliyuncs.com/blog/202401111516458.png)