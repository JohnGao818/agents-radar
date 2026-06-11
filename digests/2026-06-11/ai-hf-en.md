# Hugging Face Trending Models Digest 2026-06-11

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-06-11 03:33 UTC

---

# Hugging Face Trending Models Digest — 2026-06-11

## Today's Highlights

**DeepSeek-V4-Pro** dominates the board with 4,762 weekly likes and over 4 million downloads, cementing its position as the week's most significant release. The **Gemma-4 family** continues to expand rapidly, with Google's official 12B and 26B models spawning a rich ecosystem of GGUF quantizations from Unsloth, abliterated variants, and diffusion-integrated versions. **Nvidia** shows remarkable breadth, releasing across vision-language (LocateAnything-3B, 1,809 likes), streaming ASR (Nemotron-3.5), and the massive 550B Nemotron-3 Ultra — signaling a major push across modalities. Multimodal models are clearly the week's theme, with image-text-to-text, text-to-image, text-to-speech, and even image-text-to-video (ByteDance's Bernini-R) all represented prominently.

---

## Trending Models by Category

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **[DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** — deepseek-ai | 4,762 likes | 4,061,006 downloads  
  The new frontier model from DeepSeek, dominating both likes and downloads with strong conversational performance.

- **[nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-BF16](https://huggingface.co/nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-BF16)** — nvidia | 189 likes | 59,066 downloads  
  Nvidia's flagship 550B-parameter MoE model (55B active) for text generation, signaling the enterprise model race.

- **[nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-NVFP4](https://huggingface.co/nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-NVFP4)** — nvidia | 158 likes | 91,117 downloads  
  A 4-bit NVFP4 quantized variant of the Nemotron-3 Ultra, making the massive model more accessible.

- **[CohereLabs/North-Mini-Code-1.0](https://huggingface.co/CohereLabs/North-Mini-Code-1.0)** — CohereLabs | 263 likes | 1,859 downloads  
  Cohere's code-focused MoE model, extending their North family into the coding domain.

- **[sapientinc/HRM-Text-1B](https://huggingface.co/sapientinc/HRM-Text-1B)** — sapientinc | 741 likes | 134,752 downloads  
  A specialized 1B text-generation model for HRM (Human Resource Management) domain tasks.

- **[LiquidAI/LFM2.5-8B-A1B](https://huggingface.co/LiquidAI/LFM2.5-8B-A1B)** — LiquidAI | 584 likes | 142,134 downloads  
  Liquid's latest 8B MoE model (1B active), gaining traction for efficient inference with solid performance.

- **[JetBrains/Mellum2-12B-A2.5B-Thinking](https://huggingface.co/JetBrains/Mellum2-12B-A2.5B-Thinking)** — JetBrains | 281 likes | 18,273 downloads  
  JetBrains' MoE model with explicit "thinking" capabilities, targeting developer tooling use cases.

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — HauhauCS | 1,637 likes | 3,057,541 downloads  
  An uncensored, aggressively fine-tuned Qwen 3.6 MoE variant with vision, extremely popular for its niche.

- **[nex-agi/Nex-N2-Pro](https://huggingface.co/nex-agi/Nex-N2-Pro)** — nex-agi | 181 likes | 1,185 downloads  
  A pro-tier MoE model built on Qwen 3.5 architecture with vision-language capabilities.

- **[nex-agi/Nex-N2-mini](https://huggingface.co/nex-agi/Nex-N2-mini)** — nex-agi | 136 likes | 1,222 downloads  
  Smaller sibling of Nex-N2-Pro, offering a lighter footprint for vision-language tasks.

---

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **[google/gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it)** — google | 891 likes | 675,936 downloads  
  Google's flagship multimodal Gemma-4 instruction model, supporting any-to-any inputs and outputs.

- **[google/gemma-4-12B](https://huggingface.co/google/gemma-4-12B)** — google | 504 likes | 140,221 downloads  
  The base (non-instruction) Gemma-4 12B model, serving as the foundation for fine-tunes and quantizations.

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — nvidia | 1,809 likes | 131,794 downloads  
  A 3B vision-language model specialized in image feature extraction and object localization, trending for its niche precision.

- **[google/diffusiongemma-26B-A4B-it](https://huggingface.co/google/diffusiongemma-26B-A4B-it)** — google | 266 likes | 0 downloads  
  A novel diffusion-integrated Gemma variant (26B total, 4B active) blending generative and diffusion capabilities.

- **[ideogram-ai/ideogram-4-fp8](https://huggingface.co/ideogram-ai/ideogram-4-fp8)** — ideogram-ai | 474 likes | 7,170 downloads  
  The latest Ideogram text-to-image model in FP8 precision, pushing image generation quality.

- **[ideogram-ai/ideogram-4-nf4](https://huggingface.co/ideogram-ai/ideogram-4-nf4)** — ideogram-ai | 309 likes | 6,124 downloads  
  A 4-bit NF4 quantized version of Ideogram-4 for reduced memory footprint.

- **[bosonai/higgs-audio-v3-tts-4b](https://huggingface.co/bosonai/higgs-audio-v3-tts-4b)** — bosonai | 326 likes | 19,948 downloads  
  A 4B text-to-speech model with multimodal backbone, advancing audio generation quality.

- **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)** — nvidia | 350 likes | 4,965 downloads  
  A 600M streaming ASR model with cache-aware architecture, enabling real-time speech recognition.

- **[google/magenta-realtime-2](https://huggingface.co/google/magenta-realtime-2)** — google | 174 likes | 19,806 downloads  
  Google's latest real-time text-to-audio model for music and sound generation, leveraging TFLite.

- **[MisoLabs/MisoTTS](https://huggingface.co/MisoLabs/MisoTTS)** — MisoLabs | 186 likes | 0 downloads  
  A new text-to-speech model for speech synthesis, freshly released with zero downloads yet.

- **[ByteDance/Bernini-R](https://huggingface.co/ByteDance/Bernini-R)** — ByteDance | 213 likes | 305 downloads  
  ByteDance's image-text-to-video generation model, pushing into AI video creation.

- **[stepfun-ai/Step-3.7-Flash](https://huggingface.co/stepfun-ai/Step-3.7-Flash)** — stepfun-ai | 363 likes | 50,187 downloads  
  A vision-language model from Stepfun, optimized for efficient image-text-to-text tasks.

---

### 🔧 Specialized Models (code, math, medical, embeddings)

- **[stepfun-ai/Step-3.7-Flash](https://huggingface.co/stepfun-ai/Step-3.7-Flash)** — already listed in multimodal, but also serves as a specialized vision-language model.

---

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **[unsloth/gemma-4-12b-it-GGUF](https://huggingface.co/unsloth/gemma-4-12b-it-GGUF)** — unsloth | 551 likes | 711,706 downloads  
  Unsloth's GGUF quantization of Gemma-4-12B-it, the most downloaded Gemma variant, enabling local execution.

- **[unsloth/gemma-4-12B-it-qat-GGUF](https://huggingface.co/unsloth/gemma-4-12B-it-qat-GGUF)** — unsloth | 191 likes | 148,252 downloads  
  QAT-enhanced GGUF quantization of Gemma-4, offering improved accuracy retention after compression.

- **[unsloth/gemma-4-26B-A4B-it-qat-GGUF](https://huggingface.co/unsloth/gemma-4-26B-A4B-it-qat-GGUF)** — unsloth | 132 likes | 129,110 downloads  
  GGUF quantization of the larger Gemma-4 26B MoE variant with QAT, bringing server-class models to consumer hardware.

- **[unsloth/diffusiongemma-26B-A4B-it-GGUF](https://huggingface.co/unsloth/diffusiongemma-26B-A4B-it-GGUF)** — unsloth | 97 likes | 0 downloads  
  First GGUF quantization of the diffusion-gemma hybrid, freshly uploaded.

- **[google/gemma-4-12B-it-qat-q4_0-gguf](https://huggingface.co/google/gemma-4-12B-it-qat-q4_0-gguf)** — google | 124 likes | 96,749 downloads  
  Google's own officially released GGUF of Gemma-4 with QAT and q4_0 quantization, competing with community conversions.

- **[OBLITERATUS/Gemma-4-12B-OBLITERATED](https://huggingface.co/OBLITERATUS/Gemma-4-12B-OBLITERATED)** — OBLITERATUS | 215 likes | 14,838 downloads  
  A heavily modified "obliterated" fine-tune of Gemma-4, removing safety guardrails for niche use cases.

- **[huihui-ai/Huihui-gemma-4-12B-it-abliterated](https://huggingface.co/huihui-ai/Huihui-gemma-4-12B-it-abliterated)** — huihui-ai | 136 likes | 6,400 downloads  
  An "abliterated" (safety-removed) variant of Gemma-4-12B-it, representing the ongoing uncensoring trend.

- **[Comfy-Org/Ideogram-4](https://huggingface.co/Comfy-Org/Ideogram-4)** — Comfy-Org | 128 likes | 0 downloads  
  ComfyUI integration for Ideogram-4, enabling workflow-based image generation.

---

## Ecosystem Signal

**The Gemma-4 ecosystem is the week's dominant narrative.** Google's release of the Gemma-4 family (12B dense and 26B MoE, both any-to-any multimodal) has triggered a massive wave of quantization, fine-tuning, and abliteration activity. Unsloth alone accounts for five Gemma-4 GGUF variants in the top 30, suggesting the community is rallying around Gemma as an accessible open-weight alternative to proprietary multimodal models.

**MoE (Mixture of Experts) architecture continues to win.** Nearly all models with scale notation (e.g., 26B-A4B, 35B-A3B, 550B-A55B) use MoE, indicating the industry has standardized on activation-parasitic compute for cost-efficient inference. Even small models like LiquidAI's 8B-A1B embrace MoE.

**Open-weight leaders are consolidating.** Google (Gemma), DeepSeek (V4), Nvidia (Nemotron), and ByteDance (Bernini-R) are releasing competitive open-weight models, while proprietary options are largely absent from trending. The fine-tuning community is actively modifying these with uncensored and abliterated variants.

**Multimodal is no longer optional — it's the default.** The majority of top models support image-text-to-text pipelines or beyond (any-to-any). Even traditionally text-only categories (code, HRM) are being augmented with vision abilities.

---

## Worth Exploring

1. **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — With 1,809 likes as a specialized 3B model, this represents a shift toward *focused, task-specific* vision models rather than monolithic generalists. It's worth studying for anyone building image feature extraction pipelines, as its efficiency-to-accuracy ratio appears to resonate strongly with practitioners.

2. **[google/diffusiongemma-26B-A4B-it](https://huggingface.co/google/diffusiongemma-26B-A4B-it)** — Although it has zero downloads, this model represents an architectural innovation: directly combining diffusion and transformer-based generation in a single MoE. It's a research signal worth monitoring for the next generation of generative models that may unify understanding and generation.

3. **[ByteDance/Bernini-R](https://huggingface.co/ByteDance/Bernini-R)** — As one of the few image-text-to-video models on the list, Bernini-R points to where the next wave of generative AI is heading. With Apache-2.0 licensing and rising interest (213 likes on 305 downloads), this is a strong candidate for early adoption in video generation workflows.

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*