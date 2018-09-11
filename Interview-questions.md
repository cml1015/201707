# 201707
js学习资料
# HTML&CSS：
### 对Web标准的理解

标签闭合、标签小写、不乱嵌套、提高搜索机器人搜索几率、使用外 链css和js脚本、结构行为表现的分离、文件下载与页面速度更快、内容能被更多的用户所访问、内容能被更广泛的设备所访问、更少的代码和组件，容易维 护、改版方便，不需要变动页面内容、提供打印版本而不需要复制内容、提高网站易用性；

### 浏览器内核差异

浏览器内核又可以分成两部分：渲染引擎(layout engineer或者Rendering Engine)和JS引擎。它负责取得网页的内容（HTML、XML、图像等等）、整理讯息（例如加入CSS等），以及计算网页的显示方式，然后会输出至显示器或打印机。

**主流浏览器所使用的内核分类：**

- **Trident内核：** IE,MaxThon,TT,The World,360,搜狗浏览器等（又称MSHTM）
- **Gecko内核**：Netscape6及以上版本，FF,MozillaSuite/SeaMonkey等
- **Presto内核：** Opera7及以上（Opera内核原为：Presto，现为：Blink;）
- **Webkit内核：** Safari,Chrome等

**优缺点：**

- **Trident内核：** 是IE的浏览器内核，在早期占有大量的市场份额。由于IE的高市场占有率，微软也很长时间没有更新Trident内核，导致Trident内核和W3C标准脱节，Trident内核的大量Bug等安全问题没有得到解决，
- **Gecko内核：** 优点就是功能强大、丰富，可以支持很多复杂网页效果和浏览器扩展接口，但是代价是也显而易见就是要消耗很多的资源，比如内存。
- **Presto内核：** Presto内核被称为公认的浏览网页速度最快的内核，这得益于它在开发时的天生优势，在处理JS脚本等脚本语言时，会比其他的内核快3倍左右，缺点就是为了达到很快的   速度而丢掉了一部分网页兼容性。
- **Webkit内核：** 优点就是网页浏览速度较快，虽然不及 Presto 但是也胜于 Gecko 和 Trident，缺点是对于网页代码的容错性不高，也就是说对网页代码的兼容性较低，会使一些编写不标准的网页无法正确显示。

## 兼容性

- FF下给 div 设置 padding 后会导致 width 和 height 增加, 但IE不会.(可用!important解决)

- 浏览器默认的margin和padding不同。解决方法：加一个全局的`*{margin:0;padding:0;}`来统一

- display:inline-block;IE6，7下不兼容。解决方法：用`float:left`

- 透明度 解决方法：IE下使用filter:alpha(opacity=50)滤镜，其他浏览器用opacity:0.5;

- png24位的图片在iE6浏览器上出现背景。解决方法：做成PNG8

- IE6双边距BUG,float引起的。解决方案是使用`_display：inline`使浮动忽略

- IE下，可以使用获取常规属性的方法来获取自定义属性，也可以使用getAttribute()获取自定义属性； Firefox下，只能使用getAttribute()获取自定义属性。解决方法：统一通过getAttribute()获取自定义属性。
- IE63像素问题 使用多个float和注释引起的。解决方法：使用dislpay:inline -3px
- select 在ie6下遮盖。解决方法：使用iframe嵌套
- 超链接访问过后 hover 样式就不出现了，被点击访问过的超链接样式不在具有 hover 和 active 。解决方法：改变CSS属性的排列顺序：L-V-H-A: a:link{ }  a:visited{ } a:hover{ } a:active{ }
- Chrome中文界面下默认会将小于 12px 的文本强制按照 12px 显示。解决方法：可通过加入 CSS 属性 -webkt-text-size-adjust:none;解决
- IE下，even对象有x，y属性，但是没有pageX，pageY属性，但是没有x，y属性。解决方法：（条件注释）缺点是在IE浏览器下可能会增加额外的HTTP请求数

## 清除浮动的几种方式，优缺点

1. 使用空标签清除浮动  `<div style=”clear:both”></div>`

- 优点：通俗易懂，容易掌握；
- 缺点：增加无意义的标签，有违结构与表现的分离

2. 父元素设置 `overflow：hidden`

必须定义width或zoom:1，同时不能定义height，使用overflow:hidden时，浏览器会自动检查浮动区域的高度

- 优点：简单，代码少，浏览器支持好
- 缺点：不能和position配合使用，因为超出的尺寸的会被隐藏

3. 给父元素添加`clear:both`类

- 优点：结构和语义化完全正确,代码量居中;
- 缺点：复用方式不当会造成代码量增加。


4. 父级div定义伪类:after和zoom(用于非IE浏览器)

利用:after和:before来在元素内部插入两个元素块，从面达到清除浮动的效果。
IE8以上和非IE浏览器才支持:after，原理和方法2有点类似，zoom(IE转有属性)可解决ie6,ie7浮动问题

- 优点：浏览器支持好，不容易出现怪问题
- 缺点：代码多，不少初学者不理解原理，要两句代码结合使用，才能让主流浏览器都支持,`推荐使用`，建议定义公共类，以减少CSS代码

```
.clearfix:after {
   content: ".";
   visibility: hidden;
   display: block;
   height: 0;
   clear: both;
}
/* IE 6/7浏览器 (触发hasLayout) */
.clearfix {
  *zoom:1;
}

```
5. 父级div定义overflow:auto

必须定义width或zoom:1，同时不能定义height，使用overflow:auto时，浏览器会自动检查浮动区域的高度

- 优点：简单，代码少，浏览器支持好
- 缺点：内部宽高超过父级div时，会出现滚动条。

6. 父级div定义height

父级div手动定义height，就解决了父级div无法自动获取到高度的问题

- 优点：简单，代码少，容易掌握
- 缺点：只适合高度固定的布局，要给出精确的高度，如果高度和父级div不一样时，会产生问题,`不推荐`使用，只建议高度固定的布局时使用

7. 父元素也设置浮动

- 优点：不存在结构和语义化问题，代码量极少;
- 缺点：使得与父元素相邻的元素的布局会受到影响，不可能一直浮动到body，`不推荐`使用。

## 图片如何实现垂直居中的

```
<p><img src="1.png" alt="" ></p>
```

### 1. 利用定位和margin:auto
```
p{
    position: relative;
    border: 1px solid red;
    height: 400px;
}
img{
    position: absolute;
    left: 0;
    top: 0;
    right: 0;
    bottom: 0;
    margin: auto;
    width: 200px;
    height: 200px;
}
```

### 2.利用定位和css3的transform属性

```
p{
    position: relative;
    border: 1px solid red;
    height: 400px;
}
img{
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%,-50%);
    width: 200px;
    height: 200px;
}
```

## css hack你知道哪些？

一般来说是针对不同的浏览器写不同的CSS,就是 CSS Hack。IE浏览器Hack一般又分为三种，条件Hack、属性级Hack、选择符Hack

所有浏览器 通用 height: 100px;
IE6 专用 _height: 100px;
IE7 专用 *+height: 100px;
IE6、IE7 共用 *height: 100px;
IE7、FF 共用 height: 100px !important;


**css内部hack**

（1）前缀

*html *前缀只对IE6生效

*+html *+前缀只对IE7生效

（2）后缀

“-″减号是IE6专有的hack —待验证

“\9″ IE6/IE7/IE8/IE9/IE10都生效,11不生效

“\0″ IE8/IE9/IE10都生效，是IE8/9/10/11的hack

“\9\0″ 只对IE8/IE9/IE10生效hack


**css html头部判断**

```
所有的IE可识别 ：<!–[if IE]> Only IE <![end if]–>
只有IE5.0可以识别 ：<!–[if IE 5.0]> Only IE 5.0 <![end if]–>
IE5.0包换IE5.5都可以识别：<!–[if gt IE 5.0]> Only IE 5.0+ <![end if]–>
仅IE6可识别：<!–[if lt IE 6]> Only IE 6- <![end if]–>
IE6以及IE6以下的IE5.x都可识别：<!–[if gte IE 6]> Only IE 6/+ <![end if]–>
仅IE7可识别：<!–[if lte IE 7]> Only IE 7/- <![end if]–>
```

**样式识别**

```
IE都能识别*;标准浏览器(如FF)不能识别*；
IE6能识别*；不能识别 !important;
IE7能识别*，能识别!important;
FF不能识别*，但能识别!important;
```



## 假设高度已知，请写出三栏布局，其中左栏、右栏宽度各为300px，中间自适应

### 1.绝对定位

```
//css
.left,.right{ position:absolute; top:0; width:300px; height:400px;}
.left{ background:#99F; left:0;}
.right{ background:#39F; right:0;}
.main{ height:400px; background:#CCC; margin:0 300px;}

//html
<div class="left">左</div>
<div class="right">右</div>
<div class="main">中</div>
```

### 2.flex布局

```
.left{ width:300px; height:400px; background:#99F; left:0;}
.main{ height:400px; background:#CCC; flex: 1}
.right{ width:300px; height:400px; background:#99F; left:0;}

<div class="left"></div>
<div class="main"></div>
<div class="right"></div>
```


## CSS选择器有哪些？有哪些新特性？有哪些伪类？

### 1.CSS选择器

1. id选择器（ # myid）

2. 类选择器（.myclassname）

3. 标签选择器（div, h1, p）

4. 相邻选择器（h1 + p）

5. 子选择器（ul < li）

6. 后代选择器（li a）

7. 通配符选择器（ * ）

8. 属性选择器（a[rel = "external"]）

9. 伪类选择器（a: hover, li: nth - child）

 > !important >  id > class > tag

 > important 比 内联优先级高

### 2.新特性

1. CSS3实现圆角（border-radius），阴影（box-shadow），

2. 对文字加特效（text-shadow、），线性渐变（gradient），旋转（transform）

3. transform:rotate(9deg) scale(0.85,0.90) translate(0px,-30px) skew(-9deg,0deg);// 旋转,缩放,定位,倾斜

4. 增加了更多的CSS选择器  多背景 rgba

5. 在CSS3中唯一引入的伪元素是 ::selection.

6. 媒体查询，多栏布局

7. border-image

### 3.伪类

1.  `p：nth-child(n)`    选择所有p元素的第n个子元素

2.  `p：nth-last-child(n) `   选择所有p元素倒数的第n个子元素
3.  `p：only-child ` 选择所有仅有一个子元素的p元素
4.  `p：last-child`  选择所有p元素的最后一个子元素
5.  `p：nth-of-type(n)`   选择所有p元素第二个为n的子元素
6.  `p：only-of-type()`  选择所有仅有一个子元素为p的元素
7.  `p：empty`    选择所有没有子元素的p元素。
8.  `：checked ` 选择所有选中的表单元素


## 布局

## 谈谈你对CSS盒模型的认识

### 1.标准模型和IE模型的区别?

1 有两种， IE 盒子模型、标准 W3C 盒子模型；IE的content部分包含了 border 和 padding;

2 盒模型： 内容(content)、填充(padding)、边界(margin)、 边框(border).

### 2.CSS是如何设置这两种模型?

浏览器默认的方式是`content-box(标准模型 )`，通过改变样式`box-sizing`来切换`content-box(标准模型)`和`border-sizing(IE模型)`

### 3.JS如何设置和获取盒模型对应的宽和高?

- dom.style.width/height

  缺点:只能获取内联样式中的style值。
- dom.currentStyle.width/height

  缺点：只能获取IE浏览器下的值。兼容性不好
- window.getComputerStyle(dom).width/height

  缺点：只能用来获取不能用来设置改变值
- dom.getBoundingClientRect().width/height

  优点：能够用dom.getBoundingClientRect()获取一个矩形对象，其中包括top,left,right,bottom4个属性，以及返回的注意（IE盒子模型的宽高）。

### 4.什么是优雅降级和渐进增强?

优雅降级 ：一开始就构建完整的功能，然后再针对低版本浏览器进行兼容。
渐进增强 ：针对低版本浏览器进行构建页面，保证最基本的功能，然后再针对高级浏览器进行效果、交互等改进和追加功能达到更好的用户体验。

区别： a. 优雅降级是从复杂的现状开始，并试图减少用户体验的供给 b. 渐进增强则是从一个非常基础的，能够起作用的版本开始，并不断扩充，以适应未来环境的需要 c. 降级（功能衰减）意味着往回看；而渐进增强则意味着朝前看，同时保证其根基处于安全地带


## Flexbox


## 谈谈你对BFC的了解

### 1.什么是BFC?

BFC，浮动元素和绝对定位元素，非块级盒子的块级容器（例如 inline-blocks, table-cells, 和 table-captions），以及overflow值不为“visiable”的块级盒子，都会为他们的内容创建新的块级格式化上下文。

在一个块级格式化上下文里，盒子从包含块的顶端开始垂直地一个接一个地排列，两个盒子之间的垂直的间隙是由他们的margin 值所决定的。两个相邻的块级盒子的垂直外边距会发生叠加。

在块级格式化上下文中，每一个盒子的左外边缘（margin-left）会触碰到容器的左边缘(border-left)（对于从右到左的格式来说，则触碰到右边缘），即使存在浮动也是如此，除非这个盒子创建一个新的块级格式化上下文。


### 2.如何创建BFC?

- 根元素或其它包含它的元素；

- 浮动 (元素的float不为none)；
- 绝对定位元素 (元素的position为absolute或fixed)；
- 行内块inline-blocks(元素的 display: inline-block)；
- 表格单元格(元素的display: table-cell，HTML表格单元格默认属性)；
- overflow的值不为visible的元素；
- 弹性盒 flex boxes (元素的display: flex或inline-flex)；

> 其中，最常见的就是overflow:hidden、float:left/right、position:absolute。也就是说，每次看到这些属性的时候，就代表了该元素以及创建了一个BFC了。

### 3.BFC使用场景?

1.解决margin叠加问题
当盒子上下排布，上方盒子margin-bottom:50px;下面的盒子margin-top:50;那么神奇的事情就发生了，两个盒子按照叠加来算的话，距离应该是100px，但是我们发现实际上两个margin值进行了叠加，只剩下50px，那么这个时候我们就可以触发BFC模式，给其中一个盒子添加一个父级元素；

2.用于布局
元素的左外边距会触碰到包含块容器的做外边框，就算存在浮动也会如此，那么我们可以利用这种方式来一个两列布局，第一个盒子浮动，第二个盒子margin-left赋值；

3.用于清除浮动，计算BFC高度
我们发现由于里面两个子元素浮动的关系，两个box已经脱离了父元素的包含块，父元素高度已经塌陷，我们需要让父元素包含两个box子元素，这样计算高度时，两个浮动子元素就会参与，所以我们要闭合浮动，触发父元素的BFC，例如overflow:hidden;

# JS

## DOM事件

### 1.DOM事件级别有哪些?

- DOM事件模型分为三个等级，分别是0级、1级、2级。

    - 0级是最早的，而且目前所有的浏览器仍支持0级DOM模型。

    - 2级的典型特点是事件传播的阶段，（捕获阶段，直接目标阶段，起泡阶段），注意在第三个阶段“起泡阶段”在IE6中不支持。

### 2.描述DOM事件捕获和冒泡的具体流程?

冒泡和捕获的区别是冒泡事件是先触发子元素事件，再触发父元素事件，这个是冒泡。捕获是先触发父元素事件，再触发子元素事件。简单的来说，冒泡的顺序是由内到外，捕获的顺序是由外到内。


### 3.Event对象的常见应用场景?

在事件传播的过程中，可以随时用Event对象的stopPropagation()方法停止事件传播。

### 4.事件委托是什么？

让利用事件冒泡的原理，让自己的所触发的事件，让他的父元素代替执行！

### 5.事件冒泡,e.target和e.currentTarget的区别

target指的是事件的真正触发者，currenttarget指的是事件的监听者，当不存在冒泡或者捕获的情况下，通常两者指向的对象为同一个，但是如果存在冒泡或者捕获，就会指向各自所产生的对象


### 6.浏览器的兼容问题(js)

- 标准的事件绑定方法函数为addEventListener，但IE下是attachEvent；

-  事件的捕获方式不一致，标准浏览器是由外至内，而IE是由内到外，但是最后的结果是将IE的标准定为标准

-  window.event获取的。并且获取目标元素的方法也不同，标准浏览器是event.target，而IE下是event.srcElement

-  在低版本的IE中获取的日期处理函数的值不是与1900的差值，但是在高版本的IE中和标准浏览器保持了一致，获取的值也是与1900的差值。
 比如：var year= new Date().getYear();

-  ajax的实现方式不同，这个我所理解的是获取XMLHttpRequest的不同，IE下是activeXObject

-  IE中不能操作tr的innerHtml7.获得DOM节点的父节点、子节点的方式不同
其他浏览器：parentNode  parentNode.childNodes
IE：parentElement parentElement.children

## JS原生

### 1.JS中有哪些数据类型

String、Number、Boolean、Array、Object、Null、Undefined

### 2.什么是闭包？闭包作用？在工作中是如何应用的?

- 闭包是指有权访问另一个函数作用域中的变量的函数，并且在闭包内部形成一个外部无法访问的局部作用域。创建闭包的常见方式是在一个函数内部创建另一个函数。

- 作用：一个是可以读取函数内部的变量，另一个就是让这些变量的值始终保持在内存中，不会在f1调用后被自动清除。

- 如何应用：

    - 采用函数引用方式的setTimeout调用。

    - 将函数关联到对象的实例方法。

    - 封装相关的功能集。
    
[另一种解释]

闭包是什么

你可以这样回答：

我个人理解，闭包是就是函数中的函数，里面的函数可以访问外面函数的变量，外面的变量的是这个内部函数的一部分。

```
<script>  
    function  outer(){  
        var num=0;//内部变量  
       return  function add(){//通过return返回add函数，就可以在outer函数外访问了。  
            num++;//内部函数有引用，作为add函数的一部分了  
           console.log(num);  
        };  
    }  
    var func1=outer();//  
    func1();//实际上是调用add函数， 输出1  
    func1();//输出2  
    var func2=outer();  
    func2();// 输出1  
    func2();// 输出2  
</script>  
```
闭包的作用

1.使用闭包可以访问函数中的变量。

2.可以使变量长期保存在内存中，生命周期比较长。

加分项

闭包不能滥用，否则会导致内存泄露，影响网页的性能。闭包使用完了后，要立即释放资源，将引用变量指向null。


### 3.JS实现继承的几种方式?

-  **原型链:** 利用原型让一个引用类型继承另外一个引用类型的属性和方法。
构造函数，原型，实例之间的关系：每个构造函数都有一个原型对象，原型对象包含一个指向构造函数的指针，而实例都包含一个指向原型对象的内部指针。
- **借用构造函数:** 在子类型构造函数的内部调用超类构造函数，通过使用call()和apply()方法可以在新创建的对象上执行构造函数。

- **组合继承:** 将原型链和借用构造函数的技术组合在一块，从而发挥两者之长的一种继承模式。
- **原型式继承:** 借助原型可以基于已有的对象创建新对象，同时还不必须因此创建自定义的类型。
- **寄生式继承:** 创建一个仅用于封装继承过程的函数，该函数在内部以某种方式来增强对象，最后再像真正是它做了所有工作一样返回对象。
- **寄生组合式继承:** 通过借用函数来继承属性，通过原型链的混成形式来继承方法
### 4.创建对象的三种方式?

- 通过”字面量“方式创建。
- 通过”构造函数“方式创建
- 通过object方式创建

### 5.new Person()时发生了什么?

 1.创建一个空对象；
 ```
 var obj=new Person();  
 ```

 2.设置原型链；
 ```
 obj.__proto__= Person.prototype; 
 ```

 3.让Person中的this指向obj，并执行Person的函数体;
 ```
 var result =Person.call(obj);  
 ```

 4.判断Person的返回值类型：

如果是值类型，返回obj。如果是引用类型，就返回这个引用类型的对象。
```
if (typeof(result) == "object"){  
  Person = result;  
}  
else{  
    Person = obj;;  
} 
```


### 6.什么是深拷贝和浅拷贝？自己不用JSON.parse实现一个深拷贝的方法

深复制和浅复制最根本的区别在于是否是真正获取了一个对象的复制实体，而不是引用，

　　1）深复制在计算机中开辟了一块内存地址用于存放复制的对象，

　　2）而浅复制仅仅是指向被复制的内存地址，如果原地址中对象被改变了，那么浅复制出来的对象也会相应改变。

所谓的浅复制，只是拷贝了基本类型的数据，而引用类型数据，复制后也是会发生引用，我们把这种拷贝叫做“（浅复制）浅拷贝”。
而深复制的话，我们要求复制一个复杂的对象，那么我们就可以利用递归的思想来做，及省性能，又不会发生引用。


### 7.手工模拟完整的bind方法



### 8.什么是节流和防抖？

- 函数节流和函数防抖，两者都是优化高频率执行js代码的一种手段。
- 函数节流是指一定时间内js方法只跑一次。比如人的眨眼睛，就是一定时间内眨一次。这是函数节流最形象的解释。函数节流应用的实际场景，多数在监听页面元素滚动事件的时候会用到。
- 函数防抖是指频繁触发的情况下，只有足够的空闲时间，才执行代码一次。函数防抖的应用场景，最常见的就是用户注册时候的手机号码验证和邮箱验证了。只有等用户输入完毕后，前端才需要检查格式是否正确，如果不正确，再弹出提示语。

### 9.上拉刷新和下拉加载的实现原理？

向 ListView 头部和尾部分别添加 HeaderView、FooterView，默认使其隐藏。下拉时，逐渐使 HeaderView 显示，并不断改变 HeaderView 上的文字为“下拉刷新”、“松开刷新”和“正在加载”，当状态改为正在加载时，调接口加载数据，加载完成恢复原状。上拉时，当 ListView 滑动到最底部并且松开手指，马上显示 FooterView ，调接口加载数据，完成加载恢复默认。

### 10.写一个验证邮件的正则表达式

只允许英文字母、数字、下划线、英文句号、以及中划线组成

**分析邮件名称部分：**

- 26个大小写英文字母表示为a-zA-Z
- 数字表示为0-9
- 下划线表示为_
- 中划线表示为-
- 由于名称是由若干个字母、数字、下划线和中划线组成，所以需要用到+表示多次出现

根据以上条件得出邮件名称表达式：`[a-zA-Z0-9_-]+`

**分析域名部分：**

 一般域名的规律为“[N级域名][三级域名.]二级域名.顶级域名”，比如“qq.com”、“www.qq.com”、“mp.weixin.qq.com”、“12-34.com.cn”，分析可得域名类似“** .** .** .**”组成。

- “**”部分可以表示为`[a-zA-Z0-9_-]+`
- “.**”部分可以表示为`\.[a-zA-Z0-9_-]+`
- 多个“.**”可以表示为`(\.[a-zA-Z0-9_-]+)+`

域名部分可以表示为`[a-zA-Z0-9_-]+(\.[a-zA-Z0-9_-]+)+`

**最终表达式：**

由于邮箱的基本格式为“名称@域名”，需要使用“^”匹配邮箱的开始部分，用“$”匹配邮箱结束部分以保证邮箱前后不能有其他字符，所以最终邮箱的正则表达式为：

 ` ^[a-zA-Z0-9_-]+@[a-zA-Z0-9_-]+(\.[a-zA-Z0-9_-]+)+$`

### 11.事件绑定和普通事件的区别（可以举例说明）

普通事件只支持单个事件，而事件绑定可以添加多个事件

```
<script type="text/javascript">
var btn=document.getElementById("btn");
btn.onclick=function(){
    alert("1普通事件");
}
btn.onclick=function(){
    alert("2普通事件");
}

btn.addEventListener("click",function(){
    alert("绑定事件1");
})
btn.addEventListener("click",function(){
    alert("绑定事件2");
})

//执行结果：普通事件2、事件绑定1、事件绑定2。
</script>
```

### 12.javascript 模版引擎用过哪些？实现原理是什么？

### 13.合并两个对象

### 14.动态向一个div中插入1000个div标签，如何实现？（考性能）

### 15.html5新特性

1. 语义特性（Semantic）
2. 本地存储特性（OFFLINE & STORAGE）
3. 设备访问特性 (DEVICE ACCESS)
4. 连接特性（CONNECTIVITY）
5. 网页多媒体特性(MULTIMEDIA)
    - 支持网页端的Audio、Video等多媒体功能， 与网站自带的APPS，摄像头，影音功能相得益彰。
6. 三维、图形及特效特性（3D, Graphics & Effects)于SVG、Canvas、WebGL及CSS3的3D功能
7.  性能与集成特性（Performance & Integration）
    - HTML5会通过XMLHttpRequest2等技术，解决以前的跨域等问题，帮助您的Web应用和网站在多样化的环境中更快速的工作。

### 16.严格模式和非严格模式的区别


| 严格模式      |    非严格模式 |
| :-------- | :--------|
| 禁止使用with语句  | 允许使用with语句 |
| 所有变量要先声明     |   使用未声明的变量将隐式声明为全局变量 |
| 函数(非方法)中的this是undefined      |    this是全局对象 |
|call()和apply()传入的第一个值不会被转换|call()和apply()传入的第一个值如果是null和undefined，则会被全局对象取代，如果是原始值则转换为对应的包装对象|
|给只读属性和不可扩展的对象创建新成员将抛出类型错误异常|只是简单的操作失败|
|传入eval()的代码不能在定义变量和函数|变量和函数定义在eval()创建的新作用域中|
|函数中的arguments对象拥有传入函数值的静态副本||
|delete后跟非法标识符将抛出语法错误异常|只是简单的返回false|
|delete删除不可配置的属性将抛出类型错误异常|只是简单的返回false|
|在对象直接量中定义多个同名属性将产生语法错误|不会报错|
|函数声明存在多个同名的参数将产生语法错误|不会报错|
|不允许使用八进制直接量|某些实现是允许的|
|eval和arguments当作关键字，并且不允许更改||
|限制了对栈的检测能力，arguments.caller和arguments.callee将抛出类型错误异常||

### 17.对于js中浮点数计算会丢失精度的问题，你有什么解决思路？

### 18.JavaScript 中 this 的工作原理
1.在函数中，this通常是一个隐含的参数
2.在函数外（顶级作用域中），在浏览器中this指向的是全局对象；在NodeJs中this指向的是导出（module）的模块（export）
3.传递到eval()中的字符串：如果eval()是被直接调用的，this指向的是当前对象，如果eval()是被间接调用的，this指向的是全局对象

### 19.call和apply的作用是什么？区别是什么？
- call和apply的功能基本相同，都是实现继承或者转换对象指针的作用；
- 唯一不同的是前者参数是罗列出来的，后者是存到数组中的；
- call或apply功能就是实现继承的；与面向对象的继承extends功能相似；但写法不同；
- 语法：
.call(对象[,参数1，参数2,....]);//此地参数是指的是对象的参数，非方法的参数；
.apply(对象,参数数组)//参数数组的形式:[参数1，参数2,......]

# JQuery

## jquery.extend , jquery.fn.extend的区别

1. extend方法挂载在jQuery和jQuery.fn两个不同对象上方法，但在jQuery内部代码实现的是相同的，只是功能却不太一样；

jQuery.extend(): Merge the contents of two or more objects together into the first object.(把两个或者更多的对象合并到第一个当中)；

jQuery.fn.extend():Merge the contents of an object onto the jQuery prototype to provide new jQuery instance methods.(把对象挂载到jQuery的prototype属性，来扩展一个新的jQuery实例方法)

2. 我们先把jQuery看成了一个类，这样好理解一些。jQuery.extend()，是扩展的jQuery这个类。

假设我们把jQuery这个类看成是人类，能吃饭能喝水能跑能跳，现在我们用jQuery.extend这个方法给这个类拓展一个能说话speak()的技能。这样的话，不论是男人，女人，xx人.....等能继承这个技能（方法）了。

可以如下图这样写着：
```
JQuery.extend({
    speak:function(){
         alert("how are you!");
    }
});
```
3. 理解 jQuery.fn.extend()

从字面理解嘛，这个拓展的是jQuery.fn的方法。jQuery.fn是啥玩意呢？
```
jQuery.fn = jQuery.prototype = {
      init:funtion(selector,context){
            //..... 
 
     }
}
```

jQuery.fn.extend拓展的是jQuery对象（原型的）的方法

那就是说，jQuery.fn.extend拓展的方法，你得用在jQuery对象上面才行啊！他得是张三李四王五痳六这些实例化的对象才能用啊。

说白了就是得这么用（假设xyz()是拓展的方法）：
$('selector').xyz();

调用方法如下：

```
<script type="text/javascript">
        (function($){
               $.fn.extend({
                   speak:function(){
                       alert("how are you!");
                   }
               });
        })(jQuery);
    </script>
    <script type="text/javascript">
        $(document).ready(function(){
            $("div").speak();
        })
    </script>
  ```
  
4. 两者区别总结：

4.1 两者调用方式不同：

       jQuery.extend(),一般由传入的全局函数来调用，主要是用来拓展个全局函数，如$.init()，$.ajax();

       jQuery.fn.extend(),一般由具体的实例对象来调用，可以用来拓展个选择器，例如$.fn.each();

4.2 两者的主要功能作用不同：

        jQuery.extend(object); 为扩展jQuery类本身，为自身添加新的方法。

        jQuery.fn.extend(object);给jQuery对象添加方法

 4.3 大部分插件都是用jQuery.fn.extend()

5. JQuery的extend扩展方法：

5.1 Jquery的扩展方法原型是:

extend(dest,src1,src2,src3...);
         它的含义是将src1,src2,src3...合并到dest中,返回值为合并后的dest,由此可以看出该方法合并后，是修改了dest的结构的。
         如果想要得到合并的结果却又不想修改dest的结构，可以如下使用：
 var newSrc=$.extend({},src1,src2,src3...)//也就是将"{}"作为dest参数。
           这样就可以将src1,src2,src3...进行合并，然后将合并结果返回给newSrc了。如下例：

var result=$.extend({},{name:"Tom",age:21},{name:"Jerry",sex:"Boy"})
那么合并后的结果：  result={name:"Jerry",age:21,sex:"Boy"}
     也就是说后面的参数如果和前面的参数存在相同的名称，那么后面的会覆盖前面的参数值。

5.2 省略dest参数
           上述的extend方法原型中的dest参数是可以省略的，如果省略了，则该方法就只能有一个src参数，而且是将该src合并到调用extend方法的对象中去，如：
5.2.1 $.extend(src)
 　　该方法就是将src合并到jquery的全局对象中去，如：

  $.extend({
      hello:function(){alert('hello');}
  });
       就是将hello方法合并到jquery的全局对象中。

5.2.2 $.fn.extend(src)
 　　该方法将src合并到jquery的实例对象中去，如:

  $.fn.extend({
         hello:function(){alert('hello');}
  });
       就是将hello方法合并到jquery的实例对象中。

 　　下面例举几个常用的扩展实例：

$.extend({net:{}});
         这是在jquery全局对象中扩展一个net命名空间。

$.extend($.net,{
       hello:function(){alert('hello');}
})
        这是将hello方法扩展到之前扩展的Jquery的net命名空间中去。

5.2.3 Jquery的extend方法还有一个重载原型：

 extend(boolean,dest,src1,src2,src3...)
        第一个参数boolean代表是否进行深度拷贝，其余参数和前面介绍的一致，什么叫深层拷贝，我们看一个例子：

var result=$.extend( true, {}, 
    { name: "John", location: {city: "Boston",county:"USA"} }, 
    { last: "Resig", location: {state: "MA",county:"China"} } 
);
        我们可以看出src1中嵌套子对象location:{city:"Boston"},src2中也嵌套子对象location:{state:"MA"},第一个深度拷贝参数为true，那么合并后的结果就是： 

var result={
       name:"John",last:"Resig", location:{city:"Boston",state:"MA",county:"China"}
}
       也就是说它会将src中的嵌套子对象也进行合并，而如果第一个参数boolean为false，我们看看合并的结果是什么，如下

 var result=$.extend( false, {}, 
       { name: "John", location:{city: "Boston",county:"USA"} },  
       { last: "Resig", location: {state: "MA",county:"China"} 
 }); 
        那么合并后的结果就是:

var result={
      name:"John",last:"Resig",location:{state:"MA",county:"China"}
}
       以上就是$.extend()在项目中经常会使用到的一些细节。


## 谈一下jquery中的bind，live，delegate，on区别

```
<ul id="members" data-role="listview" data-filter="true"><!-- ... more list items ... -->  
    <li>  
<h3>John Resig</h3>  
<a href="detail.html?id=10">  
<strong>jQuery Core Lead</strong>  
   
Boston, United States  
</a></li>  
<!-- ... more list items ... --></ul> 
```
**.bind()**

.bind()注册的事件直接指向相对应的DOM元素。这个方法从jQuery 1.0都有了，并且这个方法能够很酷的处理跨浏览器的事件绑定问题。对，这个方法用起来很方便。但是问题来了，就是各种各样的性能问题，如下：
```
/* The .bind() method attaches the event handler directly to the DOM 
element in question ( "#members li a" ). The .click() method is 
just a shorthand way to write the .bind() method. */  
   
$( "#members li a" ).bind( "click", function( e ) {} );  
$( "#members li a" ).click( function( e ) {} ); 
```
**优点**
- 跨浏览器
- 非常方便和快捷地绑定事件
- 简单的实现方法（.click() .hover() ,etc…）让它用起来很方便
- 对于简单的ID选择器来说，使用.bind()不仅方便，而且当触发这个事件的时候能够即时响应。

**缺点**

- 这个方法会附加相同的处理程序到每一个匹配到的元素上
- 对于动态添加的属于匹配到的元素，不会被触发事件的
- 性能问题，对于处理大量的匹配元素的时候
- 如果在页面加载前要处理添加事件的话，会影响加载效率的


**.live()**

.live()方法使用的是事件委托的概念来执行所谓的“神奇方法”。调用.live()方法看起来和调用.bind()方法一样，非常方便。但是他们下面的实现原理却不同。.live()方法附加事件处理程序到根一级的document上来关联匹配到的元素和事件信息。通过注册事件处理程序到document上来允许事件处理程序通过冒泡来绑定事件和匹配的元素（译者：注意，事件其实在document上的）。一旦事件冒泡到document的时候，jQuery判断选择器和事件处理程序是否有匹配到的，如果有的话，则调用对应的事件处理程序。很明显的会在用户使用的过程中有性能问题，但是在绑定注册的时候是非常的迅速的。

```
/* The .live() method attaches the event handler to the root level 
document along with the associated selector and event information 
( "#members li a" & "click" ) */  
   
$( "#members li a" ).live( "click", function( e ) {} );  
```
**优点**

- 相对于.bind()的循环注册很多次事件处理程序来说，.live()只注册一次事件处理程序
- 从.bind()更新到.live()的方法对程序更改很少，只需要替换“bind”为”live”
- 对于动态添加的属于匹配到的元素，也能够“神奇”的执行处理程序
- 在document元素没有全部加载完之前都能够几乎不花时间地绑定并触发事件

**缺点**

- 此方法在jQuery1.7的时候已经废除，你应该逐步从你的代码中替换掉该方法
- 链接不能够正常的支持这个方法
- 这个方法被抛弃是因为它只能够绑定事件处理程序到document上
- event.stopPropagation()不再有效了，因为事件已经委托到了document上了
- 由于所有的选择器和事件信息都是附加到了document上的，所以一个确定的事件要触发，必须通过大量的存储信息来匹配到
- 由于事件都是委托到了document上的，所以如果DOM太深的话，会影响到性能的

**.delegate()**

.delegate()方法的行为有点类似.live()。但是不是把选择器和事件的信息附加到了document上，而是可以自行选择它要附加的DOM元素，这个技术可以让事件的委托正常工作。 如果你跳过了.live()的介绍和分析，请先跳回去读一下，接着我才能向你表述清楚下面的逻辑

```
/*.delegate()的处理方法类似.live()，但是不是将事件处理程序附加到了document上，而是可以选择它在哪里（"#members"）。选择器和事件信息（"li a" 和 "click"）将会附加到“#members”元素上。 */  
$( "#members" ).delegate( "li a", "click", function( e ) {} ); 
```
.delegate()方法是非常强大的。上面的代码会将事件处理程序以及选择器和事件信息附加到”#members”上。这个当然要比.live()将这些内容附加到document上有效的多了。另外有很多其他的一年问题也通过.delegate()这个方法解决了。请参阅下列大纲的详细列表。

**优点**

- 可以自由选择附加的选择器和事件信息的位置
- 链接也可以有效的支持了
- jQuery仍然需要循环访问选择器和事件数据来确定匹配，但是因为能够选择这些信息附加的位置，所以通过匹配的量小很多了
- 由于这种技术使用了事件委托，所以它能很好的动态处理添加到DOM元素
- 如果你委托事件到了document上，你也可以在document全部准备完之前绑定和调用

**缺点**

- 方法从.bind()更改到.delegate()比较麻烦
- 如果把选择器和事件数据附加到了document上，仍然需要很多的匹配信息，但是相对于.live()的存储量要小很多了

你知道jQuery中的.bind() .live 和 .delegate()方法都是通过同一个新方法实现的–.on() （在jQuery1.7后），下面的代码片段来自jQuery 1.7.1 codebase in GitHub…
```
Code example:  
  
// ... more code ...  
   
bind: function( types, data, fn ) {  
return this.on( types, null, data, fn );  
},  
unbind: function( types, fn ) {  
return this.off( types, null, fn );  
},  
   
live: function( types, data, fn ) {  
jQuery( this.context ).on( types, this.selector, data, fn );  
return this;  
},  
die: function( types, fn ) {  
jQuery( this.context ).off( types, this.selector || "**", fn );  
return this;  
},  
   
delegate: function( selector, types, data, fn ) {  
return this.on( types, selector, data, fn );  
},  
undelegate: function( selector, types, fn ) {  
return arguments.length == 1 ?  
this.off( selector, "**" ) :  
this.off( types, selector, fn );  
},  
   
// ... more code ...  
```

这就意味着这个新方法的用法可以像下面这样

```
/* The jQuery .bind(), .live(), and .delegate() methods are just one 
line pass throughs to the new jQuery 1.7 .on() method */  
   
// Bind  
$( "#members li a" ).on( "click", function( e ) {} );  
$( "#members li a" ).bind( "click", function( e ) {} );  
   
// Live  
$( document ).on( "click", "#members li a", function( e ) {} );  
$( "#members li a" ).live( "click", function( e ) {} );  
   
// Delegate  
$( "#members" ).on( "click", "li a", function( e ) {} );  
$( "#members" ).delegate( "li a", "click", function( e ) {} ); 
```


你会注意到，具体取决于我如何调用.on()方法来更改它的执行过程。你可以考虑“重载”.on()方法来具有不同的效果。这个方法给API带来了很多的一致性，并希望减少那些方法的混淆。
优点

为各种事件绑定方法带来了统一性
简化了jQuery代码库，并删除一个界别的重定向，因为通过调用这个方法实现了 .bind() .live() 和 .delegate()
仍然提供了好用的.delegate()方法，但是也仍然对.bind()方法提供了支持
缺点

因为调用这个方法的各个形式，会带来一些混乱

**总结**

如果你已经对各种类型的事件绑定方法混淆的神志不清的话也别担心，这是因为历史遗留问题和API在随着时间的推移导致的。有些人认为这些方法作为魔法方法，但是一旦你发现他们如何工作的将会更好的利于你的项目。

从这篇文章中应该记住的要点：
- 使用.bind()方法是很浪费资源的，因为它要匹配选择器中的每一项并且挨个设置相同的事件处理程序
- 建议停止使用.live()方法，因为它已经被弃用了，由于他有很多的问题
- .delegate()方法“很划算”用来处理性能和响应动态添加元素的时候
- 新的.on()方法主要是可以实现.bind() .live() 甚至 .delegate()的功能
- 建议使用.on()方法，如果你的项目使用了1.7+的jQuery的话

## document.ready和document.load和$(function(){})有什么区别？

1.执行时间 

   window.onload必须等到页面内包括图片的所有元素加载完毕后才能执行。 
   $(document).ready()是DOM结构绘制完毕后就执行，不必等到加载完毕。 
   
2.编写个数不同 

   window.onload不能同时编写多个，如果有多个window.onload方法，只会执行一个 
   $(document).ready()可以同时编写多个，并且都可以得到执行

3.简化写法 

   window.onload没有简化写法 
   $(document).ready(function(){})可以简写成$(function(){});

## $.data()和$('#aaa').data()各自作用是什么？有什么区别


# ES6

## 1.什么时候应该用箭头函数？什么时候不能用？ － 请写出ES6中Array.isArray()的实现代码

https://zhuanlan.zhihu.com/p/26540168

## 2.如何在项目中解析处理es6和es7代码

首先安装必要的`Babel`模块：`npm install --save-dev babel-preset-stage-0`

然后在`.babelrc`文件中添加这个preset的配置：
```
{
    "presets": ["es2015", "react", "stage-0"]
}
```

## 3.Promise常用方法，Promise.race的作用，then方法里reject和catch的区别

- 方法：Promise.all实现并行,Promise.race实现选择,Promise.then

- Promise.race实现选择
接受一个数组，数组内都是Promise实例,返回一个Promise实例，这个Promise实例的状态转移取决于参数的Promise实例的状态变化。当参数中任何一个实例处于resolve状态时，返回的Promise实例会变为resolve状态。如果参数中任意一个实例处于reject状态，返回的Promise实例变为reject状态。
```
const fs = require('fs');
let p1 =  new Promise((resolve,reject)=>{
    fs.readFile('./name.txt','utf8',function (err,data) {
        resolve(data);
    });
})
let p2 = new Promise((resolve,reject)=>{
    fs.readFile('./age.txt','utf8',function (err,data) {
        resolve(data);
    });
})
Promise.race([p1,p2]).then(([res1,res2])=>{
    console.log(res1,res2);
})
```

- 区别：

catch 当一个 promise 被拒绝(reject)时,catch 方法会被执行,通常我们在 reject 方法里处理执行失败的结果，而在catch 里执行异常结果

# 工程化

## 1.什么叫模块化？你用过哪些模块化解决方案？

- 模块化是一种将系统分离成独立功能部分的方法，可将系统分割成独立的功能部分，严格定义模块接口、模块间具有透明性。

- NodeJS，Vue.js,webpack


## 2.什么叫组件化？你在工作中是如何实现组件化的？

- 组件化：将一个页面分割成若干部分，一个页面js+css+html，将自己的内容分割出来，方便我们开发，更好的维护我们的代码，每个组件封装自己的js+css+html，避免了样式命名冲突。

## 3.gulp和webpack的相同点和不同点?

**gulp**

gulp强调的是前端开发的工作流程，我们可以通过配置一系列的task，定义task处理的事务（例如文件压缩合并、雪碧图、启动server、版本控制等），然后定义执行顺序，来让gulp执行这些task，从而构建项目的整个前端开发流程。

PS：简单说就一个Task Runner

**webpack**

webpack是一个前端模块化方案，更侧重模块打包，我们可以把开发中的所有资源（图片、js文件、css文件等）都看成模块，通过loader（加载器）和plugins（插件）对资源进行处理，打包成符合生产环境部署的前端资源。

PS：webpack is a module bundle

相同功能

gulp与webpack可以实现一些相同功能，如下（列举部分）：

**文件合并与压缩（css）**

- gulp

 使用gulp-minify-css模块
 
```
gulp.task('sass',function(){
     gulp.src(cssFiles)
     .pipe(sass().on('error',sass.logError))
     .pipe(require('gulp-minify-css')())
     .pipe(gulp.dest(distFolder));
});
```

- webpack

样式合并一般用到extract-text-webpack-plugin插件，
压缩则使用webpack.optimize.UglifyJsPlugin。

**文件合并与压缩（js）**

- gulp

使用gulp-uglify和gulp-concat两个模块

- webpack

js合并在模块化开始就已经做，
压缩则使用webpack.optimize.UglifyJsPlugin

**sass/less预编译**

- gulp

使用gulp-sass/gulp-less 模块

- webpack

sass-loader/less-loader 进行预处理

**启动server**

- gulp

使用gulp-webserver模块

```
var webserver =require('gulp-webserver');
gulp.task('webserver',function(){
     gulp.src('./')
     .pipe(webserver({
          host:'localhost',
          port:8080,
          livereload:true, //自动刷新
          directoryListing:{
               enable: true,
               path:'./'
          },
     }));
});
```

- webpack

使用webpack-dev-server模块

```
module.exports = {
     ......
     devServer: {
          contentBase: "build/",
          port:8080,
          inline: true //实时刷新
     }
}
```

**版本控制**

- gulp

使用gulp-rev和gulp-rev-collector两个模块

- webpack

将生成文件加上hash值
```
module.exports = {
     ......
    output: {
        ......
        filename: "[name].[hash:8].js"
    },
     plugins:[
          ......
          new ExtractTextPlugin(style.[hash].css")
     ]
}
```


**两者区别**
虽然都是前端自动化构建工具，但看他们的定位就知道不是对等的。

gulp严格上讲，模块化不是他强调的东西，他旨在规范前端开发流程。

webpack更是明显强调模块化开发，而那些文件压缩合并、预处理等功能，不过是他附带的功能。


## 4.什么是热加载?

热加载的思想是运行时动态注入修改后的文件内容，同时不中断 APP 的正常运行。这样，我们就不会丢失 APP 的任何状态信息，尤其是 UI 页面栈相关的。热加载基本上看不出刷新的效果，类似于局部刷新。
热加载的基础是模块热替换（HMR，Hot Module Replacement[3]），HMR 最开始是由 Webpack 引入的，我们在 React Native Packager 中也实现了这个功能。HMR 使得 Packager 可以监控文件的改动并发送 HMR 更新消息（HMR update）给包含在 APP 中的一层很薄的 HMR 运行时（HMR runtime）。


# 框架

## 1.前端路由的实现原理


## 2.MVVM框架解决了什么问题？带来了什么问题？

## 3.浏览器地址栏里面的'＃' 如何清楚？mode共有几个参数，参数有什么区别？

## 4.vue中父组件如何给子组件传递值

## 5.react的优缺点
**优点**
- React伟大之处就在于，提出了Virtual Dom这种新颖的思路，并且这种思路衍生出了React Native，有可能会统一Web/Native开发。在性能方面，由于运用了Virtual Dom技术，Reactjs只在调用setState的时候会更新dom，而且还是先更新Virtual Dom，然后和实际Dom比较，最后再更新实际Dom。这个过程比起Angularjs的bind方式来说，一是更新dom的次数少，二是更新dom的内容少，速度肯定快，
- ReactJS更关注UI的组件化，和数据的单向更新，提出了FLUX架构的新概念，现在React可以直接用Js ES6语法了，然后通过webpack编译成浏览器兼容的ES5，开发效率上有些优势. 
- React Native生成的App不是运行在WebView上，而是系统原生的UI，React通过jsx生成系统原生的UI，iOS和Android的React UI组件还是比较相似的，大量代码可以复用
- 维护UI的状态,Angular 里面使用的是 $scope，在 React 里面使用的是 this.setState。 而 React 的好处在于，它更简单直观。所有的状态改变都只有唯一一个入口 this.setState()，Angular 就比较复杂，不知道背后使用了哪些黑魔法。
- 同构的JavaScript 
- 单页面JS应用程序的最大缺陷在于对搜索引擎的索引有很大限制。React对此有了解决方案。 
- React可以在服务器上预渲染应用再发送到客户端。它可以从预渲染的静态内容中恢复一样的记录到动态应用程序中。 
- 因为搜索引擎的爬虫程序依赖的是服务端响应而不是JavaScript的执行，预渲染你的应用有助于搜索引擎优化。

## 6.React组件中props和state有什么区别？

## 7.什么是JSX

JSX就是Javascript和XML结合的一种格式


## 8.说一下angular、vue、react的相同点和不同点?各适用于什么样的项目场景?

## 9.React中不同组件传递数据的方式有哪些？至少说出三种

## 10.请描述React的组件加载生命周期函数以及shouldComponentUpdate方法的实际使用场景?


# HTTP

## 1.HTTP报文的组成部分

HTTP报文分为请求报文(request message)与响应报文(response message)。

一个HTTP报文由3部分组成，分别是:

　　(1)、起始行(start line)

　　(2)、首部(header)

　　(3)、主体(body)

## 2.GET和POST的区别

1.传输数据大小限制
   * GET以查询字符串的形式拼接到URL问号后边，？=mime类型&rvs_spt=1
   * URL是有长度限制的俄，chrome 8kb，ie 2bk
   * POST将发送给后台的数据放到请求体里面，没有大小限制
   
2.安全问题 MD5加密
   * GET 不安全，拼接到URL后边 容易被劫持
   * POST 在请求体里
   
3.缓存问题
   * get有缓存  在？后拼接随机数或时间戳
   https://www.baidu.com/_=Math.random
   https://www.baidu.com/_=Data.now
   * post是没有缓存的

## 3.HTTP常见状态码

HTTP状态码的英文为HTTP Status Code。

**下面是常见的HTTP状态码：**

- 200 - 请求成功
- 301 - 资源（网页等）被永久转移到其它URL
- 404 - 请求的资源（网页等）不存在
- 500 - 内部服务器错误

**HTTP状态码分类**

1**	信息，服务器收到请求，需要请求者继续执行操作
2**	成功，操作被成功接收并处理
3**	重定向，需要进一步的操作以完成请求
4**	客户端错误，请求包含语法错误或无法完成请求
5**	服务器错误，服务器在处理请求的过程中发生了错误

**HTTP状态码列表**

- 100	Continue	继续。客户端应继续其请求
- 101	Switching Protocols	切换协议。服务器根据客户端的请求切换协议。只能切换到更高级的协议，例如，切换到HTTP的新版本协议
- 200	OK	请求成功。一般用于GET与POST请求
- 201	Created	已创建。成功请求并创建了新的资源
- 202	Accepted	已接受。已经接受请求，但未处理完成
- 203	Non-Authoritative Information	非授权信息。请求成功。但返回的meta信息不在原始的服务器，而是一个副本
- 204	No Content	无内容。服务器成功处理，但未返回内容。在未更新网页的情况下，可确保浏览器继续显示当前文档
- 205	Reset Content	重置内容。服务器处理成功，用户终端（例如：浏览器）应重置文档视图。可通过此返回码清除浏览器的表单域
- 206	Partial Content	部分内容。服务器成功处理了部分GET请求
- 300	Multiple Choices	多种选择。请求的资源可包括多个位置，相应可返回一个资源特征与地址的列表用于用户终端（例如：浏览器）选择
- 301	Moved Permanently	永久移动。请求的资源已被永久的移动到新URI，返回信息会包括新的URI，浏览器会自动定向到新URI。今后任何新的请求都应使用新的URI代替
- 302	Found	临时移动。与301类似。但资源只是临时被移动。客户端应继续使用原有URI
- 303	See Other	查看其它地址。与301类似。使用GET和POST请求查看
- 304	Not Modified	未修改。所请求的资源未修改，服务器返回此状态码时，不会返回任何资源。客户端通常会缓存访问过的资源，通过提供一个头信息指出客户端希望只返回在指定日期之后修改的资源
- 305	Use Proxy	使用代理。所请求的资源必须通过代理访问
- 306	Unused	已经被废弃的HTTP状态码
- 307	Temporary Redirect	临时重定向。与302类似。使用GET请求重定向
- 400	Bad Request	客户端请求的语法错误，服务器无法理解
- 401	Unauthorized	请求要求用户的身份认证
- 402	Payment Required	保留，将来使用
- 403	Forbidden	服务器理解请求客户端的请求，但是拒绝执行此请求
- 404	Not Found	服务器无法根据客户端的请求找到资源（网页）。通过此代码，网站设计人员可设置"您所请求的资源无法找到"的个性页面
- 405	Method Not Allowed	客户端请求中的方法被禁止
- 406	Not Acceptable	服务器无法根据客户端请求的内容特性完成请求
- 407	Proxy Authentication Required	请求要求代理的身份认证，与401类似，但请求者应当使用代理进行授权
- 408	Request Time-out	服务器等待客户端发送的请求时间过长，超时
- 409	Conflict	服务器完成客户端的PUT请求是可能返回此代码，服务器处理请求时发生了冲突
- 410	Gone	客户端请求的资源已经不存在。410不同于404，如果资源以前有现在被永久删除了可使用410代码，网站设计人员可通过301代码指定资源的新位置
- 411	Length Required	服务器无法处理客户端发送的不带Content-Length的请求信息
- 412	Precondition Failed	客户端请求信息的先决条件错误
- 413	Request Entity Too Large	由于请求的实体过大，服务器无法处理，因此拒绝请求。为防止客户端的连续请求，服务器可能会关闭连接。如果只是服务器暂时无法处理，则会包含一个Retry-After的响应信息
- 414	Request-URI Too Large	请求的URI过长（URI通常为网址），服务器无法处理
- 415	Unsupported Media Type	服务器无法处理请求附带的媒体格式
- 416	Requested range not satisfiable	客户端请求的范围无效
- 417	Expectation Failed	服务器无法满足Expect的请求头信息
- 500	Internal Server Error	服务器内部错误，无法完成请求
- 501	Not Implemented	服务器不支持请求的功能，无法完成请求
- 502	Bad Gateway	充当网关或代理的服务器，从远端服务器接收到了一个无效的请求
- 503	Service Unavailable	由于超载或系统维护，服务器暂时的无法处理客户端的请求。延时的长度可包含在服务器的Retry-After头信息中
- 504	Gateway Time-out	充当网关或代理的服务器，未及时从远端服务器获取请求
- 505	HTTP Version not supported	服务器不支持请求的HTTP协议的版本，无法完成处理



## 4.什么是Restful API?


## 5.HTTPS和HTTP的区别是什么?

HTTP协议通常承载于TCP协议之上，在HTTP和TCP之间添加一个安全协议层（SSL或TSL），这个时候，就成了我们常说的HTTPS。

默认HTTP的端口号为80，HTTPS的端口号为443。



## 6.从在浏览器中输入URL到页面渲染出来都经过了什么过程？

**分为4个步骤：**

（1），当发送一个URL请求时，不管这个URL是Web页面的URL还是Web页面上每个资源的URL，浏览器都会开启一个线程来处理这个请求，同时在远程DNS服务器上启动一个DNS查询。这能使浏览器获得请求对应的IP地址。

（2）， 浏览器与远程`Web`服务器通过`TCP`三次握手协商来建立一个`TCP/IP`连接。该握手包括一个同步报文，一个同步-应答报文和一个应答报文，这三个报文在 浏览器和服务器之间传递。该握手首先由客户端尝试建立起通信，而后服务器应答并接受客户端的请求，最后由客户端发出该请求已经被接受的报文。

（3），一旦`TCP/IP`连接建立，浏览器会通过该连接向远程服务器发送`HTTP`的`GET`请求。远程服务器找到资源并使用HTTP响应返回该资源，值为200的HTTP响应状态表示一个正确的响应。

（4），此时，`Web`服务器提供资源服务，客户端开始下载资源。

请求返回后，便进入了我们关注的前端模块

简单来说，浏览器会解析`HTML`生成`DOM Tree`，其次会根据CSS生成CSS Rule Tree，而`javascript`又可以根据`DOM API`操作`DOM`


## 7.JSON和JSONP 区别是什么？JSONP的原理是？

json返回的是一串数据；而jsonp返回的是脚本代码（包含一个函数调用），JSONP就是用来解决跨域请求问题的。

ajax请求受同源策略影响，不允许进行跨域请求，而script标签src属性中的链接却可以访问跨域的js脚本，利用这个特性，服务端不再返回JSON格式的数据，而是返回一段调用某个函数的js代码，在src中进行了调用，这样实现了跨域。

参考网址：http://www.qdfuns.com/notes/16738/1b6ad6125747d28592a53a960b44c6f4.html


## 8.用过哪些跨域技术

- window.postMessage
- window.name
- JSONP
- Server-Proxy
- document.domain
- FIM
- Flash

## 9.ajax的参数

```


$.ajax({  
  
        type: 'GET',    // 这是请求的方式 可以是GET方式也可以是POST方式, 默认是GET  
  
        url: ' xxx.php ',   // 这是请求的连接地址 一般情况下这个地址是后台给前端的一个连接，直接写就可以  
  
        dataType: 'json',  // 这是后台返回的数据类型 一般情况下都是一个json数据， 前端遍历一下就OK  
  
        async: true, // 默认为true，默认为true时，所有请求均为异步请求，如果需要发送同步请求，需设置为false,  
  
        timeout: 8000, // 设置请求超时时间（毫秒）。此设置将覆盖全局设置  
  
        data: {  
                // 要传递的参数  
  
                'xxx' : 'xxx',  
                  
                ... ...   
        },  
  
        beforeSend: function () {  
  
                // 在发送请求前就开始执行 （一般用来显示loading图）  
  
        }，  
  
        success: function (data) {  
  
                // 发送请求成功后开始执行，data是请求成功后，返回的数据  
  
        },  
  
        complete: function () {  
  
                //当请求完成后开始执行，无论成功或是失败都会执行 （一般用来隐藏loading图）  
          
        }，  
  
        error: function (xhr, textStatus, errorThrown) {  
  
                //  请求失败后就开始执行，请求超时后，在这里执行请求超时后要执行的函数  
  
        }  
}).done(function () {  
          
        // 这个函数是在ajax数据加载完之后，对数据进行的判断，在涉及到对ajax数据进行操作无效时，在这个函数里面写是可以起到效果的  
  
}) 
```

# 前后端通信

## 1.什么是同源策略及限制?

概念:同源策略是客户端脚本（尤其是Javascript）的重要的安全度量标准。它最早出自Netscape Navigator2.0，其目的是防止某个文档或脚本从多个不同源装载。

这里的同源策略指的是：协议，域名，端口相同，同源策略是一种安全协议。

指一段脚本只能读取来自同一来源的窗口和文档的属性。

**为什么要有同源限制？**

我们举例说明：比如一个黑客程序，他利用Iframe把真正的银行登录页面嵌到他的页面上，当你使用真实的用户名，密码登录时，他的页面就可以通过Javascript读取到你的表单中input中的内容，这样用户名，密码就轻松到手了。

缺点：

现在网站的JS 都会进行压缩，一些文件用了严格模式，而另一些没有。这时这些本来是严格模式的文件，被 merge 后，这个串就到了文件的中间，不仅没有指示严格模式，反而在压缩后浪费了字节。

## 2.前后端如何通信?







## 3.用原生JS模拟一下jquery的ajax方法

```
/* 封装ajax函数
 * @param {string}opt.type http连接的方式，包括POST和GET两种方式
 * @param {string}opt.url 发送请求的url
 * @param {boolean}opt.async 是否为异步请求，true为异步的，false为同步的
 * @param {object}opt.data 发送的参数，格式为对象类型
 * @param {function}opt.success ajax发送并接收成功调用的回调函数
 */
    function ajax(opt) {
        opt = opt || {};
        opt.method = opt.method.toUpperCase() || 'POST';
        opt.url = opt.url || '';
        opt.async = opt.async || true;
        opt.data = opt.data || null;
        opt.success = opt.success || function () {};
        var xmlHttp = null;
        if (XMLHttpRequest) {
            xmlHttp = new XMLHttpRequest();
        }
        else {
            xmlHttp = new ActiveXObject('Microsoft.XMLHTTP');
        }var params = [];
        for (var key in opt.data){
            params.push(key + '=' + opt.data[key]);
        }
        var postData = params.join('&');
        if (opt.method.toUpperCase() === 'POST') {
            xmlHttp.open(opt.method, opt.url, opt.async);
            xmlHttp.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded;charset=utf-8');
            xmlHttp.send(postData);
        }
        else if (opt.method.toUpperCase() === 'GET') {
            xmlHttp.open(opt.method, opt.url + '?' + postData, opt.async);
            xmlHttp.send(null);
        } 
        xmlHttp.onreadystatechange = function () {
            if (xmlHttp.readyState == 4 && xmlHttp.status == 200) {
                opt.success(xmlHttp.responseText);
            }
        };
    }
```

使用实例

```
ajax({
    method: 'POST',
    url: 'test.php',
    data: {
        name1: 'value1',
        name2: 'value2'
    },
    success: function (response) {
       console.log(response)；
    }
});
```

## 4.跨域通信的几种方式?

1. 利用jsonp 方式

最常见的一种跨域方式，其背后原理就是利用了script标签不受同源策略的限制，在页面中动态插入了script，script标签的src属性就是后端api接口的地址，并且以get的方式将前端回调处理函数名称告诉后端，后端在响应请求时会将回调返还，并且将数据以参数的形式传递回去。

前端
```
//http://127.0.0.1:8888/jsonp.html
var script = document.createElement('script');
      script.src = 'http://127.0.0.1:2333/jsonpHandler?callback=_callback'
      document.body.appendChild(script);      //插入script标签
      //回调处理函数 _callback
      var _callback = function(obj){
          for(key in obj){
            console.log('key: ' + key +' value: ' + obj[key]);
          }
      }
```
后端:
```
//http://127.0.0.1:2333/jsonpHandler
app.get('/jsonpHandler', (req,res) => {
  let callback = req.query.callback;
  let obj = {
    type : 'jsonp',
    name : 'weapon-x'
  };
  res.writeHead(200, {"Content-Type": "text/javascript"});
  res.end(callback + '(' + JSON.stringify(obj) + ')');
})
```
在jsonp.html中打开控制台可以看到返回数据的输出:

2. CORS (XMLHttpRequest level 2)

3. postmessage跨域

在HTML5中新增了postMessage方法，postMessage可以实现跨文档消息传输（Cross Document Messaging），Internet Explorer 8, Firefox 3, Opera 9, Chrome 3和 Safari 4都支持postMessage。
该方法可以通过绑定window的message事件来监听发送跨文档消息传输内容。
使用postMessage实现跨域的话原理就类似于jsonp，动态插入iframe标签，再从iframe里面拿回数据
，私认为用作跨页面通信更加适合

4. 服务器跨域

在前后端分离的项目中可以借助服务器实现跨域，具体做法是：前端向本地服务器发送请求，本地服务器代替前端再向api服务器接口发送请求进行服务器间通信，本地服务器其实就是个中转站的角色，再将响应的数据返回给前端，下面用node.js做一个示例

前端:
```
//http://127.0.0.1:8888/server
var xhr = new XMLHttpRequest();
    xhr.onload = function(data){
      var _data = JSON.parse(data.target.responseText)
      for(key in _data){
        console.log('key: ' + key +' value: ' + _data[key]);
      }
    };
    xhr.open('POST','http://127.0.0.1:8888/feXhr',true);  //向本地服务器发送请求   
    xhr.setRequestHeader('Content-Type','application/x-www-form-urlencoded');
    xhr.send("url=http://127.0.0.1:2333/beXhr");    //以参数形式告知需要请求的后端接口
```
后端:
```
//http://127.0.0.1:8888/feXhr
app.post('/feXhr',(req,res) => {
  let url  = req.body.url;
  superagent.get(url)           //使用superagent想api接口发送请求
      .end(function (err,docs) {
          if(err){
              console.log(err);
              return
          }
          res.end(docs.res.text); //返回到前端
      })
})

//http://127.0.0.1:2333/beXhr
app.get('/beXhr',(req,res) => {
  let obj = {
    type : 'superagent',
    name : 'weapon-x'
  };
  res.writeHead(200, {"Content-Type": "text/javascript"});
  res.end(JSON.stringify(obj));     //响应
})
```
回到 http://127.0.0.1:8888/server 页面打开控制台可以看到数据输出：



# 安全

## 1.CSRF的原理以及如何防御

CSRF（Cross-Site Request Forgeries，跨站点请求伪造）：指攻击者通过设置好的陷阱，强制对已完成的认证用户进行非预期的个人信息或设定信息等某些状态更新。

**CSRF防御**

- 通过 referer、token 或者 验证码 来检测用户提交。
- 尽量不要在页面的链接中暴露用户隐私信息。
- 对于用户修改删除等操作最好都使用post 操作 。
- 避免全站通用的cookie，严格设置cookie的域。


## 2.XSS的原生和如何防御

XSS（Cross-Site Scripting，跨站脚本攻击）：指通过存在安全漏洞的Web网站注册用户的浏览器内运行非法的HTML标签或者JavaScript进行的一种攻击。

**XSS防范方法**
首先代码里对用户输入的地方和变量都需要仔细检查长度和对”<”,”>”,”;”,”’”等字符做过滤；其次任何内容写到页面之前都必须加以encode，避免不小心把html tag 弄出来。这一个层面做好，至少可以堵住超过一半的XSS 攻击。

首先，避免直接在cookie 中泄露用户隐私，例如email、密码等等。

其次，通过使cookie 和系统ip 绑定来降低cookie 泄露后的危险。这样攻击者得到的cookie 没有实际价值，不可能拿来重放。

如果网站不需要再浏览器端对cookie 进行操作，可以在Set-Cookie 末尾加上HttpOnly 来防止javascript 代码直接获取cookie 。

尽量采用POST 而非GET 提交表单

# 渲染机制

## 1.什么是DOCTYPE及作用?标准模式和兼容模式有什么区别?

- <!DOCTYPE> 声明位于文档中的最前面，处于 <html> 标签之前。告知浏览器以何种模式来渲染文档。

- 严格模式的排版和 JS 运作模式是以该浏览器支持的最高标准运行。在混杂模式中，页面以宽松的向后兼容的方式显示。模拟老式浏览器的行为以防止站点无法工作。


## 2.浏览器是如何渲染页面的?

1.解析HTML文件，创建DOM树
自上而下，遇到任何样式（link、style）与脚本（script）都会阻塞（外部样式不阻塞后续外部脚本的加载）。
2.解析CSS
优先级：浏览器默认设置<用户设置<外部样式<内联样式<HTML中的style样式；
特定级：id数*100+类或伪类数*10+tag名称*1
3.将CSS与DOM合并，构建渲染树（renderingtree）
DOM树与HTML一一对应，渲染树会忽略诸如head、display:none的元素
4.布局和绘制，重绘（repaint）和重排（reflow）
重排：若渲染树的一部分更新，且尺寸变化，就会发生重排；
重绘：部分节点需要更新，但不改变其他集合形状。如改变某个元素的颜色，就会发生重绘。

## 3.什么是重排？什么时候会触发重排?

**重排**当DOM的变化影响了元素的几何属性（宽或高），浏览器需要重新计算元素的几何属性，同样其他元素的几何属性和位置也会因此受到影响。浏览器会使渲染树中受到影响的部分失效，并重新构造渲染树。这个过程称为重排。

重排一定会引起浏览器的重绘，一个元素的重排通常会带来一系列的反 应，甚至触发整个文档的重排和重绘，性能代价是高昂的。

**何时重排**
1、添加或者删除可见的DOM元素
2、元素位置改变
3、元素尺寸改变
4、元素内容改变（例如：一个文本被另一个不同尺寸的图片替代）
5、页面渲染初始化（这个无法避免）
6、浏览器窗口尺寸改变

## 4.什么是重绘？什么时候会触发重绘?

完成重排后，浏览器会重新绘制受影响的部分到屏幕，该过程称为重绘。

# JS运行机制

## 1.如何理解JS的单线程
JavaScript语言的一大特点就是单线程，也就是说，同一个时间只能做一件事。
JavaScript的单线程，与它的用途有关。作为浏览器脚本语言，JavaScript的主要用途是与用户互动，以及操作DOM。这决定了它只能是单线程，否则会带来很复杂的同步问题。比如，假定JavaScript同时有两个线程，一个线程在某个DOM节点上添加内容，另一个线程删除了这个节点，这时浏览器应该以哪个线程为准？


## 2.什么是Event Loop,请简述其过程

Event Loop 指的是计算机系统的一种运行机制。JavaScript语言就采用这种机制，来解决单线程运行带来的一些问题。
主线程从"任务队列"中读取事件，这个过程是循环不断的，所以整个的这种运行机制又称为Event Loop（事件循环）。
主线程运行的时候，产生堆（heap）和栈（stack），栈中的代码调用各种外部API，它们在"任务队列"中加入各种事件（click，load，done）。只要栈中的代码执行完毕，主线程就会去读取"任务队列"，依次执行那些事件所对应的回调函数。

# 服务器

## 1.如何在web应用中在实现权限控制?

- 前端控制：
　　前端的控制比较简单，从后台获取到用户的权限之后，可以存在session或者cookie中，然后在页面加载的时候，通过session或者cookie中存的权限来选择让该功能展现或者禁用。

- 后台控制：
　　仅仅依靠前端的控制是无法完美解决权限控制的问题，因为前端页面的加载过程是在浏览器中完成的，用户可以自行篡改页面；或者用户可以直接通过URI请求来获取非法权限功能。所以需要在后台实现权限控制。

　　后台的控制方法也很多，比如filter、spring的AOP等。在此选用springMVC的interceptor来控制。

　　首先，在appContext-mvc.xml配置文件中配置拦截器，如下所示：
  ```
  <mvc:interceptors>
    <!-- 会员功能 -->
    <mvc:interceptor>  
        <mvc:mapping path="/fund/mem/**" />
        <bean class="org.fund.user.interceptor.AuthInterceptor" />  
    </mvc:interceptor>
</mvc:interceptors>  
```
其中，path表示需要控制的接口路径，可以使用正则表达式来匹配。

　　然后，需要自己定义一个拦截器类，继承HandlerInterceptor接口，然后在preHandle方法里进行权限判断，如下所示：
  ```
  @Override
public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
    User user = UserHolder.getUser();
    if (user.getAuth() == GameIdeaType.VIP_USER.getId()) {
        return true;
    } else {
        return false;
    }
}
```
此时，当用户访问接口时，会首先进入这个拦截器的preHandle方法去处理。若权限通过则返回true；否则返回false，此次访问结束。

到此，已经实现了权限的控制，但是无法在用户访问非法权限接口时给出提示。若要解决这个问题，需要添加一个全局异常管理。

- 全局异常管理：

　　思路是在拦截器中权限校验失败时，抛出一个权限校验失败的异常，然后通过全局异常管理类来捕获并返回前端特定的格式。具体如下。

首先，在配置文件中添加全局异常管理类，如下：

```
<!-- 全局异常管理 -->
<bean id="handlerExceptionResolver" class="org.fund.common.ExceptionHandler">
    <property name="order" value="0"></property>
</bean>
```
然后，定义异常管理类，实现SimpleMappingExceptionResolver接口。
```
/**
 * 全局异常处理类
 * 
 * @author 
 */
public class ExceptionHandler extends SimpleMappingExceptionResolver {

    @Override
    public ModelAndView resolveException(HttpServletRequest request, HttpServletResponse response, Object o, Exception e) {
        logger.info("System Error Occurred. " + e.getMessage(), e);

        ModelAndView model = new ModelAndView(new MappingJacksonJsonView());
        List<String> errors = new ArrayList<String>();

        if (e instanceof NoPermissionException) {
            errors.add("抱歉，该功能开通会员之后才能使用！");
        } else {
            errors.add("系统异常");
        }

        return paramError(model, errors);
    }

    private ModelAndView paramError(ModelAndView mv, List<String> errors) {
        mv.addObject("success", false);
        mv.addObject("data", null);
        mv.addObject("errors", errors);
        return mv;
    }

}
```
最后，修改拦截器的实现
```
@Override
public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
    User user = UserHolder.getUser();
    if (user.getAuth() == GameIdeaType.VIP_USER.getId()) {
        return true;
    } else {
        throw new NoPermissionException();
    }
}
```



## 2.Web服务器、应用服务器、Web容器、反向代理服务器的区别和联系?

Web服务器是指能够为发出请求的浏览器提供文档的程序。服务器是一种被动程序，只有浏览器发出请求的时候才会响应。应用层使用的是HTTP协议。目前最主流的三个Web服务器是Apache Nginx IIS。

Web容器是一种服务器程序，在服务器端口就有一个提供相应服务的程序。所以现在知道为什么Tomcat有默认的端口——8080。一个服务器可以有多个容器。

Web服务器设计服务于HTTP内容，应用服务器不只限于HTTP。Web服务器服务于静态内容，有插件支持动态语言，
应用服务器也具有Web服务器的这些东西，除此它还支持程序级的服务，如连接池，事务支持，信息服务等。


# 错误处理

## 1.前端错误的分类?
## 2.程序出现bug了，你是如何调试的?
## 3.如何分类捕获不同的错误?
## 4.如何把生产环境的错误上报？

# 页面性能

## 1.前端性能优化的方法有哪些？至少说出10种以上

 雅虎35条军规

## 2.如何实现JS的异步加载? async和defer的区别是什么?

defer和async、动态创建DOM方式（创建script，插入到DOM中，加载完毕后callBack）、按需异步载入js

defer并行加载js文件，会按照页面上script标签的顺序执行 async并行加载js文件，下载完成立即执行，不会按照页面上script标签的顺序执行


# 缓存

## 1.Expires和Cache-Control是如何工作的？

对一个网站而言，CSS、JavaScript、图片等静态资源更新的频率都比较低，而这些文件又几乎是每次HTTP请求都需要的，如果将这些文件缓存在浏览器中，可以极好的改善性能。通过设置http头中的cache-control和expires的属性，可设定浏览器缓存，将静态内容设为永不过期，或者很长时间后才过期。

Expires = 时间，HTTP 1.0 版本，缓存的载止时间，允许客户端在这个时间之前不去检查（发请求）
max-age = 秒，HTTP 1.1版本，资源在本地缓存多少秒。
如果max-age和Expires同时存在，则被Cache-Control的max-age覆盖。
Expires 的一个缺点就是，返回的到期时间是服务器端的时间，这样存在一个问题，如果客户端的时间与服务器的时间相差很大，那么误差就很大，所以在HTTP 1.1版开始，使用Cache-Control: max-age=秒替代。
Expires =max-age +   “每次下载时的当前的request时间”

## 2.Last-Modified和Etag是如何工作的？

什么是”Last-Modified”?

   在浏览器第一次请求某一个URL时，服务器端的返回状态会是200，内容是你请求的资源，同时有一个Last-Modified的属性标记此文件在服务期端最后被修改的时间，格式类似这样：`Last-Modified: Fri, 12 May 2006 18:53:33 GMT`
   
　　客户端第二次请求此URL时，根据 HTTP 协议的规定，浏览器会向服务器传送 If-Modified-Since 报头，询问该时间之后文件是否有被修改过：`If-Modified-Since: Fri, 12 May 2006 18:53:33 GMT`
　　
   如果服务器端的资源没有变化，则自动返回 HTTP 304 （Not Changed.）状态码，内容为空，这样就节省了传输数据量。当服务器端代码发生改变或者重启服务器时，则重新发出资源，返回和第一次请求时类似。从而保证不向客户端重复发出资源，也保证当服务器有变化时，客户端能够得到最新的资源。

什么是”Etag”?

　　HTTP 协议规格说明定义ETag为“被请求变量的实体值” （参见 —— 章节 14.19）。 另一种说法是，ETag是一个可以与Web资源关联的记号（token）。典型的Web资源可以一个Web页，但也可能是JSON或XML文档。服务器单独负责判断记号是什么及其含义，并在HTTP响应头中将其传送到客户端，以下是服务器端返回的格式：`ETag: "50b1c1d4f775c61:df3"`
  
　　客户端的查询更新格式是这样的：`If-None-Match: W/"50b1c1d4f775c61:df3"`
  
　　如果ETag没改变，则返回状态304然后不返回，这也和Last-Modified一样。本人测试Etag主要在断点下载时比较有用。

**Last-Modified和Etags如何帮助提高性能?**

last-Modified 和ETags请求的http报头一起使用，服务器首先产生 Last-Modified/Etag标记，服务器可在稍后使用它来判断页面是否已经被修改，来决定文件是否继续缓存
过程如下:
1. 客户端请求一个页面（A）。
2. 服务器返回页面A，并在给A加上一个Last-Modified/ETag。
3. 客户端展现该页面，并将页面连同Last-Modified/ETag一起缓存。
4. 客户再次请求页面A，并将上次请求时服务器返回的Last-Modified/ETag一起传递给服务器。
5. 服务器检查该Last-Modified或ETag，并判断出该页面自上次客户端请求之后还未被修改，直接返回响应304和一个空的响应体。

## 3.请描述cookie、sessionStorage和localStorage的区别

相同点：都存储在客户端
不同点：
1.存储大小
cookie数据大小不能超过4k。
sessionStorage和localStorage 虽然也有存储大小的限制，但比cookie大得多，可以达到5M或更大。
2.有效时间
localStorage    存储持久数据，浏览器关闭后数据不丢失除非主动删除数据；
sessionStorage  数据在当前浏览器窗口关闭后自动删除。
cookie          设置的cookie过期时间之前一直有效，即使窗口或浏览器关闭
3. 数据与服务器之间的交互方式
cookie的数据会自动的传递到服务器，服务器端也可以写cookie到客户端
sessionStorage和localStorage不会自动把数据发给服务器，仅在本地保存。

**设置Cookie** 

cookie的几个要素

cookie的内容：采用 key=value;key=value……存储，参数名自定义

cookie的过期时间：使用参数expires

cookie的路径：使用参数path，"/"表示这个网站的页面，不推荐!容易产生冲突

注意：形如“/pro/index.html”路径，在google浏览器正常，在IE浏览器得不到值 

cookie的表示方式示例
```
var name = "jack";  
var pwd = "123";  
var now = new Date();  
now.setTime(now.getTime() +1 * 24 * 60 * 60 * 1000);//转毫秒  
var path = "/";//可以是具体的网页  
document.cookie = "name=" + name + ";expires=" + now.toUTCString() + ";path=" + path;//姓名  
document.cookie= "pwd=" + pwd + ";expires=" + now.toUTCString()+ ";path=" + path; //密码
```
**读取cookie**

获取cookie内容
```
var data=document.cookie;//获取对应页面的cookie  
```

解析cookie
方式1：截取字符串
```
function getKey(key) {  
    var data = document.cookie;  
    var findStr = key + "=";  
    //找到key的位置  
    var index = data.indexOf(findStr);  
    if (index == -1)  
        return null;  
    var subStr = data.substring(index +findStr.length);  
    var lastIndex = subStr.indexOf(";");  
    if (lastIndex == -1) {  
        return subStr;  
 } else {  
        return subStr.substring(0,lastIndex);  
 }  
}  
```
方式2：使用正则表达式+JSON
```
function getKey(key) {  
    return JSON.parse("{\"" +document.cookie.replace(/;\s+/gim, "\",\"").replace(/=/gim, "\":\"") + "\"}")[key];  
}  
```

**清除cookie**
```

var name = null;  
var pwd = null;  
var now = new Date();  
var path = "/";//可以是具体的网页  
document.cookie= "name=" + name + ";expires=" + now.toUTCString()+ ";path=" + path;//姓名  
document.cookie = "pwd=" + pwd + ";expires=" + now.toUTCString()+ ";path=" + path; //密码  
```








