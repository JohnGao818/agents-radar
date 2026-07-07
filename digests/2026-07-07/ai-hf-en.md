# Hugging Face Trending Models Digest 2026-07-07

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-07-07 02:42 UTC

---

# Hugging Face Trending Models Digest — 2026-07-07

## Today's Highlights

The Hugging Face ecosystem is showing a clear concentration around the **Qwen 3.5/3.6** family as the dominant base for community fine-tuning and quantization, with numerous GGUF variants of Qwen-based models dominating downloads. **Nvidia** is making a strong multi-model push with quantization innovations (NVFP4) and specialized vision tools, while **deepreinforce-ai** emerges as a notable new player with the Ornith series. The "abliterated" trend continues to grow, with uncensored variants of GLM-5.2 and Qwen models gaining traction. A particularly interesting development is the rise of **tabular and non-language models** (Google's tabfm, nvidia's LocateAnything) breaking into the trending charts alongside traditional LLMs.

---

## Trending Models

### 🧠 Language Models (LLMs, chat models, instruction-tuned)

- **zai-org/GLM-5.2** ([link](https://huggingface.co/zai-org/GLM-5.2)) — Author: zai-org | Likes: 3,535 | Downloads: 231,218
  - A powerful conversational MoE model from the GLM family, trending as the highest-liked model this week, likely due to strong performance in Chinese and English benchmarks.
- **deepreinforce-ai/Ornith-1.0-35B-GGUF** ([link](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B-GGUF)) — Author: deepreinforce-ai | Likes: 759 | Downloads: 436,780
  - A 35B MoE model (based on Qwen3.5) in GGUF format, trending for its strong MIT-licensed open-weight release and endpoint compatibility.
- **deepreinforce-ai/Ornith-1.0-9B-GGUF** ([link](https://huggingface.co/deepreinforce-ai/Ornith-1.0-9B-GGUF)) — Author: deepreinforce-ai | Likes: 442 | Downloads: 393,142
  - Smaller sibling of Ornith-35B, offering strong performance in a compact form factor for local deployment.
- **deepreinforce-ai/Ornith-1.0-35B** ([link](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B)) — Author: deepreinforce-ai | Likes: 351 | Downloads: 231,342
  - The full-precision version of the 35B MoE model, gaining attention as an open-weights alternative to larger proprietary systems.
- **deepreinforce-ai/Ornith-1.0-9B** ([link](https://huggingface.co/deepreinforce-ai/Ornith-1.0-9B)) — Author: deepreinforce-ai | Likes: 393 | Downloads: 86,136
  - Full-precision 9B version of the Ornith series, offering a lightweight but capable LLM for inference.
- **deepseek-ai/DeepSeek-V4-Pro-DSpark** ([link](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-DSpark)) — Author: deepseek-ai | Likes: 409 | Downloads: 14,276
  - DeepSeek's latest flagship model with accompanying research paper (arXiv:2606.19348), showing DeepSeek's continued momentum in open-weight reasoning models.
- **Qwen/Qwen-AgentWorld-35B-A3B** ([link](https://huggingface.co/Qwen/Qwen-AgentWorld-35B-A3B)) — Author: Qwen | Likes: 556 | Downloads: 57,835
  - A Qwen3.5 MoE model specialized for agentic tasks, trending as Qwen's official entry into the agent-capable LLM space.
- **InternScience/Agents-A1** ([link](https://huggingface.co/InternScience/Agents-A1)) — Author: InternScience | Likes: 345 | Downloads: 8,766
  - A MoE model designed for agentic workflows, also based on Qwen3.5, demonstrating the "agents on MoE" trend.
- **meituan-longcat/LongCat-2.0** ([link](https://huggingface.co/meituan-longcat/LongCat-2.0)) — Author: meituan-longcat | Likes: 117 | Downloads: 43
  - A conversational model from Meituan's LongCat series, newly released and still gathering initial traction.
- **mistralai/Leanstral-1.5-119B-A6B** ([link](https://huggingface.co/mistralai/Leanstral-1.5-119B-A6B)) — Author: mistralai | Likes: 143 | Downloads: 106
  - Mistral's massive 119B MoE model (6B active), a new release pushing the boundaries of efficient large-scale language modeling.
- **nvidia/Nemotron-Labs-TwoTower-30B-A3B-Base-BF16** ([link](https://huggingface.co/nvidia/Nemotron-Labs-TwoTower-30B-A3B-Base-BF16)) — Author: nvidia | Likes: 126 | Downloads: 10,766
  - Nvidia's entry into the MoE LLM space with a novel "two-tower" architecture at 30B total / 3B active parameters.
- **froggeric/Qwen-Fixed-Chat-Templates** ([link](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates)) — Author: froggeric | Likes: 699 | Downloads: 0
  - A utility resource providing corrected Jinja chat templates for Qwen models, trending despite zero downloads — catching attention for solving a common Qwen deployment headache.

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **nvidia/LocateAnything-3B** ([link](https://huggingface.co/nvidia/LocateAnything-3B)) — Author: nvidia | Likes: 2,635 | Downloads: 1,340,559
  - A 3B image-text-to-text model for zero-shot object localization, trending as Nvidia's most popular multimodal release with huge download count.
- **baidu/Unlimited-OCR** ([link](https://huggingface.co/baidu/Unlimited-OCR)) — Author: baidu | Likes: 1,797 | Downloads: 1,070,230
  - Baidu's universal OCR model handling various document formats, trending for its practical "unlimited" OCR capability and strong download velocity.
- **empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF** ([link](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)) — Author: empero-ai | Likes: 1,644 | Downloads: 1,617,508
  - A 9B image-text-to-text GGUF model incorporating "Claude-Mythos" data, trending as the most-downloaded GGUF vision model this week.
- **HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive** ([link](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)) — Author: HauhauCS | Likes: 2,529 | Downloads: 2,910,241
  - An "uncensored" aggressive variant of Qwen3.6 35B vision MoE in GGUF, trending extremely well — likely the most downloaded model this week.
- **unsloth/Qwen3.6-27B-MTP-GGUF** ([link](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)) — Author: unsloth | Likes: 974 | Downloads: 2,818,499
  - Unsloth's optimized GGUF quantization of Qwen3.6 27B with multi-token prediction, massively popular for local vision LLM deployment.
- **empero-ai/Qwythos-9B-Claude-Mythos-5-1M** ([link](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M)) — Author: empero-ai | Likes: 702 | Downloads: 149,421
  - The full-precision version of the Qwythos-9B vision model, gaining traction alongside its GGUF variant.
- **tencent/Hy3** ([link](https://huggingface.co/tencent/Hy3)) — Author: tencent | Likes: 342 | Downloads: 2
  - A newly released text-generation model from Hunyuan/Tencent, still very early in adoption but notable as a major Chinese tech entry.
- **krea/Krea-2-Turbo** ([link](https://huggingface.co/krea/Krea-2-Turbo)) — Author: krea | Likes: 529 | Downloads: 109,470
  - A text-to-image diffusion model built on Krea-2-Raw, trending as a fast, high-quality image generation model from the Krea ecosystem.
- **Jackrong/Qwopus3.6-35B-A3B-Coder-MTP-GGUF** ([link](https://huggingface.co/Jackrong/Qwopus3.6-35B-A3B-Coder-MTP-GGUF)) — Author: Jackrong | Likes: 151 | Downloads: 126,831
  - A Qwen3.6-based GGUF vision & coding model with multi-token prediction, bridging coding and vision capabilities.
- **yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF** ([link](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)) — Author: yuxinlu1 | Likes: 1,052 | Downloads: 370,884
  - A Gemma-4-based GGUF model optimized for agentic and terminal tasks, trending as a strong mid-size agent model.
- **DavidAU/Qwen3.5-9B-Claude-4.6-HighIQ-THINKING-HERETIC-UNCENSORED** ([link](https://huggingface.co/DavidAU/Qwen3.5-9B-Claude-4.6-HighIQ-THINKING-HERETIC-UNCENSORED)) — Author: DavidAU | Likes: 158 | Downloads: 58,755
  - A fine-tuned Qwen3.5 model with uncensored "HighIQ" thinking — part of the growing uncensored fine-tuning trend.

### 🔧 Specialized Models (code, math, medical, embeddings, tabular)

- **google/tabfm-1.0.0-pytorch** ([link](https://huggingface.co/google/tabfm-1.0.0-pytorch)) — Author: google | Likes: 257 | Downloads: 7,036
  - Google's TabFM foundation model for tabular classification and regression with zero-shot capabilities, notable as a rare non-LLM trending model — signals growing interest in tabular AI.
- **yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF** ([link](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)) — Author: yuxinlu1 | Likes: 2,623 | Downloads: 664,319
  - A Gemma-4 GGUF model specialized for coding and reasoning, extremely popular as a local code assistant.
- **nationaldesignstudio/rampart** ([link](https://huggingface.co/nationaldesignstudio/rampart)) — Author: nationaldesignstudio | Likes: 136 | Downloads: 3,821
  - A BERT-based token-classification model for PII detection, optimized for ONNX/Transformers.js — trending for its practical privacy/security application.
- **eric-venti-seeds/Sun-Direction-Lora-Flux2Klein9B** ([link](https://huggingface.co/eric-venti-seeds/Sun-Direction-Lora-Flux2Klein9B)) — Author: eric-venti-seeds | Likes: 80 | Downloads: 0
  - A LoRA for lighting/sun-direction control in Flux2Klein9B, still early but indicative of the growing Flux/LoRA ecosystem.

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **huihui-ai/Huihui-GLM-5.2-abliterated-GGUF** ([link](https://huggingface.co/huihui-ai/Huihui-GLM-5.2-abliterated-GGUF)) — Author: huihui-ai | Likes: 178 | Downloads: 6,660
  - An "abliterated" (safety-filter-removed) GGUF variant of GLM-5.2, part of the growing uncensored model ecosystem.
- **nvidia/Qwen3.6-27B-NVFP4** ([link](https://huggingface.co/nvidia/Qwen3.6-27B-NVFP4)) — Author: nvidia | Likes: 290 | Downloads: 430,676
  - Nvidia's NVFP4 (4-bit floating point) quantization of Qwen3.6 27B using ModelOpt, a new quantization format that preserves more FP4 precision than traditional methods.
- **yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF** ([link](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)) — Author: yuxinlu1 | Likes: 1,052 | Downloads: 370,884
  - (Also listed above) A GGUF quantization of a community fine-tune on Gemma-4, showing the blend of fine-tuning and quantization.
- **yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF** ([link](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)) — Author: yuxinlu1 | Likes: 2,623 | Downloads: 664,319
  - (Also listed above) The coding-focused variant of the same Gemma-4 GGUF series.
- **unsloth/Qwen3.6-27B-MTP-GGUF** ([link](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)) — Author: unsloth | Likes: 974 | Downloads: 2,818,499
  - (Also listed above) Unsloth's toolchain for fast GGUF conversion remains the go-to for community quantization.

---

## Ecosystem Signal

**Qwen 3.5/3.6 is the dominant base model family this week**, appearing as the foundation

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*