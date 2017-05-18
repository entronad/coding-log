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