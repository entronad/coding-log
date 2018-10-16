keras 存储模型时尚不能存储optimizers，所以需要重新compile并且optimizer的状态都没了

------

Tensors are immutable

------

tf的操作自动将numpy array转换为tensor

numpy操作自动将tensor转换为numpy array

------

tfe.gradients_function(f) 返回的是一个函数，该函数返回值是各偏微分的数组

------

```python
with tf.GradientTape() as t:
```

起到一个记录的作用，方便后续使用

------

在numpy中，axis就是dimension，最外围的dimension是第一个axis（标号从0开始）

shape是从最外围，即第一个axis开始存放size的，



一般将第一个维度，即最外围，shape[0]，称为column，v

一般将第二个维度，即第二外围，shape[1]，称为row, h



类似sum(axis=0)这样的操作，指的是会在该维度下操作，而不影响其他维度的shape，结果的shape是抹去该维度,比如sum(axis=0)就是在column上相加，得到的只剩原来的row（但是根据定义，现在row又变成了column）

TensorFlow中输入数据的某项属性称为column

---

numpy中运算符都是元素操作，张量乘是@或.dot

运算后元素的dtype将按照最精确的一种算法