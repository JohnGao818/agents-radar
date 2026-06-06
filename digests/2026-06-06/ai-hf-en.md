# Hugging Face Trending Models Digest 2026-06-06

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-06-06 02:47 UTC

---

# 🤗 Hugging Face Trending Models Digest — 2026-06-06

## 1. Today's Highlights

The week is dominated by **DeepSeek-V4-Pro** (4,658 likes, 5.6M downloads), cementing DeepSeek’s leadership in open-weight LLMs, alongside its faster sibling **DeepSeek-V4-Flash**. **Sulphur-2-base** (1,566 likes) and **Nvidia’s LocateAnything-3B** (1,379 likes) signal a surge in video generation and visual grounding capabilities. Google’s **Gemma-4-12B-it** introduces a unified any-to-any architecture, while community fine-tunes and quantizations (especially GGUF and NVFP4 variants) of Qwen3.6 and Gemma-4 continue to see heavy adoption. MoE architectures and efficient sparsity are a clear theme across language, vision, and speech models.

## 2. Trending Models by Category

### 🧠 Language Models (LLMs, chat, instruction-tuned)

- **[DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** — DeepSeek’s flagship conversational model, with 4.6K likes and massive downloads, leading the open-weight LLM race.
- **[DeepSeek-V4-Flash](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash)** — A faster, MIT-licensed variant of V4-Pro; 1.4K likes, 3.5M downloads, ideal for production inference.
- **[LiquidAI/LFM2.5-8B-A1B](https://huggingface.co/LiquidAI/LFM2.5-8B-A1B)** — A 8B MoE model (1B active) from Liquid AI, trending for its extreme parameter efficiency.
- **[JetBrains/Mellum2-12B-A2.5B-Thinking](https://huggingface.co/JetBrains/Mellum2-12B-A2.5B-Thinking)** — JetBrains’ MoE thinking model (12B total, 2.5B active), gaining developer interest for reasoning tasks.
- **[openbmb/MiniCPM5-1B](https://huggingface.co/openbmb/MiniCPM5-1B)** — A 1B parameter LLM from OpenBMB, popular as a tiny yet capable baseline.
- **[sapientinc/HRM-Text-1B](https://huggingface.co/sapientinc/HRM-Text-1B)** — A 1B text-generation model specialized for human resource management tasks; 702 likes in a niche domain.
- **[nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-BF16](https://huggingface.co/nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-BF16)** — Nvidia’s massive 550B MoE model (55B active), pushing the boundary of open-weight scale.

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — Nvidia’s 3B model for visual grounding and object localization; 1.4K likes, popular for interactive segmentation.
- **[google/gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it)** — Google’s unified any-to-any instruction model (text, image, audio input/output), a major multimodal release.
- **[google/gemma-4-12B](https://huggingface.co/google/gemma-4-12B)** — The base version of Gemma-4-12B, offering the same any-to-any architecture without instruction tuning.
- **[stepfun-ai/Step-3.7-Flash](https://huggingface.co/stepfun-ai/Step-3.7-Flash)** — A fast vision-language model from Stepfun; 332 likes for efficient multimodal reasoning.
- **[ideogram-ai/ideogram-4-fp8](https://huggingface.co/ideogram-ai/ideogram-4-fp8)** — Ideogram’s latest text-to-image model in FP8 precision, balancing quality and efficiency.
- **[ideogram-ai/ideogram-4-nf4](https://huggingface.co/ideogram-ai/ideogram-4-nf4)** — A 4-bit NF4 version of Ideogram-4 for extremely low memory consumption.
- **[nvidia/Cosmos3-Nano](https://huggingface.co/nvidia/Cosmos3-Nano)** — Nvidia’s small video/omni model from the Cosmos3 family; 176 likes, part of a broader multi-scale video pipeline.
- **[nvidia/Cosmos3-Super](https://huggingface.co/nvidia/Cosmos3-Super)** — The larger Cosmos3 variant for higher-quality video generation.
- **[nvidia/Cosmos3-Super-Text2Image](https://huggingface.co/nvidia/Cosmos3-Super-Text2Image)** — Text-to-image branch of Cosmos3-Super.
- **[nvidia/Cosmos3-Super-Image2Video](https://huggingface.co/nvidia/Cosmos3-Super-Image2Video)** — Image-to-video branch of Cosmos3-Super.
- **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)** — A 0.6B streaming automatic speech recognition model with cache-aware architecture.
- **[nvidia/PiD](https://huggingface.co/nvidia/PiD)** — Nvidia’s diffusion-based super-resolution model (image-to-image), gaining traction for low-light enhancement.
- **[ByteDance/Bernini-R](https://huggingface.co/ByteDance/Bernini-R)** — ByteDance’s image-text-to-video model based on arxiv paper, drawing interest for generative video rendering.
- **[PaddlePaddle/PaddleOCR-VL-1.6](https://huggingface.co/PaddlePaddle/PaddleOCR-VL-1.6)** — An OCR-specific vision-language model from PaddlePaddle; 245 likes for document understanding.
- **[bosonai/higgs-audio-v3-tts-4b](https://huggingface.co/bosonai/higgs-audio-v3-tts-4b)** — A 4B text-to-speech model built on Qwen architecture; trending for high-quality multilingual synthesis.
- **[meituan-longcat/LongCat-Video-Avatar-1.5](https://huggingface.co/meituan-longcat/LongCat-Video-Avatar-1.5)** — Audio+text-to-video avatar model from Meituan; 519 likes for personalized talking head generation.
- **[SulphurAI/Sulphur-2-base](https://huggingface.co/SulphurAI/Sulphur-2-base)** — A text-to-video model with 1.5K likes, built on LTX-2.3, emerging as a top open-source video generator.
- **[MisoLabs/MisoTTS](https://huggingface.co/MisoLabs/MisoTTS)** — A fresh TTS model from MisoLabs; zero downloads yet but 111 likes, hinting at strong early interest.

### 🔧 Specialized Models (code, math, medical, embeddings)

*(No models on this list are purely specialized. LocateAnything and PaddleOCR are included in Multimodal above.)*

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ, NVFP4)

- **[unsloth/gemma-4-12b-it-GGUF](https://huggingface.co/unsloth/gemma-4-12b-it-GGUF)** — GGUF quantization of Gemma-4-12B-it by Unsloth; 379 likes, 296K downloads, the most efficient way to run Gemma-4 locally.
- **[HauhauCS/Qwen3.6-35B-A3

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*