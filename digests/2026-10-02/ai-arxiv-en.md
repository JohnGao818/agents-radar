# ArXiv AI Research Digest 2026-10-02

> Source: [ArXiv](https://arxiv.org/) (cs.AI, cs.CL, cs.LG) | 50 papers | Generated: 2026-10-02 03:49 UTC

---

# ArXiv AI Research Digest — 2026-10-01

## 1. Today's Highlights

Today's submissions are dominated by a coordinated push on **post-training efficiency and reliability**: new optimizers (TACO, SoftServe, ZFO, LoRA gain normalization) attack optimizer-state memory and step-size sensitivity, while several papers interrogate what RLVR and SFT actually do to a model's language, reasoning, and retention. A second cluster scrutinizes **agent infrastructure** — context compaction, non-destructive long-term memory, and new enterprise/security/tool-use benchmarks that expose false-positive evaluation. A third, quieter thread is **methodological skepticism**: work on self-repair, circuit-discovery objectives, and novelty judging suggests the field is increasingly auditing its own interpretability and evaluation claims. Finally, generative modeling advances span hierarchical continuous diffusion LMs, equivariant/3D generation, and chemistry-aware molecular representations.

---

## 2. Key Papers

### 🧠 Large Language Models

- **[Hierarchical Continuous Diffusion Language Models](http://arxiv.org/abs/2610.02193v1)** — H. Ren, Z. Li, C. Liu et al.
  Proposes hierarchical continuous diffusion to fix the independent-marginal sampling bottleneck of parallel decoding, potentially improving global-constraint satisfaction in non-autoregressive generation.

- **[Finetuning with Sampling: SFT Learns Better Than You Think](http://arxiv.org/abs/2610.02140v1)** — A. Karan, S. Chen, Y. Du
  Challenges the conventional wisdom that RL generalizes to new tasks better than SFT, with implications for how post-training budgets should be allocated.

- **[On Language Drift during RLVR Post-Training](http://arxiv.org/abs/2610.02015v1)** — M. Sullivan, A. Koller
  Documents systematic language degradation accompanying RLVR-driven reasoning gains — an important capability/faithfulness trade-off for reasoning models.

- **[From Gradients to Capabilities: Understanding Multi-Teacher On-Policy Distillation](http://arxiv.org/abs/2610.02179v1)** — S. Zhu, S. Huang, K. Zhang et al.
  Traces how individual RL-trained teacher signals map to parameter changes in a distilled student, moving multi-teacher distillation from heuristic to analysis-driven.

- **[The Missing Primitive: Diagnosing and Repairing Mathematical Reasoning in LLMs](http://arxiv.org/abs/2610.02191v1)** — S. Xing, Z. Dai, C. Qian et al.
  Separates surface-level answer accuracy from structural mathematical understanding, offering a diagnostic-and-repair protocol for reasoning failures.

- **[TACO: Ternary Absolute-max Column-wise One-sparse Optimizer for LLM Fine-Tuning](http://arxiv.org/abs/2610.02199v1)** — J. Jiang, C. McGee, E. H. Bergou et al.
  Compresses optimizer state to ternary, column-wise one-sparse form, targeting the memory wall that limits full-parameter fine-tuning on modern GPUs.

- **[Learn the Directions, Normalize the Gains: Post-Training Normalization for LoRA](http://arxiv.org/abs/2610.02067v1)** — Z. Tian, Y. Chen, Z. Han et al.
  Identifies "adaptation imbalance" in LoRA updates — a few dominant singular directions — and normalizes gains to preserve out-of-task capabilities.

### 🤖 Agents & Reasoning

- **[AutoCompact: Learning When to Compact Context in Long-Horizon Coding Agents](http://arxiv.org/abs/2610.02163v1)** — X. Zhang, L. Zheng, C. Du et al.
  Reframes context management as a learned decision of *when* and *what* to compact, rather than a fixed overflow-triggered heuristic for repository-scale coding.

- **[Mem++: Non-Destructive Memory for Long-Term Organizational LLM Agents](http://arxiv.org/abs/2610.02002v1)** — A. Yehia, A. O. Abdelkareem, I. Ahmed et al.
  Preserves versioned decisions across months of documents so agents can answer time-indexed questions instead of overwriting prior organizational memory.

- **[KaliBench: A Fine-Grained Benchmark for Cybersecurity Tool Use on Kali Linux with Runtime-Free Verifiable Rewards](http://arxiv.org/abs/2610.02206v1)** — P. Li, N. Suryanto, S. Zhang et al.
  Directly measures LLMs' ability to emit executable security tool commands with verifiable rewards, filling a gap between knowledge QA and end-to-end agentic tests.

- **[ScholarCatalyst: A Benchmark for Retrieving Papers That Inspire New Research](http://arxiv.org/abs/2610.02202v1)** — S. Kim, Y. Lee, B. Liu et al.
  Shifts retrieval evaluation from topical relevance to *inspiration* — which prior work a new problem actually needs — grounded in researchers' first-hand judgments.

- **[Keyword Harnesses Fail Open: A Cheap Diagnostic Ladder for Tool-Use Claims in Small Language Models](http://arxiv.org/abs/2610.02142v1)** — J. S. Santillana
  Documents a concrete false positive in keyword-matching tool-use benchmarks and supplies a cheap, strict diagnostic ladder to catch such failures.

### 🔧 Methods & Frameworks

- **[Every Ablation Is a Dose: Counterweights and the Semblance of Self-Repair](http://arxiv.org/abs/2610.02173v1)** — A. Ahmad, P. Seth, V. K. Sankarapu
  Argues apparent "self-repair" in ablated language models is largely a dose-response artifact of counterweights, challenging a widely cited mechanistic explanation.

- **[Are We Recovering Mechanisms? Objective-Level Recovery Gaps in Mechanistic Interpretability](http://arxiv.org/abs/2610.02098v1)** — C. Geng, L. Zhang, H. Ye et al.
  Shows that better scores on circuit-discovery objectives need not mean better mechanism recovery — a foundational caveat for automated interpretability.

- **[FERPO: Forward Entropy-Regularized Policy Optimization](http://arxiv.org/abs/2610.02198v1)** — S. Sanokowski, A. Sarmadi, M. Khadiv
  Targets the mismatch between accurate value predictions and accurate action *derivatives* in continuous-control critics, improving on-policy policy gradients.

- **[Embedding Prediction Helps Image Generation](http://arxiv.org/abs/2610.02203v1)** — S. Xu, J. Xie, Z. Wang et al.
  Introduces NEPA, replacing static per-step conditioning with predicted embeddings in diffusion transformers — a simple, transferable conditioning idea.

- **[Local Support Learning](http://arxiv.org/abs/2610.02126v1)** — A. Ben-Kish, A. Kumar, J. Glass et al.
  Reframes catastrophic forgetting geometrically in each weight matrix's input space and derives a retention objective that standard gradient updates handle suboptimally.

- **[When Do Intrinsic Rewards Lead to Exploration?](http://arxiv.org/abs/2610.02159v1)** — S. W. Viteri, L. Gomezjurado Gonzalez, C. Barrett
  Provides a formal criterion distinguishing intrinsic rewards that genuinely drive informative exploration from those merely maximized as objectives.

- **[Distributionally Robust Schrödinger Bridge](http://arxiv.org/abs/2610.02043v1)** — J. Sul, P. Theodoropoulos, V. Pacelli et al.
  Extends Schrödinger bridges to test-time shift in the initial distribution, learning transport dynamics that still recover the target under perturbation.

### 📊 Applications

- **[Where-OPD: Spatially Guided On-Policy Self-Distillation of MLLMs with Synthetic Scenes](http://arxiv.org/abs/2610.02117v1)** — S. Sirko-Galouchenko, M. Wysoczanska, A. Bursuc et al.
  Brings privileged-information self-distillation to multimodal models using synthetic scenes with known spatial ground truth, improving grounded reasoning.

- **[One Basis to Animate Them All: Gaussian Blendshape Distillation for Real-Time Avatars](http://arxiv.org/abs/2610.02207v1)** — R. Fazylov, S. Lefkimmiatis, I. Laptev
  Replaces costly neural inference in 3D Gaussian avatar animation with identity-independent blendshape bases, enabling genuinely real-time rendering.

- **[Generative modeling of intrinsically disordered protein regions by reinforcing sparse autoencoder features](http://arxiv.org/abs/2610.02189v1)** — J. X. Liu, S. Ibarraran, F. Hu et al.
  Applies sparse-autoencoder feature reinforcement to design IDRs, where structure-based protein design methods do not readily apply.

- **[Higher-Order Molecular Grammars for Generative and Foundation Models in Chemistry](http://arxiv.org/abs/2610.02186v1)** — Y. Huang, Y. Zeng, V. P. Dwivedi et al.
  Encodes ring systems and recurring motifs explicitly as higher-order grammars, addressing a representational blind spot of sequential and graph molecular formalisms.

- **[Controllable Multi-label Video Safety Detection via Adaptive Tversky Policy Optimization](http://arxiv.org/abs/2610.02019v1)** — G. Yang, J. Mei, M. Sun et al.
  Uses an adaptive Tversky-based objective to let operators tune the precision/recall trade-off in VLM-based harmful video detection.

- **[Foundations without Fundamentals: Zero-Shot Blind Spots in Time Series FMs](http://arxiv.org/abs/2610.02058v1)** — N. Ghoroghchian, H. Zhang, S. Han et al.
  Introduces SimpleTimeBench, a "unit test" suite revealing that time series foundation models fail basic temporal logic, especially with exogenous covariates.

---

## 3. Research Trend Signal

Three signals stand out from today's batch. First, **post-training is being re-litigated from first principles**: RLVR is shown to cause language drift, SFT is argued to generalize better than assumed, and multi-teacher distillation is analyzed at the gradient level. Second, **agent infrastructure is maturing from prompts to systems engineering** — learned context compaction, versioned non-destructive memory, and domain benchmarks (Kali Linux, enterprise data, paper retrieval) suggest the field is building the scaffolding that turns tool-using LLMs into deployable systems. Third, and most notably, **the field is auditing itself**: papers on self-repair artifacts, objective-level gaps in mechanistic interpretability, keyword-harness false positives, and novelty-judge instability all argue that headline metrics can systematically mislead. Optimization remains a live frontier too, with ternary optimizer states, quasi-Newton scaling, and decoupled direction/step selection all targeting the memory and stability limits of large-scale fine-tuning.

---

## 4. Worth Deep Reading

1. **[On Language Drift during RLVR Post-Training](http://arxiv.org/abs/2610.02015v1)** — If RLVR reliably degrades language quality while boosting reasoning, this affects essentially every reasoning-model deployment. The paper's framing of the capability/faithfulness trade-off deserves careful reading for anyone doing RL post-training.

2. **[Every Ablation Is a Dose: Counterweights and the Semblance of Self-Repair](http://arxiv.org/abs/2610.02173v1)** — A rare example of dismantling a popular mechanistic claim with a concrete alternative explanation. Read alongside **[Are We Recovering Mechanisms?](http://arxiv.org/abs/2610.02098v1)** for a paired methodological warning about interpretability evaluation.

3. **[Finetuning with Sampling: SFT Learns Better Than You Think](http://arxiv.org/abs/2610.02140v1)** — A direct challenge to the "RL generalizes, SFT memorizes" narrative that shapes most modern post-training pipelines; the theoretical framing and sampling-based argument are worth the full read.

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*