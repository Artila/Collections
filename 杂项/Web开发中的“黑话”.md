## Web开发中的“黑话”

https://segmentfault.com/a/1190000002593432

## 前言

在Web开发这个日新月异的时代，总是需要阅读一些最新的英文技术博客来跟上技术的发展的潮流。而有时候会遇到一些比较高频的“黑话”，在社区里面可能已经是人人皆知的“共同语言”，而你接触的少就偏偏看不懂。就像现在几乎所有中国人都知道duang是什么东西，但是一个刚学中文的外国人看到以后可能就一头雾水。

![img](https://segmentfault.com/image?src=https://raw.githubusercontent.com/livoras/blog-images/master/duang.jpg&objectId=1190000002593432&token=013f8900c2d1a361c022a83453b16f72)

黑话也是要学习的，本文收集各种Web开发的黑话。这里先介绍两个。

## Polyfill

`Polyfill`或者`Polyfiller`，是英国Web开发者 [Remy Sharp](https://remysharp.com/) 在咖啡店蹲坑的时候拍脑袋造出来的。当时他想用一个词来形容"用JavaScript（或者Flash之类的什么鬼）来实现一些浏览器不支持的原生API"。`Shim`这个已经有的词汇第一时间出现在他的脑海里。但是他回头想了一下`Shim`一般有自己的API，而不是单纯实现原生不支持的API。苦思冥想一直想不到合适的单词，于是他一怒之下造了一个单词`Polyfill`。除了他自己用这个词以外，他还给其他开发者用。随着他在各种Web会议演讲和他写的书《Introducing HTML5》中频繁提到这个词，大家用了都觉得很好，就一起来用。

`Polyfill`的准确意思为：**用于实现浏览器并不支持的原生API的代码。**

例如，`querySelectorAll`是很多现代浏览器都支持的原生Web API，但是有些古老的浏览器并不支持，那么假设有人写了库，只要用了这个库， 你就可以在古老的浏览器里面使用`document.querySelectorAll`，使用方法跟现代浏览器原生API无异。那么这个库就可以称为`Polyfill`或者`Polyfiller`。

好，那么问题就来了。jQuery是不是一个`Polyfill`?答案是No。因为它并不是实现一些标准的原生API，而是封装了自己API。一个`Polyfill`是抹平新老浏览器 **标准原生API** 之间的差距的一种封装，而不是实现自己的API。

已有的一些`Polyfill`，如 [Polymer](https://www.polymer-project.org/0.5/docs/start/platform.html) 是让旧的浏览器也能用上 HTML5 Web Component 的一个`Polyfill`。[FlashCanvas](http://flashcanvas.net/)是用Flash实现的可以让不支持Canvas API的浏览器也能用上Canvas的`Polyfill`。

这里有一堆`Polyfills`，有兴趣可以把玩一下：[HTML5 Cross Browser Polyfills](https://github.com/Modernizr/Modernizr/wiki/HTML5-Cross-browser-Polyfills)

## Vanilla JavaScript

`Vailla JavaScript`是目前世界上跨平台兼容性最好、最小、最快的JavaScript框架。它的官网为：<http://vanilla-js.com/>

![img](https://segmentfault.com/image?src=https://raw.githubusercontent.com/livoras/blog-images/master/vanilla.png&objectId=1190000002593432&token=a58606f2685549671aa5bddd02173ba9)

在官网上，你可以尝试可以选择不同的功能模块自定义进行下载。但是不管你怎么选怎么下，下下来的js文件都是空的。好吧，这个网站本身就是个玩笑。`Vanilla JavaScript`指的就是纯原生的JavaScript，所以不需要任何代码。

在基佬百科上`Vanilla`的意思为：

> Computer software, and sometimes also other computing-related systems like computer hardware or algorithms, is called vanilla when not customized from its original form...

在计算机软件领域中，如果你对原生系统**没有做任何定制性的修改**，就是`Vanilla`。你把`Vailla`看成是`Pure`或者`Plain`的意思都是可以的。`Vanilla JavaScript`就是`Pure JavaScript`的意思。

例如，我在巨硬官网下载了官方的xp系统镜像，这个系统就可以称为是vanilla的。但是如果你在国内某些网站下载了某些定制的盗版镜像，那就不是vanilla了。