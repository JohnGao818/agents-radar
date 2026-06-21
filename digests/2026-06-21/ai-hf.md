# Hugging Face 热门模型日报 2026-06-21

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-06-21 03:43 UTC

---

# Hugging Face 热门模型日报（2026-06-21）

## 📌 今日速览

本周 Hugging Face 最受瞩目的模型是 **DeepSeek-V4-Pro**（周赞 4,987），凭借强大的综合文本生成能力遥遥领先。多模态模型热度持续攀升：Google 的 **DiffusionGemma-26B-A4B-it** 以扩散架构冲击图像‑文本理解，MiniMax 的 **M3** 系列也稳定积累关注。代码与推理赛道同样竞争激烈，**Gemma-4-12B-Coder** 系列及 **Kimi-K2.7-Code** 均录得可观下载。社区量化活动十分活跃，大量 **Qwen3.6、GLM-5.2、Gemma-4** 的 GGUF 版本涌入，反映出用户对本地部署和高效推理的强烈需求。

---

## 📋 热门模型分类速览

### 🧠 语言模型（LLM、对话、指令微调）

| 模型 | 作者 | 点赞 | 下载 | 一句话说明 |
|------|------|------|------|------------|
| [DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro) | deepseek-ai | 4,987 | 2,797,050 | 本周最强通用语言模型，基于 DeepSeek-V4 架构，在对话和推理任务上表现卓越。 |
| [microsoft/FastContext-1.0-4B-SFT](https://huggingface.co/microsoft/FastContext-1.0-4B-SFT) | microsoft | 245 | 1,998 | 微软出品的高效上下文模型，4B参数专为快速长上下文场景优化。 |
| [zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2) | zai-org | 1,702 | 19,683 | 智谱新一代 MoE 对话模型，5.2 版本在效率和对话流畅度上有显著提升。 |

### 🎨 多模态与生成（图像、视频、音频、文本到X）

| 模型 | 作者 | 点赞 | 下载 | 一句话说明 |
|------|------|------|------|------------|
| [MiniMaxAI/MiniMax-M3](https://huggingface.co/MiniMaxAI/MiniMax-M3) | MiniMaxAI | 1,163 | 85,771 | MiniMax 第三代多模态大模型，支持图文理解与生成。 |
| [google/diffusiongemma-26B-A4B-it](https://huggingface.co/google/diffusiongemma-26B-A4B-it) | google | 1,023 | 673,464 | Google 推出的扩散式多模态模型，26B参数激活 4B，将扩散过程引入图文对话。 |
| [google/gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it) | google | 1,107 | 1,696,240 | Gemma-4 统一多模态版本（any-to-any），支持跨模态输入输出。 |
| [nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B) | nvidia | 2,217 | 235,606 | NVIDIA 开发的视觉定位模型，可基于文本或图像准确定位目标。 |
| [HauhauCS/Qwen3.6-35B-A3B-Uncensored...](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive) | HauhauCS | 2,043 | 3,812,636 | Qwen3.6 的社区无审查版，结合 MoE 与视觉能力，下载量极高。 |
| [prefeitura-rio/Rio-3.5-Open-397B](https://huggingface.co/prefeitura-rio/Rio-3.5-Open-397B) | prefeitura-rio | 327 | 190,694 | 基于 Qwen3.5 MoE 的开放多模态模型，397B参数支持图文对话。 |
| [lordx64/Qwable-v1](https://huggingface.co/lordx64/Qwable-v1) | lordx64 | 138 | 2,769 | Qwen 家族的视觉语言变体，融合 MoE 与多模态能力。 |
| [nex-agi/Nex-N2-Pro](https://huggingface.co/nex-agi/Nex-N2-Pro) | nex-agi | 340 | 7,724 | 基于 Qwen3.5 MoE 的多模态 Agent 模型，侧重图文理解。 |
| [datalab-to/lift](https://huggingface.co/datalab-to/lift) | datalab-to | 89 | 0 | 针对 PDF 文档的图文理解模型，支持跨页解析。 |
| [ostris/ideogram_4_turbotime_lora](https://huggingface.co/ostris/ideogram_4_turbotime_lora) | ostris | 83 | 1,679 | Ideogram 4 的 LoRA 微调，加速文本到图像生成。 |
| [zai-org/SCAIL-2](https://huggingface.co/zai-org/SCAIL-2) | zai-org | 241 | 0 | 基于扩散模型的角色动画视频生成模型，支持姿态驱动。 |
| [owensong/Inflect-Nano-v1](https://huggingface.co/owensong/Inflect-Nano-v1) | owensong | 143 | 0 | 超轻量级 TTS 模型，适合端侧语音合成。 |
| [bosonai/higgs-audio-v3-tts-4b](https://huggingface.co/bosonai/higgs-audio-v3-tts-4b) | bosonai | 499 | 72,225 | 基于 Qwen3 的 4B 参数语音合成模型，支持多模态输入。 |

### 🔧 专用模型（代码、数学、ASR、嵌入）

| 模型 | 作者 | 点赞 | 下载 | 一句话说明 |
|------|------|------|------|------------|
| [yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF) | yuxinlu1 | 1,993 | 312,332 | Gemma-4 专用代码推理模型，结合 Fable5 与 Composer 2.5 技术。 |
| [moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code) | moonshotai | 932 | 317,963 | 月之暗面推出的代码视觉模型，支持图文混合编程任务。 |
| [WeiboAI/VibeThinker-3B](https://huggingface.co/WeiboAI/VibeThinker-3B) | WeiboAI | 515 | 16,270 | 基于 Qwen2 的数学推理模型，专注数值与逻辑问题。 |
| [nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nvidia/nemotron-3.5-asr-streaming-0.6b) | nvidia | 588 | 21,426 | 流式自动语音识别模型，支持缓存感知 ASR，适合实时场景。 |
| [CohereLabs/North-Mini-Code-1.0](https://huggingface.co/CohereLabs/North-Mini-Code-1.0) | CohereLabs | 468 | 18,783 | Cohere 的轻量代码模型，基于 MoE 架构，适配代码生成与补全。 |
| [LiquidAI/LFM2.5-Embedding-350M](https://huggingface.co/LiquidAI/LFM2.5-Embedding-350M) | LiquidAI | 81 | 6,128 | 350M 参数的高效文本嵌入模型，适合检索与语义相似度任务。 |

### 📦 微调与量化（社区微调、GGUF、AWQ）

| 模型 | 作者 | 点赞 | 下载 | 一句话说明 |
|------|------|------|------|------------|
| [yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF) | yuxinlu1 | 190 | 6,307 | Gemma-4 Agent 版本的 GGUF 量化，专为终端交互优化。 |
| [unsloth/GLM-5.2-GGUF](https://huggingface.co/unsloth/GLM-5.2-GGUF) | unsloth | 207 | 22,586 | Unsloth 推出的 GLM-5.2 量化版本，大幅降低推理门槛。 |
| [zai-org/GLM-5.2-FP8](https://huggingface.co/zai-org/GLM-5.2-FP8

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*