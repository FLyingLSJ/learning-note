## Learning with Different Output Space Y

根据不同输出的空间进行学习。如分类（二元分类、多元分类）问题，

![img](/images/5b556e0a3938e.png)

## Learning with Different Data Label yn

监督学习：

半监督学习（Semi-supervised Learning）：数据集一部分有输出，一部分没有输出

非监督学习：

增强学习：根据输出的好坏给予正负反馈。

![img](/images/5b556e3b09cb5.png)

## Learning with Different Protocol f(xn,yn)

根据不同的协议：

- Batch Learning：数据集是一批一批的，填鸭式
- Online：数据是实时更新的，老师教学
- Active Learning：让机器具备主动问问题的能力，例如手写数字识别，机器自己生成一个数字或者对它不确定的手写字主动提问，主动学习。

![img](/images/5b556e4794851.png)

## Learning with Different Input Space X

根据输入的特征进行学习：

- concrete features：具体特征，比如说硬币分类问题中硬币的尺寸、重量等
- raw features：原始特征，如图片的像素。raw features 比较抽象，需要转化为对应的 concrete features。这个过程叫特征转换（Feature Transform）
- abstract features：抽象特征，比如某购物网站做购买预测时，提供给参赛者的是抽象加密过的资料编号或者ID，这些特征X完全是抽象的，没有实际的物理含义。所以对于机器学习来说是比较困难的，需要对特征进行更多的转换和提取。

![img](/images/5b556e674e571.png)

## 总结

![img](/images/5b556e7834508.png)

