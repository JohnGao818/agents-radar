# Hugging Face 热门模型日报 2026-06-15

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-06-15 03:51 UTC

---

# Hugging Face 热门模型日报 | 2026-06-15

## 📌 今日速览

本周 Hugging Face 热门榜由 **DeepSeek-V4-Pro**（周点赞 4,836，下载超 300 万）夺得榜首，成为社区最受关注的开源语言模型。Google **Gemma-4 系列**强势霸榜，多款变体（指令版、GGUF 量化、微调版）合计下载量超 200 万，反映全模态（any-to-any）趋势已从概念走向落地。多模态与音频生成持续升温，**Ideogram-4**（文生图）和 **Higgs Audio v3 TTS** 表现亮眼，而社区微调与量化活动异常活跃，**GGUF** 格式覆盖近半数热门模型。此外，**Qwen3.6** 衍生模型（无审查版、代码版）凭借高下载量成为社区生态的“中坚力量”。

## 🔥 热门模型分类整理

### 🧠 语言模型（LLM、对话、指令微调）

- **[DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)**  
  作者：deepseek-ai | 点赞 4,836 | 下载 3,075,369  
  DeepSeek 第四代 Pro 版本，MoE 架构，本周最热开源 LLM，对话与推理能力达到新高度。

- **[Nex-N2-Pro](https://huggingface.co/nex-agi/Nex-N2-Pro)**  
  作者：nex-agi | 点赞 260 | 下载 3,396  
  基于 Qwen3.5 MoE，专注通用文本生成的高级模型。

- **[Nex-N2-mini](https://huggingface.co/nex-agi/Nex-N2-mini)**  
  作者：nex-agi | 点赞 211 | 下载 7,010  
  Nex-N2 轻量版，适合资源受限场景。

- **[Quasar-Preview](https://huggingface.co/silx-ai/Quasar-Preview)**  
  作者：silx-ai | 点赞 74 | 下载 307  
  Silx AI 预览版，专为长上下文设计，尚处于早期测试。

---

### 🎨 多模态与生成（图像、视频、音频、any-to-any）

- **[google/gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it)**  
  作者：google | 点赞 1,010 | 下载 1,084,405  
  Gemma-4 指令版，支持任意模态输入输出，下载量破百万，多模态通用助手标杆。

- **[google/gemma-4-12B](https://huggingface.co/google/gemma-4-12B)**  
  作者：google | 点赞 545 | 下载 213,502  
  Gemma-4 基础版（未指令微调），开源权重供研究者二次开发。

- **[google/diffusiongemma-26B-A4B-it](https://huggingface.co/google/diffusiongemma-26B-A4B-it)**  
  作者：google | 点赞 802 | 下载 198,912  
  融合扩散与语言建模的 26B MoE 模型，支持图像理解与对话。

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)**  
  作者：HauhauCS | 点赞 1,809 | 下载 2,516,709  
  社区无审查多模态模型，基于 Qwen3.6 MoE，35B 参数配合“激进”风格，下载量极高。

- **[MiniMaxAI/MiniMax-M3](https://huggingface.co/MiniMaxAI/MiniMax-M3)**  
  作者：MiniMaxAI | 点赞 508 | 下载 6,643  
  MiniMax 第三代多模态模型，支持图文理解与生成。

- **[prefeitura-rio/Rio-3.5-Open-397B](https://huggingface.co/prefeitura-rio/Rio-3.5-Open-397B)**  
  作者：prefeitura-rio | 点赞 277 | 下载 112,371  
  里约市政府开源的 397B 超大 MoE 多模态模型，基于 Qwen3.5，规模惊人。

- **[Jackrong/Qwopus3.6-27B-v2-MTP-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-27B-v2-MTP-GGUF)**  
  作者：Jackrong | 点赞 303 | 下载 175,472  
  Qwopus 3.6 v2 多模态版，GGUF 量化，支持文本图像交互。

- **[ideogram-ai/ideogram-4-fp8](https://huggingface.co/ideogram-ai/ideogram-4-fp8)**  
  作者：ideogram-ai | 点赞 535 | 下载 8,263  
  Ideogram 4 代 FP8 量化版，高质量文生图模型，兼顾速度与效果。

- **[ideogram-ai/ideogram-4-nf4](https://huggingface.co/ideogram-ai/ideogram-4-nf4)**  
  作者：ideogram-ai | 点赞 337 | 下载 3,763  
  NF4 量化版，进一步降低显存需求。

- **[bosonai/higgs-audio-v3-tts-4b](https://huggingface.co/bosonai/higgs-audio-v3-tts-4b)**  
  作者：bosonai | 点赞 428 | 下载 35,122  
  4B 参数的高质量 TTS 模型，支持语音合成。

- **[zai-org/SCAIL-2](https://huggingface.co/zai-org/SCAIL-2)**  
  作者：zai-org | 点赞 176 | 下载 0  
  基于扩散的姿态驱动角色动画视频生成工具，图像→视频的创新应用。

---

### 🔧 专用模型（代码、视觉定位、语音识别等）

- **[moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)**  
  作者：moonshotai | 点赞 644 | 下载 15,145  
  月之暗面推出的代码模型，支持图像与代码联合理解。

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)**  
  作者：nvidia | 点赞 2,007 | 下载 75,201  
  NVIDIA 的通用视觉定位模型，3B 参数，可精准框选图像中任意物体。

- **[CohereLabs/North-Mini-Code-1.0](https://huggingface.co/CohereLabs/North-Mini-Code-1.0)**  
  作者：CohereLabs | 点赞 370 | 下载 9,932  
  Cohere North 系列轻量代码模型，MoE 架构。

- **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)**  
  作者：nvidia | 点赞 412 | 下载 4,505  
  流式自动语音识别模型，0.6B 参数，低延迟适合实时场景。

- **[Jackrong/Qwopus3.6-27B-Coder-MTP-GGUF](https://huggingface.co/Jackrong/Qwopus3.6-27B-Coder-MTP-GGUF)**  
  作者：Jackrong | 点赞 185 | 下载 33,720  
  面向代码生成的 Qwopus 3.6 变体，支持多模态输入，GGUF 量化。



---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*