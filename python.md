布尔值关键字为 True False

逻辑运算关键字为 and or not

空值 None

精确除法 / ; floor取整除法 //

模板字符串 '%d %f %s %x' % (1, 1.2, 'aaa', '0x16')

- %s       字符串 (采用str()的显示)
- %r       字符串 (采用repr()的显示)
- %c       单个字符
- %b       二进制整数
- %d,%i     十进制整数
- %o       八进制整数
- %x,%X     十六进制整数
- %e,%E     指数
- %f,%F      浮点数
- %g,%G     指数或浮点数 (根据显示长度)
- %u       无符号数（没有细查文档，经测试可以输出负数）
- %%       字符"%"

现在先一律使用.format吧，可以用命名参数关联，可以带:表示类型

列表分为list和tuple

获取list长度 len()

获取list最后一个参数 datas[-1]，倒数第二个 datas[-2]

list操作方法：

	末尾增加 datas.append(data)
	
	指定位置插入：datas.insert(index, data)
	
	删除末尾：datas.pop()
	
	删除指定位置：datas.pop(index)

list中数据类型可不同

tuple是不可变的list

tuple定义：(1, 2, 3)

仅一个元素的tuple：(1.2, )

冒号与缩进表示代码块，缩进多少不做规定

条件判断：

if a > b:

	a++

elif:

	b++

else:

	c++

判断的类型转换：只要`x`是非零数值、非空字符串、非空list等，就判断为`True`，否则为`False`。

不同类型无法比较，需使用显式的转换函数

循环遍历数组采用 for in

Map为dict

通过d['key']查找dict若不存在会报错

'key' in d 的判断是否包含

d.get('key')若不存在返回None

dict可用d.pop('key')删除元素

dict的key须采用字符串、整数等不可变数据类型

set只包含不重复的key

初始化s = set(list)

set增加 add(key)

set删除 remove(key)

set的交集、并集操作 s1 & s2 ; s1 | s2

函数参数数量和类型必须与定义一致，否则会报错

数据类型转换函数 int() float() str() bool()

函数定义

def abc(x):

	return 0

暂时空缺的语句块可以用pass占位

函数可以返回多个值，本质上是构成了一个tuple

可用power(x, n=2)的形式定义默认参数

如调用函数时不是按顺序省略参数，可用如下形式enroll('Adam', 'M', city='Tianjin')

默认参数必须指向不变对象，否则多次调用函数且修改参数时可能存在问题

参数类型：

	一般的参数叫做位置参数，通过在参数表中的位置表明关系
	
	可变参数定义函数calc(*numbers)会将传入的多个参数组成tuple，在调用时calc(*[1,2,3])表示将该list作为可变参数传入
	
	关键字参数定义函数def person(name, age, **kw):会将传入的键值对作为dict传入，调用如person('Adam', 45, gender='M', job='Engineer')
	
	命名关键字参数为分隔符*之后的参数def person(name, age, *, city, job)，必须这样调用person('Jack', 24, city='Beijing', job='Engineer')，如果函数定义中已经有了一个可变参数，后面跟着的命名关键字参数就不再需要一个特殊分隔符了：def person(name, age, *args, city, job):，命名关键字参数传入时必须带有参数名，命名关键字参数也可设置默认值def person(name, age, *, city='Beijing', job):

各类型顺序必须是：必选参数、默认参数、可变参数、命名关键字参数和关键字参数

递归函数：函数中调用函数本身，

切片：L[a: b: c]从a到b（左闭右开）每c个取一个

tuple和str也可切片，结果还是原类型

for in迭代dict默认是迭代key

迭代dict的value：for value in d.values()

迭代dic的key、value：for k, v in d.items()

下标循环：for i, value in enumerate(['A', 'B', 'C']):

引用多个变量的循环：for x, y in [(1, 1), (2, 4), (3, 9)]:

列表生成式：[x * x for x in range(1, 11) if x % 2 == 0]，[m + n for m in 'ABC' for n in 'XYZ']

列表生成器：可动态的生成列表中的元素，节省内存空间

列表生成器(generator)创建方式

	将列表生成式外面的[]改为()
	
	定义generator函数

变量互换：a, b = b, a

Iterable包括list、tuple、dict、set、str

Iterator包括generator

Iterator是惰性求值的

可使用iter()函数将Iterable转换为Iterator

Iterable和Iterator都可使用for，只有Iterator可使用next()

map()的返回值类型是Iterator

reduce()的回调函数接受两个参数，类似斐波那契数列，返回值类型是list元素的类型

sorted()函数第二个命名关键字参数，将原来的元素映射为可排序的

匿名函数 lambda x: x * x 仅可有一个不需要写return的表达式

装饰器@可调用高阶函数修改函数定义

偏函数functools.partial的作用就是，把一个函数的某些参数给固定住（也就是设置默认值），返回一个新的函数，调用这个新函数会更简单。

目录下必须有\_\_init\_\_.py才是包，\_\_init\_\_.py即是该包的模块

任何模块代码的第一个字符串都被视为模块的文档注释；

类的定义：class Student(object):

构造函数：def \_\_init\_\_(self):

实例的变量名如果以`__`开头，就变成了一个私有变量（private），只有内部可以访问，外部不能访问

查看类型：type()

查看继承关系：isinstance()

实例属性通过构造函数中定义self.name = name，类的属性直接写，类属性通过实例直接调用，为共享的，先看实例有没有，没有 就调用类属性

给对象绑定方法后所有实例都可使用

可通过\_\_slots\_\_ = ('name', 'age')限定类的实例可绑定的属性

可通过装饰器@property、@xxx.setter定义访问器

可多重继承class Dog(Mammal, RunnableMixIn, CarnivorousMixIn):

try语句块：

```
try:
    print('try...')
    r = 10 / 0
    print('result:', r)
except ZeroDivisionError as e:
    print('except:', e)
finally:
    print('finally...')
print('END')
```

抛异常：raise

with语句块：

```
with expression [as variable]:
    with-block
```

表示通过expression内置的打开退出异常处理，运行with-block

import Module (as name) ：引入模块

from Module import Func/Class：从模块中引入函数、类

from Module import * 引用模块中所有公开成员

元组赋值：

赋值语句中右边会被转换为元组，故左边可用逗号分隔，接受元组中的值

enumerate函数将可迭代对象的项转换成下标和项的元组，常用于循环：

```
for i, element in enumerate(seq):
```

---

\_\_call\_\_

Python中的函数是一级对象。这意味着Python中的函数的引用可以作为输入传递到其他的函数/方法中，并在其中被执行。 而Python中类的实例（对象）可以被当做函数对待。也就是说，我们可以将它们作为输入传递到其他的函数/方法中并调用他们，正如我们调用一个正常的函数那样。而类中`__call__()`函数的意义正在于此

---

**super()** 函数是用于调用父类中已被覆盖的一个方法, 主要用于处理多重继承的问题，init中不一定要写

---

类的方法与普通的函数只有一个特别的区别——它们必须有一个额外的第一个参数名称，但是在调用这个方法的时候你不为这个参数赋值，Python会提供这个值。这个特别的变量指对象本身，按照惯例它的名称是self。

---

a ** b 为幂运算符

---

一切皆是对象

---

任何一个py文件都是一个模块

py文件顶层的变量称为模块的属性，import XX 为导入的模块，可通过XX.yy使用模块的属性，或通过from XX import yy 直接导入模块的属性

字符串可通过 * 进行重复

字符串具有不可变性

可用于多种类型的操作通常是表达式或内置函数 len(x)，特定类型的操作往往是方法调用 s.upper()

list 可通过 + 拼接

列表中禁止给越界的下标赋值

分数类型Fraction

---

数字类型包括：整数和浮点数，复数，固定精度十进制数，有理分数，集合，布尔型，无穷的整数精度，其它内置类型

8进制 0o； 16进制0x；2进制0b

科学计数法：4e210或4e+210，e可大写

复数：3+4j，j可大写

---

三元运算符：x if y else z

在数字类型计算时，遵循低类型自动升级

---

变量定义时不一定要赋值，在它第一次赋值时被创建，未赋值的变量不可使用

可通过连写进行范围判断：x < y < z

// 是严格的取小于而不是截断

进制转换、位操作仅能作用于整数

使用小数对象 from decimal import Decimal 能够解决浮点数不精确的问题

使用 decimal 内置模块时可设置上下文精度

decimal.getcontext().prec = 2

常用with语句

with decimal.localcontext() as ctx:

  ctx.prec = 2

集合中只可添加不可变对象

集合 有去除后者有 - ，并 | ，交 &，相异部分 ^，判断是否包含< > 

True 和 False 本质上是 1 和 0 ,所以 True == 1 True + 4 == 5

对于小数字和字符串，两个分别建立的相等是因为有缓存复用

---

三个引号表示多行字符串，结果每行间将有换行符。由于没有多行注释，直接在脚本中出现的三引号块也被兼做多行注释

转换为字符串 str()

转换为整型 int()

获取ASCII码 ord()

将ASCII码转为字符 chr()

格式化表达式今后可能废弃，建议使用格式化方法

---

主要类型分类为数字、序列、映射三种，也可按可变类型和不可变类型分

---

list也可以用 + * 进行拼接和重复

---

字典的 D.keys()  D.values()  D.items() 返回结果都是迭代器，外面需套list()。D.items()元素为元组，

字典的键可以为任何不可变对象

字典的特殊构造方式：

dict(name='mel', age=45)  键只能是字符串

dict(('name', 'mel'), ('age', 45))

dict.fromkeys(['a', 'b'], 0)  传入键的列表，和所有值的默认值

D = {k: v for (k, v) in zip(['a', 'b', 'c'], [1, 2, 3])}  解析表达式

---

一组直接用逗号隔开的对象表示元组定义

---

文件通过内置open函数打开，参数 w 指写入，r 指读取， +指读写

b指二进制，文本文件内容为str字符串，自动执行Unicode编码和解码和末尾换行，二进制为特殊的bytes字符串类型，可以不修改的访问

pickle 是用来序列化与解析文件内容到python对象的工具

---

== 检验相等性，is 检验一致性

---

真假的概念是每个对象的固有属性，对于数字对象，0为假，其它为真；对于非数字对象，空为假，非空为真

None是一类特殊对象的唯一值，永远为假，不代表未定义

真假的本质是整数1和0，bool类型是对其的包装

类型也是一类对象，内置类型标准名称为dict, list, str, tuple, int, float, complex, byte, type, set, file，可用同名的函数来定制类型

赋值语句是引用而不是拷贝

---

由于GIL（global interperator lock）的存在，python的多线程不能利用多核，利用多核需使用多进程multiprocessing

---

赋值语句特殊形式

spam, ham = 'yum', 'YUM'  元组赋值

[spam, ham] = ['yum', 'YUM']  列表赋值

a, b, c, d = 'spam' 序列赋值，最好还是用分片

a, *b = 'spam' 序列的解构赋值

连续赋值的顺序同js

---

以单一下划线开头的变量不会被import * 语句导入

前后有双下划线的是系统定义变量名

双下划线开头但没有结尾的是类的本地变量

---

对象是强类型，但变量名没有类型，可以任意改变变量名关联到的对象

---

表达式可作为单独的语句，但语句不可作为表达式

print调用格式print(a, b, c, sep=' ', end='\n', file=sys.stdout)，注意默认的输出分隔符是空格，可通过设置end取消输出的换行

---

复合语句的通用形式是

首行 + ： + 缩进的语句块，结束缩进代码复合语句结束

---

bool()函数会将值转换为1或0

and or 具有和js类似的短路赋值

---

while语句中的else 是当循环自然退出（不是break）时触发（包括一次都没有执行），常用来表明循环没有全部成功走完没有被打断

---

pass用来对空函数体和空循环分支占位，空函数体会报错，也可用 ...来替代

---

只有for in 一种for循环，从可迭代对象中取值，for循环也可有else

in后面常跟range实现类似的效果

---

for循环搭配zip可以实现并行迭代

通过 dict(zip(ks, vs))可将键序列与值序列归并成字典

---

enumerate函数将可迭代对象返回(index, value)的元组

---

可迭代对象内部包含\_\_next\_\_方法，可通过内置方法next()调用，不是可迭代对象的可用内置函数iter()转换成可迭代对象

---

列表解析是构造列表的一种更快的方式：L = [x + 10 for x in L v]

---

dict 的keys，values，items都返回可迭代对象，iter(D) 返回键的可迭代对象

---

def 定义函数的语句是实时执行的，即要执行到该句才有函数的定义

---

由于变量没有声明，所以给一个变量赋值的地方决定了它的作用域

---

在函数中定义的变量与在外面定义的变量不冲突，是完全不同的变量

---

所有的代码都属于模块（即单个文件），全局作用域指的是模块顶层，并不存在真正的“全局”，命令行下是属于一个叫\_\_main\_\_的内置模块

函数的调用创建本地作用域

所有变量的作用域分为全局、本地、内置

---

变量名解析顺序是LEGB：本地、闭包、全局、内置（包含各种内置异常和函数，包名builtins)

使用 nonlocal 可以对上一层本地作用域的已定义变量修改状态

---

函数参数，不可变对象通过值传递，可变对象通过指针传递

---

参数匹配

调用时，可通过

func(value) 位置

func(name=value) 变量名

func(*sequence) 解析序列

func(* dict) 解析键值对

的方式传递参数

定义时

def func(name=value) 表示参数默认值

def func(*name) 表示收集所有剩余参数为元组

def func(**name) 表示收集所有剩余键值对为字典

调用顺序：位置参数在最前面，\*\*dict在最后面，中间是关键字参数和\*sequence

定义顺序：一般参数——默认值参数——\*name——keyword-only参数——\*\*name

---

keyword-only参数指定义时\*args或\*和\*\*name之间的所有参数，调用时不会被位置参数填充，只能以关键字参数传递

---

可以给函数添加属性，类似js

---

注解仅可应用在def语句中，不可应用在lambda表达式中，

参数的注解用冒号紧跟在参数名之后，返回值的注解用 -> 紧跟在参数表之后

可通过函数名.\_\_annotations\_\_获取注解字典

---

lambda 是一个表达式而不是一个语句

lambda 冒号后的主体是一个表达式而不是一个代码块

---

map, filter是内置函数，返回迭代器

reduce不是内置，需from functools import reduce

它们三者参数顺序都是先函数，后数组

---

列表解析式写在一个括号中称为生成器表达式，返回一个迭代器

---

可通过start = time.clock()  elapesd = time.clock() - start来计时

在win平台上time.clock() 最好，可达到微妙精度，在一些UNIX平台上time.time()更好

CPU time(execution time) 指CPU花在执行程序上的时间

wall-clock time指执行程序消耗的总时间，CPU可能穿插执行了其它程序的指令，所以CPU time比wall-clock time大

---

没有return的函数返回None

---

import 搜索顺序：项目主目录，PYTHONPATH目录，标准库目录，.path文件目录

import 语句导入时会刻意忽略后缀名，根据实际情况导入不同的类型

import 语句是可执行的语句，而不是编译期的声明，可出现在if、def之中

---

python 中含有\_\_init\_\_.py的目录称为包，包导入类似Java

一条路径除了第一个目录外，每一个都必须有\_\_init\_\_.py

首次导入某个目录时，会执行\_\_init\_\_.py中的代码

可在\_\_init\_\_.py文件中使用\_\_all\_\_列表类定义from \*语句导出什么

使用 . 或多个 . 开头的包名为相对导入，只可应用于from语句

\_ 开头的私有属性和\_\_all\_\_是模块的私有策略，但它们只作用于from \*语句

模块的属性\_\_name\_\_当模块被当做顶层脚本执行时值为\_\_main\_\_ 因此模块末尾可用\_\_name\_\_ == ‘\_\_main\_\_’ 来添加测试代码

可用as 为导入的模块重命名

---

class 语句和def语句类似，是可执行语句,不存在提升，一般在所在文件导入时执行，它执行时产生新的类对象，并赋值给class头部的变量名

class语句中顶层赋值语句产生类对象的属性，类似模块，class语句的作用域会变成类对象属性的命名空间

类对象的属性为所有实例共享，类中的def语句生成方法

---

每个实例继承类的属性并创建自己新的命名空间

对self的赋值运算产生对象的属性

---

类可以重载运算符，运算符对应一系列类似\_\_add\_\_的特殊钩子函数

---

不对实例的属性进行声明，但可以在构造函数中了解有哪些属性

---

实例的\_\_class\_\_属性指向类

类的\_\_bases\_\_指向父类们的元组

---

重写toString的方法是\_\_str\_\_(self)

---

对象的序列化使用pickle

---

类的属性，实例也可以直接用x.att形式直接调用，但那是类的属性，是共享的

继承搜索只会在属性引用时发生，对实例属性进行赋值会在该实例内创建或修改变量名，而不是在共享类中

---

类的实例方法，当以实例加点号的形式调用的时候，会将实例作为第一个参数传入，实际参数表从第二个开始，即 instance.method(args...)等价于Class.method(instance, args...)

类的实例方法第一个传入的参数必须是该类的实例，否则会报错

类的静态方法和类方法（第一个参数是该类对象cls）通过注解@staticmethod和@classmethod定义

---

多重继承的方法解析顺序是一个名为MRO的列表，其构成方法基本为深度优先，然后去处后面还有子类的项，然后在执行线性结果merge的结果（一般不循环交错的可以理解为就是深度优先）

---

现在无绑定的方法就是函数

---

try/except/else语句中else表示没有异常会执行的代码，except没有数量限制，但else只能有一个

except 后面跟异常类型，可为元组，空为所有异常，as后面为异常对象的值 except ErrorType as e:

raise 可跟实例、类，如果空表示抛出最近一个异常，常用于except

raise的from字句后面跟的异常将添加到前一个异常的\_\_cause\_\_属性，形成异常链

assert \<test\>, \<data\>表示断言失败抛出异常，是raise常用的一种简写

with语句可打开支持环境协议的对象，注意as后面跟的不是with语句的返回（with语句返回是环境对象）

with语句可跟多个用逗号隔开的表达式

except检测异常对象是基于继承的，即可被父类检测捕获

自定义异常类需继承自内置异常类，BaseException是最顶层的但不可直接继承，一般直接继承和全判断用Exception

定制异常类信息重写\_\_str\_\_(self)方法，还可定制一些异常处理方法

一个异常只会被第一个符合的except捕获到，故安排捕获异常的顺序，特殊先于一般

---

处理二进制序列用bytes或bytearray对象

















# python3改动

xrange与range合并为range

zip返回值要加个list（）

整型与长整型合并，8进制不可只加0

集合可通过{1, 2, 3}的字面量创建

字典不可比较大小，没有has_key

cPickle 变成了pickle

dic.iteritems 改名为 dic.items



# PEP

函数的形参表换行要缩进两次，调用处只要缩进一次，或参数对齐

if条件换行也可缩进两次

顶层函数和类间隔两行，函数或类内部间隔一行

前后双下划线的变量定义要在import之前，\_\_future\_\_之后

切片中的冒号，两边空格量要相等，如果参数没有了，对应空格也不要

函数参数表中的等号不要空格，但有注解的参数等号加空格，注解冒号后加空格

多分支的模块的字句要重启一行

多行的列表元素、参数等最后一个元素的逗号不要省

注释块开头的三引号后不换行

变量名下划线意义：

前单：模块内部变量，类内部变量

后单：避免与关键字冲突

前双：触发自动类名前缀，常用于供继承的抽象类中不希望子类使用的变量

前后双：内置变量，避免自创

模块使用小写下划线命名，包名小写避免下划线，

类名大写驼峰，但如果常被当做函数调用，也可按函数的规则

类型变量用尽可能短的大写驼峰

异常类大写驼峰并常用Error结尾

函数和变量小写下划线

方法中的指针参数名为self、cls

常量大写下划线

模块的对象接口都应该在\_\_all\_\_中列出

当判断是否为None时，使用is或is not

判断为True或False时，用==或直接if

具名的函数用def而不要用lambda

return的结果类型要统一，不要有时返回有时不返回或返回异常类

使用字符串方法而不是字符串模块

比对列表开头结尾时用startwith() 和endwith()而不是切片

对比对象类型用 isinstance 而不是type()

注意空的序列等价于False

注解后面的等号两边没有空格