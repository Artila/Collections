# jQuery基础——事件篇

### 2 鼠标事件

####2-1 jQuery鼠标事件之click与dbclick事件 

用交互操作中，最简单直接的操作就是点击操作。jQuery提供了两个方法一个是click方法用于监听用户单击操作，另一个方法是dbclick方法用于监听用户双击操作。这两个方法的用法是类似的，下面以click()事件为例

使用上非常简单：

**方法一：$ele.click()**

绑定$ele元素，不带任何参数一般是用来指定触发一个事件，用的比较少

```
<div id="test">点击触发<div>
$("ele").click(function(){
    alert('触发指定事件')
})
$("#test").click(function(){
     $("ele").click()  //手动指定触发事件 
});
```

**方法二：$ele.click( handler(eventObject) )**

绑定**$ele**元素，每次$ele元素触发点击操作会执行回调 handler函数，这样可以针对事件的反馈做很多操作了，方法中的this是指向了绑定事件的元素

```
<div id="test">点击触发<div>
$("#test").click(function() {
    //this指向 div元素
});
```

**方法三：$ele.click( [eventData ], handler(eventObject) )**

使用与方法二一致，不过可以接受一个数据参数，这样的处理是为了解决不同作用域下数据传递的问题

```
<div id="test">点击触发<div>
$("#test").click(11111,function(e) {
    //this指向 div元素
    //e.data  => 11111 传递数据
});
```

dblclick()的用法和click()的用法是类似的，可以参考以上click()的用法。

**dbclick与click事件不同的是：**

**click事件触发需要以下几点：**

- click事件其实是由mousedown与mouseup 2个动作构成，所以点击的动作只有在松手后才触发

PS: mousedown 和 mouseup 下一节会讲到

**dblclick事件触发需要以下几点：**

dblclick又是由2个click叠加而来的，所以dblclick事件只有在满足以下条件的情况下才能被触发

- 鼠标指针在元素里面时点击。
- 鼠标指针在元素里面时释放。
- 鼠标指针在元素里面时再次点击，点击间隔时间，视系统而定。
- 鼠标指针在元素里面时再次释放。

**注意：**在同一元素上同时绑定 click 和 dblclick 事件是不可取的。各个浏览器事件触发的顺序是不同的，一些浏览器在dblclick之前接受两个 click 事件 ，而一些浏览器只接受一个 click 事件。用户往往可通过不同的操作系统和浏览器配置双击灵敏度。



#### 2-2 jQuery鼠标事件之mousedown与mouseup事件

用户交互操作中，最简单直接的操作就是点击操作，因此jQuery提供了一个mousedown的快捷方法可以监听用户鼠标按下的操作，与其对应的还有一个方法mouseup快捷方法可以监听用户鼠标弹起的操作。**两种方法用法类似**，下面以mousedown()为例

使用上非常简单：

**方法一：$ele.**mousedown**()**

绑定$ele元素，不带任何参数一般是用来指定触发一个事件，可能一般用的比较少

```
<div id="test">点击触发<div>
$("ele").mousedown(function(){
    alert('触发指定事件')
})
$("#test").mousedown(function(){
     $("ele").mousedown()  //手动指定触发事件 
});
```



**方法二：$ele.mousedown( handler(eventObject) )**

绑定**$ele**元素，每次$ele元素触发点击操作会执行回调 handler函数

这样可以针对事件的反馈做很多操作了

```
<div id="test">点击触发<div>
$("#test").mousedown(function() {
    //this指向 div元素
});
```



方法三：$ele.mousedown( [eventData ], handler(eventObject) )**

使用与方法二一致，不过可以接受一个数据参数，这样的处理是为了解决不同作用域下数据传递的问题

```
<div id="test">点击触发<div>
$("#test").mousedown(11111,function(e) {
    //this指向 div元素
    //e.data  => 11111 传递数据
});
```


**mousedown事件触发需要以下几点：**

- mousedown强调是**按下触发**
- 如果在一个元素按住了鼠标不放，并且拖动鼠标离开这个元素，并释放鼠标键，这仍然是算作mousedown事件
- 任何鼠标按钮被按下时都能触发mousedown事件
- 用event 对象的which区别按键，敲击鼠标左键which的值是1，敲击鼠标中键which的值是2，敲击鼠标右键which的值是3

**mouseup事件触发需要以下几点：**

- mouseup强调是**松手触发**，与mousedown是相反的
- mouseup与mousedown组合起来就是click事件
- 如果用户在一个元素上按下鼠标按键，并且拖动鼠标离开这个元素，然后释放鼠标键，这仍然是算作mouseup事件
- 任何鼠标按钮松手时都能触发mouseup事件
- 用event 对象的which区别按键，敲击鼠标左键which的值是1，敲击鼠标中键which的值是2，敲击鼠标右键which的值是3

**另外需要注意的是：**

**click与mousedown的区别：**

- click事件其实是由mousedown于mouseup 2个动作构成，所以点击的动作只有在松手后才触发




#### 2-3 jQuery鼠标事件之mousemove事件

用交互操作中，经常需要知道用户是否有移动的操作。基于移动的机制可以做出拖动、拖拽一系列的效果出来。针对移动事件，jQuery提供了一个mousemove的快捷方法可以监听用户移动的的操作

使用上非常简单：

**方法一：$ele.mousemove()**

绑定$ele元素，不带任何参数一般是用来指定触发一个事件，用的比较少

```
<div id="test">点击触发<div>
$("ele").mousemove(function(){
    alert('触发指定事件')
})
$("#test").click(function(){
     $("ele").mousemove()  //指定触发事件 
});
```

 

**方法二：$ele.mousemove( handler(eventObject) )**

绑定**$ele**元素，每次$ele元素触发点击操作会执行回调 handler函数

这样可以针对事件的反馈做很多操作了

```
<div id="test">滑动触发<div>
$("#test").mousemove(function() {
    //this指向 div元素 
});
```

 

**方法三：$ele.mousemove( [eventData ], handler(eventObject) )**

使用与方法二一致，不过可以接受一个数据参数，这样的处理是为了解决不同作用域下数据传递的问题

```
<div id="test">点击触发<div>
$("#test").mousemove(11111,function(e) {
    //this指向 div元素
    //e.data  => 11111 传递数据
});
```

 

**mousemove事件触发需要以下几点：**

- mousemove事件是当鼠标指针移动时触发的，即使是一个像素

- 如果处理器做任何重大的处理，或者如果该事件存在多个处理函数，这可能造成浏览器的严重的性能问题

  ​


#### 2-4 jQuery鼠标事件之mouseover与mouseout事件 

jQuery当中同样提供了这样的事件来监听用户的移入移出操作，mouseover()与mouseout()事件，两者用法类似，下面一mouseover为例：

**方法一：$ele.mouseover()**

绑定$ele元素，不带任何参数一般是用来指定触发一个事件，用的比较少

```
<div id="test">点击触发<div>
$("ele").mouseover(function(){
    alert('触发指定事件')
})
$("#test").click(function(){
     $("ele").mouseover()  //指定触发事件 
});
```

**方法二：$ele.mouseover( handler(eventObject) )**

绑定**$ele**元素，每次$ele元素触发点击操作会执行回调 handler函数

这样可以针对事件的反馈做很多操作了

```
<div id="test">滑动触发<div>
$("#test").mouseover(function() {
    //this指向 div元素 
});
```

**方法三：$ele.mouseover( [eventData ], handler(eventObject) )**

使用与方法二一致，不过可以接受一个数据参数，这样的处理是为了解决不同作用域下数据传递的问题

```
<div id="test">点击触发<div>
$("#test").mouseover(11111,function(e) {
    //this指向 div元素
    //e.data  => 11111 传递数据
});
```



#### 2-5 jQuery鼠标事件之mouseenter与mouseleave事件 

用交互操作中，经常需要知道用户操作鼠标是否有移到元素内部或是元素外部，因此jQuery提供了一个mouseenter和mouseleave的快捷方法可以监听用户移动到内部的操作

使用上非常简单，三种参数传递方式与mouseover和mouseout是一模一样的，所以这里不再重复，主要讲讲区别，下面以mouseenter为例：

mouseenter JavaScript事件是Internet Explorer专有的。由于该事件在平时很有用，jQuery的模拟这一事件，以便它可用于所有浏览器。该事件在鼠标移入到元素上时被触发。任何HTML元素都可以接受此事件。

**mouseenter事件和mouseover的区别**

> 关键点就是：冒泡的方式处理问题

简单的例子：

mouseover为例：

```
<div class="aaron2">
    <p>鼠标离开此区域触发mouseleave事件</p>
</div>
```

如果在p元素与div元素都绑定mouseover事件，鼠标在离开p元素，但是没有离开div元素的时候，触发的结果:

1. p元素响应事件
2. div元素响应事件

这里的问题是div为什么会被触发？ 原因就是事件冒泡的问题，p元素触发了mouseover，他会一直往上找父元素上的mouseover事件，如果父元素有mouseover事件就会被触发

所以在这种情况下面，jQuery推荐我们使用 mouseenter事件

```
mouseenter事件只会在绑定它的元素上被调用，而不会在后代节点上被触发
```

这就是最本质的区别。



#### 2-6 jQuery鼠标事件之hover事件

学了mouseover、mouseout、mouseenter、mouseleave事件，也理解了四个事件的相同点与不同点，现在可以用来给元素做一个简单的切换效果

在元素上移进移出切换其换色，一般通过2个事件配合就可以达到，这里用mouseenter与mouseleave，这样可以避免冒泡问题

```
$(ele).mouseenter(function(){
     $(this).css("background", '#bbffaa');
 })
$(ele).mouseleave(function(){
    $(this).css("background", 'red');
})
```

这样目的是达到了，代码稍微有点多，对于这样的简单逻辑jQuery直接提供了一个hover方法，可以便捷处理

只需要在hover方法中传递2个回调函数就可以了，不需要显示的绑定2个事件

```
$(selector).hover(handlerIn, handlerOut)
```

- handlerIn(eventObject)：当鼠标指针进入元素时触发执行的事件函数
- handlerOut(eventObject)：当鼠标指针离开元素时触发执行的事件函数



#### 2-7 jQuery鼠标事件之focusin事件

当一个元素，或者其内部任何一个元素获得焦点的时候，例如：input元素，用户在点击聚焦的时候，如果开发者需要捕获这个动作的时候，jQuery提供了一个focusin事件

使用上非常简单：

**方法一：$ele.focusin()**

绑定$ele元素，不带任何参数一般是用来指定触发一个事件，一般用的比较少

```
<div id="test">点击触发<div>
$("ele").focusin(function(){
    alert('触发指定事件')
})
$("#test").mouseup(function(){
     $("ele").focusin()  //指定触发事件 
});
```

 

**方法二：$ele.focusin( handler )**

绑定**$ele**元素，每次$ele元素触发点击操作会执行回调 handler函数

这样可以针对事件的反馈做很多操作了

```
<div id="test">点击触发<div>
$("#test").focusin(function() {
    //this指向 div元素
});
```

 

**方法三：$ele.focusin( [eventData ], handler )**

使用与方法二一致，不过可以接受一个数据参数，这样的处理是为了解决不同作用域下数据传递的问题

```
<div id="test">点击触发<div>
$("#test").focusin(11111,function(e) {
    //this指向 div元素
    //e.data  => 11111 传递数据
});
```

 

#### 2-8 jQuery鼠标事件之focusout事件 

当一个元素，或者其内部任何一个元素失去焦点的时候，比如input元素，用户在点击失去焦的时候，如果开发者需要捕获这个动作，jQuery提供了一个focusout事件

使用上非常简单：

**方法一：$ele.focusout()**

绑定$ele元素，不带任何参数一般是用来指定触发一个事件，可能一般用的比较少

```
<div id="test">点击触发<div>
$("ele").focusout(function(){
    alert('触发指定事件')
})
$("#test").mouseup(function(){
     $("ele").focusout()  //指定触发事件 
});
```

 

**方法二：$ele.focusout( handler )**

绑定**$ele**元素，每次$ele元素触发点击操作会执行回调 handler函数

这样可以针对事件的反馈做很多操作了

```
<div id="test">点击触发<div>
$("#test").focusout(function() {
    //this指向 div元素
});
```

 

**方法三：$ele.focusout( [eventData ], handler )**

使用与方法二一致，不过可以接受一个数据参数，这样的处理是为了解决不同作用域下数据传递的问题

```
<div id="test">点击触发<div>
$("#test").focusout(11111,function(e) {
    //this指向 div元素
    //e.data  => 11111 传递数据
});
```

> focus和blur不支持冒泡，focusin和focusout支持冒泡



### 3 表单事件

#### 3-1 jQuery表单事件之blur与focus事件

在之前2.8与2.9节我们学过了表单处理事件focusin事件与focusout事件，同样用于处理表单焦点的事件还有blur与focus事件

它们之间的本质区别:

> 是否支持冒泡处理



举个简单的例子

```
<div>
  <input type="text" />
</div>
```

其中input元素可以触发focus()事件

div是input的父元素，当它包含的元素input触发了focus事件时，它就产生了focusin()事件。

```
focus()在元素本身产生，focusin()在元素包含的元素中产生
```

blur与focusout也亦是如此。



#### 3-2 jQuery表单事件之change事件 

<input>元素，<textarea>和<select>元素的值都是可以发生改变的，开发者可以通过change事件去监听这些改变的动作

**input元素**

```
监听value值的变化，当有改变时，失去焦点后触发change事件。对于单选按钮和复选框，当用户用鼠标做出选择时，该事件立即触发。
```

**select元素**

```
对于下拉选择框，当用户用鼠标作出选择时，该事件立即触发
```

**textarea元素**

```
多行文本输入框，当有改变时，失去焦点后触发change事件
```

change事件很简单，无非就是注意下触发的先后行为。



#### 3-3 jQuery表单事件之select事件 

当 textarea 或文本类型的 input 元素中的文本被选择时，会发生 select 事件。
这个函数会调用执行绑定到select事件的所有函数，包括浏览器的默认行为。可以通过在某个绑定的函数中返回false来防止触发浏览器的默认行为。

```
select事件只能用于<input>元素与<textarea>元素
```

使用上非常简单：

**方法一：.select()**

触发元素的select事件:

```
$("input").select();
```

 

**方法二：$ele.select( handler(eventObject) )**

绑定*$ele*元素，每次$ele元素触发点击操作会执行回调 handler函数

这样可以针对事件的反馈做很多操作了

```
<input id="test" value="文字选中"></input>
$("#test").select(function() { //响应文字选中回调
    //this指向 input元素 
});
```

 

**方法三：$ele.select( [eventData ], handler(eventObject) )**

使用与方法二一致，不过可以接受一个数据参数，这样的处理是为了解决不同作用域下数据传递的问题

```
<input id="test" value="文字选中"></input>
$("#test").select(11111,function(e) {//响应文字选中回调
    //this指向 div元素 
   //e.data  => 11111 传递数据
});
```



####3-4 jQuery表单事件之submit事件 

提交表单是一个最常见的业务需求，比如用户注册，一些信息的输入都是需要表单的提交。同样的有时候开发者需要在表单提交的时候过滤一些的数据、做一些必要的操作（例如：验证表单输入的正确性，如果错误就阻止提交，从新输入）此时可以通过submit事件，监听下提交表单的这个动作

使用上非常简单，与基本事件参数处理保持一致

**方法一：$ele.submit()**

绑定$ele元素，不带任何参数一般是用来指定触发一个事件，用的比较少

```
<div id="test">点击触发<div>
$("ele").submit(function(){
    alert('触发指定事件')
})
$("#text").click(function(){
     $("ele").submit()  //指定触发事件 
});
```

 

**方法二：$ele.submit( handler(eventObject) )**

绑定*$ele*元素，每次$ele元素触发点击操作会执行回调 handler函数

这样可以针对事件的反馈做很多操作了

```
<form id="target" action="destination.html">
  <input type="submit" value="Go" />
</form>
$("#target").submit(function() { //绑定提交表单触发
    //this指向 from元素 
});
```

 

**方法三：$ele.submit( [eventData ], handler(eventObject) )**

使用与方法二一致，不过可以接受一个数据参数，这样的处理是为了解决不同作用域下数据传递的问题

```
<form id="target" action="destination.html">
  <input type="submit" value="Go" />
</form>
$("#target").submit(11111,function(data) { //绑定提交表单触发
    //data => 1111 //传递的data数据
});
```

 

通过在<form>元素上绑定submit事件，开发者可以监听到用户的提交表单的的行为

具体能触发submit事件的行为：

- <input type="submit">
- <input type="image">
- <button type="submit">
- 当某些表单元素获取焦点时，敲击Enter（回车键）

上述这些操作下，都可以截获submit事件。

这里需要特别注意：

```
form元素是有默认提交表单的行为，如果通过submit处理的话，需要禁止浏览器的这个默认行为
传统的方式是调用事件对象  e.preventDefault() 来处理， jQuery中可以直接在函数中最后结尾return false即可
```

jQuery处理如下：

```
$("#target").submit(function(data) { 
   return false; //阻止默认行为，提交表单
});
```

> 1.event.stopPropagation();
> 　　事件处理过程中，阻止了事件冒泡，但不会阻击默认行为
> 2.return false;
> 　　事件处理过程中，阻止了事件冒泡，也阻止了默认行为
> 3.event.preventDefault();
> 　　它的作用是：事件处理过程中，不阻击事件冒泡，但阻击默认行为



### 4 键盘事件

#### 4-1 jQuery键盘事件之keydown()与keyup()事件

鼠标有mousedown,mouseup之类的事件，这是根据人的手势动作分解的2个触发行为。相对应的键盘也有这类事件，将用户行为分解成2个动作，键盘按下与松手，针对这样的2种动作，jQuery分别提供了对应keydown与keyup方法来监听

**keydown事件：**

当用户在一个元素上第一次按下键盘上字母键的时候，就会触发它。使用上非常简单，与基本事件参数处理保持一致，这里使用不在重复了，列出使用的方法

```
//直接绑定事件
$elem.keydown( handler(eventObject) )
//传递参数
$elem.keydown( [eventData ], handler(eventObject) )
//手动触发已绑定的事件
$elem.keydown()
```

 

**keyup事件：**

当用户在一个元素上第一次松手键盘上的键的时候，就会触发它。使用方法与keydown是一致的只是触发的条件是方法的

**注意：**

- keydown是在键盘按下就会触发
- keyup是在键盘松手就会触发
- 理论上它可以绑定到任何元素，但keydown/keyup事件只是发送到具有焦点的元素上，不同的浏览器中，可获得焦点的元素略有不同，但是表单元素总是能获取焦点，所以对于此事件类型表单元素是最合适的。



####4-2 jQuery键盘事件之keypress()事件

在input元素上绑定keydown事件会发现一个问题：

>每次获取的内容都是之前输入的，当前输入的获取不到



keydown事件触发在文字还没敲进文本框，这时如果在keydown事件中输出文本框中的文本，得到的是触发键盘事件前的文本，而keyup事件触发时整个键盘事件的操作已经完成，获得的是触发键盘事件后的文本

当浏览器捕获键盘输入时，还提供了一个keypress的响应，这个跟keydown是非常相似，这里使用请参考keydown这一节，具体说说不同点

keypress事件与keydown和keyup的主要区别

- 只能捕获单个字符，不能捕获组合键
- 无法响应系统功能键（如delete，backspace）
- 不区分小键盘和主键盘的数字字符

总而言之，

KeyPress主要用来接收字母、数字等ANSI字符，而 KeyDown 和 KeyUP 事件过程可以处理任何不被 KeyPress 识别的击键。诸如：功能键（F1-F12）、编辑键、定位键以及任何这些键和键盘换档键的组合等。



### 5 事件的绑定和解绑

#### 5-1 on()的多事件绑定

之前学的鼠标事件，表单事件与键盘事件都有个特点，就是直接给元素绑定一个处理函数，所有这类事件都是属于快捷处理。翻开源码其实可以看到，所有的快捷事件在底层的处理都是通过一个"on"方法来实现的。jQuery on()方法是官方推荐的绑定事件的一个方法。

**基本用法：.on( events ,[ selector ] ,[ data ] )**

最常见的给元素绑定一个点击事件，对比一下快捷方式与on方式的不同

```
$("#elem").click(function(){})  //快捷方式
$("#elem").on('click',function(){}) //on方式
```

最大的不同点就是on是可以自定义事件名，当然不仅仅只是如何，继续往下看

**多个事件绑定同一个函数**

```
 $("#elem").on("mouseover mouseout",function(){ });
```

通过空格分离，传递不同的事件名，可以同时绑定多个事件

**多个事件绑定不同函数**

```
$("#elem").on({
    mouseover:function(){},  
    mouseout:function(){}
});
```

通过空格分离，传递不同的事件名，可以同时绑定多个事件，每一个事件执行自己的回调方法

**将数据传递到处理程序**

```
function greet( event ) {
  alert( "Hello " + event.data.name ); //Hello 慕课网
}
$( "button" ).on( "click", {
  name: "慕课网"
}, greet );
```

可以通过第二参数（对象），当一个事件被触发时，要传递给事件处理函数的



#### 5-2 on()的高级用法

针对自己处理机制中，不仅有on方法，还有根据on演变出来的live方法(1.7后去掉了)，delegate方法等等。这些方法的底层实现部分 还是on方法，这是利用了on的另一个事件机制委托的机制衍变而来的

**委托机制**

```
.on( events ,[ selector ] ,[ data ], handler(eventObject) )
```

在on的第二参数中提供了一个selector选择器，简单的来描述下:

实际上是给祖先绑定一个事件。子元素通过冒泡将事传递到祖先元素，祖先元素再判断点击的是不是button，如果是，就执行相同的事件。因此，当有很多个相同的按钮需要绑定相同的事件时，可以用事件委托将事件委托给祖先节点，有祖先节点判断子节点是否执行某事件。如果不适用事假委托，那个每一个节点都需要绑定一个事件。 
使用方法是： 

```
祖先节点.on(“事件”,”子元素”,”绑定的函数”);
```

on的第二个参数需要写成所有相同元素通用的写法，不能写成:button:eq(0)这样的选择不具有通用性，祖先节点在判断的时候会无法达到预期的效果。

```   
$("div:eq(0)").on("click",":button",function(){

	$(this).clone(true).appendTo("div:eq(0)");

});

// 换成document也可：

$(document).on("click",":button",function(){

	$(this).clone(true).appendTo("div:eq(0)");

});

```



####5-3 卸载事件off()方法

- 通过.on()绑定的事件处理程序
- 通过off() 方法移除该绑定

根据on绑定事件的一些特性，off方法也可以通过相应的传递组合的事件名，名字空间，选择器或处理函数来移除绑定在元素上指定的事件处理函数。当有多个过滤参数时，只有与这些参数完全匹配的事件处理函数才会被移除

绑定2个事件

```
$("elem").on("mousedown mouseup",fn)
```

删除一个事件

```
$("elem").off("mousedown")
```

删除所有事件

```
$("elem").off("mousedown mouseup")
```

快捷方式删除所有事件，这里不需要传递事件名了，节点上绑定的所有事件讲全部销毁

```
$("elem").off()
```



### 6 事件对象的使用

#### 6-1 jQuery事件对象的作用

事件中的Event对象容易被初学者忽略掉，可能大多时候初学者不知道怎么去用它，但有些时候它还是非常有用的

一个标准的"click"点击事件

```
$(elem).on("click",function(event){
   event //事件对象
})
```

在不同浏览器之间事件对象的获取, 以及事件对象的属性都有差异。jQuery根据 W3C 标准规范了事件对象，所以在jQuery事件回调方法中获取到的事件对象是经过兼容后处理过的一个标准的跨浏览器对象

这里不在千篇一律的说方法的使用，通过实际的一个小案例，从而来了解事件对象的作用

```
<ul>
    <li class="even1"></li>
    <li class="even2"></li>
    <li class="even2"></li>
    .........
</ul>

```

ul有N个子元素li(这里只写了3个)，如果我要响应每一个li的事件，那么常规的方法就是需要给所有的li都单独绑定一个事件监听，这样写法很符合逻辑，但是同时有显得繁琐。

因为li都有一个共同的父元素，而且所有的事件都是一致的，这里我们可以采用要一个技巧来处理，也是常说的"事件委托"。

事件没直接和li元素发生关系，而且绑定父元素了。由于浏览器有事件冒泡的这个特性，我们可以在触发li的时候把这个事件往上冒泡到ul上，因为ul上绑定事件响应所以就能够触发这个动作了。唯一的问题怎么才知道触发的li元素是哪个一个？

这里就引出了事件对象了

```
事件对象是用来记录一些事件发生时的相关信息的对象。事件对象只有事件发生时才会产生，并且只能是事件处理函数内部访问，在所有事件处理函数运行结束后，事件对象就被销毁
```

回到上面的问题，既然事件对象是跟当前触发元素息息相关的，所以我们就能从里面相关的信息，从事件对象中找到 event.target。

**event.target**

target 属性可以是注册事件时的元素，或者它的子元素。通常用于比较 event.target 和 this 来确定事件是不是由于冒泡而触发的。经常用于事件冒泡时处理事件委托

简单来说：**event.target代表当前触发事件的元素，可以通过当前元素对象的一系列属性来判断是不是我们想要的元素**。

> 这个委托的意思就是减少事件绑定。
>
> $("li").on('click'  为每个li都绑定click事件  
>
> $("ul").on('click'  只为ul绑定click事件 通过事件冒泡来执行事件



####6-2 jQuery事件对象的属性和方法

事件对象的属于与方法有很多，但是我们经常用的只有那么几个，这里我主要说下作用与区别

**event.type：获取事件的类型**

触发元素的事件类型

```
$("a").click(function(event) {
  alert(event.type); // "click"事件
});
```

**event.pageX 和 event.pageY：获取鼠标当前相对于页面的坐标**

通过这2个属性，可以确定元素在当前页面的坐标值，鼠标相对于文档的左边缘的位置（左边）与 （顶边）的距离，简单来说是从页面左上角开始,即是以页面为参考点,不随滑动条移动而变化

**event.preventDefault() 方法：阻止默认行为**

这个用的特别多，在执行这个方法后，如果点击一个链接（a标签），浏览器不会跳转到新的 URL 去了。我们可以用 event.isDefaultPrevented() 来确定这个方法是否(在那个事件对象上)被调用过了

**event.stopPropagation() 方法：阻止事件冒泡**

事件是可以冒泡的，为防止事件冒泡到DOM树上，也就是不触发的任何前辈元素上的事件处理函数

**event.which：获取在鼠标单击时，单击的是鼠标的哪个键**

event.which 将 event.keyCode 和 event.charCode 标准化了。event.which也将正常化的按钮按下(mousedown 和 mouseupevents)，左键报告1，中间键报告2，右键报告3

**event.currentTarget : 在事件冒泡过程中的当前DOM元素**

冒泡前的当前触发事件的DOM对象, 等同于this.

**this和event.target的区别：**

js中事件是会冒泡的，所以this是可以变化的，但event.target不会变化，它永远是直接接受事件的目标DOM元素；

**.this和event.target都是dom对象**

如果要使用jquey中的方法可以将他们转换为jquery对象。比如this和**$(this)**的使用、event.target和$(event.target)的使用；



### 7 自定义事件

#### 7-1 jQuery自定义事件之trigger事件

众所周知类似于mousedown、click、keydown等等这类型的事件都是浏览器提供的，通俗叫原生事件，这类型的事件是需要有交互行为才能被触发。

在jQuery通过on方法绑定一个原生事件

```
$('#elem').on('click', function() {
    alert("触发系统事件")
 });
```

alert需要执行的条件：必须有用户点击才可以。如果不同用户交互是否能在某一时刻自动触发该事件呢？ 正常来说是不可以的，但是jQuery解决了这个问题，提供了一个trigger方法来触发浏览器事件

所以我们可以这样：

```
$('#elem').trigger('click');
```

在绑定on的事件元素上，通过trigger方法就可以调用到alert了，挺简单！

**再来看看.trigger是什么？**

> 简单来讲就是：根据绑定到匹配元素的给定的事件类型（第一个参数）执行所有的处理程序和行为



trigger除了能够触发浏览器事件，同时还支持自定义事件，并且自定义时间还支持传递参数

```
$('#elem').on('Aaron', function(event,arg1,arg2) {
    alert("自触自定义时间")
 });
$('#elem').trigger('Aaron',['参数1','参数2'])
```

**trigger触发浏览器事件与自定义事件区别？**

- **自定义事件对象，是jQuery模拟原生实现的**

- **自定义事件可以传递参数**

  ​


####7-2 jQuery自定义事件之triggerHandler事件

trigger事件还有一个特性：**会在DOM树上冒泡**，所以如果要阻止冒泡就需要在事件处理程序中返回false或调用事件对象中的.stopPropagation() 方法可以使事件停止冒泡

trigger事件是具有触发原生与自定义能力的，但是存在一个不可避免的问题**： 事件对象event无法完美的实现**，毕竟一个是浏览器给的，一个是自己模拟的。尽管 .trigger() 模拟事件对象，但是它并没有完美的复制自然发生的事件，若要触发通过 jQuery 绑定的事件处理函数，而不触发原生的事件，使用.triggerHandler() 来代替

triggerHandler与trigger的用法是一样的，重点看不同之处：

- triggerHandler不会触发浏览器的默认行为，.triggerHandler( "submit" )将不会调用表单上的.submit()
- .trigger() 会影响**所有与 jQuery 对象相匹配的元素**，而 .triggerHandler() **仅影响第一个匹配到的元素**
- 使用 .triggerHandler() 触发的事件，并不会在 DOM 树中向上冒泡。 如果它们不是由目标元素直接触发的，那么它就不会进行任何处理
- 与普通的方法返回 jQuery 对象(这样就能够使用链式用法)相反，.triggerHandler() 返回最后一个处理的事件的返回值。如果没有触发任何事件，会返回 undefined