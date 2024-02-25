# 开发常用样式

## 宽高设置

![image-20231228090418331](https://tiny-blog.oss-cn-guangzhou.aliyuncs.com/blog/202312280904356.png)

### padding

**padding，向内延伸，假设盒子宽度为1120px，高度300px，设置四个方向的padding为30px，则实际内容宽度和高度为1060px和240px。**

```css
.box {
  /* 第一个参数为垂直方向，第二个参数为水平方向 */
  padding: 20px 40px;
  /* top right bottom left */
  padding: 10px 20px 30px 40px;
  padding-left: 1px;
  padding-right: 1px;
  padding-top: 1px;
  padding-bottom: 1px;
  /* auto代表剩余宽高平分为padding值 */
  padding: auto;
}
```
### margin

**margin，向外延伸，假设盒子宽度为1120px，高度300px，设置四个方向的margin为30px，则盒子的内容宽度高度不变，其他盒子与该盒子的距离增加30px**

## 鼠标样式

```css
.box {
  cursor: pointer;
}
```

## 文本溢出显示省略号

```css
white-space: nowrap; /* 强制文本不换行 */
overflow: hidden; /* 隐藏溢出内容 */
text-overflow: ellipsis; /* 对溢出的文本用 ellipsis 省略号代替。 */
```

```css
display: -webkit-box; /* 将对象作为弹性伸缩盒子模型显示 */
-webkit-box-orient: vertical /* 使文本垂直（纵向）排列每一行，也就是文字是从左到右，从上到下 */
/* 限制文本的行数 or 列数，取决于-webkit-box-orient的属性值 */
-webkit-line-clamp: 2; 
overflow: hidden; /* 隐藏溢出内容 */
text-overflow: ellipsis; /* 对溢出的文本用 ellipsis 省略号代替。 */
```

```css
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
```

## 文字方向

**垂直（从左到右）**

```css
writing-mode: vertical-lr;
```

**垂直（从右到左）**

```css
writing-mode: vertical-rl;
```

## elementPlus轮播图抖动问题

**给轮播图设置一个最小高度，避免每次轮播都计算高度**

## z-index

**设置z-index，可以让设置值大的盒子在最上层**

## 盒子固定在底部

```css
position: fixed;
bottom: 0;
width: 100%;
```

**需要设置宽度**

## 圆角边框颜色渐变

```css
border: 2rpx solid transparent;
border-radius: 10rpx;
background-clip: padding-box, border-box;
background-origin: padding-box, border-box;
background-image: linear-gradient(to bottom, #fff, #fff), linear-gradient(to bottom, #76b5ec, #1380de);
```

## 绝对定位

```css
position: relative;
/* 距离顶部 */
top: 10px;
/* 距离左边 */
left: 10px;
/* 距离右边 */
right: 10px;
/* 距离底部 */
bottom: 10px
```

## 梯形

**左上为坐标系原点**

```css
/* 左下，左上，右上，右下 */
clip-path: polygon(10% 100%, 0 0, 100% 0, 90% 100%);
```

## flex布局下左侧宽度被挤压

**给被挤压的div设置以下属性**

```css
flex-shrink: 0;
```

## nth-child

**父元素:nth-child**

```css
nth-child(even); // 选择偶数元素
nth-child(odd); //选择奇数元素
```

## 修改滚动条样式

**未兼容全部浏览器**

```css
.box::-webkit-scrollbar {
  width: 4px;
  height: 4px;
}

.box::-webkit-scrollbar-thumb {
  border-radius: 10px;
  -webkit-box-shadow: inset 0 0 5px rgba(0, 0, 0, 0.2);
  background: rgba(0, 0, 0, 0.2);
}

.box::-webkit-scrollbar-track {
  -webkit-box-shadow: inset 0 0 5px rgba(0, 0, 0, 0.2);
  border-radius: 0;
  background: rgba(0, 0, 0, 0.1);
}
```

