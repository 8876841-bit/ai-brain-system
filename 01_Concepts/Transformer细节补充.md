---
status: 已理解
type: Concept
tags: [Transformer, KV Cache, Tokenizer, 上下文]
---

# Transformer 细节补充

来自 45 天学习计划 Day 6、8 的手写问题。

---

## KV Cache 是什么？如何理解？

KV Cache = 把之前计算过的 Key 和 Value 矩阵缓存下来，不用每次重新算。

**为什么需要它：**
生成文字时，每产生一个新 token，模型需要计算它和前面所有 token 的 attention。如果文本很长，每次都重新计算所有 K、V，非常浪费。

**KV Cache 的做法：**
计算过的 K、V 存下来，生成下一个 token 时直接用，只计算新 token 的部分。

**代价：**
KV Cache 占用大量显存。文本越长，缓存越大，成本越高。这是为什么长上下文模型更贵的原因之一。

---

## Tokenizer 如何拆解文字？

Tokenizer 把文字拆成 token，不同语言拆法不同：

| 语言 | 拆法 | 例子 |
|------|------|------|
| 英文 | 按词根拆 | "running" → "run" + "ning" |
| 中文 | 通常每字一个 token，或常见词组 | "定制" → 1-2个token |
| 代码 | 按语法单元 | "def" 是一个 token |

**如何判断 token 数：**
同样的内容，中文 token 数 > 英文 token 数。所以用中文调用 API，成本通常更高。

---

## 上下文窗口里都放了什么？

上下文窗口的空间是有限的（比如 128K tokens），里面塞了：

1. **system prompt**：角色定义和规则
2. **历史对话消息**：messages 数组
3. **工具调用结果**：tool 返回的内容
4. **RAG 检索内容**：从知识库里取出来的相关段落

所有这些加起来不能超过上下文窗口限制，所以需要上下文管理——压缩、截断、摘要。

## 关联

[[Transformer架构]] [[Agent核心概念]] [[RAG与向量检索]]
