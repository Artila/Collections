## toFixed() 和 toPrecision()

#### Number.prototype.toFixed()

`toFixed()` 方法使用定点表示法来格式化一个数。

**语法**

```
numObj.toFixed(digits)
```

**参数**

- digits

  小数点后数字的个数；介于 0 到 20 （包括）之间，实现环境可能支持更大范围。如果忽略该参数，则默认为 0。

**返回值**

所给数值的定点数表示法的字符串形式。

**抛出异常**

- `RangeError`

  如果 *digits* 参数太小或太大。0 到 20（包括）之间的值不会引起 `RangeError`。实现环境（implementations）也可以支持更大或更小的值。


- `TypeError`

  如果该方法在一个非`Number`类型的对象上调用。

**描述**

一个数值的字符串表现形式，不使用指数记数法，而是在小数点后有 digits（注：digits具体值取决于传入参数）位数字。该数值在必要时进行四舍五入，另外在必要时会用 0 来填充小数部分，以便小数部分有指定的位数。 如果数值大于 1e+21，该方法会简单调用 `Number.prototype.toString()`并返回一个指数记数法格式的字符串。

**示例**

```js
var numObj = 12345.6789;

numObj.toFixed();         // 返回 "12346"：进行四舍五入，不包括小数部分
numObj.toFixed(1);        // 返回 "12345.7"：进行四舍五入

numObj.toFixed(6);        // 返回 "12345.678900"：用0填充

(1.23e+20).toFixed(2);    // 返回 "123000000000000000000.00"

(1.23e-10).toFixed(2);    // 返回 "0.00"

2.34.toFixed(1);          // 返回 "2.3"

-2.34.toFixed(1);         // 返回 -2.3 （由于操作符优先级，负数不会返回字符串）

(-2.34).toFixed(1);       // 返回 "-2.3" （若用括号提高优先级，则返回字符串）
```



#### Number.prototype.toPrecision()

`toPrecision()` 方法以指定的精度返回该数值对象的字符串表示。

**语法**


```
numObj.toPrecision(precision)
```


**参数**

- precision

  可选。一个用来指定有效数个数的整数。

**返回值**

以定点表示法或指数表示法表示的一个数值对象的字符串表示，四舍五入到 `precision` 参数指定的显示数字位数。查看 `Number.prototype.toFixed()` 方法关于四舍五入的讨论，同样应用于 `toPrecision` 方法。

如果忽略 `precision` 参数，则该方法表现类似于 `Number.prototype.toString()`。如果该参数是一个非整数值，将会向下舍入到最接近的整数。

**异常**

- `RangeError`

  如果 *precison* 参数不在 1 和 100 （包括）之间，将会抛出一个 `RangeError` 。执行环境也可以支持更大或更小的范围。ECMA-262 只需要最多 21 位显示数字。

**示例**

```js
var numObj = 5.123456;

numObj.toPrecision();   // 5.123456
numObj.toPrecision(1);  // 5
numObj.toPrecision(2);  // 5.1
numObj.toPrecision(5);  // 5.1235(四舍五入)

// 注意：在某些情况下会以指数表示法返回
console.log((1234.5).toPrecision(2)); // "1.2e+3"
```
