# ���ʹ��-html2canvas

**��ҳ����ȾΪͼƬ**
[����](https://html2canvas.hertzen.com/)

## CDNʹ��
�Ƽ�ʹ��html2canvas.js�����ҽ��齫�ļ����ص��������룬�����޸Ĳ��Դ�롣

�������Ҫ�޸Ĳ����Դ�룬����ʹ��html2canvas.min.js�����֮���js�ļ������ڴ��С��
```html
<script src="https://html2canvas.hertzen.com/dist/html2canvas.js"></script>
<!-- ���� -->
<script src="https://html2canvas.hertzen.com/dist/html2canvas.min.js"></script>
```

## ʾ��
```js
const buildCanvas = () => {
    // ��Ҫ��Ⱦ��ͼƬ�Ľڵ�
    const canvasDom = document.getElementById('canvasDom')
    html2canvas(canvasDom, { useCORS: true, allowTaint: true }).them((canvas) => {
        // ֧��png��jbpg�ȸ�ʽ
        const base64 = canvas.toDataURL('image/png');
    });
}
```

**ע�⣺html2canvas��֧����ʽobject- ϵ�е���ʽ�����õı���object-fit: cover;**

## ����object-fit
���ǿ���ͨ���޸�html2canvas��Դ����ʵ�ּ���object-fit

�ҵ�`CanvasRenderer.prototype.renderReplacedElement`���������ķ����滻Ϊ
```js
CanvasRenderer.prototype.renderReplacedElement = function (container, curves, image) {
    // ����ע�͵�ԭ���Ĵ��룬�����������Լ��޸ĺ��
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
**���޸�ֻ�ܼ���object-fit, ��������object-ϵ����ʽ����object-position���ǲ�֧�֣����Ը���Ϊ������ʽ**