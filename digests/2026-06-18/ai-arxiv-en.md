# ArXiv AI Research Digest 2026-06-18

> Source: [ArXiv](https://arxiv.org/) (cs.AI, cs.CL, cs.LG) | 50 papers | Generated: 2026-06-18 03:33 UTC

---

# ArXiv AI Research Digest — June 17, 2026

## Today's Highlights

A dominant theme across today's submissions is the push to embed reinforcement learning signals—particularly verifiable rewards—into the post-training of reasoning models, with several papers tackling the resulting entropy collapse and collateral forgetting problems. On the architecture frontier, block diffusion language models are making serious inroads into chain-of-thought reasoning, challenging the auto-regressive monopoly on formal theorem proving. Multi-agent systems continue to mature, with work on fictitious play for LLM-based decision-making and neurosymbolic frameworks that unify disparate semantics under categorical structures. Meanwhile, domain-specific benchmarks—from legal ordinances to preclinical pharmacology—signal that the field is moving beyond general-purpose evaluation into high-stakes, verifiable application spaces. Finally, a cluster of papers on machine unlearning and selective forgetting suggests growing concern about data removal, safety alignment, and the unintended persistence of learned behaviors.

---

## Key Papers

### 🧠 Large Language Models (architecture, training, alignment, evaluation)

**Rethinking Reward Supervision: Rubric-Conditioned Self-Distillation**
Siyi Gu et al. | http://arxiv.org/abs/2606.19327v1
Introduces rubric-conditioned self-distillation to replace expensive chain-of-thought annotations with structured rubric signals for post-training reasoning models, reducing reliance on noisy distillation data.

**STARE: Surprisal-Guided Token-Level Advantage Reweighting for Policy Entropy Stability**
Haipeng Luo et al. | http://arxiv.org/abs/2606.19236v1
Diagnoses entropy collapse in GRPO-based RLVR training of LLMs and proposes surprisal-guided advantage reweighting to stabilize token-level policy entropy during complex reasoning.

**DreamReasoner-8B: Block-Size Curriculum Learning for Diffusion Reasoning Models**
Zirui Wu et al. | http://arxiv.org/abs/2606.19257v1
Demonstrates that block diffusion language models can be reliably scaled for long chain-of-thought reasoning through a curriculum that progressively increases denoising block sizes.

**Beyond Safe Data: Pretraining-Stage Alignment with Regular Safety Reflection**
Jinhan Li et al. | http://arxiv.org/abs/2606.19168v1
Argues that pretraining-stage safety alignment should go beyond data filtering, proposing a reflection mechanism that internalizes safety norms during pretraining rather than solely at instruction-tuning time.

**Trade-offs in Medical LLM Adaptation: An Empirical Study in French QA**
Ikram Belmadani et al. | http://arxiv.org/abs/2606.19266v1
Systematically evaluates medical domain adaptation strategies for French QA, revealing that effectiveness depends critically on the interplay between base model choice, fine-tuning data, and language-specific factors.

---

### 🤖 Agents & Reasoning (planning, tool use, multi-agent, chain-of-thought)

**Enhancing Decision-Making with Large Language Models through Multi-Agent Fictitious Play**
Leyang Shen et al. | http://arxiv.org/abs/2606.19308v1
Applies fictitious play dynamics to LLM-based multi-agent systems, enabling them to handle decision-making tasks beyond simple divide-and-conquer by coordinating through iterative belief updates.

**Diffusion-Proof: Recipe for Formal Theorem Proving Beyond Auto-Regressive Generation**
Ruida Wang et al. | http://arxiv.org/abs/2606.19315v1
Proposes diffusion-based formal theorem proving that overcomes the sequential bottleneck of auto-regressive LLMs, achieving non-autoregressive proof generation with competitive accuracy.

**User as Engram: Internalizing Per-User Memory as Local Parametric Edits**
Bojie Li | http://arxiv.org/abs/2606.19172v1
Draws inspiration from hippocampal engrams to separate per-user episodic memory from shared reasoning skills, enabling personalization through localized parametric edits rather than context window stuffing.

**Native Active Perception as Reasoning for Omni-Modal Understanding**
Zhenghao Xing et al. | http://arxiv.org/abs/2606.19341v1
Replaces the "watch-it-all" paradigm for long video understanding with a query-driven active perception framework that reasons about which frames to attend to, dramatically reducing computational cost.

**Data Intelligence Agents: Interpreting, Modeling, and Querying Enterprise Data via Autonomous Coding Agents**
Anoushka Vyas et al. | http://arxiv.org/abs/2606.19319v1
Introduces a three-agent system (Interpreter, Schema Creator, Query Agent) that automates the discovery, structuring, and querying of enterprise data, replacing repeated human handoffs in production data integration.

---

### 🔧 Methods & Frameworks (new techniques, benchmarks, efficiency improvements)

**A Multi-Domain Benchmark for Detecting AI-Generated Text-Rich Images from GPT-Image-2**
Yijin Wang et al. | http://arxiv.org/abs/2606.19259v1
Provides the first systematic benchmark for detecting AI-generated images with embedded text, covering privacy-sensitive domains like documents, receipts, and UI screenshots.

**Freeing the Law with LOCUS: A Local Ordinance Corpus for the United States**
Denis Peskoff et al. | http://arxiv.org/abs/2606.19334v1
Releases a large-scale corpus of U.S. local ordinances, filling a critical gap in legal AI resources and enabling work on zoning, housing, and public health law at municipal scale.

**Mechanism-Guided Selective Unlearning for RLVR-Induced Reasoning**
Chenyu Zhou et al. | http://arxiv.org/abs/2606.19222v1
Proposes MAST, a targeted unlearning method that removes RLVR-induced reasoning behaviors from LLMs with substantially less collateral damage than full-parameter updates.

**Essential Subspace Merging for Multi-Task Learning**
Longhua Li et al. | http://arxiv.org/abs/2606.19164v1
Analyses output shifts in model merging and introduces essential subspace merging to reduce inter-task interference when combining multiple fine-tuned models into one.

**Explaining Attention with Program Synthesis**
Amiri Hayes et al. | http://arxiv.org/abs/2606.19317v1
Replaces opaque attention head computations with executable symbolic programs, producing human-readable explanations of what individual attention heads compute.

---

### 📊 Applications (domain-specific, multimodal, code generation)

**Does VLA Even Know the Basics? Measuring Commonsense and World Knowledge Retention in Vision-Language-Action Models**
Nikita Kachaev et al. | http://arxiv.org/abs/2606.19297v1
Benchmarks how much commonsense and factual knowledge embodied VLA models retain after robotics fine-tuning, revealing significant forgetting that conflates missing knowledge with task-specific failures.

**TxBench-PP: Analyzing AI Agent Performance on Small-Molecule Preclinical Pharmacology**
Hannah Le et al. | http://arxiv.org/abs/2606.19245v1
Introduces a verifiable benchmark for AI agents in drug discovery, testing their ability to make realistic preclinical pharmacology decisions on small-molecule candidates.

**A Clinician-Centered Pipeline for Annotation and Evaluation in Ultrasound AI Studies**
Fangyijie Wang et al. | http://arxiv.org/abs/2606.19174v1
Designs a pipeline that puts clinician evaluation at the center of ultrasound AI validation, supporting blinded model comparisons that go beyond quantitative metrics.

**Language Models as Interfaces, Not Oracles: A Hybrid LLM-ML System for Pediatric Appendicitis**
Soheyl Bateni et al. | http://arxiv.org/abs/2606.19183v1
Positions LLMs as natural-language interfaces to structured ML models rather than diagnostic engines themselves, demonstrating improved robustness for pediatric appendicitis prediction.

---

## Research Trend Signal

A striking pattern in today's submissions is the convergence of reinforcement learning and diffusion-based architectures for reasoning. While RLVR methods (STARE, MAST) are becoming the dominant post-training paradigm for LLMs, the field is already confronting their pathologies—entropy collapse, reward hacking, and the difficulty of selective forgetting. Simultaneously, diffusion models are emerging as a serious alternative to auto-regressive decoding for formal reasoning tasks (DreamReasoner, Diffusion-Proof), suggesting a potential bifurcation: auto-regressive models for open-ended generation, diffusion models for structured, verifiable reasoning chains. Another visible signal is the maturation of domain-specific, verifiable benchmarks (LOCUS, TxBench-PP, the GPT-Image-2 detection benchmark, pediatric appendicitis). These move the field beyond general-purpose leaderboards toward high-stakes applications where correctness is not just desirable but auditable. Finally, safety and unlearning are co-evolving: mechanism-guided selective unlearning (MAST) and pretraining-stage safety reflection (Beyond Safe Data) indicate a shift from reactive safety patching to proactive, architecturally grounded alignment.

---

## Worth Deep Reading

1. **STARE: Surprisal-Guided Token-Level Advantage Reweighting for Policy Entropy Stability** (http://arxiv.org/abs/2606.19236v1) — Essential reading for anyone working on RL-based post-training of LLMs. The paper provides a rigorous first-order gradient analysis of entropy collapse under GRPO and offers a principled, lightweight fix. The implications extend to any verifiable-reward training pipeline.

2. **Diffusion-Proof: Recipe for Formal Theorem Proving Beyond Auto-Regressive Generation** (http://arxiv.org/abs/2606.19315v1) — A potentially paradigm-shifting paper that demonstrates diffusion models can compete with auto-regressive LLMs on formal math reasoning. The non-autoregressive approach could solve the sequential bottleneck that limits theorem proving at scale, and the architecture insights are transferable to other structured reasoning domains.

3. **Freeing the Law with LOCUS: A Local Ordinance Corpus for the United States** (http://arxiv.org/abs/2606.19334v1) — While less technically flashy, this paper fills a profound data gap in legal AI. Local ordinances govern zoning, housing, and public health but have been essentially invisible to NLP. The corpus and its release methodology will likely become a standard resource, and the paper's analysis of what makes municipal legal text challenging is valuable for domain adaptation research.

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*