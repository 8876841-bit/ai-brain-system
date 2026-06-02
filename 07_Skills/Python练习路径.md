---
status: 深挖中
type: Skill
tags: [Python, 练习, 实操]
---

# Python 练习路径

**原则**：每一步都要跑起来，看到结果，再往下走。不要只看不动手。

---

## 第一关：跑起来（1天）

**目标**：在你的电脑上运行第一个Python文件。

1. 打开终端，输入 `python3 --version`，确认Python已安装
2. 新建一个文件 `hello.py`，写入：
   ```python
   print("你好，我在学Python")
   name = "政立路"
   area = 53
   print(f"案例：{name}，面积：{area}平")
   ```
3. 终端运行：`python3 hello.py`
4. 看到输出就过关

---

## 第二关：操作字典（1-2天）

**目标**：能创建和读取字典，因为JSON就是字典。

```python
case = {
    "name": "政立路",
    "area": 53,
    "owner": "独居女性",
    "tags": ["猫", "宜家", "温柔风"]
}

# 练习：
print(case["name"])             # 取单个值
print(case["tags"][0])          # 取列表里的第一个
case["style"] = "奶油白"        # 新增一个键
print(case)                     # 打印整个字典
```

**过关条件**：自己新建一个案例字典，包含至少5个字段，能取值、能新增。

---

## 第三关：读写文件（1-2天）

**目标**：能把案例信息存到文件，再读出来。

```python
# 写：把案例存成文本
with open("政立路.txt", "w", encoding="utf-8") as f:
    f.write("客户：独居女性\n")
    f.write("面积：53平\n")
    f.write("特点：有猫，偏爱温柔风，宜家桌面板\n")

# 读：把文件内容读出来
with open("政立路.txt", "r", encoding="utf-8") as f:
    content = f.read()
    print(content)
```

**过关条件**：能把政立路案例信息写进文件，再读出来打印。

---

## 第四关：调用Claude API（2-3天）

**目标**：用Python发一条消息给Claude，收到回复。

1. 安装依赖：
   ```bash
   pip install anthropic python-dotenv
   ```

2. 新建 `.env` 文件，写入API Key：
   ```
   ANTHROPIC_API_KEY=你的key
   ```

3. 新建 `test_api.py`：
   ```python
   from dotenv import load_dotenv
   import anthropic

   load_dotenv()
   client = anthropic.Anthropic()

   message = client.messages.create(
       model="claude-opus-4-7",
       max_tokens=512,
       messages=[
           {"role": "user", "content": "你好，我在测试API，请回复一句话"}
       ]
   )

   print(message.content[0].text)
   ```

**过关条件**：成功收到Claude的回复，打印出来。

---

## 第五关：搭一个最简单的知识库（3-5天）

**目标**：把政立路案例存成文本，让Claude基于这个文本回答问题。

```python
from dotenv import load_dotenv
import anthropic

load_dotenv()
client = anthropic.Anthropic()

# 读取你的案例文件
with open("政立路.txt", "r", encoding="utf-8") as f:
    knowledge = f.read()

# 问一个具体问题
question = "根据这个案例，适合做哪几条短视频？"

# 把案例塞进prompt
prompt = f"""根据以下案例信息回答问题。

案例信息：
{knowledge}

问题：{question}
"""

message = client.messages.create(
    model="claude-opus-4-7",
    max_tokens=1024,
    messages=[{"role": "user", "content": prompt}]
)

print(message.content[0].text)
```

**过关条件**：AI给出的回答里出现了政立路案例的具体细节，而不是通用答案。

---

## 每一关遇到报错怎么办

1. 把报错信息完整复制
2. 发给Claude Code（我）或者罗西
3. 不要猜，不要乱改，先搞清楚报错是什么意思

---

## 时间预估

| 关卡 | 时间 | 验收标准 |
|------|------|---------|
| 第一关 | 1天 | 跑起来，看到输出 |
| 第二关 | 1-2天 | 能操作字典 |
| 第三关 | 1-2天 | 能读写文件 |
| fourth关 | 2-3天 | 能调通API |
| 第五关 | 3-5天 | AI用你的数据回答问题 |

**五关打完 = 有能力搭知识库的基础已经有了。**
