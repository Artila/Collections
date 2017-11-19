## jquery属性的相关js实现方法

## 元素操作

### Add Class

```javascript
//JQUERY
$(el).addClass(className);

//js
//谷歌浏览器，火狐浏览器，IE8+
if (el.classList)
  el.classList.add(className);
else
  el.className += ' ' + className;
//谷歌浏览器，火狐浏览器，IE10+
el.classList.add(className);
```

### After

```javascript
//JQUERY
$(el).after(htmlString);

//js 谷歌浏览器，火狐浏览器，IE8+
el.insertAdjacentHTML('afterend', htmlString);
```

### Append

```javascript
//JQUERY
$(parent).append(el);

//js谷歌浏览器，火狐浏览器，IE8+
parent.appendChild(el);
```

### Before

```
//JQUERY
$(el).before(htmlString);

//js谷歌浏览器，火狐浏览器，IE8+
el.insertAdjacentHTML('beforebegin', htmlString);
```

### Children

```javascript
//JQUERY
$(el).children();

//js
//谷歌浏览器，火狐浏览器，IE8+
var children = [];
for (var i = el.children.length; i--;) {
  // Skip comment nodes on IE8
  if (el.children[i].nodeType != 8)
    children.unshift(el.children[i]);
}
//谷歌浏览器，火狐浏览器，IE9+
el.children
```

### Clone

```javascript
//JQUERY
$(el).clone();

//谷歌浏览器，火狐浏览器，IE8+
el.cloneNode(true);
```

### Contains

```javascript
//JQUERY
$.contains(el, child);

//谷歌浏览器，火狐浏览器，IE8+
el !== child && el.contains(child);
```

### Contains Selector

```javascript
//JQUERY
$(el).find(selector).length;

//谷歌浏览器，火狐浏览器，IE8+
el.querySelector(selector) !== null
```

### Each

```javascript
//JQUERY
$(selector).each(function(i, el){

});

//js谷歌浏览器，火狐浏览器，IE8+
function forEachElement(selector, fn) {
  var elements = document.querySelectorAll(selector);
  for (var i = 0; i < elements.length; i++)
    fn(elements[i], i);
}

forEachElement(selector, function(el, i){

});
//js谷歌浏览器，火狐浏览器，IE9+
var elements = document.querySelectorAll(selector);
Array.prototype.forEach.call(elements, function(el, i){

});
```

### Empty

```javascript
    //JQUERY
    $(el).empty();

    //js谷歌浏览器，火狐浏览器，IE8+
    while(el.firstChild)
      el.removeChild(el.firstChild);
   //js谷歌浏览器，火狐浏览器，IE9+
    el.innerHTML = '';
```

### 过滤filter

```javascript
//JQUERY
$(selector).filter(filterFn);

//谷歌浏览器，火狐浏览器，IE8+
function filter(selector, filterFn) {
  var elements = document.querySelectorAll(selector);
  var out = [];
  for (var i = elements.length; i--;) {
    if (filterFn(elements[i]))
      out.unshift(elements[i]);
  }
  return out;
}

filter(selector, filterFn);
//谷歌浏览器，火狐浏览器，IE9+
Array.prototype.filter.call(document.querySelectorAll(selector), filterFn);
```

### 查找子元素

```javascript
//JQUERY
$(el).find(selector);

//谷歌浏览器，火狐浏览器，IE8+
el.querySelectorAll(selector);
```

### 查找、选择器

```javascript
//JQUERY
$('.my #awesome selector');

//谷歌浏览器，火狐浏览器，IE8+
document.querySelectorAll('.my #awesome selector');
```

### 获取属性值attr

```javascript
    //JQUERY
    $(el).attr('tabindex');

   //谷歌浏览器，火狐浏览器，IE8+
    el.getAttribute('tabindex');
```

### 获取Html内容

```javascript
//JQUERY
$(el).html();

//js
el.innerHTML
```

### 获取CSS样式

```javascript
//JQUERY
$(el).css(ruleName);

//谷歌浏览器，火狐浏览器，IE9+
getComputedStyle(el)[ruleName];
```

### 获取文本内容

```javascript
//JQUERY
$(el).text();

//谷歌浏览器，火狐浏览器，IE8+
el.textContent || el.innerText
//谷歌浏览器，火狐浏览器，IE9+
el.textContent
```

### Has Class

```javascript
//JQUERY
$(el).hasClass(className);

//谷歌浏览器，火狐浏览器，IE8+
if (el.classList)
  el.classList.contains(className);
else
  new RegExp('(^| )' + className + '( |$)', 'gi').test(el.className);
//谷歌浏览器，火狐浏览器，IE10+
el.classList.contains(className);
```

### 元素比较

```javascript
JQUERY
$(el).is($(otherEl));

//js
el === otherEl
```

### 比较类名

```javascript
//JQUERY
$(el).is('.my-class');

//谷歌浏览器，火狐浏览器，IE8+
var matches = function(el, selector) {
  var _matches = (el.matches || el.matchesSelector || el.msMatchesSelector || el.mozMatchesSelector || el.webkitMatchesSelector || el.oMatchesSelector);

  if (_matches) {
    return _matches.call(el, selector);
  } else {
    var nodes = el.parentNode.querySelectorAll(selector);
    for (var i = nodes.length; i--;) {
      if (nodes[i] === el)
        return true;
    }
    return false;
  }
};

matches(el, '.my-class');
//谷歌浏览器，火狐浏览器，IE9+
var matches = function(el, selector) {
  return (el.matches || el.matchesSelector || el.msMatchesSelector || el.mozMatchesSelector || el.webkitMatchesSelector || el.oMatchesSelector).call(el, selector);
};

matches(el, '.my-class');
```

### Next

```javascript
//JQUERY
$(el).next();

//谷歌浏览器，火狐浏览器，IE8+
// nextSibling can include text nodes
function nextElementSibling(el) {
  do { el = el.nextSibling; } while ( el && el.nodeType !== 1 );
  return el;
}

el.nextElementSibling || nextElementSibling(el);
//谷歌浏览器，火狐浏览器，IE9+
el.nextElementSibling
```

### Offset

```javascript
//JQUERY
$(el).offset();
//js谷歌浏览器，火狐浏览器，IE8+
var rect = el.getBoundingClientRect()

{
  top: rect.top + document.body.scrollTop,
  left: rect.left + document.body.scrollLeft
}
```

### Outer Width

```javascript
//JQUERY
$(el).outerWidth();
//js
el.offsetWidth
```

### Parent

```javascript
//JQUERY
$(el).parent();
//js
el.parentNode
```

### Position

```javascript
//JQUERY
$(el).position();
//js
{left: el.offsetLeft, top: el.offsetTop}
```

### Prev

```javascript
//JQUERY
$(el).prev();
//谷歌浏览器，火狐浏览器，IE8+
// prevSibling can include text nodes
function previousElementSibling(el) {
  do { el = el.previousSibling; } while ( el && el.nodeType !== 1 );
  return el;
}

el.previousElementSibling || previousElementSibling(el);
//谷歌浏览器，火狐浏览器，IE9+
el.previousElementSibling
```

### Remove

```javascript
//JQUERY
$(el).remove();
//js谷歌浏览器，火狐浏览器，IE8+
el.parentNode.removeChild(el);
```

### Remove Class

```javascript
//JQUERY
$(el).removeClass(className);
//js谷歌浏览器，火狐浏览器，IE8+
if (el.classList)
  el.classList.remove(className);
else
  el.className = el.className.replace(new RegExp('(^|\\b)' + className.split(' ').join('|') + '(\\b|$)', 'gi'), ' ');

//谷歌浏览器，火狐浏览器，IE10+
el.classList.remove(className);
```

### Replace From Html

```javascript
//JQUERY
$(el).replaceWith(string);
//谷歌浏览器，火狐浏览器，IE8+
el.outerHTML = string;
```

### Set Attributes

```javascript
//JQUERY
$(el).attr('tabindex', 3);
//谷歌浏览器，火狐浏览器，IE8+
el.setAttribute('tabindex', 3);
```

### Set Html

```javascript
//JQUERY
$(el).html(string);
//谷歌浏览器，火狐浏览器，IE8+
el.innerHTML = string;
```

### Set Style

```javascript
//JQUERY
$(el).css('border-width', '20px');
//谷歌浏览器，火狐浏览器，IE8+
// Use a class if possible
el.style.borderWidth = '20px';
```

### Set Text

```javascript
//JQUERY
$(el).text(string);
//谷歌浏览器，火狐浏览器，IE8+
if (el.textContent !== undefined)
  el.textContent = string;
else
  el.innerText = string;
//谷歌浏览器，火狐浏览器，IE9+
el.textContent = string;
```

### Siblings

```javascript
//JQUERY
$(el).siblings();
//谷歌浏览器，火狐浏览器，IE8+
var siblings = Array.prototype.slice.call(el.parentNode.children);

for (var i = siblings.length; i--;) {
  if (siblings[i] === el) {
    siblings.splice(i, 1);
    break;
  }
}
//谷歌浏览器，火狐浏览器，IE9+
Array.prototype.filter.call(el.parentNode.children, function(child){
  return child !== el;
});
```

### Toggle Class

```javascript
//JQUERY
$(el).toggleClass(className);
//谷歌浏览器，火狐浏览器，IE8+
if (el.classList) {
  el.classList.toggle(className);
} else {
    var classes = el.className.split(' ');
    var existingIndex = -1;
    for (var i = classes.length; i--;) {
      if (classes[i] === className)
        existingIndex = i;
    }

    if (existingIndex >= 0)
      classes.splice(existingIndex, 1);
    else
      classes.push(className);

  el.className = classes.join(' ');
}
//谷歌浏览器，火狐浏览器，IE9+
if (el.classList) {
  el.classList.toggle(className);
} else {
  var classes = el.className.split(' ');
  var existingIndex = classes.indexOf(className);

  if (existingIndex >= 0)
    classes.splice(existingIndex, 1);
  else
    classes.push(className);

  el.className = classes.join(' ');
}
//谷歌浏览器，火狐浏览器，IE10+
el.classList.toggle(className);
```

## 事件

### Off

```javascript
//JQUERY
$(el).off(eventName, eventHandler);

//谷歌浏览器，火狐浏览器，IE8+
function removeEventListener(el, eventName, handler) {
  if (el.removeEventListener)
    el.removeEventListener(eventName, handler);
  else
    el.detachEvent('on' + eventName, handler);
}
removeEventListener(el, eventName, handler);

//谷歌浏览器，火狐浏览器，IE9+
el.removeEventListener(eventName, eventHandler);
```

### On

```javascript
//JQUERY
$(el).on(eventName, eventHandler);

//谷歌浏览器，火狐浏览器，IE8+
function addEventListener(el, eventName, handler) {
  if (el.addEventListener) {
    el.addEventListener(eventName, handler);
  } else {
    el.attachEvent('on' + eventName, function(){
      handler.call(el);
    });
  }
}

addEventListener(el, eventName, handler);

谷歌浏览器，火狐浏览器，IE9+
el.addEventListener(eventName, eventHandler);
```

### Ready

```javascript
//JQUERY
$(document).ready(function(){

});

//谷歌浏览器，火狐浏览器，IE8+

function ready(fn) {
  if (document.readyState != 'loading'){
    fn();
  } else if (document.addEventListener) {
    document.addEventListener('DOMContentLoaded', fn);
  } else {
    document.attachEvent('onreadystatechange', function() {
      if (document.readyState != 'loading')
        fn();
    });
  }
}

//谷歌浏览器，火狐浏览器，IE9+

function ready(fn) {
  if (document.readyState != 'loading'){
    fn();
  } else {
    document.addEventListener('DOMContentLoaded', fn);
  }
```

### 指定事件触发

```javascript
//JQUERY
$(el).trigger('my-event', {some: 'data'});


//js谷歌浏览器，火狐浏览器，IE9+
if (window.CustomEvent) {
  var event = new CustomEvent('my-event', {detail: {some: 'data'}});
} else {
  var event = document.createEvent('CustomEvent');
  event.initCustomEvent('my-event', true, true, {some: 'data'});
}

el.dispatchEvent(event);
```

### Trigger Native

```javascript
//JQUERY
$(el).trigger('change');

//谷歌浏览器，火狐浏览器，IE8+
if (document.createEvent) {
  var event = document.createEvent('HTMLEvents');
  event.initEvent('change', true, false);
  el.dispatchEvent(event);
} else {
  el.fireEvent('onchange');
}
//谷歌浏览器，火狐浏览器，IE9+
// For a full list of event types: https://developer.mozilla.org/en-US/docs/Web/API/document.createEvent
var event = document.createEvent('HTMLEvents');
event.initEvent('change', true, false);
el.dispatchEvent(event);
```

## 技巧

### Array Each

```javascript
//JQUERY
$.each(array, function(i, item){

});

谷歌浏览器，火狐浏览器，IE8+
function forEach(array, fn) {
  for (i = 0; i < array.length; i++)
    fn(array[i], i);
}

forEach(array, function(item, i){

});

//谷歌浏览器，火狐浏览器，IE9+
array.forEach(function(item, i){

});
```

### 深度扩展

```javascript
//JQUERY
$.extend(true, {}, objA, objB);
//谷歌浏览器，火狐浏览器，IE8+
var deepExtend = function(out) {
  out = out || {};

  for (var i = 1; i < arguments.length; i++) {
    var obj = arguments[i];

    if (!obj)
      continue;

    for (var key in obj) {
      if (obj.hasOwnProperty(key)) {
        if (typeof obj[key] === 'object')
          deepExtend(out[key], obj[key]);
        else
          out[key] = obj[key];
      }
    }
  }

  return out;
};

deepExtend({}, objA, objB);
```

### proxy

```javascript
//JQUERY
$.proxy(fn, context);
//谷歌浏览器，火狐浏览器，IE8+
fn.apply(context, arguments);
//谷歌浏览器，火狐浏览器，IE9+
fn.bind(context);
```

### bind

```javascript
//jQuery
$.extend({}, objA, objB);
//谷歌浏览器，火狐浏览器，IE8+
var extend = function(out) {
  out = out || {};

  for (var i = 1; i < arguments.length; i++) {
    if (!arguments[i])
      continue;

    for (var key in arguments[i]) {
      if (arguments[i].hasOwnProperty(key))
        out[key] = arguments[i][key];
    }
  }

  return out;
};

extend({}, objA, objB);
```

### Index Of

```javascript
//JQUERY
$.inArray(item, array);
//谷歌浏览器，火狐浏览器，IE8+
function indexOf(array, item) {
  for (var i = 0; i < array.length; i++) {
    if (array[i] === item)
      return i;
  }
  return -1;
}

indexOf(array, item);
谷歌浏览器，火狐浏览器，IE9+
array.indexOf(item);
```

### Is Array

```javascript
//JQUERY
$.isArray(arr);

//谷歌浏览器，火狐浏览器，IE8+
isArray = Array.isArray || function(arr) {
  return Object.prototype.toString.call(arr) == '[object Array]';
}

isArray(arr);
//谷歌浏览器，火狐浏览器，IE9+
Array.isArray(arr);
```

### Map

```javascript
//JQUERY
$.map(array, function(value, index){

});

//js谷歌浏览器，火狐浏览器，IE8+
function map(arr, fn) {
  var results = [];
  for (var i = 0; i < arr.length; i++)
    results.push(fn(arr[i], i));
  return results;
}

map(array, function(value, index){

});
//谷歌浏览器，火狐浏览器，IE9+
array.map(function(value, index){

});
```

### Now

```javascript
//JQUERY
$.now();

//谷歌浏览器，火狐浏览器，IE8+
new Date().getTime();
//谷歌浏览器，火狐浏览器，IE9+
Date.now();
```

### Parse Html

```javascript
//JQUERY
$.parseHTML(htmlString);

谷歌浏览器，火狐浏览器，IE8+
var parseHTML = function(str) {
  var el = document.createElement('div');
  el.innerHTML = str;
  return el.children;
};

parseHTML(htmlString);
谷歌浏览器，火狐浏览器，IE9+
var parseHTML = function(str) {
  var tmp = document.implementation.createHTMLDocument();
  tmp.body.innerHTML = str;
  return tmp.body.children;
};

parseHTML(htmlString);
```

### 解析 Json

```javascript
//JQUERY
$.parseJSON(string);
//谷歌浏览器，火狐浏览器，IE8+
JSON.parse(string);
```

### Trim

```javascript
//JQUERY
$.trim(string);
//谷歌浏览器，火狐浏览器，IE8+
string.replace(/^\s+|\s+$/g, '');
//谷歌浏览器，火狐浏览器，IE9+
string.trim();
```

### Type

```javascript
//JQUERY
$.type(obj);

谷歌浏览器，火狐浏览器，IE8+
Object.prototype.toString.call(obj)
                .replace(/^\[object (.+)\]$/, "$1")
                .toLowerCase();
```

## ajax

新AJAX方法fetch()

**基本Fetch用法**

让我们先用一个例子来比较一下使用 XMLHttpRequest 和使用 fetch 之间的不同。我们要请求一个URL，获取JSON格式的返回结果。

原来的XMLHttpRequest

一个 XMLHttpRequest 请求需要两个监听器来捕捉 success 和 error 两种情形，而且需要调用 open() 和 send() 方法。

```javascript
function reqListener() {  
  var data = JSON.parse(this.responseText);  
  console.log(data);  
}

function reqError(err) {  
  console.log('Fetch Error :-S', err);  
}

var oReq = new XMLHttpRequest();  
oReq.onload = reqListener;  
oReq.onerror = reqError;  
oReq.open('get', './api/some.json', true);  
oReq.send();
```

**Fetch方法：**

我们的 fetch 请求的代码基本上是这样的：

```javascript
fetch('./api/some.json')  
  .then(  
    function(response) {  
      if (response.status !== 200) {  
        console.log('Looks like there was a problem. Status Code: ' +  
          response.status);  
        return;  
      }

      // Examine the text in the response  
      response.json().then(function(data) {  
        console.log(data);  
      });  
    }  
  )  
  .catch(function(err) {  
    console.log('Fetch Error :-S', err);  
  });
```

**用fetch执行表单数据提交**

在WEB应用中，提交表单是非常常见的操作，用fetch来提交表单数据也是非常简洁。

fetch里提供了 method 和 body 参数选项。

```javascript
fetch(url, {  
    method: 'post',  
    headers: {  
      "Content-type": "application/x-www-form-urlencoded; charset=UTF-8"  
    },  
    body: 'foo=bar&lorem=ipsum'  
  })
  .then(json)  
  .then(function (data) {  
    console.log('Request succeeded with JSON response', data);  
  })  
  .catch(function (error) {  
    console.log('Request failed', error);  
  });
```

在Fetch请求里发送用户身份凭证信息

如果你想在fetch请求里附带cookies之类的凭证信息，可以将 credentials 参数设置成 “include” 值。

```javascript
fetch(url, {  
  credentials: 'include'  
})
```

## JSON

```javascript
//JQUERY
$.getJSON('/my/url', function(data) {

});

//谷歌浏览器，火狐浏览器，IE8+
var request = new XMLHttpRequest();
request.open('GET', '/my/url', true);

request.onreadystatechange = function() {
  if (this.readyState === 4) {
    if (this.status >= 200 && this.status < 400) {
      // Success!
      var data = JSON.parse(this.responseText);
    } else {
      // Error :(
    }
  }
};

request.send();
request = null;

//谷歌浏览器，火狐浏览器，IE9+
var request = new XMLHttpRequest();
request.open('GET', '/my/url', true);

request.onload = function() {
  if (request.status >= 200 && request.status < 400) {
    // Success!
    var data = JSON.parse(request.responseText);
  } else {
    // We reached our target server, but it returned an error

  }
};

request.onerror = function() {
  // There was a connection error of some sort
};

request.send();

//谷歌浏览器，火狐浏览器，IE10+
var request = new XMLHttpRequest();
request.open('GET', '/my/url', true);

request.onload = function() {
  if (this.status >= 200 && this.status < 400) {
    // Success!
    var data = JSON.parse(this.response);
  } else {
    // We reached our target server, but it returned an error

  }
};

request.onerror = function() {
  // There was a connection error of some sort
};

request.send();
```

## Post

```javascript
//JQUERY
$.ajax({
  type: 'POST',
  url: '/my/url',
  data: data
});

//谷歌浏览器，火狐浏览器，IE8+
var request = new XMLHttpRequest();
request.open('POST', '/my/url', true);
request.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded; charset=UTF-8');
request.send(data);
```

### Request

```javascript
//JQUERY
$.ajax({
  type: 'GET',
  url: '/my/url',
  success: function(resp) {

  },
  error: function() {

  }
});

//谷歌浏览器，火狐浏览器，IE8+
var request = new XMLHttpRequest();
request.open('GET', '/my/url', true);

request.onreadystatechange = function() {
  if (this.readyState === 4) {
    if (this.status >= 200 && this.status < 400) {
      // Success!
      var resp = this.responseText;
    } else {
      // Error :(
    }
  }
};

request.send();
request = null;

//谷歌浏览器，火狐浏览器，IE9+
var request = new XMLHttpRequest();
request.open('GET', '/my/url', true);

request.onload = function() {
  if (request.status >= 200 && request.status < 400) {
    // Success!
    var resp = request.responseText;
  } else {
    // We reached our target server, but it returned an error

  }
};

request.onerror = function() {
  // There was a connection error of some sort
};

request.send();

//谷歌浏览器，火狐浏览器，IE10+
var request = new XMLHttpRequest();
request.open('GET', '/my/url', true);

request.onload = function() {
  if (this.status >= 200 && this.status < 400) {
    // Success!
    var resp = this.response;
  } else {
    // We reached our target server, but it returned an error

  }
};

request.onerror = function() {
  // There was a connection error of some sort
};

request.send();
```

## 特效

### 淡入淡出

```javascript
//JQUERY
$(el).fadeIn();

//谷歌浏览器，火狐浏览器，IE8+
function fadeIn(el) {
  var opacity = 0;

  el.style.opacity = 0;
  el.style.filter = '';

  var last = +new Date();
  var tick = function() {
    opacity += (new Date() - last) / 400;
    el.style.opacity = opacity;
    el.style.filter = 'alpha(opacity=' + (100 * opacity)|0 + ')';

    last = +new Date();

    if (opacity < 1) {
      (window.requestAnimationFrame && requestAnimationFrame(tick)) || setTimeout(tick, 16);
    }
  };

  tick();
}

fadeIn(el);

//谷歌浏览器，火狐浏览器，IE9+
function fadeIn(el) {
  el.style.opacity = 0;

  var last = +new Date();
  var tick = function() {
    el.style.opacity = +el.style.opacity + (new Date() - last) / 400;
    last = +new Date();

    if (+el.style.opacity < 1) {
      (window.requestAnimationFrame && requestAnimationFrame(tick)) || setTimeout(tick, 16)
    }
  };

  tick();
}

fadeIn(el);

//谷歌浏览器，火狐浏览器，IE10+
el.classList.add('show');
el.classList.remove('hide');
.show {
  transition: opacity 400ms;
}
.hide {
  opacity: 0;
}
```

### Hide

```javascript
//JQUERY
$(el).hide();

//谷歌浏览器，火狐浏览器，IE8+
el.style.display = 'none';
```

### Show

```javascript
//JQUERY
$(el).show();
//谷歌浏览器，火狐浏览器，IE8+
el.style.display = '';
```