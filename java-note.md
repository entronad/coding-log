抽象类命名使用Abstract或Base开头

POJO类中布尔类型的变量，都不要加is

包名统一使用小写，点分隔符之间有且仅有一个自然语义的英语单词。包名统一使用单数形式，但是类名如果有复数含义，类名可以使用复数形式

如果使用到了设计模式，建议在类名中体现出具体模式

接口类中的方法和属性不要加任何修饰符号

对于Service和DAO类，基于SOA的理念，暴露出来的服务一定是接口，内部的实现类用Impl的后缀与接口区别。如果是形容能力的接口名称，取对应的形容词做接口名（通常是–able的形式）。

枚举类名建议带上Enum后缀，枚举成员名称需要全大写，单词间用下划线隔开

【参考】各层命名规约： A) Service/DAO层方法命名规约 1） 获取单个对象的方法用get做前缀。 2） 获取多个对象的方法用list做前缀。 3） 获取统计值的方法用count做前缀。 4） 插入的方法用save（推荐）或insert做前缀。 5） 删除的方法用remove（推荐）或delete做前缀。 6） 修改的方法用update做前缀。 B) 领域模型命名规约 1） 数据对象：xxxDO，xxx即为数据表名。 2） 数据传输对象：xxxDTO，xxx为业务领域相关的名称。 3） 展示对象：xxxVO，xxx一般为网页名称。 4） POJO是DO/DTO/BO/VO的统称，禁止命名成xxxPOJO。

long或者Long初始赋值时，必须使用大写的L，不能是小写的l，小写容易跟数字1混淆，造成误解。

不要使用一个常量类维护所有常量，应该按常量功能进行归类，分开维护。如：缓存相关的常量放在类：CacheConsts下；系统配置相关的常量放在类：ConfigConsts下。

任何运算符左右必须加一个空格。

缩进采用4个空格，禁止使用tab字符。如果使用 tab 缩进，必须设置 缩进，必须设置 缩进，必须设置 缩进，必须设置 缩进，必须设置 缩进，必须设置 1个 tab 为 4个空格。 IDEA 设置 tab 为 4个空格时， 请勿勾选 Use tab character

IDE的text file encoding设置为UTF-8; IDE中文件的换行符使用Unix格式，不要使用windows格式。

推荐使用java.util.Objects#equals

关于基本数据类型与包装数据类型的使用标准如下： 1） 所有的POJO类属性必须使用包装数据类型。 2） RPC方法的返回值和参数必须使用包装数据类型。 3） 所有的局部变量【推荐】使用基本数据类型。

类内方法定义顺序依次是：公有方法或保护方法 > 私有方法 > getter/setter方法。

setter方法中，参数名称与类成员变量名称一致，this.成员名=参数名。在getter/setter方法中，尽量不要增加业务逻辑，增加排查问题的难度。

循环体内，字符串的联接方式，使用StringBuilder的append方法进行扩展。

final可提高程序响应效率，声明成final的情况： 1） 不需要重新赋值的变量，包括类属性、局部变量。 2） 对象参数前加final，表示不允许修改引用的指向。 3） 类方法确定不允许被重写。

慎用Object的clone方法来拷贝对象。

如果不允许外部直接通过new来创建对象，那么构造方法必须是private。 2） 工具类不允许有public或default构造方法。

集合初始化时，尽量指定集合初始值大小。

SimpleDateFormat 是线程不安全的类，一般不要定义为static变量，如果定义为static，必须加锁，或者使用DateUtils工具类。

如果是JDK8的应用，可以使用Instant代替Date，LocalDateTime代替Calendar，DateTimeFormatter代替Simpledateformatter，官方给出的解释：simple beautiful strong immutable thread-safe。

推荐尽量少用else， if-else的方式可以改写成：
if(condition){
...
return obj;
}
// 接着写else的业务逻辑代码;

】除常用方法（如getXxx/isXxx）等外，不要在条件判断中执行其它复杂的语句，将复杂逻辑判断的结果赋值给一个有意义的布尔变量名，以提高可读性。

循环体中的语句要考量性能，以下操作尽量移至循环体外处理，如定义对象、变量、获取数据库连接，进行不必要的try-catch操作（这个try-catch是否可以移至循环体外）。

类、类属性、类方法的注释必须使用Javadoc规范，使用/**内容*/格式，不得使用//xxx方式。

所有的抽象方法（包括接口中的方法）必须要用Javadoc注释、除了返回值、参数、异常说明外，还必须指出该方法做什么事情，实现什么功能。

所有的类都必须添加创建者信息。
待办事宜（TODO）:（ 标记人，标记时间，[预计处理时间]）
错误，不能工作（FIXME）:（标记人，标记时间，[预计处理时间]）

注意 Math.random() 这个方法返回是double类型，注意取值的范围 0≤x<1（能够取到零值，注意除零异常），如果想获取整数类型的随机数，不要将x放大10的若干倍然后取整，直接使用Random对象的nextInt或者nextLong方法。

获取当前毫秒数System.currentTimeMillis(); 而不是new Date().getTime(); 说明：如果想获取更加精确的纳秒级时间值，用System.nanoTime()。在JDK8中，针对统计时间等场景，推荐使用Instant类。

任何数据结构的构造或初始化，都应指定大小，避免数据结构无限增长吃光内存。

不要捕获Java类库中定义的继承自RuntimeException的运行时异常类，如：IndexOutOfBoundsException / NullPointerException，这类异常由程序员预检查来规避，保证程序健壮性。 正例：if(obj != null) {...} 反例：try { obj.method() } catch(NullPointerException e){...}