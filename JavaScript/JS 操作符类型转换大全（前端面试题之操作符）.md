## JS 操作符类型转换大全（前端面试题之操作符）

操作符运算符，在前端的面试题目中经常出现，很多朋友在对其运算的时候经常出错。说明对操作符运算还没有完全理解，我前面的一篇文章，[javascript双等号引起的类型转换](http://www.haorooms.com/post/js_yinxingleixing)，主要讲解双等号引起的类型转换。本篇文章可以说是对这篇文章的补充吧！

首先，我们先来做一些题目吧！为了统一，我不混着来写这些题目，面试题目中，经常将这些题目混起来，这样对你的迷惑度会更大，为了更方便演示，我在这里分模块写了一些题目，大家可以看下！

```javascript
 //操作符字符串的隐性转换
 //乘法
 console.dir("-------以下乘法---------");
 console.dir(5*"5");
 console.dir(5*"a");
 console.dir(5*NaN);
 console.dir(5*null);
 console.dir(5*undefined);
 console.dir(5*5);
 console.dir("-------以上乘法---------");
 //除法
 console.dir("-------以下除法---------");
 console.dir(5/"5");
 console.dir(5/"a");
 console.dir(5/NaN);
 console.dir(5/null);
 console.dir(null/5);
 console.dir(5/undefined);
 console.dir(5/5);
 console.dir(5/0);
 console.dir(0/5);
 console.dir(0/0);
 console.dir("-------以上除法---------"); 
 //取余、求模
 console.dir("-------以下取余、求模--------");
 console.dir(16%"5");
 console.dir(5%"a");
 console.dir(5%NaN);
 console.dir(5%null);
 console.dir(null%5);
 console.dir(5%undefined);
 console.dir(5%5);
 console.dir(5%0);
 console.dir(0%5);
 console.dir(0%0);
 console.dir("-------以上取余、求模---------"); 

 //加法
 console.dir("-------以下加法--------");
 console.dir(16+"5");
 console.dir(5+"a");
 console.dir(5+NaN);
 console.dir(5+null);
 console.dir(5+undefined);
 console.dir(5+5);
 console.dir("两个数的和是"+5+5);
 console.dir("两个数的和是"+(5+5));
 console.dir("-------以上加法--------"); 

 //减法
 console.dir("-------以下减法--------");
 console.dir(16-"5");
 console.dir(5-"a");
 console.dir(5-NaN);
 console.dir(5-null);
 console.dir(5-undefined);
 console.dir(5-5);
 console.dir(5-true);
 console.dir(5-"true");
 console.dir(5-"");
 console.dir("两个数的差是"+5-5);
 console.dir("两个数的差是"+(5-5));
 console.dir("-------以上减法--------"); 

 //关系操作符
 console.dir("-------以下关系操作符--------");
 console.dir(16>"5");
 console.dir("16">"5");
 console.dir(5<"a");
 console.dir(5>=NaN);
 console.dir(5<NaN);
 console.dir(NaN>=NaN);
 console.dir(5>=null);
 console.dir(5>=undefined);
 console.dir(5>=5);
 console.dir(5>=true);
 console.dir(5>="true");
 console.dir(5>="");
 console.dir("Brick">"alphabet");
 console.dir("brick">"alphabet");
 console.dir("-------以上关系操作符--------"); 
```

上面的题目你如果全部答对，<http://www.haorooms.com/post/js_yinxingleixing> 这篇文章中的题目也全部理解了，那么你对操作符类型转换基本上是理解了。假如您有错误，那么我们来详细的解释一下吧！

## 乘法

我们来看下前面的题目：

```javascript
 console.dir(5*"5"); //25
 console.dir(5*"a");//NaN
 console.dir(5*NaN);//NaN
 console.dir(5*null);0
 console.dir(5*undefined);//NaN
 console.dir(5*5);//25
```

**下面说一下乘法隐性转换原则：**

> 1、如果2个数值都是数字，那么直接进行乘法运算，（相信大家都会的，和小学数学一样，同时要注意数字的符号），如果乘积数值超过了ECMAscript的数值表示范围，则返回Infinity（正无穷）或者-Infinity（负无穷）
>
> 2、如果一个数是NaN,那么结果就是NaN
>
> 3、如果Infinity与0相乘，结果是NaN
>
> 4、假如一个操作符是数字，另外一个不是数值，那么先用Number()函数（**如果参数无法被转换为数字，则返回 NaN。**），将其进行转化，将转化出来的值与数字进行相乘。假如转换出来的结果出现NaN，那么结果就是NaN。

## 除法

我们看下上面的题目吧！

```javascript
 console.dir(5/"5");//1    将字符转化为数字进行相除
 console.dir(5/"a");//NaN   将“a”用Number()函数进行转化，出来的值是NaN，结果就是NaN
 console.dir(5/NaN);//NaN
 console.dir(5/null);//Infinity  null用Number()函数进行转化，结果是0，那么5/0是正无穷
 console.dir(null/5);//0  同上0/5是0
 console.dir(5/undefined);//NaN   undefined 用Number()进行转化，结果是NaN
 console.dir(5/5);//1
 console.dir(5/0);//Infinity
 console.dir(0/5);//0
 console.dir(0/0);//NaN //0除以0结果是NaN
```

**下面说一下除法隐性转换原则：**

> 和乘法类似，唯一多的一条就是0/0结果是NaN

## 取余、求模

求余在项目中用的最多的是求奇数偶数的时候。我们经常用一个数值与2进行求余，结果是0那么这个数是偶数，结果是1那么这个数是奇数。

看看上面的题目：

```javascript
 console.dir(16%"5"); //1  将字符串5通过Number()转化为5然后进行求余
 console.dir(5%"a");//NaN
 console.dir(5%NaN);//NaN
 console.dir(5%null);//NaN  将null 通过Number()转化，结果是0，然后计算5%0 ，结果是NaN
 console.dir(null%5);//0  同上0%5 取余，结果是0
 console.dir(5%undefined);//NaN
 console.dir(5%5);//0
 console.dir(5%0);//NaN
 console.dir(0%5);//0
 console.dir(0%0);//NaN
console.dir(Infinity%Infinity);//NaN
console.dir(5%Infinity);//5
 console.dir(Infinity%5); //NaN
```

**下面说一下取余隐性转换原则：**

和乘法一样，我说一下比较特别的地方吧！我们都知道被除数和除数的概念吧，小学的时候就学过的。

> 1、被除数是无穷大，除数是有限大的值，那么结果是NaN
>
> 2、被除数是有限大的值，除数是0，那么结果是NaN
>
> 3、Infinity%Infinity结果是NaN
>
> 4、被除数是有限大的值，除数是无穷大的值，结果是被除数。
>
> 5、被除数是0，结果是0

## 减法

看看上面的例子吧！

```javascript
 console.dir(16-"5");//11
 console.dir(5-"a");//NaN
 console.dir(5-NaN);//NaN
 console.dir(5-null);//5
 console.dir(5-undefined);//NaN
 console.dir(5-5);//0
 console.dir(5-true);//4
 console.dir(5-"true");//NaN
 console.dir(5-"");//5
 console.dir(5-Infinity);//-Infinity
 console.dir(Infinity-Infinity);//NaN
 console.dir("两个数的差是"+5-5);//NaN
 console.dir("两个数的差是"+(5-5));//两个数的差是0
```

**下面说一下减法隐性转换原则：**

和上面一样，相同的就不说了，我说一下减法特有的。

> 1、Infinity-Infinity结果是NaN
>
> 2、-Infinity-Infinity结果是-Infinity
>
> 3、一个数字减Infinity结果是-Infinity
>
> 4、Infinity-（-Infinity）结果是Infinity
>
> 5、如果操作数是对象，则调用对象valueOf方法，如果结果是NaN那么结果就是NaN。如果没有valueOf方法，那么调用toString()方法，并将得到的字符串转换为数值。

## 关系操作符

我们一起来看看上面的例子，关系运算符统一返回true或者false

```javascript
 console.dir(16>"5"); //true
 console.dir("16">"5");//false
 console.dir(5<"a");//false
 console.dir(5>=NaN);//false
 console.dir(5<NaN);//false
 console.dir(NaN>=NaN);//false
 console.dir(5>=null);//true
 console.dir(5>=undefined);//false
 console.dir(5>=5);//true
 console.dir(5>=true);//true
 console.dir(5>="true");//false
 console.dir(5>="");//true 
 console.dir("Brick">"alphabet");//false  B的字符串编码值是66 ，而a的字符串编码是97.因此false
 console.dir("brick">"alphabet");//true 小写字母b比a大，所以是true
```

**下面说一下关系运算符隐性转换原则：**

还是和上面一样，相同的就不说了。

> 如果比较的两个数都是字符串，那么会比较字符串对应的字符串编码值。

## 双等号隐性转换

双等号具体请看：<http://www.haorooms.com/post/js_yinxingleixing>

## 加法运算

加法运算隐性转换，我之所以最后说，是因为加法运算隐性转换和之前的不一样，之前的所有的运算符号，只要一个是数字，另一个也默认使用Number（）进行数字转换。加法运算不一样。加法运算只要其中一个是字符串，那么另外一个也会转换为字符串，然后进行字符串的拼接！

看看一开始的例子吧！

```javascript
 console.dir(16+"5"); //156
 console.dir(5+"a");//5a
 console.dir(5+NaN);//NaN
 console.dir(5+null);//5
  console.dir('5'+null);//5null
 console.dir(5+undefined);//NaN
 console.dir(null+undefined);//NaN
 console.dir(5+5);//10
 console.dir("两个数的和是"+5+5);//两个数的和是55
 console.dir("两个数的和是"+(5+5));//两个数的和是10
```

**下面说一下加法运算符隐性转换原则：**

> 1、有一个是字符串，那么另外一个也会转换为字符串进行拼接。假如一个是字符串，另外一个是null或者undefined，那么相加，null或者undefined就会调用String()方法，获得字符串“null”或者“undefined”，然后进行拼接。
>
> 2、假如一个数字加null或者undefined，那么还是把null或者undefined进行Number()转换之后再相加。
>
> 3、剩下的原则和其他的差不多，就不多说了。