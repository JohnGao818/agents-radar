# Hugging Face Trending Models Digest 2026-06-21

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-06-21 03:43 UTC

---

# Hugging Face Trending Models Digest — 2026-06-21

## Today's Highlights

This week's trending models are dominated by massive MoE architectures and multimodal systems. **DeepSeek-V4-Pro** tops the charts with nearly 5,000 likes, signaling strong community interest in next-generation conversational AI. Google's **DiffusionGemma-26B-A4B-it** and **Gemma-4-12B-it** continue to push multimodal boundaries, while NVIDIA’s **LocateAnything-3B** introduces a novel image-feature extraction paradigm. The surge in GGUF quantizations—particularly for MoE models like Qwen3.6 and Kimi K2.7—reflects growing demand for accessible, local deployment of large, sparse models.

---

## Trending Models

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **[DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** — deepseek-ai | 4,987 likes, 2.8M downloads
  A next-gen conversational LLM with massive community traction, likely due to strong reasoning benchmarks and open-weight availability.

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — zai-org | 1,702 likes, 19.7K downloads
  A Mixture-of-Experts chat model from Zhipu AI, trending for its efficient MoE-DSA architecture and strong conversational quality.

- **[WeiboAI/VibeThinker-3B](https://huggingface.co/WeiboAI/VibeThinker-3B)** — WeiboAI | 515 likes, 16.3K downloads
  A compact 3B Qwen2-based model specialized in math reasoning, gaining attention for its efficiency in resource-constrained settings.

- **[microsoft/FastContext-1.0-4B-SFT](https://huggingface.co/microsoft/FastContext-1.0-4B-SFT)** — microsoft | 245 likes, 2.0K downloads
  A Qwen3-based model with an "Explorer SubAgent" capability, designed for long-context reasoning and agentic workflows.

- **[CohereLabs/North-Mini-Code-1.0](https://huggingface.co/CohereLabs/North-Mini-Code-1.0)** — CohereLabs | 468 likes, 18.8K downloads
  A Cohere2 MoE model optimized for code generation, filling the niche for efficient coding assistants.

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **[MiniMaxAI/MiniMax-M3](https://huggingface.co/MiniMaxAI/MiniMax-M3)** — MiniMaxAI | 1,163 likes, 85.8K downloads
  A multimodal vision-language model with strong image-text-to-text performance, popular for its open-source release and comedic legacy.

- **[google/diffusiongemma-26B-A4B-it](https://huggingface.co/google/diffusiongemma-26B-A4B-it)** — google | 1,023 likes, 673K downloads
  A massive sparse diffusion model (26B total, 4B active) for image-text-to-text generation, trending for its efficient MoE architecture.

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — nvidia | 2,217 likes, 235K downloads
  A specialized 3B model for image-feature extraction with "locate anything" capabilities, gaining rapid adoption for visual grounding tasks.

- **[moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)** — moonshotai | 932 likes, 317K downloads
  A compressed, image-feature-extraction model from Moonshot AI, blending coding and multimodal capabilities with efficient tensor compression.

- **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)** — nvidia | 588 likes, 21.4K downloads
  A cache-aware streaming ASR model (0.6B params) designed for low-latency speech recognition, trending for real-time applications.

- **[zai-org/SCAIL-2](https://huggingface.co/zai-org/SCAIL-2)** — zai-org | 241 likes, 0 downloads
  A diffusion-based pose-driven character animation model turning images into video, notable despite zero downloads (likely pre-release).

- **[ostris/ideogram_4_turbotime_lora](https://huggingface.co/ostris/ideogram_4_turbotime_lora)** — ostris | 83 likes, 1.7K downloads
  A LoRA adapter for Ideogram 4, enabling faster text-to-image generation with base model compatibility.

- **[bosonai/higgs-audio-v3-tts-4b](https://huggingface.co/bosonai/higgs-audio-v3-tts-4b)** — bosonai | 499 likes, 72.2K downloads
  A 4B text-to-speech model built on Qwen3 multimodal architecture, offering high-quality voice synthesis.

- **[owensong/Inflect-Nano-v1](https://huggingface.co/owensong/Inflect-Nano-v1)** — owensong | 143 likes, 0 downloads
  An ultra-small TTS model designed for edge deployment, trending for its potential in low-resource environments.

### 🔧 Specialized Models (code, math, medical, embeddings)

- **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)** — yuxinlu1 | 1,993 likes, 312K downloads
  A GGUF-quantized Gemma-4 coder with advanced prompt composition, highly downloaded for local code generation.

- **[moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)** — (see above) — coded as image-feature-extraction but also code-oriented; high download count.

- **[LiquidAI/LFM2.5-Embedding-350M](https://huggingface.co/LiquidAI/LFM2.5-Embedding-350M)** — LiquidAI | 81 likes, 6.1K downloads
  A 350M sentence-similarity embedding model from Liquid AI, gaining interest for efficient retrieval in RAG pipelines.

- **[datalab-to/lift](https://huggingface.co/datalab-to/lift)** — datalab-to | 89 likes, 0 downloads
  A Qwen3.5-based document understanding model converting PDFs to multimodal representations, despite zero downloads.

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — HauhauCS | 2,043 likes, 3.8M downloads
  An uncensored MoE vision-language model with aggressive fine-tuning, the most downloaded model in the list by a wide margin.

- **[DavidAU/Qwen3.6-40B-Claude-4.6-Opus-Deckard-Heretic-Uncensored-Thinking-NEO-CODE-Di-IMatrix-MAX-GGUF](https://huggingface.co/DavidAU/Qwen3.6-40B-Claude-4.6-Opus-Deckard-Heretic-Uncensored-Thinking-NEO-CODE-Di-IMatrix-MAX-GGUF)** — DavidAU | 411 likes, 587K downloads
  A massive uncensored GGUF fine-tune combining multiple model weights, popular for its "heretic" style and extreme parameterization.

- **[unsloth/GLM-5.2-GGUF](https://huggingface.co/unsloth/GLM-5.2-GGUF)** — unsloth | 207 likes, 22.6K downloads
  Unsloth's GGUF quantization of GLM-5.2, enabling efficient local inference of Zhipu's latest MoE model.

- **[unsloth/Kimi-K2.7-Code-GGUF](https://huggingface.co/unsloth/Kimi-K2.7-Code-GGUF)** — unsloth | 147 likes, 37.3K downloads
  GGUF version of Kimi K2.7-Code, making this compressed coding model accessible on consumer hardware.

- **[Jackrong/Qwopus3.6-27B-Coder-MTP-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-27B-Coder-MTP-GGUF)** — Jackrong | 269 likes, 168.5K downloads
  A quantized Qwen3.6-27B coder with multi-token prediction (MTP) capabilities, optimized for llama.cpp.

- **[bytkim/Qwen3.6-27B-MTP-pi-tune-GGUF](https://huggingface.co/bytkim/Qwen3.6-27B-MTP-pi-tune-GGUF)** — bytkim | 97 likes, 20.5K downloads
  A fine-tuned GGUF version of Qwen3.6 with position interpolation tuning, designed for extended context handling.

- **[lordx64/Qwable-v1](https://huggingface.co/lordx64/Qwable-v1)** — lordx64 | 138 likes, 2.8K downloads
  A Qwen3.5 MoE fine-tune blending vision and language capabilities, gaining traction among community modifiers.

- **[Mia-AiLab/Qwable-3.6-27b](https://huggingface.co/Mia-AiLab/Qwable-3.6-27b)** — Mia-AiLab | 112 likes, 17.3K downloads
  A GGUF adaptation of Qwen 3.6-27B, providing a quantized baseline for Qwen3.6 MoE experiments.

- **[zai-org/GLM-5.2-FP8](https://huggingface.co/zai-org/GLM-5.2-FP8)** — zai-org | 116 likes, 138K downloads
  FP8 precision quantized version of GLM-5.2 for efficient GPU inference, bridging quality and speed.

---

## Ecosystem Signal

This week's trending models reveal a clear **shift toward Mixture-of-Experts (MoE) architectures**. Models like GLM-5.2 (Zhipu), Qwen3.6 (Alibaba derivatives), and Cohere's North-Mini-Code all leverage MoE, while Google's DiffusionGemma uses 26B params with only 4B active, and DeepSeek-V4-Pro likely employs similar sparsity. The community is actively fine-tuning and quantizing these sparse models—evidenced by the proliferation of **GGUF variants** for Qwen3.6, GLM-5.2, and Kimi K2.7. **Unsloth** continues to be a key quantization provider, while individual community members like DavidAU and HauhauCS dominate the "uncensored" fine-tuning space, often combining multiple model families. **Multimodal models** are now the norm, with most new releases supporting vision (image-text-to-text) or audio. **Open-weight releases** from Google (Gemma-4, DiffusionGemma), DeepSeek, and Zhipu are driving the ecosystem, contrasting with more restricted models from MiniMax and Moonshot AI. The popularity of specialized code and agentic models (yuxinlu1's Gemma-4-coder, FastContext) suggests increasing demand for **task-specific local deployment**.

---

## Worth Exploring

1. **[DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** — With the highest likes and massive downloads, this is the most impactful new LLM. Serious practitioners should evaluate its reasoning and conversational capabilities as a potential new baseline for open-weight AI.

2. **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — NVIDIA’s entry into the "grounding" space with a compact 3B model is both impressive and practical. Its strong community reception suggests it fills a real need for visual object localization without heavy compute.

3. **[bosonai/higgs-audio-v3-tts-4b](https://huggingface.co/bosonai/higgs-audio-v3-tts-4b)** — One of the few large open TTS models (4B params) built on a Qwen3 backbone. Given the scarcity of high-quality open-source TTS, this model is worth studying for voice synthesis applications and multimodal expansion.

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*