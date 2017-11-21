## 提高CSS开发技巧

## 前言

说到css开发技巧，其实我前面所有关于css的文章，都是[css](http://www.haorooms.com/tag/css)的一些小的技巧！感兴趣的可以查看：<http://www.haorooms.com/tag/css> 还有值得一提的是，我之前关于css，分别写了[css常用效果总结](http://www.haorooms.com/post/css_common) ，还有一些 [css的不常用效果总结](http://www.haorooms.com/post/css_notuse_common)，其实呢，这些都是相对的。有些效果我们在开发中不常用，但是有的项目也可能会用到！例如，最近做了一个小的项目，用到了css的resize属性。其实我本来不想用这个属性的，因为这个属性不兼容IE浏览器，但是呢，我这个项目却恰恰不需要兼容IE，是内部系统！那我先以resize属性介绍，作为本文的开头吧，虽然resize应用算不上css开发技巧！

## 一、resize实现图片对比

resize的语法如下：

```css
resize：none | both | horizontal | vertical
```

案例效果如下图 **(鼠标移到左下角白色区域，往右侧拖动，实现图片对比效果)**：

http://sandbox.runjs.cn/show/myr3ogyf

我应用到了resize的如下代码：

```css
resize: horizontal;
```

可以水平拉伸！

## 二、:not()的应用技巧

我们平时在书写导航栏分割线的时候，最后一个标签是没有分割线的，我们一般的写法如下：

```css
/* 先给所有添加右侧边框 */
.nav li {
  border-right: 1px solid #666;
}
/* 再去除最后一个边框 */
.nav li:last-child {
  border-right: none;
}
```

运用:not()之后如下书写：

```css
.nav li:not(:last-child) {
  border-right: 1px solid #666;
}
```

还可以用我们之前的~[波浪选择器](http://www.haorooms.com/post/css_selectelement)来实现，不明白的可以点击进入，查看第8条！

```css
.nav li:first-child ~ li {
  border-left: 1px solid #666;
}
```

我们在用逗号分隔的列表，最后一个让他没有逗号，写法如下：

```css
ul > li:not(:last-child)::after {
  content: ",";
}
```

not的应用，让我们方便了不少，节省了一些代码！

## 三、任意元素垂直居中

关于css垂直居中，我之前写过几篇文章：[css固定宽高DIV内部元素垂直居中的方法](http://www.haorooms.com/post/div_guding_inner_center) 和 [css的div垂直居中的方法](http://www.haorooms.com/post/css_div_juzhong) ，今天我们在body中，初始化定义一下，就可以让任意元素垂直居中，代码如下：

```css
html, body {
  height: 100%;
  margin: 0;
}

body {
  -webkit-align-items: center;  
  -ms-flex-align: center;  
  align-items: center;
  display: -webkit-flex;
  display: flex;
}
```

当然，这个有一定的兼容问题！不过现代浏览器是没有问题的！

## 四、表格单元格等宽

用如下代码可以让表格单元格等宽

```css
.haorooms{
  table-layout: fixed;
}
```

## 五、使用Flexbox摆脱各种Margin Hacks

实现侧栏时，我们不再需要各种nth-、first-和last-child等设置margin，可以使用Flexbox轻松实现均匀分布！代码如下：

```css
.list {
  display: flex;
  justify-content: space-between;
}

.list .person {
  flex-basis: 23%;
}
```

## 六、给空连接使用属性选择符

这个我上一篇文章应用过了，就是使用before或者after的[content的attr属性](http://www.haorooms.com/post/content_attr)！

具体可以看：<http://www.haorooms.com/post/content_attr>

我们还可以给空a标签添加属性，代码如下：

```css
a[href^="http"]:empty::before {
  content: attr(href);
}
```

## 七、初始化box-sizing

从html中继承box-sizing属性，这样的话，后期维护比较方便。

```css
html {
  box-sizing: border-box;
}

*, *:before, *:after {
  box-sizing: inherit;
}
```

## 八、在nth-child中使用负数

nth-child中使用负数，可以选择小于等于某个数的值，例如：

```css
li:nth-child(-n+4){
  background:red
}
```

小于等于4的li，显示为红色！

还可以如下应用：

```css
li {
  display: none;
}

li:nth-child(-n+3) {
  display: block;
}
```

上面代码的含义是，我们让前三个li显示（小于等于3的）,其他的li都隐藏！

关于nth-child的应用，我之前也写过文章，具体请看：<http://www.haorooms.com/post/css3_nth-child>

## 九、文本显示优化

```css
html {
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  text-rendering: optimizeLegibility;
}
```

上面代码可以让字体在我们的设备中最优显示！

## 十、border的应用技巧！

关于border，我前面的文章已经介绍过其对于[对话框](http://www.haorooms.com/post/css_dhk)的书写。<http://www.haorooms.com/post/css_dhk>

border的应用还是蛮广泛的！我之前在慕课网的课程 html5左侧导航，讲了[三道杠](http://www.haorooms.com/post/box_shadow_css)的书写！，是运用了box-shadow，关于文章，具体请看：<http://www.haorooms.com/post/box_shadow_css>

但是呢，这个是css3的属性，今天给大家讲运用border书写三道杠，兼容性很好！代码如下：

```css
width:40px;height:7px;
color: #999;
border-top:18px  double;
border-bottom: 6px solid;
```

运用border的double属性，可以轻松绘制三道杠，兼容性很好！并且，大家注意的是：border-color可以继承color，我们只要修改color的值，就可以修改border-color的值！

## 十一、vertical-align 属性

vertical-align 只在行内元素，或者inline、inline-block等中才起作用。当我们在某个div中使用垂直居中是不管用的，我之前的文章写了利用vertical-align，[垂直居中](http://www.haorooms.com/post/div_guding_inner_center)的办法，具体请看：<http://www.haorooms.com/post/div_guding_inner_center>

除此之外，vertical-align 还支持数值和百分比！

我们可以如下写：

```css
.haorooms{vertical-align:-2px;}
.haorooms{vertical-align:-10%;}
```

这个负值和 margin-bottom类似，但是呢，vertical-align可以将父级元素撑大！

## 十二、margin重叠解决方案列举

> 1、父级元素bfc ，不懂bfc的情看我之前的文章：<http://www.haorooms.com/post/css_BFC_bgdiv>
>
> 2、父级元素给一个padding
>
> 3、父级元素给一个border
>
> 4、子元素前面加任意一个空的内联元素，（例如：span、nbsp等等）

## 十三、父元素font-size:0的作用

**display：inline-block的元素之间会有一个字符的间隙，这个间隙导致了最后一个会掉下来。**解决方案一般有如下几种：

1、给父元素设置font-size：0px；

2、取消掉换行符，如这样：

```html
<span>aaaa</span><span>aaaa</span><span>aaaa</span>
```

连续。

或者如下：

```html
<div class="space">
    <a href="##">惆怅</a><!--
    --><a href="##">淡定</a><!--
    --><a href="##">热血</a>
</div>

<div class="space">
    <a href="##">惆怅</a
    ><a href="##">淡定</a
    ><a href="##">热血</a>
</div>
```

但是这种方式不推荐

3、使用margin负值。

4、使用浮动。

5、另外还有使用letter-spacing、word-spacing等方法。

当然最好的解决方案就是设置font-size:0

### 父元素 font-size:0 例子：

html:

```html
<div class="box">
  <div>1</div>
  <div>2</div>
  <div>3</div>
</div>
```

css:

```css
.box{
  width: 90px;
  height: 60px;
  border: 1px solid #ccc;
}
.box div{
  display: inline-block;
  box-sizing: border-box;
  font-size: 14px;
  width: 30px;
  border: 1px solid ;
}
```

理论上box下面的三个div都是30px，刚好在一行显示，但是实际效果是这样：

![enter image description here](http://sandbox.runjs.cn/uploads/rs/216/0y89gzo2/1098079-20170209145.png)

这就是上文说到的原因，我们在box下添加font-size:0;再看看效果

![enter image description here](http://sandbox.runjs.cn/uploads/rs/216/0y89gzo2/111098079-201702091.png)

## 十四、padding实现比例固定图片自适应

对于padding属性而言，任意方向的百分比padding都相对于宽度计算可以让我们轻松实现固定比例的块级容器。 例如：

```css
div { padding: 50%; }
div { padding: 100% 0 0; }
div { padding-bottom: 100%; }
```

上面div元素尺寸就是一个宽高1:1的正方形，无论其父容器宽度是多少，这个div元素总能保持比例不变。 这样我们可以实现固定宽高图片自适应布局。相比图片直接设置100% 的好处就是，这样布局不会因为图片加载，高度不定导致，文章出现弹跳效果。

之前写的一篇文章，[判断页面中所有图片加载完成](http://www.haorooms.com/post/jquery_deferred_img)，目的就是获取文章图片加载完成，页面高度。使用了padding之后，就可以避免这种情况的产生。

**套路如下：** html结构

```html
<div class="banner">
  <img src="banner.jpg">
</div>
```

css如下

```css
.banner {
    padding: 15.15% 0 0;
    position: relative;
}
.banner > img {
    position: absolute;
    width: 100%; 
    height: 100%;
    left: 0; 
    top: 0;
}
```

> 注：
>
> 1、图片宽度是100%容器的，padding的15.5%其实就是图片的高宽比例。
>
> 2、图片宽度50%容器宽度，图片高宽比4:3，我们也可以这么写
>
> ```
> .img-box {
>     padding: 0 50% 66.66% 0;
> }
> ```
>
> 3、如果没有text-align属性干扰，img的position，及left和top可以不用指定