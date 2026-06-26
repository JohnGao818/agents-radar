# Hugging Face 热门模型日报 2026-06-26

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-06-26 02:56 UTC

---

好的，作为 AI 模型生态分析师，以下是为你生成的《Hugging Face 热门模型日报》。

---

### Hugging Face 热门模型日报 | 2026-06-26

#### 📰 今日速览

本周 Hugging Face 生态迎来重磅更新：**DeepSeek 发布了 V4-Pro**，以 5062 赞的绝对热度登顶，标志着开源 MoE 大模型竞争进入新阶段。**Z-AI 的 GLM-5.2** 同样表现强势，展示了 MoE-DSA 架构的吸引力。在应用层面，**多模态融合成为标配**，Google Gemma-4 和 MiniMax-M3 等模型均支持文本、图像及“any-to-any”任务。此外，**社区微调和量化活动空前活跃**，以 HauhauCS 为代表的开发者围绕 Qwen、Gemma 系列推出了大量 Uncensored 及 QAT 版本，推动了模型的极致部署和定制化。

---

#### 🏆 热门模型

##### 🧠 语言模型（LLM、对话模型、指令微调）

- **deepseek-ai/DeepSeek-V4-Pro** (HF: [链接](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro))
   作者: deepseek-ai | 👍: 5,062 | 📥: 1,878,217
   **说明**: 本周最重磅模型，DeepSeek 第四代的专业版，在推理、对话和长上下文能力上大幅提升，树立了开源模型新标杆。
- **zai-org/GLM-5.2** (HF: [链接](https://huggingface.co/zai-org/GLM-5.2))
   作者: zai-org | 👍: 2,483 | 📥: 67,107
   **说明**: 智谱AI的最新 MoE-DSA 架构模型，在保持强大性能的同时实现了高效的稀疏激活，热度极高。
- **google/gemma-4-12B-it** (HF: [链接](https://huggingface.co/google/gemma-4-12B-it))
   作者: google | 👍: 1,178 | 📥: 2,187,644
   **说明**: Google 的旗舰多模态基础模型，除了对话能力，还支持 any-to-any 任务，下载量巨大，生态应用广泛。
- **yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF** (HF: [链接](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF))
   作者: yuxinlu1 | 👍: 2,367 | 📥: 495,813
   **说明**: 社区对 Gemma-4 的代码能力进行了极致的微调和量化打包，成为下载量最高的 GGUF 版本之一。
- **yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF** (HF: [链接](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF))
   作者: yuxinlu1 | 👍: 619 | 📥: 165,187
   **说明**: 专注于 Agent 场景的 Gemma-4 微调版，强调终端交互与工具调用能力，为 AI Agent 生态提供模型基础。
- **WeiboAI/VibeThinker-3B** (HF: [链接](https://huggingface.co/WeiboAI/VibeThinker-3B))
   作者: WeiboAI | 👍: 715 | 📥: 51,717
   **说明**: 基于 Qwen2 的轻量级数学与推理模型，以 3B 参数在特定任务上表现出色，适合资源受限场景。
- **Qwen/Qwen-AgentWorld-35B-A3B** (HF: [链接](https://huggingface.co/Qwen/Qwen-AgentWorld-35B-A3B))
   作者: Qwen | 👍: 246 | 📥: 3,389
   **说明**: Qwen 官方专为 Agent 设计的 MoE 模型，总参数量 35B 但激活仅 3B，体现了 MoE 在 Agent 领域的应用潜力。
- **moonshotai/Kimi-K2.7-Code** (HF: [链接](https://huggingface.co/moonshotai/Kimi-K2.7-Code))
   作者: moonshotai | 👍: 992 | 📥: 502,106
   **说明**: 月之暗面发布的代码增强版多模态模型，在视觉代码理解场景有特殊优化，下载量极高。
- **HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive** (HF: [链接](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive))
   作者: HauhauCS | 👍: 2,238 | 📥: 3,520,206
   **说明**: 社区对 Qwen 3.6 MoE 模型进行了“去审查”和“激进”风格微调，下载量惊人，反映了社区对开放性的强烈需求。

##### 🎨 多模态与生成（图像、视频、音频、文本到X）

- **MiniMaxAI/MiniMax-M3** (HF: [链接](https://huggingface.co/MiniMaxAI/MiniMax-M3))
   作者: MiniMaxAI | 👍: 1,241 | 📥: 154,350
   **说明**: MiniMax 的第三代旗舰多模态模型，在图文理解与生成任务上表现突出，在榜单上占据重要位置。
- **krea/Krea-2-Turbo** (HF: [链接](https://huggingface.co/krea/Krea-2-Turbo))
   作者: krea | 👍: 245 | 📥: 2,996
   **说明**: Krea 的新一代图像生成模型，基于其 Raw 模型蒸馏的 Turbo 版，主打快速、高质量生成。
- **nvidia/LocateAnything-3B** (HF: [链接](https://huggingface.co/nvidia/LocateAnything-3B))
   作者: nvidia | 👍: 2,365 | 📥: 407,838
   **说明**: Nvidia 推出的通用视觉定位模型，可精准识别并定位图像中的任意物体，是本周强大的专用视觉工具。
- **baidu/Unlimited-OCR** (HF: [链接](https://huggingface.co/baidu/Unlimited-OCR))
   作者: baidu | 👍: 900 | 📥: 70,743
   **说明**: 百度推出的通用 OCR 大模型，支持海量场景下的文字识别，准确率极高，是生产力工具的代表。
- **owensong/Inflect-Nano-v1** (HF: [链接](https://huggingface.co/owensong/Inflect-Nano-v1))
   作者: owensong | 👍: 201 | 📥: 0
   **说明**: 超小型的文本转语音模型，专注于极低资源下的语音合成，为边缘设备 TTS 提供了新可能。

##### 🔧 专用模型（代码、数学、医疗、嵌入）

- **nvidia/nemotron-3.5-asr-streaming-0.6b** (HF: [链接](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b))
   作者: nvidia | 👍: 695 | 📥: 50,553
   **说明**: 面向流式语音识别的专用模型，主打低延迟和缓存感知，适合实时语音交互场景。
- **microsoft/FastContext-1.0-4B-SFT** (HF: [链接](https://huggingface.co/microsoft/FastContext-1.0-4B-SFT))
   作者: microsoft | 👍: 345 | 📥: 5,276
   **说明**: 微软推出的长上下文加速模型，旨在突破 Transformer 的长文本处理瓶颈，技术上具有开创性。
- **datalab-to/lift** (HF: [链接](https://huggingface.co/datalab-to/lift))
   作者: datalab-to | 👍: 152 | 📥: 5,189
   **说明**: 专为 PDF 等文档场景优化的多模态模型，提升了从文档中提取和理解信息的能力。
- **Chunjiang-Intelligence/DeepSeek-v4-Fable** (HF: [链接](https://huggingface.co/Chunjiang-Intelligence/DeepSeek-v4-Fable))
   作者: Chunjiang-Intelligence | 👍: 92 | 📥: 646
   **说明**: 专注于网络安全领域的 DeepSeek-v4 微调版，体现了顶尖大模型在垂直安全场景的落地潜力。

##### 📦 微调与量化（社区微调、GGUF、AWQ）

- **unsloth/GLM-5.2-GGUF** (HF: [链接](https://huggingface.co/unsloth/GLM-5.2-GGUF))
   作者: unsloth | 👍: 387 | 📥: 88,915
   **说明**: 社区知名加速库 Unsloth 出品的 GLM-5.2 量化版，极大降低了本地部署门槛，推动了该模型的普及。
- **nvidia/Qwen3.6-35B-A3B-NVFP4** (HF: [链接](https://huggingface.co/nvidia/Qwen3.6-35B-A3B-NVFP4))
   作者: nvidia | 👍: 342 | 📥: 4,602,255
   **说明**: Nvidia 使用其 ModelOpt 工具对 Qwen 3.6 MoE 进行的 FP4 量化版，在性能损失极小的情况下大幅降低显存需求，下载量破450万。
- **empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF** (HF: [链接](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF))
   作者: empero-ai | 👍: 493 | 📥: 134,294
   **说明**: 社区基于 Qwen3.5 知识对模型进行“风格”微调后的量化版，探索了模型个性化和创意写作方向。
- **huihui-ai/Huihui-gemma-4-12B-coder-fable5-composer2.5-v1-abliterated** (HF: [链接](https://huggingface.co/huihui-ai/Huihui-gemma-4-12B-coder-fable5-composer2.5-v1-abliterated))
   作者: huihui-ai | 👍: 127 | 📥: 4,874
   **说明**: 社区对 Gemma-4 进行的“Abliterated”（去除安全限制的微调）版本，反映了社区对模型输出限制的探索和争议。
- **HauhauCS/Gemma4-12B-QAT-Uncensored-HauhauCS-Balanced** (HF: [链接](https://huggingface.co/HauhauCS/Gemma4-12B-QAT-Uncensored-HauhauCS-Balanced))
   作者: HauhauCS | 👍: 83 | 📥: 15,128
   **说明**: 使用量化感知训练（QAT）对 Gemma-4 进行微调和量化，在保持“去审查”风格的同时优化了量化性能。

---

#### 📈 生态信号

1.  **模型家族势头正旺**：**DeepSeek V4**、**GLM 5**、**Qwen 3.6** 和 **Google Gemma 4** 构成了本周最强四大家族。它们在基础能力上争奇斗艳，并催生了大量针对代码、Agent、数学等垂直领域的二次微调版本。
2.  **开源权重成为主流**：榜单上所有模型均为开放权重，且 DeepSeek-V4-Pro 等模型采用 Apache-2.0 等宽松许可，进一步巩固了开源社区在 AI 创新中的主导地位。闭源模型的影响有所减弱。
3.  **量化与微调极度活跃**：**GGUF** 和 **FP4** 成为最受欢迎的量化格式，尤其是 Nvidia 的 NVFP4 和 Unsloth 的高效工具，显著降低了顶级 MoE 模型的使用门槛。社区微调（Uncensored、Agentic、Coder）的活跃度创下新高，表明用户不再满足于基础模型，强烈追求“开箱即用”的定制化解决方案。

---

#### 🔭 值得探索

1.  **deepseek-ai/DeepSeek

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*