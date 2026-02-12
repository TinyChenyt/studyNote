## 插件使用-spritespin

### 参数说明:

#### **animate**

------

是否自动播放动画。

**animate信息**

------

类型：Boolean	默认：false	可选值：true/false

**使用方法：**

------

```js
$(".spritespin").spritespin({
	animate: true,
})
```



#### frame

------

初始时显示第几张图。默认从第0张图开始。

**frame信息**

------

类型： number	默认：0

**使用方法：**

------

```js
$(".spritespin").spritespin({
	frame: 0,
})
```



#### frames

------

总共有几张图。

**frames信息**

------

类型：number

**使用方法：**

```js
$(".spritespin").spritespin({
	frames: 80,
})
```



#### frameTime

------

每次图片旋转更新的时间（毫秒）。

**frameTime信息**

------

类型：number	默认：30

**使用方法：**

```js
$(".spritespin").spritespin({
	frameTime: 80,
})
```



#### loop

------

是否循环播放。

**loop信息**

------

类型：Boolean	默认：true

**使用方法：**

```js
$(".spritespin").spritespin({
	loop: true,
})
```



#### reverse

------

旋转方向默认（正向）是从第0张图到最后一张图，reverse可以反向旋转。

**reverse信息**

------

类型：Boolean	默认：false

**使用方法：**

```js
$(".spritespin").spritespin({
	reverse: true,
})
```



#### stopFrame

------

当loop为false时生效，表示最后停在第几帧图上。

**stopFrame信息**

------

类型：number

**使用方法：**

```js
$(".spritespin").spritespin({
	stopFrame: 80,
})
```



#### retainAnimate

------

当animate为true时生效，保留动画的最后一帧（在手动旋转之后可以继续自动旋转）。

**retainAnimate信息**

------

类型：Boolean	默认值：false

**使用方法：**

```js
$(".spritespin").spritespin({
	retainAnimate: true,
})
```

