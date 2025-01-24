# HTML基础-标签

## head标签
head标签是html文档的头部标签，用来定义文档的元信息，比如标题、关键词、作者、描述等。

## meta标签
meta标签位于head标签内

## a标签
a标签是超链接标签，用来链接到其他网页。也可以用作按钮，实现点击调用方法
```html
<a href="http://www.baidu.com">百度一下</a>
<a href="javascript:void(0)" onclick="alert('点击了')">点击我</a>
```

## img标签
img标签是图片标签，用来显示图片。
```html
<img src="https://tiny-blog.oss-cn-guangzhou.aliyuncs.com/blog/20240906143255.png" alt="百度一下">
<img src="./img/logo.png" alt="logo">
```

## button标签
button标签是按钮标签，用来实现点击调用方法。
```html
<button onclick="alert('点击了')">点击我</button>
<button onclick="window.open('https://www.baidu.com')">百度一下</button>
```

## p标签
p标签是段落标签，用来定义段落。对于大段的文本内容，可以使用p标签
```html
<p>文本文本文本文本</p>
```

## i标签
i标签是斜体标签，用来定义斜体文本。
```html
<i>斜体文本</i>
```
