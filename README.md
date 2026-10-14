# 🤖 Agent 面试 100 问（中文带答案）

> AI Agent 工程师面试手册：从 Agent 基础概念到多智能体架构，100+ 道高频面试题全中文带答案，基础/进阶/实战三级分级，一册在手，Agent 岗面试无忧。

![stars](https://img.shields.io/badge/⭐-给个Star吧-red)
![license](https://img.shields.io/badge/license-MIT-blue)
![status](https://img.shields.io/badge/status-持续更新-green)

## 为什么要有这本手册？

2025 年开始，**AI Agent 岗位爆发式增长**。但市面上的面试资料要么是英文的、要么零散不成体系、要么只有题目没有答案。

这本手册把 Agent 岗位面试的高频问题**一次性整理全**：

- ✅ **100+ 道题**：覆盖 Agent 全知识体系
- ✅ **全中文带答案**：背下来就能答
- ✅ **三级分级**：基础题保底、进阶题加分、实战题脱颖而出
- ✅ **真实场景题**：贴近大厂实际面试
- ✅ **持续更新**：紧跟 Agent 技术演进

## 📚 内容目录

### 一级：Agent 基础（30 题）

#### 概念篇
1. **什么是 AI Agent？和传统 LLM 应用有什么区别？**
   > LLM 应用通常是"一次性问答"：用户提问 → 模型回答。Agent 则是"目标驱动的自主系统"：它能理解目标、拆解任务、调用工具、观察结果、迭代调整，直到完成任务。核心区别在于：Agent 有**规划（Planning）**、**工具使用（Tool Use）**、**记忆（Memory）**和**自主循环（Agentic Loop）**。

2. **Agent 的核心组成有哪些？**
   > 四要素：①大脑（LLM，负责推理决策）②工具（Tools/Function Calling，负责执行）③记忆（Memory，短期+长期）④环境（Environment，Agent 与之交互的场所）。四者通过"感知-思考-行动-观察"循环连接。

3. **什么是 ReAct 模式？**
   > ReAct = Reasoning + Acting。模型交替进行"推理（Thought）"和"行动（Action）"，行动产生观察（Observation），观察再驱动下一轮推理。举例：查天气任务，模型先想"我需要查北京的天气"→ 调用 get_weather(北京) → 观察返回结果 → 生成最终回答。

4. **什么是 CoT（Chain of Thought）？和 ReAct 什么关系？**
   > CoT 是"思维链"：让模型分步推理，输出中间步骤。ReAct 是 CoT 的扩展，在推理基础上加入了"行动"（调用工具）。可以说 ReAct = CoT + Tool Use。

5. **什么是 Function Calling？和 Tool Use 是一回事吗？**
   > Function Calling 是 OpenAI 提出的 API 机制：模型输出结构化的函数调用参数，由应用侧执行。Tool Use 是更宽泛的概念，泛指 Agent 调用外部工具的能力。Function Calling 是 Tool Use 的一种主流实现方式。

6. **什么是 Plan-and-Execute 架构？**
   > 两阶段：先由 Planner（规划器）制定完整计划，再由 Executor（执行器）逐步执行。相比 ReAct 的"边想边做"，Plan-and-Execute 先规划后执行，适合复杂长任务，但应对动态变化能力较弱。

7. **什么是 Agentic Loop（智能体循环）？**
   > Agent 的核心运行循环：接收任务 → 思考推理 → 选择行动（调用工具）→ 观察结果 → 再思考……直到满足终止条件。这个循环也叫 Agent 的主循环（Main Loop）。

8. **Agent 和 RAG 有什么区别？**
   > RAG 是"检索增强生成"：查资料 → 拼进上下文 → 生成回答，本质是**增强知识**。Agent 是"自主执行"：拆任务 → 调工具 → 完成目标，本质是**增强行动**。两者可以结合：RAG 给 Agent 提供知识，Agent 用 RAG 完成信息密集型任务。

9. **什么是 Multi-Agent（多智能体）系统？**
   > 多个 Agent 协作完成任务的系统。常见模式：①主管-下属（Orchestrator-Workers）②辩论模式（Debate）③流水线模式（Pipeline）④市场模式（市场竞价选最优）。代表框架：AutoGen、CrewAI、LangGraph。

10. **Agent 和 Workflow 有什么区别？**
    > Workflow 是**预定义流程**：步骤固定，如"先翻译再润色"。Agent 是**动态决策**：由 LLM 决定下一步做什么。Workflow 确定性强、可预测；Agent 灵活但不可控。业界观点（如 Anthropic）：优先用简单 Workflow，必要时才上 Agent。

#### 工程篇
11. **什么是 MCP（Model Context Protocol）？**
    > Anthropic 提出的开放协议，统一了 LLM 与外部工具/数据源的连接方式，类似"AI 世界的 USB-C 接口"。通过 MCP，一个 Agent 可以接入任意实现了该协议的服务器，实现工具标准化接入。

12. **Agent 的上下文窗口（Context Window）不够用怎么办？**
    > 常见方案：①摘要压缩（对历史对话滚动摘要）②滑动窗口（只保留最近 N 轮）③向量检索（把历史存向量库，按需召回）④记忆分层（短期/长期记忆分离）。

13. **什么是 System Prompt 注入？如何防护？**
    > 攻击者把恶意指令混入用户输入或检索内容，诱导 Agent 执行非预期行为。防护：①输入/输出过滤 ②指令与数据隔离（用特殊分隔符）③权限最小化（Agent 只有最小工具权限）④对模型输出做校验 ⑤敏感操作人工确认。

14. **Agent 如何做长期记忆？**
    > 三种主流：①外部存储（向量数据库存 Embedding，如 Chroma/Pinecone）②摘要记忆（定期把历史摘要化）③结构化记忆（存到数据库表，按实体/关系组织）。生产环境常用"向量检索 + 摘要"混合方案。

15. **什么是 Embedding？Agent 里哪里会用到？**
    > Embedding 是把文本转成向量。Agent 里用于：①记忆检索（相似历史回忆）②RAG 知识检索 ③工具选择（语义匹配哪个工具合适）④用户意图分类。

#### 模型篇
16. **Agent 用的模型和普通对话模型有什么不同要求？**
    > Agent 模型需要：①强指令遵循（听懂复杂任务）②可靠的 Function Calling 能力 ③长上下文处理 ④较强的规划推理。业界常用 Claude、GPT、DeepSeek 等支持 Function Calling 的模型。

17. **什么是 Toolformer？**
    > 让模型自己学会用工具的经典论文方法：模型在文本中标记"需要调用工具的位置"，用自监督方式训练。是早期"模型工具学习"的代表作。

18. **什么是 Function Calling 的 JSON Schema？举例说明。**
    > 通过 JSON Schema 描述工具的参数结构，模型按 Schema 输出调用。例如查询天气工具：`{"name": "get_weather", "parameters": {"type": "object", "properties": {"city": {"type": "string"}}, "required": ["city"]}}`。模型输出 `{"name": "get_weather", "arguments": {"city": "北京"}}`。

19. **Agent 幻觉问题怎么缓解？**
    > ①工具结果优先（回答基于工具返回，不靠模型记忆）②强制引用来源 ③校验工具输出格式 ④对高风险结论要求多步验证 ⑤用更强的推理模型做关键决策。

20. **什么是 Self-Consistency（自洽性）？**
    > 让模型对同一问题多次采样推理，投票选最一致的答案。用于提高 Agent 关键决策的可靠性，代价是多次调用成本。

### 二级：Agent 进阶（40 题）

#### 规划与推理
21. **ReAct 和 Plan-and-Execute 怎么选？**
    > 任务简单直接、需要快速响应 → ReAct（边想边做）。任务复杂、步骤多、可以预先规划 → Plan-and-Execute（先规划后执行）。生产实践中也常混合：先规划大步骤，每步内部用 ReAct。

22. **什么是 Reflexion（反思）机制？**
    > Agent 执行失败后，把失败原因写进记忆，下次遇到类似情况避免再犯。三要素：Actor（执行）、Evaluator（评估）、Self-Reflection（自我反思）。适合需要试错的 Agent。

23. **什么是 ReWOO（Reasoning WithOut Observation）？**
    > 把"推理"和"观察"解耦：模型先一次性生成完整的工具调用计划（不等待工具结果），再统一执行。优点：减少 LLM 调用次数、节省 token。缺点：无法根据中间结果动态调整。

24. **什么是 Tree of Thoughts（思维树）？**
    > 让模型同时探索多条推理路径，像树一样分叉，评估每条路径，选择最优。比 CoT 探索空间更大，适合复杂推理问题，但成本高。

25. **Agent 规划时如何避免"规划幻觉"？**
    > 规划幻觉 = 计划看着合理但不可执行。缓解：①规划时注入工具能力清单 ②每步执行后校验是否与计划一致 ③计划要可验证（有明确完成标准）④失败时重新规划而不是硬执行。

26. **什么是任务分解（Task Decomposition）？怎么拆？**
    > 把大任务拆成可执行的小步骤。方法：①LLM 直接分解（给模型任务让它拆）②模板化分解（按固定模式，如"调研→整理→成稿"）③层次分解（递归拆到原子任务）。好拆分的标准：每步足够小、可执行、有明确产物。

27. **Agent 遇到工具失败怎么处理？**
    > ①重试（带退避）②换工具（同样能力的不同实现）③降级（绕过该步骤或人工介入）④重新规划（任务本身换思路）。生产系统必须有完善的失败处理和重试策略。

28. **如何给 Agent 设定"停止条件"？**
    > ①任务完成判定（产出物满足验收标准）②最大迭代次数（防止死循环）③用户确认（关键节点停下来问用户）④超时限制。真实系统通常组合使用。

29. **什么是 Agent 的"成本控制"？怎么控制？**
    > 成本主要来自 LLM 调用。控制手段：①减少无效循环（用 ReWOO 式预规划）②缓存重复调用 ③用便宜模型做简单子任务（模型路由）④限制最大调用次数 ⑤小模型预筛，大模型精处理。

30. **Agent 的延迟优化有哪些手段？**
    > ①并行调用（多个独立工具同时调）②流式输出（边生成边返回）③轻量模型优先 ④预加载常用上下文 ⑤工具结果缓存。

#### 记忆与状态
31. **短期记忆和长期记忆分别怎么实现？**
    > 短期：直接把对话历史放上下文（受窗口限制）。长期：①向量库（语义检索）②KV 存储（如 Redis，按 key 存取）③数据库（结构化）。Agent 框架里短期记忆常在会话对象中，长期记忆通过存储服务。

32. **Agent 的对话历史太长怎么压缩？**
    > ①递归摘要（摘要再摘要）②关键信息抽取（只保留实体、决策、待办）③时间衰减（旧消息降权）④标记重要消息（用户明确"记住这个"）。

33. **多 Agent 之间如何共享记忆？**
    > ①共享消息总线（所有 Agent 读写同一队列）②共享向量库（共同记忆池）③黑板书模式（共享一块可写区域，如 LangGraph 的 State）④数据库（结构化共享）。

34. **什么是会话状态（Session State）？Agent 里如何管理？**
    > 会话状态 = Agent 运行过程中的所有上下文（对话历史、工具结果、中间变量、目标进度）。管理要点：①状态序列化（可持久化、可恢复）②状态版本化（支持回滚）③状态隔离（多会话互不干扰）。

#### 工具与生态
35. **如何设计一个好的 Agent 工具？**
    > ①单一职责（一个工具只做一件事）②参数简单（Schema 清晰、必有参数明确）③描述清晰（让模型理解何时用）④容错（工具本身处理异常）⑤返回结构化（方便模型解析）。

36. **工具返回结果太长怎么处理？**
    > ①截断 + 摘要（把长结果先摘要）②分页获取 ③结构化提取（只留关键字段）④存文件返回引用（返回"结果已存 /tmp/x.json"）。

37. **什么是 Parallel Tool Calls（并行工具调用）？**
    > 模型一次输出多个工具调用，应用侧并行执行。OpenAI 的 Function Calling 原生支持。适合无依赖关系的多个调用，能显著降低延迟。

38. **工具调用结果如何校验？**
    > ①Schema 校验（JSON 格式对不对）②业务校验（数值合理吗）③语义校验（结果和问题匹配吗）④对工具输出做安全过滤（防注入）。

39. **什么是 Tool Schema？为什么要做 Schema 校验？**
    > Tool Schema 是工具的"接口契约"，描述工具名、参数、返回。校验防止：①模型输出格式错误 ②参数越界 ③恶意输入。生产环境必做。

40. **Agent 如何选择正确的工具？**
    > ①语义匹配（Embedding 相似度找最相关工具）②LLM 直接选择（把工具列表给模型让它选）③规则路由（按关键词/意图命中）④混合（先用轻量分类，再让 LLM 确认）。

#### 框架与实现
41. **LangChain 和 LangGraph 的区别？**
    > LangChain 是早期框架：链式（Chain）编排，偏简单流程。LangGraph 是其升级：基于图的编排，支持循环、分支、状态管理，更适合 Agent（Agent 本质是循环）。官方也推荐复杂 Agent 用 LangGraph。

42. **AutoGen 的核心设计思想？**
    > 微软的 Agent 框架，核心是"多 Agent 对话"：多个可对话的 Agent（用户代理、助手代理、工具代理）通过消息对话协作。强调对话驱动。

43. **CrewAI 和 AutoGen 有什么区别？**
    > CrewAI 主打"角色扮演"模式：定义 Role（角色）、Goal（目标）、Backstory（背景），像组队一样让 Agent 协作，使用简单。AutoGen 更底层、更灵活。CrewAI 适合快速搭协作型应用，AutoGen 适合深度定制。

44. **什么是 Agent 的 State（状态）？LangGraph 里怎么管理？**
    > LangGraph 用 State（通常是一个 TypedDict/消息列表）保存 Agent 运行状态，节点之间通过 State 传递数据。支持增删改、持久化、检查点（Checkpoint）。

45. **LangGraph 的节点（Node）和边（Edge）怎么设计？**
    > Node = 处理单元（LLM 调用、工具执行、逻辑判断）。Edge = 节点间转移（条件边：根据状态决定下一步走哪个节点）。Agent 就是"LLM 节点 → 工具节点 → 回到 LLM"的循环图。

46. **什么是 Agent 的"条件路由"？举例。**
    > 根据当前状态动态决定下一步。例：LLM 节点输出后，若有工具调用 → 走工具节点；否则 → 走输出节点。LangGraph 里用 add_conditional_edges 实现。

47. **什么是 Checkpoint（检查点）？有什么用？**
    > 保存 Agent 在某个时间点的完整状态（State）。用途：①断点续跑（失败后从检查点恢复）②人工介入（暂停在检查点等用户确认）③时间旅行（回溯历史状态）。

48. **Agent 框架里如何实现"人工介入"（Human-in-the-loop）？**
    > ①Interrupt（LangGraph 的暂停机制，中断后等用户输入再继续）②审批节点（关键动作前停住，等批准）③审核队列（异步人工审核工具结果）。高风险的 Agent 必配。

49. **如何给 Agent 做日志和追踪（Tracing）？**
    > 记录每个节点的输入输出、工具调用、token 消耗、耗时。工具：LangSmith、Langfuse、Phoenix 等。生产必备，用于排查问题、评估效果、优化成本。

50. **什么是 Agent 的 Prompt 模板化？怎么做？**
    > 把 Agent 的 System Prompt 拆成可组合的模块（角色、工具说明、约束、输出格式），动态拼装。好处：易维护、易测试、不同场景复用。

### 三级：Agent 实战（30 题）

#### 场景设计题
51. **设计一个客服 Agent，你会怎么做？**
    > 思路：①知识底座（RAG 挂接 FAQ/工单库）②意图识别（分类：查订单/退款/投诉）③工具接入（查订单、退款、转人工等）④升级机制（无法解决转人工）⑤安全（敏感信息脱敏）。架构：意图分类 → 路由 → 各场景子流程（可多 Agent）→ 兜底转人工。

52. **设计一个代码生成 Agent，核心难点是什么？**
    > 难点：①上下文太长（仓库太大）②代码正确性验证 ③迭代修改（不只是生成一次）④安全（不能执行恶意代码）。方案：仓库索引（Embedding + 代码检索）→ 生成 → 测试执行（沙箱）→ 失败反馈迭代。

53. **设计一个浏览器 Agent（能自己操作网页），要注意什么？**
    > ①DOM 解析（页面结构转 LLM 可读格式）②元素定位（ref/选择器）③操作验证（点没点中）④反爬和验证码处理 ⑤任务失败恢复（页面变化重试）。代表：Browser Use、Claude Computer Use。

54. **设计一个数据分析 Agent？**
    > ①数据源接入（数据库/文件）②NL2SQL（自然语言转查询）③可视化（图表生成）④结论生成（解读结果）⑤权限（数据访问控制）。难点：查询正确性验证、敏感数据保护。

55. **多 Agent 协作时如何避免"互相打架"（资源竞争/重复劳动）？**
    > ①任务分配明确（主管 Agent 负责拆分和调度）②共享状态锁（同一资源互斥访问）③角色边界清晰（每个 Agent 只做自己的事）④结果去重（统一汇总层）。

56. **Agent 任务失败率太高怎么优化？**
    > ①加验证节点（每步检查中间结果）②加重试和降级 ③简化任务分解 ④加反思机制（Reflexion）⑤换更强的模型做决策 ⑥人工审核兜底。

57. **如何评估一个 Agent 的效果？**
    > ①任务成功率（核心指标）②步骤有效率（多少次调用完成任务）③成本（token 消耗）④延迟⑤用户满意度。工具：AgentBench、τ-bench、LangSmith 评估。

58. **Agent 上线前要测哪些场景？**
    > ①正常流程 ②边界输入（超长、空、特殊字符）③工具失败 ④模型幻觉 ⑤注入攻击 ⑥并发和压测 ⑦长会话（上下文累积）。

59. **Agent 系统如何做灰度发布？**
    > ①流量比例（先 5% 用户）②影子模式（新旧并行，对比结果）③功能开关（按场景开关 Agent 能力）④监控告警（成功率/成本异常自动回滚）。

60. **给 Agent 设计权限体系，怎么做？**
    > ①最小权限（工具粒度授权）②分级审批（高风险操作需人工）③操作审计（全量日志）④数据脱敏（敏感字段过滤）⑤用户隔离（多租户数据隔离）。

#### 手撕代码题
61. **用 Python 实现一个最简单的 ReAct Agent（伪代码级）。**
    > ```python
    > def agent(task, tools, llm, max_steps=10):
    >     messages = [{"role": "system", "content": "你是Agent..."}]
    >     for _ in range(max_steps):
    >         resp = llm(messages)
    >         if resp["type"] == "final":
    >             return resp["answer"]
    >         result = tools[resp["tool"]](**resp["args"])
    >         messages.append(resp)
    >         messages.append({"role": "tool", "content": result})
    >     return "超时"
    > ```

62. **实现一个工具调度器（Tool Router）。**
    > ```python
    > class ToolRouter:
    >     def __init__(self):
    >         self.tools = {}
    >     def register(self, name, func, schema):
    >         self.tools[name] = {"func": func, "schema": schema}
    >     def call(self, name, args):
    >         if name not in self.tools:
    >             raise ValueError(f"工具不存在: {name}")
    >         return self.tools[name]["func"](**args)
    > ```

63. **如何把工具输出压缩后给模型？写一个摘要器。**
    > ```python
    > def summarize_tool_result(raw: str, max_len: int = 1000, llm=None):
    >     if len(raw) <= max_len:
    >         return raw
    >     if llm:
    >         return llm(f"用{max_len}字以内摘要：{raw[:max_len*4]}")
    >     return raw[:max_len] + "...(已截断)"
    > ```

64. **实现一个带重试的工具调用。**
    > ```python
    > import time
    > def call_with_retry(fn, *args, retries=3, delay=1, **kwargs):
    >     for i in range(retries):
    >         try:
    >             return fn(*args, **kwargs)
    >         except Exception as e:
    >             if i == retries - 1:
    >                 raise
    >             time.sleep(delay * (2 ** i))
    > ```

65. **实现 Agent 的简单记忆（向量检索版，伪代码）。**
    > ```python
    > class Memory:
    >     def __init__(self):
    >         self.items = []
    >     def add(self, text, embed_fn):
    >         self.items.append((text, embed_fn(text)))
    >     def recall(self, query, embed_fn, top_k=3):
    >         q = embed_fn(query)
    >         scored = sorted(self.items, key=lambda x: cos(x[1], q), reverse=True)
    >         return [t for t, _ in scored[:top_k]]
    > ```

66. **写一个"停止条件"判断器。**
    > ```python
    > def should_stop(step, max_steps, goal_met, user_confirm=False):
    >     if goal_met: return "任务完成"
    >     if step >= max_steps: return "超过最大步数"
    >     if user_confirm: return "等待用户"
    >     return None
    > ```

67. **如何把多轮工具调用串起来（带状态）？**
    > ```python
    > state = {"messages": [], "intermediate": {}}
    > while not done:
    >     action = llm(state["messages"])
    >     result = execute(action)
    >     state["intermediate"][action["name"]] = result
    >     state["messages"].append({"role": "assistant", "content": action})
    >     state["messages"].append({"role": "tool", "content": result})
    > ```

68. **实现一个简单的 Multi-Agent 消息总线。**
    > ```python
    > from collections import deque
    > class MessageBus:
    >     def __init__(self):
    >         self.queue = deque()
    >     def publish(self, msg):
    >         self.queue.append(msg)
    >     def subscribe(self, agent):
    >         while self.queue:
    >             agent.handle(self.queue.popleft())
    > ```

69. **Agent 输出的 JSON 解析失败怎么办？**
    > ```python
    > import json, re
    > def safe_parse(text):
    >     try:
    >         return json.loads(text)
    >     except:
    >         m = re.search(r"```json\s*(.*?)\s*```", text, re.S)
    >         if m:
    >             return json.loads(m.group(1))
    >         return {"error": "parse_failed", "raw": text}
    > ```

70. **Agent 的 Prompt 里如何描述工具？写一个示例。**
    > ```
    > 可用工具：
    > 1. get_weather(city: str) - 查询城市天气
    >    - 参数：city，城市名，必填
    >    - 返回：{temp, condition, wind}
    > 使用规则：
    > - 只有需要外部信息时才调用工具
    > - 一次只调用一个工具
    > - 工具返回后用中文回答用户
    > ```

#### 开放题
71. **Agent 未来会取代什么岗位？你如何看待？**
    > 开放题，考察认知。参考角度：①取代的是"任务"不是"岗位"（重复性、规则性任务先被自动化）②Agent 增强人而非完全替代（人机协作）③会出现"Agent 管理者"新岗位（编排、治理、评估）④安全与责任是落地关键。

72. **如何让 Agent 更"可控"？**
    > ①结构化输出（格式约束）②受限工具集（按需开放）③人工审批节点 ④行为边界 Prompt 约束 ⑤运行时监控与干预 ⑥沙箱执行。

73. **Agent 的商业模式有哪些？**
    > ①按调用收费（API/按任务）②订阅制（SaaS Agent）③垂直行业解决方案（客服/财务/医疗 Agent）④Agent 市场（卖 Agent/技能）⑤企业私有化部署。

74. **你怎么理解"Agent 是 AI 的下一个风口"？**
    > 参考角度：①大模型是"大脑"，Agent 是"身体"（把能力变成行动）②Agent 让 AI 从"问答"走向"办事"，价值量级不同 ③基础设施（MCP、记忆、评估）在快速成熟 ④风险：可靠性、成本、安全仍是瓶颈。

75. **Agent 的幻觉在自主执行时危害更大，为什么？**
    > 因为对话场景下幻觉只是"答错"；Agent 场景下幻觉会导致"做错"——调错工具、误删数据、错误交易，危害直接作用到现实世界。所以 Agent 的幻觉治理要求更高。

76. **什么是 Agent 的"目的漂移"？怎么防？**
    > 目的漂移 = Agent 执行过程中偏离原始目标（如做调研的 Agent 越做越偏）。防：①任务目标常驻上下文 ②每步对照目标校验 ③完成标准明确 ④阶段性人工确认。

77. **Agent 系统如何做 A/B 测试？**
    > ①同一任务跑不同版本（模型/框架/Prompt）②对比成功率、成本、延迟 ③流量切分（随机分组）④离线评估先行，在线灰度确认。

78. **你如何给非技术人员解释什么是 Agent？**
    > "Agent 就像一个'有手有脑的实习生'：你告诉它目标（比如'订机票'），它会自己拆步骤、查航班、比价格、下单，中间卡住了还会问你。而以前的 AI 只会回答'怎么订机票'，不会真的帮你订。"

79. **Agent 遇到"用户需求模糊"怎么办？**
    > ①澄清提问（不猜，先问清楚）②假设+确认（给默认方案让用户确认）③范围兜底（说明已做/未做）④渐进式确认（关键决策点停下来确认）。

80. **如何看待"Agent 框架之争"（LangChain vs 自研）？**
    > 框架适合快速验证；自研适合规模化定制。关键看团队阶段和需求复杂度。核心逻辑（循环、状态、工具）理解了，换框架成本很低——面试官想看的是底层理解。

#### 安全与治理
81. **Agent 的 Prompt Injection 攻击路径有哪些？**
    > ①用户输入直接注入 ②检索到的文档内容注入 ③工具返回结果注入 ④网页内容注入（浏览器 Agent 读到的页面）⑤工具描述被污染。任何"外部输入进上下文"的地方都是攻击面。

82. **如何给 Agent 做数据脱敏？**
    > ①输入侧过滤（手机号/身份证正则脱敏）②输出侧检查（模型输出敏感信息拦截）③工具调用参数检查（不给工具传敏感字段）④日志脱敏。

83. **Agent 的审计日志要记什么？**
    > ①完整对话（含工具调用）②谁在何时发起了什么任务 ③工具执行的输入输出 ④敏感操作标记 ⑤系统决策（为什么走这条路）⑥成本消耗。

84. **Agent 操作真实系统（数据库/支付）如何保证安全？**
    > ①只读优先（默认只读，写操作需特殊授权）②沙箱隔离（测试环境验证）③人工审批（高风险操作）④操作限额（单次/单日额度）⑤回滚机制。

85. **什么是 Agent 的"沙箱"？为什么重要？**
    > 沙箱是隔离的执行环境（容器/虚拟机），Agent 的代码在沙箱里跑，无法影响真实系统。重要：代码 Agent 必须沙箱执行，防止误操作和恶意代码。

### 附：高频速记卡（20 题快问快答）

86. Agent 四要素？→ 大脑、工具、记忆、环境
87. ReAct 全称？→ Reasoning + Acting
88. CoT 是什么？→ 思维链，分步推理
89. MCP 是什么？→ 模型上下文协议，AI 的 USB-C
90. Function Calling 干嘛的？→ 模型输出结构化工具调用
91. Plan-and-Execute 分几步？→ 先规划后执行
92. Reflexion 核心？→ 失败反思写入记忆
93. ReWOO 特点？→ 推理与观察解耦，省 token
94. Multi-Agent 主流框架？→ AutoGen、CrewAI、LangGraph
95. LangGraph 状态？→ State，节点间传数据
96. Checkpoint 作用？→ 断点恢复、人工介入
97. Human-in-the-loop 是什么？→ 人机协作，关键点人工确认
98. Agent 记忆分几种？→ 短期（上下文）+ 长期（外部存储）
99. Embedding 在哪用？→ 记忆检索、RAG、工具选择
100. 工具设计原则？→ 单一职责、参数简单、描述清晰
101. 并行工具调用好处？→ 降延迟
102. 停止条件有哪些？→ 完成/超步/超时/用户确认
103. 成本控制手段？→ 缓存、模型路由、限制循环
104. Agent 评估核心指标？→ 成功率、成本、延迟
105. Prompt Injection 是什么？→ 恶意指令注入诱导 Agent

## 📊 数据表现

本仓库为 **Agent 面试知识体系**，与 [llm-interview-zh](https://github.com/zieang88888/llm-interview-zh)（AI 大模型面试手册）形成系列：

| 仓库 | 定位 | 适合人群 |
|---|---|---|
| llm-interview-zh | LLM 大模型面试 | 算法/LLM 工程师 |
| **agent-interview-zh** | **AI Agent 面试** | **Agent/应用工程师** |
| coding-interview-zh | 程序员通用面试 | 全栈工程师 |

## 🚀 快速开始

```bash
# 直接浏览
# 打开 README.md 即可查看全部题目和答案

# 或者克隆到本地
git clone https://github.com/zieang88888/agent-interview-zh.git
```

## 🤝 贡献

欢迎补充题目和答案：
- 有新的高频面试题？提 Issue
- 想贡献答案？提 PR
- 觉得有用？点个 ⭐ Star 就是最大的支持！

## 📄 License

MIT

---

**如果这份手册帮到了你，请点个 ⭐ Star，让更多人看到！** 🙏

**关注我 [@zieang88888](https://github.com/zieang88888)，持续输出中文开源干货！**