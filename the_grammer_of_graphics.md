graph源自希腊动词写作，它也是grammar的词源

grammar广义上指rules for art and science

graphic是perceivable的graph。graph是指抽象的点的集合，不可见，graph添加了 aesthetic attributes之后是graphic

aesthetic在希腊语本意是提供principles for relating sensory attributes(color, shape, sound) to abstractions.

创建graphic的三个主要步骤：specification, assembly, display

specification的6个表述：data, trans, scale, coord, element, guide

lexcial 词法 syntax 句法 semantic 语义

**定义**

graph：{(a, f(a)): a in A} 函数输入与输出构成的tuple的总集合

composition 函数的串联

transformation 定义域与值域相同的函数

algebra 集合、集合的操作，集合操作合并的规则

variable 对象到值的映射，连续的值为continuous 有限整数值为categorical

varset variable反过来，值到对象的映射

frame 多维varset所有可能的tuple的集合

---

data是symbolic representations of observations or thoughts about the world

data大致分为三类：empirical, abstract, meta

empirical 是collected from observations of the real world 即我们通常意义上的data，处理empirical data的函数有col、map、stream、image、sample、reshape等

Abstract data 是arise from formal models 即m、n等，处理函数有iter、count、mesh、rand等

metadata 是 data on data 

---

reshape是将不同形状的data变成column，它后面跟的函数名是data本来的形状

---

transform 是 transformations on variables 有mathematical, statistical, multivariate（多元）等类型

---

corss(\*)和nest(/)的区别，

A\*B的可能域结果是A与B所有可能的组合，

A/B的可能域要剔除两者没有交集的情况，含义是a whithin b

blend(+)指取并

理论上只要以上三种运算就可以了，还有以下简写：

exponentiation(^)是多次cross的缩写

dot-cross(·)是对应元素cross

三者对应的sql：

```
#cross:
select a.*, b.*
from X a, Y b;
where a.key = b.key;

#nest:
select a.*, b.*
from X a, Y b;

#blend:
select * from X
union all
select * from Y;
```

---

cross, nest, blend 都满足结合律

cross, nest 满足分配律

0元素是空集，单位元素是所有肯能情况的集合

没有交换律

---

symbol 和 operator的组合称为expression，没有+的expression称为term，没有 *的term称为factor，只有一个term的expression称为monomial，不止一个term的expression称为polynomial

algebraic form指所有term的factor数量一样的expression，此数量称为其order

---

运算符的优先级顺序是 nest > cross > blend

---

轴可分为以下几类：norminal, ordinal, interval, ratio

---

variable、scale、coordinate 都可以进行 transform

---

直方图 histogram 虽然长的像 bar interval ，但它不是，它是统计学的概念，其面积是表意的

---

因为path可以用参数方程表示，所以被划分到function中而不是network中

---

stack的含义是下一个开始值是前一个的值而不是0