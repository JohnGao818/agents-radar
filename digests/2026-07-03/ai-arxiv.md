# ArXiv AI 研究日报 2026-07-03

> 数据来源: [ArXiv](https://arxiv.org/) (cs.AI, cs.CL, cs.LG) | 共 50 篇论文 | 生成时间: 2026-07-03 02:35 UTC

---

# ArXiv AI 研究日报  
**日期：2026-07-03** | 来源：cs.AI / cs.CL / cs.LG（共50篇）

---

## 今日速览

今日投稿呈现三大亮点：**多智能体系统的安全与鲁棒性**成为焦点（Copewell心理健康协作、UA-ChatDev不确定性感知、ContextNest上下文治理）；**LLM推理能力增强**同时从架构创新（线性注意力海马体）和训练策略（纯化自蒸馏）两个方向推进；**自动化科学发现**持续升温，覆盖计算物理全流程（自主研究管道）和论文复现（coding-agents）。此外，扩散模型的推理时控制（ART）和视频grounding专业基准（AnyGroundBench）值得关注。

---

## 重点论文

### 🧠 大语言模型（架构、训练、对齐、评估）

1. **A Hippocampus for Linear Attention: An Exact Memory for What the Recurrent State Forgets**  
   [http://arxiv.org/abs/2607.02303v1](http://arxiv.org/abs/2607.02303v1)  
   *W. Cui et al.*  
   ▶ 借鉴海马体互补学习系统，为线性注意力模型添加精确记忆，解决长序列中早期事实被覆盖的“针海捞针”问题。

2. **Purified OPSD: On-Policy Self-Distillation Without Losing How to Think**  
   [http://arxiv.org/abs/2607.02234v1](http://arxiv.org/abs/2607.02234v1)  
   *Z. Shen et al.*  
   ▶ 揭示在线自蒸馏（OPSD）在长链推理中失败的原因，提出“纯化”版本，保留教师模型推理过程而非仅标签。

3. **Challenges and Recommendations for LLMs-as-a-Judge in Multilingual Settings and Low-Resource Languages**  
   [http://arxiv.org/abs/2607.02235v1](http://arxiv.org/abs/2607.02235v1)  
   *A.S. Doğruöz et al.*  
   ▶ 系统分析LLM作为评估者在多语言场景中的偏差与局限性，提出实践建议。

4. **Bayesian Sparse Low-Rank Adaptation for Large Language Model Uncertainty Estimation**  
   [http://arxiv.org/abs/2607.02182v1](http://arxiv.org/abs/2607.02182v1)  
   *J. Zhang et al.*  
   ▶ 提出数据自适应低秩贝叶斯适配（DALorRA），在微调LLM时同时提供参数高效性和不确定性校准，抑制过拟合。

---

### 🤖 智能体与推理（规划、工具使用、多智能体、思维链）

5. **AgenticSTS: A Bounded-Memory Testbed for Long-Horizon LLM Agents**  
   [http://arxiv.org/abs/2607.02255v1](http://arxiv.org/abs/2607.02255v1)  
   *X. Cheng et al.*  
   ▶ 构建有限记忆测试床，系统评估长周期智能体在观察、工具调用和反思混杂情况下的记忆契约性能。

6. **UA-ChatDev: Uncertainty-Aware Multi-Agent Collaboration for Reliable Software Development**  
   [http://arxiv.org/abs/2607.02186v1](http://arxiv.org/abs/2607.02186v1)  
   *T.O. Ogunsusi et al.*  
   ▶ 为多智能体软件协作框架引入不确定性量化，提升需求分析、编码和测试环节的可靠性。

7. **Copewell: A Multi-Agent Swarm Architecture for Equitable Mental Wellness Support**  
   [http://arxiv.org/abs/2607.02245v1](http://arxiv.org/abs/2607.02245v1)  
   *S. Yenikent et al.*  
   ▶ 采用多智能体蜂群架构提供心理健康支持，专门面向资源匮乏地区，兼顾可及性与公平性。

8. **Coding-agents can replicate scientific machine learning papers**  
   [http://arxiv.org/abs/2607.02134v1](http://arxiv.org/abs/2607.02134v1)  
   *A. Hans, I. Bilionis*  
   ▶ 编码智能体仅凭论文材料即可复现计算声明（如误差<5%），展示自动化科学验证的可行性。

---

### 🔧 方法与框架（新技术、基准测试、效率优化）

9. **HERMES: A Multi-Granularity Labeling Substrate for Pre-training Data Mixtures**  
   [http://arxiv.org/abs/2607.02266v1](http://arxiv.org/abs/2607.02266v1)  
   *Z. Qiao et al.*  
   ▶ 提供多粒度预训练数据标签基座，克服现有分类（来源/主题/聚类）仅沿单一语义轴的局限。

10. **ART for Diffusion Sampling: Continuous-Time Control and Actor-Critic Learning**  
    [http://arxiv.org/abs/2607.02137v1](http://arxiv.org/abs/2607.02137v1)  
    *Y. Huang et al.*  
    ▶ 将扩散采样时间步分配建模为连续时间控制问题，用演员-评论家学习自动搜索最优调度，超越固定/手工方案。

11. **AbsoluteDegradation: A Physics-Inspired Synthetic Film-Degradation Pipeline and Archival Film Restoration Benchmark**  
    [http://arxiv.org/abs/2607.02131v1](http://arxiv.org/abs/2607.02131v1)  
    *M. Jastrzębski et al.*  
    ▶ 提出物理启发的胶片退化合成管道及修复基准，解决档案胶片修复中配对数据缺失和评估标准缺失问题。

12. **A$^{2}$utoLPBench: An Auto-Generated, Agent-Friendly LP Benchmark via Inverse-KKT Construction**  
    [http://arxiv.org/abs/2607.02141v1](http://arxiv.org/abs/2607.02141v1)  
    *S. Ren et al.*  
    ▶ 利用逆KKT条件自动生成线性规划文字题基准，避免静态数据集泄露问题，且面向智能体友好。

---

### 📊 应用（垂直领域、多模态、代码生成）

13. **AnyGroundBench: A Specialized-Domain Benchmark for Video Grounding in Vision-Language Models**  
    [http://arxiv.org/abs/2607.02269v1](http://arxiv.org/abs/2607.02269v1)  
    *R. Otsubo et al.*  
    ▶ 首个面向专业领域（如工业、安防）的时空视频接地基准，填补零样本评估与真实应用间的断裂。

14. **RadiomicNet: A Hybrid Radiomics-Guided Lightweight Architecture for Interpretable Medical Image Segmentation**  
    [http://arxiv.org/abs/2607.02185v1](http://arxiv.org/abs/2607.02185v1)  
    *M.A. Rahman*  
    ▶ 融合放射组学特征与轻量级深度网络，实现可解释且参数高效的医学图像分割。

15. **Guided Action Flow: Q-Guided Inference for Flow-Matching Vision-Language-Action Policies**  
    [http://arxiv.org/abs/2607.02092v1](http://arxiv.org/abs/2607.02092v1)  
    *L. Yang et al.*  
    ▶ 在流匹配视觉-语言-动作策略的推理阶段引入Q值引导，无需重新训练即可实现测试时行为优化。

---

## 研究趋势信号

- **智能体安全与治理**：多篇论文（#18 Criticality-Based Guard Rail、#42 Behind the Refusal、#45 ContextNest）探索AI代理在电信、心理健康、软件协作等场景中的运行时拦截、护栏激活监测和可验证上下文治理，预示“Agent runtime safety”将成为新子领域。
- **长序列与记忆突破**：线性注意力海马体（#3）和智能体长程记忆测试床（#10）共同指向“有损记忆”瓶颈的破解方向，二者分别从架构和评估层面发力。
- **自动化科学复现与基准生成**：自主研究管道（#1）、编码论文复现（#38）、逆KKT基准生成（#35）构成“AI for Science”中的质量控制闭环，可能加速研究的可重复性。
- **扩散模型推理时优化**：除了ART的时间分配控制（#37），Guided Action Flow（#49）也展示了推理时引导的潜力，扩散模型正在从“训练为主”转向“推理时可控”。

---

## 值得精读

1. **A Hippocampus for Linear Attention**（#3）  
   **理由**：首次将互补学习系统理论引入线性注意力模型，从生物启发的角度解决上下文压缩带来的遗忘问题。方法简洁（额外记忆模块），实验覆盖多种长程任务，对下一代高效Transformer设计有直接启发。

2. **Purified OPSD**（#14）  
   **理由**：深入诊断了当前流行的在线自蒸馏策略在长链推理中的失效模式，并提出仅监督推理过程而非结果的改进方案。这项工作可能重构LLM推理自提升的范式，对CoT蒸馏领域影响重大。

3. **A$^{2}$utoLPBench**（#35）  
   **理由**：巧用对偶理论（逆KKT条件）自动生成无限量线性规划问题，彻底避免静态基准的泄露风险。同时设计智能体友好的评估协议，为未来自动化基准构建树立标杆。

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*