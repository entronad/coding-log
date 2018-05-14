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
