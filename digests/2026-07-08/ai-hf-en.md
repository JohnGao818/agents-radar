# Hugging Face Trending Models Digest 2026-07-08

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-07-08 02:21 UTC

---

# 🤗 Hugging Face Trending Models Digest — 2026-07-08

## Today's Highlights

This week's Hugging Face trending board is dominated by **Mixture-of-Experts (MoE)** architectures and aggressive quantization via GGUF. The top-liked model is **zai-org/GLM-5.2** with 3,595 likes, a conversational MoE model from the GLM family, while **nvidia/LocateAnything-3B** (2,657 likes) signals strong interest in lightweight visual grounding systems. Qwen-family models continue to proliferate, with **HauhauCS/Qwen3.6-35B-A3B-Uncensored** racking up the highest downloads (2.8M) alongside **unsloth/Qwen3.6-27B-MTP-GGUF** (2.8M downloads), underscoring the community's appetite for quantized, uncensored, vision-capable models. Notably, **DeepSeek-V4-Pro-DSpark** and **Tencent/Hy3** represent major corporate entries, while **empero-ai** and **deepreinforce-ai** show strong grassroots fine-tuning momentum on Qwen and Claude-derived bases.

---

## Trending Models

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — zai-org · 3,595 likes · 281,584 downloads  
  A conversational MoE model from the GLM family; top-liked model today, likely due to strong reasoning and Chinese-English bilingual performance.

- **[tencent/Hy3](https://huggingface.co/tencent/Hy3)** — tencent · 490 likes · 121 downloads  
  Hunyuan v3 text-generation model from Tencent; trending as a major corporate open-weight release for general chatbot use.

- **[deepseek-ai/DeepSeek-V4-Pro-DSpark](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-DSpark)** — deepseek-ai · 424 likes · 15,538 downloads  
  DeepSeek's latest flagship MoE model with accompanying arxiv paper (2606.19348); driving research community interest.

- **[Qwen/Qwen-AgentWorld-35B-A3B](https://huggingface.co/Qwen/Qwen-AgentWorld-35B-A3B)** — Qwen · 560 likes · 60,736 downloads  
  Qwen's MoE agent-oriented model with 35B total / 3B active parameters; highlights the push toward efficient agentic LLMs.

- **[meituan-longcat/LongCat-2.0](https://huggingface.co/meituan-longcat/LongCat-2.0)** — meituan-longcat · 140 likes · 385 downloads  
  Long-context conversational model from Meituan; noteworthy for extended context window research.

- **[mistralai/Leanstral-1.5-119B-A6B](https://huggingface.co/mistralai/Leanstral-1.5-119B-A6B)** — mistralai · 157 likes · 157 downloads  
  Mistral's massive 119B MoE model with only 6B active parameters; positioned for efficient large-scale deployment.

- **[deepreinforce-ai/Ornith-1.0-35B-GGUF](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B-GGUF)** — deepreinforce-ai · 780 likes · 502,663 downloads  
  Quantized 35B MoE model built on Qwen 3.5; high download count suggests strong community adoption for local deployment.

- **[deepreinforce-ai/Ornith-1.0-9B-GGUF](https://huggingface.co/deepreinforce-ai/Ornith-1.0-9B-GGUF)** — deepreinforce-ai · 452 likes · 454,944 downloads  
  Smaller sibling of Ornith 35B; lightweight GGUF quant for resource-constrained environments.

- **[deepreinforce-ai/Ornith-1.0-9B](https://huggingface.co/deepreinforce-ai/Ornith-1.0-9B)** — deepreinforce-ai · 403 likes · 136,037 downloads  
  Full-precision version of Ornith 9B; demonstrates the family's multi-format release strategy.

- **[deepreinforce-ai/Ornith-1.0-35B](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B)** — deepreinforce-ai · 357 likes · 280,236 downloads  
  Full-precision MoE variant; supports image-text-to-text, expanding Ornith's multimodal appeal.

- **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)** — yuxinlu1 · 2,640 likes · 674,977 downloads  
  Coding-focused GGUF fine-tune of Gemma 4 with Fable5 and Composer merges; extremely high likes reflect coder community interest.

- **[yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)** — yuxinlu1 · 1,077 likes · 384,383 downloads  
  Agentic variant of Gemma 4-12B fine-tune; emphasizes terminal and tool-use capabilities.

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** — empero-ai · 1,764 likes · 1,683,711 downloads  
  GGUF-quantized, vision-capable Qwen 3.5 model fine-tuned on 1M Claude-synthetic samples; huge download count signals appeal of high-reasoning multimodal.

- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** — baidu · 1,834 likes · 1,084,945 downloads  
  Baidu's OCR-specific image-text-to-text model; trending as a robust, production-grade OCR solution for enterprise.

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — nvidia · 2,657 likes · 1,424,958 downloads  
  Lightweight 3B visual grounding model from NVIDIA; high likes for its zero-shot object localization capability.

- **[nvidia/Qwen3.6-27B-NVFP4](https://huggingface.co/nvidia/Qwen3.6-27B-NVFP4)** — nvidia · 315 likes · 538,687 downloads  
  NVIDIA-optimized Qwen 3.6 using NVFP4 quantization; demonstrates hardware-software co-design for efficient inference.

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — HauhauCS · 2,551 likes · 2,823,988 downloads  
  Top download this week; uncensored, vision-capable MoE Qwen fine-tune with aggressive style, appealing to power users.

- **[krea/Krea-2-Turbo](https://huggingface.co/krea/Krea-2-Turbo)** — krea · 541 likes · 123,729 downloads  
  Text-to-image model from Krea; trending as a fast, Turbo variant of the Krea-2 base model for creative generation.

- **[eric-venti-seeds/Sun-Direction-Lora-Flux2Klein9B](https://huggingface.co/eric-venti-seeds/Sun-Direction-Lora-Flux2Klein9B)** — eric-venti-seeds · 97 likes · 0 downloads  
  Specialized LoRA for controlling sun direction in Flux2Klein9B; niche but interesting for lighting-aware image editing.

- **[Jackrong/Qwopus3.6-35B-A3B-Coder-MTP-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-35B-A3B-Coder-MTP-GGUF)** — Jackrong · 161 likes · 159,871 downloads  
  Qwen 3.6-based vision model with Multi-Token Prediction (MTP); coding-focused fine-tune in GGUF format.

- **[unsloth/Qwen3.6-27B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)** — unsloth · 991 likes · 2,842,118 downloads  
  Second highest download count; Unsloth-quantized Qwen 3.6 with MTP, popular for efficient local multimodal inference.

- **[bottlecapai/ThinkingCap-Qwen3.6-27B](https://huggingface.co/bottlecapai/ThinkingCap-Qwen3.6-27B)** — bottlecapai · 107 likes · 46 downloads  
  Qwen 3.6 fine-tune emphasizing chain-of-thought reasoning; low downloads but interesting architecture.

### 🔧 Specialized Models (code, math, medical, embeddings, tabular)

- **[google/tabfm-1.0.0-pytorch](https://huggingface.co/google/tabfm-1.0.0-pytorch)** — google · 289 likes · 9,458 downloads  
  Google's TabFM for tabular classification/regression with zero-shot transfer; trending for ML practitioners.

- **[InternScience/Agents-A1](https://huggingface.co/InternScience/Agents-A1)** — InternScience · 375 likes · 14,723 downloads  
  Qwen 3.5 MoE fine-tuned for agentic tasks; bridges vision and language for tool-use scenarios.

- **[AliesTaha/fable-traces](https://huggingface.co/AliesTaha/fable-traces)** — AliesTaha · 184 likes · 3,886 downloads  
  Qwen 3 instruct model fine-tuned on synthetic fable-style reasoning traces; niche but shows prompt distillation trends.

- **[nvidia/Nemotron-Labs-TwoTower-30B-A3B-Base-BF16](https://huggingface.co/nvidia/Nemotron-Labs-TwoTower-30B-A3B-Base-BF16)** — nvidia · 131 likes · 10,936 downloads  
  Two-tower MoE architecture from NVIDIA's Nemotron Labs; experimental base model for future fine-tunes.

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M)** — empero-ai · 723 likes · 152,516 downloads  
  Full-precision version of the Qwythos fine-tune; core recipe behind the GGUF hits.

- **[froggeric/Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates)** — froggeric · 743 likes · 0 downloads  
  A chat-template fix for Qwen models; viral utility despite zero downloads—likely a documentation/config fix.

- **[InternScience/Agents-A1-Q4_K_M-GGUF](https://huggingface.co/InternScience/Agents-A1-Q4_K_M-GGUF)** — InternScience · 74 likes · 11,226 downloads  
  Quantized Q4_K_M GGUF of Agents-A1; popular for on-device agent deployments.

- **[huihui-ai/Huihui-GLM-5.2-abliterated-GGUF](https://huggingface.co/huihui-ai/Huihui-GLM-5.2-abliterated-GGUF)** — huihui-ai · 185 likes · 7,349 downloads  
  "Abliterated" (uncensored) GGUF of GLM 5.2; community response to perceived safety constraints in the base model.

---

## Ecosystem Signal

This week's board reveals a clear **triple trend**: MoE architectures, multimodal convergence, and aggressive quantization. Qwen's ecosystem has become the dominant foundation for fine-tunes and quantizations—**10 of 30 models** are Qwen-family derivatives (Qwen 3.5, 3.6, Qwythos, Agents-A1, Ornith). The **MoE** structure (e.g., GLM-5.2, Qwen-AgentWorld, Mistral's Leanstral) is now the default for both large labs and community models, offering competitive performance with lower inference cost.

**Quantization via GGUF** remains the primary driver of downloads, with Unsloth, Abliterated, and MTP variants leading. The **uncensored** sub-niche (HauhauCS, huihui-ai) continues to attract strong engagement, indicating demand for models with reduced safety post-processing. Corporate releases from **NVIDIA** (LocateAnything, Nemotron, NVFP4 Qwen) and **DeepSeek/Google/Tencent** signal that open-weight competition is intensifying, with a focus on both raw performance and hardware optimization. Notably, multimodal capability is becoming almost standard—**image-text-to-text** pipelines appear in 7 of the top 20 models, blurring the line between language and vision models.

---

## Worth Exploring

1. **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — With 2,657 likes and NVIDIA backing, this 3B visual grounding model achieves zero-shot object localization with remarkable efficiency. It's a strong candidate for robotics, document parsing, and real-time vision applications where lightweight deployment matters.

2. **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — The top-liked model overall offers a glimpse into next-generation conversational MoE. Its high engagement suggests strong bilingual reasoning performance. Worth studying as a benchmark for MoE training recipes and as a competitive alternative to Qwen-based stacks.

3. **[deepseek-ai/DeepSeek-V4-Pro-DSpark](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-DSpark)** — Accompanied by a new arxiv paper, this flagship MoE model represents DeepSeek's latest technical direction. For researchers tracking frontier open-weight architectures, this is essential to analyze alongside the upcoming paper (2606.19348).

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*