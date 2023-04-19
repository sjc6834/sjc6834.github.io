# Improving field boundary delineation in ResUNets via adversarial deep learning

## 生词

policy-makers  <政策制定者>

stakeholders  <利益相关者>

qualitatively however  <但从质量上看>

malformed  <畸形的>

necessitate  <使成为必要>

trial-and-error  <试错>

regime  <制度>

downstream  <下游>

in turn  <反过来>

tedious  <冗长的>

devoted  <专用于···>

abrupt  <突然的>

## 背景

先前的工作探索了各种预测田块边界的架构，但几乎全是传统的监督学习机制。

因此，本文提出了新的方法，通过研究对抗性训练对全卷积边界检测网络的影响来解决预测过程中的开放边界问题。

### Traditional approaches

#### Edge filters

通过卷积突出图像显著的变化。但是，对噪声或内部区域变化过于敏感，容易产生过分割。

#### Crop-specific spectral information

通过融入特定的作物光谱信息，可以改善田块边界边缘强度图。

#### Region-based algorithms and graph-based contour expansion algorithms

Watershed-based algorithms···

**以上的方法需要设定阈值，然而，这个阈值难以微调且不同区域需要改变**。

此时，又提到了一篇论文*《Crop field boundary delineation using historical crop rotation pattern》*，不依赖传统的边缘检测方法，而是合并历史的作物轮作数据，但不容易转移到历史记录不佳的地区。该方法的思路和我之前的工作有些类似，都是利用历史数据辅助分割，可以读一读。

### Supervised machine learning methods

**这类方法比传统方法更高效、更自动化，但依赖标注数据。**

#### Superpixel+machine learning classification

我之前的工作就是用的该方法。

#### Fully convolutional network（FCN）

该方法比较火热，将预测田块边界作为语义分割任务，可以通过对任意大小的输入产生相应大小的输出来有效地计算每个像素的预测值。

有效且常用的结构是UNet，通常与残差连接和循环连接 (recurrent connection)相结合，如ResUNet-a、ResU-Net、DSCUnet。

### Combined neural model and post-processing methods

**基于深度学习的方法仍有一定程度的不连续和断裂的边缘，难以直接使用，往往需要进行后处理操作。**

#### 迭代式轮廓合并方法闭合破碎边缘

#### 截断算法或分水岭算法生成实例分割结果

**目前的后处理技术并没有完全解决开放边界的问题。在先前的工作中，阈值是通过试错来手动设置的（或者在优化中会产生昂贵的计算成本）。**

### Generative adversarial networks (GAN)

GAN起初被用来估计生成模型，目前被广泛用于图像合成、风格迁移等，可以生成逼真或细节的结果。

对抗训练（Adversarial training）已经被证明对于语义分割是有效的，包括其他基于FCN的检测任务。

## 贡献

在这项工作中，借用了对抗性的想法，通过诱导模型输出分布的 "良好的边界风格 "来提高田块边界预测的质量。提高边界预测质量的一个潜在好处是，它可以减少对可能需要仔细优化的后处理方法的依赖。据文章所说，这是在对抗性框架中探索田块边界划分的第一项工作。实验证明，对抗性训练可以大大改善基本的边界质量，并显示出改善现有系统的巨大前景。同时，论文提出在探索对抗性设置方面还有很多工作要做，包括从以前的研究和可转移性实验中纳入未见过的区域的设置。



