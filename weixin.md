# 框架

小程序框架的核心是响应的数据绑定系统，分为两部分：视图层（View）和逻辑层（App Service）

app由根目录以下文件定义：

```
app.js
app.json
app.wxss
```

小程序页面由一个文件夹下同名的以下文件定义：

```
js
wxml
json
wxss
```

app与页面的json配置见

https://developers.weixin.qq.com/miniprogram/dev/framework/config.html



# App Service

无法使用window、document等全局变量

在app.js中通过如下App()方法注册小程序：

```
App({
  onLaunch: function(options) {
    // Do something initial when launch.
  },
  onShow: function(options) {
    // Do something when show.
  },
  onHide: function() {
    // Do something when hide.
  },
  onError: function(msg) {
    console.log(msg)
  },
  globalData: 'I am global data'
})
```

具体配置见：

https://developers.weixin.qq.com/miniprogram/dev/framework/app-service/app.html

可通过全局的 `getApp()` 函数可以用来获取到小程序 `App` 实例，以使用全局参数



在页面的js中通过`Page(Object)` 函数用来注册一个页面

Object 内容在页面加载时会进行一次深拷贝，需考虑数据大小对页面加载的开销

页面中可通过this.route获取当前路由

页面的setData类似于setState，注意

- 仅支持可JSON化的数据
- 单次设置的数据量不能超过1MB
- 不要将数据设为undefined
- 可单独设置类型为数组或对象的data的某个子字段

页面路由方法见：

https://developers.weixin.qq.com/miniprogram/dev/framework/app-service/route.html



所有js变量都是文件作用域

模块采用commonjs形式



API分为三类

- 以on开头的为事件监听，传入回调函数
- 以Sync结尾的为同步API
- 异步API传入success、fail、complete（无论成功失败都执行）回调函数



# View

双大括号可用于以下作用：

- 绑定data中的变量
- 用于组件属性字符串内
- 组件属性字符串内包裹boolean值

双大括号中可进行各种运算或数据路径运算

双大括号与属性的双引号之间不能有空格



列表渲染关键字为wx:for，用wx:for-item、wx:for-index指定元素和下标，可以渲染block标签包裹多个节点

可通过wx:key指定唯一键，`wx:key` 的值以两种形式提供

1. 字符串，代表在 for 循环的 array 中 item 的某个 property，该 property 的值需要是列表中唯一的字符串或数字，且不能动态改变。
2. 保留关键字 `*this` 代表在 for 循环中的 item 本身，这种表示需要 item 本身是一个唯一的字符串或者数字，如：

wx:for的值如果是字符串，将会解析成字符数组



条件渲染关键字为wx:if，可以渲染block标签包裹多个节点

性能成本上，wx:if主要在切换成本，hidden主要在初始加载成本



template标签为模板，name定义模板，is调用模板



事件分为非冒泡事件和冒泡事件

冒泡事件主要是触摸和动画启停，详见：https://developers.weixin.qq.com/miniprogram/dev/framework/view/wxml/event.html

除此之外都是非冒泡事件

冒泡事件绑定时，bind开头表示允许冒泡，catch表示阻止冒泡，在这前面再加capture-前缀表示在捕获阶段触发

事件对象中的timeStamp为打开页面到触发事件的毫秒数

在组件中以data-开头的自定义属性，可通过事件对象中target和currentTarget的dataset获取，键名为去除data并小写驼峰



在wxml文件中，可通过import和include引入另一wxml文件

import只引入template，且不可使用引入文件中再引入的其他template

include相当于把整个wxml拷贝到此位置



wxss中可采用rpx单位，为屏幕宽度的 1/750，

可使用@import通过相对路径引入其他wxss文件

app.wxss中的样式作用域为全局，page的wxss定义的作用域为页面局部，且优先级高于app.wxss中的样式



所有组件都有的公共属性见https://developers.weixin.qq.com/miniprogram/dev/framework/view/component.html



wxs是构建wxml的脚本语言，不同于逻辑层的JavaScript，逻辑层写在.js文件中

wxs脚本可直接写在wxs标签内或通过wxs标签的src引用

关于wxs的理解

在小程序中，逻辑层运行在单独的App Server线程中，每个页面运行在各自的page frame线程中，逻辑线程与视图线程通过响应式的消息通信，只有App Server中可以运行js，wxs就是为了供page frame线程中一些简单的逻辑所需，通过wxs运行的逻辑无需进行线程消息通信，语法是弱化版的js，适合进行一些轻量的渲染前逻辑，比如类似vue中computed的功能



# 自定义组件

自定义组件与页面的定义类似，区别：

- 在json配置中设置"component": true
- 在组件wxss中不应使用ID选择器、属性选择器和标签名选择器
- 注册函数为Component()

组件使用时需在页面配置的"usingComponents"中声明，组件中要使用其他组件也需在组件配置的"usingComponents"中声明

组件定义中使用slot标签表明子节点挂载的位置

一般slot只能挂载一个，如需挂载多个可通过配置开启：

```js
options: {
    multipleSlots: true // 在组件定义时的选项中启用多slot支持
  },
```

通过slot定义中的name属性与使用时component的slot属性进行对应



组件样式尽量使用类选择器，后代选择器、子选择器尽量不要使用

继承样式会从组件外继承至组件内，除此之外全局样式对组件内无效

可用:host选择器设置组件所在节点的默认样式

可通过配置externalClasses以及与使用时传入类名来为组件添加外部样式

特殊情况下可通过

```js
options: {
    addGlobalClass: true,
  }
```

为组件开启接受全局样式，但这样可能会导致污染不建议使用



组件的pageLifetimes可访问到组件所属页面的生命周期

组件与页面的一个差异是组件有properties，如给页面配置"usingComponents": {}参数，则可通过Component()函数注册该页面，则可定义能接受properties的页面，可通过路由中类似url参数的格式传递

setData可设置data和properties，设置properties时如为数组或对象时存在bug

注意组件属性名不要以data开头，属性名和data字段也不要重名