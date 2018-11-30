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

# 2018-01-03

**构建**

在花费时间处理一个性能问题之前，请想清楚你的确是在解决一个确实需要解决的问题。

The best is the enemy of the good.

代码调整步骤：

1. 用设计良好的代码来开发软件，从而使程序易于理解和修改。

2. 如果程序性能很差。

   a. 保存代码的可运行版本，这样你才能回到“最近的已知正常状态”；

   b. 对系统进行分析测量，找出热点；

   c. 判断性能拙劣是否源于设计、数据类型或算法上的缺陷，确定是否应该做代码调整，如果不是，请跳回到第一步；

   d. 对步骤c中所确定的瓶颈代码进行调整；

   e. 每次调整后都对性能提升进行测量；

   f. 如果调整没有改进代码的性能，就恢复到步骤a保存的代码（通常而言，超过一半的调整尝试都只能稍微改善性能甚至造成性能恶化）。

3. 重复步骤2。

# 2018-01-06

**react-native**

react-navigation中，若某个参数可为React Element，必须包裹在jsx中，不可直接引入类。

---

Image组件的图片资源属性为source

# 2018-01-08

**react-native**

WebView中，已自动将px转换为dp渲染

# 2018-01-09

**react-native**

overflow 属性仅适用于IOS，Android将切割子元素

# 2018-01-11

**react-native**

只有在全是\<View>标签的子树中才能继承字体样式

**styled-components**

在react-native不要忘了给组件的根元素添加 style={this.props.style} 才能使得styled()给它传递样式

---

不管是styled()，还是StackNavigator()都不是真正的套了一个组件，需要将有关的样式参数传递参数组件

# 2018-01-15

**react-native**

在 antd-mobile 中，组件会通过 style 属性，或 ...restProps 确保赋给组件的 style 被传递给根元素，故可直接使用styled()

# 2018-01-19

**react-native**

rn中只有Text有点击事件onPress，其他的需要包裹“Touchable...”

# 2018-01-22

**javascript**

要注意 0 的真值为false，故“有数字才显示”需使用value != null

**amap**

所有对象的属性必须使用get函数，不可直接通过marker.XX获取

# 2018-01-22

**styled-components**

在**react-native**中使用时，使用padding 或 margin 时（即合成写法）必须加单位px（其实是dp）

# 2018-01-26

**react-native**

react-navigation的navigator切换screen后并不是进行重新渲染，不会调用mount、update等生命周期方法

---

FlatList的项的点击事件好像只有TouchableOpacity有效

# 2018-01-29

**react-native**

Image如果要使用网络图片，需如下设置：source={{ uri: XXX }}

# 2018-02-01

**javascript**

数组的构造函数只有当参数大于等于两个时，才表示以此为内容创建，故如果要以此内容创建，建议用Array.of()

---

javascript数组成员类型可以各不相同

**react-native**

Webview背景默认是白色，html背景默认是无色

# 2018-02-02

**javascript**

函数最后一个参数末尾可加逗号的特性在某些情况下尚不可使用

# 2018-02-06

**react-native**

Image 需显式地设置宽高才能正确加载图形resizeMode

# 2018-02-09

**react-native**

渲染列表元素的key要保证不重复，否则更新视图时会发生错误

# 2018-02-22

**css**

宽高的百分比是在减去padding之后，绝对定位将无需考虑padding，故撑满父组件不应设置长宽100%，而应设置上下左右皆为0

# 2018-02-22

**echarts**

series在初始化的时候其中不能设置一些奇奇怪怪的东西，如null，否则后续数据更新不上，可以为空数组

# 2018-03-01

**构建**

注释应表达意图、为何做、特殊注意点

# 2018-03-15

**javascript**

let和const必须先声明后使用

# 2018-03-28

**react-native**

修改Android版包名

1. 修改`android/app/build.gradle`里的`applicationId`，为新包名，譬如：`com.xxx.yyy.myProject`
2. 修改`android/app/src/main/AndroidManifest.xml`里的`package`，为新包名，譬如：`com.xxx.yyy.myProject`
3. 在`android/app/src/main/java/com`下根据新包名中多出的两级`xxx.yyy`新创建两级新目录，譬如：`android/app/src/main/java/com/xxx/yyy` ，将之前`android/app/src/main/java/com`下的`myProject`文件夹剪切到`android/app/src/main/java/com/xxx/yyy`下面
4. 打开`android/app/src/main/java/com/xxx/yyy/myProject/MainActivity.java`和`MainApplication`，修改第一行为：`package com.xxx.yyy.myproject;`
5. android/app/BUCK，修改两个package的值`package = 'com.exease.etd.objective',`
6. 在android目录下执行`./gradlew clean`清除缓存

# 2018-04-08

**react**

在constructor中要使用传入constructor的参数props, 不可以用this.props（还没生成）

# 2018-04-18

**react-native**

link操作常见错误

- 无法删除XXX：进入android目录执行./gradlew clean
- MainApplication找不到符号：忘了import

# 2018-05-14

**react-native**

android版生成签名与打包release版

1. 在JDK的bin目录下执行

   ```
   $ keytool -genkey -v -keystore my-release-key.keystore -alias my-key-alias -keyalg RSA -keysize 2048 -validity 10000
   ```

2. 把`my-release-key.keystore`文件放到你工程中的`android/app`文件夹下。

3. 编辑`~/.gradle/gradle.properties`（没有这个文件你就创建一个），添加如下的代码（注意把其中的`****`替换为相应密码）

   ```
   MYAPP_RELEASE_STORE_FILE=my-release-key.keystore

   MYAPP_RELEASE_KEY_ALIAS=my-key-alias

   MYAPP_RELEASE_STORE_PASSWORD=*

   MYAPP_RELEASE_KEY_PASSWORD=*

   ```

4. 编辑你项目目录下的`android/app/build.gradle`，添加如下的签名配置：

   ```
   ...
   android {
       ...
       defaultConfig { ... }
       signingConfigs {
           release {
               storeFile file(MYAPP_RELEASE_STORE_FILE)
               storePassword MYAPP_RELEASE_STORE_PASSWORD
               keyAlias MYAPP_RELEASE_KEY_ALIAS
               keyPassword MYAPP_RELEASE_KEY_PASSWORD
           }
       }
       buildTypes {
           release {
               ...
               signingConfig signingConfigs.release
           }
       }
   }
   ...
   ```

5. 根据需要设置`enableProguardInReleaseBuilds`和`enableSeparateBuildPerCPUArchitecture`

6. 在android目录下执行

   ```
   ./gradlew assembleRelease
   ```

   生成APK，位于`android/app/build/outputs/apk/app-release.apk`

7. 可在android目录下执行

   ```
   ./gradlew installRelease
   ```

   测试生成的包

# 2018-05-15

**react-native**

react native打包出现unable to process incoming event 'ProcessComplete' <ProgressCompleteEvent>，换用命令：

```
./gradlew assembleRelease --console plain
```

---

\*.iso.js与\*.android.js的区别类似Platform.OS判断的区别，都是在运行时选择，如用import只会引用\*.ios.js，需用require

# 2018-05-18

**android**

在安卓中，最适合存放App文件的是外部存储中的私有目录：file:///storage/emulated/0/Android/data/com.xxx.xxx/，它会在App删除后一并删除

(手机中直接查看的位置：内部存储设备/Android/data/com.xxx.xxx/)

**react-native**

react-navigation中如果要让goBack()穿越到父navigator中，需传入参数goBack(null)

# 2018-05-24

**javascript**

class如果没有继承，constructor中不可加super()

# 2018-06-01

**javascript**

类的构造函数，最好只用来构造所需持有的成员对象的实例，初始化的函数的调用放在专门的初始化函数中，特别是异步的且要等结果的

# 2018-06-07

**javascript**

遍历对象的可枚举属性不要用for...in，因为它会将原型链上的属性都遍历出来，而应该用Object.keys()（返回值为数组），这个只会遍历它本身的属性

# 2018-06-08

**javascript**

如果报错信息中莫名其妙的提示不应该出现'<'，可能是git merge的冲突未处理，通过搜索'<<<'处理

# 2018-06-12

**javascript**

通过import引进的.json文件就已经自动解析为对象了

# 2018-06-14

**markdown**

可以使用如下形式对标题进行内部链接

```
## Block Elements

[This link](#block-elements)
```

注意：

- 链接地址要将大写改为小写，空格改为-
- 不管标题是几级，都只用一个#
- 只会链接到第一个匹配的标题

# 2018-06-15

**IoT**

串口指按字节穿行通信的物理接口，通常COM口指串口，USB也属于穿行通信

RS232、RS485属于物理层协议，他们都可以在9个针孔的DB9插口上实现

RS232全双工，距离短；RS485半双工，距离长

Modbus协议在RS232、RS485之上实现的Modbus-RTU和在以太网上实现的Modbus-TCP

Modbus协议通过功能码控制对输入继电器、输出继电器、输入寄存器、输出寄存器的读写

101与104规约都适用于厂站与调度主站间通信，应用层定义相同，区别是101基于穿行通信，104基于以太网

101/104不适用OSI七层模型，101分为物理层、链路层、应用层；104分为物理层、链路层、网络层、传输层、应用层

# 2018-06-20

**react-native**

将RN项目gradle版本升级至4.4：

in android/gradle.properties:

```
android.useDeprecatedNdk=true
android.enableAapt2=false

```

in android/build.gradle:

```
uildscript {
    repositories {
        jcenter()
        maven {
            url 'https://maven.google.com'
            name 'Google'
        }
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:3.1.0'

        // NOTE: Do not place your application dependencies here; they belong
        // in the individual module build.gradle files
    }
}

allprojects {
    repositories {
        mavenLocal()
        jcenter()
        maven {
            url 'https://maven.google.com'
            name 'Google'
        }
        maven { url "https://jitpack.io" }
        maven {
            // All of React Native (JS, Obj-C sources, Android binaries) is installed from npm
            url "$rootDir/../node_modules/react-native/android"
        }
    }
}

subprojects {
    project.configurations.all {
        resolutionStrategy.eachDependency { details ->
            if (details.requested.group == 'com.android.support'
              && !details.requested.name.contains('multidex') ) {
                details.useVersion "26.0.1"
            }
        }
    }

    afterEvaluate { 
        project -> if (project.hasProperty("android")) { 
            android { 
                compileSdkVersion 26 
                buildToolsVersion '26.0.1' 
            } 
        } 
    } 
}

```

in android/app/build.gradle:

```
android {
    compileSdkVersion 26
    buildToolsVersion "26.0.1"

    defaultConfig {
        applicationId "appName"
        minSdkVersion 16
        targetSdkVersion 22
        versionCode 1
        versionName "1.0"
        ndk {
            abiFilters "armeabi-v7a", "x86"
        }
    }

...

dependencies {
    implementation project(':react-native-camera')
    ...
    implementation fileTree(dir: "libs", include: ["*.jar"])
    implementation 'com.android.support:appcompat-v7:26.0.1'
    implementation "com.facebook.react:react-native:+"  // From node_modules
}

```

in android/gradle/gradle-wrapper.properties:

```
distributionBase=GRADLE_USER_HOME
distributionPath=wrapper/dists
zipStoreBase=GRADLE_USER_HOME
zipStorePath=wrapper/dists
distributionUrl=https\://services.gradle.org/distributions/gradle-4.4-all.zip
```
**android**

如要强制项目中所有的某个依赖版本，可按如下设置

in `android/build.gradle`

```
allprojects {
    repositories {

        // ...

+        configurations.all {
+          resolutionStrategy {
+            force 'com.google.android.gms:play-services-vision:11.8.0'
+            force 'com.google.android.gms:play-services-gcm:11.8.0'
+          }
+        }
    }

}
```
# 2018-07-02

**echarts**

echarts必须确保在第一次setOption时，data 或source字段不能为null、undefined，可以没有这个字段或有一个占位对象，占位对象需反映实际数据的结构，值可以为null。

在react-native封装使用中，可写为数据源或占位对象：

```
data: this.state.data || [{ time: null, value: null }]
```

# 2018-07-02

**react-native**

测试webview访问PC网页可设置userAgent为PC浏览器

# 2018-07-04

**react-native**

当调试没问题，打包后闪退提示com.facebook.react.common.JavascriptException: undefined is not an object (evaluating 'n.View.propTypes.style')，是因为有第三方库使用了被废弃的View.propTypes

**vscode**

全局搜索会排除/node_modules/等目录，如这些目录也想搜索，点击搜索下面的 ··· 按钮，再点掉“排除的文件”后面齿轮的高亮

# 2018-07-04

**flutter**

在国内pub的远程仓库可设置：

```
export PUB_HOSTED_URL=https://pub.flutter-io.cn //国内用户需要设置
export FLUTTER_STORAGE_BASE_URL=https://storage.flutter-io.cn //国内用户需要设置
```

（如需永久有效需在系统变量里设置）

不过如果你要在pub上发布，需将其设回原来的值

**shadowsocks**

设置代理后若要在控制台中也使用代理，需进行设置

以使用shadowsocks代理为例，ss的代理端口为1080,那么应该设置为

```
export http_proxy="http://127.0.0.1:1080"
export https_proxy="http://127.0.0.1:1080"
```

**react-native**

react-native中也可使用babel-plugin-transform-remove-console，无需特别设置即可实现开发时有console，产品打包没有console

---

gradle-tool升级到3以后目前react-navigation打包产品会有问题，需在android根目录的gradle.propertis中加入：

```
android.enableAapt2=false
```

# 2018-07-10

**react-native**

WebView不可以设置高度，强制为flex: 1，使用时外面需套上View

# 2018-07-16

**react-native**

涉及setState的异步请求最好放在componentDidMount中，因为如果请求太快setState在render之前将会警告

# 2018-07-17

**ble**

Android系统ble通信的包最大为20（IOS为182），包超过20会导致系统不发送characteristicUpdate事件

# 2018-07-18

**dart**

命名参数定义时需用大括号括起来，使用时不需要加大括号

---

"_"开头的标识符只是在这个文件中私有，不是类私有

**javascript**

JSON.stringify时遇到无法解析的自动（比如函数）会没有这个字段，不会报错，解析基本类型的值有一套奇怪的规则，基本上是转换为对应字符串类型

**flutter**

flutter中禁用运行时反射（dart中有运行时反射），故类似dartson的Json解析库不可使用

# 2018-07-19

**flutter**

flutter中的flex值需为int

# 2018-07-23

**weixin**

小程序头像不可使用带透明通道的

# 2018-07-23

**babel**

babelrc中配置的执行顺序

1. 先执行完所有Plugin，再执行Preset。
2. 多个Plugin，按照声明次序顺序执行。
3. 多个Preset，按照声明次序逆序执行。

# 2018-08-01

**babel**

在babel7中，需将

babelrc中的module-resolver的配置

```
"plugins": [
    [
      "module-resolver",
      {
        "root": ["./src"]
      }
    ],
    ]
```

在eslint中再配一份

```
"settings": {
    "import/resolver": {
      "babel-module": {
        "root": ["./src"]
      }
    }
  }
```

# 2018-08-06

**babel**

babel 7之后的改动：

所有官方的包统一改名为@babel/型的命名

stage-型的preset被废除了，提案插件单独引入，提案插件包含-proposal-关键字

年份reset被废除了，统一到env中

# 2018-08-06

**webpack**

最新的create-react-app中控制babel适配浏览器版本是通过package.json中的browserslist:

```
"browserslist": {
    "development": [
      "last 2 chrome versions",
      "last 2 firefox versions",
      "last 2 edge versions"
    ],
    "production": [
      ">0.25%",
      "not op_mini all",
      "ie 11"
    ]
  }
```

# 2018-08-06

**react**

create-react-app 可通过--scripts-version参数控制script版本

# 2018-08-22

**typescript**

对于react组件，如果需要提供给非ts应用使用，则仍需propTypes，否则则不需要

# 2018-08-23

**ble**

addListener 可以添加多个，故每次使用完listener要remove掉

# 2018-08-27

**react-native**

0.56.0版本需改动的配置

"react-native": "0.55.4"

"babel-preset-react-native": "4.0.0",

android/build.gradle

    minSdkVersion = 21

android/gradle.properties

android.enableAapt2=false

# 2018-08-23

**javascript**

在Promise的定义函数中，中途resolve或reject后，虽然Promise的状态不再受影响了，但该定义函数仍将继续执行直到结束或return；由于使用Promise和该定义函数的执行不在同一线程中，故resolve之后的代码与Promise的then执行先后顺序无法预知（一般该定义函数resolve之后的同步代码会先与Promise收到then）

可用async函数代替，async中throw即返回reject，throw之后的代码不会再执行

# 2018-09-05

**redux**

reducer对state不会有特别的处理和保障，靠开发者自觉

# 2018-09-06

**react**

js事件，从子元素到父元素称为冒泡，从父元素到子元素称为捕获，dom标准事件流程是先捕获后冒泡

react通过事件委托统一处理事件，触发采用自己的一套冒泡机制

# 2018-09-11

**echarts**

移动端推荐使用svg的原因

1. canvas内存消耗大，一个页面上canvas多了可能内存溢出
2. 浏览器把大的canvas组合到背景上的消耗比较大，所以滑动效果不好

# 2018-09-21

**linux**

proxychains与设置中的代理不可共存

# 2018-09-26

**javascript**

NaN 与 NaN === 和 == 都为false，要用isNaN()判断, isNaN()只要不是数字都true，而Number.isNaN()必须是NaN才是true

# 2018-10-11

**babel** **webpack**

改变标识符称为minify，由babel-preset-minify完成，压缩成一行称为uglify，由uglifyjs-webpack-plugin完成

# 2018-10-30

**react-native**

在android的status bar 上，黑底的称之为light，白底的称之为dark，需显式的设置backgroundcolor否则切换后颜色会出问题，可能与沉浸式机制有关

# 2018-11-29

**javascript**

没有extends的类构造函数中不需写super()，有extends的类必须写super()

为子类自己的`this`对象，必须先通过父类的构造函数完成塑造，得到与父类同样的实例属性和方法，然后再对其进行加工，加上子类自己的实例属性和方法。如果不调用`super`方法，子类就得不到`this`对象。

constructor返回的是实例，但constructor属于实例而不是类，

静态方法的this指的是类而不是实例，可通过new this返回实例

子类继承后，成员方法this指子实例，静态方法this指子类

ES5 的继承，实质是先创造子类的实例对象`this`，然后再将父类的方法添加到`this`上面（`Parent.apply(this)`）。ES6 的继承机制完全不同，实质是先将父类实例对象的属性和方法，加到`this`上面（所以必须先调用`super`方法），然后再用子类的构造函数修改`this`。

---

super关键字有作为父类构造函数和作为父类**原型**对象两种使用方式（是否加括号）

# 2018-11-30

**javascript**

构造函数、类有prototype，指向原型对象，

每个实例都包含一个内部指针指向原型对象，有时可用\_\_proto\_\_指代

---

函数默认参数可包含变量，前提是动态环境要有（惰性求值），包括可以用到前面的参数（不能用后面的参数）

---

按位运算相关

XX位整数是带符号的，第一位0为正，1为负

考虑了符号的二进制值称为真值

原码, 反码, 补码是机器存储一个具体数字的编码方式

原码：就是本身

反码：正数（0...)就是原码，负数(1...)数值位全部取反

补码：正数（0...)就是原码，负数(1...)反码+1

补码的目的方便带符号进行加法，同时-0留作最小负数

js按位运算的操作数将被转换为补码形式的32位有符号整数，超过32位的部分丢弃。按位移动会先将操作数转换为大端字节序顺序(big-endian order)的32位整数,并返回与左操作数相同类型的结果。右操作数应小于 32位，否则只有最低 5 个字节会被使用。

<< 左移右补零

\>\> 右移左拷贝

\>\>\> 右移左补零

---

可以采用new B().f()的形式新建一个对象的实例并调用实例方法