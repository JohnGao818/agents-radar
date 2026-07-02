# Hugging Face Trending Models Digest 2026-07-02

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-07-02 02:52 UTC

---

# 🧠 Hugging Face Trending Models Digest — 2026-07-02

## 1. Today’s Highlights

A wave of large‑scale MoE models dominates this week, led by **GLM‑5.2** (3,174 likes) and its numerous quantized variants from NVIDIA, Unsloth, and the community. Multimodal models continue to surge, with **baidu/Unlimited‑OCR** (1,581 likes) for image‑to‑text and **nvidia/LocateAnything‑3B** (2,548 likes) for grounded visual localization. The coding/agentic space is hot, as seen in **gemma‑4‑12B** GGUF fine‑tunes and the new **Qwen‑AgentWorld** series. Quantization remains the primary way to democratise these large models, with GGUF and NVIDIA’s NVFP4 formats seeing heavy adoption. A notable newcomer is the **HauhauCS/Qwen3.6‑35B‑A3B‑Uncensored** (2,379 likes) with over 3 million downloads, reflecting strong demand for uncensored MoE models.

## 2. Trending Models by Category

### 🧠 Language Models (LLMs, chat, instruction‑tuned)

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — zai‑org | 3,174 likes · 159,967 downloads  
  A Mixture‑of‑Experts conversational model with advanced RAG and DSA capabilities, trending as the week’s top‑liked model.
- **[deepseek-ai/DeepSeek-V4-Pro-DSpark](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-DSpark)** — deepseek‑ai | 278 likes · 7,629 downloads  
  The latest DeepSeek flagship, introducing the DSpark inference engine for efficient large‑scale generation.
- **[deepseek-ai/DeepSeek-V4-Flash-DSpark](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-DSpark)** — deepseek‑ai | 124 likes · 13,038 downloads  
  A lighter, faster variant of DeepSeek V4 optimised for real‑time applications.
- **[LiquidAI/LFM2.5-230M](https://huggingface.co/LiquidAI/LFM2.5-230M)** — LiquidAI | 182 likes · 21,935 downloads  
  A tiny but capable 230M‑parameter Liquid Foundation Model, gaining attention for its efficiency and edge‑deployment potential.

### 🎨 Multimodal & Generation (image, video, audio, text‑to‑X)

- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** — baidu | 1,581 likes · 630,246 downloads  
  A unified image‑to‑text model handling OCR, document analysis, and scene text recognition, trending for its broad utility.
- **[deepreinforce-ai/Ornith-1.0-397B](https://huggingface.co/deepreinforce-ai/Ornith-1.0-397B)** — deepreinforce‑ai | 186 likes · 5,792 downloads  
  The largest Ornith variant (397B MoE), built on Qwen3.5 and capable of both text and image understanding.
- **[deepreinforce-ai/Ornith-1.0-35B](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B)** — deepreinforce‑ai | 293 likes · 135,452 downloads  
  A 35B‑parameter multimodal MoE model, widely used as a base for community quantisations.
- **[krea/Krea-2-Turbo](https://huggingface.co/krea/Krea-2-Turbo)** — krea | 439 likes · 56,953 downloads  
  A text‑to‑image diffusion model with fast inference, built on the Krea‑2 architecture.
- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — nvidia | 2,548 likes · 896,058 downloads  
  A small 3B model for visual grounding and object localisation, incredibly popular for its zero‑shot performance.
- **[Qwen/Qwen-AgentWorld-35B-A3B](https://huggingface.co/Qwen/Qwen-AgentWorld-35B-A3B)** — Qwen | 498 likes · 34,371 downloads  
  An agent‑oriented MoE model (35B total, 3B active) designed for tool use and world modelling.

### 🔧 Specialized Models (code, math, medical, embeddings)

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** (already listed above) — also fits here as a specialised grounding model.
- **(No other strictly specialised base models in the top 30 aside from quantisations; the closest are coding GGUF fine‑tunes, covered below.)**

### 📦 Fine‑tunes & Quantizations (community fine‑tunes, GGUF, AWQ)

- **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)** — yuxinlu1 | 2,554 likes · 597,090 downloads  
  A highly liked GGUF quantisation of a gemma‑4 coder fine‑tune, optimised for code generation and reasoning.
- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** — empero‑ai | 1,163 likes · 1,113,871 downloads  
  A mythos‑style Qwen3.5 fine‑tune in GGUF format, extremely popular for creative/role‑play tasks.
- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — HauhauCS | 2,379 likes · 3,055,962 downloads  
  An uncensored MoE GGUF with aggressive persona tuning, one of the most downloaded models this week.
- **[unsloth/GLM-5.2-GGUF](https://huggingface.co/unsloth/GLM-5.2-GGUF)** — unsloth | 490 likes · 212,201 downloads  
  Official GLM‑5.2 quantisation in GG

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*