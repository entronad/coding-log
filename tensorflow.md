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