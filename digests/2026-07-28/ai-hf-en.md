# Hugging Face Trending Models Digest 2026-07-28

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-07-28 02:07 UTC

---

# 🤗 Hugging Face Trending Models Digest – 2026-07-28

## Today's Highlights

This week's top trends are dominated by **large multimodal MoE models**, **extreme quantization**, and **domain-specific OCR/code models**. Moonshot AI's **Kimi‑K3** (6.3K likes) leads as a compressed multimodal MoE, while **GLM‑5.2** (4.5K likes) confirms the shift toward sparse architectures. **Unlimited‑OCR** from Baidu (3.3K likes, 2.6M downloads) shows sustained demand for production OCR. On the quantization front, community Qwen3.6 variants like the **35B‑A3B** base model (2.5K likes, 6.2M downloads) and its many uncensored GGUF derivatives signal a hunger for efficient, customizable MoE. Microsoft’s **Fara1.5‑27B** introduces computer‑use capabilities, and **Mage‑Flow** revives interest in instruction‑based image editing.

---

## Trending Models by Category

### 🧠 Language Models

- **[poolside/Laguna-S-2.1](https://huggingface.co/poolside/Laguna-S-2.1)** – poolside | 758 likes | 63.6K downloads  
  A 2.1‑generation code‑focused LLM by poolside, attracting developers and downstream quantizers.  
- **[upstage/Solar-Open2-250B](https://huggingface.co/upstage/Solar-Open2-250B)** – upstage | 629 likes | 3.8K downloads  
  Upstage’s massive 250B open‑weight LLM, bridging the gap between open and proprietary performance.  
- **[Nanbeige/Nanbeige4.2-3B](https://huggingface.co/Nanbeige/Nanbeige4.2-3B)** – Nanbeige | 493 likes | 16.5K downloads  
  A compact 3B model optimized for efficient inference, popular for on‑device deployment.  
- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** – zai-org | 4.5K likes | 1.0M downloads  
  Zhipu AI’s latest MoE chat model (GLM‑5.2) with dynamic sparse attention, trending for its strong reasoning.  
- **[Motif-Technologies/Motif-3-Beta](https://huggingface.co/Motif-Technologies/Motif-3-Beta)** – Motif-Technologies | 199 likes | 2.5K downloads  
  A feature‑extraction LLM by Motif, gaining attention for representation‑learning applications.  

### 🎨 Multimodal & Generation

- **[moonshotai/Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3)** – moonshotai | 6.3K likes | 2.9K downloads  
  Moonshot’s multimodal MoE (image‑text‑to‑text) with compressed tensors – the week’s most hyped model.  
- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** – baidu | 3.3K likes | 2.6M downloads  
  Production‑grade OCR model from Baidu, processing arbitrary‑length text in images with high accuracy.  
- **[thinkingmachines/Inkling](https://huggingface.co/thinkingmachines/Inkling)** – thinkingmachines | 1.6K likes | 36.2K downloads  
  A conversational image‑text‑to‑text model, trending for its natural multimodal chat abilities.  
- **[Qwen/Qwen3.6-35B-A3B](https://huggingface.co/Qwen/Qwen3.6-35B-A3B)** – Qwen | 2.5K likes | 6.2M downloads  
  The official Qwen3.6 MoE (35B total, 3B active) with vision – the base for dozens of community fine‑tunes.  
- **[microsoft/Mage-Flow](https://huggingface.co/microsoft/Mage-Flow)** – microsoft | 390 likes | 1.7K downloads  
  A text‑to‑image diffusion model for instruction‑based editing, reviving interest in controllable generation.  
- **[microsoft/Mage-Flow-Edit-Turbo](https://huggingface.co/microsoft/Mage-Flow-Edit-Turbo)** – microsoft | 102 likes | 1.1K downloads  
  Faster variant of Mage‑Flow for image‑to‑image editing, optimized for iterative refinement.  
- **[owensong/Inflect-Micro-v2](https://huggingface.co/owensong/Inflect-Micro-v2)** – owensong | 224 likes | 483 downloads  
  A tiny text‑to‑speech model built for CPU and edge deployment, democratizing local TTS.  
- **[microsoft/Fara1.5-27B](https://huggingface.co/microsoft/Fara1.5-27B)** – microsoft | 152 likes | 1.4K downloads  
  A vision‑language model with computer‑use support, allowing models to interact with GUIs – a niche trend.  
- **[nvidia/Cosmos3-Edge](https://huggingface.co/nvidia/Cosmos3-Edge)** – nvidia | 133 likes | 33.1K downloads  
  NVIDIA’s edge‑optimized diffusion model (likely video/vision), targeting on‑device deployment.  

### 🔧 Specialized Models (Code, OCR, Security, Computer‑Use)

- **[moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)** – moonshotai | 1.3K likes | 695.7K downloads  
  A code‑specialized MoE model from Kimi’s lineage, excelling in multi‑language code generation and understanding.  
- **[Kwaipilot/KAT-Coder-V2.5-Dev](https://huggingface.co/Kwaipilot/KAT-Coder-V2.5-Dev)** – Kwaipilot | 242 likes | 5.3K downloads  
  A development‑focused coder based on Qwen3.5 MoE, combining vision and code for GUI‑level tasks.  
- **[ATH-MaaS/OvisOCR2](https://huggingface.co/ATH-MaaS/OvisOCR2)** – ATH-MaaS | 327 likes | 42.2K downloads  
  Another strong OCR model (Qwen3.5‑based), optimized for structured document parsing.  
- **[fdtn-ai/antares-1b](https://huggingface.co/fdtn-ai/antares-1b)** – fdtn-ai | 207 likes | 6.4K downloads  
  A 1B model fine‑tuned for cybersecurity – detecting threats and vulnerabilities with a small footprint.  

### 📦 Fine‑Tunes & Quantizations

- **[DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF)** – DavidAU | 754 likes | 634.1K downloads  
  An uncensored, maximally merged Qwen3.6 MoE fine‑tune in GGUF – a favorite for roleplay and storytelling.  
- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** – HauhauCS | 3.1K likes | 1.9M downloads  
  The most downloaded uncensored Qwen3.6 variant, aggressively fine‑tuned for creative freedom.  
- **[prism-ml/Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)** – prism-ml | 1.1

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*