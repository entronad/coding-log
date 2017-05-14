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
# 2017-05-14

**CSS**

`top`、`right`、`bottom`、`left` 属性定义与各边边距