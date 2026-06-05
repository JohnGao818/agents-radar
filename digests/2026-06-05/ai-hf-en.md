# Hugging Face Trending Models Digest 2026-06-05

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-06-05 03:25 UTC

---

# Hugging Face Trending Models Digest — 2026-06-05

## Today’s Highlights
This week’s top releases reflect a strong push toward **multimodal unification** and **efficient MoE architectures**. DeepSeek-V4-Pro dominates with 4,632 likes and 5.7M downloads, while NVIDIA’s *Cosmos3* omni ecosystem and *LocateAnything-3B* signal growing investment in open, task-agnostic models. Video generation surges with **Sulphur-2-base** (1,549 likes) and ByteDance’s *Bernini-R*, while the quantization ecosystem (GGUF, NVFP4) remains the primary vehicle for community adoption. Notably, **uncensored fine-tunes** (Qwen3.6-35B-A3B-Uncensored) and **thinking models** (JetBrains Mellum2) indicate a trend toward specialized alignment and reasoning.

---

## Trending Models

### 🧠 Language Models (LLMs, chat, conversational, thinking)

- **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)**  
  Author: deepseek-ai · Likes: 4,632 · Downloads: 5,687,031  
  Flagship mixture-of-experts LLM pushing open‑weight performance; #1 by likes this week.

- **[deepseek-ai/DeepSeek-V4-Flash](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash)**  
  Author: deepseek-ai · Likes: 1,402 · Downloads: 3,503,796  
  A smaller, faster variant of DeepSeek-V4 for efficient deployment, licensed MIT.

- **[LiquidAI/LFM2.5-8B-A1B](https://huggingface.co/LiquidAI/LFM2.5-8B-A1B)**  
  Author: LiquidAI · Likes: 513 · Downloads: 72,114  
  8B‑parameter active‑1B MoE model optimized for edge and low‑latency inference.

- **[JetBrains/Mellum2-12B-A2.5B-Thinking](https://huggingface.co/JetBrains/Mellum2-12B-A2.5B-Thinking)**  
  Author: JetBrains · Likes: 204 · Downloads: 12,157  
  A 12B‑total / 2.5B‑active thinking model designed for conversational reasoning and coding assistance.

- **[openbmb/MiniCPM5-1B](https://huggingface.co/openbmb/MiniCPM5-1B)**  
  Author: openbmb · Likes: 768 · Downloads: 79,427  
  Ultra‑compact 1B text‑generation model using a Llama‑style architecture, ideal for mobile and research.

- **[sapientinc/HRM-Text-1B](https://huggingface.co/sapientinc/HRM-Text-1B)**  
  Author: sapientinc · Likes: 619 · Downloads: 157,457  
  Lightweight 1B parameter text model for general‑purpose generation, gaining traction for its efficiency.

---

### 🎨 Multimodal & Generation (image, video, audio, text‑to‑X, any‑to‑any)

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)**  
  Author: nvidia · Likes: 1,294 · Downloads: 91,834  
  Vision‑language model (image‑text‑to‑text) for zero‑shot object localization and feature extraction.

- **[google/gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it)**  
  Author: google · Likes: 430 · Downloads: 14,866  
  Instruction‑tuned any‑to‑any model from Google’s Gemma-4 family, handling text, image, and beyond.

- **[google/gemma-4-12B](https://huggingface.co/google/gemma-4-12B)**  
  Author: google · Likes: 277 · Downloads: 1,978  
  Base version of Gemma‑4‑12B with any‑to‑any capabilities, a foundation for multimodal applications.

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)**  
  Author: HauhauCS · Likes: 1,409 · Downloads: 2,646,756  
  Community fine‑tune of Qwen3.6 (35B MoE) removing safety filters and adding an “aggressive” style.

- **[stepfun-ai/Step-3.7-Flash](https://huggingface.co/stepfun-ai/Step-3.7-Flash)**  
  Author: stepfun-ai · Likes: 252 · Downloads: 22,715  
  Compact vision‑language MoE model with strong efficiency for image–text understanding.

- **[ideogram-ai/ideogram-4-fp8](https://huggingface.co/ideogram-ai/ideogram-4-fp8)**  
  Author: ideogram-ai · Likes: 212 · Downloads: 310  
  FP8 quantized version of Ideogram 4 text‑to‑image model for reduced memory.

- **[ideogram-ai/ideogram-4-nf4](https://huggingface.co/ideogram-ai/ideogram-4-nf4)**  
  Author: ideogram-ai · Likes: 164 · Downloads: 398  
  NF4 quantized variant of Ideogram 4, trading quality for further compression.

- **[nvidia/Cosmos3-Nano](https://huggingface.co/nvidia/Cosmos3-Nano)**  
  Author: nvidia · Likes: 166 · Downloads: 17,903  
  Smallest model in NVIDIA’s Cosmos3 omni ecosystem, supporting multiple modalities (text, image, video).

- **[nvidia/Cosmos3-Super](https://huggingface.co/nvidia/Cosmos3-Super)**  
  Author: nvidia · Likes: 134 · Downloads: 16,767  
  Larger Cosmos3 variant targeting higher‑quality omni‑modal generation.

- **[nvidia/Cosmos3-Super-Text2Image](https://huggingface.co/nvidia/Cosmos3-Super-Text2Image)**  
  Author: nvidia · Likes: 108 · Downloads: 961  
  Text‑to‑image specialization built on the Cosmos3‑Super backbone.

- **[nvidia/Cosmos3-Super-Image2Video](https://huggingface.co/nvidia/Cosmos3-Super-Image2Video)**  
  Author: nvidia · Likes: 102 · Downloads: 899  
  Image‑conditioned video generation model, part of the Cosmos3 family.

- **[meituan-longcat/LongCat-Video-Avatar-1.5](https://huggingface.co/meituan-longcat/LongCat-Video-Avatar-1.5)**  
  Author: meituan-longcat · Likes: 516 · Downloads: 381  
  Audio‑text‑to‑video model for generating talking avatars with synchronized speech.

- **[nvidia/PiD](https://huggingface.co/nvidia/PiD)**  
  Author: nvidia · Likes: 303 · Downloads: 852  
  Image‑to‑image super‑resolution model using diffusion with Perceptual‑interactive Denoising.

- **[ByteDance/Bernini-R](https://huggingface.co/ByteDance/Bernini-R)**  
  Author: ByteDance · Likes: 123 · Downloads: 129  
  Image‑text‑to‑video renderer (Apache‑2.0), notable for its open license and research potential.

- **[SulphurAI/Sulphur-2-base](https://huggingface.co/SulphurAI/Sulphur-2-base)**  
  Author: SulphurAI · Likes: 1,549 · Downloads: 1,678,259  
  Text‑to‑video diffusion model built on LTX‑2.3, trending for high‑quality video generation.

- **[NemoStation/Marlin-2B](https://huggingface.co/NemoStation/Marlin-2B)**  
  Author: NemoStation · Likes: 518 · Downloads: 18,942  
  Video‑text‑to‑text model (2B) based on Qwen3.5, supporting video understanding tasks.

- **[PaddlePaddle/PaddleOCR-VL-1.6](https://huggingface.co/PaddlePaddle/PaddleOCR-VL-1.6)**  
  Author: PaddlePaddle · Likes: 233 · Downloads: 5,970  
  Vision‑language OCR model powered by ERNIE4.5, excels at document and scene text recognition.

---

### 🔧 Specialized Models (speech, OCR, super‑resolution, embeddings)

- **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)**  
  Author: nvidia · Likes: 119 · Downloads: 225  
  Streaming automatic speech recognition model with cache‑aware architecture for low‑latency ASR.

- **[OpenMOSS-Team/MOSS-TTS-v1.5](https://huggingface.co/OpenMOSS-Team/MOSS-TTS-v1.5)**  
  Author: OpenMOSS-Team · Likes: 145 · Downloads: 28,331  
  Chinese text‑to‑speech model with customizable delay synthesis, increasingly adopted for TTS pipelines.

---

### 📦 Fine‑tunes & Quantizations (GGUF, NVFP4, community adaptations)

- **[unsloth/gemma-4-12b-it-GGUF](https://huggingface.co/unsloth/gemma-4-12b-it-GGUF)**  
  Author: unsloth · Likes: 299 · Downloads: 62,850  
  GG

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*