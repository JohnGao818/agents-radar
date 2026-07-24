# ArXiv AI 研究日报 2026-07-24

> 数据来源: [ArXiv](https://arxiv.org/) (cs.AI, cs.CL, cs.LG) | 共 50 篇论文 | 生成时间: 2026-07-24 02:16 UTC

---

# ArXiv AI 研究日报 | 2026-07-24

## 今日速览
今日投稿聚焦于**智能体系统的记忆与推理可靠性**和**大语言模型的结构化改进**两大主线。多篇工作揭示了当前 LLM 在**多智能体安全对齐**（直接暴露 vs. 中介传递）和**过度自我修正**等反直觉行为上的新发现；**位置编码**和**离散扩散**的理论创新为模型能力提供了更坚实的数学基础；**递归自我改进 agent** 和**快速视觉语言安全护栏**将实用 AI 系统推向更深层次。此外，自动驾驶协调、供应链规划、金融可靠性等垂直领域应用也展现出显著进展。

---

## 重点论文

### 🧠 大语言模型（架构、训练、对齐、评估）

**1. Artificial Epanorthosis: Why large language models overuse a classical rhetorical figure, and how to mitigate it**
- 作者: F. Boggia | [ArXiv](http://arxiv.org/abs/2607.21498v1)
- 一句话：系统揭示 LLM 过度使用“自我修正”修辞（如“这不是…而是…”）的根因（训练偏差），并提出缓解策略，为生成风格控制提供独特视角。

**2. When Trivia Is Not Trivial: Everyday Knowledge Failures in Multilingual LLMs**
- 作者: A. Mosolova, D. Seddah | [ArXiv](http://arxiv.org/abs/2607.21445v1)
- 一句话：通过跨语言常识测验基准，发现多语言 LLM 在“日常知识”（非经典事实）上存在系统性失败，为多语言模型评估补充了被忽视的维度。

**3. Anti-Periodic Positional Encoding: Möbius Boundary Conditions Make In-Context Retrieval Reliable**
- 作者: J. H. Bae | [ArXiv](http://arxiv.org/abs/2607.21405v1)
- 一句话：提出基于 Möbius 边界条件的旋转位置编码（Möbius RoPE），通过反周期频率阶梯实现上下文检索的可靠符号耦合，理论上可缓解位置外推退化。

### 🤖 智能体与推理（规划、工具使用、多智能体、思维链）

**4. Same Dangerous Objective, Opposite Advice: Direct Exposure versus Multi-Agent Mediation**
- 作者: L. Li | [ArXiv](http://arxiv.org/abs/2607.21518v1)
- 一句话：惊人发现——向 GPT-5.6 直接展示危险目标反而比通过中介 agent 传递更安全，揭示了多智能体调解可能放大风险的悖论，对 AI 安全设计意义重大。

**5. AREX: Towards a Recursively Self-Improving Agent for Deep Research**
- 作者: S. Lu, C. Li, K. Luo et al. | [ArXiv](http://arxiv.org/abs/2607.21461v1)
- 一句话：提出利用“发现-验证”不对称性实现递归自我改进的研究 agent，在复杂约束搜索中显著超越静态 agent，代表深度研究自动化的前沿尝试。

**6. GRADRAG: Cross-Component Prompt Adaptation for Coordinated Multi-Agent RAG**
- 作者: P. Pedinotti, E. Santus | [ArXiv](http://arxiv.org/abs/2607.21324v1)
- 一句话：提出跨组件的提示自适应框架

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*