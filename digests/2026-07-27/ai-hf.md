# Hugging Face 热门模型日报 2026-07-27

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-07-27 02:32 UTC

---

好的，收到。作为AI模型生态分析师，以下是根据您提供的数据生成的《Hugging Face 热门模型日报》。

---

### **Hugging Face 热门模型日报 | 2026年7月27日**

---

#### **今日速览**

本周 Hugging Face 生态呈现多点开花局面。**智谱 (Zhipu AI) 的 GLM-5.2** 系列凭借其超大MoE架构和DS对齐技术，以压倒性点赞数登顶榜首，成为全网焦点。与此同时，**社区微调版 Qwen3.6** 系列在下载量上表现惊人，社区对“去审查 (Uncensored)”及特定角色风格的偏好形成强大洪流。**OCR领域**迎来巨头出手，百度的 `Unlimited-OCR` 凭借极高的实用性和下载量证明了“实用主义”模型的长尾价值。此外，以 **MiniCPM** 为代表的**机器人基础模型**开始崭露头角，标志着多模态模型向物理世界延伸的新趋势。

---

#### **热门模型**

##### 🧠 语言模型 (LLM、对话模型、指令微调)

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — 作者: zai-org | 点赞: 4,480 | 下载: 827,191
  - 由智谱AI发布的新一代MoE大模型，采用DS对齐技术。凭借强大的性能和开源诚意，成为本周最受瞩目的模型。
- **[upstage/Solar-Open2-250B](https://huggingface.co/upstage/Solar-Open2-250B)** — 作者: upstage | 点赞: 596 | 下载: 3,305
  - Upstage 推出的2500亿参数级别大模型，旨在挑战性能天花板，是开源社区向超大规模模型迈进的重要一步。
- **[Nanbeige/Nanbeige4.2-3B](https://huggingface.co/Nanbeige/Nanbeige4.2-3B)** — 作者: Nanbeige | 点赞: 450 | 下载: 14,049
  - 一款小而精的3B参数语言模型，在资源受限场景下提供强大的文本生成能力，适合本地部署和效率优先的应用。

##### 🎨 多模态与生成 (图像、视频、音频、文本到X)

- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** — 作者: baidu | 点赞: 3,212 | 下载: 2,593,460
  - 百度发布的通用OCR模型，以其超高的下载量证明了其在图像文字提取任务上的卓越实用性和广泛需求。
- **[thinkingmachines/Inkling](https://huggingface.co/thinkingmachines/Inkling)** — 作者: thinkingmachines | 点赞: 1,579 | 下载: 34,511
  - Thinking Machines 推出的多模态对话模型，具备图文理解与生成能力，是视觉语言模型的重要代表。
- **[microsoft/Mage-Flow](https://huggingface.co/microsoft/Mage-Flow)** — 作者: microsoft | 点赞: 336 | 下载: 1,375
  - 微软推出的基于扩散模型的文本到图像生成框架，展示了在图像编辑与生成领域的持续创新能力。
- **[owensong/Inflect-Micro-v2](https://huggingface.co/owensong/Inflect-Micro-v2)** — 作者: owensong | 点赞: 180 | 下载: 298
  - 一款面向边缘设备（CPU/Edge AI）的轻量级文本到语音模型，为离线语音合成场景提供了高效解决方案。
- **[nvidia/Cosmos3-Edge](https://huggingface.co/nvidia/Cosmos3-Edge)** — 作者: nvidia | 点赞: 125 | 下载: 32,700
  - 英伟达推出的新一代视觉生成模型，专注于边缘场景，表明强大的GPU厂商正在布局轻量级生成式AI。

##### 🔧 专用模型 (代码、数学、医疗、嵌入)

- **[Kwaipilot/KAT-Coder-V2.5-Dev](https://huggingface.co/Kwaipilot/KAT-Coder-V2.5-Dev)** — 作者: Kwaipilot | 点赞: 198 | 下载: 3,764
  - 基于Qwen3.5 MoE的代码模型，专注于编程辅助，是开发者社区关注的热点。
- **[microsoft/Fara1.5-27B](https://huggingface.co/microsoft/Fara1.5-27B)** — 作者: microsoft | 点赞: 110 | 下载: 1,225
  - 微软推出的“计算机使用”模型，一个能理解屏幕信息并执行操作的视觉语言模型，是智能代理 (Agent) 领域的前沿探索。
- **[openbmb/MiniCPM-RobotManip](https://huggingface.co/openbmb/MiniCPM-RobotManip)** & **[openbmb/MiniCPM-RobotTrack](https://huggingface.co/openbmb/MiniCPM-RobotTrack)** — 作者: openbmb | 点赞: ~130-177 | 下载: ~400-650
  - OpenBMB 将 MiniCPM 能力拓展至机器人领域，分别用于“操纵 (Manip)”和“追踪 (Track)”，是“视觉-语言-动作”模型落地的先锋。

##### 📦 微调与量化 (社区微调、GGUF、AWQ)

- **[DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-...](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF)** — 作者: DavidAU | 点赞: 640 | 下载: 552,026
  - 社区基于Qwen3.6进行精细化微调的典型，以“无审查”和“创意融合”为特色，下载量极高，反映了社区对个性化角色的强烈需求。
- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-...](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — 作者: HauhauCS | 点赞: 3,112 | 下载: 1,927,138
  - 与 DavidAU 类似，但模型体量更大（35B），是Qwen3.6系列社区微调的另一焦点，其夸张的下载量表明这是当前最活跃的生态圈之一。
- **[prism-ml/Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)** & **[prism-ml/Bonsai-27B-gguf](https://huggingface.co/prism-ml/Bonsai-27B-gguf)** — 作者: prism-ml | 点赞: ~650-1,051 | 下载: ~630k-2.1M
  - 一系列极低比特量化模型（1-bit和2-bit），将27B模型大小压缩至极致，代表了终端部署模型的前沿量化方向。

---

#### **生态信号**

1.  **Qwen 家族社区生态愈发繁荣：** 本周榜单一再证明，阿里Qwen系列已成为当前社区微调、量化和二次创作的“最热基底”。尤其是 `Qwen3.6` 系列，衍生出了大量针对不同角色扮演和去审查需求的变体，其总下载量甚至超越了原版模型，是“基座+社区”模式的胜利。
2.  **MoE与极简主义并行：** 以 `GLM-5.2` 和 `Solar-Open2` 为代表的超大规模MoE模型，与 `Ternary-Bonsai` 和 `Nanbeige4.2` 为代表的极致小参数或极低量化模型同时走红。这表明行业正朝着“更高性能”和“更低成本”两个截然不同但同等重要的方向狂奔。
3.  **Open Source Weights是核心壁垒：** 本周所有热门模型均为开源权重（Open Weights）模型。无论是百度的OCR、微软的Mage-Flow，还是社区微调版，开放发布的模式依然是驱动下载量和影响力增长的最强引擎。

---

#### **值得探索**

1.  **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)**: 作为本周最大赢家，其采用的DS对齐技术和MoE架构值得所有研究者和开发者深入体验，代表了前沿技术的最新应用。
2.  **[moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)**: Kimi的代码版本直接挑战了传统编码模型地位，其使用`compressed-tensors`标签，暗示了在模型压缩方面的独特技术，对部署和优化有重要启发。
3.  **[bottlecapai/ThinkingCap-Qwen3.6-27B](https://huggingface.co/bottlecapai/ThinkingCap-Qwen3.6-27B)**: 名为“思考帽”，暗示该模型可能通过特定微调增强了推理能力，是探索如何提升Qwen系列思考深度的优秀案例，潜力巨大。

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*