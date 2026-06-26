# Hugging Face Trending Models Digest 2026-06-26

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-06-26 02:56 UTC

---

Here is the Hugging Face Trending Models Digest for June 26, 2026.

---

## Hugging Face Trending Models Digest – June 26, 2026

### 1. Today's Highlights

This week’s trending landscape is dominated by a massive surge in **DeepSeek-V4-Pro**, which shot to the top with over 5,000 likes, signaling a major ecosystem shift toward advanced reasoning and conversational MoE architectures. The GLM-5.2 family (both the base model and its very popular GGUF quantizations) continues to attract strong developer interest, especially for its Mixture-of-Experts design. NVIDIA is also making a notable push with both vision (LocateAnything-3B) and efficiency (Qwen3.6-35B-A3B NVFP4) models, while community-driven "abliterated" and uncensored fine-tunes of Gemma-4 and Qwen-3.6 are seeing explosive download numbers. Overall, the trend is clear: **large, efficient MoE models paired with extensive quantization and fine-tuning ecosystems** are driving the current momentum.

### 2. Trending Models by Category

#### 🧠 Language Models (LLMs, chat models, instruction-tuned)
- **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** – deepseek-ai | 5,062 likes, 1.9M downloads. The top trending model on the hub, representing the latest in conversational LLM reasoning with massive community adoption.
- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** – zai-org | 2,483 likes, 67.1K downloads. A leading MoE architecture optimized for text generation and conversation, quickly becoming a standard for efficient, high-quality chat.
- **[WeiboAI/VibeThinker-3B](https://huggingface.co/WeiboAI/VibeThinker-3B)** – WeiboAI | 715 likes, 51.7K downloads. A compact 3B reasoning model based on Qwen2, trending for its strong math and logical performance in a small footprint.
- **[microsoft/FastContext-1.0-4B-SFT](https://huggingface.co/microsoft/FastContext-1.0-4B-SFT)** – microsoft | 345 likes, 5.3K downloads. A 4B model built for long-context tasks, enabled by a specialized "Explorer SubAgent" approach.
- **[LiquidAI/LFM2.5-230M](https://huggingface.co/LiquidAI/LFM2.5-230M)** – LiquidAI | 74 likes, 7.3K downloads. A new ultra-small, liquid foundation model for on-device deployment and efficiency research.

#### 🎨 Multimodal & Generation (image, video, audio, text-to-X)
- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** – baidu | 900 likes, 70.7K downloads. A powerful OCR model that handles diverse image-to-text scenarios, trending due to its utility in document processing.
- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** – nvidia | 2,365 likes, 407K downloads. A vision model for precise object localization and feature extraction, widely adopted for computer vision applications.
- **[MiniMaxAI/MiniMax-M3](https://huggingface.co/MiniMaxAI/MiniMax-M3)** – MiniMaxAI | 1,241 likes, 154K downloads. A multimodal vision-language model from MiniMax, gaining traction for strong image-to-text generation.
- **[krea/Krea-2-Turbo](https://huggingface.co/krea/Krea-2-Turbo)** – krea | 245 likes, 3K downloads. The turbo variant of Krea-2 for rapid text-to-image generation, supporting efficient diffusion pipelines.
- **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)** – nvidia | 695 likes, 50.6K downloads. A tiny 0.6B streaming automatic speech recognition model from NVIDIA, optimized for low-latency voice applications.
- **[owensong/Inflect-Nano-v1](https://huggingface.co/owensong/Inflect-Nano-v1)** – owensong | 201 likes, 0 downloads. A newly released ultra-small text-to-speech model pushing the boundaries of speech synthesis size and efficiency.

#### 🔧 Specialized Models (code, math, medical, embeddings)
- **[moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)** – moonshotai | 992 likes, 502K downloads. A code-focused vision model using compressed-tensors, trending for high-volume code generation and understanding tasks.
- **[Chunjiang-Intelligence/DeepSeek-v4-Fable](https://huggingface.co/Chunjiang-Intelligence/DeepSeek-v4-Fable)** – Chunjiang-Intelligence | 92 likes, 646 downloads. A cybersecurity-oriented variant of DeepSeek-v4, highlighting niche safety and threat detection applications.

#### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)
- **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)** – yuxinlu1 | 2,367 likes, 495K downloads. The most popular GGUF quantization in the list, a coding-specialized Gemma-4 variant with huge download volume.
- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** – HauhauCS | 2,238 likes, 3.5M downloads. A heavily downloaded uncensored, aggressive Qwen-3.6 MoE variant, demonstrating strong demand for unfiltered community models.
- **[nvidia/Qwen3.6-35B-A3B-NVFP4](https://huggingface.co/nvidia/Qwen3.6-35B-A3B-NVFP4)** – nvidia | 342 likes, 4.6M downloads. The highest download count on this list, NVIDIA's FP4 quantized Qwen3.6 MoE, enabling extreme efficiency on modern hardware.
- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** – empero-ai | 493 likes, 134K downloads. A quantized, reasoning-tuned Qwen-3.5 model combining "Mythos" fine-tuning for creative and logical tasks.
- **[huihui-ai/Huihui-gemma-4-12B-coder-fable5-composer2.5-v1-abliterated](https://huggingface.co/huihui-ai/Huihui-gemma-4-12B-coder-fable5-composer2.5-v1-abliterated)** – huihui-ai | 127 likes, 4.9K downloads. A popular "abliterated" (safety-filter removed) Gemma-4 variant for unrestricted code development.

### 3. Ecosystem Signal

The ecosystem is showing a decisive shift toward **efficient, Mixture-of-Experts (MoE) architectures** as the dominant paradigm for both language and multimodal models. The top of the chart is a battle between DeepSeek V4, GLM-5.2, and Qwen-3.6 moe variants, each offering strong performance with reduced computational costs. Open-weight models continue to overwhelm proprietary ones, as evidenced by massive downloads of base and quantized Open Models from NVIDIA, Google, and community creators. **Quantization is no longer optional**; FP4 and GGUF variants are seeing 10–100x more downloads than their full-precision counterparts, indicating that deployment efficiency is the primary barrier to entry. There is also a notable and growing sub-trend of **uncensored and "abliterated" fine-tunes**, particularly around Gemma-4 and Qwen-3.6, suggesting a strong community desire for models without safety alignment constraints. Finally, specialized vision and OCR models (NVIDIA, Baidu, MiniMax) are gaining dedicated niches, rounding out a diversifying model economy.

### 4. Worth Exploring

- **[microsoft/FastContext-1.0-4B-SFT](https://huggingface.co/microsoft/FastContext-1.0-4B-SFT)** – At only 4B parameters, this model is specifically designed for long-context tasks, a notoriously difficult area. Studying its "Explorer SubAgent" architecture could reveal new approaches for handling context windows far beyond typical training limits.

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** – With 2.3k likes and 400k+ downloads, this model represents a new standard in universal object localization. It is a strong candidate for both production image processing pipelines and as a benchmark for vision foundation models.

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** – Despite its controversial premise, this model’s 3.5 million downloads in its niche makes it a critical case study in community-driven model demand, the limits of safety alignment, and the practical performance of aggressive fine-tuning on a base MoE model.

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*