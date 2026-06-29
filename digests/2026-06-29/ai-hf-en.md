# Hugging Face Trending Models Digest 2026-06-29

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-06-29 03:31 UTC

---

# 🤗 Hugging Face Trending Models Digest — June 29, 2026

## 1. Today's Highlights

This week's trending landscape is dominated by a new wave of Mixture-of-Experts (MoE) models, led by **zai-org/GLM-5.2** and its rapidly adopted quantized variants. **nvidia/LocateAnything-3B** has emerged as a standout specialized model for visual grounding, while **HauhauCS** continues to push the boundaries of community fine-tuning with massive downloads of their Qwen3.6 and Gemma4 uncensored series. The debut of **DeepSeek-V4-Pro-DSpark** from DeepSeek signals continued investment in high-end, research-grade open-weight models, and the **Ornith-1.0** family from deepreinforce-ai provides a new multi-scale MoE option ranging from 9B to 397B parameters. Quantization activity remains intense, with GGUF and Nvidia's NVFP4 formats seeing heavy adoption.

---

## 2. Trending Models by Category

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — zai-org | 2,831 likes, 118,651 downloads  
  A conversational MoE-DSA model from the GLM family, trending as the week's most-liked LLM, likely due to strong benchmark results and broad task versatility.

- **[deepreinforce-ai/Ornith-1.0-35B](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B)** — deepreinforce-ai | 209 likes, 19,635 downloads  
  A 35B MoE model based on Qwen3.5, trending alongside its GGUF counterpart as a new mid-scale open-weight LLM for general text generation.

- **[deepreinforce-ai/Ornith-1.0-397B](https://huggingface.co/deepreinforce-ai/Ornith-1.0-397B)** — deepreinforce-ai | 148 likes, 1,116 downloads  
  The largest Ornith variant, a 397B MoE model likely targeting enterprise-grade reasoning and synthesis tasks.

- **[deepseek-ai/DeepSeek-V4-Pro-DSpark](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-DSpark)** — deepseek-ai | 185 likes, 373 downloads  
  A new flagship from DeepSeek accompanying an arXiv paper, representing a major open-weight research release for advanced reasoning.

- **[WeiboAI/VibeThinker-3B](https://huggingface.co/WeiboAI/VibeThinker-3B)** — WeiboAI | 743 likes, 59,337 downloads  
  A Qwen2-based 3B math-focused reasoning model, gaining traction for its small-footprint performance on mathematical tasks.

- **[microsoft/FastContext-1.0-4B-SFT](https://huggingface.co/microsoft/FastContext-1.0-4B-SFT)** — microsoft | 369 likes, 6,779 downloads  
  A Qwen3-based 4B model with SFT for efficient long-context handling, featuring an "Explorer SubAgent" architecture.

- **[LiquidAI/LFM2.5-230M](https://huggingface.co/LiquidAI/LFM2.5-230M)** — LiquidAI | 141 likes, 12,384 downloads  
  A tiny 230M liquid foundation model, interesting for deployment on edge devices with reasonable generation quality.

- **[Chunjiang-Intelligence/DeepSeek-v4-Fable](https://huggingface.co/Chunjiang-Intelligence/DeepSeek-v4-Fable)** — Chunjiang-Intelligence | 124 likes, 1,409 downloads  
  A cybersecurity-tuned variant of DeepSeek-v4, serving a specialized but growing niche in AI security applications.

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** — baidu | 1,248 likes, 295,064 downloads  
  A feature-extraction model for unlimited OCR (image-to-text), trending as a robust production-ready tool for document understanding.

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** — empero-ai | 809 likes, 831,529 downloads  
  A Qwen3.5-based image-text-to-text GGUF model, widely downloaded for vision-language reasoning tasks.

- **[krea/Krea-2-Turbo](https://huggingface.co/krea/Krea-2-Turbo)** — krea | 358 likes, 27,631 downloads  
  A text-to-image diffusion model building on Krea-2-Raw, trending for fast, high-quality image generation.

- **[krea/Krea-2-Raw](https://huggingface.co/krea/Krea-2-Raw)** — krea | 232 likes, 22,622 downloads  
  The base model for the Krea-2 diffusion family, representing a new open-source image synthesis pipeline.

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — nvidia | 2,437 likes, 646,451 downloads  
  A 3B image-feature-extraction model for spatial grounding and object localization, highly trending for multimodal perception tasks.

- **[HauhauCS/Gemma4-12B-QAT-Uncensored-HauhauCS-Balanced](https://huggingface.co/HauhauCS/Gemma4-12B-QAT-Uncensored-HauhauCS-Balanced)** — HauhauCS | 101 likes, 40,820 downloads  
  A vision-capable uncensored Gemma4 variant, part of the community's push for less constrained multimodal models.

- **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)** — nvidia | 734 likes, 67,419 downloads  
  A 600M streaming ASR model built with NeMo, offering efficient real-time speech recognition.

- **[fal/LTX-2.3-3DREAL-LoRA](https://huggingface.co/fal/LTX-2.3-3DREAL-LoRA)** — fal | 97 likes, 0 downloads  
  A LoRA adapter for LTX-2.3 enabling 3D-realistic image-to-video generation, newly released with minimal download count.

### 🔧 Specialized Models (code, math, embeddings, feature extraction)

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** *(also listed in Multimodal)* — nvidia | 2,437 likes, 646,451 downloads  
  A specialized grounding model for any-object localization in images, serving robotic and AR applications.

- **[WeiboAI/VibeThinker-3B](https://huggingface.co/WeiboAI/VibeThinker-3B)** *(also listed in LLMs)* — WeiboAI | 743 likes, 59,337 downloads  
  Specialized for mathematical reasoning with a compact 3B architecture.

- **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)** — yuxinlu1 | 2,477 likes, 549,926 downloads  
  A highly popular Gemma4 GGUF model fine-tuned for code generation and reasoning, racking up massive community adoption.

- **[yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)** — yuxinlu1 | 801 likes, 225,822 downloads  
  Another Gemma4 GGUF variant, optimized for agentic and terminal-based coding workflows.

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **[unsloth/GLM-5.2-GGUF](https://huggingface.co/unsloth/GLM-5.2-GGUF)** — unsloth | 444 likes, 146,023 downloads  
  A community-quantized GGUF version of GLM-5.2 by unsloth, enabling efficient local deployment of the MoE backbone.

- **[nvidia/GLM-5.2-NVFP4](https://huggingface.co/nvidia/GLM-5.2-NVFP4)** — nvidia | 155 likes, 45,762 downloads  
  Nvidia's NVFP4-optimized variant of GLM-5.2, designed for high throughput on Nvidia hardware with ModelOpt.

- **[nvidia/Qwen3.6-35B-A3B-NVFP4](https://huggingface.co/nvidia/Qwen3.6-35B-A3B-NVFP4)** — nvidia | 371 likes, 5,235,413 downloads  
  By far the most downloaded model on the list, an NVFP4-optimized Qwen3.6 MoE running on Nvidia's optimized inference stack.

- **[deepreinforce-ai/Ornith-1.0-35B-GGUF](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B-GGUF)** — deepreinforce-ai | 419 likes, 79,630 downloads  
  GGUF version of the Ornith-1.0-35B, popular for running the large MoE on consumer hardware via llama.cpp.

- **[deepreinforce-ai/Ornith-1.0-9B-GGUF](https://huggingface.co/deepreinforce-ai/Ornith-1.0-9B-GGUF)** — deepreinforce-ai | 278 likes, 36,846 downloads  
  Smaller GGUF variant of the Ornith family, suitable for resource-constrained setups.

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — HauhauCS | 2,302 likes, 3,248,724 downloads  
  A heavily quantized uncensored Qwen3.6 model (GGUF) with aggressive fine-tuning, trending for its high download count and controversial positioning.

- **[unsloth/Qwen-AgentWorld-35B-A3B-GGUF](https://huggingface.co/unsloth/Qwen-AgentWorld-35B-A3B-GGUF)** — unsloth | 96 likes, 79,503 downloads  
  A GGUF quantization of Qwen's AgentWorld model, designed for world-model and agent simulation tasks.

---

## 3. Ecosystem Signal

The model ecosystem is converging on **Mixture-of-Experts (MoE)** as the dominant architecture, with nearly every major release this week (GLM-5.2, Qwen3.6-35B-A3B, Ornith-1.0, DeepSeek-V4, AgentWorld) employing some form of MoE. Qwen's ecosystem appears strongest, spawning the most community fine-tunes and quantizations. **Quantization formats are bifurcating**: GGUF (via llama.cpp) remains the standard for consumer local deployment, while Nvidia is aggressively pushing **NVFP4** as a hardware-optimized alternative, achieving massive download numbers (5M+ for one variant). The presence of both **DeepSeek-V4** and **microsoft/FastContext** indicates strong corporate open-weight investment alongside community fine-tuning efforts. Notably, "uncensored" fine-tunes continue to command disproportionate download volumes, suggesting an enduring demand for less restrictive model behavior. Meanwhile, specialized models like **LocateAnything-3B** and **nemotron-3.5-asr** highlight a maturing ecosystem where task-specific models gain rapid adoption.

---

## 4. Worth Exploring

1. **[Qwen/Qwen-AgentWorld-35B-A3B](https://huggingface.co/Qwen/Qwen-AgentWorld-35B-A3B)** — A dedicated world-model MoE designed for agentic simulation, representing a frontier direction in AI research. Its GGUF variant is already available through unsloth. Worth studying for anyone working on embodied AI or multi-step planning.

2. **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — One of the highest-liked specialized models this week, combining a compact 3B footprint with state-of-the-art visual grounding. Excellent for robotic perception, AR/VR, and document layout analysis.

3. **[microsoft/FastContext-1.0-4B-SFT](https://huggingface.co/microsoft/FastContext-1.0-4B-SFT)** — A novel approach to long-context handling using a sub-agent architecture. Its compact size (4B) makes it practical for testing context-extension techniques without requiring massive compute.

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*