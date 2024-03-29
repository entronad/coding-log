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

---

概率分布：连续量只能算在某个区间上的概率，所以定义的形式是两个小于某个值概率相减，这个小于某个值的分布函数就是概率分布，概率密度是概率分布在区间趋于0的极限，或导数

---

training data 用来训练param

validation data 用来训练hyper-param

test data用来测试训练结果，param和hyper-param都用test data来测试

---

防止过拟合中奥卡姆剃刀的意义：太复杂的模型学习能力过剩会学到一些不该学到的东西，比如training data中偶然存在的规律，噪声分布等

l1,l2 regulization的意义是减小w意味着减小单个输入对模型的影响，而更注重输入整体特性对模型的影响, b的大小对过拟合影响不大，一般不regulization

事实上，regulization为什么有效尚无定论

l1 会让w更集中于少数几个重要的输入，其它的更趋于0

dropout的本质是随机的降低对单个输入的依赖

人为扩展数据集的方式很强大，比如转动图片，放快慢声音

---

高斯分布即正态分布

---

操作顺序

初始模型结果很差第一步是尝试简化问题维度，比如0-10识别先只识别0，1

可以先缩小数据量加快每步速度，以便多次试验观察效果

（参数设置初期是很难看到效果的，初期最重要的是看到meaningful signal，然后就会很快了）

- 学习率：

  首先取一个较小值，然后不断增大并观察最初几步是不是收敛，直到振荡，或者初始就振荡就减小直到收敛，这就是threshold value，实际的学习率会低于threshold value，比如一半。

- epoch

  epoch的控制主要靠early stop，为防止出现平台，通常要设置多次停止

- 学习率调度

  可以用early stop的思想调度学习率，比如出现平台就学习率除以2或10，直到初始值的1000分之一，调参初期应当使用定值学习率，等模型稳定后再用学习率调度进行优化

- 正则化参数lmbda

  首先设lmbda=0，调学习率，调完学习率后从lmbda=1开始以10为倍数增减调参，调完lmbda后要再调一遍学习率

- mini-batch

  (mini-batch为1称为online learning)通过矩阵技术，计算mini-batch为100的时间远低于100次online learning，通常在50次到1次之间，甚至接近1次，所以要在利用矩阵优势和更often之间权衡。在初期只需要大方向时，online learning效果就够了，后续对精确性要求高时用mini batch

  mini batch优化的最终目的是加快收敛速度。它与其它参数之间相对独立，一般先选几个相对可用的其它参数，调好mini batch再调其它参数

自动优化参数的方法有grid search，《3ractical %ayesian optimi]ation of machine learning algorithms, by -asper 6noek, +ugo /arochelle, and 5yan $dams. 》

---

梯度反向传播时，要么消失，要么爆炸

反向传播时最入口层参数的微分可写成反向过程多层sigmoid函数导数、w连乘，每个w期望小于1（以高斯分布初始化），每个sigmoid函数导数<0.25，故乘积很小，而加入恰巧每个w都很大（大于 1/sigmoid函数导数），则连乘后乘积很大

总之由于连乘的太多，除非恰巧连乘下来接近1（显然概率极低）入口层的梯度，即学习速度和出口比要么极小要么极大。消失的概率大些，因为w一旦大一些，sigmoid函数导数下降很多

---

DL中还可能遇到问题：sigmoid函数在输出层会很早退化为0，初始化和动量调度也会影响学习效果

---

CNN和最初的神经网络比起来仿生的成分已经很小了，所以常常不用neural这个词，神经元称为unit

被卷积核影响到的就是local receptive field（local receptive field * kernal = 后层的一个神经元）

对于后层的每个神经元，只有local receptive field大小的前层与之连接，且每个神经元的a,w,b都一样

feature map 指神经元输出

---

一般来讲relu好于sigmoid

全连接层数量、大小影响比较小

训练多个网络然后投票可提高准确率，是一种常用方法

dropout只需用在全连接层不需用在卷积层

CNN中一层卷积加一层池化算一层

---

RNN理论能处理很长期之前的信息，但实践中很难，故需要LSTM，LSTM主要优势能处理很长之前的信息

---

核函数指的是将数据从一个特征空间映射到另一个特征空间的函数