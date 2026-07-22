# Hugging Face 热门模型日报 2026-07-22

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-07-22 02:12 UTC

---

好的，作为AI模型生态分析师，以下是基于2026年7月22日数据生成的《Hugging Face热门模型日报》。

***

### Hugging Face 热门模型日报 (2026-07-22)

#### 今日速览

本周Hugging Face生态呈现三大趋势：一是**国产大模型与多模态模型强势崛起**，百度`Unlimited-OCR`与智谱`GLM-5.2`均获得数千点赞，代表了基础设施级别模型与前沿MoE架构的热度。二是**极致量化技术成为流量密码**，以`prism-ml`团队为首的1-bit和三值（Ternary）量化模型，虽然模型体量巨大（27B），但凭借极低的资源消耗获得了惊人的下载量，其中`Ternary-Bonsai-27B-gguf`下载量超43万。三是**推理与去审查化（Uncensored）模型**持续活跃，多个基于Qwen3.5/3.6的“非审查”微调版本（如HauhauCS、DavidAU）热度不减，反映出社区对开放性对话能力的追求。

#### 热门模型

##### 🧠 语言模型（LLM、对话模型、指令微调）

*   **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** | 作者: zai-org | 👍 4,283 | ⬇️ 545,109
    *   **说明**: 智谱AI推出的最新一代MoE（混合专家）大模型。作为本周点赞数最高的模型之一，它代表了顶尖国产模型的开源最新进展。
*   **[moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)** | 作者: moonshotai | 👍 1,200 | ⬇️ 722,058
    *   **说明**: 月之暗面推出的Kimi系列代码模型。作为Kimi K2的升级版，它专注于代码生成与理解，展现了国内大厂在垂直领域的深耕。
*   **[Nanbeige/Nanbeige4.2-3B](https://huggingface.co/Nanbeige/Nanbeige4.2-3B)** | 作者: Nanbeige | 👍 79 | ⬇️ 0
    *   **说明**: 一个新发布的小参数（3B）语言模型。虽然下载量尚在初期，但作为新兴模型值得关注，可能在小模型部署领域有潜力。

##### 🎨 多模态与生成（图像、视频、音频、文本到X）

*   **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** | 作者: baidu | 👍 2,609 | ⬇️ 2,237,351
    *   **说明**: 百度的通用OCR（光学字符识别）模型。凭借顶级点赞数和超过223万的下载量，该模型无疑是本周的明星，证明了其在各类图像文字识别任务中的实用性。
*   **[google/gemma-4-31B-it](https://huggingface.co/google/gemma-4-31B-it)** | 作者: google | 👍 3,314 | ⬇️ 12,113,203
    *   **说明**: 谷歌最新推出的Gemma 4多模态对话模型，参数为31B。下载量超过1200万，社区热度极高，是当前最强的开源多模态模型之一。
*   **[ATH-MaaS/OvisOCR2](https://huggingface.co/ATH-MaaS/OvisOCR2)** | 作者: ATH-MaaS | 👍 238 | ⬇️ 17,162
    *   **说明**: 基于Qwen3.5的OCR视觉模型。作为专业OCR模型，它获得了社区的积极关注，表明针对特定视觉任务的模型仍有需求。
*   **[Alissonerdx/LTX-Best-Face-ID](https://huggingface.co/Alissonerdx/LTX-Best-Face-ID)** | 作者: Alissonerdx | 👍 222 | ⬇️ 0
    *   **说明**: 一个用于LTX-Video的人脸身份保持LoRA模型。专注于文本到视频中的人脸一致性生成，虽然下载量尚处早期，但代表了视频生成领域的一个细化方向。
*   **[OpenMOSS-Team/MOSS-Transcribe-Diarize](https://huggingface.co/OpenMOSS-Team/MOSS-Transcribe-Diarize)** | 作者: OpenMOSS-Team | 👍 299 | ⬇️ 92,265
    *   **说明**: 专注于语音转录（ASR）和说话人分离的模型。它将传统语音处理与大模型结合，在多模态音频处理领域具有实用价值。

##### 🔧 专用模型（代码、数学、医疗、嵌入）

*   **[nvidia/Nemotron-3-Embed-1B-BF16](https://huggingface.co/nvidia/Nemotron-3-Embed-1B-BF16)** | 作者: nvidia | 👍 96 | ⬇️ 93,021
    *   **说明**: Nvidia推出的1B参数嵌入模型。在检索增强生成（RAG）日益流行的背景下，优质的嵌入模型是构建知识库的关键组件。
*   **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)** | 作者: nvidia | 👍 903 | ⬇️ 590,230
    *   **说明**: Nvidia的流式自动语音识别模型，参数仅0.6B。其高下载量表明，低延迟、高性能的流式ASR模型是工业级应用的刚需。
*   **[Motif-Technologies/Motif-3-Beta](https://huggingface.co/Motif-Technologies/Motif-3-Beta)** | 作者: Motif-Technologies | 👍 127 | ⬇️ 125
    *   **说明**: Motif团队发布的下一代特征提取工具模型Beta版。它被标注为“feature-extraction”，可能在信息检索、文本分类等基础任务上有创新。
*   **[openbmb/MiniCPM-RobotManip](https://huggingface.co/openbmb/MiniCPM-RobotManip)** & **[openbmb/MiniCPM-RobotTrack](https://huggingface.co/openbmb/MiniCPM-RobotTrack)** | 作者: openbmb | 👍 147/107 | ⬇️ 58/72
    *   **说明**: 面壁智能（OpenBMB）推出的机器人操作与追踪模型。属于前沿的VLA（视觉-语言-动作）模型，代表了多模态从感知到行动的最新探索。
*   **[Cactus-Compute/needle](https://huggingface.co/Cactus-Compute/needle)** | 作者: Cactus-Compute | 👍 298 | ⬇️ 1,068
    *   **说明**: 一个基于JAX的函数调用（Function Calling）和工具使用模型。在Agent生态爆发期，专注于工具调用的模型是构建智能代理的核心。

##### 📦 微调与量化（社区微调、GGUF、AWQ）

*   **[prism-ml/Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)** | 作者: prism-ml | 👍 899 | ⬇️ 432,196
    *   **说明**: 首创的**三值（Ternary）量化**大模型（27B）。它以极低的精度和存储开销，在保持一定质量的同时实现了高下载量，是量化技术的突破。
*   **[prism-ml/Bonsai-27B-gguf](https://huggingface.co/prism-ml/Bonsai-27B-gguf)** | 作者: prism-ml | 👍 571 | ⬇️ 1,404,962
    *   **说明**: **1-bit**量化的Bonsai模型。下载量超过140万，是本周最受欢迎的模型之一，表明社区对在消费级硬件上运行超大模型的渴望。
*   **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** | 作者: HauhauCS | 👍 2,971 | ⬇️ 1,997,690
    *   **说明**: 基于Qwen3.6特定版本的社区非审查（Uncensored）微调模型。点赞数极高、下载量近200万，反映了社区对“无限制”对话模型的巨大需求。
*   **[DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF)** | 作者: DavidAU | 👍 249 | ⬇️ 62,842
    *   **说明**: 另一个基于Qwen3.6的非审查模型，并进行了一系列复杂的融合与微调操作。名字极长，体现了社区在模型魔改上的极度热情。
*   **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** | 作者: empero-ai | 👍 2,389 | ⬇️ 2,133,420
    *   **说明**: 基于Qwen3.5的“神话”风格推理对话模型GGUF版本。将“推理”与“创意”结合，高下载量说明社区欢迎有特色、有“人格”的对话模型。

#### 生态信号

本周生态呈现几大信号：

1.  **模型家族群雄割据**：开源社区不再一家独大。**Qwen**（特别是3.5/3.6系列）家族生态最为庞大，大量微调和量化版本涌现，成为社区二创的主要基座。**Kimi**、**GLM**和**Gemma**也凭借大厂背书和新模型发布，形成了自己的开发者势力圈。
2.  **开源壁垒与密度**：从`google/gemma-4-31B-it`超1200万下载量可见，顶级开源模型的影响力巨大。同时，**百度**和**智谱**等公司发布高质模型，表明**开源权重模式**仍是主流，且竞争从“发布”转向了“生态服务”（如量化、微调）。
3.  **量化内卷：走向“比特”极致**：`prism-ml`的1-bit和三值量化模型获得巨大成功，标志着社区对**极致压缩**的追求。未来，如何在极低比特下保证甚至提升模型质量，将成为量化工具（如`llama.cpp`、`mlx`）和量化生态的核心竞争点。
4.  **微调方向：去审查与个性化**：大量“Uncensored”模型的高赞和高下载，表明用户对安全的限制存在普遍抵触情绪，追求无审查、高自由度体验。同时，如“Mythos”等具有特定人格的模型也受到追捧，**个性化和风格化微调**正在成为一个重要方向。

#### 值得探索

1.  **zai-org/GLM-5.2**: 推荐理由：智谱AI最新的MoE模型，代表了国产大模型在架构设计上的前沿水平。如果你是架构研究者或关注国产模型发展，这是必看模型。
2.  **google/gemma-4-31B-it**: 推荐理由：谷歌今年的重磅开源模型，多模态能力强大，且下载量惊人。适合想体验最强开源基础模型、或多模态应用的开发者。
3.  **OpenMOSS-Team/MOSS-Transcribe-Diarize**: 推荐理由：开源社区中高质量的ASR（含说话人分离）模型并不常见。如果你有音频处理、会议纪要等现实需求，这个模型值得优先尝试，它代表了大模型在垂直音频领域的落地。

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*