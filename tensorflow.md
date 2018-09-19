数据为tensor，操作为operation，结合成graph，graph构成session

tensorflow分为客户端与服务端，之间通过session通信

流程：

首先通过高级语言代码在客户端定义graph，通过session的run将此图通知服务端执行

tf.Variable第一个V要大写

constant定义时即已经初始化了，Variable一定要初始化：tf.gloabal_variable_initializer()

可通过playground.tensorflow.org感性认识学习过程

shape中的-1表示根据后面的维度确定此维度