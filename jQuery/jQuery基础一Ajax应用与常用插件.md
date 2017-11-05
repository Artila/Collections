## jQuery基础一Ajax应用与常用插件

### 1  jQuery 实现Ajax应用 

#### 1-1 使用load()方法异步请求数据

使用`load()`方法通过Ajax请求加载服务器中的数据，并把返回的数据放置到指定的元素中，它的调用格式为：

`load(url,[data],[callback])`

参数url为加载服务器地址，可选项data参数为请求时发送的数据，callback参数为数据请求成功后，执行的回调函数。

例如，点击“加载”按钮时，向服务器请求加载一个指定页面的内容，加载成功后，将数据内容显示在<div>元素中，并将加载按钮变为不可用。如下图所示：

[![img](http://img.mukewang.com/52dccb920001d2d505970337.jpg)](http://img.mukewang.com/52dccb920001d2d505970337.jpg)

在浏览器中显示的效果：

[![img](http://img.mukewang.com/52dccbaf0001c21507380393.jpg)](http://img.mukewang.com/52dccbaf0001c21507380393.jpg)

从图中可以看出，当点击“加载”按钮时，通过调用`load()`方法向服务器请求加载fruit.html文件中的内容，当加载成功后，先显示数据，并将按钮变为不可用。

```javascript
var $this = $(this);
this其实是一个html 元素。 
$this 只是个变量名，加$是为说明其是个jquery对象。 
而$(this)是个转换，将this表示的dom对象转为jquery对象，这样就可以使用jquery提供的方法操作。

作用：把当前对象保存起来，便于后边的使用。
```



#### 1-2 使用getJSON()方法异步加载JSON格式数据

使用`getJSON()`方法可以通过Ajax异步请求的方式，获取服务器中的数据，并对获取的数据进行解析，显示在页面中，它的调用格式为：

`jQuery.getJSON(url,[data],[callback])`**或**`$.getJSON(url,[data],[callback])`

其中，url参数为请求加载json格式文件的服务器地址，可选项data参数为请求时发送的数据，callback参数为数据请求成功后，执行的回调函数。

例如，点击页面中的“加载”按钮，调用`getJSON()`方法获取服务器中JSON格式文件中的数据，并遍历数据，将指定的字段名内容显示在页面中。如下图所示：

[![img](http://img.mukewang.com/52dcced70001f67806010370.jpg)](http://img.mukewang.com/52dcced70001f67806010370.jpg)

在浏览器中显示的效果：

[![img](http://img.mukewang.com/52dccefe0001c87005860341.jpg)](http://img.mukewang.com/52dccefe0001c87005860341.jpg)

从图中可以看出，当点击“加载”按钮时，通过`getJSON()`方法调用服务器中的sport.json文件，获取返回的data文件数据，并遍历该数据对象，以`data[“name”]`取出数据中指定的内容，显示在页面中。

```javascript
$.each(data, function (index, sport){})中为什么$可以遍历数据?
  
jq有两种传入对象的方式  把data理解成一个对象  each 是一个函数 
第一种   $(obj).each(function(index,value){})  在对象上调用each 函数 
第二种   $.each(obj,function(index,value){})  这种是把 obj 当作对象传入函数 each 道理是一样的。

jQuery.each(array, callback)

$.each(data, function (index, sport){}) 其中data为json里的那个数组，index为对应数组的索引，sport为对应索引的值。
而这个索引对应的值sport在数组里又是个对象，我们要的是该对象的name属性的值，所以要这样写sport.name，而name又是字符串所以要变成sport["name"]。

对象调用属性有两种写法。
第一: obj.name;
第二: 一般针对属性是字符串的形式 obj[name]。
```



#### 1-3 使用getScript()方法异步加载并执行js文件 

使用`getScript()`方法异步请求并执行服务器中的JavaScript格式的文件，它的调用格式如下所示：

`jQuery.getScript(url,[callback])`或`$.getScript(url,[callback])`

参数url为服务器请求地址，可选项callback参数为请求成功后执行的回调函数。

例如，点击“加载”按钮，调用`getScript()`加载并执行服务器中指定名称的JavaScript格式的文件，并在页面中显示加载后的数据内容，如下图所示：

[![img](http://img.mukewang.com/52dcd433000151e606000305.jpg)](http://img.mukewang.com/52dcd433000151e606000305.jpg)

在浏览器中显示的效果：

[![img](http://img.mukewang.com/52dcd44e000145de06380392.jpg)](http://img.mukewang.com/52dcd44e000145de06380392.jpg)

从图中可以看出，当点击“加载”按钮调用`getScript()`方法加载服务器中的JavaScript格式文件后，自动执行文件代码，将数据内容显示在<ul>元素中。

```
javacscript文件自带遍历和插入代码，所以在回调函数里面就无需再进行这两步,并且这种方法是从服务器上纯粹的获取数据。
```



#### 1-4 使用get()方法以GET方式从服务器获取数据  

使用`get()`方法时，采用GET方式向服务器请求数据，并通过方法中回调函数的参数返回请求的数据，它的调用格式如下：

`$.get(url,[callback])`

参数url为服务器请求地址，可选项callback参数为请求成功后执行的回调函数。

例如，当点击“加载”按钮时，调用`get()`方法向服务器中的一个.php文件以GET方式请求数据，并将返回的数据内容显示在页面中，如下图所示：

[![img](http://img.mukewang.com/52dcd5b1000161ce05970338.jpg)](http://img.mukewang.com/52dcd5b1000161ce05970338.jpg)

在浏览器中显示的效果：

[![img](http://img.mukewang.com/52dcd5d900010aaf06440326.jpg)](http://img.mukewang.com/52dcd5d900010aaf06440326.jpg)

从图中可以看出，通过`$.get()`方法向服务器成功请求数据后，在回调函数中通过data参数传回请求的数据，并以data.name格式访问数据中各项的内容。

```
json设置从服务器获取数据的类型，所以得到的数据格式为json类型的。

默认get从服务器获取到的数据是 字符串类型。
```



#### 1-5 使用post()方法以POST方式从服务器发送数据

与`get()`方法相比，`post()`方法多用于以POST方式向服务器发送数据，服务器接收到数据之后，进行处理，并将处理结果返回页面，调用格式如下：

`$.post(url,[data],[callback])`

参数url为服务器请求地址，可选项data为向服务器请求时发送的数据，可选项callback参数为请求成功后执行的回调函数。

例如，在输入框中录入一个数字，点击“检测”按钮，调用`post()`方法向服务器以POST方式发送请求，检测输入值的奇偶性，并显示在页面中，如下图所示：

[![img](http://img.mukewang.com/52dcd7430001e25004690464.jpg)](http://img.mukewang.com/52dcd7430001e25004690464.jpg)

在浏览器中显示的效果：

[![img](http://img.mukewang.com/52dcd77200010b4c05450336.jpg)](http://img.mukewang.com/52dcd77200010b4c05450336.jpg)

从图中可以看出，当点击“检测”按钮时，获取输入框中的值，并将该值使用`$.post()`方法一起发送给服务器，服务器接收该值后并进行处理，最后返回处理结果。



#### 1-6 使用serialize()方法序列化表单元素值

使用`serialize()`方法可以将表单中有name属性的元素值进行序列化，生成标准URL编码文本字符串，直接可用于ajax请求，它的调用格式如下：

`$(selector).serialize()`

其中selector参数是一个或多个表单中的元素或表单元素本身。

例如，在表单中添加多个元素，点击“序列化”按钮后，调用`serialize()`方法，将表单元素序列化后的标准URL编码文本字符串显示在页面中，如下图所示：

[![img](http://img.mukewang.com/52dcd9470001b1e705400481.jpg)](http://img.mukewang.com/52dcd9470001b1e705400481.jpg)

在浏览器中显示的效果：

[![img](http://img.mukewang.com/52dcd9660001637f05610308.jpg)](http://img.mukewang.com/52dcd9660001637f05610308.jpg)

从图中可以看出，当点击“序列化”按钮后，调用表单元素本身的`serialize()`方法，将表单中元素全部序列化，生成标准URL编码，各元素间通过&号相联。



#### 1-7

#### 1-8

#### 1-9



### 2  jQuery 常用插件

#### 2-1

#### 2-2 

#### 2-3 

#### 2-4  

#### 2-5

#### 2-6

#### 2-7

#### 2-8

#### 2-9


### 3  jQuery UI型插件

#### 3-1

#### 3-2 

#### 3-3 

#### 3-4  

#### 3-5

#### 3-6

#### 3-7

#### 3-8

#### 3-9


### 4  jQuery 工具类函数

#### 4-1

#### 4-2 

#### 4-3 

#### 4-4  

#### 4-5

#### 4-6

#### 4-7

#### 4-8

#### 4-9
