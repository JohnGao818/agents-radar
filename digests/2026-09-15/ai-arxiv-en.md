# ArXiv AI Research Digest 2026-09-15

> Source: [ArXiv](https://arxiv.org/) (cs.AI, cs.CL, cs.LG) | 50 papers | Generated: 2026-09-15 03:09 UTC

---

# ArXiv AI Research Digest — 2026-09-15

## 1. Today's Highlights

Today's submissions cluster around three converging pressures on large language models. First, **recursive self-improvement** has matured from a slogan into concrete, training-free architectures (RSIAgent, Dream-RSI, ModularRSI), all built around persistent experience mining and reusable harnesses rather than weight updates. Second, **agentic evaluation is being audited rather than trusted**: multiple papers show clean benchmark scores can mask buried-evidence failures, citation-allocation bias, and instruction-following drift in long-horizon coding sessions. Third, **inference efficiency research has shifted** from generic token-level tricks toward phase-aware, module-aware and semantic-level interventions (AgentKV, DSEI, MoME, MoARa). Running alongside all of this is a distinctly skeptical thread questioning benchmark validity itself — fairness suites passable with a single example, synthetic-user simulations that only reproduce population averages, and biomedical references that remain unreliable across 26 models.

---

## 2. Key Papers

### 🧠 Large Language Models (architecture, training, alignment, evaluation)

**1. [Temperature Fragility and the Conditional Benefits of Truncation Sampling](http://arxiv.org/abs/2609.15476v1)**
*F. La Rosa*
Shows that temperature sensitivity is highly non-uniform and that truncation samplers such as top-p and min-p help only under specific distributional conditions, giving practitioners a principled basis for choosing decoding hyperparameters.

**2. [When the Wrong Key Wins: Understanding and Detecting Hallucinations in LLMs](http://arxiv.org/abs/2609.15106v1)**
*X. Tong, J. Zhang*
Attributes hallucination to competition among pretraining associations in a latent-key view of inference, offering a mechanistic explanation and a detection signal for cases where the model "knows" the right answer but selects the wrong association.

**3. [DA-DLM: Explicitly Modeling Token Dependencies in Diffusion Language Models](http://arxiv.org/abs/2609.15070v1)**
*P. Ji, Z. Zhang, X. Hu et al.*
Tackles the conditional-independence flaw in masked diffusion decoding — the analogue of the multi-modality problem in NAR translation — to improve coherence in parallel text generation.

**4. [MoME: Mixture-of-Memory Embeddings for Context-Aware Sparse Lookup](http://arxiv.org/abs/2609.15126v1)**
*M. Li, L. Sigal, R. Liao*
Replaces deterministic token-indexed memory retrieval with a mixture-of-memory formulation, making conditional-memory layers genuinely context-sensitive at low parametric cost.

**5. [MoARa: Module-Aware Rank Allocation and Structure-Preserving Decomposition for Low-Rank LLM Pre-training](http://arxiv.org/abs/2609.15037v1)**
*K. Kim, N. Kwak*
Improves low-rank gradient projection by allocating rank per module and preserving structure, reducing both optimizer memory and wall-clock time to target quality in LLM pretraining.

**6. [Forty Shades of Blue: Quality-Diversity Alignment via Mode-Conditioned Reinforcement Learning](http://arxiv.org/abs/2609.14896v1)**
*J. Yuan, H. Kang, J. J. Liu et al.*
Directly attacks alignment-induced mode collapse by conditioning RL on explicit quality-diversity modes, restoring output plurality without sacrificing preference alignment.

**7. [One Example Is Enough to Pass Fairness Benchmarks: Rethinking Fairness Evaluation for Aligned LLMs](http://arxiv.org/abs/2609.14860v1)**
*N. Deng, S. Arif, S. Chang et al.*
Demonstrates that BBQ-style fairness benchmarks are too easy and can be passed with minimal signal, calling into question a de facto standard of fairness evaluation.

---

### 🤖 Agents & Reasoning (planning, tool use, multi-agent, chain-of-thought)

**8. [RSIAgent: Autonomous Exploration for Recursive Self-improvement in New Environments](http://arxiv.org/abs/2609.15364v1)**
*S. Zhu, S. Fan, X. Wang et al.*
A training-free multi-agent framework that builds persistent memory while exploring unfamiliar interfaces and tools, enabling recursive self-improvement without gradient updates.

**9. [Dream-RSI: Recursive Self-Improvement through Evolving Worlds](http://arxiv.org/abs/2609.14858v1)**
*T. Zheng, X. Wu, Z. Zhang et al.*
Frames exploration-strategy improvement as the core bottleneck of recursive self-improvement and proposes evolving synthetic worlds as the driver of high-value solution discovery.

**10. [ModularRSI: Modular and Generalizable Recursive Harness Self-Improvement](http://arxiv.org/abs/2609.14857v1)**
*S. Wu, J. Ren, Y. Li et al.*
Extends RSI to agent harnesses for long-horizon coding and terminal tasks while explicitly addressing overfitting to evaluation benchmarks — the key obstacle to generalizable harness evolution.

**11. [Clean Scores, Buried Evidence, and Confident Wrong: A Receipt-Based Audit of Frontier Agentic QA](http://arxiv.org/abs/2609.15319v1)**
*L. M. Sánchez*
A controlled data-room audit showing that moving evidence into buried conditions sharply degrades accuracy, inflates forced declarations and tool calls, and raises cost per correct answer — even when confidence calibration looks fine.

**12. [CITECHOICE: A Causal Audit of How Document Presentation Redistributes Citation Credit in Agentic Search](http://arxiv.org/abs/2609.15164v1)**
*S. Selvam, A. Ghosh*
Provides causal evidence that presentation order and formatting redistribute citation credit among equally supporting sources in agentic search, with implications for attribution fairness.

**13. [EMR: Self-Evolving Medical Multi-Agent System via Experience Mining and Reuse](http://arxiv.org/abs/2609.15161v1)**
*D. Shi, Y. Li, X. Yi et al.*
Adds persistent clinical memory and experience reuse to LLM multi-agent diagnosis, moving medical agents beyond static strategies toward self-evolution from prior successes and failures.

**14. [MTAC-IFBench: Benchmarking Instruction-Following in Multi-Turn Agentic Coding](http://arxiv.org/abs/2609.14992v1)**
*B. Wen, C. Wang, J. Gui et al.*
Shifts agentic coding evaluation beyond functional correctness to process-faithful instruction adherence across multi-turn tool-using sessions.

**15. [When Agents Slow Down: Understanding LLM Agents' Test-Time Strategies via Elo-per-token Analysis](http://arxiv.org/abs/2609.15309v1)**
*K. Liu, Q. Mang, B. Peng et al.*
Introduces Elo-per-token, a normalized metric for how agent performance scales with test-time compute, revealing when revision, tool use and exploration actually pay off.

---

### 🔧 Methods & Frameworks (new techniques, benchmarks, efficiency improvements)

**16. [Dynamic Semantic Compression for Efficient Latent-Space Inference in Large Language Models](http://arxiv.org/abs/2609.15338v1)**
*P. Li, D. Zhang, Y. Liu et al.*
The DSEI framework performs segment-level rather than token-level inference in latent space, targeting the memory and compute overhead that dominates production LLM serving.

**17. [AgentKV: Phase-Aware KV Eviction for Agentic LLMs](http://arxiv.org/abs/2609.14872v1)**
*T. T. Liu, J. T. H. Wong, C. Xiao et al.*
Challenges the "recent attention predicts future attention" assumption in KV eviction, replacing it with phase-aware scoring tuned to agentic workloads that consume orders of magnitude more tokens than chat.

**18. [Self-Orchestrating Language Models: Leveraging Semantic Dependence for Efficient Inference](http://arxiv.org/abs/2609.14850v1)**
*T. Jin*
Exploits semantic dependence between generation steps to orchestrate autoregressive and diffusion-style decoding, addressing latency and accelerator under-utilization at low batch sizes.

**19. [ABSOL: Aggregated Bayesian Subsampling Orchestrated with LLMs](http://arxiv.org/abs/2609.15007v1)**
*J. Hassell, C. Shen, E. Hruschka*
Couples LLM natural-language interfaces with explicit Bayesian networks to supply the consistent evidence conditioning, dependency-aware reasoning and uncertainty estimates LLMs lack on structured data.

**20. [MarKey: Marginal Utility Guided Greedy Keyframe Selection for Long Video Understanding](http://arxiv.org/abs/2609.15408v1)**
*H. Shi, J. Hu, A. Wang et al.*
A training-free keyframe selector that maximizes marginal information gain under a fixed visual budget, recovering sparse decisive evidence that uniform sampling misses in long-video MLLM tasks.

**21. [PACE: Progressive Angular-to-Norm Contrastive Embedding](http://arxiv.org/abs/2609.15152v1)**
*Y. Li, W. Zhou, Y. Liu et al.*
Extends cosine-based multimodal contrastive objectives beyond angular similarity by progressively incorporating norm information, broadening semantic compatibility across modalities.

**22. [Not All Prompts Are Equal: Exploration-Guided Prompt Scaffolding for Multimodal Reinforcement Post-Training](http://arxiv.org/abs/2609.15051v1)**
*Y. Yue, Q. Ma, C. Wang et al.*
Reallocates rollout budget away from saturated and hopelessly hard prompts toward those with genuine learning signal, improving online RL post-training efficiency.

---

### 📊 Applications (domain-specific, multimodal, code generation)

**23. [Biomedical Reference Generation Remains Unreliable across 26 Large Language Models](http://arxiv.org/abs/2609.14988v1)**
*M. Topaz, Z. Zhang, N. Roguin et al.*
A systematic audit across eight developers (2023–2026) quantifying how often LLMs fabricate references to nonexistent biomedical work — a directly actionable finding for scientific writing pipelines.

**24. [SALUTE: Benchmarking and Adapting LLMs for the Defense Domain](http://arxiv.org/abs/2609.15022v1)**
*H. Park, S. In, S. Myeong et al.*
Consolidates fragmented military-NLP efforts into a unified benchmark covering doctrine, terminology and evolving operational events, with domain-adaptation recipes.

**25. [Typhoon ASR Streaming: Steerable Low-Latency Thai Speech Recognition with Real-Time Shallow Fusion](http://arxiv.org/abs/2609.14991v1)**
*W. Sirichotedumrong, T. Samutsin, S. F. Wani et al.*
Delivers a deployable streaming Thai ASR system with user-steerable vocabulary, breaking the offline Whisper monopoly in a low-resource, latency-sensitive language.

**26. [PeerPen: AI-Assisted Writing for Online Mental Health Peer Support](http://arxiv.org/abs/2609.14886v1)**
*J. Kim, S. Gong, M. Ajit et al.*
Studies AI co-writing for untrained peer supporters, probing the tension between lowering the barrier to helping and preserving the perceived personal authenticity that gives peer support its value.

**27. [Enemray: Toward Capable Language Models for Hassaniya](http://arxiv.org/abs/2609.14829v1)**
*C. Ahmed*
Trains a Hassaniya-centric model under an explicit stability–plasticity objective, preserving general reasoning and instruction-following while acquiring competence in an extremely low-resource language.

---

## 3. Research Trend Signal

Three signals stand out. **Recursive self-improvement is consolidating into a subfield**: RSIAgent, Dream-RSI and ModularRSI independently converge on training-free, memory- or harness-centric evolution, which suggests the field is moving past "self-improving weights" toward inspectable, persistent agent state. **Agentic evaluation is becoming forensic**: audits of buried evidence, citation allocation and multi-turn instruction drift all show that headline scores conceal failure modes that only appear under realistic adversarial conditions — a maturation from capability benchmarking to reliability auditing. **Efficiency work is going conditional and phase-aware**: KV eviction keyed to agent phase, memory retrieval keyed to context, rank allocation keyed to module, and sampling truncation keyed to distribution shape all reject one-size-fits-all heuristics. Finally, a shared skeptical posture toward benchmarks (fairness, synthetic users, irreproducible references) suggests that 2026's contribution may be less about new capabilities than about knowing which claims survive scrutiny.

---

## 4. Worth Deep Reading

**1. [Clean Scores, Buried Evidence, and Confident Wrong: A Receipt-Based Audit of Frontier Agentic QA](http://arxiv.org/abs/2609.15319v1)** — This is the paper most likely to change how teams report agent performance. It does not propose a method; it dismantles a measurement assumption, showing that accuracy, confidence calibration and cost all degrade in ways that benchmark suites cannot see. Anyone deploying retrieval-augmented agents should read this before their next evaluation report.

**2

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*