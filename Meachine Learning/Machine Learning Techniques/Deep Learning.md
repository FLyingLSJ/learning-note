上节课我们主要介绍了神经网络 Neural Network。神经网络是由一层一层的神经元构成，其作用就是帮助**提取原始数据中的模式即特征，简称为pattern feature extraction**。神经网络模型的关键是计算出每个神经元的权重，方法就是使用 Backpropagation 算法，利用 GD/SGD，得到每个权重的最优解。本节课我们将继续对神经网络进行深入研究，并介绍层数更多、神经元个数更多、模型更复杂的神经网络模型，即深度学习模型。

## Deep Neural Network 

神经网络根据复杂度可以分为 Shallow Neural Networks 和 Deep Neural Networks。

-  Shallow Neural Networks：神经网络层数较少

  优点是：训练更有效率；结构比较简单；理论上是足够强大的

- Deep Neural Networks

  训练上的挑战；结构复杂；物理意义明确

![](./images/13-1.png)

举个例子：手写识别

![](./images/13-2.png)

手写识别步骤：先把写上数字的图片提取存储一块一块不同部位的特征。例如左边三幅图每张图代表了数字 1 的某个部位的特征，三幅图片组合起来就是完整的数字 1。右边四幅图也是一样，每张图代表了数字 5 的某个部位的特征，五幅图组合起来就是完整的数字 5。对计算机来说，图片由许多像素点组成。要达到识别的目的，每层神经网络从原始像素中提取出更复杂的特征，再由这些特征对图片内容进行匹配和识别。**层数越多，提取特征的个数和深度就越大，同时解决复杂问题的能量就越强，其中每一层都具有相应的物理意义。**以上就是深度学习的作用和意义。

深度学习的挑战和关键技术：

![](./images/13-3.png)

- 结构确定上的困难：

  受领域知识的影响，例如卷积神经网络用来处理图片：把相邻像素用权重连接起来，而离得比较远的像素，让他们的关系弱化（或者消失）

- 模型复杂度

  对于有大量的数据来说，这不是什么问题；

  正则化对噪声具有耐受性：例如，在某些神经网络坏掉的时候也能得到很好的输出或者数据存在噪音时也能有好的输出。

- 优化的问题

  权重的初始化很重要，能避免局部最优

  ![](./images/13-4.png)

  pre-training：我们可以先对一层的权重进行初始化，选择之后再使用 Backprop 算法训练模型，得到最佳的权重值。一层一层下去，这样能得到较好的初始值。

- 计算复杂度（数据量很大的时候）

  解决是硬件来支持：使用 GPU（能把任务分为很多块，分别处理，再整合起来）

  ## Autoencoder



如何进行 pre-training ，得到较好的权重初始值？先看看权重的物理意义是什么，神经网络中，权重代表特征转换（feature transform），另一方面，权重代表（encoding），就是把原始数据编码成另外一种数据来表示，而编码后的数据，可以最大程度的还原到原始的数据。即信息保留编码（information-preserving encoding），最大程度地保持特征。

举个例子，简单的手写识别的例子。从原始的一张像素图片转换到分解的不同笔画特征，那么反过来，这几个笔画特征也可以组合成原来的数字。这种可逆的转换被称为 information-preserving，即转换后的特征保留了原输入的特征，而且转换是**可逆的**。这正是 pre-train 希望做到的，通过 encoding 将输入转换为一些特征，而这些特征又可以复原原输入 x，实现 information-preserving 。所以， pre-training 得到的权重初始值就应该满足这样的 information-preserving 特性。

![](./images/13-5.png)

那么，如何在 pre-training 中得到这些初始权重呢？简单的方法是建立一个 3 层的神经网络：

![](./images/13-6.png)

输入原始数据 X 这些数据是 d 维的，我们通过一个神经网络，输出一个相同维度的值，而这些值最大程度上保留了原始的数据。整个网络是 $d-\breve{d}-d$ NNet 结构。其核心在于“重构性”，从输入层到隐藏层实现特征转换，从隐藏层到输出层实现重构，满足上文所说的 information-preserving 的特性。

这种结构的神经网络称作 autoencoder 输入层到隐藏层对应编码，而隐藏层到输出层对应解码。其中， $W_{ij}^{(1)}$ 表示编码权重，而 $W_{ji}^{(2)}$ 表示解码权重。整个过程类似于在学习如何近似逼近 identity function。

![](./images/13-7.png)



那么为什么要使用这样的结构来逼近 identity function，有什么好处呢？

- 对于监督学习：隐藏层对原始数据进行特征转换，例如手写识别中隐藏层分解的各个笔画，包含了有用的信息。这样就可以从数据中学习得到一些有用的**具有代表性的信息**。

- 对于非监督式学习（unsupervised learning）：可以做密度估计（density estimation）若最终的输出 $g(x)≈x$  则表示密度较大，若 g(x) 与 x 相差甚远，则表示密度较小。这种方法同样适用于outlier detection，异常检测。这样就可以从数据中学习得到一些典型的具有代表性的信息，找出哪些是典型资料，哪些不是典型资料。

  ![](./images/13-8.png)

基本的编码器（basic autoencoder）

![](./images/13-9.png)

![](./images/13-10.png)



![](./images/13-11.png)

 <img src="http://chart.googleapis.com/chart?cht=tx&chl= W_{ij}^{(1)}" style="border:none;"> 是浅度预训练的权重。

Pre-training的整个过程是：首先，autoencoder 会对深度学习网络第一层（即原始输入）进行编码和解码，得到编码权重 <img src="http://chart.googleapis.com/chart?cht=tx&chl=  W_{ij}^{(1)}  " style="border:none;"> ，作为网络第一层到第二层的的初始化权重；然后再对网络第二层进行编码和解码，得到编码权重 $W_{ij}^{(1)}$ ，作为网络第二层到第三层的初始化权重，以此类推，直到深度学习网络中所有层与层之间都得到初始化权重。值得注意的是，对于l-1层的网络 <img src="http://chart.googleapis.com/chart?cht=tx&chl= {x_n^{(l-1)}} " style="border:none;">，autoencoder中的 <img src="http://chart.googleapis.com/chart?cht=tx&chl=  \breve d   " style="border:none;"> 应与下一层（即l层）的神经元个数相同。

![](./images/13-12.png)



<img src="http://chart.googleapis.com/chart?cht=tx&chl=  W_{ij}^{(1)}  " style="border:none;">

