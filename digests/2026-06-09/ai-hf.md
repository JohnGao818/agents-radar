# Hugging Face 热门模型日报 2026-06-09

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-06-09 02:45 UTC

---

# Hugging Face 热门模型日报 ｜ 2026-06-09

## 今日速览

- **DeepSeek-V4-Pro** 以周增长 4,723 赞登顶，成为当之无愧的头号热门，下载量已超 539 万，展示了开源大模型的强劲需求。  
- **多模态与生成模型**持续爆发：NVIDIA 的 `LocateAnything-3B`（图像定位）和 `Cosmos3` 系列、Ideogram 4 系列、Sulphur-2-base（视频生成）均进入前 30，反映社区对视觉‑语言与视频生成的高度关注。  
- **量化与微调生态**异常活跃：Unsloth 和 Google 官方分别发布 Gemma-4、DeepSeek-V4 的 GGUF 版本，推动大模型在消费级硬件上的部署。  
- **视频生成赛道**出现新力量：SulphurAI 的 `Sulphur-2-base` 基于 Lightricks LTX-2.3 量化，一周内获 1,601 赞、170 万下载，成为视频领域黑马。  
- **专用模型**亮点：NVIDIA 流式 ASR 模型、PaddlePaddle 的 OCR-VL、JetBrains 的代码思考模型等细分场景模型均上榜，展示 AI 落地的多元方向。

---

## 热门模型

### 🧠 语言模型（LLM / 对话 / 指令微调）

| 模型 | 作者 | 点赞 | 下载 | 一句话说明 |
|------|------|------|------|------------|
| [DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro) | deepseek-ai | 4,723 | 5,399,597 | 最新开源旗舰语言模型，性能强劲，社区热度与下载量双双第一。 |
| [DeepSeek-V4-Flash](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash) | deepseek-ai | 1,449 | 3,262,529 | V4 的轻量版，兼顾速度与质量，适合快速推理。 |
| [NVIDIA-Nemotron-3-Ultra-550B-A55B-BF16](https://huggingface.co/nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-BF16) | nvidia | 167 | 55,910 | 超大规模 MoE 模型（550B 总参/55B 激活），NVIDIA 最新的文本生成利器。 |
| [NVIDIA-Nemotron-3-Ultra-550B-A55B-NVFP4](https://huggingface.co/nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-NVFP4) | nvidia | 145 | 66,219 | 同一模型的 NVFP4 量化版，降低推理资源需求。 |
| [JetBrains/Mellum2-12B-A2.5B-Thinking](https://huggingface.co/JetBrains/Mellum2-12B-A2.5B-Thinking) | JetBrains | 260 | 17,448 | JetBrains 推出的代码/推理增强 MoE 模型，12B 参数仅激活 2.5B，适合集成到 IDE。 |
| [LiquidAI/LFM2.5-8B-A1B](https://huggingface.co/LiquidAI/LFM2.5-8B-A1B) | LiquidAI | 551 | 135,131 | 全新的稀疏 MoE 语言模型（8B/1B 激活），在效率与效果间取得出色平衡。 |
| [nex-agi/Nex-N2-Pro](https://huggingface.co/nex-agi/Nex-N2-Pro) | nex-agi | 125 | 716 | 基于 Qwen3.5 MoE 的多模态+文本生成模型，主打推理能力。 |

### 🎨 多模态与生成（图像 / 视频 / 音频 / 文本到 X）

| 模型 | 作者 | 点赞 | 下载 | 一句话说明 |
|------|------|------|------|------------|
| [nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B) | nvidia | 1,628 | 121,594 | 强大的图像定位模型，可指代任意目标，社区追捧。 |
| [google/gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it) | google | 754 | 554,173 | Google 全模态旗舰（any‑to‑any），同时处理文本、图像、音频等。 |
| [unsloth/gemma-4-12b-it-GGUF](https://huggingface.co/unsloth/gemma-4-12b-it-GGUF) | unsloth | 504 | 645,263 | Gemma-4 的社区 GGUF 量化版，下载量极高，方便本地部署。 |
| [google/gemma-4-12B](https://huggingface.co/google/gemma-4-12B) | google | 452 | 117,509 | Gemma-4 基础版（不含指令优化），适合二次开发。 |
| [ideogram-ai/ideogram-4-fp8](https://huggingface.co/ideogram-ai/ideogram-4-fp8) | ideogram-ai | 394 | 5,495 | Ideogram 第四代文生图模型，FP8 精度，图像质量出色。 |
| [ideogram-ai/ideogram-4-nf4](https://huggingface.co/ideogram-ai/ideogram-4-nf4) | ideogram-ai | 262 | 4,963 | 同模型的 NF4 量化版，进一步降低存储与推理开销。 |
| [HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive) | HauhauCS | 1,554 | 3,036,465 | 基于 Qwen3.6 的无审查 MoE 视觉语言模型，社区定制版本，下载破 300 万。 |
| [stepfun-ai/Step-3.7-Flash](https://huggingface.co/stepfun-ai/Step-3.7-Flash) | stepfun-ai | 352 | 45,535 | 阶跃星辰推出的视觉语言模型“Step-3.7”的快速版。 |
| [ByteDance/Bernini-R](https://huggingface.co/ByteDance/Bernini-R) | ByteDance | 186 | 278 | 字节跳动的图像→视频生成模型，主打“渲染”能力，尚在早期开源。 |
| [SulphurAI/Sulphur-2-base](https://huggingface.co/SulphurAI/Sulphur-2-base) | SulphurAI | 1,601 | 1,707,062 | 基于 Lightricks LTX-2.3 量化的视频生成模型，轻量且效果惊艳。 |
| [nvidia/Cosmos3-Nano](https://huggingface.co/nvidia/Cosmos3-Nano) | nvidia | 206 | 34,104 | NVIDIA Cosmos3 系列小型版，面向多模态合一（Cossmos3 Omni）。 |
| [nvidia/Cosmos3-Super](https://huggingface.co/nvidia/Cosmos3-Super) | nvidia | 158 | 27,548 | Cosmos3 大型版，更强的多模态生成能力。 |
| [unsloth/Qwen3.6-27B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF) | unsloth | 696 | 1,186,648 | Qwen3.6 的 MTP（多令牌预测）GGUF 量化版，大受欢迎。 |
| [bosonai/higgs-audio-v3-tts-4b](https://huggingface.co/bosonai/higgs-audio-v3-tts-4b) | bosonai | 251 | 15,005 | 4B 参数 TTS 模型，基于 Qwen3 多模态架构，语音合成质量高。 |
| [google/magenta-realtime-2](https://huggingface.co/google/magenta-realtime-2) | google | 152 | 17,531 | Google 实时音乐/音频生成模型第二版，支持 TFLite 推理。 |
| [MisoLabs/MisoTTS](https://huggingface.co/MisoLabs/MisoTTS) | MisoLabs | 156 | 0 | 新兴 TTS 模型，尚无人下载但获关注，可能即将发布。 |
| [jdopensource/JoyAI-Echo](https://huggingface.co/jdopensource/JoyAI-Echo) | jdopensource | 103 | 4,053 | 京东开源文生视频模型，结合音频与视频生成。 |

### 🔧 专用模型（代码 / 数学 / 医疗 / ASR / OCR / 嵌入）

| 模型 | 作者 | 点赞 | 下载 | 一句话说明 |
|------|------|------|------|------------|
| [nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b) | nvidia | 293 | 3,957 | 流式语音识别模型，针对低延迟场景优化，适合实时应用。 |
| [PaddlePaddle/PaddleOCR-VL-1.6](https://huggingface.co/PaddlePaddle/PaddleOCR-VL-1.6) | PaddlePaddle | 277 | 9,924 | 百度飞桨推出的视觉语言 OCR 模型，支持文字识别与理解。 |
| [sapientinc/HRM-Text-1B](https://huggingface.co/sapientinc/HRM-Text-1B) | sapientinc | 728 | 163,953 | 1B 参数的人力资源领域文本生成模型，垂直场景专用，表现亮眼。 |

### 📦 微调与量化（社区微调 / GGUF / AWQ / QAT）

| 模型 | 作者 | 点赞 | 下载 | 一句话说明 |
|------|------|------|------|------------|
| [unsloth/gemma-4-12B-it-qat-GGUF](https://huggingface.co/unsloth/gemma-4-12b-it-qat-GGUF) | unsloth | 147 | 121,399 | Gemma-4 指令版的 QAT + GGUF 双优化版，适合边缘设备。 |
| [google/gemma-4-12B-it-qat-q4_0-gguf](https://huggingface.co/google/gemma-4-12B-it-qat-q4_0-gguf) | google | 101 | 52,386 | Google 官方发布的 Gemma-4 QAT 量化版（q4_0），权威性高。 |
| [unsloth/gemma-4-26B-A4B-it-qat-GGUF](https://huggingface.co/unsloth/gemma-4-26B-A4B-it-qat-GGUF) | unsloth | 104 | 87,455 | Gemma-4 26B MoE 版本的 GGUF QAT 量化，进一步降低门槛。 |

---

## 生态信号

- **DeepSeek V4 家族势头最旺**：Pro 与 Flash 合计点赞超 6,000，下载近 900 万，显示社区对高性能开源 LLM 的极度渴求。  
- **多模态全域爆发**：NVIDIA 的 LocateAnything、Google 的 Gemma-4、Ideogram 4、Sulphur-2 等覆盖了“定位、生成、音频、视频”几乎所有模态，预示着未来的模型将不再是单一任务，而是“any‑to‑any”的全能型。  
- **量化社区成为关键一环**：Unsloth 几乎为所有热门模型发布 GGUF / QAT 版本，下载量往往超越原版，说明本地部署和低资源推理已成为用户刚需。  
- **开源权重 VS 闭源**：本周榜单几乎全部为开源权重模型，仅 Magenta 等部分有闭源成分，表明开源生态已形成自我强化的正循环。  
- **视频生成赛道加速**：Sulphur-2-base 基于现有模型量化即取得巨大成功，反映出用户对“能跑起来的视频模型”的迫切需求；字节的 Bernini-R 虽是早期但预示大厂更多投入。

---

## 值得探索

1. **[DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)**  
   - 理由：当前最强开源 LLM，多项基准领先，社区资源丰富，适合作为研究或应用的基础模型。

2. **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)**  
   - 理由：独树一帜的“目标定位”任务，无需边框标注即可指代任意物体，在视觉理解与机器人等领域

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*