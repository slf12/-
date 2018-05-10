## Cyclical Learning Rates for Training Neural Networks 笔记

github 代码地址 [https://github.com/bckenstler/CLR](https://github.com/bckenstler/CLR)，文中有些图片来自这个地址

### 论文思想

这篇论文提出了一个新的训练思路，周期性的改变学习率(CLR)，原因是发现在训练时提高学习率虽然会降低精度，但是继续训练，精度会上升并且高于下降之前得精度，提出了周期性的学习率变化。

### CLR

效果图

![Alt text](images/clr-result.jpg?raw=true "Title")

图中可以看出虽然CLR方法在训练过程中精度振荡，但是最终精度高于其他方法。

#### 不同的策略
**triangular**

![](images/clr-triangular.jpg?raw=true "Title")
从图中可以看出，学习率有一个上界和下界，学习率在之间线性增长和下降。

**triangular**

![](images/clr-triangular2.png?raw=true "Title")

和**triangular**不同的是，每个周期后，学习率的上界会下降

**exp range**
![](images/clr-exp_range.png?raw=true "Title")

每个周期内，学习率上界的变化不是分段函数，是指数函数

#### 确定参数
需要确定的参数有stepsize, base\_lr, max\_lr

stepsize： 根据经验确定，在实验中发现，设为 2-10倍每个epoch的迭代数比较好

base_lr和max_lr根据“LR range test”方法确定。
学习率从0开始增大，随迭代次数线性增长到一个最大值，每次迭代都测试一个精度，画出趋势图

如图所示：

![](images/clr-lr-test.jpg?raw=true "Title")

base_lr 取精度开始增长的点，例子中取0.001

max_lr 取精度开始增长缓慢、振荡或者下降的点，例子中取0.006


