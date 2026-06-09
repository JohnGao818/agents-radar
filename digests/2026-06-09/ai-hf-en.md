# Hugging Face Trending Models Digest 2026-06-09

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-06-09 02:45 UTC

---

Here is the **Hugging Face Trending Models Digest** for June 9, 2026.

---

## 🤗 Hugging Face Trending Models Digest
**Date:** 2026-06-09

### 1. Today's Highlights

The ecosystem is dominated by two massive releases: **DeepSeek-V4** and **Google Gemma 4**. DeepSeek-V4 Pro (4.7k likes) is the week's most viral model, while the Gemma 4 family (12B and 26B variants) has spawned the highest concentration of derivative quantized and fine-tuned versions, particularly from **unsloth** and **Google** itself. Multimodal is no longer a niche—models like **NVIDIA's LocateAnything-3B** (1.6k likes) and **ByteDance's Bernini-R** for image-to-video are capturing significant attention. Notably, the week also saw the emergence of a 550B-parameter MoE behemoth from NVIDIA, alongside a strong push in video generation (Sulphur-2, JoyAI-Echo) and audio (TTS, streaming ASR).

### 2. Trending Models by Category

#### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **[DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** — *deepseek-ai* · 4,723 likes · 5.4M downloads  
  The week's runaway hit: a massive dense conversational model representing DeepSeek's next-gen flagship, trending for its sheer scale and performance.  
- **[DeepSeek-V4-Flash](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash)** — *deepseek-ai* · 1,449 likes · 3.3M downloads  
  The faster, lighter sibling of V4 Pro; trending for offering near-flagship quality with lower inference cost.  
- **[nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-BF16](https://huggingface.co/nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-BF16)** — *nvidia* · 167 likes · 55.9K downloads  
  A 550B-parameter MoE model (55B active) from NVIDIA's Nemotron-3 family, trending as one of the largest open-weight models available.  
- **[nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-NVFP4](https://huggingface.co/nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-NVFP4)** — *nvidia* · 145 likes · 66.2K downloads  
  The NVFP4 quantized version of the Nemotron-3 Ultra, enabling massive model deployment on limited hardware.  
- **[LiquidAI/LFM2.5-8B-A1B](https://huggingface.co/LiquidAI/LFM2.5-8B-A1B)** — *LiquidAI* · 551 likes · 135K downloads  
  A 1B active-parameter MoE model from Liquid AI, trending for its outstanding efficiency-to-quality ratio.  
- **[JetBrains/Mellum2-12B-A2.5B-Thinking](https://huggingface.co/JetBrains/Mellum2-12B-A2.5B-Thinking)** — *JetBrains* · 260 likes · 17.4K downloads  
  A 12B parameter "thinking" model from JetBrains, trending for its focus on reasoning and conversational quality.  
- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — *HauhauCS* · 1,554 likes · 3.0M downloads  
  An uncensored MoE vision-language model based on Qwen3.6, trending for its aggressive, unfiltered output and high download count.  
- **[nex-agi/Nex-N2-Pro](https://huggingface.co/nex-agi/Nex-N2-Pro)** — *nex-agi* · 125 likes · 716 downloads  
  A MoE image-text-to-text model, early-stage but gaining traction in the multimodal LLM space.  
- **[sapientinc/HRM-Text-1B](https://huggingface.co/sapientinc/HRM-Text-1B)** — *sapientinc* · 728 likes · 164K downloads  
  A specialized 1B text-generation model for HRM (Human Resource Management) tasks, trending for its narrow but high-value domain focus.  

#### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — *nvidia* · 1,628 likes · 122K downloads  
  A vision-language model for object localization and feature extraction, trending for its "locate anything" capability and NVIDIA's ecosystem push.  
- **[ideogram-ai/ideogram-4-fp8](https://huggingface.co/ideogram-ai/ideogram-4-fp8)** — *ideogram-ai* · 394 likes · 5.5K downloads  
  The FP8 quantized version of Ideogram-4, trending as a high-quality, low-footprint text-to-image diffusion model.  
- **[ideogram-ai/ideogram-4-nf4](https://huggingface.co/ideogram-ai/ideogram-4-nf4)** — *ideogram-ai* · 262 likes · 5.0K downloads  
  The NF4 quantized variant of Ideogram-4 for extreme memory efficiency while retaining generation quality.  
- **[ByteDance/Bernini-R](https://huggingface.co/ByteDance/Bernini-R)** — *ByteDance* · 186 likes · 278 downloads  
  An image-text-to-video generation model from ByteDance, trending for its novel "Bernini Renderer" approach and Apache 2.0 license.  
- **[SulphurAI/Sulphur-2-base](https://huggingface.co/SulphurAI/Sulphur-2-base)** — *SulphurAI* · 1,601 likes · 1.7M downloads  
  A text-to-video base model built on LTX-2.3, trending for its strong community adoption and high download volume.  
- **[nvidia/Cosmos3-Nano](https://huggingface.co/nvidia/Cosmos3-Nano)** — *nvidia* · 206 likes · 34.1K downloads  
  The small variant of NVIDIA's Cosmos3 omnimodal model, trending as an accessible entry point to the Cosmos ecosystem.  
- **[nvidia/Cosmos3-Super](https://huggingface.co/nvidia/Cosmos3-Super)** — *nvidia* · 158 likes · 27.5K downloads  
  The high-capacity version of Cosmos3, offering superior generative performance across multiple modalities.  
- **[jdopensource/JoyAI-Echo](https://huggingface.co/jdopensource/JoyAI-Echo)** — *jdopensource* · 103 likes · 4.1K downloads  
  A text-to-video model with integrated audio-video generation capabilities, trending for its unified generation approach.  
- **[google/magenta-realtime-2](https://huggingface.co/google/magenta-realtime-2)** — *google* · 152 likes · 17.5K downloads  
  Google's next-gen real-time text-to-audio generation model, trending for its low latency and Musical AI applications.  
- **[bosonai/higgs-audio-v3-tts-4b](https://huggingface.co/bosonai/higgs-audio-v3-tts-4b)** — *bosonai* · 251 likes · 15.0K downloads  
  A 4B multimodal TTS model, trending for its high-quality speech synthesis integrated with the Higgs Qwen3 framework.  
- **[stepfun-ai/Step-3.7-Flash](https://huggingface.co/stepfun-ai/Step-3.7-Flash)** — *stepfun-ai* · 352 likes · 45.5K downloads  
  A vision-language model from Stepfun, trending as the latest in the "Step" series with image-text-to-text capabilities.  

#### 🔧 Specialized Models (code, math, medical, embeddings, ASR, OCR)

- **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)** — *nvidia* · 293 likes · 4.0K downloads  
  A 0.6B streaming ASR model from NVIDIA, trending for its cache-aware streaming architecture for real-time speech recognition.  
- **[PaddlePaddle/PaddleOCR-VL-1.6](https://huggingface.co/PaddlePaddle/PaddleOCR-VL-1.6)** — *PaddlePaddle* · 277 likes · 9.9K downloads  
  The latest PaddleOCR vision-language model (based on ERNIE 4.5), trending for its strong OCR and document understanding performance.  
- **[MisoLabs/MisoTTS](https://huggingface.co/MisoLabs/MisoTTS)** — *MisoLabs* · 156 likes · 0 downloads  
  A TTS model fresh on the hub, gaining likes for its speech synthesis quality despite zero downloads (recent upload).  

#### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **[unsloth/gemma-4-12b-it-GGUF](https://huggingface.co/unsloth/gemma-4-12b-it-GGUF)** — *unsloth* · 504 likes · 645K downloads  
  The community's go-to GGUF quantization of Gemma 4 12B-it, trending for making the model accessible on consumer hardware.  
- **[unsloth/gemma-4-12B-it-qat-GGUF](https://huggingface.co/unsloth/gemma-4-12B-it-qat-GGUF)** — *unsloth* · 147 likes · 121K downloads  
  A QAT (Quantization-Aware Training) GGUF version of Gemma 4, trending for better quality-retention during quantization.  
- **[unsloth/gemma-4-26B-A4B-it-qat-GGUF](https://huggingface.co/unsloth/gemma-4-26B-A4B-it-qat-GGUF)** — *unsloth* · 104 likes · 87.5K downloads  
  The 26B variant of Gemma 4 in QAT-GGUF format, trending as the larger, more capable alternative to the 12B.  
- **[google/gemma-4-12B-it-qat-q4_0-gguf](https://huggingface.co/google/gemma-4-12B-it-qat-q4_0-gguf)** — *google* · 101 likes · 52.4K downloads  
  Google's official QAT-quantized Gemma 4 12B, trending for being first-party optimized and ready-to-run.  
- **[unsloth/Qwen3.6-27B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)** — *unsloth* · 696 likes · 1.2M downloads  
  Unsloth's GGUF adaptation of Qwen 3.6 (27B), trending for its high download count and enabling local deployment of a powerful MoE model.  

---

### 3. Ecosystem Signal

The most dominant signal this week is the **ascendancy of DeepSeek-V4**—its Pro and Flash variants collectively drove ~8.7M downloads and 6.2k likes, signaling a clear shift in community preference toward Chinese-origin open-weight LLMs. Meanwhile, **Google's Gemma 4** has become the most **quantized and fine-tuned** model family on the leaderboard, with at least six derivative versions across GGUF, QAT, and official quantized formats. This suggests a maturing "model-as-platform" pattern where the community standardizes on a few base architectures.

The **rise of massive MoE models** is unmistakable: NVIDIA's Nemotron-3 Ultra (550B total, 55B active) and LFM2.5 (8B total, 1B active) represent both ends of the MoE spectrum. The release of **Qwen3.6-35B and Qwen3.6-27B** GGUF variants indicates Qwen 3.5/3.6 is consolidating as a strong alternative to the Llama family. Finally, **video generation** is hot: Sulphur-2's 1.7M downloads and ByteDance's Bernini-R signal that text-to-video is moving from experimental to practical deployment.

### 4. Worth Exploring

1. **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — This model represents a growing niche: **open-vocabulary object localization**. With 1.6k likes and a clear "locate anything" value proposition, it is ideal for vision researchers and robotics applications who need a capable perception model without training from scratch.

2. **[ByteDance/Bernini-R](https://huggingface.co/ByteDance/Bernini-R)** — Emerging as a dark horse in image-to-video generation, Bernini-R's **Apache 2.0 license** and novel renderer architecture make it a must-study for anyone working on controllable video synthesis. Despite low downloads, its academic and license-friendly nature is notable.

3. **[JetBrains/Mellum2-12B-A2.5B-Thinking](https://huggingface.co/JetBrains/Mellum2-12B-A2.5B-Thinking)** — JetBrains is better known for IDEs than AI; this model's focus on "thinking" (extended reasoning) in a compact 12B-2.5B MoE format is worth evaluating for **code generation and multi-step reasoning** tasks, potentially offering a more efficient alternative to larger chain-of-thought models.

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*