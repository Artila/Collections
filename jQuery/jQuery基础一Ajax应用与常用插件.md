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



#### 1-7 使用ajax()方法加载服务器数据

使用`ajax()`方法是最底层、功能最强大的请求服务器数据的方法，它不仅可以获取服务器返回的数据，还能向服务器发送请求并传递数值，它的调用格式如下：

`jQuery.ajax([settings])`**或**`$.ajax([settings])`

其中参数settings为发送ajax请求时的配置对象，在该对象中，url表示服务器请求的路径，data为请求时传递的数据，dataType为服务器返回的数据类型，success为请求成功的执行的回调函数，type为发送数据请求的方式，默认为get。

例如，点击页面中的“加载”按钮，调用`ajax()`方法向服务器请求加载一个txt文件，并将返回的文件中的内容显示在页面，如下图所示：

[![img](http://img.mukewang.com/52dcdb5000014e9804600419.jpg)](http://img.mukewang.com/52dcdb5000014e9804600419.jpg)

在浏览器中显示的效果：

[![img](http://img.mukewang.com/52dcdb6b00010eea05990345.jpg)](http://img.mukewang.com/52dcdb6b00010eea05990345.jpg)

从图中可以看出，当点击“加载”按钮时，调用`$.ajax()`方法请求服务器中txt文件，当请求成功时调用success回调函数，获取传回的数据，并显示在页面中。

```
默认的请求方式是GET，但是这里一定注意type：“post”意味着就是POST请求方式，这样它代表的就是提交数据给指定的服务器处理；type：“get”意味着就是GET请求方式，这样它代表的就是从指定的服务器中获取数据（不处理），就像本节的范例，就是只获取数据并不处理数据，而下面图片中的代码是需要处理的，也就是提交一个数据（或偶数或奇数），交予服务器端封装的函数来处理，处理完成后再返回是偶数或奇数。
```



#### 1-8 使用ajaxSetup()方法设置全局Ajax默认选项

使用`ajaxSetup()`方法可以设置Ajax请求的一些全局性选项值，设置完成后，后面的Ajax请求将不需要再添加这些选项值，它的调用格式为：

`jQuery.ajaxSetup([options])`**或**`$.ajaxSetup([options])`

可选项options参数为一个对象，通过该对象设置Ajax请求时的全局选项值。

例如，先调用`ajaxSetup()`方法设置全局的Ajax选项值，再点击两个按钮，分别使用`ajax()`方法请求不同的服务器数据，并将数据内容显示在页面，如下图所示：

[![img](http://img.mukewang.com/52dcdce60001de2604780449.jpg)](http://img.mukewang.com/52dcdce60001de2604780449.jpg)

在浏览器中显示的效果：

[![img](http://img.mukewang.com/52dcdd090001ccfd06390382.jpg)](http://img.mukewang.com/52dcdd090001ccfd06390382.jpg)

从图中可以看出，使用`ajaxSetup()`方法设置了Ajax请求时的一些全局性的配置选项后，在两次调用ajax请求服务器txt文件时，只需要设置url地址即可。



#### 1-9 使用ajaxStart()和ajaxStop()方法

`ajaxStart()`和`ajaxStop()`方法是绑定Ajax事件。ajaxStart()方法用于在Ajax请求发出前触发函数，ajaxStop()方法用于在Ajax请求完成后触发函数。它们的调用格式为：

`$(selector).ajaxStart(function())`**和**`$(selector).ajaxStop(function())`

其中，两个方法中括号都是绑定的函数，当发送Ajax请求前执行`ajaxStart()`方法绑定的函数，请求成功后，执行ajaxStop ()方法绑定的函数。

例如，在调用`ajax()`方法请求服务器数据前，使用动画显示正在加载中，当请求成功后，该动画自动隐藏，如下图所示：

[![img](http://img.mukewang.com/52dcfb3a0001746d06020435.jpg)](http://img.mukewang.com/52dcfb3a0001746d06020435.jpg)

在浏览器中显示的效果：

[![img](http://img.mukewang.com/52dcfb5500013ffa06500337.jpg)](http://img.mukewang.com/52dcfb5500013ffa06500337.jpg)

从图中可以看出，由于使用`ajaxStart()`和`ajaxStop()`方法绑定了动画元素，因此，在开始发送Ajax请求时，元素显示，请求完成时，动画元素自动隐藏。

注意：该方法在1.8.2下使用是正常的



### 2  jQuery 常用插件

#### 2-1 表单验证插件——validate

该插件自带包含必填、数字、URL在内容的验证规则，即时显示异常信息，此外，还允许自定义验证规则，插件调用方法如下：

`$(form).validate({options})`

其中form参数表示表单元素名称，options参数表示调用方法时的配置对象，所有的验证规则和异常信息显示的位置都在该对象中进行设置。

例如，当点击表单中的“提交”按钮时，调用validate插件验证用户名输入是否符合规则，并将异常信息显示在页面中，如下图所示：

[![img](http://img.mukewang.com/52e474e70001b2cc04780576.jpg)](http://img.mukewang.com/52e474e70001b2cc04780576.jpg)

在浏览器中显示的效果：

[![img](http://img.mukewang.com/55ffc1b80001518c06010355.jpg)](http://img.mukewang.com/55ffc1b80001518c06010355.jpg)

从图中可以看出，在页面中导入了validate插件，当用户在输入框中录入用户名时，自动根据规则进入验证，并显示提示信息，验证成功后，表单才能提交。

```
注意：ruels:里面的那个email是表单控件的name，不是ID，它是根据name属性绑定元素节点

参数
required:true 必须有值，不能为空
remote:url 可以用于判断用户名等是否已经存在,服务器端输出true,表示验证通过
minlength:6 最小长度为6
maxlength:16 最大长度为16
rangelength:长度范围
range:[10,20] 数值范围在10-20之间
email:true 验证邮件
url:true 验证URL网址
dateISO:true 验证日期格式'yyyy-mm-dd'
digits:true 只能为数字
accept:'gif|jpg' 只接受gif或jpg为后缀的图片。常用于验证文件的扩展名
equalTo:'#pass' 与哪个表单字段的值相等，常用于验证重复输入密码
```



#### 2-2 表单插件——form 

通过表单form插件，调用`ajaxForm()`方法，实现ajax方式向服务器提交表单数据，并通过方法中的options对象获取服务器返回数据，调用格式如下：

`$(form). ajaxForm ({options})`

其中form参数表示表单元素名称；options是一个配置对象，用于在发送ajax请求过程，设置发送时的数据和参数。

例如，在页面中点击“提交”按钮，调用form插件的
`ajaxForm()`方法向服务器发送录入的用户名和密码数据，服务器接收后返回并显示在页面中，如下图所示：

[![img](http://img.mukewang.com/52e4861d000143ad04720449.jpg)](http://img.mukewang.com/52e4861d000143ad04720449.jpg)

在浏览器中显示的效果：

[![img](http://img.mukewang.com/52e4863b0001b62e07360383.jpg)](http://img.mukewang.com/52e4863b0001b62e07360383.jpg)

从图中可以看出，当点击“提交”按钮时，调用form表单插件中的ajaxForm()方法向指定的服务器以ajax方式发送数据，服务器接收后返回并将数据显示。



#### 2-3 图片灯箱插件——lightBox 

该插件可以用圆角的方式展示选择中的图片，使用按钮查看上下张图片，在加载图片时自带进度条，还能以自动播放的方式浏览图片，调用格式如下：

`$(linkimage).lightBox({options})`

其中linkimage参数为包含图片的<a>元素名称，options为插件方法的配置对象。

例如，以列表的方式在页面中展示全部的图片，当用户单击其中某张图片时，通过引入的图片插件，采用“灯箱”的方式显示所选的图片，如下图所示：

[![img](http://img.mukewang.com/52e488760001d36c05070495.jpg)](http://img.mukewang.com/52e488760001d36c05070495.jpg)

在浏览器中显示的效果：

[![img](http://img.mukewang.com/52e4889600013b1107220457.jpg)](http://img.mukewang.com/52e4889600013b1107220457.jpg)

从图中可以看出，当用户点击“我的相册”中某一张图片时，则采用“灯箱”的方式显示选中图片，在显示图片时，还可以切换上下张和自动播放及关闭图片。



#### 2-4 图片放大镜插件——jqzoom  

在调用jqzoom图片放大镜插件时，需要准备一大一小两张一样的图片，在页面中显示小图片，当鼠标在小图片中移动时，调用该插件的`jqzoom()`方法，显示与小图片相同的大图片区域，从而实现放大镜的效果，调用格式如下：

`$(linkimage).jqzoom({options})`

其中linkimage参数为包含图片的<a>元素名称，options为插件方法的配置对象。

例如，在页面中，添加一个被<a>元素包含的图片元素，当在图片元素中移动鼠标时，在图片的右边，将显示放大后的所选区域效果，如下图所示：

[![img](http://img.mukewang.com/52e49c2500014a9b04630338.jpg)](http://img.mukewang.com/52e49c2500014a9b04630338.jpg)

在浏览器中显示的效果：

[![img](http://img.mukewang.com/52e49c43000157d205720384.jpg)](http://img.mukewang.com/52e49c43000157d205720384.jpg)

从图中可以看出，当在小图片中移动鼠标时，将调用放大镜插件的`jqzoom()`方法，在图片的右侧显示与小图片所选区域相同的放大区域，实现放大镜的效果。



#### 2-5 cookie插件——cookie

使用cookie插件后，可以很方便地通过cookie对象保存、读取、删除用户的信息，还能通过cookie插件保存用户的浏览记录，它的调用格式为：

**保存：**`$.cookie(key，value)`**；读取：**`$.cookie(key)`**，删除：**`$.cookie(key，null)`

其中参数key为保存cookie对象的名称，value为名称对应的cookie值。

例如，当点击“设置”按钮时，如果是“否保存用户名”的复选框为选中状态时，则使用cookie对象保存用户名，否则，删除保存的cookie用户名，如下图所示：

[![img](http://img.mukewang.com/52e49d8100016e2c06280481.jpg)](http://img.mukewang.com/52e49d8100016e2c06280481.jpg)

在浏览器中显示的效果：

[![img](http://img.mukewang.com/52e49db900011a7706060340.jpg)](http://img.mukewang.com/52e49db900011a7706060340.jpg)

从图中可以看出，由于在点击“设置”按钮时，选择了保存用户名，因此，输入框中的值被cookie保存，下次打开浏览器时，直接获取并显示保存的cookie值。

```
expires:　　有限日期，可以是一个整数或一个日期(单位：天)。　　
　          这个地方也要注意，如果不设置这个东西，浏览器关闭之后此cookie就失效了
path:　　　 cookie值保存的路径，默认与创建页路径一致。
domin:　　  cookie域名属性，默认与创建页域名一样。　　
            这个地方要相当注意，跨域的概念，如果要主域名二级域名有效则要设置　　".xxx.com"
secrue:　　 一个布尔值，表示传输cookie值时，是否需要一个安全协议。
```



#### 2-6 搜索插件——autocomplete

搜索插件的功能是通过插件的`autocomplete()`方法与文本框相绑定，当文本框输入字符时，绑定后的插件将返回与字符相近的字符串提示选择，调用格式如下：

`$(textbox).autocomplete(urlData,[options]);`

其中，textbox参数为文本框元素名称，urlData为插件返回的相近字符串数据，可选项参数options为调用插件方法时的配置对象。

例如，当用户在文本框输入内容时，调用搜索插件的`autocomplete()`方法返回与输入内容相匹配的字符串数据，显示在文本框下，提示选择，如下图所示：

[![img](http://img.mukewang.com/52e49eb90001024606410464.jpg)](http://img.mukewang.com/52e49eb90001024606410464.jpg)

在浏览器中显示的效果：

[![img](http://img.mukewang.com/52e49ed2000183f806300354.jpg)](http://img.mukewang.com/52e49ed2000183f806300354.jpg)

从图中可以看出，当文本框与搜索插件相绑定后，输入任意字符时，都将返回与之相匹配的字符串，提示用户选择，文本框在空白双击时，显示全部提示信息。

```
minChars (Number) 
在触发autoComplete前用户至少需要输入的字符数，Default:1，如果设为0，在输入框内双击或者删除输入框内内容时显示列表。 

max (Number):autocomplete
下拉显示项目的个数，Default: 10.

 formatItem (Function) 
为每个要显示的项目使用高级标签.即对结果中的每一行都会调用这个函数,返回值将用LI元素包含显示在下拉列表中.Autocompleter会提供三个参数(row, i, max): 返回的结果数组, 当前处理的行数(即第几个项目,是从1开始的自然数), 当前结果数组元素的个数即项目的个数.Default: none, 表示不指定自定义的处理函数,这样下拉列表中的每一行只包含一个值. 

 formatResult (Function) 
和formatItem类似,但可以将将要输入到input文本框内的值进行格式化.同样有三个参数,和formatItem一样.Default: none,表示要么是只有数据,要么是使用formatItem提供的值.
```



#### 2-7 右键菜单插件——contextmenu

右键菜单插件可以绑定页面中的任意元素，绑定后，选中元素，点击右键，便通过该插件弹出一个快捷菜单，点击菜单各项名称执行相应操作，调用代码如下：

`$(selector).contextMenu(menuId,{options});`

Selector参数为绑定插件的元素，meunId为快捷菜单元素，options为配置对象。

例如，选中页面<textarea>元素，点击右键，弹出插件绑定的快捷菜单，点击菜单中的各个选项，便在页面中显示操作的对应名称。如下图所示：

[![img](http://img.mukewang.com/52e49fde0001919605370483.jpg)](http://img.mukewang.com/52e49fde0001919605370483.jpg)

在浏览器中显示的效果：

[![img](http://img.mukewang.com/52e49ff80001ed4f06910367.jpg)](http://img.mukewang.com/52e49ff80001ed4f06910367.jpg)

从图中可以看出，当文本框与右键菜单通过插件`contextmenu()`方法绑定后，选中文本框，点击右键时，弹出快捷菜单，点击“新建”选项时，显示操作对应内容。



#### 2-8 自定义对象级插件——lifocuscolor插件

自定义的lifocuscolor插件可以在<ul>元素中，鼠标在表项<li>元素移动时，自定义其获取焦点时的背景色，即定义<li>元素选中时的背景色，调用格式为：

`$(Id).focusColor(color)`

其中，参数Id表示<ul>元素的Id号，color表示<li>元素选中时的背景色。

例如，在页面中，调用自定义的lifocuscolor插件，自定义<li>元素选中时的背景色，如下图所示：

[![img](http://img.mukewang.com/52e4a100000199ac04200306.jpg)](http://img.mukewang.com/52e4a100000199ac04200306.jpg)

在浏览器中显示的效果：

[![img](http://img.mukewang.com/52e4a11d0001669107090375.jpg)](http://img.mukewang.com/52e4a11d0001669107090375.jpg)

从图中可以看出，当<ul>元素调用`focusColor()`方法绑定自定义的插件之后，当鼠标在<li>元素间移动时，显示自定义的背景色。



#### 2-9 自定义类级别插件—— twoaddresult

通过调用自定义插件twoaddresult中的不同方法，可以实现对两个数值进行相加和相减的运算，导入插件后，调用格式分别为：

`$.addNum(p1,p2) `**和**` $.subNum(p1,p2)`

上述调用格式分别为计算两数值相加和相减的结果，p1和p2为任意数值。

例如，在页面的两个文本框中输入任意数值，点击“计算”按钮调用自定义插件中`$.addNum()`方法，计算两数值的和并将结果显示在另一文本框中，如下图所示：

[![img](http://img.mukewang.com/52e4a2230001185304660432.jpg)](http://img.mukewang.com/52e4a2230001185304660432.jpg)

在浏览器中显示的效果：

[![img](http://img.mukewang.com/52e4a23c0001c1cb06890362.jpg)](http://img.mukewang.com/52e4a23c0001c1cb06890362.jpg)

从图中可以看出，当点击“计算”按钮时，调用了自定义插件中的`$.addNum()`方法计算两个文本框中输入数值的和，并将该值显示在另一文本框中。

```
jQuery为开发插件提拱了两个方法，分别是：

1. jQuery.extend();
它是为jQuery类添加类方法，可以理解为添加静态方法。如：

jQuery.extend({

　　min: function(a, b) { return a < b ? a : b; },

　　max: function(a, b) { return a > b ? a : b; }

});

jQuery.min(2,3); //  2 
jQuery.max(4,5); //  5

2. jQuery.fn.extend();
$.fn是指jQuery的命名空间，fn上的成员(方法function及属性property)，会对jQuery实例每一个有效。
```




### 3  jQuery UI型插件

#### 3-1 拖曳插件——draggable

拖曳插件draggable的功能是拖动被绑定的元素，当这个jQuery UI插件与元素绑定后，可以通过调用`draggable()`方法，实现各种拖曳元素的效果，调用格式如下：

`$(selector). draggable({options})`

options参数为方法调用时的配置对象，根据该对象可以设置各种拖曳效果，如“containment”属性指定拖曳区域，“axis”属性设置拖曳时的坐标方向。

例如，在页面中的<div>元素中添加两个子类<div>，通过与拖曳插件绑定，这两个子类<div>元素只能在外层的父<div>元素中任意拖曳，如下图所示：

[![img](http://img.mukewang.com/52e4b50c0001545304260177.jpg)](http://img.mukewang.com/52e4b50c0001545304260177.jpg)

在浏览器中显示的效果：

[![img](http://img.mukewang.com/52e4b5240001794706620379.jpg)](http://img.mukewang.com/52e4b5240001794706620379.jpg)

从图中可以看出，由于使用jQuery UI插件draggable绑定了两个子类<div>元素，并将配置对象的“containment”属性值设为“parent”，因此，这两个子类<div>元素只能在外层的父框中实现任意拖曳。



#### 3-2 放置插件——droppable 

除使用draggable插件拖曳任意元素外，还可以调用droppable UI插件将拖曳后的任意元素放置在指定区域中，类似购物车效果，调用格式如下：

`$(selector).droppable({options})`

selector参数为接收拖曳元素，options为方法的配置对象，在对象中，drop函数表示当被接收的拖曳元素完全进入接收元素的容器时，触发该函数的调用。

例如，在页面中，通过调用droppable插件将“产品区”中的元素拖曳至“购物车”中，同时改变“购物车”的背景色和数量值，如下图所示：

[![img](http://img.mukewang.com/52e4b7e000012af004800447.jpg)](http://img.mukewang.com/52e4b7e000012af004800447.jpg)

在浏览器中显示的效果：

[![img](http://img.mukewang.com/52e4b7fa0001435707090448.jpg)](http://img.mukewang.com/52e4b7fa0001435707090448.jpg)

从图中可以看出，先调用draggable插件任意拖曳“产品区”的元素，然后，调用droppable插件绑定“购物车”中接收元素，当“产品区”元素完全拖曳至“购物车”时，触发定义的drop函数，改变“购物车”中背景色和总数量值。



#### 3-3 拖曳排序插件——sortable 

拖曳排序插件的功能是将序列元素（例如<option>、<li>）按任意位置进行拖曳从而形成一个新的元素序列，实现拖曳排序的功能，它的调用格式为：

`$(selector).sortable({options});`

selector参数为进行拖曳排序的元素，options为调用方法时的配置对象，

例如，在页面中，通过加载sortable插件将<ul>元素中的各个<li>表项实现拖曳排序的功能，如下图所示：

[![img](http://img.mukewang.com/52e4bb9b0001075303890385.jpg)](http://img.mukewang.com/52e4bb9b0001075303890385.jpg)

在浏览器中显示的效果：

[![img](http://img.mukewang.com/52e4bbb60001ae1606600393.jpg)](http://img.mukewang.com/52e4bbb60001ae1606600393.jpg)

从图中可以看出，由于使用sortable插件绑定了<ul>元素，并设置了拖曳时的透明度，因此，<ul>中的各个<li>元素则能指定的透明度进行任意的拖曳排序。



#### 3-4 面板折叠插件——accordion  

面板折叠插件可以实现页面中指定区域类似“手风琴”的折叠效果，即点击标题时展开内容，再点另一标题时，关闭已展开的内容，调用格式如下：

`$(selector).accordion({options});`

其中，参数selector为整个面板元素，options参数为方法对应的配置对象。

例如，通过accordion插件展示几个相同区域面板的折叠效果，如下图所示：

[![img](http://img.mukewang.com/52e4bd2c0001e58b03680467.jpg)](http://img.mukewang.com/52e4bd2c0001e58b03680467.jpg)

在浏览器中显示的效果：

[![img](http://img.mukewang.com/52e4bd4a0001b4ea06500371.jpg)](http://img.mukewang.com/52e4bd4a0001b4ea06500371.jpg)

从图中可以看出，由于绑定了折叠面板插件，默认为第一个面板的内容为展示状态，点击第二个面板主题时，展示主题对应内容，同时关闭上一个面板内容。



#### 3-5 选项卡插件——tabs

使用选项卡插件可以将<ul>中的<li>选项定义为选项标题，在标题中，再使用<a>元素的“href”属性设置选项标题对应的内容，它的调用格式如下：

`$(selector).tabs({options});`

selector参数为选项卡整体外围元素，该元素包含选项卡标题与内容，options参数为`tabs()`方法的配置对象，通过该对象还能以ajax方式加载选项卡的内容。

例如，在页面中，添加选项卡的标题和内容元素，并绑定tabs插件，当点击标题时，以选项卡的方式切内容，如下图所示：

[![img](http://img.mukewang.com/52e4bea70001795c04470526.jpg)](http://img.mukewang.com/52e4bea70001795c04470526.jpg)

在浏览器中显示的效果：

[![img](http://img.mukewang.com/52e4bec4000174c706760344.jpg)](http://img.mukewang.com/52e4bec4000174c706760344.jpg)

从图中可以看出，在`tabs()`方法的配置对象中，通过“fx”属性设置了选项卡切换时的效果，“event”属性设置鼠标也可以切换选项卡，因此，当鼠标在移动至两个选项卡标题时，对应内容以动画的效果自动切换。



#### 3-6 对话框插件——dialog

对话框插件可以用动画的效果弹出多种类型的对话框，实现JavaScript代码中`alert()`和`confirm()`函数的功能，它的调用格式为：

`$(selector).dialog({options});`

selector参数为显示弹出对话框的元素，通常为<div>，options参数为方法的配置对象，在对象中可以设置对话框类型、“确定”、“取消”按钮执行的代码等。

例如，当点击“提交”按钮时，如果文本框中的内容为空，则通过dialog插件弹出提示框，提示输入内容不能为空，如下图所示：

[![img](http://img.mukewang.com/52e4c1370001b0e805150562.jpg)](http://img.mukewang.com/52e4c1370001b0e805150562.jpg)

在浏览器中显示的效果：

[![img](http://img.mukewang.com/52e4c150000111de05350338.jpg)](http://img.mukewang.com/52e4c150000111de05350338.jpg)

从图中可以看出，当文本框的内容为空时，调用自定义的sys_Alert函数，在该函数中再调用dialog插件的`dialog()`方法，弹出带模式的显示信息对话框。



#### 3-7 菜单工具插件——menu

菜单工具插件可以通过<ul>创建多级内联或弹出式菜单，支持通过键盘方向键控制菜单滑动，允许为菜单的各个选项添加图标，调用格式如下：

`$(selector).menu({options});`

selector参数为菜单列表中最外层<ul>元素，options为`menu()`方法的配置对象。

例如，在页面中，通过<ul>元素内联的方式构建一个三层结构的导航菜单，并将最外层<ul>元素通过`menu()`方法绑定插件，实现导航菜单的功能，如下图所示：

[![img](http://img.mukewang.com/52e4c2c10001b1a705160466.jpg)](http://img.mukewang.com/52e4c2c10001b1a705160466.jpg)

在浏览器中显示的效果：

[![img](http://img.mukewang.com/52e4c2dd0001b82505350338.jpg)](http://img.mukewang.com/52e4c2dd0001b82505350338.jpg)

从图中可以看出，通过<ul>内嵌的方式，构建一个三层结构的导航菜单，将<li>元素的class属性值设为“ui-state-disabled”，可将菜单选项置为不可用状态。



#### 3-8 微调按钮插件——spinner

微调按钮插件不仅能在文本框中直接输入数值，还可以通过点击输入框右侧的上下按钮修改输入框的值，还支持键盘的上下方向键改变输入值，调用格式如下：

`$(selector).spinner({options});`

selector参数为文本输入框元素，可选项options参数为`spinner()`方法的配置对象，在该对象中，可以设置输入的最大、最小值，获取改变值和设置对应事件。

例如，将页面中的三个输入文本框都与微调插件相绑定，当改变三个文本框值时，对应的<div>元素的背景色也将随之发生变化，如下图所示：

[![img](http://img.mukewang.com/52e4c4ad0001d4e007610813.jpg)](http://img.mukewang.com/52e4c4ad0001d4e007610813.jpg)

在浏览器中显示的效果：

[![img](http://img.mukewang.com/52e4c4c70001205f05430305.jpg)](http://img.mukewang.com/52e4c4c70001205f05430305.jpg)

从图中可以看出，由于三个文本框输入元素都绑定微调插件，因此，无论是点击右侧的上下按钮，还是直接在文本框中输入值，都可以改变<div>元素的背景色。



#### 3-9 工具提示插件——tooltip

工具提示插件可以定制元素的提示外观，提示内容支持变量、Ajax远程获取，还可以自定义提示内容显示的位置，它的调用格式如下：

`$(selector).tooltip({options})`

其中selector为需要显示提示信息的元素，可选项参数options为`tooltip()`方法的配置对象，在该对象中，可以设置提示信息的弹出、隐藏时的效果和所在位置。

例如，将三个<a>元素与工具提示插件相绑定，当把鼠标移动在<a>元素内容时，以动画效果弹出对应的提示图片，移出时，图片自动隐藏，如下图所示：

[![img](http://img.mukewang.com/52e4c6360001f38506900450.jpg)](http://img.mukewang.com/52e4c6360001f38506900450.jpg)

在浏览器中显示的效果：

[![img](http://img.mukewang.com/52e4c6530001236e05960553.jpg)](http://img.mukewang.com/52e4c6530001236e05960553.jpg)

从图中可以看出，由于各个<a>元素都绑定了工具提示插件，因此，将在指定的位置并以动画效果展示各个<a>元素中title属性所对应的内容。




### 4  jQuery 工具类函数

#### 4-1 获取浏览器的名称与版本信息

在jQuery中，通过`$.browser`对象可以获取浏览器的名称和版本信息，如`$.browser.chrome`为true，表示当前为Chrome浏览器，`$.browser.mozilla`为true，表示当前为火狐浏览器，还可以通过`$.browser.version`方式获取浏览器版本信息。

例如，调用$.browser对象，获取浏览器名称并显示在页面中，如下图所示：

[![img](http://img.mukewang.com/52e4cf7f0001d48b03770322.jpg)](http://img.mukewang.com/52e4cf7f0001d48b03770322.jpg)

在浏览器中显示的效果：

[![img](http://img.mukewang.com/52e4cf9800015ac505710448.jpg)](http://img.mukewang.com/52e4cf9800015ac505710448.jpg)

从图中可以看出，通过调用`$.browser`对象，检测当前浏览器的所属类型，并根据类型不同，将浏览器名称保存至变量中，最后将变量的内容显示在页面中。

> 已在jQuery1.9中被移除，因为识别方法不准确。



#### 4-2 检测浏览器是否属于W3C盒子模型 

浏览器的盒子模型分为两类，一类为标准的w3c盒子模型，另一类为IE盒子模型，两者区别为在Width和Height这两个属性值中是否包含padding和border的值，w3c盒子模型不包含，IE盒子模型则包含，而在jQuery 中，可以通过`$.support.boxModel`对象返回的值，检测浏览器是否属于标准的w3c盒子模型。

例如，根据页面的特征，并通过`$.support.boxModel`属性的返回值，显示当前浏览器是否属于标准的w3c盒子模型，如下图所示：

[![img](http://img.mukewang.com/52e4d0e30001a31d03850323.jpg)](http://img.mukewang.com/52e4d0e30001a31d03850323.jpg)

在浏览器中显示的效果：

[![img](http://img.mukewang.com/52e4d0fa0001a4b704360230.jpg)](http://img.mukewang.com/52e4d0fa0001a4b704360230.jpg)

从图中可以看出，由于打开的页面属于标准的w3c盒子模型，因此，在调用`$.support.boxModel`属性时，返回true值。

> jq1.8中被移除



#### 4-3 检测对象是否为空 

在jQuery中，可以调用名为`$.isEmptyObject`的工具函数，检测一个对象的内容是否为空，如果为空，则该函数返回true，否则，返回false值，调用格式如下：

`$.isEmptyObject(obj);`

其中，参数obj表示需要检测的对象名称。

例如，通过`$.isEmptyObject()`函数，检测某个指定的对象是否为空，并将结果显示在页面中，如下图所示：

[![img](http://img.mukewang.com/52e4d28b0001b06c03810337.jpg)](http://img.mukewang.com/52e4d28b0001b06c03810337.jpg)

在浏览器中显示的效果：

[![img](http://img.mukewang.com/52e4d2a600014b6604360230.jpg)](http://img.mukewang.com/52e4d2a600014b6604360230.jpg)

从图中可以看出，由于对象obj的内容为空，因此，`$.isEmptyObject()`函数检测obj时，返回true，并根据返回的true值在页面中显示对应的文字内容。



#### 4-4 检测对象是否为原始对象  

调用名为`$.isPlainObject`的工具函数，能检测对象是否为通过`{}`或`new Object()`关键字创建的原始对象，如果是，返回true，否则，返回false值，调用格式为：

`$.isPlainObject (obj);`

其中，参数obj表示需要检测的对象名称。

例如，通过`$.isPlainObject()`函数，检测某个指定的对象是否为原始，并将结果显示在页面中，如下图所示：

[![img](http://img.mukewang.com/52e4d3be0001f46806190354.jpg)](http://img.mukewang.com/52e4d3be0001f46806190354.jpg)

在浏览器中显示的效果：

[![img](http://img.mukewang.com/52e4d3d500013c5004400241.jpg)](http://img.mukewang.com/52e4d3d500013c5004400241.jpg)

从图中可以看出，由于自定义的obj_a和obj_b都是属于原始对象，因此，当调用`$.isPlainObject()`函数检测这两个对象时，都返回true值。



#### 4-5 检测两个节点的包含关系

调用名为`$.contains`的工具函数，能检测在一个DOM节点中是否包含另外一个DOM节点，如果包含，返回true，否则，返回false值，调用格式为：

`$.contains (container, contained);`

参数container表示一个DOM对象节点元素，用于包含其他节点的容器，contained是另一个DOM对象节点元素，用于被其他容器所包含。

例如，通过`$.contains()`函数，检测两个节点对象间是否存在包含关系，并将检测的结果显示在页面中，如下图所示：

[![img](http://img.mukewang.com/52e4d5fb000122c104540369.jpg)](http://img.mukewang.com/52e4d5fb000122c104540369.jpg)

在浏览器中显示的效果：

[![img](http://img.mukewang.com/52e4d61a0001923f05080306.jpg)](http://img.mukewang.com/52e4d61a0001923f05080306.jpg)

从图中可以看出，`documentElement`是DOM根结点，而body只是根结点下的子节点之一，它们之间存在包含关系，因此，返回true值，并显示“包含”字样。



#### 4-6 字符串操作函数

调用名为`$.trim`的工具函数，能删除字符串中左右两边的空格符，但该函数不能删除字符串中间的空格，调用格式为：

`$.trim (str);`

参数str表示需要删除左右两边空格符的字符串。

例如，通过`$.trim()`函数，除掉一个两边均有空格符的字符串，并将其执行前后的字符长度都显示在页面中，如下图所示：

[![img](http://img.mukewang.com/52e4d72d0001a3c005630480.jpg)](http://img.mukewang.com/52e4d72d0001a3c005630480.jpg)

在浏览器中显示的效果：

[![img](http://img.mukewang.com/52e4d7470001abd205040320.jpg)](http://img.mukewang.com/52e4d7470001abd205040320.jpg)

从图中可以看出，由于文本框中的字符串前后分别有一个空格字符，因此，它的字符长度为13，调用`trim()`函数删除字符串前后空格之后，字符串长度则变为11。



#### 4-7 URL操作函数

调用名为`$.param`的工具函数，能使对象或数组按照`key/value`格式进行序列化编码，该编码后的值常用于向服务端发送URL请求，调用格式为：

`$.param (obj);`

参数obj表示需要进行序列化的对象，该对象也可以是一个数组，整个函数返回一个经过序列化编码后的字符串。

例如，通过`$.param()`函数，对指定的对象进行序列化编码，使其成为可执行传值的URL地址，并将该地址显示在页面中，如下图所示：

[![img](http://img.mukewang.com/52e4d8a6000185af04750370.jpg)](http://img.mukewang.com/52e4d8a6000185af04750370.jpg)

在浏览器中显示的效果：

[![img](http://img.mukewang.com/52e4d8c00001965504850276.jpg)](http://img.mukewang.com/52e4d8c00001965504850276.jpg)

从图中可以看出，通过调用工具函数`$.param()`可以将一个对象进行序列化并编码成可以在地址栏中直接执行的URL字符串。

param和serialize的区别是什么？前者是对任意的参数进行URL地址格式的转换，而后者仅属于form提交的数据转换。

```
.serialize()方法可以将表单中有name属性的元素值进行序列化，生成标准URL编码文本字符串，直接可用于ajax请求

$.param() 序列化对象或者数组,常用于向服务端发送URL请求
```



#### 4-8 使用$.extend()扩展工具函数

调用名为`$. extend`的工具函数，可以对原有的工具函数进行扩展，自定义类级别的jQuery插件，调用格式为：

`$.extend ({options});`

参数options表示自定义插件的函数内容。

例如，调用`$.extend()`函数，自定义一个用于返回两个数中最大值的插件，并在页面中将插件返回的最大值显示在页面中，如下图所示：

[![img](http://img.mukewang.com/52e4d9d30001eb7305670594.jpg)](http://img.mukewang.com/52e4d9d30001eb7305670594.jpg)

在浏览器中显示的效果：

[![img](http://img.mukewang.com/52e4d9ee0001aad904820268.jpg)](http://img.mukewang.com/52e4d9ee0001aad904820268.jpg)

从图中可以看出，当点击“计算”按钮时，先调用自定义插件中名为“MaxNum”的方法，计算并返回两个数值中的最大值，然后，将该值显示在页面中。



#### 4-9 使用$.extend()扩展Object对象

除使用`$.extend`扩展工具函数外，还可以扩展原有的`Object`对象，在扩展对象时，两个对象将进行合并，当存在相同属性名时，后者将覆盖前者，调用格式为：

`$.extend (obj1,obj2,…objN);`

参数obj1至objN表示需要合并的各个原有对象。

例如，调用`$.extend()`函数对两个已有的对象进行合并，并将合并后的新对象元素内容显示在页面中，如下图所示：

[![img](http://img.mukewang.com/52e4dbff0001c35405140338.jpg)](http://img.mukewang.com/52e4dbff0001c35405140338.jpg)

在浏览器中显示的效果：

[![img](http://img.mukewang.com/52e4dc1800012ce104770270.jpg)](http://img.mukewang.com/52e4dc1800012ce104770270.jpg)

从图中可以看出，当两个对象通过`$.extend()`函数扩展合并后，返回一个包含两个对象中全部属性元素的新对象，相同名称的“name”属性，前者被后者覆盖。

