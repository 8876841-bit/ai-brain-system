---
status: 已理解
type: Concept
tags: [Python, PyTorch, numpy, tensor, 编程基础]
---

# Python 工具基础

来自 45 天学习计划 Day 3 的手写问题。

---

## numpy 是什么？

Python 的数学计算库，专门处理多维数组和矩阵运算。

类比：Excel 能做表格运算，numpy 能做更复杂的数学矩阵运算，而且速度极快。AI 训练需要大量矩阵计算，numpy 提供这些底层工具。

---

## PyTorch 是什么？

构建和训练神经网络的框架。

类比：如果 numpy 是 Excel，PyTorch 就是整个数据分析软件。它让你定义神经网络结构、计算梯度、训练模型。目前 AI 研究领域最主流的框架。

---

## tensor 是什么？

多维数组，AI 里所有数据都用 tensor 表示。

- 1维 tensor = 一行数字（列表）
- 2维 tensor = 一个表格（矩阵）
- 3维 tensor = 多个表格叠在一起

token 的 embedding 向量、注意力矩阵、模型权重——全都是 tensor。

---

## shape 是什么？

shape 描述 tensor 的维度大小。

在 transformer 里，输入数据的 shape 通常是 `[batch, seq, hidden]`：

| 维度 | 含义 | 例子 |
|------|------|------|
| batch | 一次处理几条文本 | 32 |
| seq | 每条文本有几个 token | 512 |
| hidden | 每个 token 用多少维向量表示 | 768 |

shape = [32, 512, 768] 表示：同时处理 32 条文本，每条 512 个 token，每个 token 用 768 维向量表示。

---

## Linear 层是什么？

神经网络里最基本的变换操作，把输入向量乘以一个权重矩阵，变成另一个向量。

类比：把一个坐标系里的点，映射到另一个坐标系。

transformer 里的 Q、K、V 矩阵就是三个 Linear 层——把 embedding 向量分别变换成 Query、Key、Value 向量。

---

## FFN 是什么？

Feed Forward Network，前馈神经网络。

在 transformer 里，每个 attention 层后面都有一个 FFN：两个 Linear 层 + 一个激活函数。

作用：attention 负责建立词语之间的关系，FFN 负责对每个 token 的表示进行进一步加工，增加模型的非线性表达能力。

attention + FFN 是 transformer 一个完整 block 的两个核心部件。

## 关联

[[Transformer架构]]
