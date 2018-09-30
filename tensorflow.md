NIPS

AlexNet

---

DL中的重要概念

Model

layer

activation

loss

optimizer 在两个epoch之间计算怎么从老的参数变成新的参数（常用到gradient）

train/fit 每一个epoch都会walkthrough所有data

模型train完了要evaluate，要用和traindata不一样的testdata，不过只要一遍，不需要多个epoch

evaluate完了就可以predict了，model(predict_dataset)的结果需要处理才能得到所要的

---

数据为tensor，操作为operation，结合成graph，graph构成session

tensorflow分为客户端与服务端，之间通过session通信

流程：

首先通过高级语言代码在客户端定义graph，通过session的run将此图通知服务端执行

tf.Variable第一个V要大写

constant定义时即已经初始化了，Variable一定要初始化：tf.gloabal_variable_initializer()

可通过playground.tensorflow.org感性认识学习过程

shape中的-1表示根据后面的维度确定此维度

---

数据过少、对定量的数据训练过久会过拟合，模型规模（即由隐节点层数与每层节点数决定的模型可训练参数数，称为capacity）越大越容易过拟合

防止过拟合除了用更多数据训练外，方法是regularization，常见的有weight regularization and dropout

应该先从较小的规模开始逐渐增长规模，直到loss的减小不再更优

weight decay 就是L2 regularization

dropout比例常设为0.2到0.5之间

---

防止过拟合常用方法：

增加训练数据

减小模型规模

使用 weight regularization

使用 dropout

---

keras 存储模型时尚不能存储optimizers，所以需要重新compile并且optimizer的状态都没了

---

Tensors are immutable

---

tf的操作自动将numpy array转换为tensor

numpy操作自动将tensor转换为numpy array

---

tfe.gradients_function(f) 返回的是一个函数，该函数返回值是各偏微分的数组

---

```python
with tf.GradientTape() as t:
```

起到一个记录的作用，方便后续使用

---

在numpy中，axis就是dimension，最外围的dimension是第一个axis（标号从0开始）

shape是从最外围，即第一个axis开始存放size的，



一般将第一个维度，即最外围，shape[0]，称为column，v

一般将第二个维度，即第二外围，shape[1]，称为row, h



类似sum(axis=0)这样的操作，指的是会在该维度下操作，而不影响其他维度的shape，结果的shape是抹去该维度,比如sum(axis=0)就是在column上相加，得到的只剩原来的row（但是根据定义，现在row又变成了column）

TensorFlow中输入数据的某项属性称为column

---

训练的输入输出通常称为feature、label

如果没有非线性的激活函数，该层就等于没有用

隐节点常用relu

logit是一种变换