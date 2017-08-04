# Vue.js 2.0 介绍

> 以下信息主要来自 [Vue.js官网](https://cn.vuejs.org/)。

- [Vue.js是什么](#Vue.js是什么)
- [起步](#起步)
- [声明式渲染](#声明式渲染)
    - el
    - v-bind
- [条件与循环](#条件与循环)
    - v-if
    - v-for
- [处理用户输入](#处理用户输入)
    - v-on
    - v-model
- [组件化应用构建](#组件化应用构建)
    - Vue.component
- [与自定义元素的关系](#与自定义元素的关系)

## Vue.js是什么

Vue.js（读音 /vjuː/，类似于 view） 是一套构建用户界面的渐进式框架。

Vue 的核心库只关注视图层。

它不仅易于上手，还便于与第三方库或既有项目整合。另一方面，当与单文件组件和 Vue 生态系统支持的库结合使用时，Vue 也完全能够为复杂的单页应用程序提供驱动。
    
## 起步

你可以创建一个 `.html` 文件，然后通过如下方式引入 Vue：

```<script src="https://unpkg.com/vue"></script>```

当然还有其他的安装方式，这只是最简单的一种。

## 声明式渲染

Vue.js 的核心是一个允许采用简洁的模板语法来声明式的将数据渲染进 DOM：

```
<div id="app">
  {{ message }}
</div>

var app = new Vue({
  el: '#app',
  data: {
    message: 'Hello Vue!'
  }
})
```
现在数据和 DOM 已经被绑定在一起，所有的元素都是响应式的。我们如何知道？打开你的浏览器的控制台（就在这个页面打开），并修改 app.message，你将看到上例相应地更新。

除了文本插值，我们还可以采用这样的方式绑定 DOM 元素属性：
```
<div id="app-2">
  <span v-bind:title="message">
    鼠标悬停几秒钟查看此处动态绑定的提示信息！
  </span>
</div>

var app2 = new Vue({
  el: '#app-2',
  data: {
    message: '页面加载于 ' + new Date()
  }
})
```
`v-bind` 属性被称为指令。指令带有前缀 `v-`，以表示它们是 Vue 提供的特殊属性。

它们会在渲染的 DOM 上应用特殊的响应式行为。

简言之，这里该指令的作用是：“将这个元素节点的 `title` 属性和 Vue 实例的 `message` 属性保持一致”。

再次打开浏览器的 JavaScript 控制台输入 `app2.message = '新消息'`，就会再一次看到这个绑定了 `title` 属性的 HTML 已经进行了更新。

## 条件与循环

控制切换一个元素的显示也相当简单：
```
<div id="app-3">
  <p v-if="seen">现在你看到我了</p>
</div>

var app3 = new Vue({
  el: '#app-3',
  data: {
    seen: true
  }
})
```
继续在控制台设置 `app3.seen = false`，你会发现 “现在你看到我了” 消失了。

这个例子演示了我们不仅可以绑定 DOM 文本到数据，也可以绑定 DOM 结构到数据。

而且，Vue 也提供一个强大的过渡效果系统，可以在 Vue 插入/更新/删除元素时自动应用过渡效果。

还有其它很多指令，每个都有特殊的功能。例如，`v-for` 指令可以绑定数组的数据来渲染一个项目列表：
```
<div id="app-4">
  <ol>
    <li v-for="todo in todos">
      {{ todo.text }}
    </li>
  </ol>
</div>

var app4 = new Vue({
  el: '#app-4',
  data: {
    todos: [
      { text: '学习 JavaScript' },
      { text: '学习 Vue' },
      { text: '整个牛项目' }
    ]
  }
})
```
在控制台里，输入 `app4.todos.push({ text: '新项目' })`，你会发现列表中添加了一个新项。

## 处理用户输入

为了让用户和你的应用进行互动，我们可以用 `v-on` 指令绑定一个事件监听器，通过它调用我们 Vue 实例中定义的方法：
```
<div id="app-5">
  <p>{{ message }}</p>
  <button v-on:click="reverseMessage">逆转消息</button>
</div>

var app5 = new Vue({
  el: '#app-5',
  data: {
    message: 'Hello Vue.js!'
  },
  methods: {
    reverseMessage: function () {
      this.message = this.message.split('').reverse().join('')
    }
  }
})
```
注意在 `reverseMessage` 方法中，我们更新了应用的状态，但没有触碰 DOM——所有的 DOM 操作都由 Vue 来处理，你编写的代码不需要关注底层逻辑。

Vue 还提供了 `v-model` 指令，它能轻松实现表单输入和应用状态之间的双向绑定。
```
<div id="app-6">
  <p>{{ message }}</p>
  <input v-model="message">
</div>

var app6 = new Vue({
  el: '#app-6',
  data: {
    message: 'Hello Vue!'
  }
})
```

## 组件化应用构建

组件系统是 Vue 的另一个重要概念，因为它是一种抽象，允许我们使用小型、自包含和通常可复用的组件构建大型应用。

在 Vue 里，一个组件本质上是一个拥有预定义选项的一个 Vue 实例，在 Vue 中注册组件很简单：
```
// 定义名为 todo-item 的新组件
Vue.component('todo-item', {
  template: '<li>这是个待办项</li>'
})
```

现在你可以用它构建另一个组件模板：

```
<ol>
  <!-- 创建一个 todo-item 组件的实例 -->
  <todo-item></todo-item>
</ol>
```
但是这样会为每个待办项渲染同样的文本，这看起来并不炫酷，我们应该能将数据从父作用域传到子组件。让我们来修改一下组件的定义，使之能够接受一个属性：
```
Vue.component('todo-item', {
  // todo-item 组件现在接受一个
  // "prop"，类似于一个自定义属性
  // 这个属性名为 todo。
  props: ['todo'],
  template: '<li>{{ todo.text }}</li>'
})
```
现在，我们可以使用 v-bind 指令将待办项传到每一个重复的组件中：
```
<div id="app-7">
  <ol>
    <!--
      现在我们为每个 todo-item 提供待办项对象
      待办项对象是变量，即其内容可以是动态的。
      我们也需要为每个组件提供一个“key”，晚些时候我们会做个解释。
    -->
    <todo-item
      v-for="item in groceryList"
      v-bind:todo="item"
      v-bind:key="item.id">
    </todo-item>
  </ol>
</div>

Vue.component('todo-item', {
  props: ['todo'],
  template: '<li>{{ todo.text }}</li>'
})
var app7 = new Vue({
  el: '#app-7',
  data: {
    groceryList: [
      { id: 0, text: '蔬菜' },
      { id: 1, text: '奶酪' },
      { id: 2, text: '随便其他什么人吃的东西' }
    ]
  }
})
```
这只是一个假设的例子，但是我们已经设法将应用分割成了两个更小的单元，子单元通过 `props` 接口实现了与父单元很好的解耦。我们现在可以进一步为我们的 `todo-item` 组件实现更复杂的模板和逻辑的改进，而不会影响到父单元。

在一个大型应用中，有必要将整个应用程序划分为组件，以使开发可管理。在后续教程中我们将详述组件，不过这里有一个（假想的）使用了组件的应用模板是什么样的例子：

```
<div id="app">
  <app-nav></app-nav>
  <app-view>
    <app-sidebar></app-sidebar>
    <app-content></app-content>
  </app-view>
</div>
```

## 与自定义元素的关系

你可能已经注意到 Vue 组件非常类似于**自定义元素**——它是 **Web 组件规范**的一部分，这是因为 Vue 的组件语法部分参考了该规范。例如 Vue 组件实现了 **Slot API** 与 is 特性。但是，还是有几个关键差别：

1. Web 组件规范仍然处于草案阶段，并且尚无浏览器原生实现。相比之下，Vue 组件不需要任何补丁，并且在所有支持的浏览器（IE9 及更高版本）之下表现一致。必要时，Vue 组件也可以包装于原生自定义元素之内。

2. Vue 组件提供了纯自定义元素所不具备的一些重要功能，最突出的是跨组件数据流，自定义事件通信以及构建工具集成。
