# Hugging Face Trending Models Digest 2026-06-22

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-06-22 03:50 UTC

---

# Hugging Face Trending Models Digest — June 22, 2026

## Today's Highlights

The top of the charts is dominated by DeepSeek-V4-Pro (4,999 likes, 2.6M downloads), a clear breakout release signaling continued dominance of the DeepSeek family. Qwen's Qwen3.6-35B-A3B (2,198 likes, 5.1M downloads) and NVIDIA's LocateAnything-3B (2,248 likes) round out a top tier focused on MoE architectures and multimodal capabilities. The ecosystem is also seeing strong activity around Gemma-4 variants—particularly GGUF quantizations for coding and agentic use—and an influx of vision-language models (MiniMax-M3, Kimi-K2.7-Code, DiffusionGemma). Quantization via GGUF continues to be a major community force, with Unsloth and individual developers converting nearly every major release.

---

## Trending Models

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)**  
  *deepseek-ai* | Likes: 4,999 | Downloads: 2,611,991  
  The flagship text-generation release this week, a dense MoE model driving strong community adoption for conversational and general reasoning tasks.

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)**  
  *zai-org* | Likes: 1,847 | Downloads: 27,413  
  A MoE-based conversational model from Zhipu AI, trending as the latest in the GLM lineage with strong instruction-following capabilities.

- **[MoonshotAI/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)**  
  *moonshotai* | Likes: 946 | Downloads: 363,308  
  A compressed code-focused model from the Kimi family, combining image-text capabilities with coding specialization.

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)**  
  *HauhauCS* | Likes: 2,082 | Downloads: 3,966,691  
  An uncensored, vision-capable GGUF variant of Qwen3.6-35B, trending for its aggressive creative capability and massive download count.

- **[CohereLabs/North-Mini-Code-1.0](https://huggingface.co/CohereLabs/North-Mini-Code-1.0)**  
  *CohereLabs* | Likes: 475 | Downloads: 19,551  
  A compact MoE language model optimized for code generation, reflecting Cohere's push into developer-facing tools.

- **[poolside/Laguna-M.1](https://huggingface.co/poolside/Laguna-M.1)**  
  *poolside* | Likes: 84 | Downloads: 2,580  
  A vLLM-compatible language model from poolside, targeting production deployment with SGLang support.

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **[google/gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it)**  
  *google* | Likes: 1,129 | Downloads: 1,815,370  
  Google's unified any-to-any model (image, text, audio), trending as the most versatile Gemma-4 release with massive adoption.

- **[google/diffusiongemma-26B-A4B-it](https://huggingface.co/google/diffusiongemma-26B-A4B-it)**  
  *google* | Likes: 1,037 | Downloads: 762,861  
  A diffusion-based multimodal model combining Gemma with image generation, trending for its novel architecture and conversational interface.

- **[MiniMaxAI/MiniMax-M3](https://huggingface.co/MiniMaxAI/MiniMax-M3)**  
  *MiniMaxAI* | Likes: 1,177 | Downloads: 104,076  
  A multimodal vision-language model pushing the frontier of image-text-to-text reasoning, with strong community interest.

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)**  
  *nvidia* | Likes: 2,248 | Downloads: 241,845  
  NVIDIA's image-feature-extraction model for object localization in images, trending due to its precision and small footprint.

- **[Qwen/Qwen3.6-35B-A3B](https://huggingface.co/Qwen/Qwen3.6-35B-A3B)**  
  *Qwen* | Likes: 2,198 | Downloads: 5,148,673  
  The official release of Qwen's latest MoE vision-language model, the most downloaded model this week by a wide margin.

- **[ostris/ideogram_4_turbotime_lora](https://huggingface.co/ostris/ideogram_4_turbotime_lora)**  
  *ostris* | Likes: 91 | Downloads: 2,452  
  A LoRA adapter for Ideogram-4, enabling faster text-to-image generation with style control.

- **[owensong/Inflect-Nano-v1](https://huggingface.co/owensong/Inflect-Nano-v1)**  
  *owensong* | Likes: 155 | Downloads: 0  
  An ultra-small text-to-speech model designed for on-device deployment, notable for its tiny size and novel TTS pipeline.

- **[Boogu/Boogu-Image-0.1-Edit](https://huggingface.co/Boogu/Boogu-Image-0.1-Edit)**  
  *Boogu* | Likes: 84 | Downloads: 374  
  A bilingual (EN/ZH) image editing model built on Diffusers, early but showing promise for localized applications.

### 🔧 Specialized Models (code, math, medical, embeddings)

- **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)**  
  *yuxinlu1* | Likes: 2,094 | Downloads: 358,677  
  A specialized Gemma-4 coding variant with reasoning enhancements, among the most popular GGUF-released models this week.

- **[yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)**  
  *yuxinlu1* | Likes: 289 | Downloads: 21,730  
  An agentic GGUF variant of Gemma-4-12B, optimized for terminal-based tool use and autonomous workflows.

- **[microsoft/FastContext-1.0-4B-SFT](https://huggingface.co/microsoft/FastContext-1.0-4B-SFT)**  
  *microsoft* | Likes: 267 | Downloads: 2,593  
  A 4B model fine-tuned for efficient long-context reasoning, featuring an "Explorer SubAgent" mechanism.

- **[WeiboAI/VibeThinker-3B](https://huggingface.co/WeiboAI/VibeThinker-3B)**  
  *WeiboAI* | Likes: 565 | Downloads: 20,277  
  A Qwen2-based 3B model specialized for mathematical reasoning, trending for its strong performance-to-size ratio.

- **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)**  
  *nvidia* | Likes: 613 | Downloads: 27,275  
  NVIDIA's streaming automatic speech recognition model with cache-aware architecture, a standout in the audio space.

- **[LiquidAI/LFM2.5-Embedding-350M](https://huggingface.co/LiquidAI/LFM2.5-Embedding-350M)**  
  *LiquidAI* | Likes: 93 | Downloads: 7,726  
  A compact embedding model from Liquid AI, built for sentence-similarity tasks with the LFM2.5 architecture.

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **[unsloth/GLM-5.2-GGUF](https://huggingface.co/unsloth/GLM-5.2-GGUF)**  
  *unsloth* | Likes: 229 | Downloads: 32,260  
  Unsloth's GGUF quantization of GLM-5.2, enabling efficient local inference for Zhipu's architecture.

- **[zai-org/GLM-5.2-FP8](https://huggingface.co/zai-org/GLM-5.2-FP8)**  
  *zai-org* | Likes: 123 | Downloads: 217,361  
  The official FP8 quantized version of GLM-5.2, optimized for memory-constrained deployments.

- **[Mia-AiLab/Qwable-3.6-27b](https://huggingface.co/Mia-AiLab/Qwable-3.6-27b)**  
  *Mia-AiLab* | Likes: 121 | Downloads: 22,879  
  A GGUF variant of the Qwable architecture based on Qwen3.6, representing community quantization efforts.

- **[lordx64/Qwable-v1](https://huggingface.co/lordx64/Qwable-v1)**  
  *lordx64* | Likes: 145 | Downloads: 3,351  
  A community fine-tune of Qwen3.5 MoE with multimodal support, blending coding and vision capabilities.

- **[bytkim/Qwen3.6-27B-MTP-pi-tune-GGUF](https://huggingface.co/bytkim/Qwen3.6-27B-MTP-pi-tune-GGUF)**  
  *bytkim* | Likes: 102 | Downloads: 36,421  
  A GGUF quantized version of Qwen3.6-27B with multi-token prediction tuning, popular among llama.cpp users.

- **[Jackrong/Qwopus3.6-27B-Coder-MTP-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-27B-Coder-MTP-GGUF)**  
  *Jackrong* | Likes: 276 | Downloads: 190,993  
  A coding-focused GGUF variant of Qwen3.6 with vision support and multi-token prediction, highly downloaded.

- **[unsloth/Kimi-K2.7-Code-GGUF](https://huggingface.co/unsloth/Kimi-K2.7-Code-GGUF)**  
  *unsloth* | Likes: 151 | Downloads: 42,837  
  Unsloth's GGUF conversion of Kimi-K2.7-Code, bringing compressed coding capability to local hardware.

- **[nex-agi/Nex-N2-Pro](https://huggingface.co/nex-agi/Nex-N2-Pro)**  
  *nex-agi* | Likes: 343 | Downloads: 7,872  
  A Qwen3.5-MoE-based vision-language fine-tune, showcasing community optimization of multimodal LLMs.

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)**  
  *empero-ai* | Likes: 77 | Downloads: 688  
  A GGUF quantized reasoning model based on Qwen3.5, part of the "Mythos" fine-tuning lineage.

- **[datalab-to/lift](https://huggingface.co/datalab-to/lift)**  
  *datalab-to* | Likes: 110 | Downloads: 516  
  A PDF-oriented image-text-to-text model built on Qwen3.5, emerging as a niche tool for document understanding.

---

## Ecosystem Signal

The model ecosystem this week reveals several clear signals. **Mixture-of-Experts (MoE) architectures are now the dominant paradigm**—DeepSeek-V4-Pro, GLM-5.2, Qwen3.6-35B-A3B, and Cohere's North-Mini all leverage sparse activation, reflecting a mature shift toward compute-efficient scaling. **Multimodal models are becoming the default**, not the exception: over one-third of trending models are vision-language or any-to-any systems (Gemma-4, DiffusionGemma, MiniMax-M3, Qwen3.6). **Open-weight releases continue to outpace proprietary checkpoints in community traction**, with DeepSeek and Qwen leading. **GGUF quantization remains the primary distribution mechanism** for local deployment, with Unsloth serving as the ecosystem's quantization backbone—converting nearly every major model within days of release. Niche specialization is also growing: streaming ASR (NVIDIA Nemotron-3.5), ultra-small TTS (Inflect-Nano), and image editing (Boogu-Image) indicate the ecosystem is maturing beyond general-purpose chat.

---

## Worth Exploring

1. **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — A standout for its precision visual grounding at only 3B parameters. Worth studying for embedded vision tasks, robotics, or any application requiring spatial understanding without massive compute.

2. **[google/diffusiongemma-26B-A4B-it](https://huggingface.co/google/diffusiongemma-26B-A4B-it)** — A rare diffusion-in-the-loop LLM architecture. This model blurs the line between generation and understanding, making it a fascinating research artifact for anyone exploring generative multimodal systems.

3. **[owensong/Inflect-Nano-v1](https://huggingface.co/owensong/Inflect-Nano-v1)** — With zero downloads yet high likes, this ultra-small TTS model signals a shift toward on-device speech synthesis. Worth trying for edge deployments, accessibility tools, or low-latency voice interfaces.

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*