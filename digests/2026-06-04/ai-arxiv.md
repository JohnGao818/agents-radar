# ArXiv AI 研究日报 2026-06-04

> 数据来源: [ArXiv](https://arxiv.org/) (cs.AI, cs.CL, cs.LG) | 共 50 篇论文 | 生成时间: 2026-06-04 03:31 UTC

---

# ArXiv AI 研究日报 — 2026-06-04

## 📌 今日速览

今日投稿围绕 **训练数据归因、多智能体流式推理、丰富反馈强化学习** 等方向涌现多项突破。STRIDE 以稀疏恢复技术实现了对大语言模型的高效因果归因；StreamMA 提出流式通信范式，将多智能体系统的推理延迟与管道解耦；Distributional DAgger 将单一正确性信号扩展为丰富反馈的强化学习框架。此外，**失败推理轨迹的再利用** 和 **基础模型研究效度威胁** 等反思性工作引起了广泛关注，预示着社区正从追求规模转向更精细化的方法论建设。

## 📄 重点论文

### 🧠 大语言模型（架构、训练、对齐、评估）

1. **STRIDE: Training Data Attribution via Sparse Recovery from Subset Perturbations**  
   [http://arxiv.org/abs/2606.05165v1](http://arxiv.org/abs/2606.05165v1)  
   *Rishit Dagli, Abir Harrasse, Luke Zhang et al.*  
   → 提出基于稀疏恢复的训练数据归因方法，无需反复重训练即可高效追踪 LLM 预测来源，是归因领域的重大方法革新。

2. **Failed Reasoning Traces Tell You What Is Fixable (But Not by Reading Them)**  
   [http://arxiv.org/abs/2606.05145v1](http://arxiv.org/abs/2606.05145v1)  
   *Nizar Islah, Istabrak Abbes, Irina Rish et al.*  
   → 证明失败推理轨迹包含可修复信号，但需通过特定机制而非简单重复采样来利用，挑战了单纯增加计算量的测试时扩展策略。

3. **Self-Evaluation Is Already There: Eliciting Latent Judge Calibration in Base LLMs with Minimal Data**  
   [http://arxiv.org/abs/2606.05122v1](http://arxiv.org/abs/2606.05122v1)  
   *XiuYu Zhang, Yi Shan, Junfeng Fang et al.*  
   → 发现基础 LLM 在少量示例下即可预测外部裁判的评分，表明自评估能力已内隐存在，无需专门训练。

4. **Fast & Faithful Function Vectors**  
   [http://arxiv.org/abs/2606.05079v1](http://arxiv.org/abs/2606.05079v1)  
   *Minh An Pham, Anton Segeler, Thomas Wiegand et al.*  
   → 系统研究了函数向量的定义选择（在上下文学习中提取任务表示），提出了更快速且保真的变体。

5. **Imbuing Large Language Models with Bidirectional Logic for Robust Chain Repair**  
   [http://arxiv.org/abs/2606.05030v1](http://arxiv.org/abs/2606.05030v1)  
   *Zehua Cheng, Wei Dai, Jiahao Sun et al.*  
   → 针对自回归链式推理的误差累积问题，引入双向逻辑机制实现链式修复，抑制错误雪崩。

### 🤖 智能体与推理（规划、工具使用、多智能体、思维链）

6. **Streaming Communication in Multi-Agent Reasoning**  
   [http://arxiv.org/abs/2606.05158v1](http://arxiv.org/abs/2606.05158v1)  
   *Zhen Yang, Xiaogang Xu, Wen Wang et al.*  
   → 提出 StreamMA，将推理步骤即时流式传输给下游智能体，使多智能体推理延迟不再随管道深度线性增长。

7. **AutoLab: Can Frontier Models Solve Long-Horizon Auto Research and Engineering Tasks?**  
   [http://arxiv.org/abs/2606.05080v1](http://arxiv.org/abs/2606.05080v1)  
   *Zhangchen Xu, Junda Chen, Yue Huang et al.*  
   → 构建长周期自动化科研与工程基准，评估前沿模型在迭代实验、持续改进任务上的能力。

8. **Strabo: Declarative Specification and Implementation of Agentic Interaction Protocols**  
   [http://arxiv.org/abs/2606.05043v1](http://arxiv.org/abs/2606.05043v1)  
   *Samuel H. Christie, Amit K. Chopra, Munindar P. Singh*  
   → 基于声明式交互协议实现多智能体系统，为工业 Agentic AI 提供规范化、可组合的协议框架。

### 🔧 方法与框架（新技术、基准测试、效率优化）

9. **Reinforcement Learning from Rich Feedback with Distributional DAgger**  
   [http://arxiv.org/abs/2606.05152v1](http://arxiv.org/abs/2606.05152v1)  
   *Rishabh Agrawal, Jacob Fein-Ashley, Paria Rashidinejad*  
   → 将传统 RLVR 的单一正确性反馈扩展为分布式的丰富反馈（如步骤级打分），显著提升推理模型的训练效率。

10. **Validity Threats for Foundation Model Research**  
    [http://arxiv.org/abs/2606.05029v1](http://arxiv.org/abs/2606.05029v1)  
    *Gunnar König, Martin Pawelczyk, Ulrike von Luxburg et al.*  
    → 系统性梳理基础模型研究中因代理实验、廉价近似等方法导致的效度威胁，呼吁社区建立更严格的实验准则。

11. **Knowledge Index of Noah's Ark (KINA)**  
    [http://arxiv.org/abs/2606.05104v1](http://arxiv.org/abs/2606.05104v1)  
    *Sheng Jin, Minghao Liu, Yunze Xiao et al.*  
    → 构建覆盖 261 个领域、899 道题的知识基准，通过学科代表性设计和抗懒惰共识的标注机制，提升 LLM 知识评估的可靠性。

### 📊 应用（垂直领域、多模态、代码生成）

12. **Continual Visual and Verbal Learning Through a Child's Egocentric Input**  
    [http://arxiv.org/abs/2606.05115v1](http://arxiv.org/abs/2606.05115v1)  
    *Xiaoyang Jiang, Yanlai Yang, Kenneth A. Norman et al.*  
    → 使用儿童视角的第一人称视频数据实现视觉-语言连续学习，模拟人类词义习得的自然过程。

13. **Evaluating Large Language Models in Dynamic Clinical Decision-Making with Standardized Patient Cases**  
    [http://arxiv.org/abs/2606.05112v1](http://arxiv.org/abs/2606.05112v1)  
    *Cheng Liang, Pengcheng Qiu, Ya Zhang et al.*  
    → 构建动态临床决策评估基准，通过标准化病人案例检验 LLM 在信息采集、治疗规划和长期管理上的连续性表现。

14. **M³Eval: Multi-Modal Memory Evaluation through Cognitively-Grounded Video Tasks**  
    [http://arxiv.org/abs/2606.05008v1](http://arxiv.org/abs/2606.05008v1)  
    *Jie Huang, Ruixun Liu, Sirui Sun et al.*  
    → 基于认知心理学的视频任务，系统评估多模态模型的长视频记忆能力，填补现有基准只测感知不测记忆的空白。

## 🔍 研究趋势信号

今日投稿中出现两个值得关注的趋势：一是 **“失败数据”的再利用** 从训练扩展到推理阶段（Failed Reasoning Traces、Imbuing LLMs with Bidirectional Logic），社区开始相信模型已经包含修复所需的信息，关键是如何提取。二是 **基础模型研究的方法论反思**（Validity Threats）成为独立课题，标志着该领域正从粗放实验走向严谨科学。此外，**因果归因方法** 向大型语言模型迁移（STRIDE）和 **多智能体通信范式** 的改进（StreamMA）也预示着系统级效率提升的新方向。

## 🌟 值得精读

- **STRIDE**：为 LLM 可解释性提供了可扩展的因果归因工具，直接打开“模型为什么这样回答”的黑箱，对安全对齐和数据分析具有广泛意义。  
- **Failed Reasoning Traces Tell You What Is Fixable**：挑战了“失败就再试一次”的主流做法，揭示了失败轨迹中的潜在信号，可能改变测试时计算的资源分配策略。  
- **Validity Threats for Foundation Model Research**：系统揭露了当前基础模型研究中的常见实验陷阱（如代理实验、廉价评估），是每一位研究者都应阅读的方法论指南。

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*