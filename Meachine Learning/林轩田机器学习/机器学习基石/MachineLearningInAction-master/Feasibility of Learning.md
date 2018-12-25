本节介绍机器学习的可行性。

# Learning is Impossible

![img](/images/5b556fcd351cb.png)

上面图片说明，在训练集 D 上的数据集，hypothesis 总能预测正确，但是对于 D 以外的数据不一定总是能够预测正确。

机器学习的这种特性被称为没有免费午餐（No Free Lunch）定理。NFL定理表明没有一个学习算法可以在任何领域总是产生最准确的学习器。不管采用何种学习算法，至少存在一个目标函数，能够使得随机猜测算法是更好的算法。平常所说的一个学习算法比另一个算法更“优越”，效果更好，只是针对特定的问题，特定的先验信息，数据的分布，训练样本的数目，代价或奖励函数等。

# Probability to the Rescue

![img](/images/5b556fe66e9e9.png)

从概率上说明机器学习的可行性，类似于概率上的取样，小样本可以大致推测出大样本的整体趋势。

# Connection to Learning

![img](/images/5b55701cb8b79.png)

联系到机器学习上来，样本中错误的概率可以推算出所有数据在 hypothesis 上错误的概率，这是机器学习能够工作的本质。

# Connection to Real Learning

![img](/images/5b5570bb3a811.png)

上面公式的含义是：M 是 hypothesis 的数量， N 是样本的 D 的数量， $\mu$ 是参数。

表明：如果 hypothesis 的个数 M 是有限的，N 足够大，那么通过演算法 A 任意选择一个矩 g 。说明机器学习是可行的。



# 总结

本节课主要介绍了机器学习的可行性。首先引入 NFL 定理，说明机器学习无法找到一个矩g能够完全和目标函数f一样。接着介绍了可以采用一些统计上的假设，例如 Hoeffding 不等式，建立$E_{in}$和 $E_{out}$的联系，证明对于某个h，当N足够大的时候，$E_{in}$ 和 $E_{out}$ 是 PAC 的。最后，对于 h 个数很多的情况，只要有h个数M是有限的，且N足够大，就能保证 $E_{in}\approx E_{out}$，证明机器学习是可行的。

参考资料

- [1] 林轩田机器学习基石
- [2] https://redstonewill.com/77/