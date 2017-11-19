## CSS固定宽高div内部元素垂直居中的方法

作为网页[前端](http://www.haorooms.com/)，经常会遇到垂直居中的问题，对于这个，我前面写过一篇文章，是关于[div垂直居中](http://www.haorooms.com/post/css_div_juzhong)的，不过这个垂直居中是div相对于整个网页而言的。在这篇文章中，我分析了固定高宽的div和不固定高度的div在网页中垂直居中的方法。具体大家可以看：<http://www.haorooms.com/post/css_div_juzhong>

今天，我同样说一个div垂直居中的方法，但是不同的是，我说的是div内部元素相对于div垂直居中的方法。

## 应用案例

案例是这样的，一个外层div，高宽是固定的，但是里面内容不是固定的。很多朋友的做法是头部加一个padding或者margin，这样，里面内容显得貌似是居中了，但是假如内容变化，这样头部的固定padding或者margin，始终不变。造成了垂直方向不会居中！

我们知道，假如下面一个div

```html
<div class="outer">
  <div class="inner">haorooms内部内容</div>
</div>
```

样式是这样的

```css
.outer{
  text-align:center;
  vertical-align: middle;
  width:200px;
  height:350px;
}
```

vertical-align:middle是不管用的,很多朋友就在.inner上面做文章了，和我上面说的，加margin等等！那对于这种情况，有没有更好的解决方案呢？

## 解决方法

思路：加一个cssHack，设置cssHack的line-height等于外层div的高度，就可以使用vertical-align:middle了！

div如下：

```html
<div class="outer">
    <div class="inner">haorooms内部内容</div>
    <div class="v">cssHack</div>
</div>
```

样式如下：

```css
* {
    margin: 0;
    padding: 0;
}
.outer {
    background-color: #ccc;
    font-size: 24px;
    height: 350px;
    text-align: center;
    overflow: hidden;
    width: 280px;
}
.outer  .inner,
.outer  .v {
    display: inline-block;
    zoom: 1;*display: inline; /* 用于触发支持IE67 inline-block */
}
.outer  .inner {            
    line-height: 1.8;
    padding: 0 4px 0 5px;
    vertical-align: middle;
    width: 262px;           
}
.outer  .v {
    line-height: 350px;
    text-indent:-9999px;
    width: 1px;         
}
```

这样就实现了div内部的垂直居中了！