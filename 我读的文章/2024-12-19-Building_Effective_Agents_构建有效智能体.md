# Building Effective Agents (构建有效智能体)

**Source / 来源:** [Anthropic Engineering Blog](https://www.anthropic.com/engineering/building-effective-agents)
**Authors / 作者:** Erik Schluntz, Barry Zhang
**Date / 发布日期:** 2024-12-19

---

## 摘要与核心观点 (Abstract & Key Takeaways)

**[English Original]**
Over the past year, we've worked with dozens of teams building large language model (LLM) agents across industries. Consistently, the most successful implementations weren't using complex frameworks or specialized libraries. Instead, they were building with simple, composable patterns. "Agent" can be defined in several ways. We categorize all these variations as agentic systems, but draw an important architectural distinction between workflows and agents: Workflows are systems where LLMs and tools are orchestrated through predefined code paths. Agents are systems where LLMs dynamically direct their own processes and tool usage, maintaining control over how they accomplish tasks.

**[中文翻译]**
在过去的一年里，我们与跨行业的几十个团队合作构建了大型语言模型（LLM）智能体。一致的是，最成功的实现并没有使用复杂的框架或专门的库。相反，它们使用的是简单、可组合的模式来构建的。“智能体（Agent）”有几种定义方式。我们将所有这些变体归类为智能体系统（agentic systems），但在“工作流（workflows）”和“智能体（agents）”之间划分了一个重要的架构界限：工作流是通过预定义代码路径编排 LLM 和工具的系统；而智能体则是 LLM 动态指导自己的流程和工具使用的系统，保持对如何完成任务的控制权。

---

## 核心设计模式 (Core Design Patterns)

**[English Original]**
We explore the common patterns for agentic systems we’ve seen in production. We'll start with our foundational building block—the augmented LLM—and progressively increase complexity, from simple compositional workflows to autonomous agents.
1. **The augmented LLM**: The basic building block is an LLM enhanced with augmentations such as retrieval, tools, and memory.
2. **Prompt chaining**: Decomposes a task into a sequence of steps, where each LLM call processes the output of the previous one.
3. **Routing**: Classifies an input and directs it to a specialized followup task.
4. **Parallelization**: LLMs can sometimes work simultaneously on a task and have their outputs aggregated programmatically (Sectioning and Voting).
5. **Orchestrator-workers**: A central LLM dynamically breaks down tasks, delegates them to worker LLMs, and synthesizes their results.
6. **Evaluator-optimizer**: One LLM call generates a response while another provides evaluation and feedback in a loop.
7. **Agents**: LLMs dynamically direct their own processes, plan and operate independently in a loop, using tools based on environmental feedback.

**[中文翻译]**
我们探讨了在生产环境中见到的智能体系统的常见模式。我们将从基础构建块——增强型 LLM 开始，并逐渐增加复杂性，从简单的组合工作流到完全自主的智能体。
1. **增强型 LLM (The augmented LLM)**：基本构建块是配备了检索、工具和记忆等增强功能的 LLM。
2. **提示词链 (Prompt chaining)**：将任务分解为一系列步骤，其中每个 LLM 调用都处理上一个调用的输出。
3. **路由 (Routing)**：对输入进行分类，并将其定向到专门的后续任务。
4. **并行化 (Parallelization)**：LLM 有时可以同时处理一个任务，并通过编程方式汇总它们的输出（包括分块和投票）。
5. **编排者-工作者 (Orchestrator-workers)**：一个中央 LLM 动态地分解任务，将其委托给工作者 LLM，并合成它们的结果。
6. **评估者-优化者 (Evaluator-optimizer)**：在一个循环中，一个 LLM 调用生成响应，而另一个提供评估和反馈。
7. **智能体 (Agents)**：LLM 动态地指导它们自己的流程，在一个循环中独立地规划和操作，根据环境反馈使用工具。

---

## 何时使用智能体 (When to use agents)

**[English Original]**
When building applications with LLMs, we recommend finding the simplest solution possible, and only increasing complexity when needed. This might mean not building agentic systems at all. Agentic systems often trade latency and cost for better task performance. Workflows offer predictability and consistency for well-defined tasks, whereas agents are the better option when flexibility and model-driven decision-making are needed at scale. Agents can be used for open-ended problems where it’s difficult or impossible to predict the required number of steps, and where you can’t hardcode a fixed path.

**[中文翻译]**
在构建 LLM 应用程序时，我们建议寻找尽可能简单的解决方案，只有在需要时才增加复杂性。这可能意味着根本不需要构建智能体系统。智能体系统通常以延迟和成本换取更好的任务表现。对于明确定义的任务，工作流提供了可预测性和一致性；而当需要大规模的灵活性和模型驱动的决策时，智能体是更好的选择。智能体可用于那些很难或不可能预测所需步骤数量，且无法硬编码固定路径的开放式问题。

---

## 结论与原则 (Conclusion and Principles)

**[English Original]**
Success in the LLM space isn't about building the most sophisticated system. It's about building the right system for your needs. Start with simple prompts, optimize them with comprehensive evaluation, and add multi-step agentic systems only when simpler solutions fall short. When implementing agents, we try to follow three core principles:
1. Maintain simplicity in your agent's design.
2. Prioritize transparency by explicitly showing the agent’s planning steps.
3. Carefully craft your agent-computer interface (ACI) through thorough tool documentation and testing.

**[中文翻译]**
在 LLM 领域的成功不在于构建最复杂的系统，而在于为你自己的需求构建正确的系统。从简单的提示词开始，通过全面的评估来优化它们，只有当更简单的解决方案达不到要求时，才添加多步的智能体系统。在实现智能体时，我们努力遵循三个核心原则：
1. 在智能体的设计中保持**简单性**。
2. 通过显式地展示智能体的规划步骤来优先考虑**透明度**。
3. 通过彻底的工具文档和测试，精心打造你的**智能体-计算机接口（ACI）**。
