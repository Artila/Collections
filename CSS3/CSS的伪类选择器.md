# CSS的伪类选择器

伪类表示元素的状态：排序，鼠标是否悬停，是否已被访问过，光标是否指向等。

使用伪类选择器，就可以得到诸如有鼠标悬停的元素，父元素下的第n个子元素，已被访问过的链接等使用基本选择器无法进行区分的元素。

CSS2中只有:hover、:active、:visited、:link、:first-child等有限的几种伪类选择器，CSS3中增添了大量新的伪类选择器，帮助开发者更为灵活地选取元素。

1. 结构化伪类

   结构化伪类就是可以根据文档的结构来选取元素。
   
   在CSS3出现前，只有一个:first-child可以使用。
   
   （1） :nth-child(n)
   
    n表示一个简单的表达式，它可以是大于等于0的整数，也可以进行相应的计算。
    
    比如，n有时候表示全选，2n表示所有的偶数项，2n+1表示所有的奇数项，n+5表示从第5个元素开始进行全选。
   
   **IE6~8和FF3-浏览器不支持“:nth-child”选择器。**
   
   （2） :nth-last-child(n)
   
   它和“:nth-child”选择器获取元素的顺序正好相反，是从最后一个元素开始计算。
   
   （3） :nth-of-type(n)
   
   :nth-of-type(n) 和 :nth-child 类似，区别在于，如果使用p:nth-child(3)这样的条件时，一旦第3个元素不为<p>元素，这个选择器就不起作用，而p:nth-of-type(3)则查询的是第3个<p>元素。
   如果不加标签类型，在使用:nth-of-type(n)时就会自动选择所有并列元素的第n个。
   
   （4） :nth-last-of-type(n)
   
    和 :nth-of-type(n) 的区别只是获取元素的顺序相反，从最后一个元素开始计算。
    
   （5） :last-child
   
    :last-child 选择的是元素的最后一个子元素。
    
    **:last-child是CSS3新增的伪类选择器，而与之对应的:first-child则是在CSS2就已经加入了。IE6不支持:first-child，IE6~8不支持:last-child选择器。**
 
    （6） :first-of-type 和 :last-of-type
    
    :first-of-type 相当于 :nth-of-type(1)，:last-of-type 相当于 :nth-last-of-type(1)。
    
    （7） :only-child
    
    如果一个父元素只有一个子元素，那么选取这个子元素。
    
    如果加了限定条件，例如 p:only-child 则取交集，即如果一个父元素只有一个子元素，且这个子元素为<p>，这个选择器才会生效。
    
    （8） :only-of-type
    
    基本同 :only-child，区别在于如果不指定type而直接使用:only-of-type的话会造成body被选择，而 :only-child不会出现这种状况。
    
    （9） :root
    
    选择文档的根元素，对于HTML文档来说，根元素永远是<html>标签，由于:root是一个CSS3选择器，不兼容IE6~8，因此建议在实际开发中使用标签选择器（html）来代替:root。
    
    （10） :empty
    
    用来选择没有任何内容的元素，这里所说的内容指的是一点内容都没有，哪怕是一个空格。
    
    比如，有3个段落，其中一个段落完全是空的，但是段落标签还是会根据CSS的设置占据空间，想让这个p不显示，那么可以这样来写：
    ```
    p:empty {
      display: none;
    }
    ```
    **注意：IE6~8浏览器不支持:empty选择器。**
    
2. 目标伪类:target

   URL 前面有锚名称#，指向文档内某个具体的元素，例如`<a href="#id_name"></a>`。那么`<div id="id_name"></div>`这个被链接的元素就是目标元素（target element）。
   
   :target 选择器可用于选取当前活动的目标元素。
   ```
    <style>
	    :target {
	    	border: 2px solid #d4d4d4;
	    	background: #e5eecc;
	    }
    </style>
    
	<a href="#a1">跳转至内容1</a> /* 点击a1链接，则内容1的背景变为:target中的设置 */
	<a href="#a2">跳转至内容2</a> /* 点击a2链接，则内容2的背景变为:target中的设置，a1恢复原状。 */
	
	<p id="a1">内容1</p>
	<p id="a2">内容2</p>
   ```

3. 状态伪类

   用于表示表单元素的状态，虽然使用属性选择器可以达到相同的效果，但是使用状态伪类的语义性更强，更容易理解。
   
   （1） :enabled 和 :disabled
   
   表单元素可以设置 disabled 属性表示禁用，:enabled 选择器用于选择所有可用的元素，而 :disabled 则用于选择所有已被禁用的元素。
   
   在IE6~8中可以选择属性选择器来代替：
   ```
   input:disabled{
     opacity: 0;
   }   
   /* 使用属性选择器达到和使用 :disabled 一样的效果。*/
   input[disabled]{
     opacity: 0;
   }
    ```
   
   （2） :checked
   
    input 表单中的 checkbox 和 radio 都使用 checked 属性表示是否选中，**只要 checked 属性存在**，使用 checked=false 或 checked=0 都会表示单选/复选框被选中。
    
    :checked 选择器用于选择所有被选中的 checkbox 或 radio 标签，例如：
    ```
    /* 将被选中的输入框设置为透明 */
    input:checked {
      opacity: 0;
    }
    ```
    可以使用属性选择器进行替代，而且兼容性上，使用属性选择器可以兼容所有的浏览器。
    ```
    /* 使用属性选择器达到和使用 :checked 一样的效果 */
    input[checked] {
      opacity: 0;
    }
    ```    
    
    （3） :indeterminate 和 :default
    
     :default 状态伪类选择器用来指定当前元素处于非选取状态的单选框或复选框的样式；
     
     :indeterminate 状态伪类选择器用来指定当前页面打开时，某组中的单选框或复选框元素还没有选取状态时的样式。
     
     **注意：这两个选择器只有Opera浏览器才支持，因此强烈不建议使用。**
     
4.  否定伪类:not(S)
    
    :not(selector) 选择器匹配非指定元素/选择器的每个元素，例如：
    ```
    /* 除了段落（<p>）标签以外的所有HTML元素的背景颜色都设置为红色。 */
    :not(p) {
      background: red;
    }
    ```
    还可以配合其他选择器一起使用。
    ```
    /* <div>标签的子元素中，class不为test的所有其他元素。 */
    div :not(.test) {
      background: red;
    }
    ``` 
    **和其他CSS3选择器一样，:not(S)选择器不支持IE6~8。**
