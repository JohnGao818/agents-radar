# ArXiv AI 研究日报 2026-06-18

> 数据来源: [ArXiv](https://arxiv.org/) (cs.AI, cs.CL, cs.LG) | 共 50 篇论文 | 生成时间: 2026-06-18 03:33 UTC

---

# ArXiv AI 研究日报 ｜ 2026-06-18

## 今日速览

今日投稿呈现出三个突出方向：**推理模型训练与对齐**成为焦点，DreamReasoner-8B 将扩散模型引入长链推理，STARE 揭示并缓解 GRPO 训练中的熵崩溃问题，同时机制级遗忘学习（MAST）为精准移除 RLVR 效果提供了新范式；**智能体评估与设计**向真实场景纵深推进，TxBench-PP 为药物发现智能体构建可验证基准，多智能体虚构博弈提升了 LLM 在博弈决策中的表现；**评估方法论**迎来反思，AUC 在深伪检测中的局限性被系统论证，VLA 模型的知识保留能力也受到严格拷问。此外，程序合成解释注意力、神经符号统一框架 NeSyCat 等基础方法创新同样值得关注。

---

## 重点论文

### 🧠 大语言模型（架构、训练、对齐、评估）

**1. DreamReasoner-8B: Block-Size Curriculum Learning for Diffusion Reasoning Models**  
http://arxiv.org/abs/2606.19257v1  
Zirui Wu, Lin Zheng, Jiacheng Ye et al.  
**一句话**：首个开源块扩散推理模型，通过块大小课程学习实现长链思维的有效缩放，为扩散模型应用于推理任务开辟新路径。

**2. STARE: Surprisal-Guided Token-Level Advantage Reweighting for Policy Entropy Stability**  
http://arxiv.org/abs/2606.19236v1  
Haipeng Luo, Qingfeng Sun, Songli Wu et al.  
**一句话**：对 GRPO 等 RLVR 算法进行一阶梯度分析，提出基于惊讶度的 token 级优势重加权，有效防止策略熵崩溃，提升训练稳定性。

**3. Mechanism-Guided Selective Unlearning for RLVR-Induced Reasoning**  
http://arxiv.org/abs/2606.19222v1  
Chenyu Zhou, Qiliang Jiang, Shuning Wu et al.  
**一句话**：提出 MAST 方法，通过识别 RLVR 训练引入的增量参数实现精准遗忘，相比全参数更新大幅降低副作用。

**4. Beyond Safe Data: Pretraining-Stage Alignment with Regular Safety Reflection**  
http://arxiv.org/abs/2606.19168v1  
Jinhan Li, Kexian Tang, Yihan Xu et al.  
**一句话**：将安全对齐提前至预训练阶段，提出“安全反思”机制，使模型在预训练中主动学习对不安全信号的抑制能力。

---

### 🤖 智能体与推理（规划、工具使用、多智能体、思维链）

**5. Native Active Perception as Reasoning for Omni-Modal Understanding**  
http://arxiv.org/abs/2606.19341v1  
Zhenghao Xing, Ruiyang Xu, Yuxuan Wang et al.  
**一句话**：提出原生主动感知范式，将长视频理解转化为推理任务，避免统一处理所有帧，计算成本随视频线性增长的问题得到缓解。

**6. Enhancing Decision-Making with Large Language Models through Multi-Agent Fictitious Play**  
http://arxiv.org/abs/2606.19308v1  
Leyang Shen, Yang Zhang, Xiaoyan Zhao et al.  
**一句话**：将多智能体虚构博弈引入 LLM 系统，使多个智能体在博弈中逐步收敛到更优决策，弥补了传统分治策略在决策任务上的不足。

**7. TxBench-PP:

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*