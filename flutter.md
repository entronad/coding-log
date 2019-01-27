例子

官方商店示例 https://github.com/flutter/samples/tree/master/shrine

所有组件示例 https://github.com/flutter/flutter/tree/master/examples/flutter_gallery

---

起到绘图作用的Widget是 [`CustomPaint`](https://docs.flutter.io/flutter/widgets/CustomPaint-class.html)和[`CustomPainter`](https://docs.flutter.io/flutter/rendering/CustomPainter-class.html)

层叠使用[`Stack`](https://docs.flutter.io/flutter/widgets/Stack-class.html)

StatelessWidget的build方法在三种情况下调用：

- 当挂载到树中时
- 当父Widget变化时
- 当它继承自的Widget变化时

StatefullWidget本身不需要build方法，一切依靠state，必须要一个返回类型为State的createState()方法创建state

State必须要有build方法返回视图

一个组件的state一般都是交给父组件管理，除非动画

路由靠[Route](https://docs.flutter.io/flutter/widgets/Route-class.html) （screen的抽象）和 [Navigator](https://docs.flutter.io/flutter/widgets/Navigator-class.html) （管理routes）

TabBar Drawer等在Scaffold里都有

自定义的手势事件将Widget放在 [`GestureDetector`](https://docs.flutter.io/flutter/widgets/GestureDetector-class.html)中

网络请求通过 http 包和 dart:io 包

文本输入用 [`TextEditingController`](https://docs.flutter.io/flutter/widgets/TextEditingController-class.html) ，表单用[`Form`](https://docs.flutter.io/flutter/widgets/Form-class.html) 和 [`TextFormField`](https://docs.flutter.io/flutter/material/TextFormField-class.html) 

平台指定判断：

```
Theme.of(context).platform == TargetPlatform.iOS
Theme.of(context).platform == TargetPlatform.android
Theme.of(context).platform == TargetPlatform.fuchsia
```

动画通过 [`Animation`](https://docs.flutter.io/flutter/animation/Animation-class.html) 和[`AnimationController`](https://docs.flutter.io/flutter/animation/AnimationController-class.html)

可滑走的组件用 [`Dismissible`](https://docs.flutter.io/flutter/widgets/Dismissible-class.html) 

RN与flutter组件对应表https://flutter.io/docs/get-started/flutter-for/react-native-devs#react-native-and-flutter-widget-equivalent-components

---

解决依赖冲突的一个办法是先改成any再改回来

Widget 的主要作用是实现build方法

常用Widget：

[Text](https://docs.flutter.io/flutter/widgets/Text-class.html) ：显示文本

[Row](https://docs.flutter.io/flutter/widgets/Row-class.html), [Column](https://docs.flutter.io/flutter/widgets/Column-class.html) ：按照web的flexbox模型布局组件

[Stack](https://docs.flutter.io/flutter/widgets/Stack-class.html) ：层叠组件，上面可以通过 [Positioned](https://docs.flutter.io/flutter/widgets/Positioned-class.html) 放置相对定位的组件

[Container](https://docs.flutter.io/flutter/widgets/Container-class.html) ：相当于View的容器

[Expanded](https://docs.flutter.io/flutter/widgets/Expanded-class.html) 铺满剩余空间的组件，它有决定比例的flex参数

Widget的所有成员变量都应该是final

---

如要使用[Material icons](https://design.google.com/icons/)，需在pubspec.yaml中设置：

```
name: my_app
flutter:
  uses-material-design: true
```

---

要使用MD组件，传入runApp组件的最外层需是[MaterialApp](https://docs.flutter.io/flutter/material/MaterialApp-class.html)

---

给Widget传递Widget元素作为参数是一个常用的提高组件通用化的技巧

---

 [Navigator](https://docs.flutter.io/flutter/widgets/Navigator-class.html) 属于MD组件，管理routes，并提供屏幕切换的过渡动画

---

Widget构造函数的参数都是命名参数