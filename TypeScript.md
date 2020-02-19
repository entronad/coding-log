ts package的特点：

完成后的package只有是js文件，方便不是用ts的项目使用，同时代用x.d.ts类型定义文件



typescript模块与es模块一样



类成员有public private protected 关键字修饰，有抽象类，有getter、setter定义

抽象类中的抽象方法前面也加关键字 abstract



const应用于变量，readonly应用于属性



类中也习惯先写成员后写构造函数



可以使用箭头函数，在类中使用箭头函数绑定this



函数的返回值类型可自动推断，故一般省略



ts中数组的定义类型和初始化不好合成在一起，需单独指定，特别是数组要记得指定



ts/js中目前没有注解，没有@overrides



不能在静态属性初始化表达式中引用 "this"



声明.d.ts文件是为js库加上类型应用到ts项目中用的，详情见https://ts.xcatliu.com/basics/declaration-files#npm-bao

type 关键字类似于 interface 关键字，但用来定义较为基础的类型

对于声明文件中要定义类，静态部分和实例部分要分开定义

在 npm 包的声明文件中，使用 `declare` 不再会声明一个全局变量，而只会在当前文件中声明一个局部变量。



interface 如果需要构造函数、keys等接口时可 extends Object



declare class 不需要返回类型



impliments 就能起到 mixin 的作用