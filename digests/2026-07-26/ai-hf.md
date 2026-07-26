# Hugging Face 热门模型日报 2026-07-26

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-07-26 02:25 UTC

---

好的，这是基于您提供的 2026-07-26 数据生成的《Hugging Face 热门模型日报》。

---

### 《Hugging Face 热门模型日报》- 2026-07-26

#### 今日速览

本周 Hugging Face 社区呈现出**多模态能力深化**与**极致量化微调**两大并行趋势。百度发布针对工业场景的 OCR 模型 `Unlimited-OCR` 一举登顶；而智谱的 `GLM-5.2` 和阿里通义千问的 `Qwen3.6-35B-A3B` 系列则展现了国产大模型在对话与 MoE 架构上的强大统治力。值得注意的是，围绕 `Qwen3.6` 和 `Laguna-S-2.1` 等基座模型的 **GGUF 量化与无审查微调**极度活跃，社区微调版本（如 `DavidAU`、`HauhauCS` 的作品）下载量惊人，显示用户对边缘部署和个性化模型的强烈需求。此外，微软开源了图像生成与机器人操作模型，NVIDIA 和 openbmb 分别在视频生成与机器人领域发力，AI 正加速从文本走向物理世界交互。

---

#### 热门模型

##### 🧠 语言模型（LLM、对话模型、指令微调）

- **zai-org/GLM-5.2**
  链接: https://huggingface.co/zai-org/GLM-5.2
  作者: zai-org | 👍 4,448 | ⬇️ 707,029
  **说明**：本周点赞量最高的模型，基于 MoE（混合专家）架构的对话模型，代表了国产大模型在通用对话领域的顶尖水平，是目前社区讨论的热点。

- **poolside/Laguna-S-2.1**
  链接: https://huggingface.co/poolside/Laguna-S-2.1
  作者: poolside | 👍 662 | ⬇️ 45,260
  **说明**：专注于代码生成或特定任务的文本生成模型，其强大的基座能力催生了大量下游微调和量化版本，生态扩展迅速。

- **Nanbeige/Nanbeige4.2-3B**
  链接: https://huggingface.co/Nanbeige/Nanbeige4.2-3B
  作者: Nanbeige | 👍 406 | ⬇️ 11,573
  **说明**：小尺寸但高效的语言模型，适合资源受限场景，体现了模型轻量化、高效化的生态趋势。

- **Motif-Technologies/Motif-3-Beta**
  链接: https://huggingface.co/Motif-Technologies/Motif-3-Beta
  作者: Motif-Technologies | 👍 191 | ⬇️ 2,270
  **说明**：用于特征提取的文本生成模型，显示了语言模型被用作通用特征提取器（如 RAG 场景）的趋势。

- **upstage/Solar-Open2-250B**
  链接: https://huggingface.co/upstage/Solar-Open2-250B
  作者: upstage | 👍 565 | ⬇️ 2,784
  **说明**：一个极具竞争力的巨量级（250B）开源模型，在学术界和高端企业应用场景备受关注，代表了 Scaling Law 仍在持续探索。

##### 🎨 多模态与生成（图像、视频、音频、文本到X）

- **baidu/Unlimited-OCR**
  链接: https://huggingface.co/baidu/Unlimited-OCR
  作者: baidu | 👍 3,107 | ⬇️ 2,564,264
  **说明**：百度推出的图像转文本模型，专为 OCR（光学字符识别）优化，下载量极高，显示了文档数字化和工业自动化领域对高效 OCR 模型的迫切需求。

- **Qwen/Qwen3.6-35B-A3B**
  链接: https://huggingface.co/Qwen/Qwen3.6-35B-A3B
  作者: Qwen | 👍 2,516 | ⬇️ 6,413,105
  **说明**：通义千问最新多模态 MoE 模型，仅激活 3B 参数即可达到 35B 级别的性能，下载量断层式领先，是当前社区最热门的基座模型之一。

- **thinkingmachines/Inkling**
  链接: https://huggingface.co/thinkingmachines/Inkling
  作者: thinkingmachines | 👍 1,571 | ⬇️ 31,575
  **说明**：一款支持对话的多模态模型，能够同时理解文本和图像并进行交互，展现了多模态对话系统的最新进展。

- **microsoft/Mage-Flow**
  链接: https://huggingface.co/microsoft/Mage-Flow
  作者: microsoft | 👍 277 | ⬇️ 1,156
  **说明**：微软发布的文本到图像生成模型，支持图像编辑功能，体现大厂对更可控、更灵活的图像生成工具的探索。

- **moonshotai/Kimi-K2.7-Code**
  链接: https://huggingface.co/moonshotai/Kimi-K2.7-Code
  作者: moonshotai | 👍 1,277 | ⬇️ 749,449
  **说明**：月之暗面 (Kimi) 推出的代码生成多模态模型，采用压缩张量技术，兼顾性能与效率，是代码智能领域的强有力竞争者。

- **nvidia/Cosmos3-Edge**
  链接: https://huggingface.co/nvidia/Cosmos3-Edge
  作者: nvidia | 👍 121 | ⬇️ 31,759
  **说明**：NVIDIA 的视频生成模型（边缘版），专注于在边缘设备上运行视频生成或理解任务，推动物理 AI 和仿真应用。

##### 🔧 专用模型（代码、数学、医疗、嵌入）

- **Kwaipilot/KAT-Coder-V2.5-Dev**
  链接: https://huggingface.co/Kwaipilot/KAT-Coder-V2.5-Dev
  作者: Kwaipilot | 👍 167 | ⬇️ 841
  **说明**：基于 MoE 架构的代码开发模型，针对特定编码任务优化，显示了编程助手领域百花齐放的生态。

- **openbmb/MiniCPM-RobotManip**
  链接: https://huggingface.co/openbmb/MiniCPM-RobotManip
  作者: openbmb | 👍 175 | ⬇️ 607
  **说明**：面壁智能 (openbmb) 发布的机器人操作模型，是视觉-语言-动作 (VLA) 模型的代表，连接语言模型与物理世界的关键尝试。

- **openbmb/MiniCPM-RobotTrack**
  链接: https://huggingface.co/openbmb/MiniCPM-RobotTrack
  作者: openbmb | 👍 128 | ⬇️ 379
  **说明**：与 `MiniCPM-RobotManip` 同系列的机器人轨迹跟踪模型，进一步丰富了机器人基座模型的生态。

- **owensong/Inflect-Micro-v2**
  链接: https://huggingface.co/owensong/Inflect-Micro-v2
  作者: owensong | 👍 85 | ⬇️ 47
  **说明**：面向 CPU 和边缘设备的本地文本到语音 (TTS) 模型，反应了 AI 语音合成轻量化、本地化的需求趋势。

##### 📦 微调与量化（社区微调、GGUF、AWQ）

- **DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF**
  链接: https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF
  作者: DavidAU | 👍 547 | ⬇️ 483,845
  **说明**：社区大神对 `Qwen3.6` 的极致微调与量化版本，集成了“无审查”等多种特性，下载量巨大，代表了社区用户对个性化、去限制化模型的追求。

- **HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive**
  链接: https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive
  作者: HauhauCS | 👍 3,092 | ⬇️ 1,988,680
  **说明**：针对 `Qwen3.6-35B-A3B` 的无审查微调版本，点赞数极高，再次印证了社区对原版模型行为进行调优和“解禁”的巨大热情。

- **prism-ml/Ternary-Bonsai-27B-gguf**
  链接: https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf
  作者: prism-ml | 👍 1,028 | ⬇️ 611,685
  **说明**：采用三进制（Ternary）量化的创新 27B 模型 GGUF 版本，在保持性能的同时极致压缩模型体积，是量化技术的前沿探索。

- **prism-ml/Bonsai-27B-gguf**
  链接: https://huggingface.co/prism-ml/Bonsai-27B-gguf
  作者: prism-ml | 👍 638 | ⬇️ 2,114,963
  **说明**：另一个极端量化的 27B 模型（1-bit），下载量超 200 万，虽然量化程度更深，但“Bonsai”系列说明了用户对在低功耗设备上运行大模型的强烈需求。

- **empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF**
  链接: https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF
  作者: empero-ai | 👍 2,465 | ⬇️ 1,570,995
  **说明**：结合了神话角色扮演风格的 9B 量化模型，体现了社区对“Claude 风格”对话和多样化角色扮演模型的热衷。

---

#### 生态信号

1.  **模型家族势头强劲**：**Qwen3.6** 和 **GLM-5.2** 是两个无可争议的“顶流”家族。前者凭借 MoE 架构的极高性价比（`35B-A3B`）和繁荣的社区微调生态（`DavidAU`、`HauhauCS` 等）占据半壁江山；后者则凭借传统密集 MoE 架构在对话任务上的深厚积累，以“论文级”表现赢得专业社区关注。
2.  **开源权重 vs 闭源**：本周排行榜几乎被**开源模型**及其社区衍生版本垄断。无论是企业（百度、微软、NVIDIA）还是研究机构（openbmb、zai-org），都倾向于通过开源权重来构建生态，以对抗闭源 API。微调版本的火爆，正是开源生态活力的集中体现。
3.  **量化与微调活动**：“**GGUF + 无审查**”是社区微调的两大关键词。用户不仅追求在本地（CPU/边缘设备）运行模型，更对模型的“价值观对齐”表现出了强烈的定制化需求（`Uncensored`）。这导致了以 `prism-ml` 为代表的极端量化技术（1-bit, 2-bit, Ternary）和以 `HauhauCS` 为代表的行为微调并行火爆。

---

#### 值得探索

1.  **zai-org/GLM-5.2**
  链接: https://huggingface.co/zai-org/GLM-5.2
  **理由**：作为本周点赞量冠军，它是目前国产 MoE 大模型的巅峰之作。无论你是想评估国产大模型的顶尖能力，还是希望深入研究 MoE 架构的 Scaling 潜力，这个模型都是必选项。

2.  **Qwen/Qwen3.6-35B-A3B**
  链接: https://huggingface.co/Qwen/Qwen3.6-35B-A3B
  **理由**：下载量断层领先，它是当前应用生态的核心基座。其“激活 3B 拥有 35B 性能”的 MoE 特性，为高效多模态应用（如 OCR、代码助手）提供了绝佳的起点。探索它，就是探索未来多模态应用的可能形态。

3.  **prism-ml/Ternary-Bonsai-27B-gguf**
  链接: https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf
  **理由**：如果你对模型量化的前沿技术感兴趣，这个三进制量化模型不容错过。它代表了在模型精度和部署效率之间寻求极致平衡的探索方向，对于推动大模型在个人电脑乃至手机上的运行具有重要意义。

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*