# ArXiv AI 研究日报 2026-06-26

> 数据来源: [ArXiv](https://arxiv.org/) (cs.AI, cs.CL, cs.LG) | 共 50 篇论文 | 生成时间: 2026-06-26 02:56 UTC

---

好的，以下是基于您提供的 2026 年 6 月 26 日 ArXiv 论文列表生成的 AI 研究日报。

---

# ArXiv AI 研究日报 (2026-06-26)

### 今日速览

今日论文呈现三大热点：**大语言模型的自我提升与对齐** 出现新范式，如无需真值答案的强化学习框架 RiVER，以及对安全性、偏见、可解释性的深入探讨；**多模型协作的局限性** 被首次严格量化，揭示了模型组合准确率的硬性天花板；**世界模型的可信度** 成为焦点，研究不仅关注幻觉的预测与预防，还探索了在机器人、地球观测等领域的实际应用。此外，**稀疏自编码器**在可解释性领域的应用进一步深化，并延伸至时间序列预测与线性模型效能的再评估。

### 重点论文

#### 🧠 大语言模型（架构、训练、对齐、评估）

1.  **Reinforcement Learning without Ground-Truth Solutions can Improve LLMs**
    *   Yingyu Lin et al.
    *   **一句话说明：** 提出 **RiVER** 框架，通过利用模型自身的输出排名来替代昂贵的真值标签，开创了无需标准答案即可进行RLVR训练的新路径，极大拓展了强化学习在LLM中的应用范围。
    *   http://arxiv.org/abs/2606.27369v1

2.  **When are likely answers right? On Sequence Probability and Correctness in LLMs**
    *   Johannes Zenn, Jonas Geiping
    *   **一句话说明：** 系统性地探究了LLM中“高概率序列是否等价于正确答案”这一核心问题，揭示了基于概率的采样方法的理论基础与局限性，对解码策略研究至关重要。
    *   http://arxiv.org/abs/2606.27359v1

3.  **When Does Combining Language Models Help? A Co-Failure Ceiling on Routing, Voting, and Mixture-of-Agents Across 67 Frontier Models**
    *   Josef Chen
    *   **一句话说明：** 通过对67个前沿模型进行大规模实验，首次严格证明了多模型组合系统的准确率存在一个理论上限，即**共同失败率**，挑战了“模型越多越好”的普遍认知。
    *   http://arxiv.org/abs/2606.27288v1

4.  **Paved with True Intents: Intent-Aware Training Improves LLM Safety Classification Across Training Regimes**
    *   Jeremias Ferrao et al.
    *   **一句话说明：** 发布了包含意图标注的困难安全样本集 **AIMS**，并证明用“用户意图”作为显式信号训练安全分类器，能显著提升其在各种训练范式下的安全检测性能。
    *   http://arxiv.org/abs/2606.27210v1

#### 🤖 智能体与推理（规划、工具使用、多智能体、思维链）

5.  **Empowering GUI Agents via Autonomous Experience Exploration and Hindsight Experience Utilization for Task Planning**
    *   Tianyi Men et al.
    *   **一句话说明：** 提出让GUI智能体在环境中自主探索并利用“事后经验”进行自我提升的方法，有效解决了小模型在复杂任务规划中能力不足的问题，推动了轻量级智能体的发展。
    *   http://arxiv.org/abs/2606.27330v1

6.  **E-TTS: A New Embodied Test-Time Scaling Framework for Robotic Manipulation**
    *   Wen Ye et al.
    *   **一句话说明：** 首次系统性地研究了具身智能中的**测试时扩展**机制，将模型的推理计算与对历史信息的利用相结合，证明了推理能力的提升可以有效转化为机器人操控性能的提升。
    *   http://arxiv.org/abs/2606.27268v1

7.  **Language-Based Digital Twins for Elderly Cognitive Assistance**
    *   Mohammad Mehdi Hosseini et al.
    *   **一句话说明：** 利用语言和对话模式作为无创生物标志物，构建用于早期轻度认知障碍（MCI）检测的数字孪生系统，展示了AI在个性化认知健康管理中的巨大潜力。
    *   http://arxiv.org/abs/2606.27334v1

#### 🔧 方法与框架（新技术、基准测试、效率优化）

8.  **Hallucination in World Models is Predictable and Preventable**
    *   Nicklas Hansen, Xiaolong Wang
    *   **一句话说明：** 揭示了生成式世界模型中的幻觉得以**可预测**和**可预防**的关键在于其对低覆盖度状态-动作空间中不可控动态的编码，为提升世界模型在机器人等领域的可靠性提供了新思路。
    *   http://arxiv.org/abs/2606.27326v1

9.  **Beyond the Hard Budget: Sparsity Regularizers for More Interpretable Top-k Sparse Autoencoders**
    *   Nathanaël Jacquier et al.
    *   **一句话说明：** 针对Top-k稀疏自编码器，提出用软性稀疏正则化替代硬性预算约束，不仅能达到更高可解释性，还避免了人为设定稀疏度参数，为模型特征解耦提供了更优雅的方案。
    *   http://arxiv.org/abs/2606.27321v1

10. **How Good Can Linear Models Be for Time-Series Forecasting?**
    *   Lang Huang et al.
    *   **一句话说明：** 通过精心的特征工程和超参数调优，证明了精心设计的线性模型在多数时间序列预测任务上的表现可以媲美甚至超越复杂的Transformer和基础模型，对该领域的架构选择提出了有力挑战。
    *   http://arxiv.org/abs/2606.27282v1

11. **CARVE: Content-Aware Recurrent with Value Efficiency for Chunk-Parallel Linear Attention**
    *   Sayak Dutta
    *   **一句话说明：** 指出了当前主流Delta-rule线性注意力架构中存在的“内存盲门控”缺陷，并提出了内容感知的改进方案CARVE，在保持线性复杂度的同时提升了模型对长序列信息的处理能力。
    *   http://arxiv.org/abs/2606.27229v1

#### 📊 应用（垂直领域、多模态、代码生成）

12. **Prompt Injection in Automated Résumé Screening with Large Language Models: Single and Multi-Injection Settings**
    *   Preet Baxi et al.
    *   **一句话说明：** 系统性地研究了针对LLM自动简历筛选系统的**提示注入攻击**，证明求职者通过在简历中植入隐蔽的自夸文本即可操纵排名，对AI招聘的公平性敲响了警钟。
    *   http://arxiv.org/abs/2606.27287v1

13. **From Celebrities to Anyone: Characterizing AI Nudification Content, Technology, and Community Dynamics on 4chan**
    *   Chi Cui et al.
    *   **一句话说明：** 首个对匿名社区（4chan）中AI“脱衣”内容、技术和社区动态的大规模研究，揭示其目标正从名人扩展到普通人，为内容审核与AI伦理治理提供了关键证据。
    *   http://arxiv.org/abs/2606.27234v1

14. **BetXplain: An Explanation-Annotated Dataset for Detecting Manipulative Betting Advertisements on Social Media**
    *   MSVPJ Sathvik et al.
    *   **一句话说明：** 发布了第一个带有可解释标注的博彩广告检测数据集 **BetXplain**，旨在识别社交媒体上具有操纵性的博彩内容，支持更透明的自动化内容审核。
    *   http://arxiv.org/abs/2606.27274v1

15. **EO-WM: A Physically Informed World Model for Probabilistic Earth Observation Forecasting**
    *   Junwei Luo et al.
    *   **一句话说明：** 将地球观测（EO）预测问题建模为部分可观测、由天气驱动的**世界模型**问题，引入物理信息进行概率预测，为环境监测和灾害预警提供了更强大的工具。
    *   http://arxiv.org/abs/2606.27277v1

16. **HarmVideoBench: Benchmarking Harmful Video Understanding in Large Multimodal Models**
    *   Jiajun Wu et al.
    *   **一句话说明：** 推出 **HarmVideoBench** 基准，旨在全面评估多模态大模型对视频中多层次有害内容的理解能力，弥补了现有有害视频基准在多维度和多模态理解上的不足。
    *   http://arxiv.org/abs/2606.27187v1

### 研究趋势信号

今日投稿中一个**显著的趋势**是研究者开始更审慎地看待“更大、更多”的简单堆砌。代表性工作如 **“Co-Failure Ceiling”** 量化了多模型组合的收益上限，**“How Surprising Is Historical Italian”** 和 **“How Good Can Linear Models Be”** 则挑战了复杂模型在处理特定问题时必然更好的假设。这预示着未来研究可能更加关注**效率-性能的帕累托前沿**，以及深入理解模型在特定场景下的**根本性失效模式**，例如世界模型幻觉的可预测性研究。

### 值得精读

1.  **When Does Combining Language Models Help? A Co-Failure Ceiling on Routing, Voting, and Mixture-of-Agents Across 67 Frontier Models**
    *   **推荐理由：** 提供了一个简洁而强大的理论框架来解释多模型系统的动态，并用大规模实验进行了佐证。对于任何构建或使用模型集成、智能体团队的从业者，理解这个“天花板”是至关重要的，能帮助避免资源浪费和错误的系统设计。
    *   http://arxiv.org/abs/2606.27288v1

2.  **Reinforcement Learning without Ground-Truth Solutions can Improve LLMs**
    *   **推荐理由：** 解决了强化学习中一个极具实际意义的核心痛点：依赖真值标签。RiVER框架的提出，为对齐模型到人类的复杂偏好、解决开放式问题（如创意写作、代码生成）提供了更强大且可行的工具，潜力巨大。
    *   http://arxiv.org/abs/2606.27369v1

3.  **Hallucination in World Models is Predictable and Preventable**
    *   **推荐理由：** 针对“世界模型幻觉”这一新兴热点，提供了深刻的洞见。文章不仅诊断了问题，还给出了预测和预防的路径。对于希望将生成模型用于机器人、自动驾驶等具身AI领域的研究者来说，这篇论文是必读内容。
    *   http://arxiv.org/abs/2606.27326v1

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*