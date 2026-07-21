# Hugging Face 热门模型日报 2026-07-21

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-07-21 02:14 UTC

---

好的，作为AI模型生态分析师，这是依据您提供的数据整理的《Hugging Face 热门模型日报》。

---

### **Hugging Face 热门模型日报 | 2026-07-21**

#### **今日速览**

本周Hugging Face生态呈现三大热点：**高性能开源模型的密集发布**与**社区量化热潮**并行。`zai-org` 的 **GLM-5.2** 以绝对优势登顶榜单，预示着MoE架构在生成能力上的新突破。同时，围绕 **Qwen 3.5/3.6** 家族（如`Qwythos-9B`、`Qwen3.6`系列）的社区微调与量化版本形成集群效应，特别是**1-bit/2-bit等极端量化**模型下载量惊人，显示本地化部署需求持续旺盛。此外，**Gemma-4-31B** 下载量突破千万，验证了谷歌在开源多模态领域的统治力。多模态（如图像、视频生成）和专用模型（如OCR、机器人）的碎片化趋势明显，模型生态正从“大而全”向“专而精”演进。

---

#### **热门模型**

##### 🧠 语言模型（LLM、对话模型、指令微调）

- **[GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — `zai-org` | 👍 4,226 | 📥 531,947
  - 采用MoE架构的顶尖语言模型，以压倒性周点赞数证明其在技术社区中的极高关注度。

- **[tencent/Hy3](https://huggingface.co/tencent/Hy3)** — `tencent` | 👍 847 | 📥 13,698
  - 腾讯开源的HyV3系列文本生成模型，作为新晋基础模型受到大量关注，标志着大厂在开源生态中的持续投入。

- **[AngelSlim/Hy3-GGUF](https://huggingface.co/AngelSlim/Hy3-GGUF)** — `AngelSlim` | 👍 149 | 📥 109,749
  - `tencent/Hy3`的量化版本，下载量远超原版，说明社区对可本地部署的高效模型有巨大需求。

- **[GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-Thinking](https://huggingface.co/GnLOLot/MiniCPM5-1B-Claude-Opus-Fable5-Thinking)** — `GnLOLot` | 👍 159 | 📥 5,494
  - 基于MiniCPM5的1B级小模型，融合了“思考”能力，展示了小参数模型在特定场景下的潜力。

##### 🎨 多模态与生成（图像、视频、音频、文本到X）

- **[google/gemma-4-31B-it](https://huggingface.co/google/gemma-4-31B-it)** — `google` | 👍 3,297 | 📥 11,987,240
  - 谷歌最新的多模态指令模型，下载量压倒性第一，是本周最受瞩目的开源视觉语言模型，堪称社区“基础设施”。

- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** — `baidu` | 👍 2,446 | 📥 2,122,848
  - 百度推出的通用OCR模型，凭借超高的下载量和点赞数，证明其在文本识别任务上的强大实力和广泛应用基础。

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** — `empero-ai` | 👍 2,369 | 📥 2,117,323
  - 基于Qwen 3.5的9B级多模态量化版，融合了“推理”与“Claude”风格微调，是社区二次创作的明星产品。

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — `HauhauCS` | 👍 2,937 | 📥 2,007,025
  - Qwen 3.6的35B级别MoE模型，主打“无审查”和“激进”特性，反映了社区对多样化甚至边缘化模型的需求。

- **[Wan-AI/Wan-Dancer-14B](https://huggingface.co/Wan-AI/Wan-Dancer-14B)** — `Wan-AI` | 👍 145 | 📥 2,408
  - 专注于“图像转视频”的生成模型，特别是舞蹈动作生成，展示了AI在垂直视频内容生产领域的进展。

- **[OpenMOSS-Team/MOSS-Transcribe-Diarize](https://huggingface.co/OpenMOSS-Team/MOSS-Transcribe-Diarize)** — `OpenMOSS-Team` | 👍 292 | 📥 87,533
  - 专为音频转写与说话人分离（Diarize）设计的模型，填补了音频处理在开源生态中的重要一环。

##### 🔧 专用模型（代码、数学、医疗、嵌入）

- **[moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)** — `moonshotai` | 👍 1,177 | 📥 713,992
  - 月之暗面推出的K2.5系列代码专项模型，采用压缩技术，是代码生成赛道的强有力竞争者。

- **[nvidia/Nemotron-3-Embed-1B-BF16](https://huggingface.co/nvidia/Nemotron-3-Embed-1B-BF16)** — `nvidia` | 👍 87 | 📥 61,708
  - NVIDIA出品的高效文本嵌入模型（1B参数），在语义相似度与特征提取任务上具备工业级应用价值。

- **[openbmb/MiniCPM-RobotManip](https://huggingface.co/openbmb/MiniCPM-RobotManip)** — `openbmb` | 👍 135 | 📥 0
  - 面向机器人操作任务的视觉-语言-动作（VLA）模型，虽然刚发布下载量为0，但点赞数反映了学术界和工业界对具身智能的浓厚兴趣。

- **[Cactus-Compute/needle](https://huggingface.co/Cactus-Compute/needle)** — `Cactus-Compute` | 👍 292 | 📥 950
  - 基于JAX的功能调用和工具使用专用模型，代表了AI Agent生态中的轻量化、专业化方向。

##### 📦 微调与量化（社区微调、GGUF、AWQ）

- **[prism-ml/Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)** — `prism-ml` | 👍 855 | 📥 338,945
  - 首创“三进制”（Ternary）2-bit量化的27B模型，在模型压缩技术上具有里程碑意义，下载量巨大。

- **[prism-ml/Bonsai-27B-gguf](https://huggingface.co/prism-ml/Bonsai-27B-gguf)** — `prism-ml` | 👍 542 | 📥 1,262,894
  - 另一款极致的“1-bit”量化27B模型，下载量超过百万，证明“极限量化”是社区最关注的效率革新方向。

- **[bottlecapai/ThinkingCap-Qwen3.6-27B](https://huggingface.co/bottlecapai/ThinkingCap-Qwen3.6-27B)** — `bottlecapai` | 👍 482 | 📥 10,647
  - 为Qwen 3.6设计的“思考”增强微调版本，探索在基础模型上注入“慢思考”能力的路径。

- **[DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF)** — `DavidAU` | 👍 157 | 📥 16,719
  - 名字虽长，但明确是Qwen 3.6的极端定制版，结合了多种社区技术和风格，是社区“模型拼装”文化的体现。

---

#### **生态信号**

- **Qwen家族势头正旺**：榜单中超过5个模型（Qwythos、Qwen3.6系列）直接或间接基于阿里Qwen模型家族，其强大的基础能力使其成为社区二次创作的首选底座，生态地位稳固。
- **极致量化成为主旋律**：`prism-ml`的1-bit/2-bit模型与`tencent/Hy3`等大模型的GGUF版本下载量极高，显示出模型部署正从“能用”向“在个人设备上流畅运行”转变，效率优先是硬道理。
- **开源权重模型与闭源的博弈加剧**：`google/gemma-4`和`GLM-5.2`等顶级开源权重的发布持续缩小与闭源模型的差距。同时，社区通过微调（如Uncensored版本）来探索开源模型的边界。
- **微调活动精细化**：社区不再满足于通用微调，而是出现了“思考”、“激进”、“Heretic”等特定风格与能力的精细化微调版本，标志着模型个性化定制进入了新阶段。

---

#### **值得探索**

1.  **[google/gemma-4-31B-it](https://huggingface.co/google/gemma-4-31B-it)**：作为本周的现象级模型，其下载量体现了广泛的应用基础。强烈推荐用于研究多模态理解、指令遵循和对话生成，是当前最佳的开源基线之一。
2.  **[prism-ml/Bonsai-27B-gguf](https://huggingface.co/prism-ml/Bonsai-27B-gguf)**：如果你对本地部署和大模型效率感兴趣，这个“1-bit”模型是必读和研究对象。它挑战了数据量化极限，为在消费级硬件上运行大模型提供了全新可能性。
3.  **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)**：尽管下载量不是最高，但其惊人的点赞数反映了它在技术圈内的认可度。作为MoE架构的最新代表，它值得深入分析其在训练和推理上的创新点，是理解下一代LLM架构的重要窗口。

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*