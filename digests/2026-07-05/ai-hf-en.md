# Hugging Face Trending Models Digest 2026-07-05

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-07-05 02:42 UTC

---

Here is the structured digest based on the provided trending models.

---

## Hugging Face Trending Models Digest — 2026-07-05

### 1. Today's Highlights

The Hugging Face ecosystem is dominated this week by **Mixture-of-Experts (MoE) architectures**, with **GLM-5.2** by zai-org taking the top spot by likes (3,399) as a new conversational powerhouse. **NVIDIA** is making a strong push with two high-impact models: the vision-focused **LocateAnything-3B** (2,605 likes, 1.19M downloads) and a 4-bit quantized version of GLM-5.2, signaling enterprise adoption of MoE. The **Gemma 4** family is solidifying its position in the coding niche, as two different GGUF quantizations for 12B agentic and coder variants each surpassed 2,500 weekly likes. Finally, the **Qwen 3.6** family is seeing explosive community adoption, led by an uncensored MoE variant that racked up nearly **3 million downloads** in a single week, highlighting a massive demand for unconstrained local inference.

### 2. Trending Models

#### 🧠 Language Models (LLMs, chat, instruction-tuned)
- **[GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — *zai-org* — **Likes: 3,399** — Downloads: 208,920 — A new flagship MoE chat model from zai-org, trending due to its strong conversational performance and high community engagement this week.
- **[DeepSeek-V4-Pro-DSpark](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-DSpark)** — *deepseek-ai* — **Likes: 370** — Downloads: 10,306 — DeepSeek's latest frontier reasoning model, released with an accompanying arxiv paper and sparking interest in advanced reasoning capabilities.
- **[DeepSeek-V4-Flash-DSpark](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-DSpark)** — *deepseek-ai* — **Likes: 157** — Downloads: 40,271 — The faster, distilled variant of DeepSeek-V4, gaining traction for efficiency-focused applications.
- **[Ornith-1.0-397B](https://huggingface.co/deepreinforce-ai/Ornith-1.0-397B)** — *deepreinforce-ai* — **Likes: 209** — Downloads: 33,268 — A massive 397B MoE model based on Qwen 3.5, offering extreme scale for high-end inference.

#### 🎨 Multimodal & Generation (Image, Video, Text-to-X)
- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — *nvidia* — **Likes: 2,605** — Downloads: 1,194,542 — A 3B vision model for object localization and feature extraction, trending for its high accuracy and NVIDIA’s backing.
- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — *HauhauCS* — **Likes: 2,454** — Downloads: 2,993,053 — An uncensored, vision-capable MoE model based on Qwen 3.6, trending for its massive download count driven by the unrestricted community.
- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** — *baidu* — **Likes: 1,714** — Downloads: 988,379 — Baidu’s OCR model which reads text from images, trending due to its robust performance and widespread utility.
- **[Krea-2-Turbo](https://huggingface.co/krea/Krea-2-Turbo)** — *krea* — **Likes: 496** — Downloads: 89,384 — A boosted version of the Krea-2 text-to-image model, trending for its speed improvements over the base model.
- **[fal/LTX-2.3-3DREAL-LoRA](https://huggingface.co/fal/LTX-2.3-3DREAL-LoRA)** — *fal* — **Likes: 157** — Downloads: 0 — A LoRA adapter for LTX-2.3 enabling high-fidelity 3D-realistic video generation, newly released and gaining early interest.

#### 🔧 Specialized Models (Code, Security, Tabular, Embeddings)
- **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)** — *yuxinlu1* — **Likes: 2,596** — Downloads: 641,260 — A quantized Gemma 4 coder model optimized for code and reasoning, trending as the go-to local coding assistant.
- **[google/tabfm-1.0.0-pytorch](https://huggingface.co/google/tabfm-1.0.0-pytorch)** — *google* — **Likes: 197** — Downloads: 1,177 — Google’s new foundational model for tabular data supporting zero-shot classification and regression, a niche but notable release.
- **[BugTraceAI/BugTraceAI-CORE-Ultra-27B-Q6](https://huggingface.co/BugTraceAI/BugTraceAI-CORE-Ultra-27B-Q6)** — *BugTraceAI* — **Likes: 132** — Downloads: 12,001 — A 6-bit quantized Qwen 3 model specialized for cybersecurity and offensive security, gaining interest from the infosec community.
- **[nationaldesignstudio/rampart](https://huggingface.co/nationaldesignstudio/rampart)** — *nationaldesignstudio* — **Likes: 123** — Downloads: 1,881 — A BERT-based token classifier for PII detection using ONNX, trending for privacy-focused enterprise deployments.

#### 📦 Fine-tunes & Quantizations (GGUF, NVFP4, Community)
- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** — *empero-ai* — **Likes: 1,462** — Downloads: 1,464,047 — A GGUF quantization of a mythopoetic Qwen 3.5 model, extremely popular for local storytelling and creative writing.
- **[deepreinforce-ai/Ornith-1.0-35B-GGUF](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B-GGUF)** — *deepreinforce-ai* — **Likes: 713** — Downloads: 359,659 — The quantized version of the Ornith 35B MoE model, making a high-performance model accessible to consumer hardware.
- **[nvidia/Qwen3.6-27B-NVFP4](https://huggingface.co/nvidia/Qwen3.6-27B-NVFP4)** — *nvidia* — **Likes: 251** — Downloads: 184,521 — NVIDIA’s 4-bit floating-point quantization of Qwen 3.6 using Model Optimizer, offering high quality at low bitwidth.
- **[huihui-ai/Huihui-GLM-5.2-abliterated-GGUF](https://huggingface.co/huihui-ai/Huihui-GLM-5.2-abliterated-GGUF)** — *huihui-ai* — **Likes: 162** — Downloads: 4,701 — A community GGUF of GLM-5.2 with safety filters removed ("abliterated"), popular for roleplay and uncensored chat.

### 3. Ecosystem Signal

**MoE is the architecture of the month.** From GLM-5.2 and DeepSeek-V4 to Qwen 3.6 and Ornith, nearly every major new release leverages Mixture-of-Experts, enabling massive parameter counts (35B–397B) with active parameters as low as 3B–27B. This trend allows frontier-level quality on local hardware.

**Open-weight dominance continues.** All top-10 models by likes are open-weight, with enterprise players like NVIDIA and Google releasing full weights. The **abliteration** sub-trend (removing safety guardrails in GLM-5.2 and Qwen 3.6) shows a vibrant fine-tuning ecosystem prioritizing user freedom over safety alignment.

**Quantization is the distribution layer.** Of the 30 trending models, 12 are explicitly quantized (GGUF or NVFP4). The community has standardized on GGUF for CPU/Apple Silicon and on NVIDIA’s NVFP4 for GPU efficiency. This democratizes 35B-120B MoEs for users with 24GB-48GB VRAM.

**Coding and agentic use-cases are accelerating.** Two Gemma 4 quantizations and a dedicated Qwen 3.6 coder variant signal that local code assistance is the killer app for on-device AI.

### 4. Worth Exploring

1.  **[google/tabfm-1.0.0-pytorch](https://huggingface.co/google/tabfm-1.0.0-pytorch)** — *Reason: It fills a critical gap for tabular data. While LLMs and diffusion models dominate the charts, this is a first-of-its-kind foundational model for zero-shot tabular classification and regression, a massive area for enterprise ML that lacks other SOTA pretrained models.*

2.  **[nvidia/Nemotron-Labs-TwoTower-30B-A3B-Base-BF16](https://huggingface.co/nvidia/Nemotron-Labs-TwoTower-30B-A3B-Base-BF16)** — *Reason: Represents a novel "two-tower" MoE architecture from NVIDIA, diverging from the standard decoder-only paradigm. It is worth studying for researchers interested in alternative routing and representation strategies in MoEs.*

3.  **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — *Reason: At nearly 3 million downloads, it is the most downloaded model this week by a wide margin. It is a crucial data point for understanding what the “power user” community values: high-quality vision-language capabilities combined with zero censorship, all packaged in an efficient MoE format for local inference.*

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*