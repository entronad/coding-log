机器学习领域最重要的国际学术会议是国际机器学习会议(ICML) 、国际神经信息处理系统会议(NIPS)和国际学习理论会议(COLT) ，重要的区域性会议主要有欧洲机器学习会议(ECML)和亚洲机器学习会议(ACML); 最重要的国际学术期刊是 Journal of Machine Learning Research 和 Machine Learning.人工智能领域的重要会议如 IJCAI、 AAAI 以及重要期刊如 Art侨c归1 Intelligence 、 Journal of Art听 cial Intelligence Reseαrch， 数据挖掘领域的重要议如 KDD 、 ICDM 以及重要期刊如 ACM Transactions on Knowledge DiscoveryfromDα归、 Dαtα Mining andKnowledge Discovery， 计算机视觉与模式识别 领域的重要会议如 CVPR 以及重要期刊如 IEEE Transactionson PattemAnalysis and Machine Intelligence， 神经网络领域的重要期刊如 Neural Computation、 IEEE Transaιtions on Neural Networks αηd Leαming 8ystems 等也经常发表机器学习方面的论文.此外，统计学领域的重要期刊如 Annals 旷8tαtistics 等也常有关于统计学习方面的理论文章发表. 

国内机器学习领域最主要的活动是两年一次的中国机器学习大会(CCML) 以及每年举行的"机器学习及其应用"研讨会(MLA); 很多学术刊物都经常刊登有关机器学习的论文. 

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

---

generalization 是模型适用于新样本的能力

机器学习算法在学习过程中对某种类型的假设的偏好，称为归纳偏好，任何有效的算法都有偏好，常用的偏好为奥卡姆剃刀

没有免费的午餐（NFL）：对于算法a，若在某些问题上比算法b好，则必然存在另一些问题里面b比a好，它说明算法的好坏不能脱离具体的问题

---

AI 发展：推理/逻辑（1950s) -> 知识/专家系统（1970s) -> 机器学习（1980s）

机器学习：不显式编程地赋予计算机能力的研究领 

BP算法诞生于1986年

从样例中学习是机器学习主流，分为符号主义（决策树）和连接主义（神经网络）、统计学习（支持向量机（核方法））

统计学习在1990s成为主流，在支持向量机被普遍接受后，核技巧 (kernel trick) 被人们用到了机器学习的几乎每一个角落，核方法也逐渐成为机器学习的基本内容之一. 

---

在训练集上的误差称为训练误差，新样本上的误差称为泛化误差，最终目的是减小泛化误差

过拟合是机器学习面临的关键障碍，是无法避免只能缓解

---

O(1),O(log(n)),O(n^a)等，我们把它叫做多项式级的复杂度，O(a^n)和O(n!)型复杂度，它是非多项式级的

P问题：如果一个问题可以找到一个能在多项式的时间里解决它的算法，那么这个问题就属于P问题

NP问题：NP问题是指可以在多项式的时间里验证一个解的问题，它不是非P问题

显然P问题一定是NP问题，但NP问题是否一定是P问题？

---

训练集需与测试集不一样，如果只有一份数据，需分出训练集测试集：

留出法：分出互斥的两个集合，需注意两个集合的结果分布需一致（分层采样），2/3 至 4/5 的样本用于训练，剩余样本用于测试. 一般要进行多次随机的留出划分

交叉验证法：将数据集划分成k等份，k-1个训练，剩下的测试，最终返回k个结果。一般k取10

自助法：对于有m个样本的数据集D，有放回的挑选m次，组成新的数据集D‘（极限约为1/3)作为训练集，D中未被选到的作为测试集。由于D’改变了原来的分布，引入了估计偏差，故只适用于样本较少的情况

---

给定包含 m 个样本的数据集 D ，在模型评估与选择过程中由于需要留出一部分数据进行评估测试，事实上我们只使用了一部分数据训练、模型.因此，在模型选择完成后，学习算法和参数配置己选定，此时应该用数据集 D 重新训练模型.这个模型在训练过程中使用了所有 m 个样本，这才是我们最终提交给用户的模型. 

---

，我们通常把学得模型在实际使用中遇到的数据称为测试数据，为了加以区分，模型评估与选择中用于评估测试的数据集常称为"验证集" (validation set) 

---

回归问题常用指标是均方差，分类问题常用指标是精度，在检索类问题中常用的指标是查准率（precision）：判为真中真的真，和查全率（recall）：真中被判为真的。

一般precision和recall是互斥的，故检索类问题性能判据常用PR图或ROC图分析

---

在确定了实验评估方法和性能度量后，机器学习的性能比较还是比较复杂，因为我们最终目的是泛化性能

---

泛化误差可分解为偏差与方差还有噪声（训练数据中的错误）之和，说明泛化性能是由学习算法的能力、数据的充分性以及学习任务本身的难度所共同决定的 。

在训练不足时?学习器的拟合能力不够强，训练数据的扰动不足以便学习器产生显著变化，此时偏差主导了泛化错误率;随着训练程度的加深，学习器的拟合能力逐渐增强，训练数据发生的扰动渐渐能被学习器学到，方差逐渐主导了泛化错误率;在训练程度充足后，学习器的拟合能力已非常强，训练数据发生的轻微扰动都会导致学习器发生显著变化，若训练数据自身的、非全局的特性被学习器学到了，则将发生过拟合. 

---

卷积神经网络（CNN）-> 视觉细胞 ->处理图像

循环神经网络（RNN）-> 处理时序问题

---

卷积的理解：时间尺度：过去每一点的状态与状态关于时长的转移的乘积的叠加

张量处理：通过每一点周围与核同形的一块与核点乘，重新组成形状不变的张量

抽象：x、y沿着x+y直线函数乘积的积分

---

设计cost function的原则是要smoth，即make small changes of w cause small changes of cost ,以便可通过梯度寻优

---

在大量训练数据中使用梯度下降时，理论上梯度需计算所有训练数据的cost function梯度取平均，但实际只要选取一小部分batch即可，因为每个epoch我们只要大致保持是向下变化即可

---

决定如何训练的参数称为hyper-parameters

---

炼丹调的参就是hyper-parameters和architecture