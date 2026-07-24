# Hugging Face Trending Models Digest 2026-07-24

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-07-24 02:16 UTC

---

Here is the structured Hugging Face Trending Models Digest for July 24, 2026.

---

## Hugging Face Trending Models Digest — July 24, 2026

### 1. Today's Highlights

This week's trending models reveal a strong surge in **multimodal vision-language models**, led by Chinese labs and community fine-tuners alike. **zai-org/GLM-5.2** and **google/gemma-4-31B-it** dominate the likes chart, signaling a major competitive push in open-weight, conversational vision models. In parallel, **Qwen3.6** variants are everywhere: uncensored fine-tunes, MoE versions, and highly compressed GGUF quantizations are flooding the hub, underscoring the community's deep engagement with the Qwen family. Notably, **1-bit and ternary quantization** is a breakout trend, with **prism-ml/Bonsai-27B-gguf** and its siblings achieving massive download numbers for extreme compression. Finally, specialized application models—from **NVIDIA's streaming ASR** to **Qwen's new TTS model**—point toward a maturing ecosystem where deployable, task-specific models are gaining traction alongside general-purpose LLMs.

### 2. Trending Models

#### 🧠 Language Models
- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — zai-org | 4,371 likes | 596k downloads  
  A powerful Mixture-of-Experts conversational LLM; trending as a leading open-weight alternative with strong reasoning and MoE efficiency.
- **[upstage/Solar-Open2-250B](https://huggingface.co/upstage/Solar-Open2-250B)** — upstage | 455 likes | 362 downloads  
  A 250B-parameter open LLM from Upstage; notable for its scale, though still early in community adoption.
- **[Nanbeige/Nanbeige4.2-3B](https://huggingface.co/Nanbeige/Nanbeige4.2-3B)** — Nanbeige | 323 likes | 4.5k downloads  
  A compact 3B-parameter Chinese LLM; popular for efficient deployment and high performance on Chinese benchmarks.
- **[Motif-Technologies/Motif-3-Beta](https://huggingface.co/Motif-Technologies/Motif-3-Beta)** — Motif-Technologies | 173 likes | 1.8k downloads  
  A new feature-extraction and text-generation model; gaining interest as a specialized embedding and reasoning tool.
- **[fdtn-ai/antares-1b](https://huggingface.co/fdtn-ai/antares-1b)** — fdtn-ai | 121 likes | 2.7k downloads  
  A 1B-parameter Granite-MoE hybrid focused on security-aware text generation; trending in the AI safety space.

#### 🎨 Multimodal & Generation
- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** — baidu | 2,892 likes | 2.4M downloads  
  A state-of-the-art OCR model from Baidu; trending for near-perfect text extraction across languages and challenging scenes.
- **[thinkingmachines/Inkling](https://huggingface.co/thinkingmachines/Inkling)** — thinkingmachines | 1,508 likes | 24k downloads  
  A conversational vision model designed for human-like image-text interactions; popular for creative and agentic use cases.
- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — HauhauCS | 3,033 likes | 2M downloads  
  An uncensored Qwen3.6 MoE vision model, aggressively fine-tuned; trending for high download velocity in the uncensored community.
- **[google/gemma-4-31B-it](https://huggingface.co/google/gemma-4-31B-it)** — google | 3,347 likes | 12.6M downloads  
  Google's latest visual instruction-tuned model; the most downloaded model this week, signaling strong trust and adoption.
- **[microsoft/Mage-Flow](https://huggingface.co/microsoft/Mage-Flow)** — microsoft | 187 likes | 411 downloads  
  A new text-to-image diffusion pipeline from Microsoft; early-stage but interesting for its image-editing capabilities.
- **[nvidia/Cosmos3-Edge](https://huggingface.co/nvidia/Cosmos3-Edge)** — nvidia | 101 likes | 28k downloads  
  An edge-optimized diffusion model from NVIDIA's Cosmos family; trending for on-device image generation.
- **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)** — nvidia | 926 likes | 750k downloads  
  A streaming automatic speech recognition model; widely adopted for low-latency voice applications.
- **[Qwen/Qwen3-TTS-12Hz-1.7B-CustomVoice](https://huggingface.co/Qwen/Qwen3-TTS-12Hz-1.7B-CustomVoice)** — Qwen | 1,799 likes | 2.5M downloads  
  A custom-voice text-to-speech model from Qwen; trending for high-quality voice cloning with a 12Hz frame rate.
- **[openbmb/MiniCPM-RobotManip](https://huggingface.co/openbmb/MiniCPM-RobotManip)** — openbmb | 165 likes | 408 downloads  
  A Vision-Language-Action model for robotic manipulation; a niche but significant release in embodied AI.
- **[openbmb/MiniCPM-RobotTrack](https://huggingface.co/openbmb/MiniCPM-RobotTrack)** — openbmb | 117 likes | 306 downloads  
  A companion VLA model for robot tracking and trajectory prediction; complements the RobotManip release.

#### 🔧 Specialized Models
- **[moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)** — moonshotai | 1,249 likes | 766k downloads  
  A code-focused compressed transformer from Kimi; popular for efficient code completion and agentic coding.

#### 📦 Fine-tunes & Quantizations
- **[prism-ml/Bonsai-27B-gguf](https://huggingface.co/prism-ml/Bonsai-27B-gguf)** — prism-ml | 620 likes | 1.9M downloads  
  A pioneering 1-bit quantized 27B model; extremely popular for enabling large model inference on consumer hardware.
- **[prism-ml/Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)** — prism-ml | 985 likes | 576k downloads  
  A 2-bit ternary quantization of Bonsai-27B; trending for its balance of size and coherence at extreme compression.
- **[DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF)** — DavidAU | 400 likes | 334k downloads  
  An extensively fine-tuned and uncensored Qwen3.6 variant in GGUF; exemplifies maximalist community fine-tuning.
- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** — empero-ai | 2,439 likes | 2.1M downloads  
  A Qwen3.5-based reasoning model aimed at replicating Claude-like performance, quantized for accessibility.
- **[bottlecapai/ThinkingCap-Qwen3.6-27B](https://huggingface.co/bottlecapai/ThinkingCap-Qwen3.6-27B)** — bottlecapai | 528 likes | 25k downloads  
  A vision-language fine-tune of Qwen3.6 focused on chain-of-thought reasoning; trending for improved multimodal reasoning.
- **[poolside/Laguna-S-2.1-GGUF](https://huggingface.co/poolside/Laguna-S-2.1-GGUF)** — poolside | 112 likes | 25k downloads  
  A GGUF quantized version of the Laguna-S-2.1 text-generation model, plus a variant by unsloth (150 likes, 28k downloads) indicating strong quantization ecosystem support.
- **[prism-ml/Bonsai-27B-mlx-1bit](https://huggingface.co/prism-ml/Bonsai-27B-mlx-1bit)** — prism-ml | 172 likes | 34k downloads  
  An Apple MLX-native 1-bit version of Bonsai; enabling extreme compression on Apple Silicon hardware.
- **[LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V5-GGUF](https://huggingface.co/LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V5-GGUF)** — LuffyTheFox | 117 likes | 24k downloads  
  Another community Qwen3.6 MoE fine-tune in GGUF, combining Hermes-style instruction tuning with uncensored outputs.

### 3. Ecosystem Signal

The current trending landscape reveals a **clear bifurcation between frontier-scale open models and extreme compression**. On the frontier, **Qwen3.6** and **GLM-5.2** are the dominant open-weight families, with dozens of community adapters and GGUF quantizations. The **Qwen3.6-35B-A3B MoE** architecture is particularly viral, offering a strong efficiency-accuracy tradeoff. On the compression side, **1-bit and ternary quantization** (led by prism-ml’s Bonsai series) is a breakout trend, suggesting the community is prioritizing deployment on consumer hardware. Open-weight models continue to outpace proprietary closeouts on the trending chart, with **Google’s Gemma-4** and **Baidu’s OCR** being notable corporate open-source wins. Finally, **specialized audio and robotics models** are gaining a dedicated following, with **NVIDIA’s streaming ASR** and **OpenBMB’s robot VLA models** indicating that the ecosystem is diversifying beyond pure text. The **high volume of uncensored fine-tunes** (DavidAU, HauhauCS, LuffyTheFox) remains a persistent undercurrent, reflecting ongoing demand for unrestricted model behavior.

### 4. Worth Exploring

1. **[google/gemma-4-31B-it](https://huggingface.co/google/gemma-4-31B-it)** — With 12.6 million downloads and 3,347 likes in a single week, this is the clear "must-try" model. It represents Google’s strongest open multimodal offering and is likely the best-balanced 31B vision-language model available for research and commercial use.

2. **[prism-ml/Bonsai-27B-gguf](https://huggingface.co/prism-ml/Bonsai-27B-gguf)** — This 1-bit 27B model is a fascinating technical achievement. It’s worth studying for its novel quantization scheme, which opens the door to running 27B-class models on devices with only 8-16GB of RAM while retaining reasonable coherence.

3. **[openbmb/MiniCPM-RobotManip](https://huggingface.co/openbmb/MiniCPM-RobotManip)** — As one of the first widely-shared Vision-Language-Action (VLA) models on the Hub, this is essential for anyone interested in **embodied AI**. It’s small, open, and represents a new category of model—robotics—that is likely to grow rapidly on Hugging Face.

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*