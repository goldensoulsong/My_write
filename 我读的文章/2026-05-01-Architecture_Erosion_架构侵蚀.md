# Towards Automated Identification of Violation Symptoms of Architecture Erosion
**(迈向架构侵蚀违规症状的自动识别)**

**Source / 来源:** 代表性学术文献，关于架构漂移与 LLM 的交叉研究

---

## Abstract (摘要)

**[English Original]**
Architecture erosion has a detrimental effect on maintenance and evolution, as the implementation deviates from the intended architecture. To prevent this, development teams need to understand early enough the symptoms of erosion, and particularly violations of the intended architecture. One feasible way is through the automated identification of architecture violations from textual artifacts, and particularly code reviews. In this paper, we explore how machine learning and Large Language Models (LLMs) can be utilized to identify violation symptoms of architecture erosion. We evaluate classifiers including GPT-4o, Qwen, and traditional ML models to detect architectural deviations before they become irreversible technical debt.

**[中文翻译]**
架构侵蚀（Architecture erosion）对软件的维护和演进具有有害影响，因为实际的代码实现偏离了预期的架构。为了防止这种情况发生，开发团队需要尽早了解侵蚀的症状，特别是对预期架构的违反。一种可行的方法是通过文本工件（特别是代码审查）自动识别架构违规。在本文中，我们探索了如何利用机器学习和大型语言模型（LLM）来识别架构侵蚀的违规症状。我们评估了包括 GPT-4o、Qwen 和传统 ML 模型在内的分类器，以在架构偏差成为不可逆转的技术债务之前检测出它们。

---

## 1. Introduction and The Concept of Architecture Drift (引言与架构漂移概念)

**[English Original]**
Software architecture is the foundation of any complex system. However, during the continuous lifecycle of software development, a phenomenon known as "Architecture Drift" or "Architecture Erosion" inevitably occurs. This happens when the actual codebase gradually diverges from the planned Architectural Decision Records (ADRs). With the introduction of LLM-based coding agents, this erosion is significantly accelerated. While human developers might intentionally break architectural rules due to deadline pressures, AI agents often break them due to a lack of global context and the pursuit of localized optimizations.

**[中文翻译]**
软件架构是任何复杂系统的基础。然而，在软件开发的持续生命周期中，不可避免地会发生一种被称为“架构漂移（Architecture Drift）”或“架构侵蚀（Architecture Erosion）”的现象。当实际的代码库逐渐偏离计划中的架构决策记录（ADR）时，就会发生这种情况。随着基于 LLM 的编程智能体的引入，这种侵蚀被显著加速了。虽然人类开发者可能会因为截止日期的压力而故意破坏架构规则，但 AI 智能体通常是因为缺乏全局上下文以及追求“局部优化”而破坏这些规则。

**[English Original]**
When an agent is tasked with fixing a bug or adding a feature without strict systemic constraints, it acts as an unbounded optimizer. It optimizes for passing the immediate unit test, often bypassing layering protocols or duplicating code. Over multiple iterations, this automated technical debt transforms the system into an unmaintainable state. 

**[中文翻译]**
当智能体在没有严格的系统性约束的情况下被要求修复 Bug 或添加功能时，它就像一个无界优化器。它为了通过当前的单元测试而进行优化，经常会绕过分层协议或复制冗余代码。经过多次迭代后，这种“自动化技术债务”会将系统变成一个无法维护的状态。

---

## 2. Methodology for Detecting Erosion (检测侵蚀的方法论)

**[English Original]**
To combat AI-induced architecture erosion, we must move beyond checking for syntactic correctness. We propose an automated verification layer that analyzes textual artifacts and code diffs to detect architectural violations. Our methodology involves extracting code modifications and developer discussions to identify symptoms of drift, such as unexpected direct database access from presentation layers, or the violation of interface segregation principles.

**[中文翻译]**
为了对抗 AI 引起的架构侵蚀，我们必须超越仅仅检查“语法正确性”。我们提出了一个自动化的“验证层”，该层通过分析文本工件和代码差异（diffs）来检测架构违规。我们的方法包括提取代码修改和开发者讨论，以识别漂移的症状，例如从表示层（UI层）意外地直接访问数据库，或者违反接口隔离原则。

**[English Original]**
We evaluated several models, comparing traditional ML approaches against state-of-the-art LLMs. The goal is to establish a "Guardrail" system—an automated referee that sits on the loop (Human-on-the-loop paradigm) to flag when the code generation is leaving the predefined feasible architectural region.

**[中文翻译]**
我们评估了几个模型，将传统的机器学习方法与最先进的 LLM 进行了比较。我们的目标是建立一个“护栏（Guardrail）”系统——一个位于环上（Human-on-the-loop 范式）的自动裁判，当代码生成开始离开预定义的架构可行域时，它能发出警告。

---

## 3. Discussion and The Path Forward (讨论与未来方向)

**[English Original]**
Our evaluation highlights that while LLMs are excellent at writing code, they are also highly proficient at masking architecture erosion. The code they produce is often elegant and functional, making it difficult for reviewers to immediately spot the structural damage. Therefore, defining the constraint set and the objective function of the agent is more critical than the coding capability of the model itself.

**[中文翻译]**
我们的评估突显出，虽然 LLM 非常擅长编写代码，但它们也非常擅长掩盖架构侵蚀。它们生成的代码通常很优雅且功能齐全，这使得审查人员很难立即发现其中的结构性破坏。因此，为智能体定义约束集合和目标函数，比模型本身的代码编写能力更为关键。

**[English Original]**
In the era of Agentic Software Engineering, the developer's role is shifting. Instead of manually writing syntax, the human engineer must focus on context engineering and constraint design, ensuring that the autonomous agent remains tightly bounded within the architecture's acceptable parameters.

**[中文翻译]**
在智能体软件工程（Agentic Software Engineering）时代，开发者的角色正在发生转变。人类工程师不再是手动编写语法，而是必须专注于上下文工程（Context Engineering）和约束设计，以确保自主智能体始终被严格限制在架构可接受的参数边界之内。
