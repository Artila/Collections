## jQuery编程的标准写法和最佳实践

## jQuery的加载

1. 我们经常用CDN来加载网页，我之前的文章中也多次提及，[点击查看](http://www.sitepoint.com/7-reasons-to-use-a-cdn/)使用CDN的好处，

```javascript
<script type="text/javascript" src="//ajax.googleapis.com/ajax/libs/jquery/2.1.1/jquery.min.js"></script>

<script>
  window.jQuery || document.write('<script src="js/jquery-2.1.1.min.js" type="text/javascript"><\/script>')
</script>
```

关于CDN加载，还可以查看我之前的一篇文章[CDN公共库](http://www.haorooms.com/post/cdn_all)：<http://www.haorooms.com/post/cdn_all>

2. 最好在本地备份一个相同版本的代码，以防万一，不能链接远程服务，[详情见此](http://css-tricks.com/snippets/jquery/fallback-for-cdn-hosted-jquery/)。
3. 使用裸协议的URL（去掉http:或者https:），如上面代码展示的那样，我在之前的文章中也提到过，加载CDN可以省掉http，见文章：<http://www.haorooms.com/post/web_qd_html_leng>
4. 如果可能，尽量将你的JavaScript和jQuery代码放到页面底部。我之前写的一篇关于js加载顺序的问题，提到过[js性能优化](http://www.haorooms.com/post/web_xnyh_jscss)，具体请看：<http://www.haorooms.com/post/web_xnyh_jscss>
5. 该使用哪个版本？

> 如果你想兼容 IE678 请不要用2.x的版本
>
> 针对极少数不用考虑兼容性问题的，极力推荐使用最新版本的jQuery
>
> 当从CDN服务器加载jQuery时，最好把版本写全（比如 1.11.0 而不是 1.11 或者直接写个1）
>
> 不要重复加载和多次加载
>
> 不要从jquery CDN中加载 jquery-latest.js，[具体请看](http://blog.jquery.com/2014/07/03/dont-use-jquery-latest-js/)

6. 如果你同时还使用了其他JS框架诸如Prototype,  MooTools,  Zepto 等等，这些框架中，有的也用了`$`符号，所以你就不要再用`$`来进行 jQuery 编码了，而请用`jQuery`代替。并且调用`$.noConflict()` 保证不会有冲突出现。
7. 要检测浏览器对一些新特性是否支持，请用[Modernizr](http://modernizr.com/)。



## 关于变量

1. jQuery 类型的变量最好加个$前缀。
2. 时常将 jQuery 选择器返回的内容存进变量以便重用

```javascript
var $myDiv = $("#myDiv");
$myDiv.click(function(){...});
```

3. 使用 [camel case](http://en.wikipedia.org/wiki/CamelCase)命名



## 关于选择器

1. 尽量ID选择器。实际运用的是js的`document.getElementById()`，所以速度较其他选择器快。
2. 使用类选择器时不要指定元素的类型。请看[性能比较](http://jsperf.com/jqeury-selector-test)

```javascript
var $products = $("div.products"); // 慢
var $products = $(".products"); // 快
```

3. ID父亲容器下面查找子元素请用.find()方法。这样做快的原因是通过id选择元素不会使用Sizzle引擎。[详情看这里](http://learn.jquery.com/performance/optimize-selectors/)

```javascript
// BAD, a nested query for Sizzle selector engine
var $productIds = $("#products div.id");

// GOOD, #products is already selected by document.getElementById() so only div.id needs to go through Sizzle selector engine
var $productIds = $("#products").find("div.id");
```

4. 多级查找中，右边尽量指定得详细点而左边则尽量简单点。[了解更多](http://learn.jquery.com/performance/optimize-selectors/)

```javascript
// 丑陋
$("div.data .gonzalez");

// 优化后
$(".data td.gonzalez");
```

5. 避免冗余。[详情](http://learn.jquery.com/performance/optimize-selectors/)或者查看[性能比较](http://jsperf.com/avoid-excessive-specificity)

```javascript
$(".data table.attendees td.gonzalez");

// 好的方式：去掉了中间的冗余
$(".data td.gonzalez");
```

6. 指定选择的上下文。

```javascript
// 劣质的代码：因为需要遍历整个DOM来找到.class
$('.class');

// 高品代码：因为只需在指定容器范围内进行查找
$('.class', '#class-container');
```

7. 避免使用万能选择器。查看[具体阐释](http://learn.jquery.com/performance/optimize-selectors/)

```javascript
$('div.container > *'); // 差
$('div.container').children(); // 棒
```

8. 警惕隐式的万能选择器。省略的情况下其实使用的就是*号通配符。[更多信息](http://learn.jquery.com/performance/optimize-selectors/)

```javascript
$('div.someclass :radio'); // 差
$('div.someclass input:radio'); // 棒
```

9. ID已经表示唯一了，背后使用的是`document.getElementById()`，所以不要和其他选择器混淆了。

```javascript
$('#outer #inner'); // 脏
$('div#inner'); // 乱
$('.outer-container #inner'); // 差
$('#inner'); // 干净利落，后台只需调用document.getElementById()
```



## DOM操作

1. 操作任何元素前先将其从文档卸载，然后再贴回去。[请看](http://learn.jquery.com/performance/detach-elements-before-work-with-them/)

```javascript
var $myList = $("#list-container > ul").detach(); 
// detach() 方法移除被选元素，包括所有文本和子节点。这个方法会保留 jQuery 对象中的匹配的元素，因而可以在将来再使用这些匹配的元素。
//...a lot of complicated things on $myList
$myList.appendTo("#list-container");
```

2. 使用连接字符串或数组join()，然后再append()。[请看](http://learn.jquery.com/performance/append-outside-loop/)

性能比较: <http://jsperf.com/jquery-append-vs-string-concat>

```javascript
// 不好
var $myList = $("#list");
for(var i = 0; i < 10000; i++){
    $myList.append("<li>"+i+"</li>");
}

// GOOD
var $myList = $("#list");
var list = "";
for(var i = 0; i < 10000; i++){
    list += "<li>"+i+"</li>";
}
$myList.html(list);

// EVEN FASTER
var array = []; 
for(var i = 0; i < 10000; i++){
    array[i] = "<li>"+i+"</li>"; 
}
$myList.html(array.join(''));
```

3. 不要用缺失的元素，[具体请看](http://learn.jquery.com/performance/dont-act-on-absent-elements/)

```javascript
// BAD: This runs three functions before it realizes there's nothing in the selection
$("#nosuchthing").slideUp();

// GOOD
var $mySelection = $("#nosuchthing");
if ($mySelection.length) {
    $mySelection.slideUp();
}
```



## 事件

1. 一个页面只写一个文档 ready 事件的处理程序。这样代码既清晰好调试，又容易跟踪代码的进程。
2. 不要用匿名函数来做事件的回调。匿名函数不易调试维护测试和复用。或许你想较真，看看这里吧

```javascript
$("#myLink").on("click", function(){...}); // 不要这样


// 这样
function myLinkClickHandler(){...}
$("#myLink").on("click", myLinkClickHandler);
```

3. 处理文档 ready 事件的回调也不要用匿名函数，匿名函数不易调试维护测试和复用

```javascript
$(function(){ ... }); // 糟糕的做法：无法利用此函数也无法为其写测试用例

// 好的做法
$(initPage); // 抑或 $(document).ready(initPage);
function initPage(){
  // 这里你可以进行程序的初始化了
}
```

4. 进一步，最好也将ready事件的处理程序放到外部文件中引入到页面，而页面中内嵌的代码只需调用即可。

```javascript
<script src="my-document-ready.js"></script>
<script>
    // 初始化一些必要的全局变量
    $(document).ready(initPage); // 抑或 $(initPage);
</script>
```

5. 千万不要写内联到 HTML 的 JS 代码，这是调试的噩梦！应该总是用 jQuery 来绑定事件自带程序，这样也方便随时动态地取消绑定。

```javascript
<a id="myLink" href="#" onclick="myEventHandler();">my link</a> <!-- 不好 -->
$("#myLink").on("click", myEventHandler); // GOOD
```

6. 如果可能尽量在绑定事件处理程序时使用一个命名空间，这样可以方便地取消绑定而不会影响其他绑定。

```javascript
$("#myLink").on("click.mySpecialClick", myEventHandler); // 不错
// 之后，让我们优雅地解除绑定
$("#myLink").unbind("click.mySpecialClick");
```

7. **当选择某个元素的子元素的时候，尽量在后面选择，不要在前面选择其中选择**。如下：

```javascript
$("#list a").on("click", myClickHandler); // BAD, you are attaching an event to all the links under the list.
$("#list").on("click", "a", myClickHandler); // GOOD, only one event handler is attached to the parent.
```



## Ajax异步操作

1. 不要用.getJson() 或 .get()，直接用直接用`$.ajax()` ，因为 jQuery 内部还是将前者转化为$.ajax()
2. 不要对 HTTPS 站点使用 HTTP 发起请求，最好干脆就不要指定（将HTTP或者HTTPS从你的URL中移除）
3. 不要在链接里面嵌参数，请使用专门的参数设置来传递

```javascript
// 不易阅读的代码...
$.ajax({
    url: "something.php?param1=test1&param2=test2",
    ....
});

// 更易阅读...
$.ajax({
    url: "something.php",
    data: { param1: test1, param2: test2 }
});j
```

4. 尽量指明数据类型以便你自己清楚要处理什么样的数据（见下方会提到的Ajax模板）
5. 对于异步动态加载的内容，最好使用代理来绑定事件处理程序。这样的好处是对于之后动态加载的元素事件同样有效。[了解更多](http://api.jquery.com/on/#direct-and-delegated-events)

```javascript
$("#parent-container").on("click", "a", delegatedClickHandlerForAjax);
```

6. 使用Promise模式。[更多例子](http://www.htmlgoodies.com/beyond/javascript/making-promises-with-jquery-deferred.html)

```javascript
$.ajax({ ... }).then(successHandler, failureHandler);

// 抑或
var jqxhr = $.ajax({ ... });
jqxhr.done(successHandler);
jqxhr.fail(failureHandler);
```

7. 标准的Ajax模板如下，[查看官方案例](https://api.jquery.com/jQuery.ajax/)

```javascript
var jqxhr = $.ajax({
    url: url,
    type: "GET",         // 默认为GET,你可以根据需要更改
    cache: true,         // 默认为true,但对于script,jsonp类型为false,可以自行设置
    data: {},            // 将请求参数放这里.
    dataType: "json",    // 指定想要的数据类型
    jsonp: "callback",   // 指定回调处理JSONP类型的请求
    statusCode: {        // 如果你想处理各状态的错误的话
        404: handler404,
        500: handler500
    }
});
jqxhr.done(successHandler);
jqxhr.fail(failureHandler);
```



## 动画与特效

1. 保持一个始终如一风格统一的动画实现
2. 紧遵用户体验，不要滥用动画特效

> 使用简洁的显示隐藏，状态切换，滑入滑出等效果来展示元素
>
> 使用预设值来设置动画的速度'fast'，'slow'，或者400（中等速度）



## 插件相关

1. 始终选择一个有良好支持，文档完善，全面测试过并且社区活跃的插件
2. 注意所用插件与当前使用的 jQuery 版本是否兼容
3. 一些常用功能应该写成 jQuery 插件。[jQuery插件的编写模板](http://lab.abhinayrathore.com/jquery-standards/)



## 链式结构

1. 除了用变量将jQuery选择器返回的结果保存，还可以利用好链式调用。

```javascript
$("#myDiv").addClass("error").show();
```

2. 当链式调用多达3次以上或代码因绑定回调略显复杂时，使用换行和适当的缩进来提高代码的可读性。

```javascript
$("#myLink")
    .addClass("bold")
    .on("click", myClickHandler)
    .on("mouseover", myMouseOverHandler)
    .show();
```

3. 对于特别长的调用最好还是用变量保存下中间结果来简化代码。



## 其他案例

1. 使用对象来传递参数

```javascript
$myLink.attr("href", "#").attr("title", "my link").attr("rel", "external"); 
// 糟糕：调用了三次 attr
// 不错，只调用了一次 attr
$myLink.attr({
    href: "#",
    title: "my link",
    rel: "external"
});
```

2. 不要将 CSS 与 jQuery 杂揉

```javascript
$("#mydiv").css({'color':red, 'font-weight':'bold'}); // 不好
.error {/* 不错 */
    color: red;
    font-weight: bold;
}
$("#mydiv").addClass("error"); 
```

3. 时刻关注官方Changelog，不要使用摒弃了的方法。[点此查看所有废弃的方法](http://api.jquery.com/category/deprecated/)
4. 适时地使用原生JavaScript。原生的性能肯定相当好一些，[查看性能比较](http://jsperf.com/document-getelementbyid-vs-jquery/3)

```javascript
$("#myId"); // 多少还是会逊色于...
document.getElementById("myId");
```

## 译者小结

上面的好的写法，感觉写的真的很不错，多看几遍，绝对有好处！关于jquery新版本废除了好多的用法，至今我还经常使用live()方法，有时候在动态调用click的时候管用，但是尽量不要用废弃了的方法！新版jquery不支持！