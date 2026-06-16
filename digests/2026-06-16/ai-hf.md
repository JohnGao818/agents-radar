# Hugging Face 热门模型日报 2026-06-16

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-06-16 03:40 UTC

---

好的，作为AI模型生态分析师，根据您提供的2026年6月16日Hugging Face Hub热门模型数据，我为您生成了今日的模型生态日报。

---

### **Hugging Face 热门模型日报 (2026-06-16)**

#### **今日速览**

今日榜单呈现“巨头领跑，社区紧跟”的态势。**DeepSeek** 以 **DeepSeek-V4-Pro** 的绝对优势登顶，成为当日最瞩目的模型发布。多模态及专用模型成为热点，尤其是代码生成与视觉定位方向。值得关注的是，**社区量化与微调活动异常活跃**，以 **Unsloth** 为代表的团队对热门基座模型（如Gemma 4、Kimi K2.7）进行了大量的GGUF格式适配，极大推动了模型的本地化部署。同时，**无审查（Uncensored）** 和 **聚合型** 模型也获得了大量关注，展现了社区对模型自由度的强烈需求。

#### **热门模型**

##### 🧠 **语言模型（LLM、对话模型、指令微调）**
- **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)**
  - 作者: deepseek-ai | 点赞: 4,868 | 下载: 2,934,763
  - 一句话说明：DeepSeek最新旗舰模型，以绝对优势登顶本周热榜，展示了其强大的推理与对话能力，是今日最重磅的发布。
- **[google/gemma-4-12B](https://huggingface.co/google/gemma-4-12B)**
  - 作者: google | 点赞: 551 | 下载: 250,498
  - 一句话说明：Google Gemma 4家族的12B参数基座版本，凭借其强大的通用性能（any-to-any）和开源权重，成为社区研究和微调的热门基底。

##### 🎨 **多模态与生成（图像、视频、音频、文本到X）**
- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)**
  - 作者: nvidia | 点赞: 2,059 | 下载: 86,968
  - 一句话说明：NVIDIA推出的“万物定位”模型，聚焦于图像中的目标定位与特征提取，代表了视觉理解模型的垂直化趋势。
- **[google/diffusiongemma-26B-A4B-it](https://huggingface.co/google/diffusiongemma-26B-A4B-it)**
  - 作者: google | 点赞: 886 | 下载: 311,788
  - 一句话说明：Google的混合扩散与语言模型，拥有26B总参数（4B活跃），在图像理解与多轮对话任务上表现突出。
- **[MiniMaxAI/MiniMax-M3](https://huggingface.co/MiniMaxAI/MiniMax-M3)**
  - 作者: MiniMaxAI | 点赞: 851 | 下载: 14,312
  - 一句话说明：MiniMax发布的多模态大模型，专注图像-文本处理，社区下载量预示其应用潜力正在被快速挖掘。
- **[ideogram-ai/ideogram-4-fp8](https://huggingface.co/ideogram-ai/ideogram-4-fp8)**
  - 作者: ideogram-ai | 点赞: 548 | 下载: 10,748
  - 一句话说明：顶尖文生图模型Ideogram 4的FP8量化版，在保持高质量生成的同时降低了推理门槛，推动了高质量图像生成模型的普及。
- **[bosonai/higgs-audio-v3-tts-4b](https://huggingface.co/bosonai/higgs-audio-v3-tts-4b)**
  - 作者: bosonai | 点赞: 445 | 下载: 38,429
  - 一句话说明：4B参数的文本转语音模型，凭借其高质量的自然语音生成能力，代表了多模态中音频生成方向的进步。
- **[Zyphra/ZONOS2](https://huggingface.co/Zyphra/ZONOS2)**
  - 作者: Zyphra | 点赞: 90 | 下载: 414
  - 一句话说明：新一代文本转语音模型，Apache 2.0许可，因其开源和高性能在TTS领域备关注。

##### 🔧 **专用模型（代码、数学、医疗、嵌入）**
- **[moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)**
  - 作者: moonshotai | 点赞: 750 | 下载: 56,750
  - 一句话说明：月之暗面旗下的代码专用模型，代表了Kimi系列在垂直领域的深化，压缩张量技术也降低了部署成本。
- **[CohereLabs/North-Mini-Code-1.0](https://huggingface.co/CohereLabs/North-Mini-Code-1.0)**
  - 作者: CohereLabs | 点赞: 391 | 下载: 11,145
  - 一句话说明：Cohere出品的轻量级代码模型（MoE架构），专注于代码生成与对话，体现了“小而专”的模型研发思路。
- **[microsoft/FastContext-1.0-4B-SFT](https://huggingface.co/microsoft/FastContext-1.0-4B-SFT)**
  - 作者: microsoft | 点赞: 107 | 下载: 13
  - 一句话说明：微软推出的“快速上下文”模型，旨在优化长文本处理效率，是探索长上下文推理的前沿实验性模型。

##### 📦 **微调与量化（社区微调、GGUF、AWQ）**
- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)**
  - 作者: HauhauCS | 点赞: 1,858 | 下载: 2,697,882
  - 一句话说明：基于Qwen3.6的MoE模型进行社区无审查微调的版本，下载量极高，反映了社区对“去限制化”模型的强烈偏好。
- **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)**
  - 作者: yuxinlu1 | 点赞: 663 | 下载: 20,207
  - 一句话说明：社区对Gemma 4模型进行代码能力增强，并转换为GGUF格式的典范，展示了社区结合量化与功能微调的流行路径。
- **[DavidAU/Qwen3.6-40B-Claude-4.6-Opus-Deckard-Heretic-Uncensored-Thinking-NEO-CODE-Di-IMatrix-MAX-GGUF](https://huggingface.co/DavidAU/Qwen3.6-40B-Claude-4.6-Opus-Deckard-Heretic-Uncensored-Thinking-NEO-CODE-Di-IMatrix-MAX-GGUF)**
  - 作者: DavidAU | 点赞: 359 | 下载: 369,526
  - 一句话说明：社区“缝合”与“极致微调”的代表作品，融合多种模型特性并进行无审查训练，其超长文件名和极高下载量极具话题性。
- **[unsloth/gemma-4-12b-it-GGUF](https://huggingface.co/unsloth/gemma-4-12b-it-GGUF)**
  - 作者: unsloth | 点赞: 618 | 下载: 980,781
  - 一句话说明：Unsloth推出的Gemma 4指令微调版GGUF模型，凭借其高效的量化技术，成为社区本地部署首选。

#### **生态信号**

- **多模态与代码是双主轴**：榜单显示，多模态模型（图像-文本）和代码专用模型占据了半壁江山，表明AI能力正从单一模态向融合、从通用向专用工具化快速演进。
- **开源权重生态繁荣，DeepSeek与Google引领风潮**：DeepSeek V4的开放权重和Gemma 4家族的完整开源，极大激发了社区活力。这证明了高质量开源模型对推动整个生态创新的关键作用。
- **量化活动空前活跃**：以 **GGUF** 格式为代表的量化模型下载量巨大，特别是 **Unsloth** 作为桥梁，几乎对每一个重要的新模型都提供了量化版本。这表明用户端对“在本地流畅运行高性能模型”的需求远未饱和，是生态中不可或缺的一环。
- **“定制化”与“无审查”成为社区热点**：以 **HauhauCS** 和 **DavidAU** 为代表的模型，通过融合或修改基座模型来创造“自己版本”的模型，并去除内容限制，这种“社区自制模型”的流行度正快速上升。

#### **值得探索**

1.  **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)**：作为今日榜首，它代表了当前开源大模型的最高水平之一。无论你是想研究最前沿的Transformer架构、评估模型的推理能力，还是寻找一个强大的基座进行二次开发，这个模型都是必读项。

2.  **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)**：这个模型把AI的视觉能力推向了一个新高度——从“识别是什么”到“定位在哪儿”。对于机器人、自动驾驶、以及需要精细图像理解的应用场景，它提供了一种高效的解决方案，值得深入测试其泛化能力。

3.  **[Zyphra/ZONOS2](https://huggingface.co/Zyphra/ZONOS2)**：在视频和图像模型大热的背景下，音频模型是一个被低估的蓝海。ZONOS2以Apache 2.0开源，提供了高质量TTS能力，对于那些希望构建实时语音助手、有声书或无障碍工具的研发者来说，这是一个不可多得的优质选择。

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*