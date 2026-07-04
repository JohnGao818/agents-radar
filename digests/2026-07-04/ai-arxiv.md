# ArXiv AI 研究日报 2026-07-04

> 数据来源: [ArXiv](https://arxiv.org/) (cs.AI, cs.CL, cs.LG) | 共 50 篇论文 | 生成时间: 2026-07-04 02:32 UTC

---

# ArXiv AI 研究日报 | 2026-07-04

---

## 今日速览

今日投稿聚焦于 **LLM 安全与对齐**（分布式后门攻击、在线监测、遗忘定位）、**多智能体社会涌现**（隐性目标与社交结构）、以及 **代码生成与强化学习**（模块化生成、首次可靠性分析）。此外，**长上下文推理**（递归证据回放）和 **训练效率优化**（自蒸馏数据选择、扩散模型量化）也涌现出值得关注的新方法。**安全与可靠性**成为贯穿多篇论文的核心主线。

---

## 重点论文

### 🧠 大语言模型（架构、训练、对齐、评估）

1. **Distributed Attacks in Persistent-State AI Control**  
   http://arxiv.org/abs/2607.02514v1  
   *J. Hills, I. Caspary, A. C. Stickland*  
   → 提出一类针对持久化代码库的新型攻击：恶意或 prompt-injected 的 AI 编码智能体可将攻击分布在多个 PR 中并定时触发，暴露了持续部署场景下的安全盲区。

2. **LACUNA: A Testbed for Evaluating Localization Precision for LLM Unlearning**  
   http://arxiv.org/abs/2607.02513v1  
   *M. Boglioni, T. Rousset, S. Reddy et al.*  
   → 为 LLM “遗忘”（unlearning）中目标知识定位的精度提供了标准化测试平台，推动“先定位、后删除”范式的可量化评估。

3. **Online Safety Monitoring for LLMs**  
   http://arxiv.org/abs/2607.02510v1  
   *M. Schirmer, M. Jazbec, A. Timans et al.*  
   → 提出一种轻量级实时在线监测器，利用外部验证器信号生成报警，在不依赖对齐训练的情况下拦截不安全输出。

4. **ReContext: Recursive Evidence Replay as LLM Harness for Long-Context Reasoning**  
   http://arxiv.org/abs/2607.02509v1  
   *Y. Zhao, R. Qiu, T. Wei et al.*  
   → 通过递归回放输入中已有的证据，使 LLM 在长上下文中有效利用相关信息，缓解长距离遗忘问题。

5. **DRIFTLENS: Measuring Memory-Induced Reasoning Drift in Personalized Language Models**  
   http://arxiv.org/abs/2607.02374v1  
   *X. Fang, W. Xu, Y. Ge et al.*  
   → 首次系统测量个性化记忆注入对模型推理轨迹的“漂移”影响，揭示个性化不仅改变输出，还会改变推理过程本身。

### 🤖 智能体与推理（规划、工具使用、多智能体、思维链）

6. **What LLM Agents Say When No One Is Watching: Social Structure and Latent Objective Emergence in Multi-Agent Debates**  
   http://arxiv.org/abs/2607.02507v1  
   *A. Ghaffarizadeh, D. Mohaddes, A. Izadkhah et al.*  
   → 在没有显式目标提示的情况下，仅通过角色、受众、关系结构就能使多智能体在公共和私下言论中产生分化，涌现出隐性目标。

7. **G-RRM: Guiding Symbolic Solvers with Recurrent Reasoning Models**  
   http://arxiv.org/abs/2607.02491v1  
   *T. Bertram, S. Bhavnani, R. Freinschlag et al.*  
   → 神经符号方法：用符号等变递归推理模型引导约束求解器，在处理更大规模实例时表现出更强的外推能力。

8. **DecompRL: Solving Harder Problems by Learning Modular Code Generation**  
   http://arxiv.org/abs/2607.02390v1  
   *J. Decugis, F. Gloeckle, F. Bach et al.*  
   → 用强化学习训练 LLM 生成模块化代码，将复杂问题分解为子函数，显著提升首次正确率并降低 GPU 成本。

### 🔧 方法与框架（新技术、基准测试、效率优化）

9. **Program-as-Weights: A Programming Paradigm for Fuzzy Functions**  
   http://arxiv.org/abs/2607.02512v1  
   *W. Zhang, L. Hotsko, W. Kim et al.*  
   → 提出将程序作为模型权重嵌入，用于模糊函数（如日志告警、JSON 修复），在保留可复现性和本地性的同时获得 LLM 级别的灵活性。

10. **OrbitQuant: Data-Agnostic Quantization for Image and Video Diffusion Transformers**  
    http://arxiv.org/abs/2607.02461v1  
    *D. Lee, J. Chavan, D. Nguyen et al.*  
    → 针对扩散 transformer 提出与数据无关的量化方法，能适应时步、提示和引导分支间的激活分布变化，大幅降低推理开销。

11. **DemoPSD: Disagreement-Modulated Policy Self-Distillation**  
    http://arxiv.org/abs/2607.02502v1  
    *Y. Li, H. Shi, W. Liu et al.*  
    → 改进在线自蒸馏方法，通过师生分歧度调节 token 级知识传递，避免教师密集标签带来的噪声。

12. **TestEvo-Bench: An Executable and Live Benchmark for Test and Code Co-Evolution**  
    http://arxiv.org/abs/2607.02469v1  
    *J. A. Wang, K. Wang, P. Nie*  
    → 建立首个可执行的测试与代码协同演化基准，验证测试是否随代码变更真正更新，推动软件工程智能体评估。

### 📊 应用（垂直领域、多模态、代码生成）

13. **Reasoning LLM Improves Speaker Recognition in Long-form TV Dramas**  
    http://arxiv.org/abs/2607.02504v1  
    *Y. Li, L. Xie, X. Huo et al.*  
    → 将推理型 LLM 引入长篇电视剧说话人识别，通过多轮推理准确归因每一句台词的角色身份，推动视频理解与语音识别结合。

14. **Text-Driven 3D Indoor Scene Synthesis in Non-Manhattan Environments**  
    http://arxiv.org/abs/2607.02407v1  
    *X. Meng, Z. Song, Y. Zhang et al.*  
    → 突破非曼哈顿（非正交）空间的限制，利用 LLM 生成符合非正交空间关系的 3D 室内布局，拓展了文本到 3D 的适用范围。

15. **WorldSample: Closed-loop Real-robot RL with World Modelling**  
    http://arxiv.org/abs/2607.02431v1  
    *Y. Xue, L. Xu, Z. Liu et al.*  
    → 通过世界模型在闭环环境中进行真实机器人强化学习，克服模仿学习对演示覆盖的依赖，实现更高效的试错学习。

---

## 研究趋势信号

- **安全与可靠性从静态对齐走向动态防御**：分布式攻击、在线监测、遗忘定位等论文表明，社区对 LLM 部署后的持续安全投入了显著关注。
- **多智能体社会计算成为新热点**：隐性目标涌现、社交结构分化等研究揭示，LLM 智能体在结构化群体中会自发形成复杂的非对称行为。
- **代码生成加速强化学习化**：模块化生成、测试协同演化、首次可靠性分析等方向显示，代码智能体正从“一次生成”转向“持续修改与学习”。
-

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*