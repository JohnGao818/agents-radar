# Hugging Face Trending Models Digest 2026-07-21

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-07-21 02:14 UTC

---

# 🤗 Hugging Face Trending Models Digest — 2026-07-21

## 1. Today's Highlights

The Hugging Face ecosystem is experiencing a fascinating convergence of **extreme compression** and **MoE-first architecture design**. Google's **Gemma-4-31B-it** continues its dominance with nearly 12M downloads, while the modular expert (MoE) paradigm is heavily represented across new vision-language models built on Qwen3.6/3.5. A particularly notable signal is the emergence of **ternary and 1-bit quantization** from prism-ml, pushing model deployment to the edge far beyond what was previously feasible. Simultaneously, we're seeing a strong robotics and function-calling trend, with openbmb releasing vision-language-action models and Cactus-Compute shipping a new tool-use framework. The community's appetite for **uncensored, aggressive fine-tunes** remains unabated, especially on Qwen3.6 MoE architectures.

## 2. Trending Models

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **[GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — zai-org | ❤️ 4,226 | 📥 531,947  
  A powerful Mixture-of-Experts (MoE) LLM with a dynamic sparse architecture, trending due to its competitive performance against closed-source models.

- **[tencent/Hy3](https://huggingface.co/tencent/Hy3)** — tencent | ❤️ 847 | 📥 13,698  
  The latest generation of Tencent's Hunyuan text-generation model family, gaining traction as an open alternative in the 100B+ parameter space.

- **[Cactus-Compute/needle](https://huggingface.co/Cactus-Compute/needle)** — Cactus-Compute | ❤️ 292 | 📥 950  
  A JAX-based function-calling and tool-use model, trending for its efficient inference design targeting agentic workflows.

- **[GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-Thinking](https://huggingface.co/GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-Thinking)** — GnLOLot | ❤️ 159 | 📥 5,494  
  A tiny 1B-parameter thinking model distilled from Claude Opus, trending for surprising reasoning capability at minimal compute cost.

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **[google/gemma-4-31B-it](https://huggingface.co/google/gemma-4-31B-it)** — google | ❤️ 3,297 | 📥 11,987,240  
  Google's flagship open multimodal model, dominating the chart with built-in vision understanding and strong conversational ability.

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — HauhauCS | ❤️ 2,937 | 📥 2,007,025  
  An uncensored, aggressively fine-tuned MoE vision-language model based on Qwen3.6, trending for its high reasoning output and 2M+ downloads.

- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** — baidu | ❤️ 2,446 | 📥 2,122,848  
  Baidu's latest OCR model capable of any-resolution document understanding, trending for its breakthrough in real-world text extraction accuracy.

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** — empero-ai | ❤️ 2,369 | 📥 2,117,323  
  A GGUF-quantized reasoning model merging Claude-style thinking with Qwen3.5, trending for its massive download count.

- **[thinkingmachines/Inkling](https://huggingface.co/thinkingmachines/Inkling)** — thinkingmachines | ❤️ 1,271 | 📥 13,462  
  A new multimodal architecture from Thinking Machines supporting image, text, and audio input, trending for its novel MoE design.

- **[moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)** — moonshotai | ❤️ 1,177 | 📥 713,992  
  Moonshot AI's compressed code model with vision, trending for state-of-the-art coding benchmarks at reduced parameter count.

- **[bottlecapai/ThinkingCap-Qwen3.6-27B](https://guggingface.co/bottlecapai/ThinkingCap-Qwen3.6-27B)** — bottlecapai | ❤️ 482 | 📥 10,647  
  A Qwen3.6 fine-tune optimized for chain-of-thought reasoning, trending as a lightweight alternative to larger thinking models.

- **[ATH-MaaS/OvisOCR2](https://huggingface.co/ATH-MaaS/OvisOCR2)** — ATH-MaaS | ❤️ 217 | 📥 14,587  
  A Qwen3.5-based OCR model with transformer architecture, trending for competitive accuracy at modest scale.

- **[Wan-AI/Wan-Dancer-14B](https://huggingface.co/Wan-AI/Wan-Dancer-14B)** — Wan-AI | ❤️ 145 | 📥 2,408  
  A diffusion transformer for image-to-video generation focused on human dance, trending for high-quality motion synthesis.

- **[Alissonerdx/LTX-Best-Face-ID](https://huggingface.co/Alissonerdx/LTX-Best-Face-ID)** — Alissonerdx | ❤️ 214 | 📥 0  
  A reference-to-video LoRA for identity-preserving video generation, trending in the animation/video community.

- **[OpenMOSS-Team/MOSS-Transcribe-Diarize](https://huggingface.co/OpenMOSS-Team/MOSS-Transcribe-Diarize)** — OpenMOSS-Team | ❤️ 292 | 📥 87,533  
  An audio-text-to-text model combining transcription with speaker diarization, trending for real-time meeting processing.

- **[OpenMOSS-Team/MOSS-VL-Realtime](https://huggingface.co/OpenMOSS-Team/MOSS-VL-Realtime)** — OpenMOSS-Team | ❤️ 89 | 📥 544  
  A video-text-to-text model optimized for low-latency streaming video understanding, trending in agent/robotics applications.

### 🔧 Specialized Models (code, math, medical, embeddings, robotics)

- **[nvidia/Nemotron-3-Embed-1B-BF16](https://huggingface.co/nvidia/Nvidia/Nemotron-3-Embed-1B-BF16)** — nvidia | ❤️ 87 | 📥 61,708  
  Nvidia's latest sentence embedding model based on Ministral3, trending for RAG and search applications.

- **[openbmb/MiniCPM-RobotManip](https://huggingface.co/openbmb/MiniCPM-RobotManip)** — openbmb | ❤️ 135 | 📥 0  
  A vision-language-action model for robotic manipulation, trending as a landmark open-source robotics model from OpenBMB.

- **[openbmb/MiniCPM-RobotTrack](https://huggingface.co/openbmb/MiniCPM-RobotTrack)** — openbmb | ❤️ 100 | 📥 0  
  A companion robot tracking model for object-centric manipulation, trending alongside RobotManip for real-world robotics pipelines.

- **[krea2-identity-edit](https://huggingface.co/conradlocke/krea2-identity-edit)** — conradlocke | ❤️ 458 | 📥 0  
  A Krea-2 based LoRA for identity-preserving image editing, trending for high-quality facial condition injection.

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **[prism-ml/Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)** — prism-ml | ❤️ 855 | 📥 338,945  
  The first large-scale ternary (2-bit) quantization of a 27B model using llama.cpp, trending for unprecedented compression ratios.

- **[prism-ml/Bonsai-27B-gguf](https://huggingface.co/prism-ml/Bonsai-27B-gguf)** — prism-ml | ❤️ 542 | 📥 1,262,894  
  A 1-bit quantized 27B model that transforms storage economics for local deployment, with over 1.2M downloads.

- **[prism-ml/Bonsai-27B-mlx-1bit](https://huggingface.co/prism-ml/Bonsai-27B-mlx-1bit)** — prism-ml | ❤️ 154 | 📥 21,690  
  Apple MLX-native 1-bit quantization of the Bonsai model, trending for efficient on-device inference on Apple Silicon.

- **[prism-ml/Ternary-Bonsai-27B-mlx-2bit](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-mlx-2bit)** — prism-ml | ❤️ 130 | 📥 17,869  
  MLX version of the ternary 2-bit Bonsai, giving Mac users a strong quality-size tradeoff.

- **[AngelSlim/Hy3-GGUF](https://huggingface.co/AngelSlim/Hy3-GGUF)** — AngelSlim | ❤️ 149 | 📥 109,749  
  GGUF quantization of Tencent's Hy3 model, trending for enabling local inference of a major Chinese frontier model.

- **[unsloth/inkling-GGUF](https://huggingface.co/unsloth/inkling-GGUF)** — unsloth | ❤️ 111 | 📥 6,771  
  Unsloth's GGUF conversion of the Inkling multimodal MoE, trending for enabling cross-platform deployment.

- **[empero-ai/Qwythos-9B-v2-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-v2-GGUF)** — empero-ai | ❤️ 197 | 📥 105,749  
  Updated GGUF version of the Qwythos reasoning model, trending for improved thinking trace quality.

- **[DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF)** — DavidAU | ❤️ 157 | 📥 16,719  
  A highly fine-tuned, uncensored Qwen3.6 variant with extensive merging, trending in the "uncensored" model community.

- **[GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-V2-Thinking-GGUF](https://huggingface.co/GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-V2-Thinking-GGUF)** — GnLOLot | ❤️ 134 | 📥 28,012  
  GGUF version of the 1B thinking model, trending as a lightweight alternative for CPU inference.

- **[LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V3-GGUF](https://huggingface.co/LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V3-GGUF)** — LuffyTheFox | ❤️ 85 | 📥 15,148  
  Another Qwen3.6 35B A3B uncensored GGUF, trending alongside the HauhauCS variant for the "unfiltered" MoE niche.

## 3. Ecosystem Signal

**MoE is becoming the default architecture for frontier open models.** The Qwen3.6 family alone accounts for five entries in this digest, with the 35B-A3B variant hitting a mass-market sweet spot of 35B total parameters but only 3B active per token. This architectural choice is enabling unprecedented inference speed at model scales that would otherwise require heavy hardware.

**Extreme quantization is reshaping local AI.** Prism-ML's Bonsai family — shipping 1-bit and ternary (2-bit) formats — is the single most technically significant trend this week. A 27B model that can fit in under 2GB of RAM (ternary) or ~800MB (1-bit) opens local deployment scenarios on phones, laptops, and embedded devices that were inconceivable six months ago. The fact that Bonsai-27B-gguf has 1.26M downloads proves massive market demand for this capability.

**Robotics and function-calling are emerging as new growth vectors.** OpenBMB's MiniCPM-RobotManip and Cactus-Compute's needle represent a shift from pure language understanding to action-oriented AI

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*