最简单的使用梯度信息的方法是，在负梯度方向上的一次小的移动作为式（5.27）的权值更新方法，即

$$
w^{(tau + 1)} = w^{(tau)} - \eta\nabla E(w^{(tau)}) \tag{5.41}
$$

其中$$ \eta > 0 $$被称为学习率（learning rate）。经过这样的更新之后，梯度会根据新的权值向量重新计算，然后重复这个过程。注意，误差函数是根据训练集定义的，因此每次$$ \nabla E $$的计算都要处理整个训练集。一次使用所有数据的技术被称为批方法（batch method）。每一次权向量都会沿着误差函数下降速度最快的方向移动，所以这个方法被称为梯度下降法（gradient descent）或最陡峭下降法（steepest
descent）。这种方法在直觉上看比较合理，但实际证明它是一个很差的算法，原因可以参考Bishop and Nabney(2008)。    

对于批量最优化，存在更高效的方法，例如共轭梯度法（conjugate gradient）或拟牛顿法(quasi-Newton)。与简单的梯度下降方法相比，这些方法更健壮，更快（Gill et al., 1981; Fletcher, 1987; Nocedal and Wright, 1999）。与梯度下降方法不同，这些算法具有：除非权向量到达了局部的或全局的最小值，否则误差函数在每次迭代时总是减小的性质。    

为了找到一个足够好的极小值，可能需要多次运行基于梯度的算法，每次都使用一个不同的随机选择的起始点，然后在一个独立的验证集上对比最终的表现。    

然而，梯度下降法有一个被证明在实际应用中对于使用大规模数据集来训练神经网络的情形很有用的在线的版本（LeCun et al., 1989）。基于一组独立观测的最大似然函数的误差函数由一个求和式构成，每个数据点有

$$
E(w) = \sum\limits_{n=1}^N E_n(w) \tag{5.42}
$$

在线梯度下降，也被称为顺序梯度下降（sequential gradient descent）或随机梯度下降（stochastic gradient descent）权向量的更新每次只依赖于一个数据点，即

$$
w^{(\tau + 1)} = w^{(\tau)} - \eta\nabla E_n(w^{(tau)}) \tag{5.43}
$$

这个更新在数据集上循环重复进行，并且既可以顺序地处理数据，也可以随机地有重复地选择数据点。当然，也有折中的方法，即每次更新依赖于数据点的一小部分。     

与批处理相比，在线方法的一个优点是可以更加高效地处理数据中的冗余性。为了说明这一点，让我们考虑这样一种极端的情形：给定一个数据集，我们将每个数据点都复制一次，从而将数据集的规模翻倍。注意这仅仅把误差函数乘以了一个因子$$ 2 $$，因此等价于使用原始的误差函数。批处理方法必须付出两倍的计算量来计算误差函数的梯度，而在线方法不受影响。在线梯度下降方法的另一个性质是：因为整个数据集的关于误差函数的驻点通常不会是每个数据点各自的驻点，所以它可以逃离局部最小值点。    

非线性最优化算法，以及它们对于神经网络训练的实际应用，在Bishop and Nabney(2008)中有详细的讨论。    

