# Hugging Face Trending Models Digest 2026-06-28

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-06-28 03:25 UTC

---

# Hugging Face Trending Models Digest – June 28, 2026

## Today’s Highlights

This week’s trending list is dominated by **Mixture-of-Experts (MoE) language models**, with GLM-5.2, Qwen-AgentWorld-35B-A3B, and the Ornith family all gaining strong community traction. **Vision-language models** are surging, led by baidu’s Unlimited-OCR (212k downloads) and NVIDIA’s LocateAnything-3B (2.4k likes, 570k downloads), while Qwen3.6-based uncensored and GGUF variants account for the highest raw download figures. **GGUF quantization** remains the primary vehicle for local deployment, with nearly half of the top-30 being GGUF files. Notable new entrants include DeepSeek-V4-Pro-DSpark (first public release with arxiv paper), Microsoft FastContext for long-context reasoning, and MiniMax-M3, a multimodal model from MiniMaxAI that garnered 1.25k likes.

---

## Trending Models

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — zai-org | Likes: 2,689 | Downloads: 98,994  
  A MoE-based conversational model from the GLM family; its high like-to-download ratio signals strong early community interest.

- **[Qwen/Qwen-AgentWorld-35B-A3B](https://huggingface.co/Qwen/Qwen-AgentWorld-35B-A3B)** — Qwen | Likes: 361 | Downloads: 18,872  
  Qwen’s latest MoE agent-focused model (35B total, 3B active); trending as a foundation for agentic workflows.

- **[deepreinforce-ai/Ornith-1.0-35B](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B)** — deepreinforce-ai | Likes: 163 | Downloads: 7,571  
  Base model of the Ornith series (Qwen3.5-MoE architecture); accompanied by 9B, 35B, and a massive 397B variant, all MIT-licensed.

- **[deepseek-ai/DeepSeek-V4-Pro-DSpark](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-DSpark)** — deepseek-ai | Likes: 131 | Downloads: 0  
  DeepSeek’s V4 release with accompanying arxiv paper (2606.19348); notable for its “DSpark” architecture, though downloads are yet to accumulate.

- **[microsoft/FastContext-1.0-4B-SFT](https://huggingface.co/microsoft/FastContext-1.0-4B-SFT)** — microsoft | Likes: 366 | Downloads: 6,447  
  A 4B model fine-tuned for efficient long-context reasoning via an “Explorer SubAgent” mechanism.

- **[LiquidAI/LFM2.5-230M](https://huggingface.co/LiquidAI/LFM2.5-230M)** — LiquidAI | Likes: 130 | Downloads: 9,791  
  A very small (230M) model from LiquidAI, part of the LFM2 series; trending for low-resource deployment.

- **[Chunjiang-Intelligence/DeepSeek-v4-Fable](https://huggingface.co/Chunjiang-Intelligence/DeepSeek-v4-Fable)** — Chunjiang-Intelligence | Likes: 113 | Downloads: 1,328  
  A cybersecurity-oriented fine-tune of DeepSeek-V4, indicating interest in domain-specific safety models.

- **[WeiboAI/VibeThinker-3B](https://huggingface.co/WeiboAI/VibeThinker-3B)** — WeiboAI | Likes: 742 | Downloads: 57,521  
  A Qwen2-based 3B model specialized for math reasoning; strong community uptake for its compact size.

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** — baidu | Likes: 1,142 | Downloads: 212,760  
  An image-text-to-text OCR model from Baidu; leads downloads among non-GGUF models thanks to practical utility.

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — nvidia | Likes: 2,409 | Downloads: 570,466  
  NVIDIA’s image localization model (3B parameters) that can find any object in an image; top-3 in likes and downloads.

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M)** — empero-ai | Likes: 491 | Downloads: 30,298  
  A Qwen3.5-based vision-language model fine-tuned on a large Claude-generated dataset; also available as GGUF.

- **[krea/Krea-2-Turbo](https://huggingface.co/krea/Krea-2-Turbo)** — krea | Likes: 311 | Downloads: 17,445  
  A text-to-image diffusion model (base: Krea-2-Raw) optimized for speed; accompanied by a raw variant and a ComfyUI workflow.

- **[MiniMaxAI/MiniMax-M3](https://huggingface.co/MiniMaxAI/MiniMax-M3)** — MiniMaxAI | Likes: 1,253 | Downloads: 182,714  
  A multimodal vision-language model from MiniMax; strong likes suggest high output quality for image-text tasks.

- **[Comfy-Org/Krea-2](https://huggingface.co/Comfy-Org/Krea-2)** — Comfy-Org | Likes: 159 | Downloads: 10  
  A ComfyUI workflow node pack for Krea-2; minimal downloads but relevant for the image generation ecosystem.

- **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)** — nvidia | Likes: 719 | Downloads: 61,857  
  NVIDIA’s streaming ASR model (0.6B), part of the Nemotron-3.5 speech series; trending for real-time transcription.

### 🔧 Specialized Models (code, math, medical, embeddings)

- **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)** — yuxinlu1 | Likes: 2,428 | Downloads: 536,130  
  A coding-specialized fine-tune of Gemma-4-12B using a “fable5” dataset; extremely high downloads underscore demand for open code LLMs.

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — HauhauCS | Likes: 2,279 | Downloads: 3,331,475  
  An uncensored MoE variant of Qwen3.6; by far the highest downloads in the list, indicating massive appetite for unconstrained models.

- **[nvidia/GLM-5.2-NVFP4](https://huggingface.co/nvidia/GLM-5.2-NVFP4)** — nvidia | Likes: 131 | Downloads: 6,464  
  NVIDIA’s 4-bit floating-point quantized version of GLM-5.2 using Model Optimizer; testifies to hardware-software co-optimization.

- **[Jackrong/Qwopus3.6-27B-Coder-Compat-MTP-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-27B-Coder-Compat-MTP-GGUF)** — Jackrong | Likes: 97 | Downloads: 49,935  
  A GGUF quantized 27B coding model with MTP (Multi-Turn Prediction) support; part of the Qwen3.5/3.6 ecosystem.

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** — empero-ai | Likes: 679 | Downloads: 712,627  
  The GGUF quantization of the top Qwythos vision-language model; high downloads for local inference.

- **[yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)** — yuxinlu1 | Likes: 736 | Downloads: 206,828  
  A Gemma-4-12B GGUF optimized for agentic terminal usage; complements the coding variant above.

- **[deepreinforce-ai/Ornith-1.0-35B-GGUF](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B-GGUF)** — deepreinforce-ai | Likes: 332 | Downloads: 20,266  
  GGUF version of Ornith-1.0-35B, MIT-licensed; part of a growing Ornith quantized family.

- **[deepreinforce-ai/Ornith-1.0-9B-GGUF](https://huggingface.co/deepreinforce-ai/Ornith-1.0-9B-GGUF)** — deepreinforce-ai | Likes: 222 | Downloads: 11,034  
  Lighter sibling of the 35B GGUF, also MIT-licensed.

- **[unsloth/GLM-5.2-GGUF](https://huggingface.co/unsloth/GLM-5.2-GGUF)** — unsloth | Likes: 426 | Downloads: 125,230  
  Unsloth’s optimized GGUF of GLM-5.2; benefits from memory-efficient quantization techniques.

- **[nvidia/Qwen3.6-35B-A3B-NVFP4](https://huggingface.co/nvidia/Qwen3.6-35B-A3B-NVFP4)** — nvidia | Likes: 367 | Downloads: 5,022,254  
  NVIDIA’s NVFP4 quantized Qwen3.6-35B-A3B; the single most-downloaded model on the list (over 5M), likely driven by NVIDIA ecosystem users.

- **[huihui-ai/Huihui-gemma-4-12B-coder-fable5-composer2.5-v1-abliterated](https://huggingface.co/huihui-ai/Huihui-gemma-4-12B-coder-fable5-composer2.5-v1-abliterated)** — huihui-ai | Likes: 137 | Downloads: 6,250  
  An “abliterated” (safety removal) version of Gemma-4-12B-coder, representing the “uncensored” trend in coding models.

- **[HauhauCS/Gemma4-12B-QAT-Uncensored-HauhauCS-Balanced](https://huggingface.co/HauhauCS/Gemma4-12B-QAT-Uncensored-HauhauCS-Balanced)** — HauhauCS | Likes: 97 | Downloads: 32,222  
  A QAT (Quantization-Aware Training) uncensored variant of Gemma-4-12B; balanced approach to an uncensored model.

---

## Ecosystem Signal

The current Hugging Face landscape is defined by three converging trends:

1. **MoE dominance** – Models like GLM-5.2, Qwen-AgentWorld, and the Ornith series (based on Qwen3.5 MoE) are displacing dense architectures. Their ability to deliver high capability with lower inference cost is driving adoption, especially in agentic and coding applications.

2. **GGUF as the universal quantization format** – Over half of the top-30 models are GGUF quantizations. Tools like Unsloth and llama.cpp are key enablers, while NVIDIA’s NVFP4 format offers an alternative for hardware-native acceleration. The sheer download volume (5M+ for `nvidia/Qwen3.6-35B-A3B-NVFP4`) signals that **deployment-ready, quantized models are the primary consumption pattern**.

3. **Uncensored / abliterated fine-tunes** – Community releases removing safety filters (HauhauCS, huihui-ai) continue to attract massive downloads, particularly for coding and general-purpose models. This mirrors a growing user preference for “no guardrails” experimentation, even as original model providers like DeepSeek and Qwen release official versions with safety mitigations.

Open-weight models from established labs (Qwen, GLM, NVIDIA, DeepSeek) dominate the base-model space, while community fine-tuners (HauhauCS, yuxinlu1, empero-ai) drive the most popular derivatives. LiquidAI’s tiny 230M model and Microsoft’s FastContext show that efficient architectures are also gaining ground.

---

## Worth Exploring



---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*