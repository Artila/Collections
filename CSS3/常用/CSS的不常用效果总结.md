## CSS的不常用效果总结

## 前言

css的不常用效果总结，今天分享一下css的一些不常用效果，有些效果大家可能不常用，因此可能有些朋友都没有用过，今天带领大家一起过一下这些不常用效果。关于css的一些常用的效果，我之前也总结了，请看：<http://www.haorooms.com/post/css_common>

## 不常用效果总结如下几个，后面慢慢再补充

### 1、box-reflect文字倒影效果

效果演示如下：<http://sandbox.runjs.cn/show/ljwhvtf4>

属性参数介绍：

> **box-reflect**：[ above | below | right | left ]? <length>? <image>?

代码使用如下：

```css
.reflect{
    width:100%;
    margin:0 auto;
    -webkit-box-reflect:below 0 -webkit-linear-gradient(transparent,transparent 50%,rgba(255,255,255,.3));
    font:bold 50px/1.231 georgia,sans-serif;    
}
```

### 2、背景剪辑 background-clip

background用的很多，前面也有很多文章介绍，包括多背景设置等等<http://www.haorooms.com/post/css3_bg_multi> ,今天主要说下clip这个属性，这个属性的主要功能是背景裁剪，我们在ps中可能经常用到。具体语法如下：

```css
background-clip：<box> [ , <box> ]*
<box> = border-box | padding-box | content-box | text
默认值：border-box
```

用的相对较多的是content-box和text,text可以做一些背景的文字。演示如下：<http://sandbox.runjs.cn/show/oil6be3b>

核心代码：

```css
.text p{
  width:auto;
  height:auto;
  background-repeat:repeat;
  -webkit-background-clip:text;
  -webkit-text-fill-color:transparent;
  font-weight:bold;
  font-size:120px;
}
```

### 3、text-fill-color 设置渐变字体

配合上面的clip，演示如下：<http://sandbox.runjs.cn/show/jzicv7pv>

核心代码如下：

```css
background:-webkit-linear-gradient(top,#eee,#aaa 50%,#333 51%,#000);
-webkit-background-clip:text;
-webkit-text-fill-color:transparent;
```

### 4、direction 字体排版方向

> 语法：direction：ltr | rtl   默认值：ltr

```
tr：文本流从左到右。
rtl：文本流从右到左。
```

文字正排和倒排，一般不常用！

## 5、font-stretch

设置或检索对象中的文字是否横向拉伸变形。文字的拉伸是相对于浏览器显示的字体的正常宽度。

语法：

```
font-stretch：ultra-condensed | extra-condensed | condensed | semi-condensed | normal | semi-expanded | expanded | extra-expanded | ultra-expanded
默认值：normal
```

取值：

```
ultra-condensed：比正常文字宽度窄4个基数。
extra-condensed：比正常文字宽度窄3个基数。
condensed：比正常文字宽度窄2个基数。
semi-condensed：比正常文字宽度窄1个基数。
normal：正常文字宽度
semi-expanded：比正常文字宽度宽1个基数。
expanded：比正常文字宽度宽2个基数。
extra-expanded：比正常文字宽度宽3个基数。
ultra-expanded：比正常文字宽度宽4个基数。
```

### 6、text-stroke

文字描边。

```
text-stroke：[ text-stroke-width ] || [ text-stroke-color ]
```

默认值：看每个独立属性

取值：

```
[ text-stroke-width ]：设置或检索对象中的文字的描边厚度
[ text-stroke-color ]：设置或检索对象中的文字的描边颜色
```

代码案例：

```
.stroke p{
    margin:50px auto 100px;font-size:100px;
    -webkit-text-stroke:1px #f00;
}
```

### 7、tab-size

设置对象中的制表符的长度。

语法：

word-wrap： | 默认值：8

```
pre{background:#eee;-moz-tab-size:4;-o-tab-size:4;}
```

### 8、content

用来和:after及:before伪元素一起使用，在对象前或后显示内容。

### 9、quotes

使用书名号等引用。

### 10、颜色翻转

```
.normal {
    filter: invert(0%);
}

.inverted {
    filter: invert(100%);
}
```

### 11、writing-mode

writing-mode属性很早就有了，只不过最早是IE提出来的。现在基本上大多数浏览器都支持了！

语法：

```
/* 关键字值 */
writing-mode: horizontal-tb;    /* 默认值 */
writing-mode: vertical-rl;
writing-mode: vertical-lr;

/* 全局值-关键字inherit IE8+，initial和unset IE13才支持 */
writing-mode: inherit;
writing-mode: initial;
writing-mode: unset;
```

一般用于文字的竖排版：

例如，css如下写法：

```
.verticle-mode {
    writing-mode: tb-rl;
    -webkit-writing-mode: vertical-rl;      
    writing-mode: vertical-rl;
}
/* IE7比较弱，需要做点额外的动作 */
.verticle-mode {
    *width: 120px;
}
.verticle-mode h4,
.verticle-mode p {
    *display: inline;
    *writing-mode: tb-rl;
}
.verticle-mode h4 {
    *float:right;
}
```

html如下下：

```
<div class="verticle-mode">
    <h4>咏柳</h4>
    <p>碧玉妆成一树高，<br>万条垂下绿丝绦。<br>不知细叶谁裁出，<br>二月春风似剪刀。</p>
</div>
```

我们就可以看到古诗文的竖排了！

### 12、 pointer-event

字面理解是点击鼠标事件，值分别是auto和none,当使用pointer-events:none,表示它将捕获不到任何点击。假如一个a标签，我们不想让其点击，可以使用pointer-event：none

演示如下：

[我有链接，但是点击不到我](http://www.haorooms.com/)

上面的代码如下：

```html
<div style="pointer-events: none;">
	<a href="http://www.haorooms.com/">我有链接，但是点击不到我</a>
</div>
```

虽然有a标签，但是我们点击这个标签是没有效果的！

上面的也可以这么写，点击也是没有效果的！

```html
<div>
	<a href="http://www.haorooms.com/" style="pointer-events: none;">我有链接，但是点击不到我</a>
</div>
```

大家可以测试看一下哦！