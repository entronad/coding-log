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

**架构**

# 2017-05-06

**vue**

- Vue 实例可以认为是 ViewModel，常用 vm 作为变量名
- Vue 中的 data 对象为代理，类似于引用赋值


# 2017-05-08

**vue**

- 组件中的data需定义为函数，且返回一个新的data对象

- 父子组件的通讯

  > props down, events up


# 2017-05-10

**vue **

element-ui 中 NavMenu 导航菜单中若在` <el-menu/>`中设置 router 参数，则其中`<el-menu-item/>`的 index 参数值即为路由地址

**git**

添加密钥到ssh中时，为防止报

> Could not open a connection to your authentication agent

的错误需用以下命令：

```
eval `ssh-agent -s`
ssh-add
```
# 2017-05-11

**css**

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

**css**

`box-shadow`属性：向框添加阴影

```
box-shadow: insert h-shadow v-shadow blur spread color;
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

> 逗号为或
>
> 紧贴为且
>
> 空格为子

以上为同类，若元素+类则为具有此类的元素

**vue**

component 类似“类”的概念，名称、文件名大写

------

`<template>` 中的根标签要缩进，`<sctipt>`、`<style>` 中的内容不缩进

# 2017-05-14

**css**

`top`、`right`、`bottom`、`left` 属性定义与各边边距

# 2017-05-15

**vue**

父组件通过事件接受子组件参数时，绑定处只要写函数名，参数会自动传入函数中

---

**css**

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

**css**

`line-height: 1.5`  和 `line-height: 150%`  的区别区别体现在子元素继承时，如下：

- 父元素设置line-height:1.5会直接继承给子元素，子元素根据自己的font-size再去计算子元素自己的line-height。
- 父元素设置line-height:150%是计算好了line-height值，然后把这个计算值给子元素继承，子元素继承拿到的就是最终的值了。此时子元素设置font-size就对其line-height无影响了。

# 2017-05-17

**vue**

组件的 `<style>` 如果加了scope属性，则其子组件也无法继承这些样式

---

**html**

`<table>` 表格

`<tr>` 行

`<th>` 表头项

`<td>` 内容项

---

**css**

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

**vue**

事件处理器参数可为：

- JavaScript 代码：`@click="counter += 1"`

- 方法：`@click="greet"`

- 内联处理器方法：`@click="say('what')"`

  其中内联语句处理器中访问原生 DOM 事件。可以用特殊变量 `$event` 把它传入方法

   `$event` 为`this.$emit('click', value)`中的第二个参数value（$emit只有两个参数）

# 2017-05-18

**vue**

props 中的参数，子组件中无权修改，只有 $emit 事件通知父组件修改

---

vue 中引入 axios 分两种情况，组件中通过原型链引入，vuex 中直接引入，两者相互独立

# 2017-05-19

**vue**

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

**css**

通过`margin: 0 auto;`设置居中需设置 width 值

# 2017-05-23

**vue**

当<style>标签设置scoped属性后，将在该标签里的类名添加后缀以区别

**css**

宽高的百分比是在减去padding之后，无需考虑滚动条

# 2017-05-24

**vue**

尝试在`actions`里面`commit`另一个`mutation`，而不是在`mutation`里调用另一个`mutation`方法。

---

状态中的数据来源如是后端api，网络请求应当放在action中

# 2017-05-25

**javascript**

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

**vue**

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

**css**

margin 的 auto 为“浏览器设置的外边距”，左右会自动居中，但上下为0，故可通过`margin: 0 auto;`设置水平居中，但不可`margin: auto 0;`设置垂直居中。

---

高度首先要比较父元素设定z-index之后确定的 stacking context，同一stacking context再进行比较

z-index仅对**定位元素**有效（定位元素：不是static，而是relative, absolute, fixed）

**vue**

Vue 中引入JS库的最佳实践：以插件的形式引入

---

iview组件阻断了原生的事件，且无法接受捕捉与冒泡的事件

# 2017-05-27

**vue**

不应该对 data 属性使用箭头函数，不应该使用箭头函数来定义computed, methods, watch, 生命周期钩子中的函数。这是因为这些属性将被混入到 Vue 实例中。所有 的 this 上下文自动地绑定为 Vue 实例。而箭头函数绑定了父上下文，因此 `this` 与你期待的 Vue 实例不同。

---

state 在组件中通过computed引用

**html**

localStorage中只可存储字符串，如存入对象，需用JSON.stringfy()，取出对象需用JSON.parse()

取出对象字符串在parse前需判断对象字符串是否存在

# 2017-05-31

**vue**

在Vue组件中定义的函数都不该用箭头函数，因为其中的this需与运行时的调用对象——Vue实例绑定，而其中若要定义函数则需使用箭头函数，以与其定义时，即Vue对象的运行时的调用对象——Vue实例绑定

---

v-bind:class 参数对象中的变量名需加引号

# 2017-06-01

**vue**

vue中父组件调用子组件的方法：

```
<child1 ref="child1"></child1>

this.$refs.child1.handleParentClick("ssss")
```

# 2017-06-03

**vue**

iview中menu组件的active-name属性并不是与当前选项双向绑定，只决定初始选项，或通过updateActiveName手动更新当前选项

**html**

HTML的属性分为两种：content attribute 和IDL attribute

content attribute即标签里的设置的属性，它必是字符串

IDL attribute即JavaScript DOM对象的属性

这两者的关联尽可能的developer-friendly，不过有时会很奇怪

https://developer.mozilla.org/zh-CN/docs/Web/HTML/Attributes

# 2017-06-06

**vue**

初始化逻辑不可直接写在script标签中，需写在钩子中，beforeMount钩子中还没有dom

---

不同组件内的标签id，也要是全局唯一的

# 2017-06-10

**browser**

```
webkit内核
+---safari
+---chrome
+---chromium (改造为blink内核)
+---mobile webviews
```
**vue**
webpack打包的index.html中，所引用的文件目录都是绝对路径，起点为站点的根"/"，如作为webapp，需改为相对目录

---

把根目录下`config/index.js`中的`productionSourceMap: true`改为`false`可不打包map文件，减小目标文件体积

# 2017-06-12

**css**

background-size属性必须在background属性之后，且在同一个class中定义

**vue**

在data中的变量定义时不可引用data中的其他变量，因为此时data还没生成

# 2017-06-13

**vue**

Tip: built files are meant to be served over an HTTP server.
  Opening index.html over file:// won't work.

**静态直读不可用history模式**

**css**

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

**vue**

vue-router 有时候，同一个路径可以匹配多个路由，此时，匹配的优先级就按照路由的定义顺序：谁先定义的，谁的优先级就最高。

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

**react**

组件名称必须以大写字母开头

组件的返回值只能有一个根元素

React 元素的事件处理和 DOM元素的很相似。但是有一点语法上的不同:

- React事件绑定属性的命名采用驼峰式写法，而不是小写。
- 如果采用 JSX 的语法你需要传入一个函数作为事件处理函数，而不是一个字符串(DOM元素的写法)

**javascript**

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

**javascript**

obj.a == null可同时起到obj.a === null与obj.a === undefined作用

# 2017-07-06

**dom**

addEventListener的回调函数中添加e.preventDefault()阻止默认行为，比如a标签的跳转

---

DOM0级事件：通过标签内或onclick = 的方式定义的事件；DOM0级事件只能存在一个，后面的会覆盖前面的；DOM0级事件方法被认为属于元素作用域，this绑定元素

DOM2级事件：通过addEventListener()添加的事件，DOM2级事件多个可以共存，可以与DOM0级事件共存。只有DOM2级事件有事件流；removeEventListener()参数与addEventListener()相同，故要能移除，回调函数需具名；第三个参数，是否是捕获时触发

DOM3级事件：内容和验证上更多的扩展

# 2017-07-07

**webpack**

脚本流程：rm删除dist/static下的所有文件，执行webpack(config, callback)

# 2017-07-08

**dom**

<html>可通过document.documentElement快捷访问，等价于

document.childNode[0]

document.firstChild

<body>可通过document.body快捷访问

**webpack**

webpack-dev-server和webpack-dev-middleware打包的结果是在内存中

# 2017-07-09

**html**

元素的布尔属性，只要出现，不管值为什么表示true，不出现为false，不可用true/false赋值，以前习惯用同名值

HTML5规定：

> The presence of a boolean attribute on an element represents the true value, and the absence of the attribute represents the false value.
>
> If the attribute is present, its value must either be the empty string or a value that is an ASCII case-insensitive match for the attribute’s canonical name, with no leading or trailing whitespace.
>
> The values “true” and “false” are not allowed on boolean attributes. To represent a false value, the attribute has to be omitted altogether.

# 2017-07-10

**html**

标签语义化

> 方便开发维护
>
> 更好的SEO
>
> 无CSS时能呈现
>
> 利于浏览器加载

# 2017-07-11

**javascript**

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

**vue**

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

**css**

CSS预处理使用情况：

antd / antd-mobile: less

iview: less

element-ui: bootstrap

---

**javascript**

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

**vue**

Vue中可注册全局过滤器，仅在{{}}和v-bind中可用

# 2017-07-24

**markdown**

移动阅读时代，markdown的格式不宜嵌套过深，一般同一内容只宜使用一种格式（无序列表、有序列表、代码），尽量flat，以适应手机ListView式的阅读

文章链接发布到聚合网站尽量在工作日早晨，因为白天人们习惯使用PC网页浏览，晚上习惯使用手机APP，PC的链接直接跳转到源文章，方便转化，而手机APP只会打开webview，不能跳转到源文章APP，不好转化

**echarts**

echarts的init方法要传入的是唯一的元素，官方推荐的getElementById就是这个目的，但不一定必须使用这个方法，vue中可用this.$el（此组件挂载的元素）或ref/this.refs.（内部子元素）来指定

# 2017-07-27

**vue**

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

**javascript**

splice删除一个元素后，数组length

箭头函数与this：

- 箭头函数根本没有自己的`this`，导致内部的`this`就是定义时外层代码块的`this`
- 由于箭头函数没有自己的`this`，所以当然也就不能用`call()`、`apply()`、`bind()`这些方法去改变`this`的指向，
- 所以也不能做构造函数

# 2017-07-28

**node**

require() 执行会将对应文件内的脚本都执行一遍

# 2017-07-29

**css**

选择器优先级：

!important > # > . > 标签 > *

不同选择器的优先级与先后无关

设置的样式高于继承

# 2017-07-30

**css**

伪类p:first-child指的是作为p元素的且是第一个子元素

伪类：假想给该元素添加一个类名 :link :hover

伪元素：假想给该元素某部分添加元素标签，并应用样式 :first-letter :first-line :before :after

# 2017-07-31

**http**

仅有POST、PUT以及PATCH这三个动词时会包含请求体，而GET、HEAD、DELETE、CONNECT、TRACE、OPTIONS这几个动词时不包含请求体。

关于GET等与请求体的关系：

HTTP协议不限制你携带请求体，但严格符合协议的server是不应该处理这个请求体的，也就是说可以带，但带了没意义

> Yes. In other words, any HTTP request message is allowed to contain a message body, and thus must parse messages with that in mind. Server semantics for GET, however, are restricted such that a body, if any, has no semantic meaning to the request. The requirements on parsing are separate from the requirements on method semantics.
>
> So, yes, you can send a body with GET, and no, it is never useful to do so.
>
> This is part of the layered design of HTTP/1.1 that will become clear again once the spec is partitioned (work in progress).
>
> ​    ——HTTP 规范的主要创作人之一 Roy T. Fielding
>
# 2017-08-01


**vue**

iview size默认值是'default'

---

```
<input v-model="something">
```

这不过是以下示例的语法糖：

```
<input
  v-bind:value="something"
  v-on:input="something = $event.target.value">
```

所以要让组件的 `v-model` 生效，它应该 (在 2.2.0+ 这是可配置的)：

- 接受一个 `value` 属性
- 在有新的值时触发 `input` 事件

自定义事件$emit 到 v-on 的参数传递：emit的arg[1],arg[2]...直接传到handler的arg[0],arg[1]...

在监听原生 DOM 事件时，方法以事件为唯一的参数。如果使用内联语句，语句可以访问一个 `$event` 属性： `v-on:click="handle('ok', $event)"`

---

对于多数特性来说，传递给组件的值会覆盖组件本身设定的值。即例如传递 `type="large"`将会覆盖 `type="date"` 且有可能破坏该组件！索性我们对待 `class` 和 `style` 特性会更聪明一些，这两个特性的值都会做合并 (merge) 操作，让最终生成的值为：`form-control date-picker-theme-dark`。

---

**javascript**

String的三个子串方法slice(), substr(), substring(): 第一个参数都是起始位置（左闭）

slice(),  第二个参数是结束位置（右开）；负数第一个第二个都将与长度相加

substring() 第二个参数是结束位置（右开）；负数第一个与长度相加，第二个转换为0

substr()第二个参数是长度 ；负数第一个第二个都转换为0

# 2017-08-02

**vue**

ie浏览器无法使用es6等新特性，需使用babel-polyfill

```
npm install --save babel-polyfill
```

```
import "babel-polyfill" //在main.js中
```

```
module.exports = {
  entry: ["babel-polyfill", "./app/js"] //在webpack.config.js中
};
```
# 2017-08-04

**javascript**

delete 操作符：从对象中移除某属性，后面跟这个引用

- 一般都返回true，包括对象中没有这个属性，只有属性configurable: false时不能删除，返回false
- 只会删除自身的属性，不会删除原型链上的属性
- 不能删除全局/局部作用域中的变量、函数（他们的configurable: false）

---

数组的堆栈方法，都不是链式的方式，进（push，unshift）返回长度，出（pop，shift）返回出的项

unshift方法多个参数时，完成的顺序与参数原顺序一致（整体推入）

# 2017-08-06

**javascript**

#### 1. TC39

TC39（Technical Committee 39）是一个推动JavaScript发展的委员会。
它的成员由各个主流浏览器厂商的代表构成。
会议的每一项决议必须大部分人赞同，并且没有人强烈反对才可以通过。
因为，对成员来说，同意就意味着有责任去实现它。

#### 2. Stage

每一项新特性，要最终纳入ECMAScript规范中，TC39拟定了一个处理过程，称为TC39 process。
其中共包含5个阶段，Stage 0 ~ Stage 4。

**Stage 0: strawman**
一种推进ECMAScript发展的自由形式，任何TC39成员，或者注册为TC39贡献者的会员，都可以提交。

**Stage 1: proposal**
该阶段产生一个正式的提案。
（1）确定一个**带头人**来负责该提案，带头人或者联合带头人必须是TC39的成员。
（2）描述清楚要解决的问题，解决方案中必须包含例子，API以及关于相关的语义和算法。
（3）潜在问题也应该指出来，例如与其他特性的关系，实现它所面临的挑战。
（4）polyfill和demo也是必要的。

**Stage 2: draft**
草案是规范的第一个版本，与最终标准中包含的特性不会有太大差别。
草案之后，原则上只接受增量修改。
（1）草案中包含新增特性语法和语义的，尽可能的完善的形式说明，允许包含一些待办事项或者占位符。
（2）必须包含**2个实验性的具体实现**，其中一个可以是用转译器实现的，例如Babel。

**Stage 3: candidate**
候选阶段，获得具体实现和用户的反馈。
此后，只有在实现和使用过程中出现了重大问题才会修改。
（1）规范文档必须是完整的，评审人和ECMAScript的编辑要在规范上签字。
（2）至少要有**两个符合规范的具体实现**。

**Stage 4: finished**
已经准备就绪，该特性会出现在年度发布的规范之中。
（1）通过[Test 262](http://test262.ecmascript.org/)的**验收测试**。
（2）有2个通过测试的实现，以获取使用过程中的重要实践经验。
（3）ECMAScript的编辑必须规范上的签字。

# 2017-08-08

**css**

相同特殊性需要通过层叠实现效果的例子：

超链接的LVHA顺序声明：

```
:link {color: blue;}
:visited {color: purple;}
:hover {color: red;}
:active {color: orange}
```

---

em: 设置长度时为当前元素font-size的大小，设置font-size时为父元素font-size的大小

---

在CSS中，相对URL要相对于样式表本身，而不是使用CSS的html（主要针对跨域）

---

font-family: 指定到具体字体太复杂了不现实，所以css只指定到字体族

# 2017-08-09

**css**

font-weigt是可继承的，是相对的在100-900上

---

垂直对齐文本 vertical-align 只能应用于行内元素和替换元素

vertical-align: middle; 会把行内元素框的中点与父元素基线上方0.25em处对齐

---

内容的背景也会应用到padding，padding不可为负，margin可以为负

width、margin可以为auto，其他默认为0

margin、padding、width加起来要是父元素的width（与父元素padding无关），百分百的值是相对于父元素的width

过量设定后，margin-right将是自动计算值

# 2017-08-10

**css**

垂直方向上的margin会合并，嵌套元素的margin也会合并

当margin有负数时，一正一负合并，正的会减去负的绝对值；两个负的合并，绝对值会取大的

---

替换元素：img

非替换元素

# 2017-08-12

**react**

组件类中的方法不会自动绑定对象，可用属性初始化器语法：

```
class LoggingButton extends React.Component {
  // This syntax ensures `this` is bound within handleClick.
  // Warning: this is *experimental* syntax.
  handleClick = () => {
    console.log('this is:', this);
  }

  render() {
    return (
      <button onClick={this.handleClick}>
        Click me
      </button>
    );
  }
}
```

# 2017-08-15

**css**

替换元素：<img>、<input>、<textarea>、<select>、<object>

line-height最好的办法是设置原始数字值，这将成为一个缩放因子

行内元素的边框边界由font-size而不是line-height控制

inline-block外部类似替换行内元素，内部类似块元素(行内非替换元素不可设置宽高)

如果一个元素为绝对定位，float为none，display将用计算值：block

行内非替换元素的左右内边距有效

# 2017-08-16

**css**

浮动元素的margin不会合并

浮动非替换元素必须申明width

包含块（containing block）：浮动元素的包含块是其最近的块级祖先元素

浮动元素会自动变成块级框

---

position: relative原本所占的空间仍保留

position: absolute会变为块级框

包含块：

​	HTML的根元素是html元素，其包含块是视窗大小的矩形

​	static/relative包含块由最近的块级框、行内块祖先元素构成

​	absolute包含块为最近的不是static的祖先元素（即一般是absolute或relative，由于absolute本身要求相同，所以一般会要设一个relative），如果是块级元素，则为border，即包含padding；行内元素则为内容边界

！！！设置top等偏移属性值为百分比时，相对于的是包含块，即static时是块级框，absolute时是border框

width/height属性优先级高于top等，设置冗余了优先满足width等

# 2017-08-17

**css**

对于absolute元素来说，left设为auto，将往左边顶，top设为auto将会为其文档流中的位置

替换元素的width、height若设为auto，将自动计算为图片的大小

z-index中存在叠放上下文，概念与父子元素类似

# 2017-08-18

**javascript**

```
let { foo: baz } = { foo: "aaa", bar: "bbb" };
baz // "aaa"
foo // error: foo is not defined

```

上面代码中，`foo`是匹配的模式，`baz`才是变量。真正被赋值的是变量`baz`，而不是模式`foo`。

如果要将一个已经声明的变量用于解构赋值，必须非常小心。

```
// 错误的写法
let x;
{x} = {x: 1};
// SyntaxError: syntax error

```

上面代码的写法会报错，因为 JavaScript 引擎会将`{x}`理解成一个代码块，从而发生语法错误。只有不将大括号写在行首，避免 JavaScript 将其解释为代码块，才能解决这个问题。

```
// 正确的写法
let x;
({x} = {x: 1});
```

由于数组本质是特殊的对象，因此可以对数组进行对象属性的解构。

```
let arr = [1, 2, 3];
let {0 : first, [arr.length - 1] : last} = arr;
first // 1
last // 3

```

上面代码对数组进行对象解构。数组`arr`的`0`键对应的值是`1`，`[arr.length - 1]`就是`2`键，对应的值是`3`。

只要有可能，就不要在模式中放置圆括号。

---

rest运算符：

函数的arguments对象只是一个类似数组的对象，不是Array实例，没有Array的实例方法，但可以用[]取值，有length

rest对象则就是数组，后面不能有参数。函数的`length`属性，不包括 rest 参数。

对象的扩展运算符使用时，总是后面的覆盖前面的

# 2017-08-23

**javascript**

JSON 键必须加双引号，字符串要用双引号，最外面要有大括号或方括号

---

escape character : 转义字符

# 2017-08-24

**mobx**

mobx-react在ReactNative中是通过"mobx-react/native"引入

# 2017-08-25

**react-native**

```
AppRegistry.registerComponent('项目名',() => ...);
```

与./ios/项目名/appDelegate.m中的

```
RCTRootView*rootView = [[RCTRootViewalloc]initWithBundleURL:jsCodeLocation
moduleName:@"项目名" launchOptions:launchOptions];
```

或是./android/app/src/main/java/com/项目名/MainActivity.java中的

```
mReactRootView.startReactApplication(mReactInstanceManager, "项目名", null);
```

必须保持一致

# 2017-08-26

**javascript**

class中的变量需这样定义：

```
class MyClass {
  a = 12;
  static b = 12;
}
```

# 2017-09-03

**mobx**

observable store在根组件处通过Providerobserver 组件

一般会在入口文件进行初始化

`observer` 是由单独的 `mobx-react` 包提供的

# 2017-09-05

**mobx**

store 先定义calss，然后在同一个文件中new实例，输出实例，文件名和实例名小写

只要确定该网络请求是更新数据的唯一方法，可将网络请求写在action中，但store中不放“自动逻辑”

**javascript**

类中用等号定义的是类的“实例属性”，用此方法定义的方法（foo = () => {}）将自动与“类的实例”（React组件）绑定

---

- 函数声明
  `async function foo () {}`
- 函数表达式
  `const foo = async function () {}`
- 方法定义
  `const obj = { async foo () {} }`
- 箭头函数
  `async () => {}`

# 2017-09-08

**react**

ref添加到Compoennt上获取的是Compoennt实例，添加到原生HTML上获取的是DOM

新版本的React已经不推荐我们使用ref string转而使用ref callback

在说ReactDOM.findDOMNode，当参数是DOM，返回值就是该DOM（这个没啥卵用）；当参数是Component获取的是该Component render方法中的DOM

# 2017-09-11

**javascript**

类、对象中的访问器可通过关键字set、get定义

# 2017-09-12

**react**

react组件的内容分发（slot）通过props实现

JSX中的注释也要写到大括号中

需要直接插入html需用属性dangerouslySetInnerHTML={{__html: myHTML}}

---

初始化时钩子顺序：

constructor
componentWillMount
render
componentDidMount

---

虚拟DOM、diff算法使得每次render的时候只会更改必要的元素

---

css-in-js会被转换为内联样式

# 2017-09-19

**javascript**

在import语句中，同级没有同名但后缀名不同的文件可省略后缀，或.js可省略

**babel**

preset：

env: 已进入规范的特性

stage3-0:尚未进入规范（stage4）各阶段提案，每个包含前面所有

react：react要用的

其他要用的靠plugins补充

react-app包括es2015，stage2，react

# 2017-09-21

**css**

水平居中垂直居中

1.

```
// 父元素宽高要确定
margin: 0 auto; /*水平居中*/
position: relative;
top: 50%; /*偏移*/
transform: translateY(-50%);
```

2.

```
// 父元素中：
display: flex;
align-items: center; /*定义body的元素垂直居中*/
justify-content: center; /*定义body的里的元素水平居中*/
```

# 2017-09-22

**javascript**

Module 是尽量静态化，使得编译时就能确定模块的依赖关系，以及输入和输出的变量。CommonJS 和AMD 是动态的。

`import`语句会执行所加载的模块。

如果多次重复执行同一句`import`语句，那么只会执行一次，而不会执行多次。

采用default输出的变量，import时无需知道其名字，import后面（不加大括号）跟的是别名，

```
import _, { each, each as forEach } from 'lodash';
```

可同时引入export的变量和export default。

```
export { es6 as default } from './someModule';

// 等同于
import { es6 } from './someModule';
export default es6;
```

**css**

子元素的margin-top会顶开父元素的margin-top，解决办法给父元素加1px的padding。

要想margin auto水平居中，width必须是定值。

class的覆盖顺序是按样式表中的定义的顺序来的，而不是元素中定义的顺序

# 2017-09-24

**styled-components**

sc与antd

只要有import就会执行

执行过程中用到才会加载

sc首次用到生成style sheet，之后的都是填到其中，antd有用到就会生成类

加载：只有当jsx中出现了该元素才会加载

# 2017-09-27

**css**

inline 行内元素 宽高无效。
margin padding只有左右边距有效，上下无效。

**react**

React构造函数和其中的super都应当传入props。

React组件的构造函数将会在装配之前被调用。当为一个`React.Component`子类定义构造函数时，你应该在任何其他的表达式之前调用`super(props)`。否则，`this.props`在构造函数中将是未定义，并可能引发异常。

# 2017-09-28

**styled-components**

其本质是将生成的样式的class以calssName为名的参数传给组件，故组件中根元素需加入className={this.props.className}

# 2017-09-29

**javascript**

由于大括号被解释为代码块，所以如果箭头函数直接返回一个对象，必须在对象外面加上括号。

# 2017-09-30

**react**

组件内部使用的逻辑，以绑定方法的形式定义在类中

# 2017-10-02

**http**

跨域资源共享中，预请求之后的每次请求，response中也必须添加头Access-Control-Allow-Origin

# 2017-10-03

**react**

this.props.history.push 要使用必须在 Route标签中，否则就要通过history={this.props.history}传递一下

# 2017-10-06

**react**

React中元素的事件处理需传递一个方法，第一个参数为e

---

styled-components通过传入参数确定的CSS属性不能实现动态修改

给styled-components包裹的根元素添加ref要用innerRef

# 2017-10-10

**mobx**

observable 之后的Array不是Array，但是具有Array的方法，可以用slice()转变为真Array

装饰器要先inject，后observer

**react**

单纯的props改变并不会触发组件更新，只有父组件重新渲染会触发子组件更新

ref不要重新赋值，设个新的变量

# 2017-10-12

**react**

子组件向父组件传递参数（修改父组件参数），是以父组件将函数传递给子组件的形式

# 2017-10-13

**javascript**

异常向外抛出时，只要在某一层捕获就行了（不一定当场捕获），一直没有捕获程序就会中断

**http**

如果后端要求 application/x-www-form-urlencoded 格式的Post请求体，可采用

```
var params = new URLSearchParams();
params.append('param1', 'value1');
params.append('param2', 'value2');
axios.post('/foo', params);
```

# 2017-10-14

**mobx**

Observable Object 不适用于有原型的对象，也无法监视键的增减，要监视键的增减用Map

---

当 `observer` 需要组合其它装饰器或高阶组件时，请确保 `observer` 是最深处(第一个应用)的装饰器，否则它可能什么都不做。

**javascript**

只要捕获了异常，之后的语句照常执行；

而finally中的语句将“一定”被执行，哪怕在try、catch中return了。

---

decorator 只可修饰类和类的属性，不可修饰函数（因为存在变量提升）

---

`Object.assign()` 方法用于将所有可枚举属性的值从一个或多个源对象复制到目标对象。它将返回目标对象。

# 2017-10-17

**css**

currentColor 可作为属性值使用

```
hr {
  height: .5em;
  background: currentColor;
}
```

---

合成属性 background 包含：

- [`background-image`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-image): `none`
- [`background-position`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-position): `0% 0%`
- [`background-size`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-size): `auto auto`
- [`background-repeat`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-repeat): `repeat`
- [`background-origin`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-origin): `padding-box`
- [`background-clip`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-clip): `border-box`
- [`background-attachment`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-attachment): `scroll`
- [`background-color`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-color): `transparent`

---

默认时（background-clip: border-box）border会被放置在background之上，设置background-clip: padding-box时border会被放置在padding上

---

box-shadow 中的spread是指不模糊的范围，可用以设置多重边框

---

条纹背景可以通过linear-gradient与background-size配合实现

---

当任意两个相邻圆角的半径之和超过border box 的尺寸时，用户代理必须按比例减小各个边框半径所使用的值，直到它们不会相互重叠为止

border-radius可单独设置水平半径、垂直半径，并可用百分百：

```
border-radius: 50% / 50%;
```

---

对元素使用了3D变形之后，其内部的变形效应是“不可逆转”的

---

使用高斯模糊算法（或类似算法）进行模糊处理，在阴影边缘发生阴影色和纯透明色之间的颜色过渡长度近似于模糊半径的两倍

# 2017-10-18

**css**

在代码标签中，可控制tab 的宽度

```
pre {
	tab-size: 2;
}
```

---

可以隐藏光标：

```
cursor: none;
```

**javascript**

delete: 从对象中删除某个属性，操作数为对象某个属性的引用

---

类的实例属性：用等号定义，通过对象实例的this调用，相当于在constructor中用this定义

类的静态属性：用static和等号定义，通过类名.调用

# 2017-10-19

**css**

```
figure {
  width: min-content;
  margin: auto;
}
```

min-content 这个关键字将解析为这个容器内部最大的不可断行元素的宽度（即最宽的单词、图片或具有固定宽度的盒元素）

---

\<table> 会自动根据内容跳转列宽，也可通过设置table-layout调整布局方式：

```
table {
	table-layout: fixed;
	width: 100%;
}
```

---

margin 的百分比值是以父元素的宽度作为解析基准的。没错，即使对于margin-top 和margin-bottom 来说也是这样！

---

内容长度变化页脚固定底部可使用flex设置：

```
body {
	display: flex;
	flex-flow: column;
	min-height: 100vh;
}
main { flex: 1; }
```

---

可以使用max-width来处理需要压缩的宽度

# 2017-10-20

**javascript**

引用类的静态属性时，要用类名. 不能用 this.

# 2017-10-25

**react-native**

\<View> 标签内部不可以直接添加字符串

# 2017-10-16

**react-native**

react-navigation 中navigationOptions不仅可以设给screen，还可以设给嵌套路由中的子路由，以应用到该子路由中所有的screen

---

**redux**

大部分的组件都应该是展示型的，但一般需要少数的几个容器组件把它们和 Redux store 连接起来。

# 2017-10-16

**react**

直接在jsx中给onClick赋值匿名箭头函数的方式并不推荐，因为每次都会生成新副本，且引起不必要的重新渲染

---

生命周期方法中该做的：

constructor：初始化state，因为它是第一个执行的，且后续生命周期方法都有可能用到state

render：对于不需要渲染视图的组件，返回null或false

componentWillMount：基本不用用到，render之前要做的事放到constructor中。但是在SSR中只有他没有componentDidMount

componentDidMount：由于render只是返回jsx，实际渲染react会在综合考虑父子组件后统一渲染，故componentDidMount不一定总是紧贴render执行；他其中可以放心使用DOM了。

componentWillReceiveProps：任何父组件更新引起的更新都会调用它因此有必要在其中对比nextProps与this.props不一致才执行需要的setState；state变化引起的更新不会调用它（否则其中的setState就会引起循环调用了）。

shouldComponentUpdate：通过重写该函数可避免不必要的重新渲染，提高性能；在执行this.setState之后this.state不会立即重设，故可进行nextState和shis.state的对比。

componentDidUpdate：和mount不同，此方法在SSR中也会调用（良好的设计中，SSR不应该有更新）

componentWillUnmount：在componentDidMount中用非React方法创造的DOM元素要在此处理，否则会内存泄露。  

# 2017-10-30

**react**

`this.props.children` 的值有三种可能：如果当前组件没有子节点，它就是 `undefined` ;如果有一个子节点，数据类型是 `object` ；如果有多个子节点，数据类型就是 `array` 。

在React.Children中提供了map等一些列方法处理this.props.children而不用担心它是什么类型

---

网络请求适宜放在componentDidMount中还有一个原因是ssr中无此函数，正好可省去无意义的请求

**fetch**

fetch().then() 中还不可直接读取response中的内容，因为fetch在接受到http报头部分就会调用then，不会等到整个响应完成，所以要继续用response.json().then()

**javascript**

thunk是一个计算机编程中的术语，表示辅助调用另一个子程序（设为g）时，被调用的那个子程序g。

# 2017-11-02

**fetch**

当接收到一个代表错误的 HTTP 状态码时，从 `fetch()`返回的 Promise **不会被标记为 reject，** 即使该 HTTP 响应的状态码是 404 或 500。相反，它会将 Promise 状态标记为 resolve （但是会将 reolve 的返回值的 ok 属性设置为 false ），  仅当网络故障时或请求被阻止时，才会标记为 reject。

# 2017-11-03

**架构**

错误处理需要考虑的问题：

- 错误处理是进行纠正还是仅仅进行检测
- 错误检测是主动的还是被动的
- 程序如何传播错误
- 错误消息的处理有什么约定
- 如何处理异常
- 在程序中，在什么层次上处理错误
- 每个类在验证其输入数据的有效性方面需要负何种责任
- 你是希望用运行环境中内建的错误处理机制，还是想建立自己的一套机制

---

常见容错策略：

- 系统在监测到错误的时候退回去，再试一次
- 系统拥有一套辅助代码，以备在主代码出错的时候使用
- 系统使用一种表决算法。
- 系统使用某个不会对系统其余部分产生危害的虚假值代替这个错误的值
- 在遇到错误的时候，让系统转入某种“部分运转”的状态，或者转入某种“功能退化”的状态
- 系统可以自动关闭或重启

---

设计中的两个原则：

高扇入（high fan-in）：让大量的类使用某个特定的类；

低扇出（low fan-out）：让一个类里少量或适中地使用其他的类；

---

无环图（acyclic graph）原则：

以子系统为节点，相互间的通信为边的图，应当是无环图，换句话说，程序中不应该有任何环形关系

---

你可能会认为，由于有了额外层次的对象实例化和子程序调用等，间接访问对象会带来性能上的损耗。事实上，这种担心为时尚早，因为你能够衡量系统的性能，并且找出妨碍性能的瓶颈所在之前，在编码层能为性能目标所做的最好准备，便是做出高度模块化的设计来。等你日后找出了性能的瓶颈，你就可以针对个别的类或者子程序进行优化而不会影响系统的剩余部分了。

“过早的优化是万恶之源”

---

模块耦合的灵活性

传入某个类的参数应该是最小而明确的，比如如果只要使用employee对象中age和level，就应当只接受这两个参数，而不是将employee对象全部传入

# 2017-11-05

**echarts**

技术对比：

echarts：canvas

highcharts：svg

D3：v3为svg，v4为canvas

# 2017-11-07

**javascript**

传统上，JavaScript只有`indexOf`方法，可以用来确定一个字符串是否包含在另一个字符串中。ES6又提供了三种新方法。

- **includes()**：返回布尔值，表示是否找到了参数字符串。
- **startsWith()**：返回布尔值，表示参数字符串是否在原字符串的头部。
- **endsWith()**：返回布尔值，表示参数字符串是否在原字符串的尾部。

---

如果使用模板字符串表示多行字符串，所有的空格和缩进都会被保留在输出之中。

# 2017-11-09

**javascript**

javascript 中的事件循环（event-loop）

重要概念：

对task-queue实行event-loop，当前执行的东西拿到callstack中，DOM、setTimeout、Promise等会访问WebAPI，返回来的task（macrotask）或job（microtask）会放到queue中，task和job的关系类似二维数组

## 简介

一个事件循环(EventLoop)中会有一个正在执行的任务(Task)，而这个任务就是从 macrotask 队列中来的。在[whatwg规范](https://link.juejin.im/?target=https%3A%2F%2Fhtml.spec.whatwg.org%2Fmultipage%2Fwebappapis.html%23task-queue)中有 queue 就是任务队列。当这个 macrotask 执行结束后所有可用的 microtask 将会在同一个事件循环中执行，当这些 microtask 执行结束后还能继续添加 microtask 一直到真个 microtask 队列执行结束。

### 怎么用

基本来说，当我们想以同步的方式来处理异步任务时候就用 microtask（比如我们需要直接在某段代码后就去执行某个任务，就像Promise一样）。

其他情况就直接用 macrotask。

### 两者的具体实现

- macrotasks: setTimeout setInterval setImmediate I/O UI渲染
- microtasks: Promise process.nextTick Object.observe MutationObserver

## 从规范中理解

whatwg规范：[html.spec.whatwg.org/multipage/w…](https://link.juejin.im/?target=https%3A%2F%2Fhtml.spec.whatwg.org%2Fmultipage%2Fwebappapis.html%23task-queue)

- 一个事件循环(event loop)会有一个或多个任务队列(task queue) task queue 就是 macrotask queue
- 每一个 event loop 都有一个 microtask queue
- task queue == macrotask queue != microtask queue
- 一个任务 task 可以放入 macrotask queue 也可以放入 microtask queue 中
- 当一个 task 被放入队列 queue(macro或micro) 那这个 task 就可以被立即执行了

再来回顾下事件循环如何执行一个任务的流程

当执行栈(call stack)为空的时候，开始依次执行：

1. 把最早的任务(task A)放入任务队列
2. 如果 task A 为null (那任务队列就是空)，直接跳到第6步
3. 将 currently running task 设置为 task A
4. 执行 task A (也就是执行回调函数)
5. 将 currently running task 设置为 null 并移出 task A
6. 执行 microtask 队列
   - a: 在 microtask 中选出最早的任务 task X
   - b: 如果 task X 为null (那 microtask 队列就是空)，直接跳到 g
   - c: 将 currently running task 设置为 task X
   - d: 执行 task X
   - e: 将 currently running task 设置为 null 并移出 task X
   - f: 在 microtask 中选出最早的任务 , 跳到 b
   - g: 结束 microtask 队列
7. 跳到第一步

上面就算是一个简单的 event-loop 执行模型

再简单点可以总结为：

1. 在 macrotask 队列中执行最早的那个 task ，然后移出
2. 执行 microtask 队列中所有可用的任务，然后移出
3. 下一个循环，执行下一个 macrotask 中的任务 (再跳到第2步)

## 其他

- 当一个task(在 macrotask 队列中)正处于执行状态，也可能会有新的事件被注册，那就会有新的 task 被创建。比如下面两个

  1. promiseA.then() 的回调就是一个 task

  - promiseA 是 resolved或rejected: 那这个 task 就会放入当前事件循环回合的 microtask queue
  - promiseA 是 pending: 这个 task 就会放入 事件循环的未来的某个(可能下一个)回合的 microtask queue 中

  1. setTimeout 的回调也是个 task ，它会被放入 macrotask queue 即使是 0ms 的情况

- microtask queue 中的 task 会在事件循环的当前回合中执行，因此 macrotask queue 中的 task 就只能等到事件循环的下一个回合中执行了

- click ajax setTimeout 的回调是都是 task, 同时，包裹在一个 script 标签中的js代码也是一个 task 确切说是 macrotask。

---

在promise中，reject相当于throw一个错误，reject和前面then中的错误都能被catch捕获；

resolve语句后面再抛出的错误就无法被catch捕获了，因为promise状态只会改变一次，错过了那一次then、catch都不会被调用；

如果没有catch或then的第二个参数，promise中的错误不会层层抛出导致系统中止，但可以通过node中的unhandledRejection事件等监听，此机制node今后有可能会改

---

`Promise.all`方法用于将多个 Promise 实例，包装成一个新的 Promise 实例。

```
const p = Promise.all([p1, p2, p3]);

```

上面代码中，`Promise.all`方法接受一个数组作为参数，`p1`、`p2`、`p3`都是 Promise 实例，如果不是，就会先调用下面讲到的`Promise.resolve`方法，将参数转为 Promise 实例，再进一步处理。（`Promise.all`方法的参数可以不是数组，但必须具有 Iterator 接口，且返回的每个成员都是 Promise 实例。）

`p`的状态由`p1`、`p2`、`p3`决定，分成两种情况。

（1）只有`p1`、`p2`、`p3`的状态都变成`fulfilled`，`p`的状态才会变成`fulfilled`，此时`p1`、`p2`、`p3`的返回值组成一个数组，传递给`p`的回调函数。

（2）只要`p1`、`p2`、`p3`之中有一个被`rejected`，`p`的状态就变成`rejected`，此时第一个被`reject`的实例的返回值，会传递给`p`的回调函数。

---

`Promise.race`方法同样是将多个Promise实例，包装成一个新的Promise实例。

```
const p = Promise.race([p1, p2, p3]);

```

上面代码中，只要`p1`、`p2`、`p3`之中有一个实例率先改变状态，`p`的状态就跟着改变。那个率先改变的 Promise 实例的返回值，就传递给`p`的回调函数。

`Promise.race`方法的参数与`Promise.all`方法一样，如果不是 Promise 实例，就会先调用下面讲到的`Promise.resolve`方法，将参数转为 Promise 实例，再进一步处理。

---

可用Promise.resoleve()或Promise.reject()返回一个立即变化的Promise对象

---

目前Promise尚无finally方法

# 2017-11-10

**javascript**

在await后面的promise中，只要有一个reject，async返回的promise就reject了，后面的await都不会执行了，如果不希望这样可以用try/catch或.catch()处理这个promise

---

await同时触发，可有两种方式：

```
// 写法一
let [foo, bar] = await Promise.all([getFoo(), getBar()]);

// 写法二
let fooPromise = getFoo();
let barPromise = getBar();
let foo = await fooPromise;
let bar = await barPromise;
```

不要将await写在forEach回调中

---

箭头函数中如返回值仅为对象字面量，需在大括号外包裹括号，若参数仅为对象的展开写法，也需在大括号外包裹括号