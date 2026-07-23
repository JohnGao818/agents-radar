# Hugging Face Trending Models Digest 2026-07-23

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-07-23 02:23 UTC

---

# 🤗 Hugging Face Trending Models Digest — 2026-07-23

## Today's Highlights

This week's trending leaderboard is dominated by **extreme quantization** and **multimodal expansion**. The top model by likes is **zai-org/GLM-5.2** (4,339 likes), signaling strong community interest in MoE-based open-weight LLMs, while **google/gemma-4-31B-it** continues its explosive adoption with 12.1M+ downloads. A notable cluster of models from **prism-ml** (Bonsai, Ternary-Bonsai) demonstrates the community's appetite for sub-2-bit compression to run 27B models on consumer hardware. Meanwhile, **Qwen3.5/3.6 variants** (Uncensored, Claude-finetuned, GGUF) remain the most active base for fine-tuning, and **robotics VLA models** from openbmb point to an emerging applied-AI frontier.

---

## Trending Models by Category

### 🧠 Language Models (LLMs, Chat Models, Instruction-Tuned)

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — Author: zai-org | Likes: 4,339 | Downloads: 545,109  
  *A MoE-DSA conversational LLM, trending as the week's most-liked model and a clear leader in open-weight Chinese-English bilingual generation.*

- **[upstage/Solar-Open2-250B](https://huggingface.co/upstage/Solar-Open2-250B)** — Author: upstage | Likes: 296 | Downloads: 0  
  *A massive 250B open-weight LLM with sparse activation, generating buzz for its open release despite zero recorded downloads this week.*

- **[Nanbeige/Nanbeige4.2-3B](https://huggingface.co/Nanbeige/Nanbeige4.2-3B)** — Author: Nanbeige | Likes: 236 | Downloads: 0  
  *A compact 3B general-purpose LLM, drawing attention as an efficient small-model contender for edge deployment.*

- **[Motif-Technologies/Motif-3-Beta](https://huggingface.co/Motif-Technologies/Motif-3-Beta)** — Author: Motif-Technologies | Likes: 161 | Downloads: 125  
  *A new feature-extraction and generation model, likely an embedding-heavy foundation model gaining early traction.*

- **[google/gemma-4-31B-it](https://huggingface.co/google/gemma-4-31B-it)** — Author: google | Likes: 3,329 | Downloads: 12,113,203  
  *Google's latest 31B instruction-tuned multimodal model, trending with massive download volume reflecting widespread deployment.*

### 🎨 Multimodal & Generation (Image, Video, Audio, Text-to-X)

- **[thinkingmachines/Inkling](https://huggingface.co/thinkingmachines/Inkling)** — Author: thinkingmachines | Likes: 1,455 | Downloads: 16,441  
  *A multimodal conversational model (image+text in, text out) that is rapidly gaining community attention as a generalist vision-language agent.*

- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** — Author: baidu | Likes: 2,717 | Downloads: 2,237,351  
  *A high-performance OCR feature-extraction model from Baidu, trending due to its utility in document AI pipelines.*

- **[ATH-MaaS/OvisOCR2](https://huggingface.co/ATH-MaaS/OvisOCR2)** — Author: ATH-MaaS | Likes: 249 | Downloads: 17,162  
  *A Qwen3.5-based multimodal OCR model, gaining traction as a specialized vision-language tool for text extraction.*

- **[microsoft/Mage-Flow](https://huggingface.co/microsoft/Mage-Flow)** — Author: microsoft | Likes: 128 | Downloads: 0  
  *A Microsoft text-to-image generation model using diffusers, notable for positioning in the image-editing and generation space.*

- **[nvidia/Cosmos3-Edge](https://huggingface.co/nvidia/Cosmos3-Edge)** — Author: nvidia | Likes: 90 | Downloads: 6,623  
  *An NVIDIA Cosmos3 Edge model for diffusion-based generation, targeting edge-device deployment of generative AI.*

- **[Alissonerdx/LTX-Best-Face-ID](https://huggingface.co/Alissonerdx/LTX-Best-Face-ID)** — Author: Alissonerdx | Likes: 235 | Downloads: 0  
  *A text-to-video LoRA for identity-preserved reference-to-video generation, trending in the video-personalization niche.*

- **[OpenMOSS-Team/MOSS-Transcribe-Diarize](https://huggingface.co/OpenMOSS-Team/MOSS-Transcribe-Diarize)** — Author: OpenMOSS-Team | Likes: 308 | Downloads: 92,265  
  *An audio-text-to-text model combining transcription and speaker diarization, a rare end-to-end spoken-language understanding model.*

### 🔧 Specialized Models (Code, Robotics, ASR, Feature Extraction)

- **[moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)** — Author: moonshotai | Likes: 1,226 | Downloads: 722,058  
  *A compressed-tensor code-specialized model from Kimi AI, trending strongly among developers for its efficient code generation.*

- **[openbmb/MiniCPM-RobotManip](https://huggingface.co/openbmb/MiniCPM-RobotManip)** — Author: openbmb | Likes: 155 | Downloads: 58  
  *A vision-language-action model for robot manipulation, one of the few robotics VLA models gaining niche traction.*

- **[openbmb/MiniCPM-RobotTrack](https://huggingface.co/openbmb/MiniCPM-RobotTrack)** — Author: openbmb | Likes: 114 | Downloads: 72  
  *A companion VLA model for robot tracking and motion planning, signaling early interest in embodied AI on Hugging Face.*

- **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)** — Author: nvidia | Likes: 914 | Downloads: 590,230  
  *A streaming ASR model optimized for real-time speech recognition, trending due to its efficiency at 0.6B parameters.*

### 📦 Fine-tunes & Quantizations (Community Fine-tunes, GGUF, AWQ)

- **[prism-ml/Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)** — Author: prism-ml | Likes: 946 | Downloads: 432,196  
  *A 2-bit ternary quantized version of the Bonsai 27B model, enabling near-1-bit performance for massive model deployment.*

- **[prism-ml/Bonsai-27B-gguf](https://huggingface.co/prism-ml/Bonsai-27B-gguf)** — Author: prism-ml | Likes: 597 | Downloads: 1,404,962  
  *A 1-bit quantized 27B conversational model, one of the most downloaded GGUF models due to extreme compression.*

- **[prism-ml/Bonsai-27B-mlx-1bit](https://huggingface.co/prism-ml/Bonsai-27B-mlx-1bit)** — Author: prism-ml | Likes: 165 | Downloads: 25,273  
  *Apple MLX-compatible 1-bit version of Bonsai-27B, extending extreme quantization to Apple Silicon users.*

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — Author: HauhauCS | Likes: 3,004 | Downloads: 1,997,690  
  *An uncensored MoE vision-language GGUF fine-tune of Qwen3.6, extremely popular for its aggressive creative writing capabilities.*

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** — Author: empero-ai | Likes: 2,417 | Downloads: 2,133,420  
  *A 9B Qwen3.5-based GGUF fine-tune blending Claude-style reasoning with creative mythology, one of the highest-download community models.*

- **[DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF)** — Author: DavidAU | Likes: 324 | Downloads: 62,842  
  *A heavily fine-tuned (Unsloth-based) uncensored Qwen3.6 variant with extensive tagging, appealing to frontier experimenters.*

- **[bottlecapai/ThinkingCap-Qwen3.6-27B](https://huggingface.co/bottlecapai/ThinkingCap-Qwen3.6-27B)** — Author: bottlecapai | Likes: 514 | Downloads: 12,002  
  *A reasoning-enhanced Qwen3.6 multimodal model, trending for adding structured chain-of-thought to vision-language tasks.*

- **[unsloth/inkling-GGUF](https://huggingface.co/unsloth/inkling-GGUF)** — Author: unsloth | Likes: 120 | Downloads: 7,377  
  *An official GGUF quantization of the Inkling multimodal model, extending the original to efficient local inference.*

- **[GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-V2-Thinking-GGUF](https://huggingface.co/GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-V2-Thinking-GGUF)** — Author: GnLOLot | Likes: 154 | Downloads: 51,746  
  *A 1B GGUF fine-tune of MiniCPM5 with Claude-inspired response style, notable for packing advanced reasoning into a tiny footprint.*

- **Laguna-S-2.1 ecosystem variants** — Multiple entries from **poolside** (Laguna-S-2.1, Laguna-S-2.1-NVFP4, Laguna-S-2.1-GGUF) and **unsloth/Laguna-S-2.1-GGUF** — collectively accumulating downloads and quantization experiments around poolside's enterprise code-generation LLM, indicating strong developer interest in deploying it locally.

- **[conradlocke/krea2-identity-edit](https://huggingface.co/conradlocke/krea2-identity-edit)** — Author: conradlocke | Likes: 497 | Downloads: 0  
  *A ComfyUI-compatible LoRA for identity-preserving image editing based on Krea-2-Raw, gaining likes rapidly despite zero downloads (likely a pipeline-specific artifact).*

---

## Ecosystem Signal

Several structural trends define this week's Hugging Face ecosystem:

1. **Extreme quantization goes mainstream.** The prism-ml Bonsai family (1-bit and ternary 2-bit) accounts for over 1.8M combined downloads, proving the community will sacrifice quality for the ability to run 27B-class models on consumer hardware. This signals a permanent shift toward ultra-compact deployment.

2. **Qwen3.5/3.6 as the fine-tuning base of choice.** At least 7 out of 30 trending models derive from Qwen 3.5 or 3.6, with uncensored, reasoning, and Claude-mythology variants all carving distinct niches. The model family has effectively become the community standard for open-weight fine-tuning, displacing earlier favorites like Llama.

3. **Bimodal distribution of interest: massive open-weights vs. tiny specialized models.** At one extreme, Google's Gemma-4-31B-it and upstage's Solar-Open2-250B represent the frontier of open-weight scaling. At the other, openbmb's MiniCPM robotics models and GnLOLot's 1B thinking model show deep investment in small, task-specific, or embodied agents.

4. **Quantization pipelines are accelerating.** The race between GGUF, MLX, and NVFP4 formats — all applied to the same base models (Laguna-S-2.1, Inkling, Bonsai) — indicates a maturing ecosystem where the bottleneck is no longer model quality but format compatibility and inference speed.

5. **OCR and audio domain models achieve breakout volume.** Baidu's Unlimited-OCR (2.2M downloads) and NVIDIA's Nemotron ASR (590K downloads) outpace many general-purpose LLMs, suggesting that specialized "utility" models are driving real-world production usage on Hub.

---

## Worth Exploring

- **[prism-ml/Bonsai-27B-gguf](https://huggingface.co/prism-ml/Bonsai-27B-gguf)** — With 1.4M downloads and 1-bit quantization, this is the most downloaded sub-2-bit model. It is worth studying for anyone deploying LLMs on consumer hardware, as it represents the current quality boundary of extreme compression.

- **[openbmb/MiniCPM-RobotManip](https://huggingface.co/openbmb/MiniCPM-RobotManip)** — One of the very few vision-language-action (VLA) models on Hugging Face. As the robotics-AI field transitions from research to deployment, this model signals how VLA will be distributed and fine-tuned. Low downloads now could mean early mover advantage later.

- **[OpenMOSS-Team/MOSS-Transcribe-Diarize](https://

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*