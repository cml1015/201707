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

- 渐进增强 progressive enhancement：针对低版本浏览器进行构建页面，保证最基本的功能，然后再针对高级浏览器进行效果、交互等改进和追加功能达到更好的用户体验。

- 优雅降级 graceful degradation：一开始就构建完整的功能，然后再针对低版本浏览器进行兼容。

- 区别：优雅降级是从复杂的现状开始，并试图减少用户体验的供给，而渐进增强则是从一个非常基础的，能够起作用的版本开始，并不断扩充，以适应未来环境的需要。降级（功能衰减）意味着往回看；而渐进增强则意味着朝前看，同时保证其根基处于安全地带

- “优雅降级”观点

　　“优雅降级”观点认为应该针对那些最高级、最完善的浏览器来设计网站。而将那些被认为“过时”或有功能缺失的浏览器下的测试工作安排在开发周期的最后阶段，并把测试对象限定为主流浏览器（如 IE、Mozilla 等）的前一个版本。

　　在这种设计范例下，旧版的浏览器被认为仅能提供“简陋却无妨 (poor, but passable)” 的浏览体验。你可以做一些小的调整来适应某个特定的浏览器。但由于它们并非我们所关注的焦点，因此除了修复较大的错误之外，其它的差异将被直接忽略。

- “渐进增强”观点

　　“渐进增强”观点则认为应关注于内容本身。

　　内容是我们建立网站的诱因。有的网站展示它，有的则收集它，有的寻求，有的操作，还有的网站甚至会包含以上的种种，但相同点是它们全都涉及到内容。这使得“渐进增强”成为一种更为合理的设计范例。这也是它立即被 Yahoo! 所采纳并用以构建其“分级式浏览器支持 (Graded Browser Support)”策略的原因所在。



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

 1.创建一个新对象；

 2.将构造函数的作用域赋给新对象（因此 this 就指向了这个新对象）；

 3.执行构造函数中的代码（为这个新对象添加属性） ；

 4.返回新对象。

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

# JQuery

## jquery.extend , jquery.fn.extend的区别

## 谈一下jquery中的bind，live，delegate，on区别

## document.ready和document.load和$(function(){})有什么区别？

## $.data()和$('#aaa').data()各自作用是什么？有什么区别


# ES6

## 1.什么时候应该用箭头函数？什么时候不能用？ － 请写出ES6中Array.isArray()的实现代码

## 2.如何在项目中解析处理es6和es7代码

## 3.Promise常用方法，Promise.race的作用，then方法里reject和catch的区别


# 工程化

## 1.什么叫模块化？你用过哪些模块化解决方案？

## 2.什么叫组件化？你在工作中是如何实现组件化的？

## 3.gulp和webpack的相同点和不同点?

## 4.什么是热加载?



# 框架

## 1.前端路由的实现原理

## 2.MVVM框架解决了什么问题？带来了什么问题？

## 3.浏览器地址栏里面的'＃' 如何清楚？mode共有几个参数，参数有什么区别？

## 4.vue中父组件如何给子组件传递值

## 5.react的优缺点

## 6.React组件中props和state有什么区别？

## 7.什么是JSX

## 8.说一下angular、vue、react的相同点和不同点?各适用于什么样的项目场景?

## 9.React中不同组件传递数据的方式有哪些？至少说出三种

## 10.请描述React的组件加载生命周期函数以及shouldComponentUpdate方法的实际使用场景?













