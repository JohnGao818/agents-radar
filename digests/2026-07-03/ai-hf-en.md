# Hugging Face Trending Models Digest 2026-07-03

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-07-03 02:35 UTC

---

# Hugging Face Trending Models Digest — 2026-07-03

## Today's Highlights

This week’s trending models reflect a strong shift toward **MoE (Mixture-of-Experts) architectures**, with GLM-5.2 (3,257 likes) and the Qwen3.5-derived Ornith family dominating. **Specialized vision models** are surging — Nvidia’s **LocateAnything-3B** (2,573 likes, 1M+ downloads) leads the pack for object localization, while Baidu’s **Unlimited-OCR** (1,653 likes) shows enterprise-grade OCR going mainstream. **GGUF quantizations** of popular models continue to drive downloads, with the uncensored Qwen3.6 variant from HauhauCS reaching an astonishing **3M weekly downloads**. The coding segment sees strong competition from Gemma-4-based fine-tunes and the new Qwopus Coder GGUF. DeepSeek V4 Pro & Flash bring cutting-edge reasoning capabilities, and Google’s tabfm-1.0.0 hints at growing interest in **tabular foundation models**.

---

## Trending Models by Category

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — *zai-org* · 3,257 likes · 176k downloads  
  A 5.2B MoE conversational model that has quickly become one of the most popular open-weight Chinese-English LLMs.

- **[deepseek-ai/DeepSeek-V4-Pro-DSpark](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-DSpark)** — *deepseek-ai* · 303 likes · 8k downloads  
  The latest flagship in DeepSeek’s V4 series, optimized for high-throughput reasoning with DSpark acceleration.

- **[deepseek-ai/DeepSeek-V4-Flash-DSpark](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-DSpark)** — *deepseek-ai* · 128 likes · 24k downloads  
  A lighter, faster variant of DeepSeek-V4 for low-latency applications, also DSpark-enabled.

- **[deepreinforce-ai/Ornith-1.0-397B](https://huggingface.co/deepreinforce-ai/Ornith-1.0-397B)** — *deepreinforce-ai* · 196 likes · 7k downloads  
  The largest Ornith variant (397B MoE) targeting high-end reasoning and multimodal tasks.

- **[deepreinforce-ai/Ornith-1.0-35B](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B)** — *deepreinforce-ai* · 312 likes · 186k downloads  
  The 35B MoE version of Ornith, balanced for performance and accessibility.

- **[deepreinforce-ai/Ornith-1.0-9B](https://huggingface.co/deepreinforce-ai/Ornith-1.0-9B)** — *deepreinforce-ai* · 353 likes · 58k downloads  
  The smallest Ornith base model, offering strong reasoning in a compact 9B MoE footprint.

- **[Qwen/Qwen-AgentWorld-35B-A3B](https://huggingface.co/Qwen/Qwen-AgentWorld-35B-A3B)** — *Qwen* · 511 likes · 39k downloads  
  An agent-oriented MoE model from Qwen, designed for tool use and multi-turn autonomy.

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M)** — *empero-ai* · 645 likes · 125k downloads  
  A fine-tuned Qwen3.5–9B with synthetic Claude-style reasoning data, popular for creative text generation.

- **[InternScience/Agents-A1](https://huggingface.co/InternScience/Agents-A1)** — *InternScience* · 182 likes · 1.5k downloads  
  An experimental MoE model specialized for autonomous agent workflows.

- **[LiquidAI/LFM2.5-230M](https://huggingface.co/LiquidAI/LFM2.5-230M)** — *LiquidAI* · 193 likes · 26k downloads  
  A tiny 230M parameter language model from Liquid AI, optimized for edge deployment with surprising coherence.

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** — *baidu* · 1,653 likes · 758k downloads  
  An enterprise-grade OCR model from Baidu that reads text from any image with near-perfect accuracy, driving massive downloads.

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — *nvidia* · 2,573 likes · 1M downloads  
  A 3B vision-language model that can locate any object in an image via natural language queries, trending for its precision and speed.

- **[krea/Krea-2-Turbo](https://huggingface.co/krea/Krea-2-Turbo)** — *krea* · 462 likes · 70k downloads  
  A turbo-charged text-to-image diffusion model built on Krea-2-Raw, optimized for real-time generation.

- **[fal/LTX-2.3-3DREAL-LoRA](https://huggingface.co/fal/LTX-2.3-3DREAL-LoRA)** — *fal* · 145 likes · 0 downloads (new)  
  A LoRA adapter for LTX-2.3 video models that adds photorealistic 3D-aware motion.

- **[ilkerzgi/fal-Krea-2-Style-LoRAs](https://huggingface.co/ilkerzgi/fal-Krea-2-Style-LoRAs)** — *ilkerzgi* · 107 likes · 0 downloads (new)  
  A collection of style LoRAs for Krea-2, enabling consistent artistic styles in generated images.

### 🔧 Specialized Models (code, math, medical, embeddings, tabular, etc.)

- **[google/tabfm-1.0.0-pytorch](https://huggingface.co/google/tabfm-1.0.0-pytorch)** — *google* · 119 likes · 89 downloads  
  A foundational tabular model from Google supporting zero-shot classification and regression across diverse datasets.

- **[nationaldesignstudio/rampart](https://huggingface.co/nationaldesignstudio/rampart)** — *nationaldesignstudio* · 105 likes · 790 downloads  
  A BERT-based token classifier for detecting personally identifiable information (PII), useful for compliance pipelines.

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ, NVFP4)

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** — *empero-ai* · 1,258 likes · 1.25M downloads  
  GGUF quantized version of the Claude-Mythos fine-tune, extremely popular for local inference with llama.cpp.

- **[deepreinforce-ai/Ornith-1.0-35B-GGUF](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B-GGUF)** — *deepreinforce-ai* · 658 likes · 285k downloads  
  GGUF quantized 35B Ornith model for efficient local deployment with good reasoning quality.

- **[deepreinforce-ai/Ornith-1.0-9B-GGUF](https://huggingface.co/deepreinforce-ai/Ornith-1.0-9B-GGUF)** — *deepreinforce-ai* · 397 likes · 255k downloads  
  The smaller GGUF variant of Ornith, balanced for performance and memory footprint.

- **[yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)** — *yuxinlu1* · 963 likes · 314k downloads  
  An agentic fine-tune of Gemma-4-12B in GGUF format, optimized for coding and terminal tasks.

- **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)** — *yuxinlu1* · 2,573 likes · 614k downloads  
  A top-tier coding fine-tune of Gemma-4-12B, achieving high reasoning accuracy in a quantized format.

- **[nvidia/Qwen3.6-27B-NVFP4](

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*