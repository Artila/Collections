## 网站前端性能优化之javascript和css

转自：http://www.haorooms.com/post/web_xnyh_jscss

之前看过Yahoo团队写的一篇关于网站性能优化的文章，文章是2010年左右写的，虽然有点老，但是很多方面还是很有借鉴意义的。关于css的性能优化，他提到了如下几点：

### CSS性能优化

#### 1、把样式表置于顶部

现把样式表放到文档的`< head />`内部似乎会加快页面的下载速度。这是因为把样式表放到`< head />`内会使页面有步骤的加载显示。

**注重性能的前端服务器往往希望页面有秩序地加载。**同时，我们也希望浏览器把已经接收到内容尽可能显示出来。这对于拥有较多内容的页面和网速较慢的用户来说特别重要。向用户返回可视化的反馈，比如进程指针，已经有了较好的研究并形成了正式文档。在我们的研究中HTML页面就是进程指针。当浏览器有序地加载文件头、导航栏、顶部的logo等对于等待页面加载的用户来说都可以作为可视化的反馈。这从整体上改善了用户体验。

**把样式表放在文档底部的问题是在包括Internet Explorer在内的很多浏览器中这会中止内容的有序呈现。浏览器中止呈现是为了避免样式改变引起的页面元素重绘。用户不得不面对一个空白页面。**

HTML 规范清 楚指出样式表要放包含在页面的`< head />`区域内：“和`< a />`不同，`< link />`只能出现在文档的`< head />`区域内，尽管它可以多次使用它”。无论是引起白屏还是出现没有样式化的内容都不值得去尝试。最好的方案就是按照HTML规范在文 档`< head />`内加载你的样式表。



#### 2、避免使用 CSS 表达式（Expression）

表达式的问题就在于它的计算频率要比我们想象的多。不仅仅是在页面显示和缩放时，就是在页面滚动、乃至移动鼠标时都会要重新计算一次。给CSS表达式增加一个计数器可以跟踪表达式的计算频率。在页面中随便移动鼠标都可以轻松达到10000次以上的计算量。

一个减少CSS表达式计算次数的方法就是使用一次性的表达式，它在第一次运行时将结果赋给指定的样式属性，并用这个属性来代替CSS表达式。如果样式属性 必须在页面周期内动态地改变，使用事件句柄来代替CSS表达式是一个可行办法。如果必须使用CSS表达式，一定要记住它们要计算成千上万次并且可能会对你 页面的性能产生影响。



#### 3、使用外部 JavaScript 和 CSS

很多性能规则都是关于如何处理外部文件的。但是，在你采取这些措施前你可能会问到一个更基本的问题：JavaScript和CSS是应该放在外部文件中呢还是把它们放在页面本身之内呢？

在实际应用中使用外部文件可以提高页面速度，**因为JavaScript和CSS文件都能在浏览器中产生缓存。**内置在HTML文档中的JavaScript 和CSS则会在每次请求中随HTML文档重新下载。这**虽然减少了HTTP请求的次数，却增加了HTML文档的大小。**从另一方面来说，如果外部文件中的 JavaScript和CSS被浏览器缓存，**在没有增加HTTP请求次数的同时可以减少HTML文档的大小。**

关键问题是，外部JavaScript和CSS文件缓存的频率和请求HTML文档的次数有关。虽然有一定的难度，但是仍然有一些指标可以一测量它。如果一 个会话中用户会浏览你网站中的多个页面，并且这些页面中会重复使用相同的脚本和样式表，缓存外部文件就会带来更大的益处。

对于拥有较大浏览量的首页来说，有一种技术可以平衡内置代码带来的HTTP请求减少与通过使用外部文件进行缓存带来的好处。其中一个就是在首页中内置 JavaScript和CSS，但是在页面下载完成后动态下载外部文件，在子页面中使用到这些文件时，它们已经缓存到浏览器了。

#### 4、削减 JavaScript 和 CSS

精简是指从去除代码不必要的字符，减少文件大小从而节省下载时间。消减代码时，所有的注释、不需要的空白字符（空格、换行、tab缩进）等都要去掉。在 JavaScript中，由于需要下载的文件体积变小了从而节省了响应时间。

精简JavaScript中目前用到的最广泛的两个工具是JSMin和YUI Compressor。YUI Compressor还可用于精简CSS。我之前的一篇文章关于前端部署的，ant+YUI Compressor 地址是：<http://www.haorooms.com/post/ant_yuicom> 小工具中也有ant的用法：<http://www.haorooms.com/tools/ant_book/>

混淆是另外一种可用于源代码优化的方法。这种方法要比精简复杂一些并且在混淆的过程更易产生问题。在对美国前10大网站的调查中发现，精简也可以缩小原来 代码体积的21%，而混淆可以达到25%。尽管混淆法可以更好地缩减代码，但是对于JavaScript来说精简的风险更小。

除消减外部的脚本和样式表文件外，< script>和< style>代码块也可以并且应该进行消减。即使你用Gzip压缩过脚本 和样式表，精简这些文件仍然可以节省5%以上的空间。由于JavaScript和CSS的功能和体积的增加，消减代码将会获得益处。

#### 5、用代替@import

前面的最佳实现中提到CSS应该放置在顶端以利于有序加载呈现。

在IE中，页面底部@import和使用< link>作用是一样的，因此最好不要使用它。



#### 6、避免使用滤镜

IE独有属性 AlphaImageLoader 用于修正7.0以下版本中显示PNG图片的半透明效果。这个滤镜的问题在于浏览器加载图片时它会终止内容的 呈现并且冻结浏览器。在每一个元素（不仅仅是图片）它都会运算一次，增加了内存开支，因此它的问题是多方面的。

完全避免使用AlphaImageLoader的最好方法就是使用PNG8格式来代替，这种格式能在IE中很好地工作。如果你确实需要使用AlphaImageLoader，请使用下划线_filter又使之对IE7以上版本的用户无效。



### JavaScript 性能优化

#### 1、把脚本置于页面底部

**脚本带来的问题就是它阻止了页面的平行下载。**HTTP/1.1 规范建议，浏览器每个主机名的并行下载内容不超过两个。如果你的图片放在多个主机名上，你可以在每个并行下载中同时下载2个以上的文件。但是当下载脚本时，浏览器就不会同时下载其它文件了，即便是主机名不相同。

在某些情况下把脚本移到页面底部可能不太容易。比如说，如果脚本中使用了document.write来插入页面内容，它就不能被往下移动了。这里可能还会有作用域的问题。很多情况下，都会遇到这方面的问题。

一个经常用到的替代方法就是使用延迟脚本。DEFER属性表明脚本中没有包含document.write，它告诉浏览器继续显示。不幸的 是，Firefox并不支持DEFER属性。在Internet Explorer中，脚本可能会被延迟但效果也不会像我们所期望的那样。如果脚本可以被延迟，那么它就可以移到页面的底部。这会让你的页面加载的快一点。



#### 2、使用外部JavaScript和CSS

同上，css中写了，我之前文章中列举了一下cdn，可以调用外部的。cdn公共库：<http://www.haorooms.com/post/cdn_all



#### 3、削减JavaScript和CSS

同上，css中写了



#### 4、剔除重复脚本

在同一个页面中重复引用JavaScript文件会影响页面的性能。你可能会认为这种情况并不多见。对于美国前10大网站的调查显示其中有两家存在重复引 用脚本的情况。有两种主要因素导致一个脚本被重复引用的奇怪现象发生：团队规模和脚本数量。如果真的存在这种情况，重复脚本会引起不必要的HTTP请求和 无用的JavaScript运算，这降低了网站性能。

在Internet Explorer中会产生不必要的HTTP请求，而在Firefox却不会。在Internet Explorer中，如果一个脚本被引用两次而且它又不可缓存，它就会在页面加载过程中产生两次HTTP请求。即时脚本可以缓存，当用户重载页面时也会产 生额外的HTTP请求。

**除增加额外的HTTP请求外，多次运算脚本也会浪费时间。**在Internet Explorer和Firefox中不管脚本是否可缓存，它们都存在重复运算JavaScript的问题。

**一个避免偶尔发生的两次引用同一脚本的方法是在模板中使用脚本管理模块引用脚本。**在HTML页面中使用< script />标签引用脚本的最常见方法就是：

```javascript
<script type="text/javascript" src="menu_1.0.17.js"></script> 
```

在PHP中可以通过创建名为insertScript的方法来替代：

```php
<?php insertScript("menu.js") ?> 
```

为了防止多次重复引用脚本，这个方法中还应该使用其它机制来处理脚本，如检查所属目录和为脚本文件名中增加版本号以用于Expire文件头等。



#### 5、减少DOM访问

使用JavaScript访问DOM元素比较慢，因此为了获得更多的应该页面，应该做到：

- 缓存已经访问过的有关元素
- 线下更新完节点之后再将它们添加到文档树中
- 避免使用JavaScript来修改页面布局



#### 6、开发智能事件处理程序

有时候我们会感觉到页面反应迟钝，这是因为DOM树元素中附加了过多的事件句柄并且些事件句病被频繁地触发。这就是为什么说使用event delegation（事件代理）是一种好方法了。如果你在一个div中有10个按钮，你只需要在div上附加一次事件句柄就可以了，而不用去为每一个按 钮增加一个句柄。事件冒泡时你可以捕捉到事件并判断出是哪个事件发出的。

你同样也不用为了操作DOM树而等待onload事件的发生。你需要做的就是等待树结构中你要访问的元素出现。你也不用等待所有图像都加载完毕。



### 如何加载JS，JS应该放在什么位置研究

#### 外部JS的阻塞下载

**所有浏览器在下载JS的时候，会阻止一切其他活动，比如其他资源的下载，内容的呈现等等。至到JS下载、解析、执行完毕后才开始继续并行下载其他资源并呈现内容。**

有人会问：为什么JS不能像CSS、image一样并行下载了？这里需要简单介绍一下浏览器构造页面的原理， 当浏览器从服务器接收到了HTML文档，并把HTML在内存中转换成DOM树，在转换的过程中如果发现某个节点(node)上引用了CSS或者 IMAGE，就会再发1个request去请求CSS或image,然后继续执行下面的转换，而不需要等待request的返回，当request返回 后，只需要把返回的内容放入到DOM树中对应的位置就OK。但当引用了JS的时候，浏览器发送1个js request就会一直等待该request的返回。因为浏览器需要1个稳定的DOM树结构，而JS中很有可能有代码直接改变了DOM树结构，比如使用 document.write 或 appendChild,甚至是直接使用的location.href进行跳转，浏览器为了防止出现JS修改DOM树，需要重新构建DOM树的情况，所以 就会阻塞其他的下载和呈现.

阻塞下载图：下图是访问blogjava首页的时间瀑布图，可以看出来开始的2个image都是并行下载的，而后面的2个JS都是阻塞下载的(1个1个下载)。

![enter image description here](http://www.haorooms.com/uploads/images/jsload.jpg)

#### 嵌入JS的阻塞下载

嵌入JS是指直接写在HTML文档中的JS代码。上面说了引用外部的JS会阻塞其后的资源下载和其后的内容呈现，哪嵌入的JS又会是怎样阻塞的了，看下面的列2个代码：

```html
**代码1：** 

< div >
         < ul >
             < li > blogjava </ li >
             < li > CSDN </ li >
             < li > haorooms博客 </ li >
             < li > ABC </ li >
             < li > AAA </ li >
         < ul >     
     </ div >
     < script  type ="text/javascript" >
         // 循环5秒钟
         var  n  =  Number( new  Date());
         var  n2  =  Number( new  Date());
         while ((n2  -  n)  <  ( 6 * 1000 )) {
           n2  =  Number( new  Date());
         }
     </ script >
   < div >
         < ul >
             < li > MSN </ li >
             < li > GOOGLE </ li >
             < li > YAHOO </ li >
         < ul >     
</ div > 
```

运行后，会发现代码1中，在前5秒中页面上是一篇空白，5秒中后页面全部显示。 代码2中，前5秒中blogjava,csdn等先显示出来，5秒后MSN才显示出来。

可以看出嵌入JS会阻塞所有内容的呈现，而外部JS只会阻塞其后内容的显示，2种方式都会阻塞其后资源的下载。

#### 嵌入JS导致CSS阻塞加载的问题

CSS怎么会阻塞加载了？CSS本来是可以并行下载的，在什么情况下会出现阻塞加载了(在测试观察中，IE6下CSS都是阻塞加载，下面的测试在非IE6下进行)：

代码1(为了效果，这里选择了1个国外服务器的CSS)：

```html
< html  xmlns ="http://www.w3.org/1999/xhtml" >
         < head >
           < title > js test </ title >
           < meta  http-equiv ="Content-Type"  content ="text/html; charset=UTF-8"   />  
           < link  type ="text/css"  rel ="stylesheet"  href ="http://69.64.92.205/Css/Home3.css"   />
         </ head >
         < body >
             < img  src ="http://www.haorooms.com/images/logo.gif"   />< br  />
              < img  src ="http://www.haorooms.com/images/csdnindex_piclogo.gif"   />
         </ body >
</ html > 
```

时间瀑布图：

![enter image description here](http://www.haorooms.com/uploads/images/jsload2.jpg)

代码2(只加了1个空的嵌入JS)：

```html
< head >
     < title > js test </ title >
     < meta  http-equiv ="Content-Type"  content ="text/html; charset=UTF-8"   />  
   < link  type ="text/css"  rel ="stylesheet"  href ="http://69.64.92.205/Css/Home3.css"   />
   < script  type ="text/javascript" >
         function  a(){}
   </ script >
</ head >
< body >
         < img  src ="http://www.haorooms.com/images/logo.gif"   />< br  />
         < img  src ="http://www.haorooms.com/images/csdnindex_piclogo.gif"   />
</ body >
```

时间瀑布图:

![enter image description here](http://www.haorooms.com/uploads/images/jsload3.jpg)

从时间瀑布图中可以看出，代码2中，CSS和图片并没有并行下载，而是等待CSS下载完毕后才去并行下载后面的2个图片，当CSS后面跟着嵌入的JS的时候，该CSS就会出现阻塞后面资源下载的情况。

有人可能会问，这里为什么不说说嵌入的JS阻塞了后面的资源，而是说CSS阻塞了？ 想想我们现在用的是1个空函数，解析这个空函数1ms就够，而后面2个图片是等CSS下载完1.3s后才开始下载。大家还可以试试把嵌入JS放到CSS前 面，就不会出现阻塞的情况了。

根本原因：因为浏览器会维持html中css和js的顺序，样式表必须在嵌入的JS执行前先加载、解析完。而嵌入的JS会阻塞后面的资源加载，所以就会出现上面CSS阻塞下载的情况。

#### 嵌入JS应该放在什么位置

1、放在底部，虽然放在底部照样会阻塞所有呈现，但不会阻塞资源下载。

2、如果嵌入JS放在head中，请把嵌入JS放在CSS前面。

3、使用defer

4、不要在嵌入的JS中调用运行时间较长的函数，如果一定要用，可以用setTimeout来调用,关于settimeout，我之前的一篇文章中写过，请看：<http://www.haorooms.com/post/js_setTimeout>