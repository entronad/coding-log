**javascript**

**vue**

**git**

**css**

**html**

**browser**

**webpack**

**react**

**npm**

**vpn**

**react-native**

**dom**

**设计**

**markdown**

**echarts**

**node**

**http**

**mobx**

**babel**

**styled-components**

**redux**

**fetch**

**构建**

**android**

**amap**

**IoT**

**vscode**

**dart**

**flutter**

**shadowsocks**

**ble**

**weixin**

**typescript**

**linux**

**jest**

**算法**

# 2019-01-08

**javascript**

父类构造函数有参数的，记得子类构造函数用...args传给super

# 2019-01-15

**javascript**

import中.js后缀名是否省略，文件夹是否默认导入index.js不是由标准决定的，airbnb认为文件不加后缀名是最佳实践，node中有自动识别index.js的功能，但deno不推荐这样做

# 2019-01-16

**javascript**

在浏览器中，如果script标签引入的是module，要加type="module"，import中模块不可省略后缀名，也没有默认的index.js

浏览器加载中的import文件一定要放在服务器上不能直接通过文件系统，这样会引发跨域错误

# 2019-01-17

**javascript**

特别注意当作为表达式时，a++的值为加之前的，a+=1的值为加之后的，++a为加之前的

**vscode**

在debug配置中，传给启动程序（比如node）的参数给runtimeArgs，传给脚本（比如index.js）的参数给args

# 2019-01-20

**javascript**

ArrayBuffer构造函数传入的是字节数，如果传入的参数大，可能会分派失败

通过给TypedArray传入另一个TypedArray的方式的构造函数，底层是一个新的ArrayBuffer，如需同一个ArrayBuffer，可传入typedArray.buffer

TypedArray与普通数组比，没有concat

x86 体系的计算机都采用小端字节序，TypedArray 数组内部也采用小端字节序读写数据，或者更准确的说，按照本机操作系统设定的字节序读写数据，如要设定字节序用DataView

`TypedArray`视图，是用来向网卡、声卡之类的本机设备传送数据，所以使用本机的字节序就可以了；而`DataView`视图的设计目的，是用来处理网络设备传来的数据，所以大端字节序或小端字节序是可以自行设定的

# 2019-01-21

**javascript**

ArrayBuffer构造函数传入的字节数如果大于1E9，视图获取length会失败

# 2019-02-03

**git**

git bash 中如果要执行.bat需加上XX.bat

# 2019-02-26

**react-native**

很多老版本的库其原生依赖jcenter中可能没有了，需手动进入其源代码添加优先的google()

**android**

AndroidManifest中有uses-sdk标签指定android:minSdkVersion和android:targetSdkVersion

# 2019-02-27

**git**

git add 只会添加当前目录及子目录的内容，如要添加仓库所有改动，确保在根目录下执行

**android**

26版本之后，关键权限一定要求用户在App中确认了

# 2019-05-17

**javascript**

call 从第二个起的参数表将直接作为函数参数表，而apply则是将第二个参数数组的元素作为参数传给数组

call(this, a)    f(a)

apply(this.a)    f(...a)

---

concat(values1, values2)的作用：如果values不是数组，则放到原数组后面，是数组则取出元素放到数组后面，

# 2019-06-13

**css**

当浏览器最大化时，chrome中window.innerWidth, window.outerWidth, screen.width都相等，火狐、IE等window.outerWidth会大于浏览器实际宽度

vw, vh是相对于window.innerWidth, window.outerWidth

---

块级元素不仅仅是display: block的元素

---

对于绝对定位模型（absolute, fixed)，宽度默认是包裹性的，但当top等属性存在对位属性时，宽度表现为充满

---

内部尺寸的表现形式

- 包裹性

按钮有两种：

```
<button>按钮</button>
<input type="button" value="按钮">
```

区别是input默认不换行

按钮是inline-block具有典型的包裹性：宽度根据内容变大，但顶到父元素了内部会换行

- 首选最小宽度

CSS中图片和文字的权重是远大于布局的，width: auto最小的宽度不是0，而是单独汉字或英文单词（以空格, -, ?分隔除非设置了word-break:break-all）

- 最大宽度

最大连续内联盒子的宽度和

---

width作用在最内层的内容上（不含padding）

# 2019-06-14

**css**

由于width是决定内容的，所以对于width的设置建议使用宽度分离原则，即width不与padding、border等设置在同一个元素上，而是设置在外面再嵌套的盒子上。也可以用box-sizeing，但它是没有margin-box的选项的

理论上来讲，非替换元素都不需要设置width

---

替换元素的特点之一是无论display是inline还是block，尺寸由内容决定

---

父元素auto时，width可以设置百分比，高度不可设置百分比，这不是由于计算死循环引起的，事实上auto是不可以乘以百分比的，而width的auto浏览器都给其定义了数值规则

absolut的元素高可设置百分比

绝对定位的百分比相对于padding box 其它的相对于content box

---

width/height默认值是auto，min-width/min-height默认值是auto，max-width/max-height默认值是none

max- min- 的优先级比!important还高，min- 和 max- 冲突时min-优先级高 

---

为高度不定的元素设置收起动画，可用max-height ，为其设置一个保证足够的最小值

```
element {
    max-height: 0;
    overflow: hidden;
    transition: max-height .25s
}
element.active {
    max-height: 666px;
}
```

---

内联元素中重要的盒子

- 内容区域：指围绕文字的看不见的区域，通常为鼠标选中文本的区域（chrome略有偏差）
- 内联盒子：内联标签的盒子，如果是单独的文字构成匿名内联盒子，注意如果单独文字在块级标签中则构成匿名块级盒子
- 行框盒子：指每一行，由内联盒子组成
- 包含盒子（包含块）指所有行盒子构成的

在HTML5中每个行框如同前面有一个空白节点一样，它不占任何宽度，但有高度，称为strut

---

替换元素有默认尺寸，比如img是0，video, iframe, canvas 是300px*150px

---

文字是否换行，连续空白符是否合并由wite-space属性决定：

|            | 换行符 | 空格和制表符 | 文字转行 |
| ---------- | ------ | ------------ | -------- |
| `normal`   | 合并   | 合并         | 转行     |
| `nowrap`   | 合并   | 合并         | 不转行   |
| `pre`      | 保留   | 保留         | 不转行   |
| `pre-wrap` | 保留   | 保留         | 转行     |
| `pre-line` | 保留   | 合并         | 转行     |

---

替换元素的display不管是什么，尺寸计算规则都是一样的

替换元素的尺寸由内而外分为：

- 固有尺寸：内容本身的尺寸
- html尺寸：直接在标签中设置的width, height, size, cols, rows
- css尺寸

input是替换元素，其font-size/padding/margin的默认值单位是px，以便保证固有尺寸不受外界css的影响

优先级是css > html > 固有尺寸，宽高如果只设置了一个将根据其固有尺寸的宽高比确定另一个

占位空图片的最好方式：

```
<img>
img {visibility: hidden;}
img[src] {visibility: visible;}
```

可通过::before或::after伪元素的content属性，插入非替换内容

# 2019-06-19

**css**

flex布局项目最终的主轴方向长度是grow和shrink后的结果，显示设置height不一定有用，利用此特性可以添加滚动条，因为overflow属性要起作用一定要有height，可以设置个height: 0;

---

flex自动计算出的东西百分比宽高是可用的

---

background-size等只能作用于图片

---

对于长度不定，但想显示出无限延伸效果的，即太短不铺满屏幕时它铺满屏幕，太长时自动包裹内容撑大父元素的，可再其后再加个元素，背景与其衔接，前置设置flex: none 后者设置flex: auto

---

table元素本身不是block所以不可以设置高度，一般包裹一层div

为tr设置border，需将tr所在table的css样式border-collapse设置为 collapse；

比如：

table{border-collapse: collapse;}

table tr{border-bottom:solid 1px #d0dee5;}

# 2019-06-20

**css**

::before ::after伪元素（单引号为过时写法）表示生成一个行内元素作为目标的第一个子元素，配合content属性使用，常用作字体图标

配合q标签可添加引号：

```
<q>一些引用</q>, 他说, <q>比没有好。</q>.

q::before { 
  content: "«";
  color: blue;
}
q::after { 
  content: "»";
  color: red;
}
```

---

内联元素也是有垂直方向上的padding的，只是由于内联元素没有可视高度与可视宽度，垂直方向的行为由line-height和vertical-align控制，当设置overflow:auto 就可以看出区别了

利用这一特性，可以增加行内文字的可点击区域，而不影响视觉表现，还可以在地址栏hash定位时给上面空距离

padding百分比都是相对宽度，利用这一特性可以制作宽高比一定，根据屏幕宽度缩放的图片容器（内容用绝对定位）

ol ul input button select等标签注意会有个默认的padding，

button标签的padding在不同浏览器下千差万别且不好控制，所以一般用a标签模拟，如果为保持button的表单特性，也可用label标签处理，但注意id对应

实现菜单三道杠按钮

```
.icon-menu {
    display: inline-block;
    width: 140px; height: 10px;
    padding: 35px 0;
    border-top: 10px solid;
    border-bottom: 10px solid;
    backgroud-color: currentColor;
    background-clip: content-box;
}
```

双层原点

```
.icon-dot {
    display: inline-block;
    width: 100px; height: 100px;
    padding: 10px;
    border: 10px solid;
    border-radius: 50%;
    background-color: currentColor;
    background-clip: content-box;
}
```

---

滚动容器的padding-bottom在chrome下正常，在Firefox，IE下不显示，可通过给子元素设置margin-bottom处理

---

设置左右两栏等高为最高的一栏的内容，且背景填满：可理解为不改变元素本身所占尺寸的外涂色

```
.column-box {
    overflow: hidden;
}
.column-left, column-right {
    margin-bottom: -9999px;
    padding-bottom: 9999px;
}
```

----

空块级元素（没有height）的上下margin会合并

---

margin的auto值会自动填充剩余，而缺省值是0，所以margin-left: auto会使其右对齐

margin: auto有效有一个前提条件是元素在该方向上是自动充满的，因此height方向是无效的

利用这一特性实现绝对定位实现垂直水平居中：

```
.father {
    width: 300px;
    height: 150px;
    position: relative;
}
.son {
    positive: absolute;
    top: 0; right: 0; bottom: 0; left: 0;
    width: 200px; height: 100px;
    margin: auto;
}
```

---

display为inline的非替换元素垂直margin无效，替换元素有效且永无合并

---

绝对定位，或定宽高容器，在对应方向上的margin-right，margin-bottom计算优先级很低，不一定有效

---

border-width不能设百分比，其它还有outline，各种shadow

---

border-style默认值为none

---

border-style dash和dotted在不同浏览器下样式不同

---

border-style double 只有在width大于等于3时才有效，宽度分配规则是双线宽度永远相等，中间间隔加减1

---

border-color默认就是color，可以方便悬浮变色等场景

---

border也算点击区域，可以用它扩大点击区域

---

overflow的规则边界是border内边缘，即padding里的内容保留

---

line-height的定义是两基线间的距离

---

字母小写x的高度称为x-height，x的下边缘是baseline，上边缘是等分线（或中线），vertical-align:middle对其的线是1/2 x-height（x的交叉点），由于各个字体重心不同，所以vertical-align:middle不能保证文字在行内看起来居中

单位ex即x-height的高度，它随字体变化，故不用来定义长度，但可用来对齐行里的小箭头等图标：

行内元素，图标高度1ex，背景图片居中

```
.icon-arrow {
    display: inline-block;
    height: 1ex;
    background: url(arrow.png) no-repeat center;
}
```

---

div中写几个字就有了高度，这个高度是完全由line-height决定的而不是font-size, margin, padding，border等对其完全没有影响

---

css中的行距为行高-em-box,即line-height-font-size，分成两半文字上下方各一半，称为半行距，文字实际可能超出或小于em-box

---

line-height不能为负值，但行距可以为负值（即font-size大于line-height）

---

当行内有替换元素时，line-height只能决定行的最小高度

---

line-height的默认值是normal，它是变化的，随浏览器和字体而不同，基本在1~1.5之间

不加单位的line-height子元素继承的是计算规则，加了单位或百分比继承的是结果，如果要也继承规则，需用选择器进行通配* {line-height: 150%}

line-height全局设置固定值、百分比，数值都有很多应用

line-height的计算值是向上取整的

---

块级元素、内联元素都可以设置line-height，对于块级元素套内联元素的情况，块级元素的行高作用于strut，因此最终块级元素的高度由strut与内联元素中高的决定，即表现为块级元素高度由父子行高中高的决定，

很多时候就算块级父元素只有一个内联子元素，块级元素的表现也会受strut影响，比如当父子字号不一样但line-height一样时，基线对齐后的错位会撑高高度

---

vertical-align设置为长度值、百分比时，是相对于baseline移动，向上为正，百分比是相对于line-height

vertical-align只能作用于行内元素和table-cell

vertical-align: middle指的是元素中部与x-height的一半对齐

---

不同元素的baseline：文字x的下边缘，替换元素下边缘，inline-block如果没有内联元素或overflow不是visible是margin下边缘否则是最后一行内联元素基线

---

vertical-align top 与 text-top的区别为前者是行框的顶部，后者是内容区域的顶部不受左右其它内联元素影响

---

vertical-align 中的sub和super这两个值，对应的有sup, sub这两个标签，注意属性不会改变文字大小，而标签font-size默认是smaller

---

float的浮动参考是行框盒子

---

overflow-x和overflow-y当一边不是visibal，则另一边如设置visibal会表现的像auto，即不可能出现一边显示，另一边隐藏/滚动

---

在pc端，页面最外面的滚动条是html的，而移动端不一定

# 2019-06-26

**css**

包含块：

1.初始包含块为根元素，尺寸等同于浏览器视窗

2.relative或static包含块为最近的祖先容器的content box

3.fixed包含块为初始包含块

4.absolute包含块为最近的不为static的祖先元素的padding box建立，如果祖先是内联的情况比较复杂

注意height: 100%是相对于包含块，而height: inherit则是相对于父元素

---

absolute定位的元素具有包裹性，也有自适应性，自适应性是相对于包含块，文字超过包含块宽度就会换行，不管它位置在哪里，设置white-space: nowrap可以避免

---

当没有设置top等属性时，absolute不是相对于包含块，而是成为“无依赖绝对定位”，是相对于父元素左上，如果只设置了一个方向上的位置，则另一方向仍是无依赖绝对定位

# 2019-06-27

**javascript**

用new Array(n)生成的数组每个元素是没有值，hasOwnProperty为false，因此不可调用map，而显式设置undefined是有值的，hasOwnProperty为true，可以调用map

将iterable转换为数组最方便的方式是[...it]，所以生成n个等于下标的数组，生成1-n的数组：

```
[...Array(n).keys()]

[...Array(n + 1).keys()].slice(1)

// Ts 中只能用Array.from
```

# 2019-07-02

**css**

如果overflow不是定位元素，同时绝对定位元素和overflow容器之间也没有定位元素，则overflow不对absolute元素进行裁剪

fixed元素包含块是根元素，中间所有的overflow无效

transform会对overflow原则有意外的影响

clip属性将被移除，建议使用clip-path，它可实现可访问性隐藏

---

虽然relative的移动是相对于自身，但是top等的百分比却是相对于包含块

relative不会表现流动性，left right只有其一能有效

relative的z-index比正常文档流高

relative尽量不要用，要用要坚持影响最小，即套一个不可见的wrapper设为relative，自身设为absolute

fixed元素不会覆盖html的滚动条，鼠标在fixed蒙层上滑动后面依然会动，可用js阻止滚动事件，并设置overflow 和border-right

---

z-index只对定位元素、flex box的子元素有效，z-index只是层叠水平规则的一小部分，任何元素都有层叠水平

层叠顺序按装饰 -> 布局 -> 内容的顺序：层叠上下文 -> 负z-index -> block -> float -> inline -> auto,0 z-index -> 正z-index

z-index谁大谁上面，后来的在上面

---

谁会形成层叠上下文：

页面根元素、定位元素（relative/absolute/fixed）、z-index不为auto、flex布局且z-index不为auto，opacity不为1，transform不为none

特别注意z-index为负结果是放在层叠上下文之上，block块之下，可用来做背景、隐藏元素等

非浮层元素避免设置z-index，z-index理论上来讲不需要超过2

---

常用字体族分为

serif: 衬线字体

sans-serif: 无衬线字体

monospace: 等宽字体

system-ui:系统UI字体

无衬线字体指笔划宽度基本一样，现在人一般喜欢这种，比如微软雅黑，苹方，droid都挺好看的，一般可设置sans-serif

代码展现常用等宽字体

单位ch指数字0的宽度，当使用等宽字体时有用，可用在号码输入等场合

---

font-weight如为数值只可以是100-900的整百数。400是normal，900是bold，bolder和lighter指的是处在临界范围内的相对于父元素font-weight，注意可能有些字体只有normal和bold

font-style指斜体，italic指用字体的斜体如果没有则让其斜过来，oblique指让字斜过来，很多中文字体没有斜体，一般都设italic

可用@font-face定义字体

现在web开发不考虑兼容性最好的字体文件格式是woff2, url后面的format是为了让浏览器提前知道字体格式

用字体定义图标主要为了兼容，今后应该会被svg替代

---

可以用letter-spacing设置字符间距，word-spacing控制单词间空格的大小

word-wrap:break-word不能打断英文单词，还是用word-break:break-all

text-align:justify要起效需超过一行，非最后一行起效，英文要超过一个词

移动端text-align-last无效

---

word-break, white-space适用于所有元素，具有继承性

text-align，text-indent等是块级元素的，具有继承性

line-height是块级元素的时指子元素的最小行盒高度，是内联元素的时指行盒高度，具有继承性

vertical-align是内联元素的，不具有继承性

---

text-decoration一般用line-through做删除线，作下划线时会与文字粘住，一般用内联元素的border-bottom比较好，它不会影响布局，默认颜色和文字一样，

可用text-transform控制大小写，作用于所有元素，具有继承性

---

::first-letter伪元素限制很多，可设属性也有限，::first-line相对好点

---

隐藏元素的background-img是否请求各浏览器不一, img标签的图片都会请求；base64图片当尺寸大时渲染性能不好

background-position设置百分比时计算方法独特

---

背景色一定是在最低处的，因此可用background-color统一设置点击效果（它覆盖原来的背景色）

# 2019-07-03

**css**

display:none会使本身和所有子元素都不可见，而visibility:hidden只会作用本身，但它具有继承性

transition可作用于visibility

outline是元素获得焦点时的提示，语法类似border

cursor有很多，比如none用于在视频上隐藏光标，progress和wait提示等待，move表示可移动，not-allowed表示禁用，zoom-in,zoom-out放大缩小，url()自定义光标

direction ltr,rtl可以改变文字左右方向，writing-mode可以改变文字横竖，注意使用标准语法：horizontal-tb, vertical-rl, vertical-lr,注意它会改变整个css的规则

# 2019-08-21

**javascript**

sort方法的比较函数，一般就用前面的减后面的，注意当等于0时，理论上来讲并不保证顺序不变，所以可以做个处理，dart也是

# 2019-08-28

**javascript**

debounce 和 throttle

wait: 按下后等待此时间再执行training，期间如果再按将刷新此等待时间，直到最后一次按完后再等待此时间后执行

options.maxWait: 第一次按下后此时间后将一定会执行training，哪怕其间多次按了使得wait不断刷新

throttle 为 maxWait强制等于wait的debounce，即一定确保在wait后执行

此外debounce只有trailing默认true，throttle两个都默认true

# 2019-09-02

**javascript**

常见导致内存泄露的情况：

1.全局变量

2.未销毁的定时器，它会导致其回调函数也无法回收

3.闭包

4 DOM引用，如果保存DOM对象的对象或数组还存在，即使此DOM已经从树上移除（document.body.removeChild）其也还会在内存中；子元素不回收父元素也不会被回收

WeakSet 和 WeakMap 就是为解决此问题的，WeakSet中的元素和WeakMap中的**键**只能是对象，它们是若引用的，如无其它引用（比如从DOM树上移除了），将自动消失。比如可将DOM与其对应的数据作为WeakMap的键值（注意WeakMap的值不是弱引用）

# 2019-09-04

**html**

下载可用a标签带download属性来实现

```
const a = document.createElement('a');
a.download = 'somename';
a.href = url;
document.body.appendChild(a);
a.click();
a.remove();
```

将其插入目录树是为了兼容火狐

**react**

react的onClick不是原生的事件，可用e.stopPropagation()阻止进一步传播

# 2019-09-11

**react**

Context

通过Mycontext = React.createContext(value)生成，value为初始值

在需要用到的子树的根部通过<MyContext.Provider value={}>注入

需要使用时，class定义的组件通过Calss.contextType和this.context使用；函数定义的组件通过<MyContext.Consumer>使用，组件函数的参数是value

Context的主要作用是参数透传，要实现参数的修改，需在Provider处注入参数修改器

如需组合多个Context，只有采取嵌套的办法

# 2019-10-10

**html**

元素的子节点有childNodes和children两个字段，前者是标准的，返回所有类型节点（元素、属性、文本），后者是非标准的，只返回节点

# 2019-10-11

**javascript**

原型链是面向编程的概念，在引擎中相同“形状”的对象会优化统一成“shape”，论文中一般称为Hidden Class，v8称为Map，JSC称为Structure。

如果是动态的增加对象的字段，将会形成transition chains and trees，transition chains产生的对象和直接产生的对象哪怕结果形状一样，也不会认为是一样的shape，

不要对数组使用 `Object` 对象下的方法，尤其是 `defineProperty`，因为这会让 JS 引擎在存储数组元素时，使用 `Dictionary Elements` 结构替代 `Elements`，而 `Elements` 结构是共享 `PropertyDescriptor` 的

使用 `proxy` 监听对象变化比 `Object.defineProperty` 更优，因为 `Object.defineProperty` 会破坏 JS 引擎对数组做的优化。

# 2019-10-16

**html**

动态设置元素高度要起效，需用：

```
document.getElementById('div_register').setAttribute("style","width:500px");
```

的形式

---

获取元素实际的width、height、top、left等位置信息，有

offset-    client-   scroll 三种前缀

其中宽高：offset是border外，client是border内，scroll是没有滚动条的border内

起点：offset是margin框，client就是上下border，scroll是滚动条位置

---

overflow: visible 有一条非常重要的隐藏特性：当没有其它auto或hidden限制时，当元素在用户代理视口中放不下时，用户代理会出现“神秘滚动条”，以确保visible的部分一定能显现，这是用户代理的部分，而不是由auto或scroll产生的，

解决办法是在html标签上加overflow: hidden

---

html可以设置大小位置小于窗体，但其背景一定会作用到整个

# 2019-11-12

**css**

offsetWidth会触发重绘，对性能影响极大，建议使用 getBoundingClientRect

# 2019-12-13

**react**

注意事件冒泡只能在dom树的上下关系中传递（不是屏幕上的上下关系，不能传给兄弟）

---

reac中的e是单例池化的，异步或传递之后就又空了，故要在最直接的handler中浅拷贝一下const eCopy = {...e};

---

js中也可以直接this.rootDiv.current.style.XXX设置style的具体属性，但不能用个新对象设置this.rootDiv.current.style全体

**css**

当使用css module时，animation要name放第一个，不能用时间放第一个的写法

---

重新触发css动画的办法可以是移除再重新加上类名，注意中间用获取一下element.offsetWidth触发回流

# 2019-12-18

**javascript**

脚本中如果要用到dom的话，不能放在head中，要放在body，而且放在body中所要用的dom之后，此时才已经有了这个dom，事实上一般script都建议放在body末尾

在<head>中加载的脚本，不能使用dom，此时dom还没有生成，