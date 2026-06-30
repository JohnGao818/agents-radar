# Hugging Face 热门模型日报 2026-06-30

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-06-30 02:55 UTC

---

好的，作为AI模型生态分析师，以下是根据您提供的 2026-06-30 数据生成的《Hugging Face 热门模型日报》。

---

### **Hugging Face 热门模型日报 | 2026-06-30**

#### **今日速览**

本周 Hugging Face 生态呈现 **“巨头争霸、百花齐放”** 的态势。**GLM-5.2** 和 **DeepSeek-V4** 两大新系列模型正式亮相并迅速登顶，标志着国产大模型在全球社区的影响力进一步提升。**Qwen 家族**的社区衍生版本（如 Qwen3.6 及各类 Agent 变体）持续火爆，显示了其强大的基座潜力。在图像生成领域，**Krea-2** 系列凭借 Turbo 和 Raw 变体高调进入社区视野。此外，模型优化与社区微调活动异常活跃，NVIDIA 和 Unsloth 等团队在量化（NVFP4, GGUF）方面的贡献支撑了大规模模型的本地化部署趋势。

---

#### **热门模型**

##### 🧠 语言模型（LLM、对话模型、指令微调）

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** | 作者: zai-org | 👍 2,947 | ⬇️ 133,350
  GLM 系列最新版本，采用 MoE 架构，以强大的对话和推理能力成为本周榜单冠军，势头强劲。
- **[deepreinforce-ai/Ornith-1.0-35B-GGUF](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B-GGUF)** | 作者: deepreinforce-ai | 👍 483 | ⬇️ 123,598
  基于 Qwen3.5 MoE 架构的 35B 模型量化版，主打高效的推理性能，下载量极高。
- **[Qwen/Qwen-AgentWorld-35B-A3B](https://huggingface.co/Qwen/Qwen-AgentWorld-35B-A3B)** | 作者: Qwen | 👍 438 | ⬇️ 26,223
  Qwen 官方推出的 Agent 专用世界模型，探索将 LLM 用于构建虚拟环境交互，代表了前沿研究方向。
- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M)** | 作者: empero-ai | 👍 561 | ⬇️ 79,540
  基于 Qwen3.5 的社区微调版本，融合了“Claude 神话”系列风格，具备图像理解能力，是社区创意微调的典型案例。
- **[deepseek-ai/DeepSeek-V4-Pro-DSpark](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-DSpark)** | 作者: deepseek-ai | 👍 217 | ⬇️ 5,460
  DeepSeek 新一代 V4 模型的 Pro 版本，附带研究论文，是开源社区追赶前沿闭源模型的重要力量。
- **[deepseek-ai/DeepSeek-V4-Flash-DSpark](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-DSpark)** | 作者: deepseek-ai | 👍 95 | ⬇️ 2,239
  DeepSeek-V4 的快速推理精简版，与 Pro 版形成高低搭配，扩大生态覆盖。
- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** | 作者: HauhauCS | 👍 2,333 | ⬇️ 3,089,944
  Qwen3.6 的社区“无审查”激进风格变体，多模态且下载量惊人，反映了社区对模型“去限制化”的强烈需求。
- **[WeiboAI/VibeThinker-3B](https://huggingface.co/WeiboAI/VibeThinker-3B)** | 作者: WeiboAI | 👍 750 | ⬇️ 63,449
  专注于数学推理的 3B 小模型，以小博大，在特定领域展示了远超大小的能力。
- **[Chunjiang-Intelligence/DeepSeek-v4-Fable](https://huggingface.co/Chunjiang-Intelligence/DeepSeek-v4-Fable)** | 作者: Chunjiang-Intelligence | 👍 130 | ⬇️ 1,463
  基于 DeepSeek-v4 的网络安全专用变体，指向了行业垂直化微调的趋势。
- **[nvidia/Qwen3.6-35B-A3B-NVFP4](https://huggingface.co/nvidia/Qwen3.6-35B-A3B-NVFP4)** | 作者: nvidia | 👍 378 | ⬇️ 5,392,518
  NVIDIA 对 Qwen3.6 系列进行 NVFP4 量化后的版本，下载量巨大，是GPU厂商推动大模型部署的关键一环。
- **[unsloth/Qwen-AgentWorld-35B-A3B-GGUF](https://huggingface.co/unsloth/Qwen-AgentWorld-35B-A3B-GGUF)** | 作者: unsloth | 👍 114 | ⬇️ 116,693
  Unsloth 对 Qwen Agent 模型的 GGUF 量化版，进一步降低了前沿 Agent 模型的部署门槛。

##### 🎨 多模态与生成（图像、视频、音频、文本到X）

- **[krea/Krea-2-Turbo](https://huggingface.co/krea/Krea-2-Turbo)** | 作者: krea | 👍 394 | ⬇️ 38,454
  Krea 图像生成模型的 Turbo 版本，在速度和效率上进行了优化，代表了文生图领域的社区新势力。
- **[krea/Krea-2-Raw](https://huggingface.co/krea/Krea-2-Raw)** | 作者: krea | 👍 245 | ⬇️ 27,464
  Krea-2 的基础版本，为社区提供了底层模型，方便进行风格化微调。
- **[Comfy-Org/Krea-2](https://huggingface.co/Comfy-Org/Krea-2)** | 作者: Comfy-Org | 👍 190 | ⬇️ 10
  ComfyUI 工作流平台官方引入 Krea-2 模型，表明其在图像生成生态中的重要性。
- **[fal/LTX-2.3-3DREAL-LoRA](https://huggingface.co/fal/LTX-2.3-3DREAL-LoRA)** | 作者: fal | 👍 116 | ⬇️ 0
  用于 LTX 图像转视频模型的 LoRA，专注于生成 3D 真实感效果，代表了视频生成领域的精细化趋势。
- **[ilkerzgi/fal-Krea-2-Style-LoRAs](https://huggingface.co/ilkerzgi/fal-Krea-2-Style-LoRAs)** | 作者: ilkerzgi | 👍 75 | ⬇️ 0
  为 Krea-2 模型创作的风格 LoRA 合集，显示了围绕新基础模型迅速形成的微调生态系统。

##### 🔧 专用模型（代码、数学、医疗、嵌入）

- **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)** | 作者: yuxinlu1 | 👍 2,504 | ⬇️ 561,577
  Google Gemma-4 的社区代码专用微调版，结合了 Composer 技术，在代码生成和推理任务上表现突出。
- **[yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)** | 作者: yuxinlu1 | 👍 849 | ⬇️ 241,409
  同样是 Gemma-4 的社区微调版，但聚焦于 Agent 和终端任务，标志着 LLM 向具身智能和工具使用方向发展。
- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** | 作者: nvidia | 👍 2,483 | ⬇️ 728,320
  NVIDIA 推出的通用目标定位模型，可识别并定位图像中任何物体，是计算机视觉领域的“通才”模型，潜力巨大。
- **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)** | 作者: nvidia | 👍 745 | ⬇️ 76,154
  NVIDIA 推出的流式语音识别模型，专为实时语音交互和边缘设备设计，是语音AI领域的重要进展。

##### 📦 微调与量化（社区微调、GGUF、AWQ）

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** | 作者: empero-ai | 👍 954 | ⬇️ 907,682
  榜单中下载量最高的模型之一，证明了社区对高质量角色扮演/风格微调并量化为GGUF的需求极其旺盛。
- **[unsloth/GLM-5.2-GGUF](https://huggingface.co/unsloth/GLM-5.2-GGUF)** | 作者: unsloth | 👍 466 | ⬇️ 164,180
  Unsloth 团队官方出品，为最新的 GLM-5.2 模型提供了高效率 GGUF 量化版本，极大促进了其本地部署。
- **[nvidia/GLM-5.2-NVFP4](https://huggingface.co/nvidia/GLM-5.2-NVFP4)** | 作者: nvidia | 👍 171 | ⬇️ 81,944
  NVIDIA 为 GLM-5.2 提供的 NVFP4 量化版本，代表了GPU硬件厂商对模型优化的深度参与。
- **[HauhauCS/Gemma4-12B-QAT-Uncensored-HauhauCS-Balanced](https://huggingface.co/HauhauCS/Gemma4-12B-QAT-Uncensored-HauhauCS-Balanced)** | 作者: HauhauCS | 👍 107 | ⬇️ 46,053
  Gemma-4 的 QAT（量化感知训练）+ 无审查社区版，展示了社区如何结合高级量化技术和“去限制”需求。

---

#### **生态信号**

1.  **模型家族新贵崛起**：**GLM-5.2** 和 **DeepSeek-V4** 双雄并立，标志着国产大模型在开源社区已形成强大号召力，正从追赶者转变为引领者。**Gemma-4** 和 **Qwen3.5/3.6** 则构成了高质量基座模型的中坚力量，社区围绕它们的“二次创作”异常繁荣。
2.  **开源权重模型势头正盛**：榜单中绝大多数模型均为开源权重，闭源模型无出现。这表明 Hugging Face 生态的核心驱动力仍是开放的、可被社区自由使用和修改的模型。特别是 DeepSeek-V4 和 GLM-5.2 的论文同步发布，强化了开源研究的透明度。
3.  **量化与微调是部署的“两驾马车”**：GGUF 和 NVFP4 等量化形式几乎成为大模型的标配，下载量普遍远超原始权重。同时，社区微调（如 **HauhauCS** 的“无审查”版、**empero-ai** 的角色扮演版）极其活跃，它们定义了模型的实际使用场景和风格，是生态繁荣的关键。**Unsloth** 和 **NVIDIA** 作为量化工具的提供者，已成为模型分发链条上的关键基础设施。

---

#### **值得探索**

1.  **[[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)]**：这是一个极具潜力的“全能”视觉模型。它能理解任意描述并在图像中定位物体，打破了传统目标检测对固定类别的限制。对于希望构建自定义视觉应用的开发者和研究者来说，这是必须尝试的下一代工具。
2.  **[[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)]**：虽然“无审查”标签值得商榷，但其高达 300 万的下载量是社区需求的真实写照。这个模型是研究 **模型微调边界、安全对齐与用户偏好** 之间博弈的绝佳样本。如果你想探索社区力量如何塑造模型的“性格”，这个模型是典型案例。
3.  **[[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)]**：结合了 Google 的 Gemma-4 基座与社区先进的微调技术（Composer），在代码生成领域表现卓越。对于需要一个高性能、可离线运行的代码助手的研究者或开发者来说，这是一个非常值得尝试的直接替代方案。

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*