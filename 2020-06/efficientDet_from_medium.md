- [Original Link - EfficientDet: Scalable and Efficient Object Detection](https://medium.com/@nainaakash012/efficientdet-scalable-and-efficient-object-detection-ea05ccd28427)

## EfficientDet: 可拓展的和有效的目标检测
- 目标检测发展了很长的一段时间。由目标检测中的比较琐碎的计算机视觉技术发展到高级的目标检测器，这个改进非常的巨大。卷积神经网络(CNNs)，在这次变革中担任了一个非常重要的角色。我们希望我们的检测器的精度尽可能的高，并且尽可能的快，能够做到实时。但这个两个指标(精度和速度)存在一个权衡，而大多数的检测器都是在其中一个指标表现好，另外一个指标的表现则相对较差的。通常地，精度更高的检测器需要更多的计算量，但这不是一个很好的应用场景。所以，我们在不断寻求更高效的检测模型。这篇来自谷歌大脑团队的论文提出了一个新的检测器家族，它们是更加**高效的**，更加准确的和更快的。

### 为什么我们在讨论效率？
- 我们想到的一个比较自然的问题就是，为什么我们那么在乎效率呢？我们不是更应该考虑检测器的精度吗？总之，我们知道有些技术像[**Global Filter Pruning**](https://medium.com/@nainaakash012/gate-decorator-global-filter-pruning-afc12fcc71c6)，是能够用来压缩大的模型的。

- 那么，以上这些讨论都是有道理的。尽管你能够通过剪支来压缩大模型，但它是一个多阶段的操作，并且无论模型多小，肯定存在精度的损失。过去几年检测器的改进有了非常打的进步，但是我们仍然没有探索出一种从0开始设计一个有效的检测模型的方法。在[**fficientNet**](https://medium.com/@nainaakash012/efficientnet-rethinking-model-scaling-for-convolutional-neural-networks-92941c5bfb95)论文中展示了如何拓展CNNs，它对目标检测器中高级研究是有贡献的，另外，在实际应用场景中，例如机器人和无人驾驶汽车，**模型大小，内存占用和延迟性**对模型的部署来说尤为重要。
