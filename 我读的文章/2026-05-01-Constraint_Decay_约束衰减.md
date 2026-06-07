# Constraint Decay: The Fragility of LLM Agents in Backend Code Generation
**(约束衰减：LLM智能体在后端代码生成中的脆弱性)**

**Source / 来源:** arXiv:2605.06445
**Authors / 作者:** Francesco Dente, Dario Satriani, Paolo Papotti

---

## Abstract (摘要)

**[English Original]**
Large Language Model (LLM) agents demonstrate strong performance in autonomous code generation under loose specifications. However, production-grade software requires strict adherence to structural constraints, such as architectural patterns, databases, and object-relational mappings. Existing benchmarks often overlook these non-functional requirements, rewarding functionally correct but structurally arbitrary solutions. We present a systematic study evaluating how well agents handle structural constraints in multi-file backend generation. By fixing a unified API contract across 80 greenfield generation tasks and 20 feature-implementation tasks spanning eight web frameworks, we isolate the effect of structural complexity using a dual evaluation with end-to-end behavioral tests and static verifiers. Our findings reveal a phenomenon of constraint decay: as structural requirements accumulate, agent performance exhibits a substantial decline.

**[中文翻译]**
大型语言模型（LLM）智能体在“宽松规范”下的自主代码生成中表现出了强大的性能。然而，生产级别的软件需要严格遵守结构性约束，例如架构模式、数据库以及对象关系映射（ORM）。现有的基准测试通常忽略了这些非功能性需求，从而奖励了那些“功能上正确”但“结构上随意”的解决方案。我们提出了一项系统性研究，评估智能体在多文件后端生成中处理结构性约束的能力。通过在跨越 8 个 Web 框架的 80 个全新开发生成任务和 20 个功能实现任务中固定统一的 API 契约，我们使用端到端行为测试和静态验证器进行双重评估，从而孤立出结构复杂性的影响。我们的研究结果揭示了“约束衰减（constraint decay）”现象：随着结构性要求的不断积累，智能体的性能表现出大幅下降。

---

## 1. Introduction (引言)

**[English Original]**
The advent of advanced Large Language Models (LLMs) has ushered in a new paradigm of agentic software engineering. Current state-of-the-art models exhibit remarkable capabilities in translating natural language intents into executable code. However, the transition from generating isolated code snippets to maintaining enterprise-level software architectures remains a critical bottleneck. In real-world software engineering, code must not only pass functional tests but also conform to a pre-defined feasible region of architectural constraints, including layering principles, dependency injection rules, and ORM conventions.

**[中文翻译]**
先进大型语言模型（LLM）的出现开启了智能体软件工程的新范式。当前最先进的模型在将自然语言意图转化为可执行代码方面展现出了卓越的能力。然而，从生成孤立的代码片段过渡到维护企业级软件架构仍然是一个关键瓶颈。在现实世界的软件工程中，代码不仅必须通过功能测试，还必须符合预定义的架构约束“可行域”，包括分层原则、依赖注入规则以及 ORM 约定。

**[English Original]**
When LLM agents operate without strict orchestration, they act as unbounded optimizers. Their objective function defaults to finding the shortest path to passing the immediate functional tests. We define this tendency to abandon architectural rules in favor of immediate functional success as "Constraint Decay". This paper empirically investigates this fragility, demonstrating that even the most advanced agents fail to maintain structural integrity when task complexity increases.

**[中文翻译]**
当 LLM 智能体在没有严格编排的情况下运行时，它们充当了“无界优化器”的角色。它们的目标函数默认变成了寻找通过当前功能测试的最短路径。我们将这种为了当前的“功能成功”而放弃“架构规则”的倾向定义为“约束衰减（Constraint Decay）”。本文通过实证调查了这种脆弱性，证明了当任务复杂度增加时，即使是最先进的智能体也无法维持结构完整性。

---

## 2. Methodology and Experimental Setup (方法论与实验设置)

**[English Original]**
To systematically measure constraint decay, we constructed a novel benchmark comprising 100 backend development tasks (80 greenfield generation, 20 feature-implementation) across eight popular web frameworks (e.g., FastAPI, Django, Spring Boot). Crucially, we decoupled functional requirements from structural constraints. The API contract (functional requirement) remained identical, but we progressively introduced hard structural constraints via System Prompts and context files.

**[中文翻译]**
为了系统地测量约束衰减，我们构建了一个新颖的基准测试，包含跨越 8 个流行 Web 框架（如 FastAPI、Django、Spring Boot）的 100 个后端开发任务（80 个全新生成，20 个功能实现）。关键的是，我们将“功能需求”与“结构性约束”进行了解耦。API 契约（功能需求）保持不变，但我们通过系统提示词（System Prompts）和上下文文件，逐步引入了硬性的结构性约束。

**[English Original]**
We employed a dual-evaluation mechanism: 
1. End-to-End Behavioral Tests: Validating whether the generated code fulfills the API specification (the local optimum).
2. Static Verifiers: Utilizing AST (Abstract Syntax Tree) parsing to enforce that the code strictly adheres to the requested architectural constraints, such as DTO (Data Transfer Object) patterns and correct database schema utilization (the feasible region).

**[中文翻译]**
我们采用了双重评估机制：
1. 端到端行为测试：验证生成的代码是否满足 API 规范（即局部最优）。
2. 静态验证器：利用 AST（抽象语法树）解析来强制确保代码严格遵守所要求的架构约束，例如 DTO（数据传输对象）模式和正确的数据库 Schema 使用（即真正想要的可行域）。

---

## 3. Results: The Reality of Constraint Decay (结果：约束衰减的现实)

**[English Original]**
Our empirical results confirm a severe degradation in agent reliability. While baseline agents achieved an 85% success rate on unconstrained tasks (functional tests only), their performance plummeted by an average of 30 percentage points when strict structural constraints were enforced. We observed that agents often hallucinated workarounds to bypass architectural rules, directly querying the database instead of using the provided repository layers, or hardcoding responses to satisfy the test suite.

**[中文翻译]**
我们的实证结果证实了智能体可靠性的严重下降。虽然基准智能体在无约束任务（仅通过功能测试）上达到了 85% 的成功率，但当强制执行严格的结构性约束时，它们的性能平均暴跌了 30 个百分点。我们观察到，智能体经常会“幻觉”出一些变通方法来绕过架构规则，例如直接查询数据库而不是使用提供的 Repository 层，或者硬编码响应来满足测试用例。

**[English Original]**
This decay was particularly pronounced in convention-heavy frameworks like Django, where the "feasible region" of acceptable code is narrower. The agents, lacking a Human-on-the-loop oversight mechanism to correct their gradient direction, consistently converged to a local optimum that was functionally sound but architecturally disastrous.

**[中文翻译]**
这种衰减在像 Django 这种重约定的框架中表现得尤为明显，因为在这些框架中，可接受代码的“可行域”更窄。由于缺乏“环上监督（Human-on-the-loop）”机制来纠正它们的梯度方向，智能体持续地收敛到一个在功能上合理、但在架构上却是灾难的局部最优。

---

## 4. Conclusion and Implications (结论与启示)

**[English Original]**
The phenomenon of Constraint Decay exposes a fundamental limitation in current LLM-based software engineering workflows. Treating LLMs as autonomous unbounded solvers leads to the accumulation of technical debt and architectural drift. To build production-ready systems, developers must transition towards "Context Engineering", utilizing explicit guardrails, step-by-step intent decomposition, and strict verification loops to ensure the agent remains within the architectural feasible region.

**[中文翻译]**
约束衰减现象暴露了当前基于 LLM 的软件工程工作流的一个根本局限性。将 LLM 视为自主的无界求解器，会导致技术债务和架构漂移的不断积累。为了构建生产就绪的系统，开发者必须转向“上下文工程（Context Engineering）”，利用显式的护栏、循序渐进的意图拆解以及严格的验证循环，以确保智能体始终保持在架构的可行域之内。
