# ArXiv AI Research Digest 2026-07-29

> Source: [ArXiv](https://arxiv.org/) (cs.AI, cs.CL, cs.LG) | 50 papers | Generated: 2026-07-29 02:10 UTC

---

# ArXiv AI Research Digest — 2026-07-29

## Today's Highlights

This week's submissions reveal a strong pivot toward **process-oriented evaluation** over outcome-only metrics, with multiple papers arguing that how a model arrives at an answer matters as much as the answer itself. **Interpretability and safety** dominate across subfields, from sparse autoencoders that encode both concepts and functions (Hoang et al.) to novel hallucination detection via hidden-state geometry (Raimondi et al.) and stratified risk control for LLM tool calls (Rahman et al.). **Agentic systems** continue to mature, with work on multi-turn planning distillation, closed-loop refinement for ECG classifiers, and evidence-grounded RAG for scientific facilities. Several papers also tackle **efficiency under real-world constraints**—MXFP4 attention quantization for video generation, page-local KV cache summaries, and speculative decoding for MoE models on end devices.

---

## Key Papers

### 🧠 Large Language Models

1. **The Physics of Multi-Turn Long-Horizon Planning: From Pre-training to Post-training via Single- and Multi-Teacher On-Policy Agentic Distillation**
   http://arxiv.org/abs/2607.24720v1
   *Men et al.*
   Systematically decomposes how planning ability is acquired across pre-training and post-training, proposing a distillation framework that isolates the contribution of each training stage.

2. **D-Score: A Spectral Hidden-State Signal for Hallucination Detection in Large Language Models**
   http://arxiv.org/abs/2607.24586v1
   *Raimondi et al.*
   Introduces a simple spectral score derived from hidden activation geometry that detects hallucinations without requiring external knowledge bases or sampling.

3. **Sparse Autoencoders Encode Both Concepts and Functions: The Downstream Geometry of Feature Effects**
   http://arxiv.org/abs/2607.24645v1
   *Hoang et al.*
   Shows that SAE features have inconsistent causal effects on model behavior and proposes a geometric analysis framework to bridge feature activations with downstream steering outcomes.

4. **Hierarchical Group-Conditional Conformal Risk Control for Selective Prediction in Language Models**
   http://arxiv.org/abs/2607.24562v1
   *Salem et al.*
   Extends conformal risk control to guarantee per-group rather than marginal coverage, addressing failure cases where overall metrics mask poor performance on minority subgroups.

5. **Beyond Aggregate Risk: Role-Stratified Conformal Risk Control for LLM Tool Calls**
   http://arxiv.org/abs/2607.24343v1
   *Rahman et al.*
   Controls risk separately for different argument roles in tool calls (e.g., recipient vs. email body), preventing untrusted content from influencing high-stakes fields.

6. **UNIFUSION: Adapting Autoregressive Language Models into Discrete Diffusion under a Unified Reverse-Rate Objective**
   http://arxiv.org/abs/2607.24507v1
   *Jiang et al.*
   Adapts pretrained AR language models to uniform-noise discrete diffusion, enabling fully editable token sequences during sampling while preserving pretrained weights.

### 🤖 Agents & Reasoning

7. **DataOrchestra: Learning to Orchestrate Per-Example Curation of Pretraining Data**
   http://arxiv.org/abs/2607.24717v1
   *Huang et al.*
   Moves beyond corpus-level filtering by learning an agent that curates each pretraining example individually, significantly improving downstream LLM performance.

8. **A corrective agentic hybrid RAG and an operations-grounded evaluation for a scientific facility**
   http://arxiv.org/abs/2607.24663v1
   *Sainju et al.*
   Presents APS-RAG, a production RAG system for the Advanced Photon Source that fuses heterogeneous operational data sources with agentic correction loops.

9. **Failures Reveal What Metrics Miss: An Evidence-Driven Agent for Recursive Refinement of ECG Classifiers**
   http://arxiv.org/abs/2607.24419v1
   *Deng et al.*
   Proposes an LLM-based agent that inspects classification failures and recursively revises model designs, outperforming aggregate-metric-guided refinement.

10. **Closed-Loop Validation-Repair for Healthcare Interoperability: A Multi-Model Study of Schema Compliance in Clinical LLMs**
    http://arxiv.org/abs/2607.24371v1
    *Shen*
    Introduces a validation-repair loop ensuring LLM outputs conform to medical schemas (ICD-10, CPT, HL7 FHIR), critical for clinical deployment.

### 🔧 Methods & Frameworks

11. **MXAttention: Data-Free Optimal Scaling and Pre-Normalization Quantization for MXFP4 Attention**
    http://arxiv.org/abs/2607.24377v1
    *Yu et al.*
    Solves clipping-underflow tradeoffs in MXFP4 attention quantization for diffusion video models, restoring generation quality without calibration data.

12. **LOCKS: Page-Local Compact Key Summaries for Efficient Long-Context Decoding**
    http://arxiv.org/abs/2607.24555v1
    *Hwang*
    Exploits locally low-rank structure of attention keys to build compact page-level summaries, reducing KV cache memory without significant accuracy loss.

13. **DraftExpert: Expansion-Aware Self-Speculative Decoding for End-Device MoE Inference**
    http://arxiv.org/abs/2607.24434v1
    *Han*
    Speculative decoding that accounts for expert routing in MoE models, enabling latency-critical single-user inference on memory-constrained devices.

14. **Eviction as Estimation: A Fixed-Lag Smoothing View of Test-Time Memory, and When Measuring Beats Accumulating**
    http://arxiv.org/abs/2607.24667v1
    *Vemula & Gajula*
    Reframes bounded working memory eviction as an estimation problem on a hidden signal, showing that state-space models can outperform accumulation-based key-value compression.

### 📊 Applications

15. **ClinFusion: A Vision-Centric Multimodal LLM System for Holistic Medical Understanding**
    http://arxiv.org/abs/2607.24743v1
    *Yuan et al.*
    Unifies 2D and 3D medical image understanding through a single MLLM architecture, addressing a core vision-centric challenge in clinical AI.

16. **KANEx: Translating Kolmogorov-Arnold Networks' Interpretability to Medical Explainability**
    http://arxiv.org/abs/2607.24730v1
    *Shailya et al.*
    Adapts Kolmogorov-Arnold Networks for chest X-ray classification, providing inherently interpretable decisions paired with VLM-generated natural language explanations.

17. **Stress-Testing EEG Foundation Models for Clinical Decoding: Dataset Identity and Targeted Negative Controls**
    http://arxiv.org/abs/2607.24519v1
    *Zare*
    Benchmarks six EEG foundation models across four datasets, revealing that pretraining on large unlabeled data does not reliably improve clinical decoding transfer.

---

## Research Trend Signal

Two convergent trends are particularly noteworthy. First, **evaluation is shifting from aggregate metrics to process-centric auditing**: multiple papers argue that a model producing the right final answer while using wrong rationale is a failure mode requiring explicit detection (Pandey & Jajoo on social simulators, Zhao et al. on faithfulness audit, Gao et al. on looping vs. reliability). This reflects growing recognition that black-box outcome evaluation is insufficient for deployment in high-stakes domains. Second, **topology and geometry are emerging as unifying analytical tools** across previously separate problems: spectral hallucination detection from hidden-state manifolds (Raimondi et al.), topological privacy guarantees via Betti numbers for split learning (Nair et al.), and geometric analysis of SAE feature effects (Hoang et al.). This suggests a maturing theoretical infrastructure for interpretability and safety that moves beyond "attention visualization" toward principled structural analysis.

---

## Worth Deep Reading

1. **The Physics of Multi-Turn Long-Horizon Planning** (Men et al., 2607.24720) — One of the most comprehensive empirical dissections of how planning ability emerges across training stages. The multi-teacher distillation framework provides a rigorous experimental protocol that could become a standard methodology for studying capability acquisition in foundation models.

2. **Sparse Autoencoders Encode Both Concepts and Functions** (Hoang et al., 2607.24645) — Directly challenges the dominant narrative that SAE features cleanly correspond to interpretable concepts. The geometric framework for understanding feature *effects* (not just activations) is a significant step toward making SAEs practically useful for model steering.

3. **Beyond Aggregate Risk: Role-Stratified Conformal Risk Control for LLM Tool Calls** (Rahman et al., 2607.24343) — Addresses a critical blind spot in LLM safety: treating all tool call arguments as equally sensitive. The stratified approach is immediately applicable and could prevent a class of real-world injection vulnerabilities that aggregate safeguards miss.

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*