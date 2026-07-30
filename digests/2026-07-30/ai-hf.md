# Hugging Face 热门模型日报 2026-07-30

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-07-30 01:59 UTC

---

好的，作为一名AI模型生态分析师，以下是基于2026年7月30日Hugging Face排行榜数据为您生成的《Hugging Face 热门模型日报》。

---

### **Hugging Face 热门模型日报 | 2026-07-30**

#### **今日速览**

本周Hugging Face榜单由**月之暗面（Moonshot AI）** 的 **Kimi-K3** 模型强势领跑，以超过8600的周点赞数登顶，显示出社区对其强大多模态理解能力的高度期待。与此同时，多模态模型（Image-Text-to-Text）持续成为绝对主流，占据榜单近半壁江山。在开源生态方面，**Qwen3.6、GLM-5.2** 等系列家族派生模型众多，社区微调和量化（特别是GGUF格式）活动极其活跃，体现了硬件友好和可定制化是当前开源模型发展的核心驱动力。值得关注的是，模型量化不断挑战极限，如“1-bit”和“2-bit”的模型也已登上热门榜。

---

#### **热门模型**

##### 🧠 **语言模型（LLM、对话模型、指令微调）**

1.  **[GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** （zai-org, 点赞: 4,644, 下载: 1.27M）
    智谱AI最新一代通用大语言模型，具备强大的对话与推理能力，下载量巨大，是榜单上最受关注的纯文本对话模型之一。
2.  **[poolside/Laguna-S-2.1](https://huggingface.co/poolside/Laguna-S-2.1)** （poolside, 点赞: 827, 下载: 67k）
    专注于软件工程领域的S级模型，在代码生成任务上表现突出，代表了专用垂直领域LLM的探索。
3.  **[upstage/Solar-Open2-250B](https://huggingface.co/upstage/Solar-Open2-250B)** （upstage, 点赞: 696, 下载: 4.8k）
    Upstage推出的250B参数级别超大规模开源模型，代表了当前开源LLM规模的顶尖水平，吸引了对模型能力上限有极致追求的研究者和开发者。

##### 🎨 **多模态与生成（图像、视频、音频、文本到X）**

1.  **[moonshotai/Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3)** （moonshotai, 点赞: 8,662, 下载: 99k）
    本周冠军！月之暗面推出的新一代多模态模型，支持图像与文本输入，在特征提取和理解方面表现卓越，被广泛视为“大模型原生应用”的基石。
2.  **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** （baidu, 点赞: 3,516, 下载: 2.69M）
    百度推出的“无限”OCR模型，因其强大的文字识别能力和极高的下载量，被认为是生产环境中文OCR的标杆模型。
3.  **[Qwen/Qwen3.6-35B-A3B](https://huggingface.co/Qwen/Qwen3.6-35B-A3B)** （Qwen, 点赞: 2,586, 下载: 6.15M）
    通义千问官方发布的MoE（混合专家）多模态模型，以35B总参数、仅3B激活参数实现极致的性价比与效率，是榜单上下载量最高的模型之一。
4.  **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** （empero-ai, 点赞: 2,516, 下载: 1.26M）
    基于Qwen3.5的社区微调模型，结合了“Claude Mythos”的推理风格，经过GGUF量化，是社区风格微调的热门代表。
5.  **[owensong/Inflect-Micro-v2](https://huggingface.co/owensong/Inflect-Micro-v2)** （owensong, 点赞: 290, 下载: 645）
    专为CPU和边缘设备设计的轻量级文本转语音（TTS）模型，代表了将AI能力下沉到终端设备的趋势。

##### 🔧 **专用模型（代码、数学、医疗、嵌入）**

1.  **[Kwaipilot/KAT-Coder-V2.5-Dev](https://huggingface.co/Kwaipilot/KAT-Coder-V2.5-Dev)** （Kwaipilot, 点赞: 317, 下载: 6.2k）
    基于Qwen3.5-MoE架构的专用代码生成模型，针对开发者场景进行了优化，是专业代码模型领域的有力竞争者。
2.  **[microsoft/VibeVoice-ASR-BitNet](https://huggingface.co/microsoft/VibeVoice-ASR-BitNet)** （microsoft, 点赞: 103, 下载: 1.7k）
    微软推出的自动语音识别（ASR）模型，采用了创新的BitNet架构，预示着低比特量化在音频领域的应用前景。

##### 📦 **微调与量化（社区微调、GGUF、AWQ）**

1.  **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-...](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** （HauhauCS, 点赞: 3,171, 下载: 1.85M）
    基于Qwen3.6的原生MoE模型，经过去审查（Uncensored）与极具攻击性风格的微调，在偏好定制化的用户群体中极受欢迎。
2.  **[prism-ml/Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)** （prism-ml, 点赞: 1,095, 下载: 665k）
    挑战极限量化的代表，将27B参数模型压缩至2-bit，使其能在消费级硬件上运行，这是社区对“模型压缩”极致追求的体现。
3.  **[prism-ml/Bonsai-27B-gguf](https://huggingface.co/prism-ml/Bonsai-27B-gguf)** （prism-ml, 点赞: 688, 下载: 2.33M）
    同样是prism-ml的产品，但这是1-bit量化的版本。尽管精度大幅降低，但其运行速度和在极低功耗设备上的潜力使其下载量巨大，反响热烈。
4.  **[DavidAU/Qwen3.6-27B-Fable-Fusion-...-GGUF](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF)** （DavidAU, 点赞: 945, 下载: 736k）
    对基础模型进行大量社区风格微调并转化为GGUF格式的典型代表，展示了社区在定制化模型上的创造力。

---

#### **生态信号**

1.  **多模态为王，Kimi-K3 崛起**：榜单前三名中有两个是多模态模型，且月之暗面的Kimi-K3以绝对优势登顶。这表明市场重心已从纯文本大模型转向能处理图像、视频等多模态信息的全能模型。**Kimi生态正在形成**（包括官方版和社区量化版），是继Qwen后又一强势崛起的模型家族。
2.  **开源权重持续发酵，社区微调高度活跃**：以 **Qwen3.6** 和 **GLM-5.2** 为代表的强大基础模型，催生了大量社区微调版本（包括去审查、角色扮演、特定风格等）。这说明开放权重模式极大地激发了社区创造力，形成了“基础模型+微调模型”的繁荣生态。
3.  **量化“军备竞赛”进入深水区**：1-bit、2-bit模型（如Bonsai系列）和NVFP4等新型量化技术的出现，不仅仅是简单的“模型变小”，更是在移动端、IoT设备上实现复杂推理的关键基础设施。**GGUF格式已成为社区量化的事实标准**，应用于绝大多数本地部署场景。

---

#### **值得探索**

1.  **[moonshotai/Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3)**：作为本周榜一，强烈建议下载体验。它不仅代表了多模态模型的最新进展，其压缩张量技术也值得深入研究。社区版 **[unsloth/Kimi-K3](https://huggingface.co/unsloth/Kimi-K3)** 则提供了高效的微调入口。
2.  **[prism-ml/Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)**：对于有本地化部署需求、追求极致效率的开发者而言，这个2-bit模型是必选项。它让你看到大模型在个人设备上流畅运行的可能性，是探索模型压缩与性能平衡的绝佳样本。
3.  **[owensong/Inflect-Micro-v2](https://huggingface.co/owensong/Inflect-Micro-v2)**：端侧AI是新趋势，这款专为CPU设计的TTS模型是研究边缘智能的绝佳起点。用它可以在低功耗设备上快速搭建语音交互应用，值得所有对端侧AI感兴趣的开发者关注。

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*