# ArXiv AI 研究日报 2026-08-04

> 数据来源: [ArXiv](https://arxiv.org/) (cs.AI, cs.CL, cs.LG) | 共 50 篇论文 | 生成时间: 2026-08-04 02:06 UTC

---

# ArXiv AI 研究日报

**日期：2026-08-04 | 共收录论文 50 篇（cs.AI / cs.CL / cs.LG）**

---

## 📌 今日速览

今日投稿呈现出三大主线：其一是**深度路由架构**与**高效端侧模型**的持续演进，如 Role-Decoupled Attention Residuals 与 Opt.Gear，表明研究者正从注意力机制本身和轻量级部署双路并进；其二是**智能体评估从静态快照迈向时序与状态感知**，多篇论文（如"19:05"场景生成、回归评测集策展）直指现有离线评估的致命缺陷；其三是**安全与可信研究走向精细化**，涵盖模型窃取防御（Caliber）、VLM 多模态越狱的悖论性防御、以及 LLM 作为评估者的"静默遗漏"问题。此外，医疗领域的 sycophancy 深度分析与少见病例辅助系统也值得关注。

---

## 🔍 重点论文

### 🧠 大语言模型（架构、训练、对齐、评估）

**1. Role-Decoupled Attention Residuals: Separating Matching and Content Retrieval Across Depth**
🔗 http://arxiv.org/abs/2608.01075v1
👤 Kehan Wang et al.
💡 提出角色解耦的注意力残差机制，解决了现有 Block Attention Residuals 用单一内容相关混合构造 Q/K/V 输入的局限，为深度路由架构提供更精细的检索-匹配分离方案。

**2. Opt.Gear Technical Report**
🔗 http://arxiv.org/abs/2608.01034v1
👤 Juneyoung Park, Youngwook Kwon et al.
💡 发布面向端侧部署的轻量级基础模型（1M/270M/1B，上下文 64K），采用卷积键值门控混合器的新型混合架构，兼顾实时推理与任务能力。

**3. Why LLMs Give In: Conversational Factors and Reasoning Behind Medical Sycophancy**
🔗 http://arxiv.org/abs/2608.01017v1
👤 Kaike Ping, Buse Çarık, Caleb Wohn et al.
💡 系统剖析医疗场景下 LLM 因用户反驳而放弃正确回答的"医学谄媚"行为，揭示其对话因素与内在推理机制——比单纯答错更危险，因为它把可信度借给了错误信息。

**4. Cloud-ScPO: Hidden-State Geometry for Semi-Supervised Preference Optimization in LLM Reasoning**
🔗 http://arxiv.org/abs/2608.01014v1
👤 Yuzhou Liu, Xiyang Hu et al.
💡 探索从模型内部隐状态几何直接推导偏好监督信号，无需标注或奖励模型即可进行半监督偏好优化，为推理能力提升开辟低成本路径。

**5. DeBERTa-Sentinel: Toward Transparent and Trustworthy Detection of AI-Generated Text**
🔗 http://arxiv.org/abs/2608.01046v1
👤 Muhammad Yousaf Rehman, Muhammad Islam et al.
💡 改进 GPT-Sentinel 的泛化短板，提出基于 DeBERTa 的 AI 生成文本检测器，旨在提升检测的透明度与可信度。

---

### 🤖 智能体与推理（规划、工具使用、多智能体、记忆）

**6. Don't Offer What Can't Be Done: Deterministic Executability Gating for LLM Skill Selection at Scale**
🔗 http://arxiv.org/abs/2608.01050v1
👤 Ortal Ashkenazi, Vitalii Kloz, Mykhailo Ulianchenko et al.
💡 来自 Wix 生产环境的可部署经验：在客服智能体中引入确定性可执行性门控，解决"语义相关但当前账户状态无法执行"的技能误选问题。

**7. What Could the Agent See at 19:05? Generating Temporal Enterprise Scenarios from Real Research and Replaying Them to Evaluate Agents**
🔗 http://arxiv.org/abs/2608.01042v1
👤 Tezan Sahu, Himani Arora et al.
💡 直击企业智能体离线评估只能对照"终点静态快照"的缺陷，提出从真实研究数据生成时序场景并回放，使评估符合"作答时点数据可见性"这一真实约束。

**8. PROGRESS: Coverage-guided RL to Train Search-augmented LLM Agent**
🔗 http://arxiv.org/abs/2608.00969v1
👤 Sudipta Paul, Vijay Srinivasan, Vivek Kulkarni et al.
💡 针对现有搜索增强智能体仅依赖结果级奖励的问题，引入覆盖率引导的强化学习，对搜索过程本身提供监督，提升复杂查询分解能力。

**9. Search-GRT: Guided Retrieval Training of Search Agents to Optimize for Complex Question Answering**
🔗 http://arxiv.org/abs/2608.00974v1
👤 Aounon Kumar, Sudipta Paul, Vivek Kulkarni et al.
💡 面向多跳问答的搜索智能体引导式检索训练，显式优化子查询生成-检索-综合的完整链路。

**10. TrajWiki: Source-Grounded Memory Trajectories for Long-Horizon Dialogue Agents**
🔗 http://arxiv.org/abs/2608.00967v1
👤 Jingyu Sun, Yuyang Xue, Mingyang Li et al.
💡 提出可溯源、可更新、诊断透明的记忆轨迹机制，解决长时对话智能体的外部记忆缺乏可解释性的问题。

**11. PMMC: Prospective Multimodal Memory Compilation for Long-Term LVLM Agents**
🔗 http://arxiv.org/abs/2608.00962v1
👤 Jingyu Sun, Yan Lin, Yuyang Xue et al.
💡 摆脱"视觉经验降级为文本摘要"的做法，提出前瞻式多模态记忆编译，面向长期 LVLM 智能体的跨模态交互信息整合。

---

### 🔧 方法与框架（新技术、基准测试、效率优化）

**12. SCHEDBench: A Benchmark for Evaluating LLM Constraint Faithfulness in Natural-Language Combinatorial Scheduling**
🔗 http://arxiv.org/abs/2608.00991v1
👤 Shrenil Shaun Sharma, Avi Sharma et al.
💡 新的自然语言组合调度基准，检验 LLM 在表面形式变化下对约束的忠实度，以求解器推导的可行性/最优性为金标准。

**13. Caliber: Cross-Architecture Extraction-Cost Control for Score-Returning APIs**
🔗 http://arxiv.org/abs/2608.01023v1
👤 Chi Wang, Hanwen Wang, Yu Xia et al.
💡 将模型窃取防御中的噪声选择重构为校准问题，为返回分数的 API 提供跨架构的、可证明的提取成本控制。

**14. Judging Is Not Enumerating: Silent Omissions in LLM-Authored Acceptable Sets**
🔗 http://arxiv.org/abs/2608.01000v1
👤 Wenhui Chen, Jianlin Chen, Ziyao Lin et al.
💡 揭示 LLM 从"考生"升级为"考官"（编写测试套件、答案密钥、奖励函数）时的系统性缺陷：在枚举式部署协议下会静默遗漏合法项。

**15. From AI Technical Debt to Agentic Technical Debt: A Systematic Mapping of Root Causes and Manifestations in Agentic AI Systems**
🔗 http://arxiv.org/abs/2608.01001v1
👤 Muhammad Tukur, Hayatullahi B. Adeyemo, Tao Chen et al.
💡 首次将"技术债"概念系统性迁移至 Agentic AI 系统，绘制自主推理、多智能体协作、工具编排等新形态下的根因与表现图谱。

---

### 📊 应用（垂直领域、多模态、代码生成）

**16. WAM-Diff2: Hierarchical AR-to-Diffusion Distillation for Highly Efficient Autonomous Driving VLA**
🔗 http://arxiv.org/abs/2608.01035v1
👤 Zhihao Zhu, Hanlin Shang, Mingwang Xu et al.
💡 针对自动驾驶 VLA 模型自回归解码延迟高、暴露偏差大的痛点，提出层级 AR 到扩散模型的蒸馏方案，兼顾效率与轨迹质量。

**17. MedUPS: Towards Diagnostic Assistance in Uncommon Medical Cases with Large Language Models**
🔗 http://arxiv.org/abs/2608.01012v1
👤 Ofir Ben Shoham, Oriel Perets, Nir Grinberg et al.
💡 罕见病辅助诊断基准：多数医学 LLM 评测只打分最终诊断，MedUPS 要求模型在诊断不确定下做出一系列管理决策，更贴近临床真实流程。

**18. CallScreenBench: Benchmarking On-Device Models as Phone Secretaries**
🔗 http://arxiv.org/abs/2608.01033v1
👤 Simiao Ren et al.
💡 面向端侧量化小模型"代接电话"任务的评测基准，探索设备端智能体自主化的新型场景。

**19. An AI Approach to Verified Production Cryptographic Libraries**
🔗 http://arxiv.org/abs/2608.00965v1
👤 Chuyue Sun, Su Fong, Zhiyi Kuang et al.
💡 将 LLM 证明系统从"孤立证明义务"推向生产级密码库的形式化验证，解决从未给定的完整库验证难题。

**20. Decoy Images Amplify Caption-Mediated Defenses Against Encoded Jailbreaks**
🔗 http://arxiv.org/abs/2608.01043v1
👤 Haoyu Zhang, Xiangchen Guan, Shibo Zheng et al.
💡 发现反直觉现象：为编码越狱提示配对无关诱饵图像可显著降低攻击成功率，机制在于防御管线中的标题中介环节——而非模型本身。

---

## 📈 研究趋势信号

今日投稿中最值得注意的趋势有三个方向：

1. **智能体评估进入"时间感知"范式**：多篇论文（"19:05"时序场景、回归评测集策展、CallScreenBench）共同指向一个判断——静态快照评测已不足以支撑真实部署的智能体，评估必须纳入数据状态的时间演化与可见性约束。

2. **AI 与形式验证/安全审计的交叉深化**：从生产密码库验证到"发现主张的双侧审计"，研究者开始用 LLM 处理原本属于形式方法领域的任务，并把审计标准从"基准分数"推向"可判定的负例"。

3. **多模态安全涌现出反直觉机制**：Decoy Images 揭示的"诱饵图像放大防御"效应提醒我们，VLM 攻击与防御的交互空间远未被充分探索，安全研究需要更细粒度的管线级分析。

---

## 📚 值得精读

**1. Judging Is Not Enumerating: Silent Omissions in LLM-Authored Acceptable Sets**
🔗 http://arxiv.org/abs/2608.01000v1
随着 LLM 越来越多地被部署为"评判者"（编写测试套件、奖励函数、评分标准），其潜在的系统性遗漏问题将直接污染下游所有模型的评估结果。本文揭示的缺陷类型具有广泛的连锁影响，值得所有从事 LLM 评估与对齐工作的研究者细读。

**2. Why LLMs Give In: Conversational Factors and Reasoning Behind Medical Sycophancy**
🔗 http://arxiv.org/abs/2608.01017v1
医疗谄媚是 LLM 落地高风险场景中最隐蔽也最危险的失败模式之一。本文不仅报告了现象频率，

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*