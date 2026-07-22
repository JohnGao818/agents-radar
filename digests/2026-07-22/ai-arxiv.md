# ArXiv AI 研究日报 2026-07-22

> 数据来源: [ArXiv](https://arxiv.org/) (cs.AI, cs.CL, cs.LG) | 共 50 篇论文 | 生成时间: 2026-07-22 02:12 UTC

---

# ArXiv AI 研究日报 — 2026-07-22

---

## 今日速览

1. **推理增强与 RLVR 范式扩展** — 多篇工作将强化学习与可验证奖励（RLVR）应用到机器翻译、分子生成、作文评分等场景，验证了“推理-验证”框架在开放任务中的泛化潜力。
2. **多模态理论与心智推理** — MeetingToM 提出多模态会议场景的心智理论基准，挑战 AI 对多人交互中信念与意图的理解能力。
3. **投机解码与高效推理** — AdaFlash 利用在线策略蒸馏的扩散草稿模型实现自适应投机解码，在保持质量的同时显著加速 LLM 推理。
4. **科学模拟与物理信息学习** — 热力学、超临界燃烧、电解质溶液活性、粘弹性接触等物理领域涌现出一批结合先验知识与深度学习的实用方法。
5. **数据质量与自动化数据决策** — SFGA 将 SFT 数据采购建模为成本感知路由问题，利用统计优先的门控架构实现可信数据获取；AutoJourn 探索新闻生成的偏差检测与多视角摘要。

---

## 重点论文

### 🧠 大语言模型（架构、训练、对齐、评估）

1. **The Price of Reasoning: Cost-Quality Tradeoffs in Reinforcement Learning for Neural Machine Translation**  
   [ArXiv](http://arxiv.org/abs/2607.19226v1) · Jungo, An  
   → 系统研究 RLVR 在神经机器翻译中的成本-质量权衡，证明在翻译任务中 RLVR 可替代 SFT。

2. **Beyond Score Prediction: LLM-Based Essay Scoring and Feedback Generation via Reinforcement Learning with Rubric Rewards**  
   [ArXiv](http://arxiv.org/abs/2607.19219v1) · Jin et al.  
   → 首次将 RL 后训练（评分规则奖励）用于自动化作文评分与反馈生成，超越传统提示工程方法。

3. **Measuring Reward-Seeking via Contrastive Belief Updates**  
   [ArXiv](http://arxiv.org/abs/2607.18966v1) · Højmark et al.  
   → 提出对比信念更新方法检测语言模型是否“迎合评分者偏好”而非真正优化目标，为对齐研究提供新工具。

4. **DAIS: Dependency-Aware Intermediate QA Supervision for Complex Reasoning**  
   [ArXiv](http://arxiv.org/abs/2607.19088v1) · Wang, Fan et al.  
   → 引入依赖感知的中间问题监督，使 CoT 推理中局部结论能显式支持后续决策，提升复杂推理能力。

### 🤖 智能体与推理（规划、工具使用、多智能体、思维链）

5. **MeetingToM: Evaluating Multimodal LLMs on Theory-of-Mind Reasoning in Multi-Party Meetings**  
   [ArXiv](http://arxiv.org/abs/2607.19235v1) · Wang, Wu et al.  
   → 首个面向多人会议场景的多模态心智理论基准，评估模型从言语与行为推断他人信念的能力。

6. **S3: Stable Subgoal Selection by Constraining Uncertainty of Coarse Dynamics in Hierarchical Reinforcement Learning**  
   [ArXiv](http://arxiv.org/abs/2607.19232v1) · Srivastava, Jerath  
   → 约束粗粒度动力学的不确定性以稳定子目标选择，显著提升分层强化学习在长程任务中的性能。

7. **Adopting Reinforcement Learning with Verifiable Rewards for Molecular Generation**  
   [ArXiv](http://arxiv.org/abs/2607.19044v1) · Ouyang et al.  
   → 将 RLVR 范式引入分子生成，利用可验证化学属性作为奖励信号，无需大规模标注数据。

8. **AutoJourn: Multi-Perspective Summarisation, Bias Detection and Bias Neutralisation for LLM-Generated News**  
   [ArXiv](http://arxiv.org/abs/2607.18983v1) · Ghosh et al.  
   → 演示系统，自动从社交媒体提取多视角、检测并中和新闻生成中的偏见，推动负责任的自动新闻。

### 🔧 方法与框架（新技术、基准测试、效率优化）

9. **AdaFlash: Adaptive Speculative Decoding via On-Policy Distilled Diffusion Drafters**  
   [ArXiv](http://arxiv.org/abs/2607.19223v1) · Qian et al.  
   → 利用在线策略蒸馏的扩散草稿模型实现自适应投机解码，推理加速显著且保持生成质量。

10. **One Model, Many Graphs: Learning over Attributed Graphs across Heterogeneous Modalities with Vision-Language Models**  
    [ArXiv](http://arxiv.org/abs/2607.19128v1) · Yang et al.  
    → 提出 VLM 作为通用图骨干网络，统一处理文本、图像等多模态属性图，突破异质性障碍。

11. **SFGA: A Statistics-First Gating Architecture with Adjudicative Escalation for Trustworthy SFT Data Procurement**  
    [ArXiv](http://arxiv.org/abs/2607.18960v1) · Tian et al.  
    → 把 SFT 数据采购视为成本感知路由问题，通过统计优先的门控与裁决升级机制实现可信数据获取。

12. **Disentangling Curriculum Learning in NLP: Towards a Unifying Taxonomy**  
    [ArXiv](http://arxiv.org/abs/2607.18984v1) · Toborek et al.  
    → 提出细粒度难度函数与调度器分类法，为 NLP 课程学习提供原则性指导，填补领域理论空白。

### 📊 应用（垂直领域、多模态、代码生成）

13. **Thermodynamics-Informed Input Reparameterization for Neural Prediction of Real-Fluid Thermodynamic Properties**  
    [ArXiv](http://arxiv.org/abs/2607.19241v1) · Zhang et al.  
    → 热力学启发的输入重参数化，大幅降低超临界燃烧模拟中物性评估的计算成本，具有工程实用价值。

14. **Predicting Activities in Aqueous Electrolyte Solutions with Hybrid Machine Learning**  
    [ArXiv](http://arxiv.org/abs/2607.19114v1) · Romero et al.  
    → 混合机器学习方法预测电解质溶液活度和渗透系数，结合 Pitzer 模型与数据驱动，精度超越传统经验模型。

15. **DBMol: Design of High-Affinity, Target-Specific Small Molecules through Structure Prediction Models**  
    [ArXiv](http://arxiv.org/abs/2607.19237v1) · Qin et al.  
    → 利用 AlphaFold-3/Boltz-2 等结构预测模型直接设计高亲和力小分子，药物发现流程新范式。

16. **MIRAGE: Multi-scale Lesion-Informed Representation with Auxiliary Guidance for MRI Contrast Enhancement**  
    [ArXiv](http://arxiv.org/abs/2607.19137v1) · Borghesi et al.  
    → 多尺度病灶感知表示与辅助引导用于增强 MRI 对比度推断，解决无增强基线下的病灶增强不确定性问题。

---

## 研究趋势信号

- **“推理-验证”范式的扩散**：RLVR 从代码和数学走向机器翻译、分子生成、作文评分等开放任务，表明可验证奖励与显式推理链的结合正成为通用后训练框架。
- **物理信息学习走向实用化**：多篇论文（热力学、电解质、粘弹性接触）将先验物理知识（守恒律、对称性、热力学一致性）直接编码为网络结构或损失函数，而非仅作为数据增强，显著提升泛化与可靠性。
- **自动化数据质量与采购**：从 SFT 数据采购（SFGA）到新闻偏差中和（AutoJourn），社区越来越关注如何系统性地评估和获取高质量、低偏差的训练数据，这可能在工业应用中成为关键基础设施。
- **多智能体与心智理论评估**：MeetingToM 等基准的出现标志着 LLM 评估从单轮问答向复杂的、需要持续推理他人心智状态的多方交互场景演进。

---

## 值得精读

1. **AdaFlash: Adaptive Speculative Decoding via On-Policy Distilled Diffusion Drafters**  
   *理由：* 将扩散模型与在线策略蒸馏结合用于投机解码，在保证生成质量的同时显著提速，突破了传统自回归草稿模型的瓶颈。对 LLM 推理部署有直接工程价值。

2. **MeetingToM: Evaluating Multimodal LLMs on Theory-of-Mind Reasoning in Multi-Party Meetings**  
   *理由：* 填补了多模态、多人交互场景下心智理论评估的空白。任务设计紧密结合真实会议场景（言语+行为线索），是了解当前 MLLM 社交推理能力上限的重要基准。

3. **The Price of Reasoning: Cost-Quality Tradeoffs in Reinforcement Learning for Neural Machine Translation**  
   *理由：* 系统回答了“RLVR 在非代码任务中是否真的值得”这一关键问题。作者不仅展示效果，更量化计算成本与质量提升的权衡，为从业者选择训练范式提供了实证依据。

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*