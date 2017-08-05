# 2017-05-06

**Vue 笔记**

- Vue 实例可以认为是 ViewModel，常用 vm 作为变量名
- Vue 中的 data 对象为代理，类似于引用赋值


# 2017-05-08

**Vue 笔记**

- 组件中的data需定义为函数，且返回一个新的data对象

- 父子组件的通讯

  > props down, events up


# 2017-05-10

**element-ui **

NavMenu 导航菜单中若在` <el-menu/>`中设置 router 参数，则其中`<el-menu-item/>`的 index 参数值即为路由地址

**git**

添加密钥到ssh中时，为防止报

> Could not open a connection to your authentication agent

的错误需用以下命令：

```
eval `ssh-agent -s`
ssh-add
```
# 2017-05-11

**CSS**

`color`属性：检索或设置对象的文本颜色。`color`属性值被间接用来提供一个中间值` currentColor`以供其他接受颜色值的属性使用。

`text-align`属性规定元素中文本的**水平**对齐方式，有`left`, `right`, `center`, `justify`等值。行内元素的垂直对齐方式通过`vertical-align`属性设置。

---

`background`可以设置 背景颜色、背景图片、定位等 ；
`background-color`只能设置 背景颜色 。

设置`background-color: #aaa;`时仅仅改变了背景色，但此时有一个默认的的`background:repeat;`
而设置`background: #aaa;`后，相当于同时设置了`background:no-repeat;`
即：

```
{background-color: #aaa;background:no-repeat;}=={background: #aaa;}
```
# 2017-05-12

**CSS**

`box-shadow`属性：向框添加阴影

```
box-shadow: h-shadow v-shadow blur spread color inset;
```

```
box-shadow: 10px 10px 5px #888888;
```

```
box-shadow: 0 0 1px #ddd;
```

------

`white-space`属性：设置如何处理元素内的空白

------

选择器中写两个类，如中间无空格为多类选择器，有空格为派生选择器

------

**Vue**

component 类似“类”的概念，名称、文件名大写

------

`<template>` 中的根标签要缩进，`<sctipt>`、`<style>` 中的内容不缩进

# 2017-05-14

**CSS**

`top`、`right`、`bottom`、`left` 属性定义与各边边距

# 2017-05-15

**Vue**

父组件通过事件接受子组件参数时，绑定处只要写函数名，参数会自动传入函数中

---

**CSS**

想要`heigt: 100%`起作用需先同时设置`body`与`html`的高度：

```
<html style="height: 100%;">
  <body style="height: 100%;">
    <div style="height: 100%;">
      <p>
        这样这个div的高度就会100%了
      </p>
    </div>
  </body>
</html>
```

# 2017-05-16

**CSS**

`line-height: 1.5`  和 `line-height: 150%`  的区别区别体现在子元素继承时，如下：

- 父元素设置line-height:1.5会直接继承给子元素，子元素根据自己的font-size再去计算子元素自己的line-height。
- 父元素设置line-height:150%是计算好了line-height值，然后把这个计算值给子元素继承，子元素继承拿到的就是最终的值了。此时子元素设置font-size就对其line-height无影响了。

# 2017-05-17

**Vue**

组件的 `<style>` 如果加了scope属性，则其子组件也无法继承这些样式

---

**HTML**

`<table>` 表格

`<tr>` 行

`<th>` 表头项

`<td>` 内容项

---

**CSS**

top、margin-top的区别：

1. top、bottom、left、right是绝对定位，必须设置position为absolute。

   margin一系列设置是相对定位。

   注意：如果用top等，而position未设置为absolute，那设置是不起作用的。

2. top这些在绝对定位的前提下，这个绝对定位，是相对body  或者  position：relative的父级元素的绝对定位。

   margin的相对定位，是指相对相邻元素的定位。

---

文本不换行，超出以省略号显示

```
white-space: nowrap;
overflow: hidden;
text-overflow:ellipsis;
```

---

**Vue**

事件处理器参数可为：

- JavaScript 代码：`@click="counter += 1"`

- 方法：`@click="greet"`

- 内联处理器方法：`@click="say('what')"`

  其中内联语句处理器中访问原生 DOM 事件。可以用特殊变量 `$event` 把它传入方法

   `$event` 为`this.$emit('click', value)`中的第二个参数value（$emit只有两个参数）

# 2017-05-18

**Vue**

props 中的参数，子组件中无权修改，只有 $emit 事件通知父组件修改

---

vue 中引入 axios 分两种情况，组件中通过原型链引入，vuex 中直接引入，两者相互独立

# 2017-05-19

**Vue**

vuex 中的 state 可直接读取，getters 相当于计算属性

---

mutation 的参数为 (state, payload)，

action 的参数为(context, payload)，action 可为 async 函数

---

模块内部的 action、mutation、和 getter 现在仍然注册在**全局命名空间**，直接引用其 Types，引用state需加模块名

---

1. `v-if`和`v-for`放在一个元素内同时使用，因为Vue总会先执行`v-for`，所以导致`v-if`不会被执行。替代地，你可以使用一个额外的`template`元素用来放置`v-if`或者`v-for`从而达到同样的目的。这是相关的[issue](https://github.com/vuejs/vue/issues/3106)。
2. 计算属性对于直接的数据比如`a: 2` -> `a: 3`这样的数据变动可以直接检测到。但是如果是本例中的`list`的某一项的`status`这个属性变化了，如果我们直接使用`list[index].status = true`这样的写法的话，Vue将无法检测到数据变动。替代地，可以使用`set`方法（全局是`Vue.set()`，实例中是`this.$set()`），通过`set`方法可以让数据的变动变得可以被检测到。从而让计算属性能够捕捉到变化。可以参考官方文档对于响应式原理的[描述](https://cn.vuejs.org/v2/guide/reactivity.html)。

---

`overflow: auto;`如果内容被修剪，则浏览器会显示滚动条以便查看其余的内容。

# 2017-05-19

**CSS**

通过`margin: 0 auto;`设置居中需设置 width 值

# 2017-05-22

**CSS**

只有当父元素的 position 设为 relative 时， 其子元素的 absolute position 是按照父元素的相对位置来的 

# 2017-05-23

**Vue**

当<style>标签设置scoped属性后，将在该标签里的类名添加后缀以区别

**CSS**

宽高的百分比是在减去padding之后，无需考虑滚动条

# 2017-05-24

**Vue**

尝试在`actions`里面`commit`另一个`mutation`，而不是在`mutation`里调用另一个`mutation`方法。

---

状态中的数据来源如是后端api，网络请求应当放在action中

# 2017-05-25

在字面量定义对象中如所定义方法只有一个表达式，宜采用`方法名: 箭头函数`的形式：

```
const getters = {
  checkoutStatus: state => state.checkoutStatus
}
```

如所定义方法有多个语句，宜采用`方法名(参数) {语句块}`的形式：

```
const actions = {
  checkout ({ commit, state }, products) {
    const savedCartItems = [...state.added]
    commit(types.CHECKOUT_REQUEST)
  }
}
```

在箭头函数中，以下两种情况需注意加括号：

- 参数虽然只有一个，但为对象解构赋值的:

  ```
  ({state, payload}) => state.checkoutStatus
  ```

- 只有一个表达式，但为对象字面量的:

  ```
  state => ({a: state.checkout, b: state.Status})
  ```

---

**Vue**

Vue组件中要用到模块尽量挂载在Vue示例中，其他.js模块中哪个要用哪个引入

---

import from 文件夹 即为引用该文件夹中的index.js

---

async 函数的多种声明方式：

```
// 函数声明
async function foo() {}

// 函数表达式
const foo = async function () {};

// 对象的方法
let obj = { async foo() {} };
obj.foo().then(...)

// Class 的方法
class Storage {
  constructor() {
    this.cachePromise = caches.open('avatars');
  }

  async getAvatar(name) {
    const cache = await this.cachePromise;
    return cache.match(`/avatars/${name}.jpg`);
  }
}

const storage = new Storage();
storage.getAvatar('jake').then(…);

// 箭头函数
const foo = async () => {};
```

---

JavaScript 的 Array方法push()返回值是数组长度而不是数组本身

# 2017-05-27

**CSS**

margin 的 auto 为“浏览器设置的外边距”，左右会自动居中，但上下为0，故可通过`margin: 0 auto;`设置水平居中，但不可`margin: auto 0;`设置垂直居中。

---

高度首先要比较父元素设定z-index之后确定的 stacking context，同一stacking context再进行比较

当 position 为默认的 static （处于文档流中）时，z-index 无效

**Vue**

Vue 中引入JS库的最佳实践：以插件的形式引入

---

iview组件阻断了原生的事件，且无法接受捕捉与冒泡的事件

# 2017-05-27

**Vue**

不应该对 data 属性使用箭头函数，不应该使用箭头函数来定义computed, methods, watch, 生命周期钩子中的函数。这是因为这些属性将被混入到 Vue 实例中。所有 的 this 上下文自动地绑定为 Vue 实例。而箭头函数绑定了父上下文，因此 `this` 与你期待的 Vue 实例不同。

---

state 在组件中通过computed引用

**HTML**

localStorage中只可存储字符串，如存入对象，需用JSON.stringfy()，取出对象需用JSON.parse()

取出对象字符串在parse前需判断对象字符串是否存在

# 2017-05-31

**Vue**

在Vue组件中定义的函数都不该用箭头函数，因为其中的this需与运行时的调用对象——Vue实例绑定，而其中若要定义函数则需使用箭头函数，以与其定义时，即Vue对象的运行时的调用对象——Vue实例绑定

---

v-bind:class 参数对象中的变量名需加引号

# 2017-06-01

**Vue**

vue中父组件调用子组件的方法：

```
<child1 ref="child1"></child1>

this.$refs.child1.handleParentClick("ssss")
```

# 2017-06-03

**Vue**

iview中menu组件的active-name属性并不是与当前选项双向绑定，只决定初始选项，或通过updateActiveName手动更新当前选项

**HTML**

HTML的属性分为两种：content attribute 和IDL attribute

content attribute即标签里的设置的属性，它必是字符串

IDL attribute即JavaScript DOM对象的属性

这两者的关联尽可能的developer-friendly，不过有时会很奇怪

https://developer.mozilla.org/zh-CN/docs/Web/HTML/Attributes

# 2017-06-06

**Vue**

初始化逻辑不可直接写在script标签中，需写在钩子中，beforeMount钩子中还没有dom

---

不同组件内的标签id，也要是全局唯一的

# 2017-06-10

**Browser**

```
webkit内核
+---safari
+---chrome
+---chromium (改造为blink内核)
+---mobile webviews
```
**Vue**
webpack打包的index.html中，所引用的文件目录都是绝对路径，起点为站点的根"/"，如作为webapp，需改为相对目录

---

把根目录下`config/index.js`中的`productionSourceMap: true`改为`false`可不打包map文件，减小目标文件体积

# 2017-06-12

**CSS**

background-size属性必须在background属性之后，且在同一个class中定义

**Vue**

在data中的变量定义时不可引用data中的其他变量，因为此时data还没生成

# 2017-06-13

**Vue**

Tip: built files are meant to be served over an HTTP server.
  Opening index.html over file:// won't work.

**静态直读不可用history模式**



**响应式**

**五、rem 适配**

对于移动端的开发，rem 适配必不可少，我们可以用多种方式实现，下面给出一种方案

在 index.html 中添加如下代码

`<``script``>`

` ``let html = document.documentElement;`

 

` ``window.rem = html.getBoundingClientRect().width / 16 ;`

` ``html.style.fontSize = window.rem + 'px';`

`</``script``>`

这里基于宽 320px 的屏幕分成了 16 份，也就是 1rem = 20px，目前大多数设计稿都是根据 iphone6 的宽（ 375px ）走的，建议大家在这里分成 25 份，也就是 1rem = 15px，计算起来方便些。

**简单说下 rem 原理**：根据 html 的 fontSize 属性值为基准，其它所有的 rem 值，根据这个基准计算。

我们根据屏幕宽度用 js 动态修改了 html 的 fontSize 属性值，达到移动端适配的目的

**总结**

以上就是这篇文章的全部内容了，本文作为移动端配置的基础篇，深入了解框架后才能继续构建网站，希望这是一个好的开始，有了这个架子再填充代码就方便了许多，不用再去考虑开发环境问题了。希望本文的内容对有需要的朋友们能有所帮助。

**vue-router**

有时候，同一个路径可以匹配多个路由，此时，匹配的优先级就按照路由的定义顺序：谁先定义的，谁的优先级就最高。

要注意，以 / 开头的嵌套路径会被当作根路径。 这让你充分的使用嵌套组件而无须设置嵌套的路径。

vue-router 的导航方法 （`push`、 `replace`、 `go`） 在各类路由模式（`history`、 `hash` 和`abstract`）下表现一致

---

'#' 称为hash或锚点

协议, 域名, 路径, 参数 这些数据都是与服务器进行交互的。唯独 hash 是与浏览器进行交互的。

改变 hash 的值浏览器不会刷新

**vue作为静态资源打包**

assetsPublicPath: './',或''
productionSourceMap: false,

路由模式用hash

在文件系统中没有根，只能用相对的

# 2017-06-15

**webpack**

热监视编译：webpack --watch

热更新编译：全局安装 webpack-dev-server 命令：webpack-dev-server --contentbase src --inline --hot

# 2017-06-23

**React**

组件名称必须以大写字母开头

组件的返回值只能有一个根元素

React 元素的事件处理和 DOM元素的很相似。但是有一点语法上的不同:

- React事件绑定属性的命名采用驼峰式写法，而不是小写。
- 如果采用 JSX 的语法你需要传入一个函数作为事件处理函数，而不是一个字符串(DOM元素的写法)

**JavaScript**

func.bind(obj)：返回一个新创建的函数实例，其this值绑定到obj

# 2017-06-24

**npm**

修改package.json后需关注package-lock.json

# 2017-06-30

**react**

JSX中标签的类名为className

ReactNative在加载网络图片时一定要事先设置宽高

加载原生图片资源时，Android只能加载drawable中的而不能加载mipmap中的

加载本地文件系统中的图片：

```
let imgUrl = Platform.OS === 'android' ? 'file:///' + this.state.imgPath : this.state.imgPath
source = {{uri: imgUrl}}
```

# 2017-07-02

**webpack**

设置多个entry是为多个页面使用，用对象可配置chunk的name

filename: 文件名，path: 路径

filename中可使用占位符

hash是本次打包的hash，每次打包不一样，每个文件一样

chunkhash是模块的hash，每个文件只有有变化就不一样，类似md5校验

config上下文默认的是运行脚本时的当前目录（不是config的目录），而config中的__dirname则是参数文件所在目录

loader是用来处理资源文件的

include, exclude需跟绝对路径，一般采用path.resolve()、path.join()方法来处理

在main.js中直接import css

loaders数组的顺序按加载的顺序逆序

**vpn**

MonoCloud

# 2017-07-03

**react-native**

fetch中post的body要将对象序列化：JSON.stringfy(data)

# 2017-07-04

**JavaScript**

obj.a == null可同时起到obj.a === null与obj.a === undefined作用

# 2017-07-06

**DOM**

addEventListener的回调函数中添加e.preventDefault()阻止默认行为，比如a标签的跳转

---

DOM0级事件：通过标签内或onclick = 的方式定义的事件；DOM0级事件只能存在一个，后面的会覆盖前面的；DOM0级事件方法被认为属于元素作用域，this绑定元素

DOM2级事件：通过addEventListener()添加的事件，DOM2级事件多个可以共存，可以与DOM0级事件共存。只有DOM2级事件有事件流；removeEventListener()参数与addEventListener()相同，故要能移除，回调函数需具名；第三个参数，是否是捕获时触发

DOM3级事件：内容和验证上更多的扩展

# 2017-07-07

**Webpack**

脚本流程：rm删除dist/static下的所有文件，执行webpack(config, callback)

# 2017-07-08

**DOM**

<html>可通过document.documentElement快捷访问，等价于

document.childNode[0]

document.firstChild

<body>可通过document.body快捷访问

**Webpack**

webpack-dev-server和webpack-dev-middleware打包的结果是在内存中

# 2017-07-09

**HTML**

元素的布尔属性，只要出现，不管值为什么表示true，不出现为false，不可用true/false赋值，以前习惯用同名值

HTML5规定：

> The presence of a boolean attribute on an element represents the true value, and the absence of the attribute represents the false value.
>
> If the attribute is present, its value must either be the empty string or a value that is an ASCII case-insensitive match for the attribute’s canonical name, with no leading or trailing whitespace.
>
> The values “true” and “false” are not allowed on boolean attributes. To represent a false value, the attribute has to be omitted altogether.

# 2017-07-10

**HTML**

标签语义化

> 方便开发维护
>
> 更好的SEO
>
> 无CSS时能呈现
>
> 利于浏览器加载

**webpack**

UglifyJs无法处理es6模板字符串

webpack-dev-middleware需要老老实实用express

# 2017-07-11

**JavaScript**

slice方法的两个参数前闭后开

---

&&

> 如果第一个操作数是 Boolean 类型，而且值为 false ，那么直接返回 false。 
> 如果第一个操作数是 Boolean 类型，而且值为 true，另外一个操作数是 object 类型，那么将返回这个对象。 
> 如果两个操作数都是 object 类型，那么，返回第二个对象。 
> 如果任何一个操作数是 null，那么，返回 null。 
> 如果任何一个操作数是 NaN，那么返回 NaN。 
> 如果任何一个操作数是 undefinded，那么返回 undefined。 

||

> 如果第一个操作数是 boolean 类型，而且值为 true， 那么，直接返回 true。 
> 如果第一个操作数是 Boolean 类型，而且值为 false ，第二个操作数为 object，那么返回 object 对象。 
> 如果两个操作数都是 object 类型，那么返回第一个对象。 
> 如果两个操作数都是 null，那么，返回 null。 
> 如果两个操作数都是 NaN，那么返回 NaN。 
> 如果两个操作数都是 undefined，那么，返回 undefined。 

**Vue**

数组会触发视图更新的方法：

- `push()`
- `pop()`
- `shift()`
- `unshift()`
- `splice()`
- `sort()`
- `reverse()`

当使用非变异方法`filter()`, `concat()`, `slice()`时，可以用新数组替换旧数组：

```
example1.items = example1.items.filter(function (item) {
  return item.message.match(/Foo/)
})
```

由于 JavaScript 的限制， Vue 不能检测以下变动的数组：

1. 当你利用索引直接设置一个项时，例如： `vm.items[indexOfItem] = newValue`
2. 当你修改数组的长度时，例如： `vm.items.length = newLength`

为了解决第一类问题，以下两种方式都可以实现和 `vm.items[indexOfItem] = newValue` 相同的效果， 同时也将触发状态更新：

```
// Vue.set
Vue.set(example1.items, indexOfItem, newValue)
```

```
// Array.prototype.splice
example1.items.splice(indexOfItem, 1, newValue)
```

为了解决第二类问题，你可以使用 `splice`：

```
example1.items.splice(newLength)
```

# 2017-07-19

**react-native**

RN中：`flexDirection`的默认值是`column`而不是`row`，而`flex`也只能指定一个数字值

RN支持WebSocket

|                 | react-native-cli                         | create-react-native-app                  |
| --------------- | ---------------------------------------- | ---------------------------------------- |
| 命名              | 项目名不可含有-，可有_                             | 项目名可有-                                   |
| dependencies    | react, react-native                      | expo, react, react-native                |
| devDependencies | babel-jest, babel-preset-react-native, jest, react-test-renderer | react-native-scripts, jest-expo, react-test-renderer |
|                 |                                          |                                          |

官方支持的导航是 react-navigation

require中的图片名字必须是一个静态字符串（不能使用变量！因为require是在编译时期执行，而非运行时期执行！）

Android、IOS都可使用@2x、@3x加载不同分辨率图片

在React Native中，另一个值得一提的变动是我们把`src`属性改为了`source`属性，而且并不接受字符串，正确的值是一个带有`uri`属性的对象。

```
<Image source={{uri: 'something.jpg'}} />
```

开发者们常面对的一种需求就是类似web中的背景图（`background-image`）。要实现这一用例，只需简单使用`<ImageBackground>`组件，然后把需要背景图的子组件嵌入其中即可。

```
return (
  <ImageBackground source={...}>
    <Text>Inside</Text>
  </ImageBackground>
);
```

如果要在**Android**上使用LayoutAnimation，那么目前还需要在`UIManager`中启用：

```
UIManager.setLayoutAnimationEnabledExperimental && UIManager.setLayoutAnimationEnabledExperimental(true);
```

务必在卸载组件前清除定时器

> 什么时候使用setNativeProps呢？在（不得不）频繁刷新而又遇到了性能瓶颈的时候。
>
> 直接操作组件并不是应该经常使用的工具。一般来说只是用来创建连续的动画，同时避免渲染组件结构和同步太多视图变化所带来的大量开销。`setNativeProps`是一个“简单粗暴”的方法，它直接在底层（DOM、UIView等）而不是React组件中记录state，这样会使代码逻辑难以理清。所以在使用这个方法之前，请尽量先尝试用`setState`和shouldComponentUpdate方法来解决问题。
>
> 避免和render方法的冲突
>
> 如果要更新一个由render方法来维护的属性，则可能会碰到一些出人意料的bug。因为每一次组件重新渲染都可能引起属性变化，这样一来，之前通过`setNativeProps`所设定的值就被完全忽略和覆盖掉了。
>
> setNativeProps与shouldComponentUpdate
>
> 通过巧妙运用 `shouldComponentUpdate`方法，可以避免重新渲染那些实际没有变化的子组件所带来的额外开销，此时使用`setState`的性能已经可以与`setNativeProps`相媲美了。

RN性能优化：http://reactnative.cn/docs/0.46/performance.html#content

特定平台：1.ios.和.android. 2 Platform.select() 3 Platform.OS === 'ios'

# 2017-07-20

CSS预处理使用情况：

antd / antd-mobile: less

iview: less

element-ui: bootstrap

---

**JavaScript**

限制小数位数：toFixed(/* 0~20 */)

# 2017-07-21

**设计**

RN中单位为dp

1pt= (DPI / 72) px：在PS中设置画布ppi为72时pt=px

1dp在160ppi时等于1px

| 密度     | 密度值  | 代表分辨率     | px -> dp | dp -> px |
| ------ | ---- | --------- | -------- | -------- |
| ldpi   | 120  | 240*320   | 1.33     | 0.75     |
| mdpi   | 160  | 320*480   | 1        | 1        |
| hdpi   | 240  | 480*800   | 0.67     | 1.5      |
| xhdpi  | 320  | 720*1280  | 0.5      | 2        |
| xxhdpi | 480  | 1080*1920 | 0.33     | 3        |

Android尺寸规范

字体

MD推荐12/14/16/20/34字体排版缩放

| 类型        | 大小    | 透明度（黑） |
| --------- | ----- | ------ |
| display 4 | 112 l | 54     |
| display 3 | 56 r  | 54     |
| display 2 | 45 r  | 54     |
| display 1 | 34 r  | 54     |
| headline  | 24 r  | 87     |
| title     | 20 m  | 87     |
| subhead   | 16 r  | 87     |
| body 2    | 14 m  | 87     |
| body 1    | 14 r  | 87     |
| caption   | 12 r  | 54     |
| menu      | 14 m  | 87     |
| button    | 14 m  | 87     |

图标：24dp

间隔网格：8dp，文字：4dp

参考：

​	状态栏：24dp

​	Navigation：56/64dp

​	tabbar：48dp

​	边距：16dp

​	item：72dp

​	细边距：8dp

​	底部动作条：item：48dp

​	悬浮按钮：56dp，内容24dp，至少放在距边缘16dp以内，弹出3-6个

​	迷你悬浮按钮：40dp，内容24dp

​	扁平按钮：88dp*36dp

​	

触摸目标最小尺寸是48dp

卡片布局准则

卡片圆角2dp

字体设计
正文：14 sp 或 16 sp
标题：24 sp 或更大
第 6 章 组件 | 403
扁平按钮：Roboto Medium, 14 sp, 10 sp 字间距
移动设备上的卡片间距
屏幕边界与卡片间留白：8 dp
卡片间留白：8 dp
内容留白
16 dp



网格列表表头/表尾（header/footers）
单行表头/表尾
高： 48dp
文本内边距： 16dp
默认字体大小： 16sp
次要动作与尾右对齐
两行表头/表尾
高： 68dp
文本内边距： 16dp
每行的默认字体大小： 16sp/12sp或者14sp/14sp

# 2017-07-24

**Vue**

Vue中可注册全局过滤器，仅在{{}}和v-bind中可用

# 2017-07-24

移动阅读时代，markdown的格式不宜嵌套过深，一般同一内容只宜使用一种格式（无序列表、有序列表、代码），尽量flat，以适应手机ListView式的阅读

文章链接发布到聚合网站尽量在工作日早晨，因为白天人们习惯使用PC网页浏览，晚上习惯使用手机APP，PC的链接直接跳转到源文章，方便转化，而手机APP只会打开webview，不能跳转到源文章APP，不好转化

**Echarts**

echarts的init方法要传入的是唯一的元素，官方推荐的getElementById就是这个目的，但不一定必须使用这个方法，vue中可用this.$el（此组件挂载的元素）或ref/this.refs.（内部子元素）来指定

# 2017-07-27

**Vue**

为了发现对象内部值的变化，可以在选项参数中指定 `deep: true` 。注意监听数组的变动不需要这么做。

```
vm.$watch('someObject', callback, {
  deep: true
})
vm.someObject.nestedValue = 123
// callback is fired
```

---

计算属性返回如果是一个对象，重新计算后将返回一个新的对象，watch它时无需deep

**JavaScript**

splice删除一个元素后，数组length

箭头函数与this：

- 箭头函数根本没有自己的`this`，导致内部的`this`就是定义时外层代码块的`this`
- 由于箭头函数没有自己的`this`，所以当然也就不能用`call()`、`apply()`、`bind()`这些方法去改变`this`的指向，
- 所以也不能做构造函数

# 2017-07-28

**Node**

require() 执行会将对应文件内的脚本都执行一遍

# 2017-07-29

**CSS**

选择器优先级：

!important > # > . > 标签 > *

不同选择器的优先级与先后无关

设置的样式高于继承

# 2017-07-30

**CSS**

伪类p:first-child指的是作为p元素的且是第一个子元素

伪类：假想给该元素添加一个类名 :link :hover

伪元素：假想给该元素某部分添加元素标签，并应用样式 :first-letter :first-line :before :after