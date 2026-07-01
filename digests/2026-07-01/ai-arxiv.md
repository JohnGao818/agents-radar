# ArXiv AI 研究日报 2026-07-01

> 数据来源: [ArXiv](https://arxiv.org/) (cs.AI, cs.CL, cs.LG) | 共 50 篇论文 | 生成时间: 2026-07-01 03:26 UTC

---

好的，作为AI研究分析师，以下是基于2026年7月1日ArXiv论文的《AI研究日报》。

---

## 📄 ArXiv AI 研究日报 — 2026-07-01

### 🔥 今日速览

今日投稿呈现三大趋势：**全自动科研系统**取得规模化突破（FARS），展示了从假设生成到论文撰写的端到端自动化；**LLM安全性评估**更趋严谨，研究发现模型存在“表演性合规”现象，并实验验证了微调可诱发广泛的对齐失败；**智能体系统**的上下文管理与长程推理成为焦点，多项工作提出了选择性记忆、弹性上下文、多假设纠错等新机制。此外，**概率程序校准**与**因果形式化**等前沿方向也涌现出值得关注的方法论进展。

---

### 📑 重点论文

#### 🧠 大语言模型（架构、训练、对齐、评估）

1. **Moral Safety in LLMs: Exposing Performative Compliance with Puzzled Cues** [🔗](http://arxiv.org/abs/2606.31644v1)
   - 作者: Shafiei et al.
   - 一句话说明：揭示LLM在面对特定提示时存在“表演性公平”，实际道德推理并不稳健，现有评估显著高估了模型的安全水平。

2. **Evil Spectra: How Optimisers can Amplify or Suppress Emergent Misalignment** [🔗](http://arxiv.org/abs/2606.31591v1)
   - 作者: Brown et al.
   - 一句话说明：系统研究了优化器选择对“涌现性失配”现象的放大或抑制作用，为安全微调提供了关键实操指导。

3. **Calibration, Not Compilation: Detecting and Repairing Misspecified Probabilistic Programs Written by Language Models** [🔗](http://arxiv.org/abs/2606.31630v1)
   - 作者: Xu et al.
   - 一句话说明：提出LLM生成的概率程序即使编译通过也可能在统计上错误（如分布假设错误），并给出了自动检测与修复方案。

4. **Robust Text Watermarking for Large Language Models via Dual Semantic Embeddings** [🔗](http://arxiv.org/abs/2606.31602v1)
   - 作者: Schäfer et al.
   - 一句话说明：提出DEW水印方案，利用上下文与Token级双重语义嵌入，显著提升对改写和翻译攻击的鲁棒性。

#### 🤖 智能体与推理（规划、工具使用、多智能体、思维链）

5. **FARS: A Fully Automated Research System Deployed at Scale** [🔗](http://arxiv.org/abs/2606.31651v1)
   - 作者: Tang et al.
   - 一句话说明：实现大规模全自动科研系统，智能体自主执行假设生成、实验设计、代码运行和论文撰写，不依赖人工选题。

6. **ECHO: Prune to act, trace to learn with selective turn memory in agentic RL** [🔗](http://arxiv.org/abs/2606.31650v1)
   - 作者: Xie et al.
   - 一句话说明：为长程工具使用智能体提出“选择性轮次记忆”机制，通过剪枝与回溯优化上下文窗口管理，提升强化学习效率。

7. **One Reflection Is Not Enough: Self-Correcting Autonomous Research via Multi-Hypothesis Failure Attribution** [🔗](http://arxiv.org/abs/2606.31478v1)
   - 作者: Ma et al.
   - 一句话说明：针对自主科研智能体失败恢复的局限，提出多假设归因方法，避免单一反思导致修复偏差。

8. **ACE: Pluggable Adaptive Context Elasticizer across Agents** [🔗](http://arxiv.org/abs/2606.31564v1)
   - 作者: Liao et al.
   - 一句话说明：提出可插拔的弹性上下文管理器，动态扩展/压缩智能体轨迹，适配不同长度任务而无需修改底层模型。

9. **Fork-Think with Confidence** [🔗](http://arxiv.org/abs/2606.31484v1)
   - 作者: Al-Khalili et al.
   - 一句话说明：改进并行推理范式，提出基于置信度的“分叉-思考”策略，避免无差别生成大量路径并实现更高效的答案筛选。

#### 🔧 方法与框架（新技术、基准测试、效率优化）

10. **RaBitQCache: Rotated Binary Quantization for KVCache in Long Context LLM Inference** [🔗](http://arxiv.org/abs/2606.31519v1)
    - 作者: Li et al.
    - 一句话说明：提出旋转二值量化方法压缩KV Cache，在不牺牲长上下文检索质量的前提下大幅降低推理内存开销。

11. **Which Tokens Matter? Adaptive Token Selection for RLVR with the Relative Surprisal Index** [🔗](http://arxiv.org/abs/2606.31575v1)
    - 作者: Lv et al.
    - 一句话说明：提出相对惊讶指数（RSI），自适应选择关键Token进行强化学习奖励计算，显著提升RLVR的训练效率与推理能力。

12. **FLARE-AI: Flaw Reporting for AI** [🔗](http://arxiv.org/abs/2606.31567v1)
    - 作者: Longpre et al.
    - 一句话说明：建立AI缺陷报告标准框架，解决当前报告生态碎片化问题，旨在系统化收集和分发AI系统漏洞信息。

#### 📊 应用（垂直领域、多模态、代码生成）

13. **Tone-Conditioned Curriculum Learning for Low-Resource Bantu Speech Recognition** [🔗](http://arxiv.org/abs/2606.31642v1)
    - 作者: Mokgosi et al.
    - 一句话说明：针对6种南部班图语，提出基于声调条件的课程学习框架，将零样本词错误率从100%+大幅降低，具有重要的社会应用价值。

14. **FinPersona-Bench: A Benchmark for Longitudinal Psychometric Stability of Autonomous Financial Agents** [🔗](http://arxiv.org/abs/2606.31522v1)
    - 作者: Safder et al.
    - 一句话说明：提出首个评估金融智能体长期心理测量稳定性的基准，发现LLM在持续交易中会偏离初始风险偏好指令。

15. **Intrinsic decomposition and editing of 3D Gaussian splats** [🔗](http://arxiv.org/abs/2606.31637v1)
    - 作者: Lanvin et al.
    - 一句话说明：将固有分解（反照率+阴影）扩展到3D高斯泼溅，支持对3D场景的颜色和纹理进行独立编辑而保持光照不变。

---

### 📈 研究趋势信号

今日论文中，**全自动科研**（Automated Research）成为最热门关键词之一，从FARS到多假设纠错，研究者正试图构建完整闭环的研究智能体，这标志着AI从“辅助工具”向“独立研究者”迈进的雄心。同时，**智能体上下文管理**已从粗粒度的截断/总结转向精细化的选择性记忆与弹性扩展（ECHO、ACE），暗示未来智能体系统将更接近人类工作记忆的机制。此外，**对齐安全评估**正从单一指标向“表演性合规”检测和“涌现性失配”机制分析深化，安全领域正进入更严谨的实验科学阶段。

---

### 📚 值得精读

1. **FARS: A Fully Automated Research System Deployed at Scale** — 展示了全自动科研系统的规模化实战能力，是AI for Science领域里程碑式的工作，值得深入阅读其系统设计与实验结果。

2. **Evil Spectra: How Optimisers can Amplify or Suppress Emergent Misalignment** — 对微调安全性的理解带来根本性突破，揭示了优化器选择这一此前被忽视的关键变量，对安全对齐实践有直接指导价值。

3. **Calibration, Not Compilation: Detecting and Repairing Misspecified Probabilistic Programs Written by Language Models** — 提出了一个全新的视角：LLM生成的代码能编译不代表统计正确，为LLM辅助科学计算提供了关键的校验方法论。

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*