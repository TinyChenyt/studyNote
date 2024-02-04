## 循环请求

**问题描述：**

数组通过forEach或者map进行循环，循环中有异步请求，需要循环获取对应的请求结果，没有获取到对应的请求结果，return值为空

**解决方法：**

将循环换成for in， for of

## uniapp的表单组件实现uni-file-picker组件手动上传

**问题描述：**

uni.uploadFile方法成功回调函数返回的res值无法传递给对应函数，且fileUpload方法中无法直接返回res

**解决方法**

构造promise

```javascript
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
```

## 修改富文本内容的样式

**问题描述：**

对于接口返回的富文本内容，Vue中可以直接用v-html进行渲染，但无法修改富文本内容的样式

**解决方法：**

1.通过样式穿透进行修改，但富文本的html片段没有class值，只能通过标签选择器修改

2.直接修改富文本的html片段，通过正则匹配添加内联样式。

```javascript
newContent = newContent.replace(/\<span style="font-size: 16px; font-family: 微软雅黑;">/gi, '<span style="color: #333333; line-height: 28px; font-size: 16px; font-family: 微软雅黑;">');
```

```javascript
  const changeText = ['一、', '二、', '三、', '四、', '五、', '六、'];

  let newContent = html;
  changeText.forEach((item) => {
    let str = '\<p style="text-indent: 37px; text-align: start;"><strong>' + item + '<\/strong><\/p>';
    let reg = new RegExp(str, 'gi');

    newContent = newContent.replace(
      reg,
      `<div style="display: flex;margin: 18px 0 11px 0;">
	     <div style="font-size:17px; background-color: #1380DE;color: #ffffff;height: 25px;width: 133px;padding: 4px 0 4px 10px;clip-path: polygon(0 100%, 0 0, 91% 0, 100% 100%);">${item}</div>
	 	 <div style="width: 20px; height: 33px; background-color: #1380DE;clip-path: polygon(65% 100%, 0 0, 35% 0, 100% 100%);position: relative;left: -5px;"></div>
	   </div>`
    );
  });
```

## uniapp自定义导航栏的底部高度问题

**问题描述：**

uniapp自定义导航栏之后，底部的导航栏会覆盖页面一部分内容

**解决方法：**

1.在页面底部添加一个节点，设置一定的高度

2.给页面最大的节点添加样式

```css
padding-bottom: calc(env(safe-area-inset-bottom));
```

## uniapp渲染富文本时，图片样式h5与小程序不兼容

**问题描述：**

渲染html片段，直接给img标签加内联样式，在小程序端不生效

**解决方法：**

先清除小程序给图片默认加的样式，再添加内联样式

```javascript
const formRichText = (html) => {
  // 将图片原先样式清除（小程序样式兼容）
  let newContent = html.replace(/(style="(.*?)")|(width="(.*?)")|(height="(.*?)")/gi, '');
  newContent = newContent.replace(/\<img/gi, '<img style="width: 100%;object-fit: cover; display: table-cell;vertical-align: middle;"');

  return newContent;
};
```

