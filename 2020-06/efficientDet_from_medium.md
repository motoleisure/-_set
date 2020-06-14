- [Original Link - EfficientDet: Scalable and Efficient Object Detection](https://medium.com/@nainaakash012/efficientdet-scalable-and-efficient-object-detection-ea05ccd28427)

## EfficientDet: 可拓展的和有效的目标检测
- 目标检测发展了很长的一段时间。由目标检测中的比较琐碎的计算机视觉技术发展到高级的目标检测器，这个改进非常的巨大。卷积神经网络(CNNs)，在这次变革中担任了一个非常重要的角色。我们希望我们的检测器的精度尽可能的高，并且尽可能的快，能够做到实时。但这个两个指标(精度和速度)存在一个权衡，而大多数的检测器都是在其中一个指标表现好，另外一个指标的表现则相对较差的。通常地，精度更高的检测器需要更多的计算量，但这不是一个很好的应用场景。所以，我们在不断寻求更高效的检测模型。这篇来自谷歌大脑团队的论文提出了一个新的检测器家族，它们是更加**高效的**，更加准确的和更快的。

### 为什么我们在讨论效率？
- 我们想到的一个比较自然的问题就是，为什么我们那么在乎效率呢？我们不是更应该考虑检测器的精度吗？总之，我们知道有些技术像[**Global Filter Pruning**](https://medium.com/@nainaakash012/gate-decorator-global-filter-pruning-afc12fcc71c6)，是能够用来压缩大的模型的。

- 
