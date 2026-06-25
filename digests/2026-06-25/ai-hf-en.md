# Hugging Face Trending Models Digest 2026-06-25

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-06-25 02:51 UTC

---

# Hugging Face Trending Models Digest – 2026-06-25

## Today's Highlights

This week’s trending list is dominated by **MoE and any-to-any architectures**, with DeepSeek-V4-Pro leading at 5,049 likes and 2M+ downloads, while Google’s gemma-4-12B-it and diffusiongemma-26B showcase the rising appeal of unified multimodal models. **Quantized and fine-tuned variants** continue to surge – GLM-5.2 GGUF and FP8 versions, plus multiple gemma-4-coder quantizations, reflect strong community demand for efficient, deployable models. Notable newcomers include **NVIDIA’s LocateAnything-3B** (localization + vision) and **Baidu’s Unlimited-OCR**, pushing the frontier of practical image-text pipelines. The ecosystem is clearly shifting toward **smaller, specialized, and quantized MoE models** that balance performance with accessibility.

## Trending Models

### 🧠 Language Models (LLMs, chat, instruction-tuned)

- **[DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** – deepseek-ai • 5,049 likes • 2,052,463 downloads  
  Flagship conversational LLM from DeepSeek, trending due to its massive community adoption and top-tier performance in reasoning and instruction following.

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** – zai-org • 2,360 likes • 57,186 downloads  
  A new MoE-based chat model (GLM family) with DSA attention, gaining attention for its efficient architecture and strong Chinese-English bilingual capabilities.

- **[zai-org/GLM-5.2-FP8](https://huggingface.co/zai-org/GLM-5.2-FP8)** – zai-org • 158 likes • 445,304 downloads  
  FP8 quantized version of GLM-5.2, offering reduced memory usage while preserving quality – download spike suggests strong interest in deployment.

- **[google/gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it)** – google • 1,163 likes • 2,114,441 downloads  
  An any-to-any multimodal model from Google, bridging text, image, and audio; its unified interface makes it a key release for universal AI assistants.

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** – HauhauCS • 2,209 likes • 3,769,369 downloads  
  An uncensored MoE variant of Qwen3.6 with aggressive instruction tuning – huge download counts reflect demand for unrestricted conversational models.

- **[microsoft/FastContext-1.0-4B-SFT](https://huggingface.co/microsoft/FastContext-1.0-4B-SFT)** – microsoft • 336 likes • 4,805 downloads  
  A 4B-parameter model optimized for fast context retrieval and agentic tasks, signaling Microsoft’s push into efficient sub-5B reasoning models.

- **[Qwen/Qwen-AgentWorld-35B-A3B](https://huggingface.co/Qwen/Qwen-AgentWorld-35B-A3B)** – Qwen • 151 likes • 223 downloads  
  An MoE agent-oriented model from Qwen, designed for interactive decision-making and tool use – early-stage but with high potential.

- **[poolside/Laguna-M.1](https://huggingface.co/poolside/Laguna-M.1)** – poolside • 95 likes • 2,913 downloads  
  A production-ready LLM with vLLM and SGLang support, aimed at enterprise applications – relatively low hype but notable for its deployment focus.

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** – baidu • 743 likes • 45,687 downloads  
  A full pipeline for OCR without text length limits, combining vision and text decoding – trending for its practical utility in document digitization.

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** – nvidia • 2,347 likes • 359,498 downloads  
  A 3B vision-language model for object localization and referring expression comprehension – NVIDIA’s entry into lightweight, directed VLMs.

- **[MiniMaxAI/MiniMax-M3](https://huggingface.co/MiniMaxAI/MiniMax-M3)** – MiniMaxAI • 1,228 likes • 143,093 downloads  
  Multimodal vision-language model (M3) with strong image understanding, trending for its balance of size and capability.

- **[moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)** – moonshotai • 984 likes • 480,013 downloads  
  A compressed multimodal model focused on code comprehension and generation from visuals – notable for its "compressed-tensors" technique.

- **[google/diffusiongemma-26B-A4B-it](https://huggingface.co/google/diffusiongemma-26B-A4B-it)** – google • 1,061 likes • 1,036,328 downloads  
  A diffusion-based multimodal LLM combining image generation and understanding – part of Google’s unified gemma family, with strong community engagement.

- **[krea/Krea-2-Turbo](https://huggingface.co/krea/Krea-2-Turbo)** – krea • 194 likes • 878 downloads  
  A text-to-image diffusion model optimized for speed (Turbo), built on Krea-2-Raw – early traction in the generative art space.

- **[krea/Krea-2-Raw](https://huggingface.co/krea/Krea-2-Raw)** – krea • 163 likes • 1,205 downloads  
  Base version of Krea-2, a diffusers-based image generator – serves as foundation for fine-tuning.

- **[Boogu/Boogu-Image-0.1-Edit](https://huggingface.co/Boogu/Boogu-Image-0.1-Edit)** – Boogu • 121 likes • 743 downloads  
  An image editing diffusion model with bilingual (EN+ZH) support – niche but relevant for local markets.

- **[owensong/Inflect-Nano-v1](https://huggingface.co/owensong/Inflect-Nano-v1)** – owensong • 194 likes • 0 downloads  
  Ultra-small text-to-speech model (Nano-size) – interesting for edge TTS deployment despite zero download count (very new).

- **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)** – nvidia • 679 likes • 47,208 downloads  
  A streaming automatic speech recognition model (0.6B), cache-aware for low-latency inference – NVIDIA strengthens its speech stack.

- **[datalab-to/lift](https://huggingface.co/datalab-to/lift)** – datalab-to • 147 likes • 4,644 downloads  
  A vision-language model specialized in PDF understanding and image-text tasks – targets document AI workflows.

### 🔧 Specialized Models (code, math, medical, embeddings, reasoning)

- **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)** – yuxinlu1 • 2,302 likes • 483,139 downloads  
  A fine-tuned gemma-4-12B for coding with composer2.5 recipe, quantized to GGUF – extremely popular among code LLM users.

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** – empero-ai • 359 likes • 63,637 downloads  
  A reasoning-focused model (Claude-Mythos flavor) on Qwen3.5 base, GGUF quantized – appealing for logic and math tasks.

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M)** – empero-ai • 317 likes • 5,123 downloads  
  Non-quantized version of the above, preserving full precision for research.

- **[WeiboAI/VibeThinker-3B](https://huggingface.co/WeiboAI/VibeThinker-3B)** – WeiboAI • 692 likes • 49,569 downloads  
  A 3B math reasoning model based on Qwen2, gaining traction for efficient chain-of-thought on small hardware.

- **[LiquidAI/LFM2.5-Embedding-350M](https://huggingface.co/LiquidAI/LFM2.5-Embedding-350M)** – LiquidAI • 119 likes • 11,471 downloads  
  Sentence embedding model (350M) using liquid foundation model 2.5 – important for retrieval and RAG pipelines.

- **[LiquidAI/LFM2.5-ColBERT-350M](https://huggingface.co/LiquidAI/LFM2.5-ColBERT-350M)** – LiquidAI • 88 likes • 3,362 downloads  
  ColBERT-style retrieval embedding model from Liquid, designed for efficient multi-vector search.

- **[Jackrong/Qwopus3.6-27B-Coder-Compat-MTP-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-27B-Coder-Compat-MTP-GGUF)** – Jackrong • 83 likes • 10,867 downloads  
  A 27B MoE coder model with multi-token prediction, GGUF quantized – niche for advanced code generation.

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **[unsloth/GLM-5.2-GGUF](https://huggingface.co/unsloth/GLM-5.2-GGUF)** – unsloth • 349 likes • 76,971 downloads  
  Official unsloth quantized GGUF of GLM-5.2 – highly efficient and widely used for local inference.

- **[huihui-ai/Huihui-gemma-4-12B-coder-fable5-composer2.5-v1-abliterated](https://huggingface.co/huihui-ai/Huihui-gemma-4-12B-coder-fable5-composer2.5-v1-abliterated)** – huihui-ai • 124 likes • 4,402 downloads  
  An “abliterated” (uncensored) gemma-4 coder variant – part of the growing abliteration trend that removes safety filters.

- **[yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)** – yuxinlu1 • 539 likes • 138,704 downloads  
  Agentic task tuning on gemma-4-12B, with 3.5x context extension and tau2 scaling – specialized for terminal/agent use, heavily downloaded.

- **[Comfy-Org/Krea-2](https://huggingface.co/Comfy-Org/Krea-2)** – Comfy-Org • 91 likes • 10 downloads  
  ComfyUI workflow node for Krea-2 image generation – very new but signals integration of diffusion models into node-based UI.

## Ecosystem Signal

The current trending list reveals several key shifts in the open‑weight model ecosystem:

1. **MoE is mainstream.** Models like GLM-5.2, DeepSeek-V4-Pro, Qwen3.6-35B-A3B, and diffusiongemma-26B all use Mixture-of-Experts. The community is embracing MoE for its cost‑efficiency: high capacity with lower compute per forward pass.

2. **Any‑to‑any unification is accelerating.** Google’s gemma-4-12B-it explicitly supports any modality (text/image/audio), and diffusiongemma adds generation. This points to a future where a single model handles multiple tasks, reducing pipeline complexity.

3. **Quantization is no longer an afterthought.** Quantized variants (GGUF, FP8) consistently see high download counts (e.g., GLM-5.2-FP8 at 445k, Qwen3.6 uncensored at 3.7M). The community prioritizes deployable models for local hardware, gaming, and edge devices.

4. **Uncensored and “abliterated” models remain niche but strong.** The Qwen3.6 uncensored MoE variant leads all but DeepSeek in downloads, and huihui-ai’s abliterated gemma shows sustained interest. This reflects a persistent demand for models without safety guardrails, especially for creative and role‑play use.

5. **Code and reasoning models dominate fine‑tuning.** Gemma‑4‑12B‑coder variants, Qwythos (reasoning), VibeThinker (math), and Qwopus (code) indicate that community energy is concentrated on programming and logical tasks.

6. **Embedding models are gaining steam.** LiquidAI’s LFM2.5 embeddings (350M, ColBERT) are live. With RAG being a top application, lightweight and high‑quality embeddings are becoming essential infrastructure.

## Worth Exploring

Here are three models that stand out for their technical contribution or practical value:

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)**  
  At only 3B parameters, it performs object localization and referring expression comprehension. It’s a strong candidate for low‑latency vision applications (robotics, UI automation) and demonstrates that fine‑grained visual grounding doesn’t require huge models.

- **[google/diffusiongemma-26B-A4B-it](https://huggingface.co/google/diffusiongemma-26B-A4B-it)**  
  Combining diffusion with a language model in a single architecture is a bold move. With 1M+ downloads, it’s already popular, but worth studying for its potential to unify image generation and understanding in

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*