# CSS3 的变换和动画

1. 变换（transform）

    CSS3 的变换（transform）属性主要有两个作用：
    
    一是构建一些 CSS2 中难以构造的图形，可以把一些过去由 Photoshop 做的工作交给浏览器渲染本身；
    
    二是配合 JavaScript 制作更为丰富的动画。
    
    transform 的兼容性如下：
    
    - Internet Explorer 10、Firefox、Opera 支持 transform 属性。
    - Internet Explorer 9 支持替代的 -ms-transform 属性（仅适用于 2D 转换）。
    - Safari 和 Chrome 支持替代的 -webkit-transform 属性（3D 和 2D 转换）。
    - Opera 只支持 2D 转换。
    
    ***
    
    （1） rotate 旋转
    
    transform 属性有很多选项， rotate 是比较常用的一种，rotate 英文是轮转、回转的意思，在 CSS3 中用于元素的旋转。
    
    为 rotate 传入一个角度值作为参数，元素将沿中轴线顺时针偏转这个角度值。
    
    如果用 rotateX（角度值）则表示沿 *x* 轴方向上旋转，同样地，用 rotateY（角度值）则表示沿 *y* 轴方向上旋转。
    
    如果将 rotateX 用在网页上，则效果如图所示：
    
    从图中可以发现，在平面的感官上，对于空白的区域来说，应用 rotateX 只是让图形高度变低了，上下边框变细了，但是一旦在元素中加入图片或文字，就很容易发现其中的差异。
    
    **注意： rotateZ 等效于 rotate。**
    
    如果需要在其他向量上应用旋转，可以使用 rotate3d(x, y, z, deg), 编辑 x, y, z 的值构建三维向量，最后一个参数是偏转的角度。
    
    （2） skew 扭曲
    
    skew 属性用于设置元素的扭曲变形。
    
    可以使用 skewX()、skewY() 表示单一方向上的 skew 变换。
    
    **注意： skew 没有 3D 和 skewZ 选项。**
    
    （3） scale 比例缩放
    
    scale 在英文中是尺寸的意思，在 transform 中用于尺寸缩放的控制。
    
    可以使用 scaleX()、scaleY()、scaleZ() 做单一方向上的缩放，不过元素内的图片、文字等也会被拉伸，造成失真的情况。
    
    （4） translate 位移
    
    transform 属性的 translate 参数定义了元素的位移。
    
    可以使用 translateX()、translateY()、translateZ() 表示单一方向上的位移。
    
    （5） transform 小结
    
     transform 属性用于元素的变换操作，常用的选项有以下几个：
     
     - rotate： 旋转，支持3D；
     - skew： 扭曲，不支持3D；
     - translate： 位移，支持3D；
     - scale： 缩放，支持3D。
     
     ***
     
2. transition——制作交互动画

    transition，中文译作过渡，在CSS中表示属性渐进变化的效果。
    
    transition 允许CSS的属性值在一定时间区间内平滑地过渡。
    
    这种效果可以在鼠标单击、获得焦点、被点击或对元素进行任何改变时触发，并圆滑地以动画效果改变CSS的属性值。
    
    transition 还包含设置渐进动画的函数，有6种：
    
    - ease： 逐渐变慢，默认值；
    - linear： 匀速；
    - ease-in： 加速；
    - ease-out： 减速；
    - ease-in-out： 加速然后减速；
    - cubic-bezier： 允许开发者自定义一个时间曲线。
    
     ***
    
    transition 还可以设置动画的延迟时间，表示延迟多少秒后执行动画。
    
    一个添加了所有属性的 transition 定义如下：
    
    ``` 
    transition: all .5s ease-in-out 1s; /* all 表示任意属性的变化都应用过渡动画效果。*/
    ```
    
    4个参数依次表示属性、过渡时间、过渡函数、延迟时间。
    
3. @keyframes——制作动画

    @keyframes 的基本语法：
    
    ```
    @keyframes spin {
        from {
            transform: rotateY(0);
        }
        to {
            transform: rotateY(-360deg);
        }
    }
    @keyframes spin {
        0% {
            transform: rotateY(0);
        }
        50% {
            transform: rotateY(-180deg);
        }       
        100% {
            transform: rotateY(-360deg);
        }
    }    
    
    ```
    @keyframes 声明后紧跟动画的名称，花括号内部就是一些不同时间段的样式规则。
    
    @keyframes 必须配合元素中定义的 animation 属性，它用于定义动画，语法如下：
    
    ``` animation: spin 8s infinite linear; ```
    
    第1个参数是动画名称，第2个参数是动画执行一次的时间，第3个参数是动画循环的次数，如果使用 infinite 则为无限循环，第4个参数是动画的速度函数，和 transition 中的速度函数一致。 
    
    此外还可以设置动画开始前的延迟时间、动画是否轮流反向播放等。
    
    ``` animation: name 8s linear 2s infinite altermate; /* alternate 表示动画正向循环完成后再反向循环。 */```    
    
    现在看到的动画是不可控的，在页面上一直循环，无法停止和启动。实际上，我们可以为元素添加 animation-play-state 属性。
    
    ``` animation-play-state: paused; ```
    
    paused 用于暂停动画，running 用于开启动画。这样就可以用 JavaScript 来控制动画的启动和暂停了。
    
    小结：
    
    - 使用百分比来规定变化发生的时间，或用关键词 from 和 to，等同于 0% 和 100%。
    - 0% 是动画的开始，100% 是动画的完成。
    - 为了得到最佳的浏览器支持，应该始终定义 0% 和 100% 选择器。
    - IE10、Firefox 以及 Opera 支持 @keyframes 规则和 animation 属性，Chrome 和 Safari 需要前缀 -webkit-。IE9 以及更早的IE版本，不支持 @keyframes 规则和 animation 属性。
    
 
