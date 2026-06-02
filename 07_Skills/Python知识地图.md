---
status: 深挖中
type: Skill
tags: [Python, 编程, 知识库, API]
---

# Python 知识地图

目标：能搭知识库、能调API、能让工具从通用回答变成有针对性的回答。

不是学完整的Python，是学**够用的Python**。

---

## 第一层：能跑起来

**变量和基础数据类型**
```python
name = "政立路"          # 字符串 str
area = 53               # 数字 int
is_female = True        # 布尔 bool
```

**列表和字典**（最重要，JSON就是这个）
```python
# 列表 - 一组东西
tags = ["独居", "女性", "猫"]

# 字典 - 键值对，就是JSON
case = {
    "name": "政立路",
    "area": 53,
    "style": "温柔"
}

# 取值
print(case["name"])     # 输出：政立路
```

**函数**
```python
def greet(name):
    return f"你好，{name}"

result = greet("倩倩")
print(result)           # 输出：你好，倩倩
```

**循环**
```python
for tag in tags:
    print(tag)          # 依次输出 独居、女性、猫
```

---

## 第二层：能读写文件

知识库的核心就是读写文件。

```python
# 读文件
with open("案例.txt", "r", encoding="utf-8") as f:
    content = f.read()

# 写文件
with open("输出.txt", "w", encoding="utf-8") as f:
    f.write("政立路案例处理完成")
```

---

## 第三层：能装库、能调API

**安装第三方库**
```bash
pip install requests          # 发网络请求
pip install python-dotenv     # 读取.env文件
pip install anthropic         # 调用Claude API
```

**保护API Key（.env文件）**
```
# .env 文件里写
ANTHROPIC_API_KEY=sk-ant-xxxxxx
```

```python
# 代码里读取
from dotenv import load_dotenv
import os

load_dotenv()
api_key = os.getenv("ANTHROPIC_API_KEY")
```

**调用Claude API**
```python
import anthropic

client = anthropic.Anthropic()

message = client.messages.create(
    model="claude-opus-4-7",
    max_tokens=1024,
    messages=[
        {"role": "user", "content": "政立路这个案例适合做什么类型的视频？"}
    ]
)

print(message.content[0].text)
```

---

## 第四层：能搭知识库（RAG雏形）

知识库最简单的形态：把你的案例文本存好，让AI读着回答。

```python
# 1. 读取你的知识库文件
with open("案例/政立路.txt", "r", encoding="utf-8") as f:
    knowledge = f.read()

# 2. 把知识塞进prompt
prompt = f"""
你是木属木艺的助手。根据以下案例信息回答问题。

案例信息：
{knowledge}

问题：这个案例适合做哪几条短视频？
"""

# 3. 发给AI
message = client.messages.create(
    model="claude-opus-4-7",
    max_tokens=1024,
    messages=[{"role": "user", "content": prompt}]
)

print(message.content[0].text)
```

这就是RAG最朴素的实现——把你的数据塞进去，AI基于你的数据回答，而不是凭空猜。

---

## 不需要现在学的

- 面向对象（class）
- 异步编程（async/await）
- 算法和数据结构
- 爬虫
- 机器学习框架

先把上面四层用熟，够用了。
