# Hugging Face Trending Models Digest 2026-07-04

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-07-04 02:32 UTC

---

# Hugging Face Trending Models Digest – July 4, 2026

(Data: 30 models sorted by weekly likes; all links preserved.)

---

## 1. Today’s Highlights

The open‑weight ecosystem continues to accelerate, with **GLM‑5.2** (zai‑org) leading in likes (3,345) and **LocateAnything‑3B** (NVIDIA) in multimodal grounding (2,589 likes, 1.1M downloads). Community quantization is the dominant activity—half of the top‑10 most downloaded models are GGUF variants, and **unsloth/Qwen3.6‑27B‑MTP‑GGUF** alone reached 1.77M downloads. The **Ornith‑1.0** family from deepreinforce‑ai spans sizes from 9B to 397B, signaling a push toward massive MoE architectures, while **DeepSeek V4** (both Pro and Flash DSpark) marks continued progress in efficient reasoning models. A notable outlier is **BugTraceAI‑CORE‑Ultra‑27B**, a security‑focused model, hinting at vertical‑specific fine‑tuning gaining traction.

---

## 2. Trending Models by Category

### 🧠 Language Models (LLMs, chat, instruction‑tuned)

- **GLM‑5.2** ([link](https://huggingface.co/zai-org/GLM-5.2)) – zai‑org, 3,345 ♥, 191k ↓  
  A novel MoE transformer with DSA routing, trending for its strong conversational performance and open‑weight release.
- **DeepSeek‑V4‑Pro‑DSpark** ([link](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-DSpark)) – deepseek‑ai, 345 ♥, 9k ↓  
  Fourth‑generation reasoning LLM with sparse activation; draws attention for its arxiv paper and benchmark results.
- **DeepSeek‑V4‑Flash‑DSpark** ([link](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-DSpark)) – deepseek‑ai, 144 ♥, 33k ↓  
  A lighter, faster variant of DeepSeek‑V4, optimized for low‑latency inference.
- **Ornith‑1.0‑9B** ([link](https://huggingface.co/deepreinforce-ai/Ornith-1.0-9B)) – deepreinforce‑ai, 366 ♥, 64k ↓  
  Base 9B MoE model (Qwen3.5‑based) with image‑to‑text support; part of a family spanning 9B–397B.
- **Ornith‑1.0‑35B** ([link](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B)) – deepreinforce‑ai, 323 ♥, 211k ↓  
  35B MoE flagship of the Ornith series, downloaded heavily for its balance of scale and efficiency.
- **Ornith‑1.0‑397B** ([link](https://huggingface.co/deepreinforce-ai/Ornith-1.0-397B)) – deepreinforce‑ai, 201 ♥, 8k ↓  
  The largest open‑weight Ornith model (397B, MoE), attracting early adopters of extreme‑scale LLMs.
- **Qwen‑AgentWorld‑35B‑A3B** ([link](https://huggingface.co/Qwen/Qwen-AgentWorld-35B-A3B)) – Qwen, 526 ♥, 45k ↓  
  Agent‑oriented MoE model with 35B total / 3B active parameters, trending for tool‑use and task‑planning capabilities.
- **InternScience/Agents‑A1** ([link](https://huggingface.co/InternScience/Agents-A1)) – InternScience, 211 ♥, 3.5k ↓  
  A MoE agent model built on Qwen3.5, focused on autonomous task execution.
- **LiquidAI/LFM2.5‑230M** ([link](https://huggingface.co/LiquidAI/LFM2.5-230M)) – LiquidAI, 198 ♥, 30k ↓  
  A tiny 230M liquid foundation model, gaining interest for efficient on‑device deployment.

### 🎨 Multimodal & Generation (image, video, text‑to‑X)

- **baidu/Unlimited‑OCR** ([link](https://huggingface.co/baidu/Unlimited-OCR)) – baidu, 1,692 ♥, 885k ↓  
  Universal OCR model capable of handling diverse document images; popular for its accuracy and ease of use.
- **nvidia/LocateAnything‑3B** ([link](https://huggingface.co/nvidia/LocateAnything-3B)) – nvidia, 2,589 ♥, 1.1M ↓  
  A 3B grounding model that localizes objects in images given text prompts—trending for zero‑shot visual recognition.
- **krea/Krea‑2‑Turbo** ([link](https://huggingface.co/krea/Krea-2-Turbo)) – krea, 484 ♥, 84k ↓  
  Fast text‑to‑image model fine‑tuned from Krea‑2‑Raw, optimized for iterative generation workflows.
- **empero‑ai/Qwythos‑9B‑Claude‑Mythos‑5‑1M** ([link](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M)) – empero‑ai, 660 ♥, 131k ↓  
  A Qwen3.5 fine‑tune blending Claude‑style outputs with mythos narrative data; supports image inputs.
- **fal/LTX‑2.3‑3DREAL‑LoRA** ([link](https://huggingface.co/fal/LTX-2.3-3DREAL-LoRA)) – fal, 151 ♥, 0 ↓  
  LoRA adapter for LTX‑2.3 that adds 3D‑realistic video generation from images; early interest despite zero downloads.

### 🔧 Specialized Models (code, security, tabular, grounding, PII)

- **nvidia/LocateAnything‑3B** (also listed above) – fits both multimodal and specialized categories; here as a grounding model.
- **google/tabfm‑1.0.0‑pytorch** ([link](https://huggingface.co/google/tabfm-1.0.0-pytorch)) – google, 152 ♥, 450 ↓  
  Foundation model for tabular data supporting classification and regression with zero‑shot transfer.
- **BugTraceAI/BugTraceAI‑CORE‑Ultra‑27B‑Q6** ([link](https://huggingface.co/BugTraceAI/BugTraceAI-CORE-Ultra-27B-Q6)) – BugTraceAI, 127 ♥, 11k ↓  
  A 27B Q6‑quantized model specialized for cybersecurity and offensive security analysis.
- **nationaldesignstudio/rampart** ([link](https://huggingface.co/nationaldesignstudio/rampart)) – nationaldesignstudio, 116 ♥, 1.1k ↓  
  BERT‑based token classifier for detecting Personally Identifiable Information (PII) in text.

### 📦 Fine‑tunes & Quantizations (GGUF, NVFP4, community versions)

- **empero‑ai/Qwythos‑9B‑Claude‑Mythos‑5‑1M‑GGUF** ([link](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)) – empero‑ai, 1,374 ♥, 1.37M ↓  
  GGUF quantized version of the Qwythos‑9B model, leading downloads for easy local inference.
- **deepreinforce‑ai/Ornith‑1.0‑35B‑GGUF** ([link](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B-GGUF)) – deepreinforce‑ai, 687 ♥, 323k ↓  
  GGUF quant of Ornith‑1.0‑35B, widely used for consumer‑grade hardware.
- **deepreinforce‑ai/Ornith‑1.0‑9B‑GGUF** ([link](https://huggingface.co/deepreinforce-ai/Ornith-1.0-9B-GGUF)) – deepreinforce‑ai, 415 ♥, 288k ↓  
  Smaller GGUF variant (9B), popular for lightweight deployments.
- **yuxinlu1/gemma‑4‑12B‑agentic‑fable5‑composer2.5‑v2‑3.5x‑tau2‑GGUF** ([link](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)) – yuxinlu1, 992 ♥, 329k ↓  
  GGUF of a heavily fine‑tuned Gemma‑4 12B for agentic and coding tasks.
- **yuxinlu1/gemma‑4‑12B‑coder‑fable5‑composer2.5‑v1‑GGUF** ([link](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)) – yuxinlu1, 2,585 ♥, 628k ↓  
  Coding‑focused Gemma‑4 12B GGUF, one of the highest‑liked quantized models this week.
- **nvidia/Qwen3.6‑27B‑NVFP4** ([link](https://huggingface.co/nvidia/Qwen3.6-27B-NVFP4)) – nvidia, 232 ♥, 94k ↓  
  NVIDIA‑optimized Qwen3.6 27B using 4‑bit floating point (NVFP4), showcasing hardware‑specific quantization.
- **nvidia/GLM‑5.2‑NVFP4** ([link](https://huggingface.co/nvidia/GLM-5.2-NVFP4)) – nvidia, 215 ♥, 190k ↓  
  NVFP4 quantized GLM‑5.2, enabling efficient inference on NVIDIA GPUs.
- **HauhauCS/Qwen3.6‑35B‑A3B‑Uncensored‑HauhauCS‑Aggressive** ([link](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*