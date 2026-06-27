# Hugging Face Trending Models Digest 2026-06-27

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-06-27 02:46 UTC

---

# Hugging Face Trending Models Digest — 2026-06-27

## Today's Highlights

This week's trending models reveal a clear push toward **multimodal vision-language systems** and **efficient quantized deployments**, with NVIDIA, Qwen, and Baidu leading the charge. Baidu's **Unlimited-OCR** (1,046 likes) dominated the image-text-to-text pipeline as a brand-new feature-extraction OCR model, while NVIDIA's **LocateAnything-3B** (2,385 likes) became the go-to for spatial grounding. The **Gemma-4** ecosystem exploded — fine-tunes like yuxinlu1's coder/agentic variants and huihui-ai's abliterated version collectively racked up millions of downloads. Meanwhile, the **Ornith family** (deepreinforce-ai) launched across scales from 9B to 397B, and NVIDIA's **Qwen3.6-35B-A3B-NVFP4** posted an astonishing 4.8M downloads, signaling massive demand for memory-efficient MoE models.

## Trending Models

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — zai-org | 2,602 likes, 83,589 downloads  
  A conversational MoE-DSA model from the GLM-5 series, trending for its strong dialogue quality and efficient sparse attention.

- **[microsoft/FastContext-1.0-4B-SFT](https://huggingface.co/microsoft/FastContext-1.0-4B-SFT)** — microsoft | 355 likes, 5,735 downloads  
  A 4B SFT model designed for long-context tasks with Explorer SubAgent capabilities, signaling Microsoft's continued investment in agentic LLMs.

- **[deepreinforce-ai/Ornith-1.0 series](https://huggingface.co/deepreinforce-ai/Ornith-1.0-9B)** — deepreinforce-ai | 9B (115 likes), 35B (124 likes), 397B (107 likes)  
  A new MoE family based on Qwen3.5, covering sizes from 9B to 397B with vision-language support — trending as a complete open-weight lineup for scaling experiments.

- **[LiquidAI/LFM2.5-230M](https://huggingface.co/LiquidAI/LFM2.5-230M)** — LiquidAI | 113 likes, 8,286 downloads  
  A tiny 230M text-generation model from LiquidAI, gaining traction for edge deployment and research on small language models.

- **[WeiboAI/VibeThinker-3B](https://huggingface.co/WeiboAI/VibeThinker-3B)** — WeiboAI | 734 likes, 54,638 downloads  
  A 3B reasoning and math model based on Qwen2, popular for its strong arithmetic performance in a compact package.

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** — baidu | 1,046 likes, 134,146 downloads  
  A state-of-the-art OCR model for image-text-to-text, trending for its unlimited-scope text recognition capabilities.

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — nvidia | 2,385 likes, 494,756 downloads  
  A 3B vision model for object localization and grounding, widely adopted for robotics and visual QA pipelines.

- **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)** — nvidia | 709 likes, 56,434 downloads  
  A streaming automatic speech recognition model at 0.6B parameters, gaining traction for real-time audio applications.

- **[MiniMaxAI/MiniMax-M3](https://huggingface.co/MiniMaxAI/MiniMax-M3)** — MiniMaxAI | 1,247 likes, 169,951 downloads  
  A multimodal vision-language model with strong image-text-to-text performance, trending as a competitive open-weight alternative to proprietary VLMs.

- **[krea/Krea-2-Turbo](https://huggingface.co/krea/Krea-2-Turbo)** — krea | 285 likes, 8,721 downloads  
  A text-to-image diffusion model fine-tuned from Krea-2-Raw for speed and quality, popular in creative workflows.

- **[datalab-to/lift](https://huggingface.co/datalab-to/lift)** — datalab-to | 159 likes, 6,054 downloads  
  A Qwen3.5-based vision model specialized for PDF understanding and document layout — trending for enterprise document AI.

- **[HauhauCS/Gemma4-12B-QAT-Uncensored-HauhauCS-Balanced](https://huggingface.co/HauhauCS/Gemma4-12B-QAT-Uncensored-HauhauCS-Balanced)** — HauhauCS | 93 likes, 23,772 downloads  
  A quantized, uncensored Gemma-4 variant with vision support, balancing output safety and creativity.

- **[Comfy-Org/Krea-2](https://huggingface.co/Comfy-Org/Krea-2)** — Comfy-Org | 137 likes, 10 downloads  
  A ComfyUI integration for Krea-2, enabling node-based image generation workflows.

- **[Qwen/Qwen-AgentWorld-35B-A3B](https://huggingface.co/Qwen/Qwen-AgentWorld-35B-A3B)** — Qwen | 323 likes, 13,186 downloads  
  A 35B MoE model optimized for agentic tasks with vision-language capabilities, part of Qwen's expanding agent ecosystem.

### 🔧 Specialized Models (code, math, medical, embeddings)

- **[Chunjiang-Intelligence/DeepSeek-v4-Fable](https://huggingface.co/Chunjiang-Intelligence/DeepSeek-v4-Fable)** — Chunjiang-Intelligence | 108 likes, 1,103 downloads  
  A DeepSeek v4 variant fine-tuned for cybersecurity — trending for its domain-specific safety capabilities.

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** — empero-ai | 596 likes, 486,810 downloads  
  A GGUF-quantized Qwen3.5 fine-tune for reasoning, heavily downloaded for local inference with llama.cpp.

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M)** — empero-ai | 452 likes, 20,346 downloads  
  The base safetensors version of the same reasoning fine-tune, popular for full-precision experimentation.

- **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)** — yuxinlu1 | 2,402 likes, 516,333 downloads  
  A GGUF-quantized Gemma-4 fine-tune for code and reasoning — the most downloaded coding model this week.

- **[yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)** — yuxinlu1 | 690 likes, 186,663 downloads  
  A GGUF variant optimized for agentic and terminal-based tasks, complementing the coder version.

- **[unsloth/GLM-5.2-GGUF](https://huggingface.co/unsloth/GLM-5.2-GGUF)** — unsloth | 411 likes, 107,553 downloads  
  An unsloth-optimized GGUF of GLM-5.2, enabling fast local inference of the popular MoE model.

- **[nvidia/Qwen3.6-35B-A3B-NVFP4](https://huggingface.co/nvidia/Qwen3.6-35B-A3B-NVFP4)** — nvidia | 361 likes, 4,812,629 downloads  
 

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*