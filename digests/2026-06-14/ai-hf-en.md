# Hugging Face Trending Models Digest 2026-06-14

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-06-14 03:37 UTC

---

# Hugging Face Trending Models Digest – June 14, 2026

## Today’s Highlights

The week is dominated by **DeepSeek-V4-Pro**, which leads both in weekly likes (4,813) and downloads (3.25M), signaling strong community adoption of the latest open‑weight conversational LLM. **Google’s Gemma‑4 family** continues to see explosive ecosystem activity, with multiple fine‑tunes (abliterated, uncensored) and GGUF quantizations from unsloth and community members. **Multimodal and generative models** are the hottest category – from ByteDance’s video‑generating **Bernini‑R** to Ideogram‑4 variants and nvidia’s **LocateAnything** for spatial understanding. The rise of **MoE architectures** is unmistakable: at least nine models in the top 30 use mixture‑of‑experts, including DiffusionGemma, Kimi‑K2.7, MiniMax‑M3, and the massive Rio‑3.5‑Open‑397B. Quantization remains the default community workflow, with unsloth alone contributing four GGUF variants of Gemma‑4.

---

## Trending Models

### 🧠 Language Models (LLMs, chat, instruction‑tuned)

- **[nex-agi/Nex-N2-Pro](https://huggingface.co/nex-agi/Nex-N2-Pro)**  
  Author: nex‑agi | Likes: 238 | Downloads: 3,092  
  A 35B‑A3B MoE text‑generation model from the Nex series, trending for its balanced efficiency and generation quality.

- **[nex-agi/Nex-N2-mini](https://huggingface.co/nex-agi/Nex-N2-mini)**  
  Author: nex‑agi | Likes: 195 | Downloads: 3,760  
  The smaller sibling of Nex‑N2‑Pro, offering a lightweight MoE for resource‑constrained deployments.

- **[XiaomiMiMo/MiMo-V2.5-Pro-FP4-DFlash](https://huggingface.co/XiaomiMiMo/MiMo-V2.5-Pro-FP4-DFlash)**  
  Author: XiaomiMiMo | Likes: 106 | Downloads: 3,590  
  A 4‑bit FP4 quantized text‑generation model with agent‑focused capabilities, gaining attention for on‑device LLM deployment.

- **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)**  
  Author: deepseek‑ai | Likes: 4,813 | Downloads: 3,250,404  
  The week’s absolute top model – a high‑performance conversational LLM that combines strong reasoning with massive community download volume.

### 🎨 Multimodal & Generation (image, video, audio, text‑to‑X)

- **[google/diffusiongemma-26B-A4B-it](https://huggingface.co/google/diffusiongemma-26B-A4B-it)**  
  Author: google | Likes: 719 | Downloads: 92,080  
  A 26B‑A4B MoE model that merges diffusion with language understanding for image‑text tasks; the foundation for numerous community quants.

- **[MiniMaxAI/MiniMax-M3](https://huggingface.co/MiniMaxAI/MiniMax-M3)**  
  Author: MiniMaxAI | Likes: 422 | Downloads: 1,031  
  A multimodal MoE designed for image‑text‑to‑text reasoning, building on MiniMax’s previous M2 series.

- **[google/gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it)**  
  Author: google | Likes: 995 | Downloads: 1,005,883  
  Flagship instruction‑tuned any‑to‑any model from Google – supports text, image, and audio I/O; downloaded over one million times this week.

- **[google/gemma-4-12B](https://huggingface.co/google/gemma-4-12B)**  
  Author: google | Likes: 534 | Downloads: 207,338  
  The base pretrained version of Gemma‑4‑12B, giving researchers full control over fine‑tuning and adaptation.

- **[bosonai/higgs-audio-v3-tts-4b](https://huggingface.co/bosonai/higgs-audio-v3-tts-4b)**  
  Author: bosonai | Likes: 414 | Downloads: 32,162  
  A 4B‑parameter text‑to‑speech model with Qwen3‑based architecture, producing natural multi‑speaker audio.

- **[ideogram-ai/ideogram-4-fp8](https://huggingface.co/ideogram-ai/ideogram-4-fp8)**  
  Author: ideogram‑ai | Likes: 517 | Downloads: 6,535  
  FP8 quantized version of Ideogram‑4, offering high‑quality text‑to‑image generation with reduced memory footprint.

- **[ideogram-ai/ideogram-4-nf4](https://huggingface.co/ideogram-ai/ideogram-4-nf4)**  
  Author: ideogram‑ai | Likes: 334 | Downloads: 3,276  
  NF4 quantization variant of Ideogram‑4, optimized for low‑precision inference without noticeable quality loss.

- **[zai-org/SCAIL-2](https://huggingface.co/zai-org/SCAIL-2)**  
  Author: zai‑org | Likes: 154 | Downloads: 0  
  A pose‑driven image‑to‑video diffusion model for character animation, representing the cutting edge of controllable video generation.

- **[ByteDance/Bernini-R](https://huggingface.co/ByteDance/Bernini-R)**  
  Author: ByteDance | Likes: 235 | Downloads: 426  
  Image‑text‑to‑video model from ByteDance (arxiv:2605.22344), enabling temporally coherent video generation from a single image and prompt.

- **[google/magenta-realtime-2](https://huggingface.co/google/magenta-realtime-2)**  
  Author: google | Likes: 189 | Downloads: 7,331  
  Real‑time text‑to‑audio model for music and sound generation, published with accompanying arxiv papers and TFLite support.

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)**  
  Author: HauhauCS | Likes: 1,763 | Downloads: 2,411,202  
  A community fine‑tune of Qwen3.6‑MoE (35B‑A3B) with uncensored outputs and aggressive style; widely downloaded for creative role‑play tasks.

- **[prefeitura-rio/Rio-3.5-Open-397B](https://huggingface.co/prefeitura-rio/Rio-3.5-Open-397B)**  
  Author: prefeitura‑rio | Likes: 143 | Downloads: 5,943  
  A massive 397B‑parameter MoE multimodal model (Qwen3.5‑based) released by a public institution, showcasing government‑scale open‑weight AI.

### 🔧 Specialized Models (code, math, medical, embeddings, ASR)

- **[moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)**  
  Author: moonshotai | Likes: 524 | Downloads: 1,689  
  A compressed‑tensor code model built

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*