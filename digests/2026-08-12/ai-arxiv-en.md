# ArXiv AI Research Digest 2026-08-12

> Source: [ArXiv](https://arxiv.org/) (cs.AI, cs.CL, cs.LG) | 50 papers | Generated: 2026-08-12 03:01 UTC

---

# ArXiv AI Research Digest — 2026-08-12

## 1. Today's Highlights

Today's submissions reveal three dominant threads. First, **cross-lingual generalization** emerges as a critical weak point: studies show safety misalignment in low-resource languages, dropped policy-retention in multilingual tool-using agents, and inconsistent text-to-image generation across languages. Second, the field is moving **beyond frozen deployment** toward test-time adaptation and self-evolving systems — exemplified by GUI grounding that refines itself during inference, skill-compressing agents, and a world-action model for surgical robotics. Third, **mechanistic interpretability and verification** are converging on actionable control: sparse autoencoder instability, attention-path uncertainty signals, data attribution of emergent misalignment, and polynomial-time consistency verification for probabilistic predictors. Notably, the Grothendieck constant case study demonstrates how long-horizon human-AI collaboration can produce publishable mathematical results.

## 2. Key Papers

### 🧠 Large Language Models

- **The Illusion of Cross-Lingual Safety in Low-Resource Languages** — [http://arxiv.org/abs/2608.11146v1](http://arxiv.org/abs/2608.11146v1) — Abigail Oppong, P Sam Sahil, Tadesse Destaw Belay et al.
  Shows that English-centric safety alignment does not transfer to low-resource languages, exposing a critical multilingual vulnerability.

- **Attention-Path Fragility as an Uncertainty Signal in Large Language Models** — [http://arxiv.org/abs/2608.11138v1](http://arxiv.org/abs/2608.11138v1) — Minsoo Kim, Sungyoung Ji, Kisung Moon et al.
  Proposes ASMI, a training-free uncertainty signal based on whether a confident prediction collapses under attention-subnetwork perturbation.

- **ReRound: Reconstructive Rounding to Resolve Midpoint Ambiguity in Calibration-Free LLM Quantization** — [http://arxiv.org/abs/2608.11045v1](http://arxiv.org/abs/2608.11045v1) — He-Yen Hsieh, H. T. Kung
  Uses a conditional diffusion model to resolve quantization midpoint ambiguity, achieving calibration-free post-training quantization.

- **Mapping and Measuring the Behavioral Evolution of Large Language Models** — [http://arxiv.org/abs/2608.11027v1](http://arxiv.org/abs/2608.11027v1) — Dong Qiao, Chris Ding, Jicong Fan
  Characterizes output behavior of 32 models across six families on 10,000 prompts, providing a behavioral-dynamics complement to benchmark leaderboards.

- **Data Attribution of Emergent Misalignment with Persona Features** — [http://arxiv.org/abs/2608.11025v1](http://arxiv.org/abs/2608.11025v1) — Clemens Vetter, David Kaczér, Lucie Flek et al.
  Attributes harmful fine-tuning side effects to pre-trained persona features, offering a data-level account of emergent misalignment.

### 🤖 Agents & Reasoning

- **Surgical WAM: A World-Action Model for Data-Efficient Surgical Robot Learning** — [http://arxiv.org/abs/2608.11204v1](http://arxiv.org/abs/2608.11204v1) — Wenrui Bao, Tianyun Jiang, Zhiben Chen et al.
  Introduces a world-action model that fuses forward dynamics with action prediction, dramatically reducing the action-labeled demonstrations needed for surgical manipulation policies.

- **Long-Horizon AI Research for Grothendieck Constant: A Case Study in Human-AI Mathematical Collaboration** — [http://arxiv.org/abs/2608.11195v1](http://arxiv.org/abs/2608.11195v1) — Alan Li, Rahul Saha, Anton Xue et al.
  Documents a full case study of AI-assisted improvement of bounds on the Grothendieck constant, offering a rare blueprint for long-horizon AI use in mathematics.

- **Actions Speak Louder than Words: Measuring Cross-Lingual Policy Retention in Tool-Using Agents** — [http://arxiv.org/abs/2608.11110v1](http://arxiv.org/abs/2608.11110v1) — Sourabrata Mukherjee, Kalika Bali, Sunayana Sitaram
  Evaluates whether tool-using agents execute the same action steps across languages, showing that final-answer metrics mask substantial policy divergence.

### 🔧 Methods & Frameworks

- **How to Verify Consistency of Probabilistic Claims** — [http://arxiv.org/abs/2608.11181v1](http://arxiv.org/abs/2608.11181v1) — Orr Paradise, Oliver Richardson, Yoshua Bengio et al.
  Proves that self-consistency of a probabilistic predictor's conditional-probability answers can be verified in polynomial time, with direct AI-safety implications.

- **Beyond a Bag of Features: Set-Level Instability in Sparse Autoencoders** — [http://arxiv.org/abs/2608.11197v1](http://arxiv.org/abs/2608.11197v1) — Nikolai Bolik, Lennart Stöpler, Artur Andrzejak
  Demonstrates that sparse autoencoder feature sets are unstable across seeds, challenging the reliability of SAE-based interpretability analyses.

- **From Interpretability to Control: Insights from Six Years of the TrustNLP Workshop** — [http://arxiv.org/abs/2608.11171v1](http://arxiv.org/abs/2608.11171v1) — Rahul Gupta, Abhinav Mohanty, Anaelia Ovalle et al.
  Synthesizes six editions of TrustNLP, documenting the field's shift from post-hoc interpretability to mechanistic understanding and proactive control.

### 📊 Applications

- **MultiModal Code-Switching: Interleaving Visual Objects into Language for Explicit Object-Level Alignment** — [http://arxiv.org/abs/2608.11167v1](http://arxiv.org/abs/2608.11167v1) — Changhao Xiang, Shangyu Xing, Zhen Wu et al.
  Interleaves visual objects directly into text sequences to resolve referential ambiguity in MLLM pretraining, enabling explicit object-level alignment.

- **Test-Time Self-Evolving GUI Visual Grounding via Reflection-Guided On-Policy Self-Distillation** — [http://arxiv.org/abs/2608.11191v1](http://arxiv.org/abs/2608.11191v1) — Shiyu Xuan, Zechao Li
  Lets GUI grounding models adapt to unseen interfaces at test time via reflection-guided self-distillation, without parameter freezing after deployment.

- **V-FiLLM: Verified Financial LLM Reasoning Benchmark** — [http://arxiv.org/abs/2608.11047v1](http://arxiv.org/abs/2608.11047v1) — Alicia Larsen, Victoire Laurent, Aulia Kharis Rakhamsari et al.
  Generates financial reasoning benchmarks from executable computation trees, providing machine-verifiable ground truth for structured-data financial QA.

- **On the Limitations of Cross-Lingual Consistency in Multilingual Text-to-image Generation** — [http://arxiv.org/abs/2608.11002v1](http://arxiv.org/abs/2608.11002v1) — Sicheng Zhang, Zhonghao Yan, Binzhu Xie et al.
  Introduces LingT2I, a benchmark revealing systematic performance gaps and language-specific effects in multilingual text-to-image generation.

## 3. Research Trend Signal

Today's submissions indicate a maturing field moving from static benchmark chasing to **behavioral, process-level, and cross-lingual assessment**. The unusually high concentration of cross-lingual papers (safety transfer, tool-use policy retention, T2I consistency, Burmese medical ASR) suggests that multilingual deployment is now recognized as a first-class research problem requiring dedicated benchmarks rather than incidental evaluation. Parallel to this, **test-time adaptation and self-evolving systems** — GUI grounding, skill compression, reflective self-distillation — signal a shift from pretrain-then-freeze to continual on-policy refinement. In interpretability, the center of gravity has moved from post-hoc explanation toward causal attribution and uncertainty signals usable for control. Finally, **formal verification and safety** are increasingly prominent: polynomial-time consistency checking, verified financial reasoning, and quantum coordination results all point toward a field concerned with guarantees, not just capability.

## 4. Worth Deep Reading

- **Long-Horizon AI Research for Grothendieck Constant** — [http://arxiv.org/abs/2608.11195v1](http://arxiv.org/abs/2608.11195v1) — One of the few detailed, honest case

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*