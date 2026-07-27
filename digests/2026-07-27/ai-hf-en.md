# Hugging Face Trending Models Digest 2026-07-27

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-07-27 02:32 UTC

---

Here is the structured digest for the Hugging Face trending models as of 2026-07-27.

---

## Today's Highlights

This week’s trending list is dominated by two major themes: the explosive growth of **open-weight MoE architectures** and the **proliferation of community fine-tunes** on the Qwen3.6/3.5 base. The standout is **zai-org/GLM-5.2** (4,480 likes), a massive MoE conversational model that has rapidly become the community’s most-talked-about release. Meanwhile, **Baidu’s Unlimited-OCR** (3,212 likes, 2.6M downloads) demonstrates a continued hunger for powerful, accessible OCR pipelines. A notable secondary trend is the arrival of specialized robotics models from **OpenBMB** and an unusually high concentration of **uncensored GGUF quantizations** on the Qwen3.6 family, suggesting a strong grassroots appetite for locally-deployable, unconstrained generation.

---

## Trending Models

### 🧠 Language Models (LLMs, chat, instruction-tuned)

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — Author: zai-org | Likes: 4,480 | Downloads: 827,191  
  A flagship open-weight MoE model with exceptional conversational performance, trending due to its state-of-the-art mix of scale, efficiency, and accessibility.

- **[poolside/Laguna-S-2.1](https://huggingface.co/poolside/Laguna-S-2.1)** — Author: poolside | Likes: 702 | Downloads: 56,445  
  A text-generation model from poolside, gaining traction as a strong general-purpose open-source baseline with multiple quantization variants.

- **[upstage/Solar-Open2-250B](https://huggingface.co/upstage/Solar-Open2-250B)** — Author: upstage | Likes: 596 | Downloads: 3,305  
  A 250B-parameter model from Upstage, pushing the frontier of very-large-scale open-weight LLMs and attracting developers seeking frontier-level capability.

- **[Nanbeige/Nanbeige4.2-3B](https://huggingface.co/Nanbeige/Nanbeige4.2-3B)** — Author: Nanbeige | Likes: 450 | Downloads: 14,049  
  A compact 3B-parameter language model that balances efficiency and quality, popular for resource-constrained deployment scenarios.

### 🎨 Multimodal & Generation (image, video, audio, text-to-X)

- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** — Author: baidu | Likes: 3,212 | Downloads: 2,593,460  
  A robust image-text-to-text OCR model with massive download numbers, dominating the practical document-understanding space.

- **[thinkingmachines/Inkling](https://huggingface.co/thinkingmachines/Inkling)** — Author: thinkingmachines | Likes: 1,579 | Downloads: 34,511  
  A conversational multimodal model designed for image-text interaction, trending as a flexible vision-language assistant.

- **[moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)** — Author: moonshotai | Likes: 1,298 | Downloads: 730,129  
  A compressed, code-specialized multimodal model with strong reasoning capabilities, widely adopted for on-device coding tasks.

- **[ATH-MaaS/OvisOCR2](https://huggingface.co/ATH-MaaS/OvisOCR2)** — Author: ATH-MaaS | Likes: 310 | Downloads: 35,562  
  A Qwen3.5-based OCR system, following the trend of specialized vision-language models for document processing.

- **[microsoft/Fara1.5-27B](https://huggingface.co/microsoft/Fara1.5-27B)** — Author: microsoft | Likes: 110 | Downloads: 1,225  
  A vision-language model fine-tuned for computer-use tasks (GUI agents), reflecting industry interest in digital automation.

- **[microsoft/Mage-Flow](https://huggingface.co/microsoft/Mage-Flow)** — Author: microsoft | Likes: 336 | Downloads: 1,375  
  A text-to-image diffusion model with editing capabilities, Microsoft’s latest entry in the generative imaging space.

- **[microsoft/Mage-Flow-Edit-Turbo](https://huggingface.co/microsoft/Mage-Flow-Edit-Turbo)** — Author: microsoft | Likes: 89 | Downloads: 946  
  A turbo-charged image-to-image editing variant of Mage-Flow, optimized for instruction-based edits.

- **[owensong/Inflect-Micro-v2](https://huggingface.co/owensong/Inflect-Micro-v2)** — Author: owensong | Likes: 180 | Downloads: 298  
  A CPU-friendly text-to-speech model designed for local and edge deployment, serving the growing local-TTS community.

- **[nvidia/Cosmos3-Edge](https://huggingface.co/nvidia/Cosmos3-Edge)** — Author: nvidia | Likes: 125 | Downloads: 32,700  
  Nvidia’s latest diffusion-model for edge-based image/video generation, signaling the push for on-device generative media.

- **[conradlocke/krea2-identity-edit](https://huggingface.co/conradlocke/krea2-identity-edit)** — Author: conradlocke | Likes: 544 | Downloads: 0  
  A LoRA for Krea-2-Raw enabling identity-preserving image editing, trending despite zero downloads (likely published just before the snapshot).

- **[baseten/GLM-5.2-Vision-NVFP4](https://huggingface.co/baseten/GLM-5.2-Vision-NVFP4)** — Author: baseten | Likes: 114 | Downloads: 2,033  
  A quantized (NVFP4) multimodal variant of GLM-5.2, optimized for efficient vision-language inference.

### 🔧 Specialized Models (code, math, OCR, robotics, security)

- **[Kwaipilot/KAT-Coder-V2.5-Dev](https://huggingface.co/Kwaipilot/KAT-Coder-V2.5-Dev)** — Author: Kwaipilot | Likes: 198 | Downloads: 3,764  
  A MoE code model built on Qwen3.5, trending among developers for its strong programming-language comprehension.

- **[openbmb/MiniCPM-RobotManip](https://huggingface.co/openbmb/MiniCPM-RobotManip)** — Author: openbmb | Likes: 177 | Downloads: 643  
  A vision-language-action model for robotic manipulation, signaling the emergence of fine-tuned VLAs in open-source.

- **[openbmb/MiniCPM-RobotTrack](https://huggingface.co/openbmb/MiniCPM-RobotTrack)** — Author: openbmb | Likes: 130 | Downloads: 398  
  A companion robotics model focused on trajectory tracking, extending the MiniCPM family into embodied AI.

- **[fdtn-ai/antares-1b](https://huggingface.co/fdtn-ai/antares-1b)** — Author: fdtn-ai | Likes: 187 | Downloads: 5,978  
  A security-focused 1B model with a hybrid MoE architecture, gaining attention for its specialized threat-detection capabilities.

- **[Motif-Technologies/Motif-3-Beta](https://huggingface.co/Motif-Technologies/Motif-3-Beta)** — Author: Motif-Technologies | Likes: 193 | Downloads: 2,400  
  A feature-extraction model from Motif, designed for embedding and retrieval tasks rather than generative chat.

### 📦 Fine-tunes & Quantizations (community fine-tunes, GGUF, AWQ)

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — Author: HauhauCS | Likes: 3,112 | Downloads: 1,927,138  
  The most popular uncensored Qwen3.6 fine-tune with aggressive instruction-following, driving massive download numbers.

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** — Author: empero-ai | Likes: 2,480 | Downloads: 1,410,054  
  A GGUF-quantized reasoning model blending Qwen3.

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*