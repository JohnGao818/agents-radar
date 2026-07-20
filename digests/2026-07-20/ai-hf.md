# Hugging Face 热门模型日报 2026-07-20

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-07-20 02:35 UTC

---

好的，作为AI模型生态分析师，以下是根据您提供的2026-07-20数据生成的《Hugging Face 热门模型日报》。

---

### **Hugging Face 热门模型日报 | 2026-07-20**

#### **今日速览**

本周 Hugging Face 生态呈现出明显的小型化与专业化趋势。GLM-5.2 凭借新一代 MoE-DSA 架构和强大的多模态能力问鼎榜首，成为社区新宠。同时，**量化模型**（尤其是GGUF格式）占据了排行榜的半壁江山，其中 `prism-ml` 团队专注于 **1-bit 和三元量化** 的Bonsai-27B系列下载量惊人，反映出社区对低成本、高效率推理的极致追求。值得注意的是，以 **“思考”或“推理”** 为标签的模型（如 `Qwythos-9B` 系列）持续火热，表明模型内在推理能力仍是核心竞争点。此外，国产模型阵营强势崛起，百度、腾讯、智谱AI及月之暗面均有明星产品上榜。

---

#### **热门模型**

##### 🧠 **语言模型（LLM、对话模型、指令微调）**

*   **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** - 作者: zai-org | 点赞: 4,170 | 下载: 536k
    *   **一句话说明**: 智谱AI新一代旗舰模型，采用 MoE-DSA（动态稀疏注意力）架构，在对话和多模态任务上表现卓越，凭借权威背景和硬核技术登顶本周趋势榜首。

*   **[tencent/Hy3](https://huggingface.co/tencent/Hy3)** - 作者: tencent | 点赞: 835 | 下载: 13k
    *   **一句话说明**: 腾讯混元系列的第三代模型 `Hy3`，作为国产大厂的新一代语言模型，其基础权重发布受到社区高度关注，标志着腾讯在开源LLM领域的持续投入。

*   **[moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)** - 作者: moonshotai | 点赞: 1,158 | 下载: 749k
    *   **一句话说明**: 月之暗面推出的Kimi系列最新代码专用模型，以压缩张量技术实现高效推理，在代码生成和特性提取方面表现突出，深受开发者欢迎。

##### 🎨 **多模态与生成（图像、视频、音频、文本到X）**

*   **[thinkingmachines/Inkling](https://huggingface.co/thinkingmachines/Inkling)** - 作者: thinkingmachines | 点赞: 1,153 | 下载: 13k
    *   **一句话说明**: 最新的多模态MoE模型，能够处理图文、音频等多种输入，代表了前沿的全能型多模态大模型方向，是新晋的焦点模型。

*   **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** - 作者: empero-ai | 点赞: 2,347 | 下载: 2.1M
    *   **一句话说明**: 基于Qwen3.5的9B推理模型变体，为长上下文（1M）任务优化，下载量超过200万，是社区热门的“小参数、强推理”选择。

*   **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** - 作者: baidu | 点赞: 2,194 | 下载: 2.1M
    *   **一句话说明**: 百度推出的全能OCR模型，突破传统OCR限制，广泛应用于各类文字识别场景，其海量下载证明了顶级实用性需求。

*   **[Wan-AI/Wan-Dancer-14B](https://huggingface.co/Wan-AI/Wan-Dancer-14B)** - 作者: Wan-AI | 点赞: 128 | 下载: 2k
    *   **一句话说明**: 图像到视频生成的专用模型，专注于将静态图像转化为动态舞蹈视频，代表了AI视频生成在垂直领域的精细化探索。

##### 🔧 **专用模型（代码、数学、医疗、嵌入）**

*   **[InternScience/Agents-A1](https://huggingface.co/InternScience/Agents-A1)** - 作者: InternScience | 点赞: 584 | 下载: 35k
    *   **一句话说明**: 上海AI实验室推出的Agent专用模型，基于Qwen3.5 MoE，专门优化了工具调用和自主代理任务，是AI Agent生态的基石模型。

*   **[Cactus-Compute/needle](https://huggingface.co/Cactus-Compute/needle)** - 作者: Cactus-Compute | 点赞: 279 | 下载: 955
    *   **一句话说明**: 一个专注于功能调用和工具使用的新兴JAX模型，代表了轻量级、高性能函数式AI Agent的发展方向。

*   **[froggeric/Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates)** - 作者: froggeric | 点赞: 947 | 下载: 0
    *   **一句话说明**: 一个非模型权重，而是提供修正后的Qwen模型聊天模板（Jinja），完美解决了社区模型格式不兼容问题，是开发者的实用工具。

##### 📦 **微调与量化（社区微调、GGUF、AWQ）**

*   **[prism-ml/Bonsai-27B-gguf](https://huggingface.co/prism-ml/Bonsai-27B-gguf)** - 作者: prism-ml | 点赞: 499 | 下载: 1.2M
    *   **一句话说明**: **本周下载之王**，将27B模型压缩到极致1-bit GGUF格式，大幅降低部署门槛，是社区追求“极限性价比”的典型代表。

*   **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** - 作者: HauhauCS | 点赞: 2,901 | 下载: 2.0M
    *   **一句话说明**: 基于Qwen3.6的35B MoE模型（A3B激活参数），并去除了审查限制，定制化程度高且推理快，满足部分社区对“无限制”模型的需求。

*   **[prism-ml/Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)** - 作者: prism-ml | 点赞: 794 | 下载: 338k
    *   **一句话说明**: Bonsai-27B的2-bit三元量化版本，在1-bit与原始精度之间取得了微妙的平衡，是Bonsai家族中兼具性能与效率的热门选择。

---

#### **生态信号**

本周生态呈现出 **“双轨并行”** 的清晰信号：

1.  **模型家族强势内卷**：以 **智谱GLM-5.2**、**腾讯Hy3**、**月之暗面Kimi** 和 **阿里系的Qwen3.5/3.6** 为代表的国产模型家族竞争白热化，各家均有重量级模型登场，争夺社区话语权。
2.  **开源权重深度“压榨”**：大量活动集中在模型量化和微调上。`prism-ml` 的 **Bonsai-27B** 系列引领了**1-bit和三元量化**的革命，证明了即使旗舰模型发布后，社区通过极端的量化技术（GGUF/MLX）延长其生命周期并普及化的力量。`empero-ai` 的Qwythos系列则体现了“基座模型 + 推理增强 + 极致量化”的成熟社区MO。
3.  **闭源壁垒被开源生态**瓦解：几乎所有上榜的国产大模型都选择开源权重，并提供社区商用友好的许可（如Apache-2.0、自定义开放许可）。这表明，对于B端应用和社区影响力而言，**开源权重而非仅公开API，已成为建立信任和生态护城河的关键**。

---

#### **值得探索**

1.  **thinkingmachines/Inkling** - **理由**：作为最新的多模态MoE模型，它代表了模型架构从单一任务走向全能感知的进化方向。探索其在不同模态（图像、文本、音频）间的交互逻辑，对理解下一代通用人工智能架构非常有启发。

2.  **prism-ml/Ternary-Bonsai-27B-gguf** - **理由**：这是目前量化技术的“天花板”实验。研究一个27B模型如何通过1-bit或2-bit量化还能保持有用性，对于在边缘设备（手机、笔记本）上部署大模型具有革命性意义。这不仅是模型，更是一项关键的基础设施技术。

3.  **google/gemma-4-31B-it** - **理由**：虽然点赞数位居第二，但下载量（1,237万）是其他所有模型的数倍。它是Google最强大的开源多模态模型，性能对标Gemini级产品。基础研究和技术验证的首选标杆，值得深度研究和评测。

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*