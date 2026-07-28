# ArXiv AI 研究日报 2026-07-28

> 数据来源: [ArXiv](https://arxiv.org/) (cs.AI, cs.CL, cs.LG) | 共 44 篇论文 | 生成时间: 2026-07-28 02:07 UTC

---

好的，作为AI研究分析师，我已为您整理好今日的《ArXiv AI 研究日报》。

---

### 📅 ArXiv AI 研究日报 | 2026年7月28日

### 1. 今日速览

今日论文聚焦于**AI智能体的**安全、授权与评估，成为最突出的主题。多篇论文深入探讨了智能体在复杂环境中面临的授权漂移（Evolved Authority）、运行时保证（Runtime Assurance）及安全幻觉问题。同时，**LLM的推理能力**研究从多模态、符号逻辑和新兴基准（如中文歇后语）等多个维度被重新审视。此外，**AI治理与战略**也引起了关注，学界开始尝试分离技术能力与操作权限，并为企业选择AI项目提供决策框架。

### 2. 重点论文

#### 🧠 大语言模型（架构、训练、对齐、评估）

1.  **The Illusion of Secure LLM Code: Closing the Security Gap via Iterative Reprompting**
    - **作者:** I. Singh 等
    - **链接:** http://arxiv.org/abs/2607.23710v1
    - **一句话说明:** 揭示了当前AI编码助手生成的身份验证代码存在严重安全缺陷，并提出了“迭代重新提示”方法，显著缩小了人工编写与AI生成代码之间的安全差距。

2.  **Do LLMs Know Their Vulnerable Scenarios?**
    - **作者:** Z. Peng 等
    - **链接:** http://arxiv.org/abs/2607.23496v1
    - **一句话说明:** 从元认知角度切入，研究了LLM是否知晓自身在哪些特定场景下容易失效，为理解LLM安全漏洞的底层原因提供了新视角。

3.  **Auditing Alignment Controllability in LLMs via Political Axes**
    - **作者:** B. Bućan 等
    - **链接:** http://arxiv.org/abs/2607.23519v1
    - **一句话说明:** 提出不应只关注LLM的“静态”政治立场，而应审计其“可控性”，即模型回答能被外部提示在政治光谱上引导多远，对AI对齐研究具有重要方法论意义。

4.  **Reasoning or Memorization: Can LLMs Understand and Generate Chinese Xiehouyu Riddles?**
    - **作者:** H. Hu 等
    - **链接:** http://arxiv.org/abs/2607.23440v1
    - **一句话说明:** 采用语言学专家新造的歇后语来规避数据污染，测试了LLM在汉语语言游戏中的推理与生成能力，为评估模型真正的理解和创造力设立了高难度标杆。

#### 🤖 智能体与推理（规划、工具使用、多智能体、思维链）

5.  **E-Bench: Benchmarking Multi-Step Tool-Use Agents in Real-World Product Scenarios**
    - **作者:** W. Zheng 等
    - **链接:** http://arxiv.org/abs/2607.23722v1
    - **一句话说明:** 提出了一个针对现实产品场景中多步工具使用智能体的新基准，填补了现有评估在状态循环和复杂工具组合上的空白，对智能体开发至关重要。

6.  **Are You Still the Agent I Authorized? Earned Authority under a Fixed Ceiling for Evolving Agents**
    - **作者:** Z. Zhang 等
    - **链接:** http://arxiv.org/abs/2607.23586v1
    - **一句话说明:** 指出了一个关键的安全问题：长期演化的AI智能体在部署后积累新技能，可能超越最初授权的权限边界，并提出了“固定上限下的赚取式授权”治理概念。

7.  **Offline-Online Curriculum RL for Multimodal Reasoning**
    - **作者:** W. Deng 等
    - **链接:** http://arxiv.org/abs/2607.23700v1
    - **一句话说明:** 提出了一种离线和在线结合的课程强化学习方法，以解决多模态大模型在推理中“答案正确、过程错误”的不可靠问题，旨在提升模型的可解释性和鲁棒性。

8.  **Plans Work in Mysterious Ways: Evaluating a Plan Mode for Spreadsheet Agents**
    - **作者:** A. Kumar 等
    - **链接:** http://arxiv.org/abs/2607.23670v1
    - **一句话说明:** 首次系统评估了“计划模式”在表格处理智能体中的有效性，发现计划能够提供透明度，但其生成质量与最终执行效率之间并非简单的正相关。

#### 🔧 方法与框架（新技术、基准测试、效率优化）

9.  **SpecAHD: Localize to Specialize for Automated Heuristic Design in Large-Scale Routing Problems**
    - **作者:** K. Lai 等
    - **链接:** http://arxiv.org/abs/2607.23676v1
    - **一句话说明:** 针对大规模路径规划问题，提出了一种利用LLM在“局部”进行启发式算法自动设计的方法，通过集中优化修复区域，比全局优化更高效。

10. **TLA$^{+}$-Bench: An Execution-Grounded Benchmark and Dataset for Natural-Language to TLA+ Specification Generation**
    - **作者:** A. Bisharat 等
    - **链接:** http://arxiv.org/abs/2607.23425v1
    - **一句话说明:** 发布了首个基于“执行正确性”而非语法或文本相似度的TLA+规范生成基准，为评估LLM在形式化验证领域的应用提供了更可靠的度量标准。

11. **Offline-to-Online Creative Optimization with Generative Models and Adaptive Testing**
    - **作者:** K. Lee 等
    - **链接:** http://arxiv.org/abs/2607.23696v1
    - **一句话说明:** 提出一个结合离线数据和在线自适应测试的广告创意优化框架，解决了生成式模型产出众多但真实评估昂贵的核心难题。

#### 📊 应用（垂直领域、多模态、代码生成）

12. **Verification-Notebook Learning for Source-Aware Multimodal Misinformation Detection**
    - **作者:** J. Tan
    - **链接:** http://arxiv.org/abs/2607.23581v1
    - **一句话说明:** 提出“验证笔记本”学习框架，让LVLM在检测多模态谣言时，能自适应地为不同实例选择最合适的推理路径，效果优于固定流程的方法。

13. **Neonatal Hypoxic-ischaemic Encephalopathy Classification from the EEG and HRV Signals Using a Conformer based Masked Autoencoder**
    - **作者:** S. Yu 等
    - **链接:** http://arxiv.org/abs/2607.23554v1
    - **一句话说明:** 将Conformer架构与掩码自编码器结合，用于新生儿缺氧缺血性脑病的早期诊断，是自监督学习在关键医疗信号处理领域的成功应用。

14. **Do Small Models Use the Law You Give Them? Context-Injected Fine-Tuning for Legal QA in Bangladesh**
    - **作者:** M. Mahadi 等
    - **链接:** http://arxiv.org/abs/2607.23446v1
    - **一句话说明:** 实验证明，通过“上下文注入”微调，即使是小模型也能在特定法律问答任务中，学会正确使用提供的法律条文进行推理，展示了低资源场景下的一种实用路径。

### 3. 研究趋势信号

- **“授权”成为智能体研究新核心：** 随着智能体从实验室走向生产环境，其**权限的初始赋予、动态演化与安全审计**（如论文 `Are You Still the Agent I Authorized?`）正在成为一个严肃的研究分支，超越了传统的提示注入和越狱攻击。
- **动态和人格化评估的兴起：** 对LLM的评估正从单一静态基准转向**动态、可引导**的评估，如审计其政治“可控性”（`Auditing Alignment Controllability`）或通过在真实环境中“赢得”权限来评估其能力。
- **小模型的“上下文学习”潜能：** 趋势表明，在特定垂直领域，通过精巧的微调策略（如“上下文注入”，`Context-Injected Fine-Tuning`），**小模型有能力高效利用提供的上下文信息**，这为在受限环境中部署实用AI提供了经济可行的方案。

### 4. 值得精读

1.  **《Are You Still the Agent I Authorized? Earned Authority under a Fixed Ceiling for Evolving Agents》**
    - **推荐理由:** 这篇文章提出了一个极具前瞻性的AI治理问题。它直击了长期运行智能体的核心安全挑战：智能体如何在不超出初始授权的情况下，通过学习和自我更新来“赚取”新的权限？这个概念可能对未来智能体的架构设计和法律框架产生深远影响。

2.  **《Auditing Alignment Controllability in LLMs via Political Axes》**
    - **推荐理由:** 它颠覆了以往对LLM政治偏见的评价方式。从关注“模型是什么立场”转向关注“模型能被引导到什么立场”，更贴近实际应用场景。这种评估“可控性”的思路，为理解LLM对齐的鲁棒性与脆弱性提供了强大的分析工具。

3.  **《TLA$^{+}$-Bench: An Execution-Grounded Benchmark for Specification Generation》**
    - **推荐理由:** 该工作为利用LLM辅助形式化验证这一前沿方向提供了坚实的实验基础。通过将评估标准从“写得好不好”提升到“写得对不对（能通过执行验证）”的高度，有望推动AI在关键任务领域（如航天、云计算）的应用。

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*