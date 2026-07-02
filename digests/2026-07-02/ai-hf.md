# Hugging Face 热门模型日报 2026-07-02

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-07-02 02:52 UTC

---

好的，作为AI模型生态分析师，以下是根据您提供的2026年7月2日数据生成的《Hugging Face热门模型日报》。

---

### **Hugging Face 热门模型日报 | 2026年7月2日**

#### **今日速览**

今日Hugging Face生态呈现“基座模型争霸”与“社区微调狂欢”并存的局面。智源的**GLM-5.2**凭借其MoE架构和高达3,174的周点赞量，成为今日最耀眼的明星，生态热度远超其他模型。同时，以**Ornith-1.0**系列和**Qwythos**系列为代表的Qwen 3.5衍生模型形成集群效应，占据了榜单大量席位。值得注意的是，百度与NVIDIA带来的**多模态模型**（OCR、定位）和**模型优化工具**（NVFP4）下载量极高，反映出模型在“好用”与“易用”上的务实需求。社区对GGUF量化版本的追逐依然狂热，大量微调与量化版本（如Huihui-GLM、Unsloth版本）持续涌现。

#### **热门模型**

##### 🧠 **语言模型（LLM、对话模型、指令微调）**

*   **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — **作者:** zai-org | **点赞:** 3,174 | **下载:** 159,967
    *   **一句话说明:** 智源研究院发布的全新MoE大模型，凭借强大的综合性能成为本周最炙手可热的模型，社区纷纷对其进行二次开发和量化。
*   **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M)** — **作者:** empero-ai | **点赞:** 620 | **下载:** 114,499
    *   **一句话说明:** 基于Qwen 3.5的社区微调模型，融合了“Claude-Mythos”数据集的精炼风格，主打推理能力，在语言模型社区中颇受关注。
*   **[deepseek-ai/DeepSeek-V4-Pro-DSpark](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-DSpark)** — **作者:** deepseek-ai | **点赞:** 278 | **下载:** 7,629
    *   **一句话说明:** DeepSeek V4系列的旗舰级模型，以极强的数学与代码能力著称，即使发布时间略早，依然是顶尖的通用基座模型。
*   **[InternScience/Agents-A1](https://huggingface.co/InternScience/Agents-A1)** — **作者:** InternScience | **点赞:** 140 | **下载:** 511
    *   **一句话说明:** 专为智能体Agent场景设计的MoE模型，基于Qwen 3.5架构优化，代表了模型从“回答问题”向“执行任务”转变的新方向。

##### 🎨 **多模态与生成（图像、视频、音频、文本到X）**

*   **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** — **作者:** baidu | **点赞:** 1,581 | **下载:** 630,246
    *   **一句话说明:** 百度发布的通用OCR模型，无需特定训练即可识别多种场景下的文字，因实用性极强而获得海量下载。
*   **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — **作者:** nvidia | **点赞:** 2,548 | **下载:** 896,058
    *   **一句话说明:** NVIDIA推出的小型视觉定位模型，能以自然语言指令在图像中精准定位任意物体，精确度和效率引发关注。
*   **[krea/Krea-2-Turbo](https://huggingface.co/krea/Krea-2-Turbo)** — **作者:** krea | **点赞:** 439 | **下载:** 56,953
    *   **一句话说明:** 新一代文生图模型Krea-2的加速版，在推理速度和图像质量上取得平衡，是图像生成赛道的有力竞争者。
*   **[fal/LTX-2.3-3DREAL-LoRA](https://huggingface.co/fal/LTX-2.3-3DREAL-LoRA)** — **作者:** fal | **点赞:** 137 | **下载:** 0
    *   **一句话说明:** 针对LTX视频模型开发的LoRA模块，专为生成3D写实风格视频而设计，展示了社区在垂直视频风格化上的探索。

##### 🔧 **专用模型（代码、数学、医疗、嵌入）**

*   **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)** — **作者:** yuxinlu1 | **点赞:** 2,554 | **下载:** 597,090
    *   **一句话说明:** 基于Google Gemma 4的代码专用模型，经过深度微调后代码生成与推理能力极强，其GGUF量化版本深受开发者喜爱。
*   **[BugTraceAI/BugTraceAI-CORE-Ultra-27B-Q6](https://huggingface.co/BugTraceAI/BugTraceAI-CORE-Ultra-27B-Q6)** — **作者:** BugTraceAI | **点赞:** 109 | **下载:** 3,377
    *   **一句话说明:** 专注于网络安全与攻击性安全的专用模型，代表了AI在特定专业领域的精细化应用趋势。

##### 📦 **微调与量化（社区微调、GGUF、AWQ）**

*   **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** — **作者:** empero-ai | **点赞:** 1,163 | **下载:** 1,113,871
    *   **一句话说明:** 同名模型的GGUF量化版，小体积与大参数模型性能的结合，使其下载量突破百万，是本地部署场景的热门选择。
*   **[deepreinforce-ai/Ornith-1.0-35B-GGUF](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B-GGUF)** — **作者:** deepreinforce-ai | **点赞:** 615 | **下载:** 233,701
    *   **一句话说明:** Ornith-1.0系列35B参数模型的量化版本，其出色的性能与高性价比，使其成为社区用户本地体验大模型的标杆之一。
*   **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — **作者:** HauhauCS | **点赞:** 2,379 | **下载:** 3,055,962
    *   **一句话说明:** Qwen 3.6的无审查激进风格微调版，下载量突破300万，反映了社区对内容限制宽松和特定风格的强烈需求。
*   **[unsloth/GLM-5.2-GGUF](https://huggingface.co/unsloth/GLM-5.2-GGUF)** — **作者:** unsloth | **点赞:** 490 | **下载:** 212,201
    *   **一句话说明:** Unsloth为GLM-5.2提供的GGUF量化版本，作为生态知名工具链，其版本往往意味着更高的下载量和兼容性。

#### **生态信号**

本周生态格局清晰：**GLM系列**异军突起，凭借新一代MoE架构力压群雄，形成了围绕基座模型的量化与微调热潮。**Qwen 3.5/3.6**家族则凭借开源生态的深度渗透，衍生出**Ornith、Qwythos**等多个分支，呈现出“基座 + 社区微调”的繁荣景象。在量化方面，**GGUF**格式依然占据绝对统治地位，**NVIDIA的NVFP4**优化方案也开始崭露头角，暗示企业级部署对模型压缩工具链的重视。值得注意的是，**Unlimited-OCR**和**LocateAnything**的成功，表明“小而精”的专用多模态模型具备极高的爆发力，其下载量远超同榜单中的大型语言模型。

#### **值得探索**

1.  **尝试：[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)**
    *   **理由:** 这是一个开箱即用的高效工具。如果你有图文识别需求，它能提供领先的识别精度，而无需准备训练数据和进行繁琐的微调，是真正能提升生产力的“模型即服务”产品。

2.  **关注：[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)**
    *   **理由:** 它在代码领域的量化版本获得了极高点赞，值得研究其微调策略和量化方法。特别是其12B的参数量在本地部署和高效推理间取得了良好平衡。

3.  **深挖：[Qwen/Qwen-AgentWorld-35B-A3B](https://huggingface.co/Qwen/Qwen-AgentWorld-35B-A3B)**
    *   **理由:** Qwen官方出品的“世界模型”，专为智能体设计。它代表了下一代大模型从单纯对话向Agent推理和执行进化的方向，是研究多智能体系统和环境交互的重要基座。

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*