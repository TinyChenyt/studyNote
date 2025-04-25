# 插件使用-html2canvas

**将页面渲染为图片**
[官网](https://html2canvas.hertzen.com/)

## CDN使用
推荐使用html2canvas.js，并且建议将文件下载到本地引入，方便修改插件源码。

如果不需要修改插件的源码，可以使用html2canvas.min.js，打包之后的js文件所需内存更小。
```html
<script src="https://html2canvas.hertzen.com/dist/html2canvas.js"></script>
<!-- 或者 -->
<script src="https://html2canvas.hertzen.com/dist/html2canvas.min.js"></script>
```

## 示例
```js
const buildCanvas = () => {
    // 需要渲染成图片的节点
    const canvasDom = document.getElementById('canvasDom')
    html2canvas(canvasDom, { useCORS: true, allowTaint: true }).them((canvas) => {
        // 支持png、jbpg等格式
        const base64 = canvas.toDataURL('image/png');
    });
}
```

**注意：html2canvas不支持样式object- 系列的样式，常用的比如object-fit: cover;**

## 兼容object-fit
我们可以通过修改html2canvas的源码来实现兼容object-fit

找到`CanvasRenderer.prototype.renderReplacedElement`方法，将改方法替换为
```js
CanvasRenderer.prototype.renderReplacedElement = function (container, curves, image) {
    // 上面注释的原来的代码，下面是我们自己修改后的
    // Start Custom Code
    if (image && container.intrinsicWidth > 0 && container.intrinsicHeight > 0) {
      var box = contentBox(container);
      var path = calculatePaddingBoxPath(curves);
      this.path(path);
      this.ctx.save();
      this.ctx.clip();
      let newWidth;
      let newHeight;
      let newX = box.left;
      let newY = box.top;
      if(container.intrinsicWidth / box.width < container.intrinsicHeight / box.height) {
        newWidth = box.width;
        newHeight = container.intrinsicHeight * (box.width / container.intrinsicWidth);
        newY = box.top + (box.height - newHeight) / 2;
      } else {
        newWidth = container.intrinsicWidth * (box.height / container.intrinsicHeight);
        newHeight = box.height;
        newX = box.left + (box.width - newWidth) / 2;
      }
      this.ctx.drawImage(image, 0, 0, container.intrinsicWidth, container.intrinsicHeight, newX, newY, newWidth,newHeight);
      this.ctx.restore();
    }
    // End Custom Code
};
```
**该修改只能兼容object-fit, 对于其他object-系列样式，如object-position还是不支持，可以更换为其他样式**