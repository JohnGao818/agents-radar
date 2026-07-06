# Hugging Face Trending Models Digest 2026-07-06

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-07-06 02:47 UTC

---

# 🤗 Hugging Face Trending Models Digest – 2026-07-06

## Today's Highlights

This week’s lineup is dominated by **quantized MoE models** and **agent‑centric fine‑tunes**, with GLM‑5.2, Qwen3.6‑based variants, and Gemma‑4‑12B coding editions topping the leaderboard. **zai‑org/GLM‑5.2** (3,470 likes) leads overall, while nvidia’s **LocateAnything‑3B** (2,618 likes) shows strong interest in vision‑driven grounding. The surge of **GGUF quantizations** (7 of the top 10 by downloads) signals a community‑wide push for efficient local deployment, and niche fine‑tunes like **HauhauCS/Qwen3.6‑35B‑A3B‑Uncensored** (2,488 likes) and **yuxinlu1/gemma‑4‑12B‑coder‑fable5** (2,610 likes) highlight demand for uncensored and coding‑specialized agents. Among new base model releases, **deepseek‑ai/DeepSeek‑V4‑Pro‑DSpark** and **nvidia/GLM‑5.2‑NVFP4** indicate that both frontier labs and hardware vendors are iterating rapidly on sparse architectures.

---

## Trending Models by Category

### 🧠 Language Models (LLMs, chat, instruction‑tuned)

| Model | Author | Likes | Downloads | Summary |
|-------|--------|-------|-----------|---------|
| [GLM-5.2](https://huggingface.co/zai-org/GLM-5.2) | zai-org | 3,470 | 220,379 | The latest generation of the GLM MoE conversational model, setting a new community benchmark for open‑weight Chinese‑friendly LLMs. |
| [DeepSeek-V4-Pro-DSpark](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-DSpark) | deepseek-ai | 391 | 12,580 | Next‑gen DeepSeek‑V4 variant optimized for distributed inference with DSpark, backed by a companion technical report (arxiv:2606.19348). |
| [DeepSeek-V4-Flash-DSpark](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-DSpark) | deepseek-ai | 162 | 48,696 | Faster, smaller sibling of DeepSeek‑V4‑Pro, also using DSpark acceleration – popular for lightweight deployments. |
| [Leanstral-1.5-119B-A6B](https://huggingface.co/mistralai/Leanstral-1.5-119B-A6B) | mistralai | 117 | 26 | Mistral’s massive 119B‑parameter MoE (6B active) built on Leanstral‑2603, designed for high‑throughput chat and code via vLLM. |
| [Nemotron-Labs-TwoTower-30B-A3B-Base-BF16](https://huggingface.co/nvidia/Nemotron-Labs-TwoTower-30B-A3B-Base-BF16) | nvidia | 123 | 10,696 | NVIDIA’s experimental two‑tower MoE architecture (30B total, 3B active) targeting efficient reasoning and multi‑task scaling. |
| [fable-traces](https://huggingface.co/AliesTaha/fable-traces) | AliesTaha | 162 | 277 | A Qwen3‑based instruction fine‑tune exploring trace‑level alignment for better tool‑use and agent reasoning. |
| [Qwen-AgentWorld-35B-A3B](https://huggingface.co/Qwen/Qwen-AgentWorld-35B-A3B) | Qwen | 549 | 55,113 | Qwen’s dedicated agent‑oriented MoE model, optimized for hierarchical planning and multi‑step tool execution. |

### 🎨 Multimodal & Generation (image, video, text‑to‑X)

| Model | Author | Likes | Downloads | Summary |
|-------|--------|-------|-----------|---------|
| [Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR) | baidu | 1,750 | 1,044,217 | Baidu’s state‑of‑the‑art OCR model capable of handling arbitrary‑length documents without cropping – a workhorse for digitization workflows. |
| [LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B) | nvidia | 2,618 | 1,247,265 | A compact 3B vision‑language model for open‑vocabulary object localization, trending for its zero‑shot grounding accuracy. |
| [Krea-2-Turbo](https://huggingface.co/krea/Krea-2-Turbo) | krea | 515 | 99,049 | Turbo variant of Krea‑2 for high‑speed text‑to‑image generation, built on top of the Krea‑2‑Raw base model. |
| [Krea-2](https://huggingface.co/Comfy-Org/Krea-2) | Comfy-Org | 256 | 10 | Official ComfyUI release of Krea‑2, the core image generation model now bundled with workflow‑compatible nodes. |
| [Qwythos-9B-Claude-Mythos-5-1M (full)](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M) | empero-ai | 688 | 144,933 | Full‑precision version of the Qwen3.5‑based multimodal fine‑tune that blends Claude‑style reasoning with “Mythos” storytelling. |
| [Ornith-1.0-9B](https://huggingface.co/deepreinforce-ai/Ornith-1.0-9B) | deepreinforce-ai | 385 | 76,189 | The 9B base member of the Ornith family, a Qwen3.5‑inspired multimodal model trained for both text and vision tasks. |
| [Ornith-1.0-35B](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B) | deepreinforce-ai | 342 | 224,641 | Larger 35B MoE sibling of Ornith‑1.0, offering stronger multimodal performance while keeping active parameters low. |
| [DavidAU/Qwen3.5-9B-Claude-4.6-HighIQ…](https://huggingface.co/DavidAU/Qwen3.5-9B-Claude-4.6-HighIQ-THINKING-HERETIC-UNCENSORED) | DavidAU | 153 | 53,962 | An uncensored, thinking‑enhanced fine‑tune of Qwen3.5‑9B optimized for role‑play and creative reasoning. |

### 🔧 Specialized Models (code, math, tabular, embeddings, security)

| Model | Author | Likes | Downloads | Summary |
|-------|--------|-------|-----------|---------|
| [tabfm-1.0.0-pytorch](https://huggingface.co/google/tabfm-1.0.0-pytorch) | google | 226 | 2,670 | Google’s TabFM foundation model for zero‑shot classification and regression on tabular data – a rare entry pushing structured‑data transformers. |
| [rampart](https://huggingface.co/nationaldesignstudio/rampart) | nationaldesignstudio | 129 | 2,783 | A BERT‑based PII‑detection model packaged for ONNX and Transformers.js, enabling client‑side privacy filtering. |

### 📦 Fine‑tunes & Quantizations (GGUF, AWQ, NVFP4, abliterated)

| Model | Author | Likes | Downloads | Summary |
|-------|--------|-------|-----------|---------|
| [Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF) | empero-ai | 1,560 | 1,533,844 | Quantized GGUF variant of the Qwythos multimodal fine‑tune, wildly popular for local inference of “Claude‑Mythos” storytelling. |
| [Ornith-1.0-35B-GGUF](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B-GGUF) | deepreinforce-ai | 731 | 394,164 | GGUF‑quantized version of the 35B Ornith MoE, enabling high‑quality multimodal chat on consumer hardware. |
| [gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF) | yuxinlu1 | 2,610 | 651,758 | A GGUF‑quantized Gemma‑4‑12B fine‑tune for code generation with the “fable5” reasoning recipe – top by likes in its category. |
| [gemma-4-12B-agentic-fable5-composer2.5-v2…GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF) | yuxinlu1 | 1,029 | 355,871 | An agentic variant of the same Gemma‑4 fine‑tune, optimized for terminal tool‑use and multi‑step autonomy. |
| [Qwen3.6-27B-NVFP4](https://huggingface.co/nvidia/Qwen3.6-27B-NVFP4) | nvidia | 274 | 297,130 | NVIDIA’s own 4‑bit floating‑point quantization of Qwen3.6‑27B, demonstrating ModelOpt compression for sustained throughput. |
| [HauhauCS/Qwen3.6-35B-A3B-Uncensored…GGUF](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive) | HauhauCS | 2,488 | 3,018,257 | The most downloaded model in the list – a highly aggressive, uncensored GGUF of Qwen3.6‑35B MoE, popular for unrestricted chatting. |
| [Huihui-GLM-5.2-abliterated-GGUF](https://huggingface.co/huihui-ai/Huihui-GLM-5.2-abliterated-GGUF) | huihui-ai | 169 | 5,609 | An abliterated (safety‑removed) GGUF of GLM‑5.2, appealing to users who want maximal creative freedom. |
| [Ornith-1.0-9B-GGUF](https://huggingface.co/deepreinforce-ai/Ornith-1.0-9B-GGUF) | deepreinforce-ai | 434 | 352,002 | Lighter 9B GGUF of the Ornith family, balancing performance and portability for local multimodal use. |
| [Qwopus3.6-35B-A3B-Coder-MTP-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-35B-A3B-Coder-MTP-GGUF) | Jackrong

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*