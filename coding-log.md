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

**属性直接传值是字符串，要怎么变成数字还要研究**

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























