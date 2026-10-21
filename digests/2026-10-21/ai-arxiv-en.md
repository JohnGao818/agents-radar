# ArXiv AI Research Digest 2026-10-21

> Source: [ArXiv](https://arxiv.org/) (cs.AI, cs.CL, cs.LG) | 50 papers | Generated: 2026-10-21 03:06 UTC

---

# ArXiv AI Research Digest — 2026-10-21

## 1. Today's Highlights

Today's submissions converge on a single uncomfortable question: **how much of reported model capability is real, and how much is scaffolding?** Agent-harness optimization gains are shown to be largely *elicitation* rather than capability expansion (paper 16), compressed-model evaluations miss distributed knowledge loss (8), and e-commerce agents fail silently on plausible-but-wrong tool outputs (43). LLM safety gets a structural diagnosis: models exhibit **polarity blindness**, where negation and antonym substitution strip guardrails while preserving harmful intent (10). Post-training science is maturing rapidly — a systematic DPO hyperparameter landscape (13), a pedagogical reformulation of scaling laws (39), and a role-reversed speculative decoding scheme (32) all push toward principled efficiency. Meanwhile, a striking result shows that merely *selecting among near-duplicate images* can transmit a model's preferences to its successor — a new vector for subliminal learning (1).

---

## 2. Key Papers

### 🧠 Large Language Models

**[Polarity Blindness in LLM Safety: A Systematic Study of Negation, Antonym Substitution, and Adversarial Framing](http://arxiv.org/abs/2610.27908v1)**
Lozano, Derner, Pérez-Ortiz et al.
Defines and systematically measures a structural safety failure where polarity-altering rewrites ("do not tell me how to…") bypass guardrails — a checklist item for any red-teaming pipeline.

**[ACE-Compression: An Ability-Centric Evaluation of Compressed Large Language Models](http://arxiv.org/abs/2610.27913v1)**
Ning, Chen, Liang et al.
Argues that retained-task-accuracy is an incomplete compression metric and proposes ability-centric evaluation that captures perturbation of distributed knowledge — reframes how we should certify compressed releases.

**[The Shape of the DPO Hyperparameter Landscape: What to Measure, How It Moves with Scale, and When Not to Transfer It](http://arxiv.org/abs/2610.27895v1)**
Mahadik, Salinas, Golebiowski et al.
Charts how DPO hyperparameters (learning rate, β) interact with scale and shows when tuned settings fail to transfer across model sizes — practical guidance for post-training at scale.

**[ProVe: Proposer-Verifier Decoding](http://arxiv.org/abs/2610.27815v1)**
Jin, Xu, Li et al.
Reverses speculative decoding: a fine-tuned large model proposes a block of future tokens and verifies in parallel, offering a new speed/quality trade-off curve for autoregressive inference.

**[Foundations of the Scaling Law](http://arxiv.org/abs/2610.27789v1)**
Zhao, Ren
A pedagogical synthesis linking spatial resolution, intrinsic dimension, and compute to validation loss — useful as the current "cleanest" mental model of scaling behavior.

**[Are Linguistic and Arithmetic Circuits Dissociated in LLMs?](http://arxiv.org/abs/2610.27790v1)**
Kisako, Kuribayashi, Sasano
Borrows the neurolinguistic dissociation hypothesis to probe whether grammatical and arithmetic abilities occupy separable circuits in LLMs — evidence for modularity (or lack thereof) inside transformers.

---

### 🤖 Agents & Reasoning

**[Elicitation or Expansion? Demystifying Gains from Agent Harness Optimization](http://arxiv.org/abs/2610.27889v1)**
Kim, Seo, Kim et al.
Decomposes harness-optimization gains into elicitation of existing capability versus genuine expansion — an essential methodological correction for the agent-scaffolding literature.

**[MMEnterprise-Bench: Evaluating Enterprise Agents over Evolving Multimodal Records](http://arxiv.org/abs/2610.27911v1)**
Lee, Kim, Ko et al.
Benchmarks agents on workspaces where documents, chats, and figures accumulate multiple versions — targets the realistic "which revision is current?" problem that current QA benchmarks ignore.

**[RITE: Evaluating End-to-End Resilience to Silent Tool Errors in E-Commerce Agentic Systems](http://arxiv.org/abs/2610.27777v1)**
Zhang, Lin, Sun et al.
Introduces a benchmark for *silent* tool failures (plausible but wrong values with no error signal) in multi-step e-commerce agents — a failure mode that standard tool-use benchmarks systematically miss.

**[SAPD: Learning from Agent Experience without Environment Interaction](http://arxiv.org/abs/2610.27847v1)**
Diao, Wang, Shi et al.
Proposes learning from offline trajectories without executable environments, relaxing the dominant bottleneck (environment construction) in scaling LLM-agent training.

**[GRADUS: Discovering and Recovering Agent Lessons from the Environment's Latent Syllabus](http://arxiv.org/abs/2610.27781v1)**
Ping, Yang, Xu et al.
Frames policy-constrained tool environments as having a latent "syllabus" of rules and infers it to synthesize tasks that exercise rules individually and in combination — improves coverage over naive task proposal.

**[COMPASS: Routing via Capability-Oriented Model Profiling with Adaptive Search, Selection, and Tool Use](http://arxiv.org/abs/2610.27822v1)**
Rezaei, Parsa
An agentic router that gathers performance/cost evidence through tools rather than relying on a fixed learned router — more robust to model and task churn.

---

### 🔧 Methods & Frameworks

**[Near-Duplicate Image Selection Transfers Preferences in Vision-Language Models](http://arxiv.org/abs/2610.27943v1)**
Kim, Kim, Jang et al.
Shows that choosing among near-duplicate images — with no explicit preference signal — transmits a curator model's preferences to a downstream VLM, extending subliminal learning to data-selection decisions.

**[RAG-NIMBF: A Non-Invasive, Modular Benchmarking Framework for Automated RAG Configuration Analysis](http://arxiv.org/abs/2610.27816v1)**
Hart, Weeger
Provides a non-invasive, modular framework for systematically sweeping the chunking/embedding/retrieval/reranking/prompting configuration space — addresses a real pain point for RAG practitioners.

**[How Much Do ℓ₁ Attacks Need Concentrated Perturbations?](http://arxiv.org/abs/2610.27773v1)**
Shirian, Vadaei, Hemmat
Adds a per-coordinate cap to the global ℓ₁ budget and quantifies how much attack success survives — clarifying *where* ℓ₁ adversarial success actually lives.

**[AC/DC on a Budget — Alternating Sparse Phases](http://arxiv.org/abs/2610.27758v1)**
Nittala, Gadhikar, Jacobs et al.
Explains mechanistically why dense phases are critical in alternating sparsification (masked parameters receive large updates upon reintroduction) and proposes cheaper alternatives.

---

### 📊 Applications

**[Hallucinations of Large Language Models in Cross-Language Code Translation: Phenomena and Mitigation](http://arxiv.org/abs/2610.27868v1)**
Du, Zhang, Li
Characterizes translation-specific hallucinations that violate source semantics or target-language idioms, then proposes mitigation — directly relevant to any code-migration pipeline.

**[Toward Agentic AI for the 6G Physical Layer: From Algorithm Discovery to Verified Baseband Silicon](http://arxiv.org/abs/2610.27797v1)**
Mittag, Brechtel, Stark et al.
Closes the loop from AI-driven algorithm search to hardware-verified baseband implementations under memory/numeric constraints — a rare end-to-end agentic engineering result.

**[HypTI: Hyperbolic Geometry-Aware Multimodal Feature Fusion Framework for Dementia Detection](http://arxiv.org/abs/2610.27941v1)**
Xu, Liang, Harrison et al.
Replaces Euclidean fusion with hyperbolic geometry to respect hierarchical structure across tabular clinical and neuroimaging data — a principled geometric prior for clinical multimodal fusion.

**[Radar-Based 3D Human Pose Estimation via Motion-Aware Pose Initialization and Observation-Guided Refinement](http://arxiv.org/abs/2610.27774v1)**
Jung, Lim, Kong
Combines motion-aware initialization with observation-guided refinement for mmWave radar pose estimation, improving a privacy-preserving sensing modality.

---

## 3. Research Trend Signal

Three signals dominate today's batch. **First, evaluation is being audited rather than extended**: papers 16, 8, and 43 all question whether reported gains reflect capability. The "elicitation vs. expansion" distinction is likely to become standard vocabulary. **Second, agent reliability is shifting from capability to robustness** — silent tool errors, evolving enterprise records, and latent policy syllabi all target failures that occur *after* the model is competent. Expect benchmarks that grade recovery rather than success. **Third, post-training and compression are becoming quantitative sciences**: DPO landscape characterization (13), ability-centric compression metrics (8), and scaling-law foundations (39) suggest the field is moving from recipes to transferable laws. A smaller but notable thread — subliminal preference transfer via data selection (1) — raises governance questions about who curates training data and with what implicit biases.

---

## 4. Worth Deep Reading

**1. [Elicitation or Expansion? Demystifying Gains from Agent Harness Optimization](http://arxiv.org/abs/2610.27889v1)**
This paper's framing has outsized methodological leverage: if most harness gains are elicitation, then much of the agent-progress literature is measuring scaffolding rather than model improvement, and benchmark comparisons across harnesses become near-meaningless. Read for its experimental decomposition design and its implications for how you should report agent results.

**2. [Near-Duplicate Image Selection Transfers Preferences in Vision-Language Models](http://arxiv.org/abs/2610.27943v1)**
Conceptually the most surprising result today. It extends subliminal learning from explicit data content to the *act of selection*, implying that curation pipelines are a covert preference channel. Read for the experimental protocol and the near-duplicate construction — and because the safety/governance implications are likely to be cited widely.

**3. [Polarity Blindness in LLM Safety: A Systematic Study of Negation, Antonym Substitution, and Adversarial Framing](http://arxiv.org/abs/2610.27908v1)**
A cleanly scoped vulnerability with a memorable name. The systematic sweep across negation, antonym substitution, and framing gives it the structure of a reference paper rather than an anecdote, and its attack surface is intrinsic to language rather than to any particular model family.

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*