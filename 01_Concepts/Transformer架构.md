---
status: 深挖中
type: Concept
tags: [AI, Transformer, 深度学习, LLM]
---

# Transformer 架构

帮助 AI 同时阅读整段文字、考虑每个词之间关系的架构模板。GPT、Claude 等大模型的底层都是 transformer。

## 核心组件

### Token
最小的输入单元，词语被拆成 token 进入模型。

### Embedding（嵌入）
把 token 变成数值坐标（向量），代表这个词在模型里的语义位置。语义相近的词，坐标也相近。

### Position Encoding（位置编码）
告诉模型每个 token 在序列里的位置。因为 attention 本身不感知顺序，所以需要额外注入位置信息。

### Self-Attention（自注意力）
词语之间建立上下文关系。每个词都会"看"句子里其他词，判断谁对自己最重要。

### Multi-Head Attention（多头注意力）
同时跑多次 self-attention，每个"头"关注不同维度的关系，最后合并。

### Feed Forward Network（前馈神经网络）
attention 之后的加工层，快速归纳、整理信息。

### Layer Normalization（层归一化）
让每一层的数据保持稳定，防止层数越深越混乱。多层叠加时保证各层数据同步。

## Transformer → GPT

GPT = **G**enerative **P**re-trained **T**ransformer

- Generative：生成式，输出文字
- Pre-trained：在大量数据上预训练
- Transformer：底层架构

GPT 是基于 transformer 的文本生成模型。

## 关联

[[AI Agent底层原理]] [[RAG检索增强]]
