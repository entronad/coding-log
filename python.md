布尔值关键字为 True False

逻辑运算关键字为 and or not

空值 None

精确除法 / ; 取整除法 //

模板字符串 '%d %f %s %x' % (1, 1.2, 'aaa', '0x16')

列表分为list和tuple

获取list长度 len()

获取list最后一个参数 datas[-1]，导数第二个 datas[-2]

list操作方法：

​	末尾增加 datas.append(data)

​	指定位置插入：datas.insert(index, data)

​	删除末尾：datas.pop()

​	删除指定位置：datas.pop(index)

list中数据类型可不同

tuple是不可变的list

tuple定义：(1, 2, 3)

仅一个元素的tuple：(1.2, )

冒号与缩进表示代码块，缩进多少不做规定

条件判断：

if a > b:

​	a++

elif:

​	b++

else:

​	c++

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

​	return 0

暂时空缺的语句块可以用pass占位

函数可以返回多个值，本质上是构成了一个tuple

可用power(x, n=2)的形式定义默认参数

如调用函数时不是按顺序省略参数，可用如下形式enroll('Adam', 'M', city='Tianjin')

默认参数必须指向不变对象，否则多次调用函数且修改参数时可能存在问题

参数类型：

​	一般的参数叫做位置参数，通过在参数表中的位置表明关系

​	可变参数定义函数calc(\*numbers)会将传入的多个参数组成tuple，在调用时calc(\*[1,2,3])表示将该list作为可变参数传入

​	关键字参数定义函数def person(name, age, **kw):会将传入的键值对作为dict传入，调用如person('Adam', 45, gender='M', job='Engineer')

​	命名关键字参数为分隔符\*之后的参数def person(name, age, \*, city, job)，必须这样调用person('Jack', 24, city='Beijing', job='Engineer')，如果函数定义中已经有了一个可变参数，后面跟着的命名关键字参数就不再需要一个特殊分隔符了：def person(name, age, \*args, city, job):，命名关键字参数传入时必须带有参数名，命名关键字参数也可设置默认值def person(name, age, *, city='Beijing', job):

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

​	将列表生成式外面的[]改为()

​	定义generator函数

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