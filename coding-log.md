**javascript**

**vue**

**git**

**css**

**html**

**browser**

**webpack**

**react**

**npm**

**vpn**

**react-native**

**dom**

**设计**

**markdown**

**echarts**

**node**

**http**

**mobx**

**babel**

**styled-components**

**redux**

**fetch**

**构建**

**android**

**amap**

**IoT**

**vscode**

**dart**

**flutter**

**shadowsocks**

**ble**

**weixin**

**typescript**

**linux**

**jest**

**算法**

# 2019-01-08

**javascript**

父类构造函数有参数的，记得子类构造函数用...args传给super

# 2019-01-15

**javascript**

import中.js后缀名是否省略，文件夹是否默认导入index.js不是由标准决定的，airbnb认为文件不加后缀名是最佳实践，node中有自动识别index.js的功能，但deno不推荐这样做

# 2019-01-16

**javascript**

在浏览器中，如果script标签引入的是module，要加type="module"，import中模块不可省略后缀名，也没有默认的index.js

浏览器加载中的import文件一定要放在服务器上不能直接通过文件系统，这样会引发跨域错误

# 2019-01-17

**javascript**

特别注意当作为表达式时，a++的值为加之前的，a+=1的值为加之后的，++a为加之前的

**vscode**

在debug配置中，传给启动程序（比如node）的参数给runtimeArgs，传给脚本（比如index.js）的参数给args

# 2019-01-20

**javascript**

ArrayBuffer构造函数传入的是字节数，如果传入的参数大，可能会分派失败

通过给TypedArray传入另一个TypedArray的方式的构造函数，底层是一个新的ArrayBuffer，如需同一个ArrayBuffer，可传入typedArray.buffer

TypedArray与普通数组比，没有concat

x86 体系的计算机都采用小端字节序，TypedArray 数组内部也采用小端字节序读写数据，或者更准确的说，按照本机操作系统设定的字节序读写数据，如要设定字节序用DataView

`TypedArray`视图，是用来向网卡、声卡之类的本机设备传送数据，所以使用本机的字节序就可以了；而`DataView`视图的设计目的，是用来处理网络设备传来的数据，所以大端字节序或小端字节序是可以自行设定的

# 2019-01-21

**javascript**

ArrayBuffer构造函数传入的字节数如果大于1E9，视图获取length会失败

# 2019-02-03

**git**

git bash 中如果要执行.bat需加上XX.bat

# 2019-02-26

**react-native**

很多老版本的库其原生依赖jcenter中可能没有了，需手动进入其源代码添加优先的google()

**android**

AndroidManifest中有uses-sdk标签指定android:minSdkVersion和android:targetSdkVersion

# 2019-02-27

**git**

git add 只会添加当前目录及子目录的内容，如要添加仓库所有改动，确保在根目录下执行

**android**

26版本之后，关键权限一定要求用户在App中确认了

# 2019-05-17

**javascript**

call 从第二个起的参数表将直接作为函数参数表，而apply则是将第二个参数数组的元素作为参数传给数组

call(this, a)    f(a)

apply(this.a)    f(...a)

---

concat(values1, values2)的作用：如果values不是数组，则放到原数组后面，是数组则取出元素放到数组后面，