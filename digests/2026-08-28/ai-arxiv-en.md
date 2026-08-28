# ArXiv AI Research Digest 2026-08-28

> Source: [ArXiv](https://arxiv.org/) (cs.AI, cs.CL, cs.LG) | 50 papers | Generated: 2026-08-28 08:47 UTC

---

# ArXiv AI Research Digest — 2026-08-28

## Today’s Highlights

Today’s submissions show a strong shift toward **inference-time and test-time methods** for improving LLM reasoning, including weak-to-strong generalization from small model failure modes and policy optimization without ground-truth labels. Agent research is moving from static tool-use toward **experience-driven skill evolution**, persistent knowledge accumulation, and auditable execution architectures. Several papers challenge existing evaluation paradigms: code-review benchmarks now target dynamic multi-turn workflows, while video world-model benchmarks demand probabilistic alignment rather than single plausible futures. Efficiency and data quality also remain central, with work on low-cost pretraining and filtering agent trajectories by supervision quality rather than task success.

## Key Papers

### 🧠 Large Language Models

- **CritICL: Inference-Time Weak-to-Strong Generalization from Small Language Model Failure Modes**  
  Yufan Wu et al. · [http://arxiv.org/abs/2608.27455v1](http://arxiv.org/abs/2608.27455v1)  
  Introduces an inference-time framework that leverages small-model failure modes to improve large-model reasoning without repeated generation or external verification.

- **TTPO: Test-Time Policy Optimization**  
  Aozhe Wang et al. · [http://arxiv.org/abs/2608.27448v1](http://arxiv.org/abs/2608.27448v1)  
  Extends test-time training to policy optimization, removing dependence on ground-truth labels and opening new post-training routes for mathematical reasoning.

- **Boosting LLM Exploration via Weak-Model Guidance in RLVR**  
  Xingyu Shen et al. · [http://arxiv.org/abs/2608.27420v1](http://arxiv.org/abs/2608.27420v1)  
  Uses weak-model guidance to counteract entropy collapse in reinforcement learning with verifiable rewards, improving pass@k for large k.

- **Understanding Evolution Strategies for LLM Reasoning: Broader Reasoning Coverage than GRPO**  
  Yunpeng Ba et al. · [http://arxiv.org/abs/2608.27351v1](http://arxiv.org/abs/2608.27351v1)  
  Provides a mechanistic comparison showing evolution strategies can yield broader reasoning coverage than GRPO, informing post-training algorithm choice.

### 🤖 Agents & Reasoning

- **WikiSkill: Compiling Agent Experience into Persistent Knowledge for Skill Evolution**  
  Liyan Tang et al. · [http://arxiv.org/abs/2608.27454v1](http://arxiv.org/abs/2608.27454v1)  
  Proposes persistent, wiki-like knowledge structures that let agents compile experience into reusable skills for progressive adaptation.

- **RedEvoAgent: Automatic Red-Teaming Agent with Experience-Driven Skill Evolution**  
  Junjie Zhang et al. · [http://arxiv.org/abs/2608.27439v1](http://arxiv.org/abs/2608.27439v1)  
  Combines red-teaming with skill evolution to discover jailbreaks that trigger harmful tool use in product-level agent harnesses.

- **What Makes Good Agentic Data? An ACE Lens on Data Generation for LLM Agents**  
  Xingshan Zeng et al. · [http://arxiv.org/abs/2608.27260v1](http://arxiv.org/abs/2608.27260v1)  
  Proposes an ACE (accuracy-consistency-effectiveness) framework for generating agent interaction data that is useful rather than merely abundant.

### 🔧 Methods & Frameworks

- **SWE-Prime: Fewer Trajectories, Better Performance**  
  Dewu Zheng et al. · [http://arxiv.org/abs/2608.27449v1](http://arxiv.org/abs/2608.27449v1)  
  Shows that filtering successful but low-quality agent trajectories can improve software-engineering LLM performance more than scaling up SFT data.

- **From Static to Dynamic: Benchmarking Real-World Code Review with MCR-Bench**  
  Dewu Zheng et al. · [http://arxiv.org/abs/2608.27442v1](http://arxiv.org/abs/2608.27442v1)  
  A benchmark that models iterative developer–reviewer interactions, moving code-review evaluation closer to real-world workflows.

- **PAWBench: How Far Are We from Probabilistically Aligned World Modeling?**  
  Yuandong Pu et al. · [http://arxiv.org/abs/2608.27345v1](http://arxiv.org/abs/2608.27345v1)  
  Evaluates whether video-generation world models reproduce the full distribution of possible futures, not just one plausible trajectory.

- **CLAP: Cross-Embodiment Video World Models are Zero-Shot Physical Simulators**  
  Kechen Liu, Ola Shorinwa · [http://arxiv.org/abs/2608.27406v1](http://arxiv.org/abs/2608.27406v1)  
  Learns action-conditioned video world models across heterogeneous embodiments, enabling zero-shot physical simulation for new robot morphologies.

- **Verify Smarter, Evolve Further: Efficient Harness Evolution through Behavior-Aware Verification**  
  Jinghan Xu et al. · [http://arxiv.org/abs/2608.27311v1](http://arxiv.org/abs/2608.27311v1)  
  Reduces verification cost in agent-harness evolution by scoring candidates only on behaviors relevant to the proposed changes.

### 📊 Applications

- **CorporateBench: Large-Scale Q&A Benchmarking with Temporal Knowledge Bases**  
  Sil Hamilton et al. · [http://arxiv.org/abs/2608.27391v1](http://arxiv.org/abs/2608.27391v1)  
  A human-validated, enterprise-scale Q&A benchmark with temporal knowledge bases, targeting realistic LLM use over internal document collections.

- **LLMs Can Design Near-Optimal OR Algorithms**  
  Jackie Baek · [http://arxiv.org/abs/2608.27296v1](http://arxiv.org/abs/2608.27296v1)  
  Demonstrates that LLMs can produce near-optimal algorithms for inventory control, queueing network control, and assortment optimization.

- **MM-Spectrum: Multimodal Multi-spectral Molecular Structural Elucidation with a Stable MoE Framework**  
  Hai-tao Yu et al. · [http://arxiv.org/abs/2608.27286v1](http://arxiv.org/abs/2608.27286v1)  
  Uses a stable mixture-of-experts framework to integrate heterogeneous spectroscopic signals for molecular structure inference.

## Research Trend Signal

A clear trend is the move beyond “more RLVR” toward **exploration control and label-free test-time adaptation**: weak-model guidance, evolution strategies, and test-time policy optimization all address reasoning diversity and supervision bottlenecks. Agent papers increasingly emphasize **persistent skill memory and execution auditability**, reflecting real-world deployment concerns. Evaluation is also becoming more behaviorally grounded—code review benchmarks embrace multi-turn interaction, and world-model benchmarks demand probabilistic output alignment. Across topics, data quality is overtaking data volume: SWE-Prime and agentic-data frameworks argue that carefully filtered or structured experience beats indiscriminate scaling. Finally, low-cost pretraining and efficient verification signal growing pressure to make advanced AI research more accessible and sustainable.

## Worth Deep Reading

1. **CritICL** ([http://arxiv.org/abs/2608.27455v1](http://arxiv.org/abs/2608.27455v1)) — A novel inference-time paradigm that turns small-model failure modes into weak-to-strong supervision signals, potentially reducing reliance on external verifiers in reasoning tasks.

2. **SWE-Prime** ([http://arxiv.org/abs/2608.27449v1](http://arxiv.org/abs/2608.27449v1)) — Directly challenges the assumption that successful trajectories are high-quality supervision; its trajectory-filtering insight may reshape SFT pipelines for agentic coding models.

3. **PAWBench** ([http://arxiv.org/abs/2608.27345v1](http://arxiv.org/abs/2608.27345v1)) — Important for grounding the “video generation as world model” claim in probabilistic evaluation, with direct implications for robotics and simulation.

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*