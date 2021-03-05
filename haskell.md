函数式的基础是 lambda演算 （lambda calculus）

类型相关的首字母都大写

非是 not

Char 单引号是字符类型

Int 有符号整数，范围由操作系统和 GHC 确定

Word 无符号整数，需要导入 Data.Word 库

Integer 任意精度整数，但要注意性能低于 Int

此外在 Data.Int 和 Data.Word 中还有 Int8, Int16 等特殊类型

Float，Double 为小数，Rational 为有理数类型，用两个 Integer 来表示小数 4 % 3

String 是 [Char] 的别名，可以用双引号括起来

() 元组类型，一旦确定个数和类型不可变，最多支持 62 个元素

以元组作为输入参数的称为非柯里化函数，而定义多个参数的函数如果传入参数不足，会返回函数作为结果，称为柯里化函数

多态函数：一个函数的某个参数可以是任何类型，用小写字母开头的标识符表示并可作为类型变量 :: [a] -> a

重载字面量：可以理解为多种类型的字面量 :: Num a => a

重载函数：相同名字的函数传入的参数类型或个数不同有不同的实现

可用 type 关键字定义类型别名

/= 不等于

Eq 相等类型

Ord 有序类型，属于相等类型

Enum 枚举类型，可按顺序枚举，... 表示列出中间全部，succ，pred 表示前一个后一个

Bounded 有界类型，实现了 maxBound，minBound

Num 非常全面负责，有的要从 Data.Complex, Data.Ratio 中导入

小数乘方 \*\*

复数 5:+5

不同数的类型需要用 fromRational, toRational 的转换函数

NaN，根据 IEEE 规定，它与任何数包括它自身都不相等，可用 RealFloat 中的 isNaN 判定是否为NaN

Show 可打印类型，函数不是可打印类型

-> 是一个向右结合的符号，即 a -> a -> a 等价于 a -> (a -> a)

函数定义一般先写类型签名，再写函数定义。也有类型推导。函数类型签名也可用逗号分隔多个一起定义。

类型签名中，柯里化函数多个参数用 -> 连接。

多个类型类限定一个类型时，用类似元组的写法或 => 连接 (Show a, Ord a) => a 或者 Show a => Ord a

.hs 文件中全局函数名必须从每行最前端开始写

函数定义与 lambda 表达式

```
f x y = 4 * x + 5 * y + 1
f = \x -> \y -> 4 * x + 5 * y + 1
f = \x y -> 4 * x + 5 * y + 1
```

lambda 表达式的每一项和类型定义一一对应

lambda 表达式优先级的原则是尽可能向右延伸直到碰到不平衡的右括号（代表这个括号在 lambda 表达式之外开始的）

alpha 变换：变量名不重要

beta 规约：传入参数调用函数，等价于将函数体中的形参替换为该参数

eta 变换：函数是同一个函数等价于对于任意输入结果相同

表达式或函数中绑定参数用 let in ：

绑定多个变量 let x=2; y=2 in x+y

绑定函数 let f x = x + 1 in f 5

或 where，where只能用于函数中 f = x + y where x=2; y=2

条件表达式 if then else，注意else后不可省略。它更像三目运算符而不是控制语句

分情形表达式 case of。注意它不会进行到下一条不需要break，默认用通配符 '_'，不可省略。每个分支返回值用 ->

卫语句用 | 注意要对齐，默认定义用 otherwise ，同时满足条件匹配第一个

可以连写多个函数定义模式匹配

函数名后面跟空格和参数表示调用 (+) 5 6

可以用反引号包起二元函数在两个参数之间调用： 5 \`div\` 2

运算符有三个属性：优先级 precedence 结合性 associativity 位置 fixity

优先级 0-9 共10个

函数可以认为是一个最高优先级，左结合的运算符

!! 表示从列表中取出第 n 个元素

^ 表示底数任意，指数为整数的乘方

^^ 表示底数必须为 Fractional ，指数为整数的乘方

** 表示底数指数都为 Floating 的乘方

Haskell 中有大量的中缀运算符，注意勤加括号防止优先级问题

: 元素列表连接运算符，表示将左边的元素添加到右边列表的第一个位置；在函数参数定义tuple中，左右分别指代列表的第一项和余下的项

符号除减号外都是中缀运算符，中缀运算符需要考虑结合性

猜想：应用式中只有两种东西，函数（变量），运算符（中缀，优先级0-9），函数与函数间填充调用运算符（中缀，最高优先级），运算符两侧不要填充

猜想：结合性定义是多个连续的同优先级的运算符，从左往右算还是从右往左算

a \`op\` b 应用式可以转换成 (op a) b，注意括号体现的优先级

函数应用为左结合，即 f g h 意为 (f g) h

-> 符号为右结合，即 a -> b -> c 意为 a -> (b -> c)

Haskell 中可定义自己的运算符，但不可改变现有运算符，定义时需指明结合性（infixl, infixr, infixx）和优先级

模块的导出：module Test (f1, f2) where 可以导出函数和类型，如果没有括号则所有都导出，如果空括号或没有此行则都不导出

模块的导入：import (f1) 如果要隐藏一些，用 hiding (f1)，如果要重命名 import qualified Test as T

常用函数：

id 恒值函数，返回输入

const 常值函数，给定两个元素，只返回第一个

const id 返回两个参数中的第二个

flip 将二元函数参数反置调用，它是一个三参数的函数

error 异常函数，输入是 String，返回是多态类型

undefined 未定义，用来占位尚未定义的函数

null 判断列表是否为空

length 列表长度，返回值是Int，所以太长的列表要使用 Data.list 中的 genericLength

注意求一组数字的平均值要用：avg xs = sum xs / (fromIntegral $ length xs) 或者 avg xs = sum xs / genericLength xs

init, tail 将一个列表的最后一个元素与第一个元素去掉得到一个新的列表

map 类型是 (a -> b) -> [a] -> [b]

递归函数本身之外还有值参与运算的 x + f x 称为扩展递归（augmenting recursion），递归函数本身之外没有其它运算（调用时可以串联其它函数）的 f (x + 1) 称为尾递归（tail recursion）。尾递归不用记录每步的中间值比较节省内存

两个递归函数定义中都用到了对方称为互调递归（mutual recursion）

存在一类递归函数，目前不能证明它一定会终止，但它确实会终止，称为考拉兹猜想

不动点指的是函数中输入和输出相同的点，不动点函数 fix 可以用来获得函数的不动点，它可以用来使得递归函数中不用使用自身函数名

列表生成式：[exp | q1, ... qn] q 可以是生成器：x <- [0..100]

foldl, foldr 可以起到 reduce 的作用

. 复合函数（composite function）符号，(f.g) x 等价于 f (g x) 或 f $ g x。注意由于函数调用优先级高于符号，所以要加括号

data 定义类型的关键字

| 枚举定义类型，注意每个值都是大写

deriving 定义继承的类型

() 被称为单位类型或哑元类型，这个类型只有一个值 ()

当类型中的某些数据需要其他类型作为参数时：data Book = Book Name Author 其中第二个 Book 称为数据构造器，首字母大写的特殊函数。即类型定义式中可以凭空出现大写字母的，它是定义构造器函数，后面跟的是输入参数类型

访问器函数可以方便的定义：

```
data Book = Book {
  name :: Name,
  author :: Author
}
```

name 的类型是 Book -> Name

定义了访问器的类型可直接操作：

```
increasePrice :: ([Book], [Book]) -> Book -> Price -> ([Book], [Book])
increasePrice (b1, b2) b pri = (b: b1, (b {price = pri + (price b)}) : b2)
```

data Maybe a = Nothing | Just a 其中 Just 是一个构造器，输入a类型变量返回 Maybe a 类型变量

data Either a b = Left a | Right b 其中 Left 和 Right 也是构造器

定义式中出现要定义的类型称为递归类型，比如自然数：data Nat = Zero | Succ Nat deriving (Show, Eq, Ord)，使用递归类型的函数常常是递归函数

类型的类型称为 kind，所有类型的类型通常写作 \*

类型同构（isomorphism）指的是两种类型能找到同构映射，同构映射指的是能找到一个映射（称为逆）与其进行复合后是恒值映射

同构具有自反、对称、传递的性质

两个个数一样的枚举是同构的，基数（cardinal number）相同的无穷多个也是同构的

newtype 也可定义类型，但有且只能有一个参数

类型类的关键字是class，但它与OO中的class完全不一样

如果类型类有依赖（约束）关系，用 => 关键字：class Eq a => Ord a where

类型实现类型类就是实现其中的函数声明，用 instance，先写类型类再写类型：instance Show Weight where

类似可以定义 map 函数的 List 这种的称为函子（Functor）类型，它需要定义一个 fmap ，同时满足：

应用恒值映射作为 fmap 后和原来一样，在复合函数运算符上服从分配律

默认的 String 类型是字符的单链表，某些情况不高效，因此 Data.String 中还有 ByteString，Text 等类型，他们的类型类是 IsString

7.8以前 Applicative 不是 Monad 的超类，现在是了。pure 和 return 是一样的，一般 pure 好， do notation 习惯用 return

\>\>= 被称为 bind

**由于柯里化的存在，函数是可组合的，一个函数的”参数类型“和”返回类型“是动态的，比如 add，两个数相加得到一个数 num -> num -> num，可转变为” add 传入一个数得到 num-> num 类型的函数“，从另一个角度讲，也可理解为” 一个需要num 的函数，可以以 add 作为参数，这样输入端还需要一个num以便add获得num，这样得到的 结果是一个 num->num 的函数“ ，所以认为函数都是有且仅有一个输入输出的就好理解**

函子相关白话解释：

pure/return 从内容获取容器的函数

$ 函数，应用到参数上，得到新的返回

\<\$\> 输入内容返回内容的函数，应用到容器上，得到新的容器

\<\*\> 输入内容返回容器的函数，应用到容器上，得到容器

\*\> 两个容器都算一下，返回右边的

\<\* 两个容器都算一下，返回左边的

LiftA 就是 \<\$\>

LiftA2 第一个函数是二元的输入两个内容返回一个内容，后面跟两个容器

empty 定义空的容器

\<|\> 两个容器中选出需要的那个容器，**注意前面几个运算符两遍内容类型可以不一样，这个两边必须一样**

\>\>= 容器，内容到目标容器的函数，返回目标容器

\>\> 同 \*\>

Functor，Applicative，Monad 不仅仅要实现函数，还要满足相应的定律才是

列表满足monad定律，是monad

MonadPlus 就是 Alternative

对于纯函数，函数调用可以直接被结果代替，称为引用透明性（referential transparency）

