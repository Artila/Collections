## JavaScript双等号引起的类型转换（js隐性类型转换）

## 引子

if语句应该是程序员用的比较多的语句，很多时候都要进行if判断，if语句一般用双等号来判断前后两个元素是否是一致的，假如是一致，那么返回是true，然后执行下面的语句，否则，执行别的语句。

本问所说的隐性类型的转换，说的是==引起的转换。举个简单的例子，双等号不是全等号，全等号是“===”三个等号，语句"1"==1，那么一般情况下是前面的字符串”1“转换为数字1，然后进行比较。通过这个例子应该了解了什么是隐性类型的转换了吧！

## 隐性类型转换步骤

一、首先看双等号前后有没有NaN，如果存在NaN，一律返回false。

二、再看双等号前后有没有布尔，有布尔就将布尔转换为数字。（false是0，true是1）

三、接着看双等号前后有没有字符串, 有三种情况：

> 1、对方是对象，对象使用toString()或者valueOf()进行转换；
>
> 2、对方是字符串，字符串转数字；（前面已经举例）
>
> 3、对方是数字，直接比较；
>
> 4、其他返回false

四、如果是数字，对方是对象，对象取valueOf()或者toString()进行比较, 其他一律返回false

五、null, undefined 不会进行类型转换, 但它们俩相等

上面的转换顺序一定要牢记，面试的时候，经常会出现类型的问题。

## .toString()方法和.valueOf()方法数值转换

通常情况下我们认为，将一个对象转换为字符串要调用toString()方法，转换为数字要调用valueOf()方法，但是真正应用的时候并没有这么简单，看如下代码实例:

```javascript
var obj = {
 webName: "haorooms前端博客",
 url:"www.haorooms.com"
}
console.log(obj.toString()); // [object Object]
```

同理，我们再看valueOf()方法：

```javascript
var arr = [1, 2, 3];
console.log(arr.valueOf()); // [1, 2, 3]
```

从上面的代码可以看出，valueOf()方法并没有将对象转换为能够反映此对象的一个数字。相反，我们用toString()

```javascript
var arr = [1, 2, 3];
console.log(arr.toString()); // 1,2,3
```

**注：很多朋友认为，转换为字符串首先要调用toString()方法， 其实这是错误的认识，我们应该这么理解，调用toString()方法可以转换为字符串，但不一定转换字符串就是首先调用toString()方法。**

我们看下下面代码：

```javascript
var arr = {};
arr.valueOf = function () { return 1; }
arr.toString = function () { return 2; }
console.log(arr == 1); // true

var arr = {};
arr.valueOf = function () { return []; }
arr.toString = function () { return 1; }
console.log(arr == 1); // true
```

上面代码我们可以看出，转换首先调用的是valueOf()，假如valueOf()不是数值，那就会调用toString进行转换！

```javascript
var arr = {};
arr.valueOf = function () { return "1"; }
arr.toString = function () { return "2"; }
console.log(arr == "1"); // true
```

假如"1"是字符串，那么它首先调用的还是valueOf()。

```javascript
var arr = [2];
console.log(arr + "1"); // 21
```

上面的例子，调用的是toString();因为arr.toString()之后是2。

转换过程是这样的，首先arr会首先调用valueOf()方法，但是数字的此方法是简单继承而来，并没有重写（当然这个重写不是我们实现），返回值是数组对象本身，并不是一个值类型，所以就转而调用toString()方法，于是就实现了转换为字符串的目的。

## 小结

**大多数对象隐式转换为值类型都是首先尝试调用valueOf()方法。但是Date对象是个例外**，此对象的valueOf()和toString()方法都经过精心重写，**默认是调用toString()方法**，比如使用+运算符，如果在其他算数运算环境中，则会转而调用valueOf()方法。

```js
var date = new Date();
console.log(date + "1"); // Sun Apr 17 2014 17:54:48 GMT+0800 (CST)1
console.log(date + 1);   // Sun Apr 17 2014 17:54:48 GMT+0800 (CST)1
console.log(date - 1);   // 1460886888556
console.log(date * 1);   // 1460886888557
```

## 举例巩固提高

下面我们一起来做做下面的题目吧！

```js
var a;
console.dir(0 == false); // true
console.dir(1 == true);  // true

console.dir(2 == {valueOf: function(){return 2}}); // true
console.dir(2 == {toString: function(){return 2}}); // true

console.dir(a == NaN);   // false
console.dir(NaN == NaN); // false

console.dir(8 == undefined); // false
console.dir(1 == undefined); // false
console.dir(0 == undefined); // false

console.dir(undefined == null); // true

console.dir(null == 1);  // false
console.dir(null == 0);  // false

console.dir({ toString:function(){ return 1 } , valueOf:function(){ return [] }} == 1);//true

console.dir(1 == "1");  // true
console.dir(1 === "1"); // false
```

做完上面的题目，不知道你对js隐性类型转换步骤了解了不？