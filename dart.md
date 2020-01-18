#基本特点

- 任何变量都是对象，包括基本类型，所有对象都继承自 Object 类
- 强类型，自带类型推断，但也可指定类型
- 有泛型
- 支持最外层函数定义，也支持类的静态方法与对象的实例方法，函数中可定义内部函数
- 支持最外层变量定义，也支持类的静态成员和对象字段
- 没有表示私有公用的关键字，以“_”开头的标识符表示库中私有
- 标识符以字母或“_”开头，后面可随意组合
- 语句末尾要加分号


#变量与类型


- 不指定类型定义变量的关键字是var，会根据初始化的值推断类型，但一旦确定后不可赋给其它类型的值
- 如需要定义**可变类型**的变量，可使用关键字dynamic或指定类型为Object
- 任何类型变量没有初始化，值都为null，表示“没有”的只有null
- 表示常量的关键字是final和const，他们可以代替var关键字或写在类型之前
- const是编译时常量，在编译时确定，不可定义为实例变量；final是运行时常量，在第一次使用时确定；一个常量是const类型也暗示必然是final类型
- const也可定义为其它const的算式结果，在类中定义需与static一起
- const可写在变量或构造函数前用来定义常值，常量表示引用关系不可变，常值表示值本身不可变
- 数值类型num，有两个子类int，double，int可进行按位运算，没有基本类型的概念，由于int，double都是num的子类，定义为num的变量可以在int、double间多态
- 数值转字符串用int.parse('1')，double.parse('1.1')，字符串转数值用1.toString()，3.14159.toStringAsFixed(2)
- 字符串字面量中可用\${}引用表达式，或直接\$引用标识符
- 两个字面相同的字符串相等
- 可用连续三个单引号或双引号表示多行字符串
- 字符串前加字母 r 则不处理转义
- 布尔类型bool，所有需要判断的地方只能传入严格的bool结果
- List类型，在定义时会推断泛型
- Map类型，key可为任意类型，在定义时会推断泛型，用{}字面量定义的会推断为Map类型
- 在用构造函数新建对象时，可不用new关键字
- 当用map[key]取值时，如没有此key，会返回null
- UTF-16字符用\uxxxx表示，其它长度编码的UTF字符（不是4位）要加{}：\u{xxxxx}
- 可通过\#获取标识符的Symbol，压缩会改变标识符的名称但不会改变它的Symbol


#函数


- 函数的返回值、参数可设定类型也可不设，无返回值的函数返回类型可设为void
- 只有一个表达式的函数可写成箭头函数
- 函数的可选参数分为命名参数和位置参数
- 命名参数的定义：

```
void enableFlags({bool bold, bool hidden}) {...}
```

- 命名参数的调用：

```
enableFlags(bold: true, hidden: false);
```

- 命名参数可用在参数很多很复杂的情况，定义时时，可通过@required确定其为必须的，需引入package:meta/meta.dart或package:flutter/material.dart包：

```
const Scrollbar({Key key, @required Widget child})
```

- 在函数定义时，形参表最后可用[]获取位置参数：

```
String say(String from, String msg, [String device]) {
  var result = '$from says $msg';
  if (device != null) {
    result = '$result with a $device';
  }
  return result;
}
```

- 可选参数可通过 = 设置默认值，不设置默认值为null
- 应用必须有一个main函数：

```
void main() {
  
}

或

void main(List<String> arguments) {
  
}
```

- 函数定义式（包括前面带上名字的箭头函数）相当于定义了一个闭包类型的变量，等价于定义并将一个匿名函数赋值给一个变量，但不可以同时定义命名函数又赋值给变量
- 作用域遵循词法作用域，作用域是静态确定的，函数可使用其定义时的变量
- 任何函数都有返回值，如未显示指明则返回null，故函数调用式一定是表达式



- 多元运算符的版本由最左边一个参数决定
- ~/：整除（向下取整）
- ==规则：如果涉及到null，必须两边都为null则返回true，否则返回false；如果不涉及null，返回左边参数的*x*.==(*y*)方法结果
- is；is!：判断一个对象是（不是）一个类的实现（包括子类）
- as：将一个对象强转为一个类，如果该对象为null或不是该类将报错
- ??=：如果为null就赋值，否则不动
- ^：按位异或
- ~：按位取反
- ??：条件运算符，如果左边不为null返回左边，否则返回右边
- ..：级联运算符，表示把左边对象中的右边成员取出进行某项操作再返回该对象
- ?.：条件获取成员，如果左边为null也不报错而是返回null


#结构语句

- else if中间分开一个空格
- 可以用forEach()和for-in遍历可迭代对象，比如Map，List
- switch分支比对的目标必须是编译时常量，被比较实例必须是同一类（不可以是子类），不可重写==



- 异常分为Exception和Error两类以及它们的子类
- 方法无需进行异常声明和检查
- 可以throw任意对象，当然不建议这样做
- throw式是一个表达式
- on指明捕捉的异常类型，catch指明异常参数，两者可配合使用，有了on可省略catch
- catch有第二个参数StackTrace
- 在catch块中，可用rethrow关键字继续抛出该异常
- 就算遇到未捕获的异常，也会先执行完finally中的异常再抛出


#面向对象


- 类只可以有一个父类，子类可使用任意级父类的内容
- 对于定义了常量构造函数的类，可用const关键字调用，调用相同常量构造函数（包括参数）构造的对象是同一个实例
- 在一个常量作用域内（比如一个常量Map）都是常量，不需要再重复写const了
- 对象类信息的字段是runtimeType
- 类中声明了初始值的字段，字段会在constructor之前初始化
- 在类中只有命名冲突时才需要this.xx
- 可以以如下的形式定义命名构造函数

```
Point.origin() {
    x = 0;
    y = 0;
  }
```

- 任何构造函数都不会被继承
- 如果没有特别指明，子类的构造函数中第一步会调用父类的默认构造函数
- 子类构造函数的执行顺序是：初始化字段表->父类构造函数->子类构造函数
- 定义了构造函数会覆盖掉默认构造函数，如父类没有默认构造函数，子类构造函数需在函数体大括号前用冒号手动指明调用父类构造函数

```
class Employee extends Person {
  // Person does not have a default constructor;
  // you must call super.fromJson(data).
  Employee.fromJson(Map data) : super.fromJson(data) {
    print('in Employee');
  }
}
```
- 构造函数大括号前还可用冒号指明初始化字段表，常用来设置final字段：

```
// Initializer list sets instance variables before
// the constructor body runs.
Point.fromJson(Map<String, num> json)
    : x = json['x'],
      y = json['y'] {
  print('In Point.fromJson(): ($x, $y)');
}
```

- 没有函数体，而是用冒号指向调用其他构造函数，称为重定向构造函数：

```
class Point {
  num x, y;

  // The main constructor for this class.
  Point(this.x, this.y);

  // Delegates to the main constructor.
  Point.alongXAxis(num x) : this(x, 0);
}
```

- 固定不变的对象可设为编译时常量，通过类定义中的常量构造函数实现：

```
class ImmutablePoint {
  static final ImmutablePoint origin =
      const ImmutablePoint(0, 0);

  final num x, y;

  const ImmutablePoint(this.x, this.y);
}
```

- 如果不希望构造函数总是新建一个实例，添加了factory关键字成为工厂构造函数，工厂构造函数不可访问this：

```
class Logger {
  final String name;
  bool mute = false;

  // _cache is library-private, thanks to
  // the _ in front of its name.
  static final Map<String, Logger> _cache =
      <String, Logger>{};

  factory Logger(String name) {
    if (_cache.containsKey(name)) {
      return _cache[name];
    } else {
      final logger = Logger._internal(name);
      _cache[name] = logger;
      return logger;
    }
  }

  Logger._internal(this.name);

  void log(String msg) {
    if (!mute) print(msg);
  }
}
```

- 所有实例的字段都有getter，非final的有setter，也可通过get、set关键字设置
- 没有定义函数体的方法称为抽象方法，抽象方法只可出现在抽象类中
- 通过abstract关键字可定义抽象方法，除非定义了工厂构造函数，抽象类不能被实例化
- 任何类都是一个接口，一个类要实现一个接口（类），用关键字impliments，可以实现多个接口
- 子类通过@override注解重写父类方法
- 可通过operator关键字重写运算符（重写 == 运算符需同时重写 hashCode的getter）
- 调用一个实例的未实现方法，将会报错，触发1.实例类型为dynamic；或2.实例定义了该方法（为抽象）同时重写了noSuchMethod()
- 枚举类型定义形式为：


```
enum Color { red, green, blue }
```

- 枚举类型中的每一个值都有一个index属性，枚举类的values属性可获得所有的值
- 不可以继承、混入、实现枚举类型，也不可以实例化枚举类型
- 创建mixin的要求是继承Object，不声明构造函数，不调用super
- 使用mixin在类定义后使用关键词with，和混入多个mixin
- 可用static关键字定义类变量和类方法，类变量在第一次使用时才会初始化；类方法不可使用this；对于公有功能，建议使用函数而不是类方法
- 除了限制类型，泛型还能起到指代类型，减少代码的作用：

```
abstract class Cache<T> {
  T getByKey(String key);
  void setByKey(String key, T value);
}
```

- 可在集合的字面量定义中使用泛型

```
var names = <String>['Seth', 'Kathy', 'Lars'];
var pages = <String, String>{
  'index.html': 'Homepage',
  'robots.txt': 'Hints for web robots',
  'humans.txt': 'We are people, not machines'
};
```

- 集合类型机制是reified（不同于Java的erasure），会在运行时保留

```
print(names is List<String>);
```

#异步处理

- 处理异步过程的类是Future和Stream，函数是async/await函数
- async关键字写在参数表与函数体之间
- 可将main函数定义为async函数
- 不需要返回值的async函数返回类型可设为Future\<void\>
- 可用await for等待遍历stream的所有值，但要小心使用：

```
await for (varOrType identifier in expression) {
  // Executes each time the stream emits a value.
}
```

- 同步generator用sync\*关键字定义，返回Iterable，异步generator用async\*关键字定义，返回Stream
- 递归generator函数中调用自身时可用yield*关键字提高性能

#其它

- 当给类实现了call()方法，类的实例就可以像函数一样被调用了


- 通过isolate处理多线程，isolate有单独的内存堆，相互之间不可访问
- 通过typedef关键字，可定义函数的具体（参数、返回值）类型：

```
typedef Compare<T> = int Function(T a, T b);

int sort(int a, int b) => a - b;

void main() {
  assert(sort is Compare<int>); // True!
}
```

- 文档级注释用///或/**开头，编译器会忽略文档级注释，但其中用[]括起来的内容仍然可以链接





dart项目安装用 pub get 指令

flutter项目安装用 flutter packages get





模块体系类似于java，该体系称为library，

当使用import语句引入一个文件，该文件所有顶层的对象都进入引用者的命名空间

library的内容放在lib文件夹下，该文件夹中通过一个与library同名的文件export想要导出的文件

导入其它library的文件，需加package:指令，在同一个library中，也可使用相对路径，但不能跨lib文件夹，保险的方式是都用package:

相对路径不需要.开头，绝对路径巧用package:指令

如果命名冲突，要用as show hide等方法

---

面向对象的继承体系同时基于 class 和 mixin

当对象有可能为null时，用 ?. 调用其成员

构造函数既可以是className的形式，也可以是ClassName.methodName的形式

由于仅传递给成员初始值的构造函数太常见了，因此有如下简写语法糖

```
Point(this.x, this.y);
或
MyAppBar({this.title});
```

可定义如下命名构造函数：

```
Point.origin() {
    x = 0;
    y = 0;
  }
```

构造函数不会继承（包括命名构造函数），没有定义构造函数的子类只会有默认构造函数（无参数传递）

类构造函数参数表与函数体（可以没有）之间用 : 开头的部分，按顺序可放置（逗号隔开）：

1初始化参数表

2.子类的构造函数如果不加指定，会自动调用父类的默认（无参匿名）构造函数，没有在构造函数体中使用super()这样的写法；如父类无默认构造函数或需要特别指定放在这里

3.通过this()重定向到本类的其他构造函数

---

函数的参数可按是否必须、是否命名来分

位置参数天生是必须参数，命名参数（写在{}中）天生是非必须参数

位置参数变成可选需写到[]中，命名参数变成必须参数需加@required

不能同时有命名可选参数与位置可选参数。[]{}只能出现一个且在最后，后面不能有逗号

可选参数可用 = 添加默认值

---

类似于class关键字用来定义类对象，typedef关键字用来定义“函数类型”对象：

首字母大写，用Function关键字指代函数标识符，可有泛型

```
typedef Compare = int Function(Object a, Object b);
typedef Compare<T> = int Function(T a, T b);
```

---

匿名函数，箭头函数：有大括号的不要加箭头，就一个表达式的要加箭头，参数只有一个也要加括号

---

在List和Map的字面量前可用\<\>指定泛型

---

const 必然是final的

实例只能是final

final在第一次用到时初始化

类中的const 一定是static const

const写在应用类型的值前面表示它是编译时固定了

const只能被赋予编译时常量，如果被赋给了引用类型，该值会编译时固定

在const作用域内的const都可省略

---

String中变量$后面如果是一个标识符，大括号可省略

---

强类型，当用var定义时类型不可改变，如需改变可用 Object 类型或 dynamic关键字

任何未赋值的变量值为null

类成员如果要是const，一定要设为static const

---

num 的常用子类是整数 int 和小数 double ，整数字面量可直接赋值给小数自动转换

数字与字符串转换 int.parse('1')；1.toString()

int 类型是64位的，有位操作

如果操作符的操作数都是编译时常量，则操作符结果也是编译时常量

---

拼接字符串可用加号或直接按顺序放在一起，多行字符串用三引号

---

因为条件判断的对象必须严格是bool类型，所以要加上判断：

name.isEmpty

unicorn == null

mean.isNaN

注意null、String等不可用isNaN判断

---

List的成员类型必须一致，符合其泛型

---

string是utf16字符，如果需要utf32类型字符，需要rune类型，如果4个数字可以是'\u2665'，超过4个数字要'\u{1f600}'

---

\# 可以提取标识符或操作符的Symbol

---

箭头函数前半段语法与普通函数一样，即不加括号部分是函数名，参数一定要加括号

---

main函数有一个List\<String\> arguments参数获取命令行调用时传入的参数

---

函数的作用域是在定义时通过代码的层级确定的，称为词法作用域

---

顶层函数、类的静态方法都是同一个函数，不同实例的实例实例方法不是同一个函数

---

函数都有返回值，默认是null

---

switch语句中，如果case有了内容，一定要break或continue结尾，如果case里没有内容可以穿过

---

assert只有dev环境下有用，production中无用

---

throw是表达式

---

多个catch子句只会抓住第一个符合类型的

catch的第二个参数s是StackTrace

---

加了factory关键字的构造函数不总是返回新实例

factory构造函数中不可使用this

---

getter setter 是方法前加了get、set关键字，并与成员同名

赋值语句也是表达式，可用于箭头函数

---

抽象类只能包含抽象方法，抽象方法只能出现在抽象类中

抽象类不能实例化，只能用来被继承或实现

---

除了extends继承一个类外，还可以implements实现一个类的多个接口，以实现多态

---

operator关键字，函数名为操作符，可以重写操作符

---

定义noSuchMethod()方法可以确定调用未定义的方法时的行为

只有dynamic类型、定义了unimplemented方法的static类型或实现了noSuchMethod()的对象可以唤起未实现的方法

---

枚举是一种特别的类，定义方式如下：

```
enum Color { red, green, blue }
```

一般调用时类似Color.blue，常用于switch判断

Color.blue.index可以获取值的序号，Color.values可以获取所有枚举的列表

---

mixin的作用是复用代码，

mixin以mixin关键字代替class，on后面跟一个接口或超类，表明只有实现此超类或接口的可以使用此mixin

调用时使用with关键字

---

泛型在运行时依然存在，在运行时可以检测一个类型的泛型，这是dart和java的区别

要限制参数的类型，可以使用extends关键字

---

函数泛型

定义在first\<T\> 里，可在返回类型、参数类型、本地变量类型中使用

---

async函数调用时会同步执行，直到遇到await

处理Stream可以使用await for语句或Stream的API

---

同步generator函数关键字是sync\*，返回类型是Iterable,

异步generator函数关键字是async\*，返回类型是Stream

---

涉及多核多线程使用Isolate

---

dart:core 会自动引入所有程序中

---

parse可用关键字参数radix指定进制

toStringAsFixed可指定小数位数，toStringAsPrecision可指定有效数字（1.2e+2）

---

字符串常用方法：

contains

startsWith

endsWith

indexOf

substring

spilt

直接通过[]取第几个字符

toUpperCase

toLowerCase

trim

isEmpty

isNotEmpty

replaceAll

注意字符串是不可变的，所以以上方法都是返回新的字符串

StringBuffer可以用来构建字符串，在执行toString方法前都可改动：

```
var sb = StringBuffer();
sb
  ..write('Use a StringBuffer for ')
  ..writeAll(['efficient', 'string', 'creation'], ' ')
  ..write('.');

var fullString = sb.toString();

assert(fullString ==
    'Use a StringBuffer for efficient string creation.');
```

---

RegExp的规则同js

方法有contains, replaceAll, hasMatch, allMatches

---

List方法：add, addAll, indexOf, removeAt, clear, sort

---

Set类型方法：add, addAll, remove, contains, containsAll, Set.from, intersection（交集）

---

Map类型方法：keys,values表示键和值的遍历器，containsKey, putIfAbsent（如果没有此键就加入）

---

map方法返回的是可遍历对象，注意可遍历对象是惰性求值的，如果需要立即求值需要加上toList

返回所有符合条件的对象where, 判断是否符合条件any, every，它们都是可遍历对象的方法

---

处理URI、URL用Uri对象

---

处理时间对象为DateTime

获取当前时间 DateTime.now()

时间段对象为Duration对象

---

要使一个类的实例可比较，要实现Comparable接口，重写compareTo方法

---

每个对象都有个hashCode getter，供map方法使用，可以重写

---

Future有then、catchError方法

async函数一定返回Future

多个Future完成用 Future.awit方法

---

Stream 常用于监听点击事件，它可用listen方法监听

```
// Find a button by ID and add an event handler.
querySelector('#submitInfo').onClick.listen((e) {
  // When the button is clicked, it runs this code.
  submitData();
});
```

添加对返回值的处理用transform

处理错误和结束给listen传入onError和onDone

---

数学处理在

```
import 'dart:math';
```

中

随机数通过Random对象获取，有多种类型：

```
var random = Random();
random.nextDouble(); // Between 0.0 and 1.0: [0, 1)
random.nextInt(10); // Between 0 and 9.
random.nextBool(); // true or false
```

---

数据转换处理在

```
import 'dart:convert';
```

中

JSON处理有jsonDecode和jsonEncode

UTF8字符串处理有utf8.decode和utf8.encode

---

赋值运算是表达式

---

类型FutureOr\<T\>只T或Future\<T\>

---

num类型中有三个特殊的值，double.nan  double.infinity  double.negativeInfinity，打印效果是NaN Infinity -Infinity，但不可直接通过关键字设置，可通过isFinite判断

---

工厂构造函数需添加factory关键字以便能按构造函数的方式调用

---

泛型只能起到编译期辅助检查类型的作用，如不指定泛型则可以为任意类型，泛型不能做到根据不同类型决定选择分支的作用

---

类中以_开头的字段，在此文件中、此类以外还是可见的，出了此文件，哪怕在此类中，也不可见了

---

静态成员和方法，不会被继承和重写

---

mixin的优先级顺序是：子类最高，mixin越往后优先级越高，高于父类

mixin的类直接继承自Object，且不能有构造函数

---

比较 == !=的规则是

1.如果有一个是null，则都是null为true，一个不为null为false

2.都不为null，调用左边数的对应方法

3.常用的内置类型都有类型不同的判定，不同类型为false

---

List越界会报错，[]适用[]运算符会报错，这点和js返回undefined不一样，可以用length进行检查

[]调用first、last等字段会报错

---

dart的double和js的number一样，都是IEEE 754 64位浮点数，会遇到一样的浮点数精度问题

---

目前函数参数如果显式的传入null，是不会触发默认值的，所以在必要的场合比如bool，需使用??

---

??= 和??都是为默认值准备的

---

确保不会变的类可在构造函数前加const，使得其可在编译期初始化，调用时前面加const

---

在super中设置的默认值，子类构造函数缺省时不会起效，要在调用super时手动补上

---

判断泛型用T == int,注意只能用在基本类型上，

---

Iterabale如果泛型类型比较广泛，元素可以是此泛型中的不同类型，比如<Object>[],就可以放任意不同的东西，包括一个函数

---

List<Object> 是不可以被推断为具体类型元素的List的，因为元素可以是不同的具体类型，此情况如果确保已存在的类型一致，可以用List.from，这与

> 可遍历对象转换为数组时，用toList而不是List.from除非你要改变元素类型，因为这会改变元素类型

对应

---

num 的三个方法

isNaN: 只有double.nan满足

isInfinite: 只有正负infinite满足

isFinite: 只有正常数字满足，那三个都不满足

因此常用判断要用isFinite，而另两个用来判断字面上指定的特殊类型

---

Rect 是ui中的类，表示图形，Rectangle是math中的类，表抽象的

---

switch case语句选项必须是编译期常量，且类型必须完全匹配不能是子类，

每个case后必须有break或continue，除了一种情况就是里面没有任何内容，表示落入下一个case，

case前可用引号加标签，continue后面跟标签名，表示继续落入此case

---

Map的[]运算符，当没有此key时，返回null，当没有此key赋值时，会创建相应的键值对

---

用强制规定类型然后addAll浅拷贝的方法，不能扩展里面引用元素的类型

直接没有泛型的[]{}定义，其泛型是Object，可随意往其中加东西，故一般字面量定义也要加泛型

---

关于集合的一些工具函数在库collection中，flutter自带此库

---

dart:convert 为sdk自带，其只提供utf-8和json的少量转换

官方pub上另有一个叫convert的库，功能更全

两者命名空间不冲突

---

2.3之后添加了...和...?运算符 ，在Map中使用时，同键名后面的会覆盖前面的

---

null 可满足所有的 as 

----

父类中的this.method，只要子类重写了method，那就是指子类中的method

---

null是有toString hashCode runtimeType等方法，它的类型是Null

---

list.indexOf如果找不到是-1

---

?. 和ES比，具有函数调用安全，但是不可应用于遍历器调用符[]和函数调用符()，[]用(map ?? const {})[key]代替







# lint

类型名（class typedef）用大写驼峰，包括注解的类，

如果注解类只有无参的构造函数，可以赋给一个const常量方便使用，此时用小写驼峰：

```
const foo = Foo();

@foo
class C { ... }
```

文件名、包名、import中的前缀，用小写下划线

常量也用小写驼峰

缩写也要进行驼峰化

import顺序为dart:, 外部package, 内部package 相对路径

export 放到所有inport之后

不建议使用part

不要直接引入其他lib的src中的内容

引入自己lib中 的内容用相对路径

对于字面量字符串，用拼接不要用+, 尽量用\$,\$后面能不要大括号就不要大括号

集合尽量用字面量定义

判断集合是不是空用isEmpty和isNotEmpty，不要length

当要定义新的回调函数时，用for in循环而不是forEach

可遍历对象转换为数组时，用toList而不是List.from除非你要改变元素类型，因为这会改变元素类型

要过滤集合的类型用whereType

尽量不要用cast()

当函数需要名字时，使用函数声明式

连接参数的默认值既可以是=也可是:，尽量用=

没有显示指明的可选参数的默认值是null，不需要显式指明

变量初始化为null不需要显式指明

类的成员变量不应该存储冗余的可从其它成员推断的量

在java和c井中，getter和直接调用成员的机制不同，所以成员都应该通过getter访问，但dart中是相同的，所以不需要给直接调用成员设置getter

只读成员应设为final

对于简单的函数，使用箭头函数，对于复杂的逻辑（超过两三行）不要用箭头函数

简单的函数即使不需要返回值也可以用箭头函数，特别是有对应getter的setter

当没有冲突时，类定义中指代成员不需要this，构造函数中不需要this

尽可能在定义式中初始化成员

不要使用new

以下情况属于const环境，其中的变量是自动的const不需要添加const关键字：const集合字面量，const构造函数，注解，const变量的声明，switch语句中case紧跟的对比项

尽量不要有没有on的catch语句，即使有，也要做好处理

程序的bug用Error，运行时的问题用Exception

不要捕获Error，应该修好bug

需要继续抛异常使用rethrow

尽量使用async/await而不是直接使用Future

注意不要滥用async

尽量不要直接使用Completer

FutureOr的测试中要将Future\<T\>作为第一判断分支，以防T为Object

不要重写类的字段，如有需要，用getter setter处理

可以为任意类型用Object，dynamic有特殊的含义



