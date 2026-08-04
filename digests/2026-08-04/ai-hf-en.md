# Hugging Face Trending Models Digest 2026-08-04

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-08-04 02:06 UTC

---

# Hugging Face Trending Models Digest — 2026-08-04

## 1. Today's Highlights

This week’s HF trending board is dominated by **Kimi-K3**, a compressed multimodal model from Moonshot AI that racked up nearly 10k likes in seven days — the strongest community signal on the list. DeepSeek also made a major push with two **DeepSeek-V4-Flash** entries plus an official GGUF conversion, cementing its position as a leading open-weight LLM family. The rise of **Qwen3.6 MoE fine-tunes** is impossible to ignore: several uncensored/community GGUF variants (DavidAU, HauhauCS, LuffyTheFox) earned massive download counts. On the media side, **MiniMax-H3** is a fresh image-text-to-video release with official and ComfyUI-packaged versions, while **Baidu Unlimited-OCR** continues to dominate as one of the most downloaded specialist models. Quantization and edge-friendly formats (GGUF, NVFP4, INT8) remain the strongest cross-cutting trend.

## 2. Trending Models

### 🧠 Language Models

- [**deepseek-ai/DeepSeek-V4-Flash-0731**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) — deepseek-ai | ❤️ 2,068 | ⬇️ 236,076  
  A newly dated DeepSeek-V4 Flash checkpoint, trending as the latest official fast-generation LLM release from DeepSeek.

- [**deepseek-ai/DeepSeek-V4-Flash**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash) — deepseek-ai | ❤️ 1,991 | ⬇️ 2,746,291  
  The base DeepSeek-V4 Flash model, with huge download numbers thanks to strong open-weight reputation and conversational performance.

- [**zai-org/GLM-5.2**](https://huggingface.co/zai-org/GLM-5.2) — zai-org | ❤️ 4,798 | ⬇️ 2,180,509  
  Zhipu’s GLM-5.2 is one of the most-liked models of the week, powered by a MoE architecture and attracting massive adoption.

- [**XYZAILab/XYZ-Aquila-mini**](https://huggingface.co/XYZAILab/XYZ-Aquila-mini) — XYZAILab | ❤️ 391 | ⬇️ 1,063  
  A compact Qwen3.5/3.6-based MoE LLM, trending for its mini-scale efficiency and multimodal tag overlap.

- [**EschaLabs/Qwen3.6-35B-A3B-Escha-W2**](https://huggingface.co/EschaLabs/Qwen3.6-35B-A3B-Escha-W2) — EschaLabs | ❤️ 156 | ⬇️ 2,682  
  A 35B MoE model with only 3B active parameters, reflecting the industry push toward ultra-efficient sparse LLMs.

- [**Nanbeige/Nanbeige4.2-3B**](https://huggingface.co/Nanbeige/Nanbeige4.2-3B) — Nanbeige | ❤️ 652 | ⬇️ 34,705  
  A compact 3B LLM gaining traction for lightweight deployment and a solid likes-to-download ratio.

- [**poolside/Laguna-S-2.1**](https://huggingface.co/poolside/Laguna-S-2.1) — poolside | ❤️ 910 | ⬇️ 81,584  
  Poolside’s latest code-adjacent reasoning model, trending among developers evaluating frontier open models.

- [**XYZAILab/XYZ-Aquila-pro**](https://huggingface.co/XYZAILab/XYZ-Aquila-pro) — XYZAILab | ❤️ 351 | ⬇️ 1,214  
  A larger Aquila variant with an agentic-search tag, pointing to growing interest in search-augmented LLMs.

- [**amd/Instella-MoE-16B-A3B-Think**](https://huggingface.co/amd/Instella-MoE-16B-A3B-Think) — amd | ❤️ 150 | ⬇️ 2,078  
  AMD’s MoE reasoning model, inspired by DeepSeek-V3-style active-parameter sparsity and aimed at efficient thinking.

### 🎨 Multimodal & Generation

- [**moonshotai/Kimi-K3**](https://huggingface.co/moonshotai/Kimi-K3) — moonshotai | ❤️ 9,854 | ⬇️ 967,622  
  The week’s top-liked model — a compressed multimodal vision-language model from Moonshot AI with feature-extraction support.

- [**MiniMaxAI/MiniMax-H3**](https://huggingface.co/MiniMaxAI/MiniMax-H3) — MiniMaxAI | ❤️ 1,476 | ⬇️ 0  
  A brand-new image-text-to-video model from MiniMax using diffusers, generating strong buzz despite zero downloads yet.

- [**Comfy-Org/MiniMax-H3**](https://huggingface.co/Comfy-Org/MiniMax-H3) — Comfy-Org | ❤️ 449 | ⬇️ 2  
  Official ComfyUI packaging of MiniMax-H3, positioning the video model for creative workflow adoption.

- [**thinkingmachines/Inkling-Small**](https://huggingface.co/thinkingmachines/Inkling-Small) — thinkingmachines | ❤️ 264 | ⬇️ 8,504  
  A compact image-text-to-text conversational model, trending as a lightweight multimodal assistant.

- [**microsoft/Mage-VL**](https://huggingface.co/microsoft/Mage-VL) — microsoft | ❤️ 233 | ⬇️ 431,487  
  Microsoft’s vision-language model, with strong download momentum despite moderate likes.

- [**lodestones/Kroma**](https://huggingface.co/lodestones/Kroma) — lodestones | ❤️ 159 | ⬇️ 0  
  A text-to-image LoRA for Krea2/ComfyUI, showing continued community interest in stylized image generation.

- [**empero-ai/Qwythos-27B-v1**](https://huggingface.co/empero-ai/Qwythos-27B-v1) — empero-ai | ❤️ 119 | ⬇️ 1,736  
  A Qwen3.5-based image-text-to-text model, part of the wave of multimodal fine-tunes on Qwen architectures.

### 🔧 Specialized Models

- [**baidu/Unlimited-OCR**](https://huggingface.co/baidu/Unlimited-OCR) — baidu | ❤️ 3,847 | ⬇️ 2,601,062  
  The most-downloaded model this week — a universal OCR system from Baidu with strong feature-extraction support.

- [**Kwaipilot/KAT-Coder-V2.5-Dev**](https://huggingface.co/Kwaipilot/KAT-Coder-V2.5-Dev) — Kwaipilot | ❤️ 446 | ⬇️ 14,339  
  A dev-stage MoE coder built on Qwen3.5-MoE, trending among practical code-generation users.

- [**microsoft/Fara1.5-27B**](https://huggingface.co/microsoft/Fara1.5-27B) — microsoft | ❤️ 268 | ⬇️ 2,988  
  Microsoft’s computer-use multimodal model, specialized for GUI grounding and agentic screen interactions.

### 📦 Fine-tunes & Quantizations

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*