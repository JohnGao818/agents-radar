# ArXiv AI 研究日报 2026-06-25

> 数据来源: [ArXiv](https://arxiv.org/) (cs.AI, cs.CL, cs.LG) | 共 50 篇论文 | 生成时间: 2026-06-25 02:51 UTC

---

# ArXiv AI 研究日报 (2026-06-25)

## 今日速览

今日投稿聚焦于大语言模型（LLM）与智能体的安全性与可靠性，包括对抗性攻击的规避、安全对齐的量化评估、以及代理监控下的风险控制。同时，模型效率优化（LoRA迁移至强化学习策略库、位量化文本嵌入）和领域应用（医疗错误检测、工业化欧盟IT基准认证）也涌现出实用方案。此外，视频理解与语言模型的可解释性（稀疏自编码器联合训练、抑郁诊断的可解释模型）为多模态信任提供了新思路。

## 重点论文

### 🧠 大语言模型（架构、训练、对齐、评估）

1. **RAS: Measuring LLM Safety Through Refusal Alignment**  
   作者: Chang-Chieh Huang et al.  
   [链接](http://arxiv.org/abs/2606.25750v1)  
   一句话说明：提出基于拒绝对齐的LLM安全度量方法，避免依赖昂贵的人工标注，可直接评估模型对不安全输入的拒绝能力。

2. **OPERA: Aligning Open-Ended Reasoning via Objective Perplexity-based Reinforcement Learning**  
   作者: Wenxuan Jiang et al.  
   [链接](http://arxiv.org/abs/2606.25757v1)  
   一句话说明：用基于客观困惑度的RL方法对齐LLM在开放式任务（如创意写作）中的推理，缓解LLM-as-a-judge的偏见问题。

3. **BitNet Text Embeddings**  
   作者: Zhen Li et al.  
   [链接](http://arxiv.org/abs/2606.25674v1)  
   一句话说明：将LLM文本嵌入量化至1比特，大幅降低存储和带宽开销，同时保持检索和语义表示质量。

4. **SARA: Unlocking Multilingual Knowledge in Mixture-of-Experts via Semantically Anchored Routing Alignment**  
   作者: Tianyu Dong et al.  
   [链接](http://arxiv.org/abs/2606.25821v1)  
   一句话说明：针对稀疏MoE架构中低资源语言知识不足问题，提出语义锚定路由对齐，提升多语言性能。

### 🤖 智能体与推理（规划、工具使用、多智能体、思维链）

5. **AI Snitches Get Glitches: Towards Evading Agentic Surveillance**  
   作者: Hyejun Jeong et al.  
   [链接](http://arxiv.org/abs/2606.25836v1)  
   一句话说明：揭示AI代理在受监控环境中的安全风险，提出规避工具滥用的对抗方法，对隐私保护有警示意义。

6. **Beyond Function Calling: Benchmarking Tool-Using Agents under Tool-Environment Unreliability**  
   作者: Yang Tian et al.  
   [链接](http://arxiv.org/abs/2606.25819v1)  
   一句话说明：引入工具环境不可靠性（如调用失败、返回值错误），建立更真实代理评测基准。

7. **Semantic Consistency Policy Optimization for Reinforcement Learning of LLM Agents**  
   作者: Peng Xu et al.  
   [链接](http://arxiv.org/abs/2606.25852v1)  
   一句话说明：解决基于组的RL中语义相同步骤因轨迹结局不同而获得相反信用的问题，提出语义一致性策略优化。

8. **Confidence Sequences for Online Statistical Model Checking of Markov Decision Processes**  
   作者: Konstantin Kueffner et al.  
   [链接](http://arxiv.org/abs/2606.25797v1)  
   一句话说明：利用置信序列实现对MDP在线验证，无需假设已知概率，适用于自适应系统安全监控。

### 🔧 方法与框架（新技术、基准测试、效率优化）

9. **AutoRelAnnotator: Calibrated Model Cascades for Cost-Efficient Relevance Evaluation in Sponsored Search**  
   作者: Md Omar Faruk Rokon et al.  
   [链接](http://arxiv.org/abs/2606.25871v1)  
   一句话说明：利用校准模型级联替代人工标注，低成本生成高质量搜索相关性标注，对工业搜索系统有直接价值。

10. **Space-Efficient Language Generation in the Limit**  
    作者: Nicolas Flammarion et al.  
    [链接](http://arxiv.org/abs/2606.25777v1)  
    一句话说明：研究在空间效率约束下的语言生成极限学习理论，证明存在可学习但需线性空间的类，为小模型理论奠基。

11. **Memory-Efficient Policy Libraries with Low-Rank Adaptation in Reinforcement Learning**  
    作者: Samuel Valland Lyngset et al.  
    [链接](http://arxiv.org/abs/2606.25700v1)  
    一句话说明：将LoRA迁移至强化学习策略库，实现多任务策略的高效存储与微调，降低机器人部署内存成本。

12. **Is GraphRAG Needed? From Basic RAG to Graph-/Agentic Solutions with Context Optimization**  
    作者: Long Chen et al.  
    [链接](http://arxiv.org/abs/2606.25656v1)  
    一句话说明：系统对比普通RAG、GraphRAG、Modular RAG和Agentic RAG，提供基于半结构化知识库的选型框架。

### 📊 应用（垂直领域、多模态、代码生成）

13. **MedGuards: Multi-Agent System for Reliable Medical Error Detection and Correction**  
    作者: Congbo Ma et al.  
    [链接](http://arxiv.org/abs/2606.25651v1)  
    一句话说明：构建多智能体系统检测和纠正LLM生成的医疗文本错误，提升临床安全，针对现有方法覆盖率不足问题。

14. **Expresso-AI: Explainable Video-Based Deep Learning Models for Depression Diagnosis**  
    作者: Felipe Moreno et al.  
    [链接](http://arxiv.org/abs/2606.25606v1)  
    一句话说明：提出可解释视频深度学习模型用于抑郁诊断，结合面部动作、语音等特征，输出可视化解释，助力临床决策。

15. **Steering Vision-Language Models with Joint Sparse Autoencoders**  
    作者: Huizhen Shu et al.  
    [链接](http://arxiv.org/abs/2606.25657v1)  
    一句话说明：提出联合稀疏自编码器，从VLM中提取可控跨模态引导方向，实现图像生成或检索中的语义操控。

## 研究趋势信号

今日投稿凸显三个新兴方向：**模型级联与成本优化**（如 AutoRelAnnotator 的校准级联、BitNet 的1比特嵌入）成为大规模部署的关键；**智能体的安全与可审计性**（代理监控规避、工具环境不可靠性基准）从功能转向可靠性；**生成式因果与合成数据**（OncoSynth 合成肿瘤治疗数据保留因果关系）推动因果推断在隐私敏感领域的落地。此外，**稀疏MoE的多语言对齐**与**联合稀疏自编码器**表明，可解释性与效率正从纯语言向多模态扩展。

## 值得精读

1. **Beyond Function Calling: Benchmarking Tool-Using Agents under Tool-Environment Unreliability**  
   理由：首次系统引入工具环境不可靠性，填补现有代理评测盲区，对实际部署极具指导意义。

2. **RAS: Measuring LLM Safety Through Refusal Alignment**  
   理由：提出无需昂贵人工判断的安全度量，可自动化评估模型拒绝能力，对对齐研究有方法论贡献。

3. **Steering Vision-Language Models with Joint Sparse Autoencoders**  
   理由：开创性地将稀疏自编码器扩展至多模态，实现跨模态语义操控，为VLM可解释性提供新工具。

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*