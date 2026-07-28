# Hugging Face 热门模型日报 2026-07-28

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-07-28 02:07 UTC

---

好的，以下是基于您提供的数据生成的《Hugging Face 热门模型日报》。

---

## Hugging Face 热门模型日报 | 2026-07-28

### 今日速览

本周 Hugging Face 生态呈现出“多模态统治、量化遍地、寡头暂歇”的格局。`Qwen3.6-35B-A3B` 凭借其 MoE 架构和官方权重成为下载量冠军，而 **Kimi K3** 与 **GLM-5.2** 则摘得点赞数前两名，显示市场对国产大模型（Moonshot、智谱）的高期待。值得注意的是，**Kimi K2.7-Code** 和 **Unlimited-OCR** 等垂直任务模型下载量激增，说明开发者正在将注意力从“聊天”转向“落地应用”。社区量化活动依然火爆，`Bonsai-27B` 系列凭借极低比特量化（1-2bit）持续霸榜下载量，展现了边缘部署的强烈需求。

### 热门模型

#### 🧠 语言模型（LLM、对话模型、指令微调）

- **zai-org/GLM-5.2**
  - 作者: zai-org | 点赞: 4,552 | 下载: 1,003,547
  - 一句话说明：智谱 GLM-5.2 多专家 MoE 模型，凭借强大的对话与推理能力成为本周点赞亚军，是国产闭源模型转开源的标杆。
- **upstage/Solar-Open2-250B**
  - 作者: upstage | 点赞: 629 | 下载: 3,761
  - 一句话说明：韩国 Upstage 开源 250B 超大参数模型，虽下载量不大，但证明了非中美团队在超大模型领域的持续投入。
- **Nanbeige/Nanbeige4.2-3B**
  - 作者: Nanbeige | 点赞: 493 | 下载: 16,518
  - 一句话说明：小而精的语言模型，专注 3B 参数的高效部署场景，适合资源受限的任务。
- **Motif-Technologies/Motif-3-Beta**
  - 作者: Motif-Technologies | 点赞: 199 | 下载: 2,532
  - 一句话说明：Motif 新一代基础模型，定位通用文本生成，尚处 Beta 阶段，社区正在观察其能力上限。

#### 🎨 多模态与生成（图像、视频、音频、文本到X）

- **moonshotai/Kimi-K3**
  - 作者: moonshotai | 点赞: 6,326 | 下载: 2,850
  - 一句话说明：Moonshot 最新多模态旗舰（image-text-to-text），本周新星，点赞数断层第一，标志着 Kimi 系列开始发力多模态。
- **baidu/Unlimited-OCR**
  - 作者: baidu | 点赞: 3,333 | 下载: 2,645,773
  - 一句话说明：百度开源的“无限”OCR 模型，下载量惊人，精准击中了文档数字化与图像信息提取的高频需求。
- **microsoft/Mage-Flow**
  - 作者: microsoft | 点赞: 390 | 下载: 1,691
  - 一句话说明：微软的文本到图像与编辑开源方案，对标 FLUX 与 DALL·E，代表了大型科技公司在开源文生图领域的布局。
- **owensong/Inflect-Micro-v2**
  - 作者: owensong | 点赞: 224 | 下载: 483
  - 一句话说明：专为 CPU 和边缘 AI 设计的本地 TTS 模型，关注实时语音合成中的隐私与低延迟需求。
- **microsoft/Mage-Flow-Edit-Turbo**
  - 作者: microsoft | 点赞: 102 | 下载: 1,115
  - 一句话说明：Mage-Flow 的加速编辑版本，专攻基于指令的图像编辑任务，推理速度更快。
- **conradlocke/krea2-identity-edit**
  - 作者: conradlocke | 点赞: 556 | 下载: 0
  - 一句话说明：基于 Krea-2 的身份编辑 LoRA，用于生成风格一致的特定人物图像，正在探索 AI 写真等场景。

#### 🔧 专用模型（代码、数学、医疗、嵌入）

- **moonshotai/Kimi-K2.7-Code**
  - 作者: moonshotai | 点赞: 1,323 | 下载: 695,744
  - 一句话说明：Kimi K3 系列的代码特化版本，兼具视觉能力（image-text-to-text）与编程能力，几乎成为开发者标配。
- **Kwaipilot/KAT-Coder-V2.5-Dev**
  - 作者: Kwaipilot | 点赞: 242 | 下载: 5,312
  - 一句话说明：基于 Qwen3.5 MoE 的代码生成模型，针对开发环境进行了优化。
- **ATH-MaaS/OvisOCR2**
  - 作者: ATH-MaaS | 点赞: 327 | 下载: 42,152
  - 一句话说明：OCR 细分领域的专精模型，与百度 Unlimited-OCR 形成竞争，专注更特定的识别场景。
- **microsoft/Fara1.5-27B**
  - 作者: microsoft | 点赞: 152 | 下载: 1,406
  - 一句话说明：微软开源的“电脑使用”（computer-use）模型，旨在让 AI 通过视觉理解来操作 GUI 界面。
- **fdtn-ai/antares-1b**
  - 作者: fdtn-ai | 点赞: 207 | 下载: 6,421
  - 一句话说明：专注于网络安全的 1B 级语言模型，代号“Antares”，验证了安全领域的垂域模型需求。

#### 📦 微调与量化（社区微调、GGUF、AWQ）

- **DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF**
  - 作者: DavidAU | 点赞: 754 | 下载: 634,146
  - 一句话说明：经典的社区暴力微调+量化案例，在 Qwen3.6 基础上灌入多种数据集，追求极致“去审查”，下载量极高。
- **unsloth/Laguna-S-2.1-GGUF**
  - 作者: unsloth | 点赞: 218 | 下载: 117,456
  - 一句话说明：Unsloth 团队对 `poolside/Laguna-S-2.1` 的高效 GGUF 量化版本，推理效率优化首选。
- **prism-ml/Ternary-Bonsai-27B-gguf**
  - 作者: prism-ml | 点赞: 1,069 | 下载: 648,938
  - 一句话说明：创新的“三值化”（Ternary）量化方案，将模型权重压缩至 2-bit，在极低损条件下实现 27B 模型本地运行。
- **HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive**
  - 作者: HauhauCS | 点赞: 3,133 | 下载: 1,894,395
  - 一句话说明：Qwen3.6-35B-A3B 的社区“激进”微调版，兼顾 MoE 效率与去审查，下载量直逼官方版本。
- **prism-ml/Bonsai-27B-gguf**
  - 作者: prism-ml | 点赞: 659 | 下载: 2,257,928
  - 一句话说明：Ternery Bonsai 的“前辈”，将参数压缩到 1-bit 极限量化的代表，下载量全网第一，证明了极限量化的高热度。
- **empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF**
  - 作者: empero-ai | 点赞: 2,491 | 下载: 1,336,263
  - 一句话说明：融合 Claude 风格与推理能力的微调模型，9B 参数兼具高效与创意，是“角色扮演”类社区的宠儿。

### 生态信号

本周生态呈现三大信号：
1.  **“Qwen 宇宙”成型**：来自 Qwen、DavidAU、HauhauCS、LuffyTheFox 等不同作者的 Qwen3.6 系列模型（包括 MoE 版本）占据了多模态与量化领域的大量份额。Qwen 已经从单一模型演变为一个庞大的生态系统。
2.  **量化竞赛白热化**：社区已经不满足于常规的 4-bit 或 8-bit 量化。`Bonsai-27B` 系列（1-bit/2-bit）的极高下载量表明，开发者正在疯狂追求在消费级硬件（如 MacBook、RTX 4090）上运行 20B+ 大模型的极限体验，尽管这通常会牺牲一定精度。
3.  **多模态落地加速**：头部模型（Kimi K3, Unlimited-OCR）的任务标签几乎都是 `image-text-to-text`，而非单纯的 `text-generation`。这表明社区关注点已从“能聊天”转向“能看、能读、能操作（Computer Use）”，多模态 Agent 是下一个明确的爆发点。

### 值得探索

- **moonshotai/Kimi-K3**：作为本周最受关注的模型（点赞数第一），且来自现象级产品 Kimi 的官方团队，其多模态能力（尤其是长上下文与图像解析）非常值得尝试，代表了国内多模态模型开源的最高水准之一。
- **prism-ml/Ternary-Bonsai-27B-gguf**：如果你对在低配 GPU 或 Mac 上跑 27B 大模型感兴趣，这个模型代表了当前量化技术的天花板。理解它的“三值化”原理，对于研究模型压缩有极大启发。
- **microsoft/Fara1.5-27B**：这是微软在“Agent + 计算机视觉”方向的重要开源尝试。结合目前的“Computer Use”潮流，研究这个模型如何通过截图来操作电脑界面，将有助于理解下一代通用 AI 助手的形态。

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*