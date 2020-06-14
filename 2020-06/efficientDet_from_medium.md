- [Original Link - EfficientDet: Scalable and Efficient Object Detection](https://medium.com/@nainaakash012/efficientdet-scalable-and-efficient-object-detection-ea05ccd28427)

## EfficientDet: 可拓展的和有效的目标检测
- 目标检测发展了很长的一段时间。由目标检测中的比较琐碎的计算机视觉技术发展到高级的目标检测器，这个改进非常的巨大。卷积神经网络(CNNs)，在这次变革中担任了一个非常重要的角色。我们希望我们的检测器的精度尽可能的高，并且尽可能的快，能够做到实时。但这个两个指标(精度和速度)存在一个权衡，而大多数的检测器都是在其中一个指标表现好，另外一个指标的表现则相对较差的。通常地，精度更高的检测器需要更多的计算量，但这不是一个很好的应用场景。所以，我们在不断寻求更高效的检测模型。这篇来自谷歌大脑团队的论文提出了一个新的检测器家族，它们是更加**高效的**，更加准确的和更快的。

### 为什么我们在讨论效率？
- 我们想到的一个比较自然的问题就是，为什么我们那么在乎效率呢？我们不是更应该考虑检测器的精度吗？总之，我们知道有些技术像[**Global Filter Pruning**](https://medium.com/@nainaakash012/gate-decorator-global-filter-pruning-afc12fcc71c6)，是能够用来压缩大的模型的。

- 那么，以上这些讨论都是有道理的。尽管你能够通过剪枝来压缩大模型，但它是一个多阶段的操作，并且无论模型多小，肯定存在精度的损失。过去几年检测器的改进有了非常打的进步，但是我们仍然没有探索出一种从0开始设计一个有效的检测模型的方法。在[**fficientNet**](https://medium.com/@nainaakash012/efficientnet-rethinking-model-scaling-for-convolutional-neural-networks-92941c5bfb95)论文中展示了如何拓展CNNs，它对目标检测器中高级研究是有贡献的，另外，在实际应用场景中，例如机器人和无人驾驶汽车，**模型大小，内存占用和延迟性**对模型的部署来说尤为重要。

### 这篇论文的贡献
- 本篇论文只要提出了以下3点贡献：
  - (1) **BiFN**，一个双向权重特征网络，用来进行简单和快速多尺度特征融合。
  - (2) **Compound scaling**，一种新的方法，它能够按照某种规则联合向上拓展的backbone，特征网络，box/class 网络和分辨率。
  - (3) **EfficientDet**，一种新检测器家族，能够在一系列的资源限制下，得到非常好的精度和效率。

- 这篇论文主要是在一系列的资源限制中建立了一个可拓展的，高精度和高效率的检测器架构。(譬如，从3B到300B FLOPS). 它主要尝试解决以下2个方面的挑战：
  - (1). **Efficient multi-scale feature fusion, 高效的多尺度特征融合**, FPN, 特征金字塔已经成为了融合多尺度特征的主要方法。一些用到FPN的检测器包括： RetinaNet, PANet, NAS-FPN等等。大多数适应这些检测器的融合策略在进行融合时都没有考虑到filters的重要性。他们毫无分别的堆叠它们。实际上，并不是所有的特征对输出特征有同等的贡献的。所以，我们需要一个更好的融合测率。
  - (2). **Model Scaling， 模型缩放**，前人的大多数工作都是使得backbone更大，以得到更好的精度。论文作者发现在同时关注精度和速度的同时增大特征网络和box/class预测网络也显得尤为重要。受[**compound scaling in EfficientNets**](https://medium.com/@nainaakash012/efficientnet-rethinking-model-scaling-for-convolutional-neural-networks-92941c5bfb95)的启发，作者提出了一个目标检测器的混合缩放方法，它是通过联合增大所有backbone，特征网络，box/class预测网络的分辨率，深度和宽度。
  
- 让我们逐个点逐个点来具体分析，从而更好的理解这边论文吧。

### 特征金字塔网络(FPNs)
- 在讨论特征金字塔之前，我们先来回顾一下FPN的思路和讨论一下它的优缺点。尽管FPN并不是一个新东西，最先提出在deep CNN中利用深层多尺度堆叠的特征金字塔是2017年的这篇[**论文**](https://zpascal.net/cvpr2017/Lin_Feature_Pyramid_Networks_CVPR_2017_paper.pdf)。

- ![Figure1. Feature Pyramid Network](../asserts/EfficientDet/FPN.png)
