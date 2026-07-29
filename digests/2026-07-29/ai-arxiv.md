# ArXiv AI 研究日报 2026-07-29

> 数据来源: [ArXiv](https://arxiv.org/) (cs.AI, cs.CL, cs.LG) | 共 50 篇论文 | 生成时间: 2026-07-29 02:10 UTC

---

## 📰 ArXiv AI 研究日报 — 2026-07-29

### 🔍 今日速览
本期投稿集中在**多模态医疗理解**（ClinFusion、KANEx）与**智能体安全与推理**（Agentic Permissions、SIREN）两大方向上，同时涌现出一批关注**可解释性与可靠性**的工作（Sparse Autoencoders的因果几何、D-Score幻觉检测）。效率优化方面，**MoE自推测解码**（DraftExpert）和**注意力量化**（MXAttention）等方案直指部署瓶颈。此外，**长程规划**（Physics of Multi-Turn）与**数据策展**（DataOrchestra）也从原理层面推动了基础模型训练与能力提升。

---

### 📌 重点论文

#### 🧠 大语言模型（架构、训练、对齐、评估）

1. **ClinFusion: A Vision-Centric Multimodal LLM System for Holistic Medical Understanding**  
   [http://arxiv.org/abs/2607.24743v1](http://arxiv.org/abs/2607.24743v1)  
   *H. Yuan, Y. Qian, Z. Tang et al.*  
   → 提出以视觉为中心的多模态医学LLM系统，统一处理2D/3D医学图像与文本，创新在于将视觉编码作为核心而非附属模块。

2. **Rethinking Classifier-Free Guidance in On-Policy Diffusion Distillation**  
   [http://arxiv.org/abs/2607.24731v1](http://arxiv.org/abs/2607.24731v1)  
   *B. Li, H. Wang, H. Xiong et al.*  
   → 首次系统分析无分类器引导（CFG）在同策略扩散蒸馏中的行为，指出现有方法在CFG下的问题并给出改进方向。

3. **DataOrchestra: Learning to Orchestrate Per-Example Curation of Pretraining Data**  
   [http://arxiv.org/abs/2607.24717v1](http://arxiv.org/abs/2607.24717v1)  
   *Z. Huang, Y. Wang, S. Xia et al.*  
   → 提出基于学习的逐样本数据策展方法，而非固定规则，显著提升预训练数据质量对下游性能的影响。

4. **D-Score: A Spectral Hidden-State Signal for Hallucination Detection in LLMs**  
   [http://arxiv.org/abs/2607.24586v1](http://arxiv.org/abs/2607.24586v1)  
   *B. Raimondi, D. Evangelista, M. Gabbrielli et al.*  
   → 从隐藏态激活的谱几何中提取简单信号（D‑Score）用于幻觉检测，无需外部知识，计算代价极低。

#### 🤖 智能体与推理（规划、工具使用、多智能体、思维链）

5. **The Physics of Multi-Turn Long-Horizon Planning: From Pre-training to Post-training**  
   [http://arxiv.org/abs/2607.24720v1](http://arxiv.org/abs/2607.24720v1)  
   *T. Men, Z. Jin, K. Liu et al.*  
   → 系统研究基础模型代理的多轮长程规划能力如何获得与提升，提出从预训练到后训练的完整视角和蒸馏方案。

6. **Agentic Permissions Policy Algebra for Taint Confinement in LLM Agents**  
   [http://arxiv.org/abs/2607.24625v1](http://arxiv.org/abs/2607.24625v1)  
   *A. Kravchenko, V. Liventsev, I. Konstantinov et al.*  
   → 定义智能体权限代数系统，通过信息流控制严格约束污点传播，解决提示注入和推理错误的安全问题。

7. **SIREN: Towards End-to-End Extreme-Weather Early Warning with Experience-Grounded LLM Agents**  
   [http://arxiv.org/abs/2607.24588v1](http://arxiv.org/abs/2607.24588v1)  
   *H. Ni, W. Zhang, F. Liu et al.*  
   → 端到端极端天气预警智能体，结合LLM与经验数据库实现从感知到行动的完整流程，实用价值显著。

#### 🔧 方法与框架（新技术、基准测试、效率优化）

8. **Sparse Autoencoders Encode Both Concepts and Functions: The Downstream Geometry of Feature Effects**  
   [http://arxiv.org/abs/2607.24645v1](http://arxiv.org/abs/2607.24645v1)  
   *P. G. Hoang, A. Chatterjee, T. Chakraborty et al.*  
   → 揭示稀疏自编码器特征不仅编码概念，还编码函数效应，通过下游几何分析为可解释性提供了新的因果视角。

9. **UNIFUSION: Adapting Autoregressive Language Models into Discrete Diffusion under a Unified Reverse-Rate Objective**  
   [http://arxiv.org/abs/2607.24507v1](http://arxiv.org/abs/2607.24507v1)  
   *X. Jiang, J. Li, Y. Jiang et al.*  
   → 首次将自回归语言模型适配为**均匀噪声离散扩散**模型，统一反向率目标，允许采样时所有token仍可编辑。

10. **MXAttention: Data-Free Optimal Scaling and Pre-Normalization Quantization for MXFP4 Attention**  
    [http://arxiv.org/abs/2607.24377v1](http://arxiv.org/abs/2607.24377v1)  
    *J. Yu, J. Lin, L. Kong et al.*  
    → 针对MXFP4注意力量化提出无数据最优缩放和预归一化方法，在不损失生成质量的前提下大幅降低扩散视频模型的计算成本。

11. **DraftExpert: Expansion-Aware Self-Speculative Decoding for End-Device MoE Inference**  
    [http://arxiv.org/abs/2607.24434v1](http://arxiv.org/abs/2607.24434v1)  
    *D. Han*  
    → 面向边缘设备MoE模型的高效自推测解码，利用扩展感知策略缓解专家路由带来的内存和延迟问题。

#### 📊 应用（垂直领域、多模态、代码生成）

12. **EchoBridge: Long-Tail-Aware ECG-Echocardiography Text Alignment**  
    [http://arxiv.org/abs/2607.24553v1](http://arxiv.org/abs/2607.24553v1)  
    *X. Fang, J. Cai, G. Nie et al.*  
    → 专为长尾分布设计的心电图-超声心动图文本对齐方法，提升罕见心脏发现表征学习效果，医疗应用价值高。

13. **CADER: Confidence-Aware Dynamic Evidence Reasoning for Long-Video Understanding**  
    [http://arxiv.org/abs/2607.24582v1](http://arxiv.org/abs/2607.24582v1)  
    *J. Yang, W. Zhang, K. Lin et al.*  
    → 基于置信度的动态证据推理框架，按问题难度自适应调用工具辅助，避免长视频理解中不必要的计算开销。

14. **LLM-SoccerArena: Benchmarking LLMs on Real-World Predictions in Sports**  
    [http://arxiv.org/abs/2607.24573v1](http://arxiv.org/abs/2607.24573v1)  
    *J. Schröder, J. Schweisthal, O. Müller et al.*  
    → 首个面向真实世界体育预测的LLM动态基准，评估模型整合新信息进行未来预测的能力，填补静态基准空白。

---

### 📈 研究趋势信号
本期投稿折射出三个新兴方向：① **可解释性与安全性的融合**——从SAE的因果几何（论文14）到智能体权限代数（15）再到幻觉检测的谱信号（20），研究者正将解释方法与运行时安全监控结合。② **“小代价”推理优化**——无论是MXAttention的无数据量化（46）、DraftExpert的MoE推测解码（41），还是LOCKS（29）的局部KV压缩，都瞄准低资源场景下的高效推理。③ **垂直领域端到端智能体**——SIREN（19）、DeepFaith（49）等作品将LLM代理直接嵌入气象预警、网络防御等高风险流程，并配套可信审计机制，标志着智能体从玩具走向关键应用。

---

### ⭐ 值得精读

1. **《The Physics of Multi-Turn Long-Horizon Planning: From Pre-training to Post-training》**  
   [http://arxiv.org/abs/2607.24720v1](http://arxiv.org/abs/2607.24720v1)  
   → 当前对智能体规划能力最系统的分析之一，从预训练数据特性到后训练蒸馏，逻辑链条完整，对理解基础模型能力上限有重要启发。

2. **《Sparse Autoencoders Encode Both Concepts and Functions: The Downstream Geometry of Feature Effects》**  
   [http://arxiv.org/abs/2607.24645v1](http://arxiv.org/abs/2607.24645v1)  
   → 突破性地将SAE特征与模型行为因果联系起来，提出特征效应的下游几何概念，是可解释性领域的关键推进。

3. **《DraftExpert: Expansion-Aware Self-Speculative Decoding for End-Device MoE Inference》**  
   [http://arxiv.org/abs/2607.24434v1](http://arxiv.org/abs/2607.24434v1)  
   → 面向边缘设备MoE部署的实用解决方案，方法新颖且效率提升显著（文中报告数倍加速），对实际工程有直接参考价值。

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*