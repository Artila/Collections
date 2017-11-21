## JavaScript实用技巧和小知识

## 一、JS整数的操作

使用|0和~~可以将浮点转成整型且效率方面要比同类的parseInt，Math.round 要快,在处理像素及动画位移等效果的时候会很有用。性能比较[见此](http://jsperf.com/math-floor-vs-math-round-vs-parseint/42)。

```javascript
var foo = (12.4 / 4.13) | 0; // 结果为3
var bar = ~~(12.4 / 4.13); // 结果为3
```

还有一个小技巧，就是！！2个叹号，可以讲一个值，快速转化为布尔值。你可以测试一下！

```javascript
var eee="eee";
alert(!!eee); // true
```

返回的是true,也就是说任何一个值前面加！！都可以恒等于true。除非这个值本来就是布尔值，或者为 undefined, null, 0, false, NaN, ''，因为我提到的 undefined, null, 0, false, NaN, '' ，这些，本来就是false,所以加了两个！！之后，还是fasle。

## 二、重写原生alert,记录弹框次数

```js
(function() {
  var oldAlert = window.alert,
      count = 0;
  window.alert = function(a) {
    count++;
    oldAlert(a + "\n You've called alert " + count + " times now. Stop, it's evil!");
  };
})();
alert("Hello Haorooms");
```

## 三、数字交换不声明中间变量的方法

两个数字之间做交换，我们的一般做法是声明一个中间变量，但是今天的做法比较奇葩，不用声明中间变量，看看是如何实现的！

```js
var a=1, b=2;
a = [b,b=a][0]; // 把a，b塞入数组，a的位置放上b，b的位置放上a
console.log('a:'+a+', b:'+b);

 //输出a:2,b:1
```

怎么样，这个方法是不是有一种焕然一新的感觉？

## 四、万物皆对象

在JavaScript的世界，万物皆对象。除了null和undefined，其他基本类型数字，字符串和布尔值都有对应有包装对象。对象的一个特征是你可以在它身上直接调用方法。

对于数字基本类型，当试图在其身上调用toString方法会失败，但用括号括起来后再调用就不会失败了，内部实现是用相应的包装对象将基本类型转为对象。所以(1).toString()相当于new Number(1).toString()。因此，你的确可以把基本类型数字，字符串，布尔等当对象使用的，只是注意语法要得体。

同时我们注意到，JavaScript中数字是不分浮点和整形的，所有数字其实均是浮点类型，只是把小数点省略了而以，比如你看到的1可以写成1.，这也就是为什么当你试图1.toString()时会报错，所以正确的写法应该是这样：1..toString()，或者如上面所述加上括号，这里括号的作用是纠正JS解析器，不要把1后面的点当成小数点。内部实现如上面所述，是将1.用包装对象转成对象再调用方法。

## 五、If语句的变形

当你需要写一个if语句的时候，不妨尝试另一种更简便的方法，用JavaScript中的逻辑操作符来代替。

```js
var day = (new Date).getDay() === 0;
//传统if语句
if (day) {
    alert('Today is Sunday!');
};
//运用逻辑与代替if
day&&alert('Today is Sunday!');
```

比如上面的代码，首先得到今天的日期，如果是星期天，则弹窗，否则什么也不做。我们知道逻辑操作存在短路的情况，对于逻辑与表达式，只有两者都真才结果才为真，如果前面的day变量被判断为假了，那么对于整个与表达式来说结果就是假，所以就不会继续去执行后面的alert了，如果前面day为真，则还要继续执行后面的代码来确定整个表达式的真假。利用这点达到了if的效果。

对于传统的if语句，如果执行体代码超过了1 条语句，则需要加花括号，而利用逗号表达式，可以执行任意条代码而不用加花括号。

```js
if(true) alert(1),alert(2),console.log(3);
```

## 六、使用===，而不是==

我之前的一篇文章中写个 ==的隐性转换，请看：<http://www.haorooms.com/post/js_yinxingleixing>

==（或!=）操作符在需要的时候会自动执行类型转换。===（或!==）操作不会执行任何转换。它将比较值和类型，而且在速度上也被认为优于==。

```js
[10] === 10    // is false
[10] == 10     // is true
'10' == 10     // is true
'10' === 10    // is false
 [] == 0       // is true
 [] ===  0     // is false
 '' == false   // is true but true == "a" is false
 '' ===  false // is false
```

## 七、使用闭包实现私有变量

关于闭包，我之前也有个介绍：<http://www.haorooms.com/post/js_bb>

```js
function Person(name, age) {
    this.getName = function() { return name; };
    this.setName = function(newName) { name = newName; };
    this.getAge = function() { return age; };
    this.setAge = function(newAge) { age = newAge; };

    //未在构造函数中初始化的属性
    var occupation;
    this.getOccupation = function() { return occupation; };
    this.setOccupation = function(newOcc) { occupation = 
                         newOcc; };
}
```

## 八、创建对象的构造函数

```js
function Person(firstName, lastName){
    this.firstName =  firstName;
    this.lastName = lastName;
}

var Saad = new Person("Saad", "Mousliki");
```

## 九、小心使用typeof、instanceof和constructor

```js
var arr = ["a", "b", "c"];
typeof arr;            // return "object"
arr instanceof Array;  // true
arr.constructor();     // []
```

## 十、创建一个自调用函数（Self-calling Funtion）

这个经常被称为自调用匿名函数（Self-Invoked Anonymous Function）或者即时调用函数表达式（IIFE-Immediately Invoked Function Expression)。这是一个在创建后立即自动执行的函数，通常如下：

```js
(function(){
    // some private code that will be executed automatically
})();
(function(a,b){
    var result = a+b;
    return result;
})(10,20);
```

## 十一、从数组中获取一个随机项

```js
var items = [12, 548 , 'a' , 2 , 5478 , 'foo' , 8852, , 'Doe' , 2145 , 119];
var random = Math.floor(Math.random() * items.length);
var randomItem = items[random];
```

## 十二、在特定范围内获取一个随机数

这个代码片段在你想要生成测试数据的时候非常有用，比如一个在最小最大值之间的一个随机薪水值。

```js
var x = Math.floor(Math.random() * (max - min + 1)) + min;
```

## 十三、在0和设定的最大值之间生成一个数字数组

```js
var arr = [] , max = 100;
// 简写
for(var i = 0; arr.push(i++) < max;);  // arr = [0,1,2,3 ... 99]
// 展开
for (var i = 0; i < max; i++) {
  arr.push(i);
}
console.log(arr); // // arr = [0,1,2,3 ... 99]
```

## 十四、生成一个随机的数字字母字符串

```js
function generateRandomAlphaNum(len) {
    var rdmString = "";
    for( ; rdmString.length < len; rdmString  += Math.random().toString(36).substr(2));
    return  rdmString.substr(0, len);
}

//调用方法generateRandomAlphaNum(15);
generateRandomAlphaNum(15);
```

## 十五、打乱一个数字数组

```js
var numbers = [5, 458 , 120 , -215 , 228 , 400 , 122205, -85411];
numbers = numbers.sort( function() { 
  return Math.random() - 0.5;
});
/* the array numbers will be equal for example to [120, 5, 228, -215, 400, 458, -85411, 122205]  */
```

## 十六、 String的trim函数

我之前写个一个去掉空格的函数，请看：<http://www.haorooms.com/post/js_kong_ge>

这里的是这个

```js
String.prototype.trim = function(){
  return this.replace(/^\s+|\s+$/g, "");
};
```

## 十七、 附加（append）一个数组到另一个数组上

```js
var array1 = [12 , "foo" , {name: "Joe"} , -2458];

var array2 = ["Doe" , 555 , 100];

// 两种
[].concat(array1, array2); // array1 array2 不会变 

Array.prototype.push.apply(array1, array2); // array1会变

/* array1 = [12 , "foo" , {name "Joe"} , -2458 , "Doe" , 555 , 100] */
```

## 十八、将arguments对象转换成一个数组

```js
var argArray = Array.prototype.slice.call(arguments);
【译者注：arguments对象是一个类数组对象，但不是一个真正的数组】
```

## 十九、验证参数是否是数字（number）

```js
function isNumber(n){
    return !isNaN(parseFloat(n)) && isFinite(n);
}
```

## 二十、验证参数是否是数组

```js
function isArray(obj){
    return Object.prototype.toString.call(obj) === '[object Array]' ;
}
```

注意：如果toString()方法被重写了（overridden），你使用这个技巧就不能得到想要的结果了。或者你可以使用：

```js
Array.isArray(obj); // 这是一个新的array的方法
```

如果你不在使用多重frames的情况下，你还可以使用 instanceof 方法。但如果你有多个上下文，你就会得到错误的结果。

```js
var myFrame = document.createElement('iframe');
document.body.appendChild(myFrame);

var myArray = window.frames[window.frames.length-1].Array;
var arr = new myArray(a,b,10); // [a,b,10]

// instanceof will not work correctly, myArray loses his constructor
// constructor is not shared between frames
arr instanceof Array; // false
```

【译者注：关于如何判断数组网上有不少讨论，大家可以google一下。这篇就写的挺详细的。】

## 二十一、获取一个数字数组中的最大值或最小值

```js
var  numbers = [5, 458 , 120 , -215 , 228 , 400 , 122205, -85411];
var maxInNumbers = Math.max.apply(null, numbers);
var minInNumbers = Math.min.apply(null, numbers);
```

【译者注：这里使用了Function.prototype.apply方法传递参数的技巧】

## 二十二、清空一个数组

```js
var myArray = [12 , 222 , 1000 ];
myArray.length = 0; // myArray will be equal to [].
```

## 二十三、不要使用 delete 来删除一个数组中的项。

**使用 splice 而不要使用 delete 来删除数组中的某个项。使用 delete 只是用 undefined 来替换掉原有的项，并不是真正的从数组中删除。**

不要使用这种方式：

```js
var items = [12, 548 ,'a' , 2 , 5478 , 'foo' , 8852, , 'Doe' ,2154 , 119 ];
items.length; // return 11
delete items[3]; // return true
items.length; // return 11
/* items will be equal to [12, 548, "a", undefined × 1, 5478, "foo", 8852, undefined × 1, "Doe", 2154,       119]   */
```

而使用：

```js
var items = [12, 548 ,'a' , 2 , 5478 , 'foo' , 8852, , 'Doe' ,2154 , 119 ];
items.length; // return 11
items.splice(3,1) ;
items.length; // return 10
/* items will be equal to [12, 548, "a", 5478, "foo", 8852, undefined × 1, "Doe", 2154,       119]   */
```

**delete 方法应该被用来删除一个对象的某个属性。**

## 二十四、使用 length 来截短一个数组

跟上面的清空数组的方式类似，我们使用 length 属性来截短一个数组。

```js
var myArray = [12 , 222 , 1000 , 124 , 98 , 10 ];
myArray.length = 4; // myArray will be equal to [12 , 222 , 1000 , 124].
```

此外，如果你将一个数组的 length 设置成一个比现在大的值，那么这个数组的长度就会被改变，会增加新的 undefined 的项补上。 数组的 length 不是一个只读属性。

```
myArray.length = 10; // the new array length is 10
myArray[myArray.length - 1] ; // undefined
```

## 二十五、使用逻辑 AND/OR 做条件判断

同（五），if变形语句！

```js
var foo = 10;
foo == 10 && doSomething(); // 等价于 if (foo == 10) doSomething();
foo == 5 || doSomething(); // 等价于 if (foo != 5) doSomething();
```

逻辑 AND 还可以被使用来为函数参数设置默认值

```js
function doSomething(arg1){
    Arg1 = arg1 || 10; // 如果arg1没有被设置的话，Arg1将被默认设成10
}
```

## 二十六、使用 map() 方法来遍历一个数组里的项

关于map（）,我之前的一篇文章中也写过，具体请看：<http://www.haorooms.com/post/jquery_grep_join>

```js
var squares = [1,2,3,4].map(function (val) {
    return val * val;
});
// squares will be equal to [1, 4, 9, 16]
```

## 二十七、四舍五入一个数字，保留N位小数

```js
var num =2.443242342;
num = num.toFixed(4);  // num will be equal to 2.4432
```

## 二十八、浮点数问题

```js
0.1 + 0.2 === 0.3 // is false
9007199254740992 + 1 // is equal to 9007199254740992
9007199254740992 + 2 // is equal to 9007199254740994
```

为什么会这样？ 0.1+0.2等于0.30000000000000004。你要知道，所有的JavaScript数字在内部都是以64位二进制表示的浮点数，符合IEEE 754标准。更多的介绍，可以阅读这篇博文。你可以使用 toFixed() 和 toPrecision() 方法解决这个问题。

## 二十九、使用for-in遍历一个对象内部属性的时候注意检查属性

下面的代码片段能够避免在遍历一个对象属性的时候访问原型的属性

```js
for (var name in object) {
    if (object.hasOwnProperty(name)) {
        // do something with name
    }
}
```

关于js变量对象，除了for in之外，我后面文章中也有jquery的写法，具体请看：<http://www.haorooms.com/post/object_bjxh>

## 三十、 逗号操作符

```
var a = 0;
var b = ( a++, 99 );
console.log(a);  // a will be equal to 1
console.log(b);  // b is equal to 99
```

## 三十一、缓存需要计算和查询（calculation or querying）的变量

对于jQuery选择器，我们最好缓存这些DOM元素。

```js
var navright = document.querySelector('#right');
var navleft = document.querySelector('#left');
var navup = document.querySelector('#up');
var navdown = document.querySelector('#down');
```

## 三十二、在调用 isFinite()之前验证参数

```js
isFinite(0/0) ; // false
isFinite("foo"); // false
isFinite("10"); // true
isFinite(10);   // true
isFinite(undifined);  // false
isFinite();   // false
isFinite(null);  // true  !!!
```

## 三十三、避免数组中的负数索引（negative indexes）

```js
var numbersArray = [1,2,3,4,5];
var from = numbersArray.indexOf("foo") ;  // from is equal to -1
numbersArray.splice(from,2);    // will return [5]
```

确保调用 indexOf 时的参数不是负数。

## 三十四、基于JSON的序列化和反序列化（serialization and deserialization）

```js
var person = {name :'Saad', age : 26, department : {ID : 15, name : "R&D"} };
var stringFromPerson = JSON.stringify(person);
/* stringFromPerson is equal to "{"name":"Saad","age":26,"department":{"ID":15,"name":"R&D"}}"   */
var personFromString = JSON.parse(stringFromPerson);
/* personFromString is equal to person object  */
```

## 三十五、避免使用 eval() 和 Function 构造函数

使用 eval 和 Function 构造函数是非常昂贵的操作，因为每次他们都会调用脚本引擎将源代码转换成可执行代码。

```js
var func1 = new Function(functionCode);
var func2 = eval(functionCode);
```

## 三十六、避免使用 with()

使用 with() 会插入一个全局变量。因此，同名的变量会被覆盖值而引起不必要的麻烦。

## 三十七、避免使用 for-in 来遍历一个数组

避免使用这样的方式：

```js
var sum = 0;
for (var i in arrayNumbers) {
    sum += arrayNumbers[i];
}
```

更好的方式是：

```js
var sum = 0;
for (var i = 0, len = arrayNumbers.length; i < len; i++) {
    sum += arrayNumbers[i];
}
```

附加的好处是，i 和 len 两个变量的取值都只执行了一次，会比下面的方式更高效：

```
for (var i = 0; i < arrayNumbers.length; i++)
```

为什么？因为arrayNumbers.length每次循环的时候都会被计算。

## 三十八、在调用 setTimeout() 和 setInterval() 的时候传入函数，而不是字符串。

关于setTimeout，我之前也写过：<http://www.haorooms.com/post/js_setTimeout>

如果你将字符串传递给 setTimeout() 或者 setInterval()，这个字符串将被如使用 eval 一样被解析，这个是非常耗时的。

不要使用：

```js
setInterval('doSomethingPeriodically()', 1000);
setTimeOut('doSomethingAfterFiveSeconds()', 5000)
```

而用：

```js
setInterval(doSomethingPeriodically, 1000);
setTimeOut(doSomethingAfterFiveSeconds, 5000);
```

## 三十九、使用 switch/case 语句，而不是一长串的 if/else

在判断情况大于2种的时候，使用 switch/case 更高效，而且更优雅（更易于组织代码）。但在判断的情况超过10种的时候不要使用 switch/case。

## 四十、在判断数值范围时使用 switch/case

在下面的这种情况，使用 switch/case 判断数值范围的时候是合理的：

```js
function getCategory(age) {
    var category = "";
    switch (true) {
        case isNaN(age):
            category = "not an age";
            break;
        case (age >= 50):
            category = "Old";
            break;
        case (age <= 20):
            category = "Baby";
            break;
        default:
            category = "Young";
            break;
    };
    return category;
}
getCategory(5);  // will return "Baby"
```

【译者注：一般对于数值范围的判断，用 if/else 会比较合适。 switch/case 更适合对确定数值的判断】

## 四十一、为创建的对象指定prototype对象

写一个函数来创建一个以指定参数作为prototype的对象是有可能：

```js
function clone(object) {
    function OneShotConstructor(){};
    OneShotConstructor.prototype= object;
    return new OneShotConstructor();
}
clone(Array).prototype ;  // []
```

## 四十二、一个HTML转义函数

```js
function escapeHTML(text) {
    var replacements= {"<": "<", ">": ">","&": "&", "\"": """};
    return text.replace(/[<>&"]/g, function(character) {
        return replacements[character];
    });
}
```

## 四十三、避免在循环内部使用 try-catch-finally

在运行时，每次当 catch 从句被执行的时候，被捕获的异常对象会赋值给一个变量，而在 try-catch-finally 结构中，每次都会新建这个变量。

避免这样的写法：

```js
var object = ['foo', 'bar'], i;
for (i = 0, len = object.length; i <len; i++) {
    try {
        // do something that throws an exception
    }
    catch (e) {
        // handle exception
    }
}
```

而使用：

```js
var object = ['foo', 'bar'], i;
try {
    for (i = 0, len = object.length; i <len; i++) {
        // do something that throws an exception
    }
}
catch (e) {
    // handle exception
}
```

## 四十四、为 XMLHttpRequests 设置超时。

在一个XHR请求占用很长时间后（比如由于网络问题），你可能需要中止这次请求，那么你可以对XHR调用配套使用 setTimeout()。

```js
var xhr = new XMLHttpRequest ();
xhr.onreadystatechange = function () {
    if (this.readyState == 4) {
        clearTimeout(timeout);
        // do something with response data
    }
}
var timeout = setTimeout( function () {
    xhr.abort(); // call error callback
}, 60*1000 /* timeout after a minute */ );
xhr.open('GET', url, true);  

xhr.send();
```

此外，一般你应该完全避免同步的Ajax请求。

## 四十五、处理WebSocket超时

通常，在一个WebSocket连接创建之后，如果你没有活动的话，服务器会在30秒之后断开（time out）你的连接。防火墙也会在一段时间不活动之后断开连接。

为了防止超时的问题，你可能需要间歇性地向服务器端发送空消息。要这样做的话，你可以在你的代码里添加下面的两个函数：一个用来保持连接，另一个用来取消连接的保持。通过这个技巧，你可以控制超时的问题。

使用一个 timerID：

```js
var timerID = 0;
function keepAlive() {
    var timeout = 15000;
    if (webSocket.readyState == webSocket.OPEN) {
        webSocket.send('');
    }
    timerId = setTimeout(keepAlive, timeout);
}
function cancelKeepAlive() {
    if (timerId) {
        cancelTimeout(timerId);
    }
}
```

keepAlive()方法应该被添加在webSOcket连接的 onOpen() 方法的最后，而 cancelKeepAlive() 添加在 onClose() 方法的最后。

## 四十六、牢记，原始运算符始终比函数调用要高效。使用VanillaJS。

举例来说，不使用：

```js
var min = Math.min(a,b);
A.push(v);
```

而用：

```js
var min = a < b ? a : b;
A[A.length] = v;
```

## 四十七、从整数中，随机选取一个数值

有如下公式，非常有用，可以让我们随机显示某些名人名言或者新闻事件！

```js
值=Math.floor(Math.random()*可能值的总数+第一个可能的值)
```

例如：要想选择一个介于2到10之间的值，我们可以这么写

```js
var num=Math.floor(Math.random()*9+2)
```

请记住上面公式！~

## 四十八、时间格式化之后，前面个位数少零处理

处理起来有很多方法，但是如下方法比较简单，也有效一些，记录一下！

```js
function paddingLeftZero(str){
    return ("00"+str).substr(str.length);
}
```