# Hugging Face Trending Models Digest 2026-06-07

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-06-07 03:30 UTC

---

# Hugging Face Trending Models Digest – 2026-06-07

## Today’s Highlights

DeepSeek continues its dominance with **DeepSeek‑V4‑Pro** (4,681 weekly likes) and **DeepSeek‑V4‑Flash** (1,421 likes), cementing the V4 family as the most downloaded and liked LLM family this week. Meanwhile, **nvidia** has made a massive push across modalities—from the landmark **LocateAnything‑3B** (object detection via text) to the **Cosmos3** omni‑models (text‑to‑image, image‑to‑video, and the full‑stack Super variant). The trend toward **mixture‑of‑experts (MoE)** and **quantized inference** is unmistakable: models like **Qwen3.6‑35B‑A3B** (both the uncensored GGUF‑variant and nvidia’s NVFP4‑packed version) and **LiquidAI’s LFM2.5‑8B‑A1B** are attracting serious developer interest for their efficiency and performance tradeoffs. Finally, the **Gemma‑4** series from Google, with its “any‑to‑any” multimodal pipeline, signals a shift toward truly unified models that can handle vision, language, and audio in a single architecture.

## Trending Models by Category

### 🧠 Language Models (LLMs, Chat, Instruction‑Tuned)

- **[deepseek‑ai/DeepSeek‑V4‑Pro](https://huggingface.co/deepseek‑ai/DeepSeek‑V4‑Pro)**  
  Author: deepseek‑ai | Likes: 4,681 | Downloads: 5.5M  
  The flagship open‑weight conversational LLM from DeepSeek, surging as the community’s go‑to for high‑performance chat and reasoning.

- **[deepseek‑ai/DeepSeek‑V4‑Flash](https://huggingface.co/deepseek‑ai/DeepSeek‑V4‑Flash)**  
  Author: deepseek‑ai | Likes: 1,421 | Downloads: 3.4M  
  A faster, more accessible variant of V4, optimized for deployment and real‑time applications.

- **[sapientinc/HRM‑Text‑1B](https://huggingface.co/sapientinc/HRM‑Text‑1B)**  
  Author: sapientinc | Likes: 712 | Downloads: 161K  
  A 1B‑parameter text‑generation model from Sapient, trending for its potential in human‑resource‑related reasoning tasks.

- **[LiquidAI/LFM2.5‑8B‑A1B](https://huggingface.co/LiquidAI/LFM2.5‑8B‑A1B)**  
  Author: LiquidAI | Likes: 534 | Downloads: 95K  
  A MoE model (8B total, 1B active) that delivers strong performance for its size, capitalizing on the MoE wave.

- **[JetBrains/Mellum2‑12B‑A2.5B‑Thinking](https://huggingface.co/JetBrains/Mellum2‑12B‑A2.5B‑Thinking)**  
  Author: JetBrains | Likes: 240 | Downloads: 16K  
  JetBrains’ entry into conversational AI with a 12B MoE model that emphasizes “thinking” mechanisms for code and logic tasks.

- **[openbmb/MiniCPM5‑1B](https://huggingface.co/openbmb/MiniCPM5‑1B)**  
  Author: openbmb | Likes: 775 | Downloads: 100K  
  A compact 1B parameter LLM that punches above its weight, popular for on‑device and edge deployments.

### 🎨 Multimodal & Generation (Image, Video, Audio, Text‑to‑X)

- **[nvidia/LocateAnything‑3B](https://huggingface.co/nvidia/LocateAnything‑3B)**  
  Author: nvidia | Likes: 1,459 | Downloads: 111K  
  A state‑of‑the‑art object localization model that can locate any object in an image via text prompts, trending as a foundational computer‑vision tool.

- **[google/gemma‑4‑12B‑it](https://huggingface.co/google/gemma‑4‑12B‑it)**  
  Author: google | Likes: 621 | Downloads: 315K  
  Google’s “any‑to‑any” instruction‑tuned multimodal model (text, image, audio), sparking interest as a unified foundation for multimodal agents.

- **[ideogram‑ai/ideogram‑4‑fp8](https://huggingface.co/ideogram‑ai/ideogram‑4‑fp8)**  
  Author: ideogram‑ai | Likes: 311 | Downloads: 2.8K  
  A high‑quality text‑to‑image diffusion model with FP8 quantization, balancing output fidelity and inference speed.

- **[stepfun‑ai/Step‑3.7‑Flash](https://huggingface.co/stepfun‑ai/Step‑3.7‑Flash)**  
  Author: stepfun‑ai | Likes: 343 | Downloads: 39K  
  A vision‑language model from StepFun that excels at image‑based reasoning and chat, gaining traction in East Asian AI circles.

- **[ByteDance/Bernini‑R](https://huggingface.co/ByteDance/Bernini‑R)**  
  Author: ByteDance | Likes: 151 | Downloads: 223  
  A novel image‑to‑video model that generates dynamic scenes from static images, accompanied by an arXiv paper and Apache‑2.0 license.

- **[nvidia/Cosmos3‑Super‑Text2Image](https://huggingface.co/nvidia/Cosmos3‑Super‑Text2Image)**  
  Author: nvidia | Likes: 120 | Downloads: 1.6K  
  Part of the Cosmos3 omni family, this sub‑model focuses on text‑to‑image generation with the quality expected from nvidia’s diffusion pipeline.

- **[SulphurAI/Sulphur‑2‑base](https://huggingface.co/SulphurAI/Sulphur‑2‑base)**  
  Author: SulphurAI | Likes: 1,581 | Downloads: 1.7M  
  A text‑to‑video diffusion model (base model: Lightricks/LTX‑2.3) that has exploded in downloads, likely due to its straightforward video generation from text prompts.

- **[nvidia/Cosmos3‑Super‑Image2Video](https://huggingface.co/nvidia/Cosmos3‑Super‑Image2Video)**  
  Author: nvidia | Likes: 111 | Downloads: 1.3K  
  The image‑to‑video counterpart of Cosmos3, enabling video generation conditioned on a single reference image.

- **[meituan‑longcat/LongCat‑Video‑Avatar‑1.5](https://huggingface.co/meituan‑longcat/LongCat‑Video‑Avatar‑1.5)**  
  Author: meituan‑longcat | Likes: 525 | Downloads: 1.8K  
  An audio‑text‑to‑video model for creating talking‑head avatars, from Meituan’s research team, drawing interest for virtual character applications.

- **[bosonai/higgs‑audio‑v3‑tts‑4b](https://huggingface.co/bosonai/higgs‑audio‑v3‑tts‑4b)**  
  Author: bosonai | Likes: 156 | Downloads: 2.2K  
  A large text‑to‑speech model (4B parameters) leveraging Qwen3 architecture, standing out for high‑fidelity voice synthesis.

- **[google/magenta‑realtime‑2](https://huggingface.co/google/magenta‑realtime‑2)**  
  Author: google | Likes: 111 | Downloads: 9.4K  
  A real‑time text‑to‑audio model from Google’s Magenta project, aimed at music and sound generation with low latency.

- **[nvidia/PiD](https://huggingface.co/nvidia/PiD)**  
  Author: nvidia | Likes: 312 | Downloads: 972  
  An image‑to‑image super‑resolution model, gaining interest from the photo‑enhancement and upscaling community.

### 🔧 Specialized Models (Speech, OCR, Feature Extraction)

- **[nvidia/nemotron‑3.5‑asr‑streaming‑0.6b](https://huggingface.co/nvidia/nemotron‑3.5‑asr‑streaming‑0.6b)**  
  Author: nvidia | Likes: 221 | Downloads: 1.4K  
  A streaming automatic speech recognition model (0.6B parameters) designed for low‑latency voice applications.

- **[PaddlePaddle/PaddleOCR‑VL‑1.6](https://huggingface.co/PaddlePaddle/PaddleOCR‑VL‑1.6)**  
  Author: PaddlePaddle | Likes: 258 | Downloads: 8.4K  
  The latest version of PaddleOCR’s vision‑language model, integrating ERNIE 4.5 for superior OCR and document understanding.

### 📦 Fine‑Tunes & Quantizations (GGUF, NVFP4, Community Variants)

- **[unsloth/gemma‑4‑12b‑it‑GGUF](https://huggingface.co/unsloth/gemma‑4‑12b‑it‑GGUF)**  
  Author: unsloth | Likes: 423 | Downloads: 458K  
  A GGUF‑quantized version of Google’s Gemma‑4 instruction‑tuned model, making it accessible on consumer hardware and edge devices.

- **[HauhauCS/Qwen3.6‑35B‑A3B‑Uncensored‑HauhauCS‑Aggressive](https://huggingface.co/HauhauCS/Qwen3.6‑35B‑A3B‑Uncensored‑HauhauCS‑Aggressive)**  
  Author: HauhauCS | Likes: 1,491 | Downloads: 2.8M  
  A community fine‑tune of the Qwen3.6 MoE model (35B total, 3B active) with uncensored and aggressive instruction tuning, heavily downloaded for its “no‑filter” behavior.

- **[nvidia/Qwen3.6‑35B‑A3B‑NVFP4](https://huggingface.co/nvidia/Qwen3.6‑35B‑A3B‑NVFP4)**  
  Author: nvidia | Likes: 198 | Downloads: 1M  
  An official nvidia‑optimized 4‑bit NVFP4 quantization of the Qwen3.6 MoE model, illustrating the industry push for efficient inference on RTX and datacenter GPUs.

- **[nvidia/NVIDIA‑Nemotron‑3‑Ultra‑550B‑A55B‑NVFP4](https://huggingface.co/nvidia/NVIDIA‑Nemotron‑3‑Ultra‑550B‑A55B‑NVFP4)**  
  Author: nvidia | Likes: 119 | Downloads: 17K  
  A quantized version of nvidia’s massive 550B MoE model, bringing enterprise‑grade reasoning to affordable GPU setups.

- **[ideogram‑ai/ideogram‑4‑nf4](https://huggingface.co/ideogram‑ai/ideogram‑4‑nf4)**  
  Author: ideogram‑ai | Likes: 213 | Downloads: 2.7K  
  A 4‑bit NF4 quantized variant of the Ideogram‑4 text‑to‑image model, reducing memory footprint while preserving generation quality.

## Ecosystem Signal

The week’s trending models reveal **three clear shifts** in the Hugging Face ecosystem:

1. **Mixture‑of‑Experts (MoE) is now mainstream.** More than half of the large‑scale LLMs in this digest use MoE architectures (DeepSeek‑V4, Qwen3.6, Nemotron‑3 Ultra, LFM2.5, Mellum2). The community is embracing sparse activation for better performance‑per‑parameter, and quantized MoE models (NVFP4, GGUF) are enabling these massive systems to run on consumer GPUs.

2. **Nvidia has become the most active corporate publisher** on Hugging Face, releasing models across the entire modality spectrum—from object localization (LocateAnything) and speech (Nemotron‑ASR) to omni‑diffusion (Cosmos3). This indicates a strategic push to dominate the open‑weight ecosystem, offering both foundation models and optimized quant

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*