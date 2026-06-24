# Hugging Face 热门模型日报 2026-06-24

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-06-24 02:51 UTC

---

# Hugging Face 热门模型日报（2026-06-24）

## 📌 今日速览

- **DeepSeek-V4-Pro** 以 5,031 赞高居榜首，成为本周最受瞩目的开源文本生成模型，下载量突破 224 万。  
- **多模态模型** 竞争激烈：NVIDIA 的 LocateAnything‑3B、Google 的 diffusiongemma‑26B、以及 MiniMax‑M3 均跻身前列，支持图文理解/生成。  
- **GGUF 量化生态持续活跃**，Gemma‑4、GLM‑5.2、Qwen3.6 等系列均有多个社区量化版，下载量动辄数十万。  
- **百度 Unlimited‑OCR** 与 **NVIDIA Nemotron ASR** 等专用模型上线即获关注，大模型从通用向垂直场景扩散。

---

## 🔥 热门模型

### 🧠 语言模型（LLM、对话、指令微调）

- **[deepseek‑ai/DeepSeek‑V4‑Pro](https://huggingface.co/deepseek‑ai/DeepSeek‑V4‑Pro)**  
  作者：deepseek‑ai | ⭐ 5,031 | ⬇️ 2,245,489  
  最新一代 DeepSeek 旗舰模型，在推理、编码与对话上均有提升，凭借开源权重引发社区追捧。

- **[zai‑org/GLM‑5.2](https://huggingface.co/zai‑org/GLM‑5.2)**  
  作者：zai‑org | ⭐ 2,202 | ⬇️ 40,127  
  采用 MoE‑DSA 架构的 5.2 版 GLM，主打高效推理与对话能力，代表国产模型的又一突破。

- **[google/gemma‑4‑12B‑it](https://huggingface.co/google/gemma‑4‑12B‑it)**  
  作者：google | ⭐ 1,156 | ⬇️ 1,991,703  
  Google “any‑to‑any” 多模基础模型，12B 参数融合文本、图像理解，可统一处理多模态指令。

- **[microsoft/FastContext‑1.0‑4B‑SFT](https://huggingface.co/microsoft/FastContext‑1.0‑4B‑SFT)**  
  作者：microsoft | ⭐ 323 | ⬇️ 4,391  
  基于 Qwen3 的 4B 级指令微调模型，引入 “Explorer SubAgent” 机制提升长上下文处理效率。

- **[poolside/Laguna‑M.1](https://huggingface.co/poolside/Laguna‑M.1)**  
  作者：poolside | ⭐ 93 | ⬇️ 2,787  
  面向软件工程任务的 1B 级语言模型，优化 vLLM / sglang 部署，轻量级 AGI 尝试。

---

### 🎨 多模态与生成（图像、音频、文生图、OCR、ASR）

- **[nvidia/LocateAnything‑3B](https://huggingface.co/nvidia/LocateAnything‑3B)**  
  作者：nvidia | ⭐ 2,319 | ⬇️ 274,025  
  NVIDIA 发布的视觉定位模型，支持任意物体在图像中的检测与定位，3B 参数即达高效。

- **[HauhauCS/Qwen3.6‑35B‑A3B‑Uncensored‑HauhauCS‑Aggressive](https://huggingface.co/HauhauCS/Qwen3.6‑35B‑A3B‑Uncensored‑HauhauCS‑Aggressive)**  
  作者：HauhauCS | ⭐ 2,161 | ⬇️ 3,955,016  
  Qwen3.6 的 35B 参数 MoE 量化版，移除审查滤镜，具备视觉能力，“Aggressive” 风格，下载量惊人。

- **[MiniMaxAI/MiniMax‑M3](https://huggingface.co/MiniMaxAI/MiniMax‑M3)**  
  作者：MiniMaxAI | ⭐ 1,221 | ⬇️ 131,057  
  MiniMax 第三代多模态大模型，图文理解生成一体，在创意辅助与智能助手场景应用广泛。

- **[google/diffusiongemma‑26B‑A4B‑it](https://huggingface.co/google/diffusiongemma‑26B‑A4B‑it)**  
  作者：google | ⭐ 1,056 | ⬇️ 948,996  
  融合扩散模型与语言模型的新架构，26B 参数仅 4B 激活，擅长大规模图像生成与理解。

- **[moonshotai/Kimi‑K2.7‑Code](https://huggingface.co/moonshotai/Kimi‑K2.7‑Code)**  
  作者：moonshotai | ⭐ 976 | ⬇️ 447,920  
  Kimi 系列代码版，支持图文混合输入，在代码生成、截图理解等场景表现出色。

- **[baidu/Unlimited‑OCR](https://huggingface.co/baidu/Unlimited‑OCR)**  
  作者：baidu | ⭐ 494 | ⬇️ 8,396  
  百度开源的无限制 OCR 模型，可处理复杂版面、手写及多语言文字识别，提供端到端解决方案。

- **[nvidia/nemotron‑3.5‑asr‑streaming‑0.6b](https://huggingface.co/nvidia/nemotron‑3.5‑asr‑streaming‑0.6b)**  
  作者：nvidia | ⭐ 658 | ⬇️ 41,050  
  NVIDIA 流式语音识别模型，0.6B 参数支持低延迟实时转录，适合对话系统与会议场景。

- **[ostris/ideogram_4_turbotime_lora](https://huggingface.co/ostris/ideogram_4_turbotime_lora)**  
  作者：ostris | ⭐ 111 | ⬇️ 3,672  
  基于 Ideogram‑4 的 LoRA 插件，加速文生图推理速度，创意社区热门。

---

### 🔧 专用模型（代码、数学、嵌入、检索）

- **[WeiboAI/VibeThinker‑3B](https://huggingface.co/WeiboAI/VibeThinker‑3B)**  
  作者：WeiboAI | ⭐ 667 | ⬇️ 41,170  
  专为数学推理优化的 3B 模型，基于 Qwen2，在数学基准上表现突出，轻量级科研助手。

- **[LiquidAI/LFM2.5‑Embed

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*