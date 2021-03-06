例子

官方商店示例 https://github.com/flutter/samples/tree/master/shrine

所有组件示例 https://github.com/flutter/flutter/tree/master/examples/flutter_gallery

---

起到绘图作用的Widget是 [`CustomPaint`](https://docs.flutter.io/flutter/widgets/CustomPaint-class.html)和[`CustomPainter`](https://docs.flutter.io/flutter/rendering/CustomPainter-class.html) 的子类，Painter传递给Paint的painter属性

层叠使用[`Stack`](https://docs.flutter.io/flutter/widgets/Stack-class.html)

---

StatelessWidget的build方法在三种情况下调用：

- 当挂载到树中时
- 当父Widget变化时
- 当它继承自的Widget变化时

StatefullWidget本身不需要build方法，一切依靠state，必须要一个返回类型为State的createState()方法创建state

State必须要有build方法返回视图

---

状态一般交由容器父组件管理，子组件仅管理自身的动画等状态

---

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

起到绘图作用的Widget是 [`CustomPaint`](https://docs.flutter.io/flutter/widgets/CustomPaint-class.html)和[`CustomPainter`](https://docs.flutter.io/flutter/rendering/CustomPainter-class.html)

---

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

---

打包命令是在根目录下执行flutter build apk 生成的在根目录下build文件中

当没有设置release key时，默认用debug key代替让你可打包，但记得正是发布时要替换

---

Widget与State

Widget是一种临时的对象，仅用来构建App当前的表现，任何Widget（stateless、statefull）都是immutable的，仅可有final成员变量，

Widget的核心是build方法，它返回挂载到树上的Widget

StatefullWidget本身没有可变的状态，它没有build方法，但有createState，它返回一个State，依靠State管理可变状态、用build返回挂载到树上的Widget

State对象在两次调用它自身build方法之间是持久化的，State状态的更新通过显示的调用setState方法，它的参数为一个匿名函数，函数的内容可以写的随意点，类似react，setSate一般是异步的。

仅当同一种StatefullWidget第一次被挂载时createState被调用生成State实例，当父Widget重构时，StatefullWidget会重构实例，但State的实例不会发生变化，State的build返回的Widget也会复用，仅当调用setState时，它的build方法会复用，返回新Widget

StatefullWidget两者的联系：State传入StatefullWidget作为泛型，StatefullWidget仅用来通过成员变量传递父组件的参数，State通过内置的widget 参数获得包裹的StatefullWidget对象

---

生命周期方法属于Sate而不是Widget，有：

[initState](https://docs.flutter.io/flutter/widgets/State-class.html#initState)

 [dispose](https://docs.flutter.io/flutter/widgets/State-class.html#dispose) 

---

Widget的比对靠的是类型，当有大量同类的Widget时，可以使用key，global key

---

布局依靠 [layout widgets](https://flutter.io/docs/development/ui/widgets/layout) ，视图组件放在它的child或children参数中

---

一般整个App是一个StatelessWidget，其build方法，如果要MD返回一个MaterialApp，首页放在其home参数中。

如果需要的是一个完整的页面（包含title等），用Scaffold

---

assets可仅指明文件夹名表示其中所有文件都包括，目录地址相对于pubspec.yaml文件：

```
flutter:
  assets:
    - assets/
```

---

yaml

递归式命名

大小写敏感

仅可使用空格缩进

数据结构类型：对象、数组

\# 注释

对象：

```
animal: pets
hash: { name: Steve, foo: bar } 
```

数组

```
- Cat
- Dog
- Goldfish

-
 - Cat
 - Dog
 - Goldfish
```

http://www.ruanyifeng.com/blog/2016/07/yaml.html

---

使用assets中的图片或package的assets中的图片可以：

```
AssetImage('graphics/background.png')

AssetImage('icons/heart.png', package: 'my_icons')
```

---

MaterialApp是一种特殊的Navigator，虽然它们之间没有继承关系，Navigator一般被用来调用其静态方法

Scaffold 起到Screen（Route）的作用

MaterialApp、Scaffold都是Widget，可以被放到可以放Widget的地方

routes是MaterialApp的属性

screens和pages合称routes

跳转最基本的方法是 [`Navigator.push()`](https://docs.flutter.io/flutter/widgets/Navigator/push.html)和 [`Navigator.pop()`](https://docs.flutter.io/flutter/widgets/Navigator/pop.html)

第一个参数都是context，push第二个参数是Route

Route作用是占据整个屏幕，并提供页面跳转的动画，它传入一个builder参数，返回Widget。常用的是MaterialPageRoute

push是一个异步方法，返回的Future的result可由目标路由的pop方法的第二个参数设置

跳转到命名路由用 [`Navigator.pushNamed`](https://docs.flutter.io/flutter/widgets/Navigator/pushNamed.html)方法，此时需要在App中传入routes（路由名与builder的键值对）和initialRoute，此时不要home了

不全遮挡的路由通过[PopupRoute](https://docs.flutter.io/flutter/widgets/PopupRoute-class.html)实现

定制路由通过 [PageRouteBuilder](https://docs.flutter.io/flutter/widgets/PageRouteBuilder-class.html) 实现

---

State的构造函数中不可调用setState

---

在hotreload使用中以下情况会出问题：Widget的stateful、stateless类型改变，枚举类型变成普通类，类定义的泛型变化

---

Widget中常见的contex类是BuildContext ，它用来表明此组件及其子组件在数中的位置，很多类可通过静态方法of将其添加到实例中

---

scaffold的body属性一般放在Center中

---

BottomNavigationBarItem无标题还不能实现，只能先把标题设为Container(height: 0.0)

---

自定义颜色用32位色Color类（dart:ui)，构造函数可直接传入0xAARRGGBB的16进制数，注意忘了AA会永远透明，也可用Color.fromARGB，这样每一位可是16进制或10进制，Color.fromRGBO，这样透明度用最后一位小数表示

---

在某些强制使用Theme参数而不可直接设置的地方，可以通过嵌套Theme来设置自己想要的效果

---

**Animation**

动画分两种tween animation和physics-based animation

---

基本绘图类

**[CustomPaint](https://docs.flutter.io/flutter/widgets/CustomPaint-class.html)**：(flutter) 提供canvas的widget，它最主要的功能是定义painter 和 foregroundPainter 和child

绘图顺序：自己的canvas -> 子元素绘图 -> 自己的foregroundPainter

只能在自己的尺寸内绘制，出去会导致未定义的行为

它的绘制行为由Painter控制，不可使用setState和markNeedsLayout

决定大小的顺序是：包裹子元素 -> size属性（默认是0）



**[CustomPainter](https://docs.flutter.io/flutter/rendering/CustomPainter-class.html)**：(flutter) 给CustomPaint使用的接口，主要功能是定义paint 和 shouldRepaint方法

paint方法在任何需要重绘的时候调用，paint方法会传入canvas和size，其中进行对canvas的绘制

shouldRepaint方法在类生成新实例的时候决定是否需要重绘。常通过以下两种方式触发repaint：

- 继承此类，并传入repaint参数给构造函数，该参数对象会通知何时repaint
- 继承一个 [Listenable](https://docs.flutter.io/flutter/foundation/Listenable-class.html) 或其实现类，实现 [CustomPainter](https://docs.flutter.io/flutter/rendering/CustomPainter-class.html)接口，这样其本身就能提供通知



**[Canvas](https://docs.flutter.io/flutter/dart-ui/Canvas-class.html)**：(dart:ui) 记录图形操作的接口，

canvas有一个作用于所有操作的transformation matrix，初始为1矩阵，可通过translate, scale, rotate, skew, transfrom等方法修改

canvas有一个作用于所有操作的clip region，初始为无穷大，可通过clipRect, clipRRect, clipPath等方法修改

这两个状态可通过 save, saveLayer, restore等方法进行栈操作

Canvas创建的是 [Picture](https://docs.flutter.io/flutter/dart-ui/Picture-class.html) 对象，但这由框架处理开发者不用管



 [Paint](https://docs.flutter.io/flutter/dart-ui/Paint-class.html) ：(dart:ui) 描述canvas上绘图样式的类，大部分canvas的API中都会带一个Paint对象以描述样式

 [RenderCustomPaint](https://docs.flutter.io/flutter/rendering/RenderCustomPaint-class.html)：CustomPaint的createRenderObject方法的返回对象

**总结** 绘图主要操作对象是canvas对象，开发者的绘图定义在Painter中

---

类似react中的，ref需要的是state而不是Widget

---

虽然写程序的时候万物皆是Widget，但屏幕上视图树上的是Element，Widget不可修改，Element可修改，Element类实现了BuildContext，事实上我们使用的BuildContext就是Element, 为什么要封装这个接口主要是为了避免直接使用Element

Navigator.of(context)的作用是向上遍历寻找最近的NavigatorState，故要确保传进来的context上方包含NavigatorState，比如有MaterialApp

---

对于Widget，只有新旧的key和runtimeType都变了才会更新Element

---

flutter中目前不准备有dart:mirrors，因为这会导致没法tree shaking

---

StatelessWidget 的 build 方法只会在三种情况下调用：第一次被插入组件树；组件的父元素改变配置；它所依赖的InheritedWidget发生改变。

当build要被反复调用更改时，还不如用StatefulWidget

当key被设置为GlobalKey时，StatelessWidget被移动时它不会被销毁重建

StatefullWidget有两种模式

一、只在State.initState中创建资源，在State.dispose中销毁资源，不会调用setState或依赖inheritedWidgets，一般用在应用或页面的根组件，通过ChangeNotifier或Stream等与子组件通信。这里组件消耗少，可以由比较复杂的build方法

二、会调用setState或依赖inheritedWidgets，会多次rebuild，需要尽量减少rebuild的影响

减少rebuild消耗的办法：

- state尽量放在末端
- build方法中的Widget尽量少，最好只有一个简单组件（直接继承自[RenderObjectWidget](https://api.flutter.dev/flutter/widgets/RenderObjectWidget-class.html)）（不一定现实）
- 不变的子树尽量不重构，常用方法是将stateful的部分提取出来接受一个child参数
- 尽可能使用const Widgets
- 不要改变树的层级和节点的类型（类似react）
- 不变的地方使用GlobalKey

state的生命周期：

创建：

1. [StatefulWidget.createState](https://api.flutter.dev/flutter/widgets/StatefulWidget/createState.html)
2. state将与 [BuildContext](https://api.flutter.dev/flutter/widgets/BuildContext-class.html) 永久绑定，mounted变为true
3. 调用 [initState](https://api.flutter.dev/flutter/widgets/State/initState.html) 
4. 调用 [didChangeDependencies](https://api.flutter.dev/flutter/widgets/State/didChangeDependencies.html) ，里面主要是涉及 [InheritedWidget](https://api.flutter.dev/flutter/widgets/InheritedWidget-class.html) 的东西
5. 完成初始化，build方法可用

更新

​    如果因为外界因素（父组件rebuild）导致生成了同类型和key的widget，将会调用[didUpdateWidget](https://api.flutter.dev/flutter/widgets/State/didUpdateWidget.html) 方法，其后总会自动调用build方法

注意state自身调用setState引起的更新，只会调用 build 而不会调用 didUpdateWidget 。父组件中该子组件是写好每次build的时候都是同一个实例时，子组件也不会调用 didUpdateWidget。

销毁：

1. 当从组件树中移除时调用deactivate
2. 当移除后不再挂到新的位置时，调用dispose

---

当需要获取某个 Widget 的实例，以便对其进行控制时，可不直接将其构造函数写在build树中，而是通过一个方法，在此方法中创建此实例并保存，然后将其返还，在build树中调用此方法。

---

有些类型灵活的接口参数，可否采用 null - defaultValue - customValue 的形式？还是 hasXXX, XXX 组合的形式？

采用前者的优势，绝大部分接口，要么默认值是null，没有 defaultValue, 要么默认值就是defaultValue，要么默认值就是 defaultValue ，挂在本体类下面即可，只有默认值是null，但还要提供 defaultValue 这一种情况比较复杂，但这是很少的一种情况，在本体类（参数是基本类型或类）或参数类型类（有自定义的类）下面挂上 defaultXX 即可，注意一般要const。
多个组件要通过继承复用实现某一结构类似的视图时，可以这样：widget 或state 里的 build 方法一样，将其中要变的部分视图抽取出来，单独用函数提供，然后重写这个函数

---

Hero 组件的作用是通过动画跨页面传递组件

---

Curve 对象使用时用 transform, 子类实现时重写 transformInterval ，transform 对 transformInterval包装并添加了越界逻辑

---

flutter每次update之后，都会重新执行一遍build方法，即build内定义的东西每次都换新的，即widget（不管StatefulWidget还是staetelessWidget）是用完即丢的东西。

而state是持久化的东西，每次StatefulWidget换新的了不会执行createState重新实例化state

因此才需要将 widget 和 state 分离，

因此想要持久化的东西需保持在state中，传递的话通过state -> widget.xx -> 传递，而不能在widget的构造函数中新建

一般StatefulWidget中的成员或方法都是表征当前组件树状态，供state使用的，或供state进行初始化用的

---

通过CustomXXXChildLayout 和 XXXChildLayoutDelegate 可以设置和获取子元素的位置、大小