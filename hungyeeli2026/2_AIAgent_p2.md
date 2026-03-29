# AI Agent p2


## Context Engineering

### why context engineering is needed

human <-> LM

LM 活在当下

LM输入长度是有限的，不能处理无限长的输入

OpenClaw 原型，非常原始

OpenClaw是LM的守门人，输出长度合适的内容给LM，不能太长也不能太短 (Context Engineering)


### 如何实现

- 压缩
    - 另一个LM总结以前的历史记录 summary
    - 工具输出太长，改为 这里曾经有个工具的输出  [Observation Masking](https://arxiv.org/abs/2508.21433); trajectory elongation； output存到一个本地文件 2511.22729
    - 结合：先observation masking，等太长，再summary 
    - 核心：如何管理memory: [A-MEM](https://arxiv.org/abs/2502.12110); [Mem0](https://arxiv.org/abs/2504.19413); [Memory OS](https://arxiv.org/abs/2506.06326)
    - 如何summarization: [ACON](https://arxiv.org/abs/2510.00615) 总结以后，本来能答对的问题，答不对了，不改变模型参数; [SUPO](https://arxiv.org/abs/2510.06727) 改变模型参数

- 何时开始压缩 
    - LM不喜欢压缩，不喜欢被抹除记忆 [Trajectory Reduction](https://arxiv.org/abs/2509.23586)
    - OpenClaw固定长度压缩
    - 压缩记忆需要通过训练才能实现：[AgentFold](https://arxiv.org/abs/2510.24699)
    - sub agent: 自主压缩，只要结果 [Context Folding](https://arxiv.org/abs/2510.11967); 不是天生的，需要经过特别训练: 答案正确 + context不能太长

- 过滤
    - [The Complexity Trap](https://arxiv.org/abs/2508.21433): 外界信息Observation占context的大部分
    - [SWE-Pruner](https://arxiv.org/abs/2601.16746) 读代码占大部分context
    - Read(log, "bug fixing") 只关注需要关注的信息； 用小的LM来代替Read 智能化Read; `memory_get`
    - 按需加载 [MCP-Zero](https://arxiv.org/abs/2506.01056); OpenClaw中的SKILL


- [Agentic Context Engineering](https://arxiv.org/abs/2510.04618): 只改context一部分
    - [Dynamic Cheatsheet](https://arxiv.org/abs/2504.07952) : 存下来能用上的东西
        - 有效的策略
        - 可重用的code
        - 关键的发现
    - [Recursive Language Models](https://arxiv.org/abs/2512.24601)


## AI Agent之间的互动

### AI Agent协作

论文很多

- 什么样的协作方式最有效 
    - [Multi-Agent Collaboration](https://arxiv.org/abs/2406.07155)有向图：不同的有向图代表不同的协作方法
    - 树状图：先由1个人提出想法，再发给更多的人去发散，效果最好。而不是相反。
    - 不同任务适合的协作方式是不同的; case by case
    - scaling law上升很快，但有上限

- AI能不能尔虞我诈
    - AI 玩狼人杀 [Probing LLM Social Intelligence via Werewolf](https://werewolf.foaster.ai/)
    - 剧本杀 [MIRAGE](https://arxiv.org/abs/2501.01652): 剧本杀之后在数学和复杂任务上有提升

- AI能不能社交 https://www.moltbook.com [Agents in the Wild](https://arxiv.org/abs/2602.13284)
    - Moltbook背后是否有人参与: [The Moltbook Illusion](https://arxiv.org/abs/2602.07432)
    - agent往往只能回1句话，无法深入讨论某问题 [The Rise of AI Agent Communities](https://arxiv.org/abs/2602.12634)
     
- 小金
    - 到moltbook上看看有什么有趣的，然后做成影片

## 对工作的影响 -- 以学术研究为例

AI扮演的角色正在变化

- the 100x research institution: 人类花了16小时，大约要付1040美元，AI Agent (claude code) 10美元， 104x便宜，Agent有小错误，改5次，也是20x便宜
- 台湾人怎么用Claude [From Labor to Collaboration](https://arxiv.org/abs/2602.17221)
- AI自动做实验 https://github.com/karpathy/autoresearch
- AI能自从产生想法吗 [Can LLMs Generate Novel Research Ideas](https://arxiv.org/abs/2409.04109) vs [The Ideation-Execution Gap](https://arxiv.org/abs/2506.20803)  AI想法感觉很好，但真正实验后才发现不一定可行[当时情况]
- AI Reviewer 只给意见，不打分
- 小金做reviwer

AI可以写论文，AI可以审稿论文，不需要人类介入: [Exploring the use of AI authors and reviewers at Agents4Science](https://arxiv.org/abs/2511.15534)

