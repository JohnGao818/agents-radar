# Hugging Face 热门模型日报 2026-06-10

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-06-10 02:58 UTC

---

# Hugging Face 热门模型日报 (2026-06-10)

## 📰 今日速览

本周 Hugging Face 生态呈现 **两大亮点**：一是 **DeepSeek-V4-Pro** 以超 4700 点赞、430 万下载量强势登顶，成为通用对话领域的新标杆；二是 **Google Gemma 4 系列** 全面开花，其 12B 和 26B 模型的量化、微调版本（unsloth、OBLITERATUS 等）在社区中掀起二次开发热潮。与此同时，**NVIDIA** 贡献了多款多模态工具（LocateAnything-3B、Cosmos3-Nano）和超大 MoE 模型（Nemotron-3 Ultra 550B），**Ideogram 4** 作为顶级文生图模型也备受关注。多模态、MoE 稀疏化、量化部署成为本周最强劲的三大技术趋势。

## 🔥 热门模型

### 🧠 语言模型（LLM、对话模型、指令微调）

| 模型 | 作者 | 点赞/下载 | 一句话说明 |
|------|------|-----------|------------|
| [DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro) | deepseek-ai | 4,741 / 4,302,553 | 新一代超大规模对话模型，MoE 架构，推理与生成能力全面领先，本周绝对焦点。 |
| [NVIDIA-Nemotron-3-Ultra-550B-A55B-BF16](https://huggingface.co/nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-BF16) | nvidia | 175 / 56,864 | 550B 总参数、55B 激活的 MoE 巨模型，专为高难度推理任务设计，企业级性能标杆。 |
| [NVIDIA-Nemotron-3-Ultra-550B-A55B-NVFP4](https://huggingface.co/nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-NVFP4) | nvidia | 154 / 71,818 | 同一模型的 NVFP4 低精度版本，兼顾极低成本与高性能，适合大规模云端部署。 |
| [North-Mini-Code-1.0](https://huggingface.co/CohereLabs/North-Mini-Code-1.0) | CohereLabs | 167 / 1,784 | Cohere 推出的小型编程专用 MoE 模型，专注代码生成与推理，轻量实用。 |
| [LFM2.5-8B-A1B](https://huggingface.co/LiquidAI/LFM2.5-8B-A1B) | LiquidAI | 572 / 137,138 | 8B 总参、1B 激活的高效 MoE 语言模型，以超低推理成本提供强大性能，社区热度高。 |
| [HRM-Text-1B](https://huggingface.co/sapientinc/HRM-Text-1B) | sapientinc | 735 / 133,351 | 10B 参数但仅有 1B 激活的 MoE 模型，强调高效推理与资源节省，适合边缘部署。 |
| [Nex-N2-Pro](https://huggingface.co/nex-agi/Nex-N2-Pro) | nex-agi | 162 / 783 | 基于 Qwen3.5 MoE 架构的进阶版，支持图像+文本多模态生成。 |
| [Nex-N2-mini](https://huggingface.co/nex-agi/Nex-N2-mini) | nex-agi | 112 / 748 | 同系列的迷你版，适合快速原型验证。 |
| [Mellum2-12B-A2.5B-Thinking](https://huggingface.co/JetBrains/Mellum2-12B-A2.5B-Thinking) | JetBrains | 273 / 17,571 | JetBrains 推出的思考型 MoE 模型，注重逻辑推理与对话质量。 |

### 🎨 多模态与生成（图像、视频、音频、文本到X）

| 模型 | 作者 | 点赞/下载 | 一句话说明 |
|------|------|-----------|------------|
| [Ideogram-4-fp8](https://huggingface.co/ideogram-ai/ideogram-4-fp8) | ideogram-ai | 442 / 5,915 | 第四代文生图旗舰模型，FP8 量化版，生成质量与速度兼备。 |
| [Ideogram-4-nf4](https://huggingface.co/ideogram-ai/ideogram-4-nf4) | ideogram-ai | 288 / 5,250 | 同样基于 Ideogram-4 的 NF4 量化版，显存需求更低。 |
| [Ideogram-4 (Comfy-Org)](https://huggingface.co/Comfy-Org/Ideogram-4) | Comfy-Org | 113 / 0 | ComfyUI 社区封装版本，方便在 ComfyUI 工作流中直接使用。 |
| [LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B) | nvidia | 1,733 / 123,922 | NVIDIA 推出的通用视觉定位模型，可基于文本描述在图像中定位任意物体，零样本能力强。 |
| [Gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it) | google | 817 / 581,354 | Google 最新多模态统一模型，支持图像、文本、音频任意输入，被称为“全能模型”。 |
| [Gemma-4-12B](https://huggingface.co/google/gemma-4-12B) | google | 480 / 122,464 | 基础版（非指令版），供开发者进一步微调。 |
| [Gemma-4-12B-it-GGUF](https://huggingface.co/unsloth/gemma-4-12b-it-GGUF) | unsloth | 533 / 660,140 | unsloth 社区量化的 GGUF 版，极受终端用户欢迎，下载量最高。 |
| [Gemma-4-12B-it-qat-GGUF](https://huggingface.co/unsloth/gemma-4-12B-it-qat-GGUF) | unsloth | 172 / 127,332 | 基于 QAT（量化感知训练）的二次量化版，质量更高。 |
| [Gemma-4-12B-it-qat-q4_0-gguf](https://huggingface.co/google/gemma-4-12B-it-qat-q4_0-gguf) | google | 115 / 63,049 | Google 官方发布的 QAT 量化版，采用 q4_0 量化格式。 |
| [Gemma-4-26B-A4B-it-qat-GGUF](https://huggingface.co/unsloth/gemma-4-26B-A4B-it-qat-GGUF) | unsloth | 115 / 96,059 | 26B 总参、4B 激活的 MoE 版本量化，兼顾规模与效率。 |
| [Qwen3.6-35B-A3B-Uncensored](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive) | HauhauCS | 1,596 / 2,983,909 | 社区基于 Qwen3.6 的 MoE 无审查版，35B 参数 3B 激活，下载量近 300 万。 |
| [Gemma-4-12B-OBLITERATED](https://huggingface.co/OBLITERATUS/Gemma-4-12B-OBLITERATED) | OBLITERATUS | 145 / 8,106 | 社区对 Gemma-4 进行的极致“剃度”微调版，追求开放自由度。 |
| [Step-3.7-Flash](https://huggingface.co/stepfun-ai/Step-3.7-Flash) | stepfun-ai | 359 / 46,729 | 阶跃星辰推出的视觉语言模型，轻量快速，适合多场景部署。 |
| [Bernini-R](https://huggingface.co/ByteDance/Bernini-R) | ByteDance | 197 / 281 | 字节跳动推出的文生视频模型，基于渲染器架构，生成连贯视频序列。 |
| [JoyAI-Echo](https://huggingface.co/jdopensource/JoyAI-Echo) | jdopensource | 115 / 4,502 | 京东开源的文生视频/音频联合生成模型，支持音视频同步。 |
| [Higgs-Audio-v3-tts-4b](https://huggingface.co/bosonai/higgs-audio-v3-tts-4b) | bosonai | 285 / 16,207 | 4B 参数的文本到语音模型，基于 Higgs 多模态架构，语音自然度高。 |
| [MisoTTS](https://huggingface.co/MisoLabs/MisoTTS) | MisoLabs | 175 / 0 | 新型 TTS 模型，今日刚发布即获关注，零下载但点赞可观。 |
| [magenta-realtime-2](https://huggingface.co/google/magenta-realtime-2) | google | 164 / 18,216 | Google 实时音乐/音频生成模型，TFLite 格式，适合交互式创作。 |
| [Cosmos3-Nano](https://huggingface.co/nvidia/Cosmos3-Nano) | nvidia | 214 / 36,739 | NVIDIA 新一代多模态全能模型（Cosmos3 系列），支持视觉、语言、音频理解与生成。 |

### 🔧 专用模型（代码、数学、医疗、嵌入）

| 模型 | 作者 | 点赞/下载 | 一句话说明 |
|------|------|-----------|------------|
| [PaddleOCR-VL-1.6](https://huggingface.co/PaddlePaddle/PaddleOCR-VL-1.6) | PaddlePaddle | 281 / 10,139 | 百度飞桨推出的视觉语言 OCR 模型，基于 ERNIE 4.5，文字识别与理解能力突出。 |
| [LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B) | nvidia | 1,733 / 123,922 | 虽属多模态，但其核心为“视觉定位”专用任务，零样本目标检测表现惊艳。 |
| [HRM-Text-1B](https://huggingface.co/sapientinc/HRM-Text-1B) | sapientinc | 735 / 133,351 | 企业级 HRM（高效推理模型）专用，强调低延迟与资源节约。 |

### 📦 微调与量化（社区微调、GGUF、AWQ）

| 模型 | 作者 | 点赞/下载 | 一句话说明 |
|------|------|-----------|------------|
| [unsloth/gemma-4-12b-it-GGUF](https://huggingface.co/unsloth/gemma-4-12b-it-GGUF) | unsloth | 533 / 660,140 | 最受欢迎的 Gemma-4 量化版，下载量 66 万+，16-bit GGUF 格式即开即用。 |
| [unsloth/gemma-4-12B-it-qat-GGUF](https://huggingface.co/unsloth/gemma-4-12B-it-qat-GGUF) | unsloth | 172 / 127,332 | 采用 QAT 训练的量化版，精度损失更小。 |
| [unsloth/gemma-4-26B-A4B-it-qat-GGUF](https://huggingface.co/unsloth/gemma-4-26B-A4B-it-qat-GGUF) | unsloth | 115 / 96,059 | 26B MoE 模型的 QAT 量化，适合低资源场景。 |
| [google/gemma-4-12B-it-qat-q4_0-gguf](https://huggingface.co/google/gemma-4-12B-it-qat-q4_0-gguf) | google | 115 / 63,049 | Google 官方亲自下场量化，使用 4bit GGUF 格式。 |
| [HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive) | HauhauCS | 1,596 / 2,983,909 | 社区微调无审查版，MoE 量化（GGUF），下载量近 300 万，反映用户对“自由度”的强烈需求。 |
| [OBLITERATUS/Gemma-4-12B-OBLITERATED](https://huggingface.co/OBLITERATUS/Gemma-4-12B-OBLITERATED) | OBLITERATUS | 145 / 8,106 | 社区极端微调版，去除内容限制，配合量化格式发布。 |
| [NVIDIA-Nemotron-3-Ultra-550B-A55B-NVFP4](https://huggingface.co/nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-NVFP4) | nvidia | 154 / 71,818 | 官方提供 FP4 量化版本，推动超大模型落地。 |
| [nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b) | nvidia | 321 / 4,181 | 专门用于流式语音识别的轻量 ASR 模型，具备缓存感知设计。 |

## 🌐 生态信号

1. **DeepSeek V4 与 Gemma 4 双雄对峙**：DeepSeek-V4-Pro 以绝对优势占据下载与点赞榜首，显示开源大模型在通用对话领域仍具统治力；而 Google 的 Gemma 4 系列凭借“any-to-any”多模态能力，吸引了大量社区二次创作，量化版本下载量合计超 90 万。
2. **MoE 与量化成为标配**：本周 Top 30 中近 2/3 的模型采用 MoE 架构（如 DeepSeek V4、Nemotron 3、Gemma 4-A4B、LFM2.5、Nex-N2 等），且几乎都有 GGUF 或 FP4 量化版。社区对“更便宜、更快、更小”的执念持续增强，unsloth 成为量化生态核心贡献者。
3. **多模态全面开花**：从图像（Ideogram 4）、视频（Bernini-R、JoyAI-Echo）、音频（Higgs TTS、MisoTTS）到统一感知（Gemma 4、Cosmos3），模型能感知的模态越来越多。NVIDIA 的 LocateAnything 重新定义了“视觉定位”任务，零样本能力令人瞩目。
4. **大厂开源权重加速**：Google、NVIDIA、ByteDance、京东、百度均在本周发布自有开源模型，闭源阵营进一步收缩。但社区“uncensored”微调版的流行（Qwen3.6 无审查版下载 300 万）也暗示用户对内容限制的抵触。

## 🔍 值得探索

- **[DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)** — 如果想体验当前最强开源通用模型（对话、推理、代码），这是首选。4.3M 下载量已证明了它的可靠性，建议直接运行 FP16 版或尝试社区量化版。
- **[LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — NVIDIA 的零样本视觉定位模型，只需自然语言文本即可在图像中定位任意物体，效果惊艳。适合机器人、图像标注等应用场景，强烈推荐尝试在线 demo。
- **[Ideogram-4-fp8](https://huggingface.co/ideogram-ai/ideogram-4-fp8)** — 当前文生图领域的新标杆，结合 FP8 量化后可在消费级 GPU 上运行。若对图像生成质量有极致要求，这是目前最好的选择之一。

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*