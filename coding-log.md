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