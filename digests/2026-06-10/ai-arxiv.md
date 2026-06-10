# ArXiv AI 研究日报 2026-06-10

> 数据来源: [ArXiv](https://arxiv.org/) (cs.AI, cs.CL, cs.LG) | 共 50 篇论文 | 生成时间: 2026-06-10 02:58 UTC

---

# 📰 ArXiv AI 研究日报 — 2026-06-10

## 今日速览

今日投稿呈现三大亮点：**多模态学习理论突破**——论文提出跨模态对齐与预测的“相图”，为选择训练范式提供系统指导；**智能体能力与安全的双重聚焦**——生物安全基准（ABC-Bench）、控制干预意识评估（CIAware-Bench）等基准涌现，同时测试时提示学习（EEVEE）与预算分配（TRACE）推动智能体实用化；**推理模型的副作用被发现**——CoT微调会系统性破坏混合注意力模型的长文回忆，提醒社区关注对齐保持。此外，全双工语音交互对齐（多面交互对齐）和一步扩散生成（Itô map）也带来方法层面的新视角。

---

## 重点论文

### 🧠 大语言模型（架构、训练、对齐、评估）

**1. When to Align, When to Predict: A Phase Diagram for Multimodal Learning**  
作者: Ilay Kamai et al. | [ArXiv](http://arxiv.org/abs/2606.11190v1)  
一句话说明：首次系统刻画跨模态对齐（CA）与跨模态预测（CP）的成功/失败条件，给出训练范例选择的相图，对多模态模型设计具有根本性指导意义。

**2. Multi-Faceted Interactivity Alignment in Full-Duplex Speech Models**  
作者: Atsumoto Ohashi et al. | [ArXiv](http://arxiv.org/abs/2606.11167v1)  
一句话说明：针对全双工语音对话模型提出多面交互对齐方法，超越token级最大似然，直接优化交互级行为，是语音交互范式的重要升级。

**3. Attention Amnesia in Hybrid LLMs: When CoT Fine-Tuning Breaks Long-Range Recall, and How to Fix It**  
作者: Xinyu Zhou et al. | [ArXiv](http://arxiv.org/abs/2606.11052v1)  
一句话说明：发现CoT SFT会显著降低混合线性注意力模型的长上下文召回能力（“注意力遗忘”），并给出修复策略，对推理模型部署有直接警示。

**4. Does Reasoning Preserve Alignment? On the Trustworthiness of Large Reasoning Models**  
作者: Prajakta Kini et al. | [ArXiv](http://arxiv.org/abs/2606.11046v1)  
一句话说明：研究将指令微调模型转化为推理模型后，对齐行为（如安全拒绝）是否退化，强调推理精度与对齐保护之间的张力。

---

### 🤖 智能体与推理（规划、工具使用、多智能体、思维链）

**5. EEVEE: Towards Test-time Prompt Learning in the Real World for Self-Improving Agents**  
作者: Weixian Xu et al. | [ArXiv](http://arxiv.org/abs/2606.11182v1)  
一句话说明：首个支持多数据集测试时提示学习的LLM智能体框架，使智能体在真实异构任务流中持续自我改进。

**6. ABC-Bench: An Agentic Bio-Capabilities Benchmark for Biosecurity**  
作者: Andrew Bo Liu et al. | [ArXiv](http://arxiv.org/abs/2606.11150v1)  
一句话说明：构建评估LLM智能体生物安全能力的基准，涵盖从文献合成到湿实验模拟的智能体任务，为双用途风险评估提供工具。

**7. TRACE: A Unified Rollout Budget Allocation Framework for Efficient Agentic Reinforcement Learning**  
作者: Heming Zou et al. | [ArXiv](http://arxiv.org/abs/2606.11119v1)  
一句话说明：针对可验证奖励的强化学习提出统一的rollout预算分配框架，通过动态分配解决奖励对比不足问题，提升智能体训练效率。

**8. T1-Bench: Benchmarking Multi-Scenario Agents in Real-World Domains**  
作者: Genta Indra Winata et al. | [ArXiv](http://arxiv.org/abs/2606.11070v1)  
一句话说明：覆盖多个真实领域的长程、工具调用密集型智能体基准，弥补现有基准在任务复杂性和领域多样性上的不足。

**9. CIAware-Bench: Benchmarking Control Intervention Awareness Across Frontier LLMs**  
作者: Joachim Schaeffer et al. | [ArXiv](http://arxiv.org/abs/2606.11063v1)  
一句话说明：评估LLM对控制协议干预的感知能力——当模型被监控并修改输出时，是否能推断出监视器的存在，对AI控制安全至关重要。

---

### 🔧 方法与框架（新技术、基准测试、效率优化）

**10. A Unifying Lens on Supervised Fine-Tuning Through Target Distribution Design**  
作者: Tong Xie et al. | [ArXiv](http://arxiv.org/abs/2606.11189v1)  
一句话说明：将SFT统一视为目标分布设计问题，指出严格拟合one-hot标签的次优性，为设计更灵活的微调目标提供理论框架。

**11. Itô maps for any-step SDEs**  
作者: Zhengkai Pan et al. | [ArXiv](http://arxiv.org/abs/2606.11156v1)  
一句话说明：将一步生成模型（流匹配）扩展到随机动力学，提出Itô map，实现精确的随机蒸馏，为扩散模型加速提供新思路。

**12. Provenance-Grounded Gating and Adaptive Recovery in Synthetic Post-Training Data Curation**  
作者: Soham Bhattacharjee et al. | [ArXiv](http://arxiv.org/abs/2606.11127v1)  
一句话说明：在合成数据过滤中引入溯源门控+自适应恢复机制，系统性地利用被拒样本，提升后训练数据质量。

**13. PhantomBench: Benchmarking the Non-existential Threat of Language Models**  
作者: Haeji Jung et al. | [ArXiv](http://arxiv.org/abs/2606.11105v1)  
一句话说明：专门针对LM幻觉现象设计的高风险评估基准，覆盖高风险领域，是当前最系统的幻觉基准之一。

**14. What Fits (Into Few Tokens) Doesn’t Overfit: Compression and Generalization in ML Research Agents**  
作者: Martin Andres Bertran et al. | [ArXiv](http://arxiv.org/abs/2606.11045v1)  
一句话说明：从压缩角度解释为何自适应复用基准不会过拟合，为LLM研究智能体的泛化提供理论支撑。

---

### 📊 应用（垂直领域、多模态、代码生成）

**15. Data Journalist Agent: Transforming Data into Verifiable Multimodal Stories**  
作者: Kevin Qinghong Lin et al. | [ArXiv](http://arxiv.org/abs/2606.11176v1)  
一句话说明：构建数据记者智能体，自动完成从数据探索、统计分析到可视化生成的多模态新闻故事，验证了LLM在专业创作流程中的潜力。

**16. Workflow-GYM: Towards Long-Horizon Evaluation of Computer-use Agentic tasks in Real-World Professional Fields**  
作者: Liya Zhu et al. | [ArXiv](http://arxiv.org/abs/2606.11042v1)  
一句话说明：提出面向真实专业领域的超长程计算机操作智能体评估环境，涵盖多步高价值工作流，填补现有基准的空白。

---

## 研究趋势信号

今日投稿揭示了三个值得关注的新兴方向：  
1. **推理模型的后效研究**：多篇论文（#45、#46）关注CoT微调对模型其他能力（长文记忆、对齐安全）的意外损害，预示“推理后效”将成为对齐社区热点。  
2. **智能体风险基准的实用化**：ABC-Bench（生物安全）和CIAware-Bench（控制干预意识）等基准不再停留于问答层面，而是模拟真实操作链，反映业界对智能体安全评估的迫切需求。  
3. **合成数据管道内的信息流控制**：溯源门控（#20）、预算分配（#24）等工作开始精细化管理合成数据的产生与筛选过程，从“生成-过滤”二元模式转向更复杂的反馈回路设计。

---

## 值得精读

1. **《When to Align, When to Predict: A Phase Diagram for Multimodal Learning》** — 本文为多模态学习提供了理论相图，指导何时使用跨模态对齐、何时使用跨模态预测，是众多实践选择背后的统一解释，对多模态领域所有研究者均有启发。

2. **《Attention Amnesia in Hybrid LLMs: When CoT Fine-Tuning Breaks Long-Range Recall》** — 揭示了一个被忽视的严重问题：CoT SFT会破坏混合线性注意力模型的长文记忆。文章同时提出修复方法，对于当前大规模部署推理模型的团队具有直接实操价值。

3. **《ABC-Bench: An Agentic Bio-Capabilities Benchmark for Biosecurity》** — 智能体生物安全是双用途治理的前沿议题。该基准系统评估了LLM智能体在生物研究各环节的能力，为政策制定者和安全研究者提供第一个可操作的评估工具。

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*