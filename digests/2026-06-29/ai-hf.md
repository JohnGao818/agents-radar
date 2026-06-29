# Hugging Face 热门模型日报 2026-06-29

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-06-29 03:31 UTC

---

好的，作为AI模型生态分析师，这是根据您提供的2026年6月29日数据整理的《Hugging Face 热门模型日报》。

---

### Hugging Face 热门模型日报 | 2026-06-29

#### 今日速览

本周Hugging Face生态呈现“多模态”与“量化部署”双轮驱动的强劲势头。NVIDIA凭借 **LocateAnything-3B** 和一系列NVFP4量化版模型，展示了其在视觉+语言理解与高效推理上的全面领先。国产模型家族**GLM-5.2** 与**DeepSeek-V4**表现亮眼，多个版本（原版、量化版、微调版）同时冲入榜单，社区参与度极高。值得注意的是，**HauhauCS** 的 **Qwen3.6-35B** 量化无审查版以惊人的324万周下载量，证明了社区对高性能、可本地部署大模型的旺盛需求。此外，**Krea-2** 作为唯一上榜的文本生图模型，标志着图像生成领域的持续活跃。

---

#### 热门模型

##### 🧠 语言模型（LLM、对话模型、指令微调）

- **GLM-5.2** | [链接](https://huggingface.co/zai-org/GLM-5.2)
  - `zai-org` | 点赞: 2,831 | 下载: 118,651
  - 智谱新一代MoE大模型，凭借强大的综合对话能力成为本周最受关注的语言模型之一。
- **Ornith-1.0-35B-GGUF** | [链接](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B-GGUF)
  - `deepreinforce-ai` | 点赞: 419 | 下载: 79,630
  - 基于Qwen3.5的35B MoE变体，经过强化学习微调，其量化版本兼顾了性能与部署便利性。
- **Qwen-AgentWorld-35B-A3B** | [链接](https://huggingface.co/Qwen/Qwen-AgentWorld-35B-A3B)
  - `Qwen` | 点赞: 402 | 下载: 23,697
  - 通义千问官方推出的Agent专用模型，专为工具调用和世界模型推理场景优化。
- **VibeThinker-3B** | [链接](https://huggingface.co/WeiboAI/VibeThinker-3B)
  - `WeiboAI` | 点赞: 743 | 下载: 59,337
  - 微博AI出品，专注数学推理的3B小参数模型，以小博大的推理能力引起社区关注。
- **Ornith-1.0-9B-GGUF** | [链接](https://huggingface.co/deepreinforce-ai/Ornith-1.0-9B-GGUF)
  - `deepreinforce-ai` | 点赞: 278 | 下载: 36,846
  - Ornith系列的9B量化版，为资源有限的环境提供更高效的部署选择。
- **DeepSeek-V4-Pro-DSpark** | [链接](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-DSpark)
  - `deepseek-ai` | 点赞: 185 | 下载: 373
  - DeepSeek-V4旗舰版，采用DSpark推理加速架构，代表了开源大模型的最新前沿技术。
- **Ornith-1.0-397B** | [链接](https://huggingface.co/deepreinforce-ai/Ornith-1.0-397B)
  - `deepreinforce-ai` | 点赞: 148 | 下载: 1,116
  - 当前榜单中参数规模最大的模型之一，展示了MoE架构在超大模型上的潜力。
- **LFM2.5-230M** | [链接](https://huggingface.co/LiquidAI/LFM2.5-230M)
  - `LiquidAI` | 点赞: 141 | 下载: 12,384
  - 液态AI出品，基于新型液体神经网络架构的小参数模型，主打高效与动态推理。
- **FastContext-1.0-4B-SFT** | [链接](https://huggingface.co/microsoft/FastContext-1.0-4B-SFT)
  - `microsoft` | 点赞: 369 | 下载: 6,779
  - 微软推出的超长上下文模型，以4B参数实现强大的长序列处理能力，SFT版本实用性更强。

##### 🎨 多模态与生成（图像、视频、音频、文本到X）

- **Unlimited-OCR** | [链接](https://huggingface.co/baidu/Unlimited-OCR)
  - `baidu` | 点赞: 1,248 | 下载: 295,064
  - 百度开源的通用OCR大模型，支持图片到文字的端到端识别，下载量极高，需求巨大。
- **Qwythos-9B-Claude-Mythos-5-1M** | [链接](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M)
  - `empero-ai` | 点赞: 526 | 下载: 52,492
  - 融合了Qwen3.5与Claude-Mythos风格的多模态模型，社区微调产物，极具创意。
- **LocateAnything-3B** | [链接](https://huggingface.co/nvidia/LocateAnything-3B)
  - `nvidia` | 点赞: 2,437 | 下载: 646,451
  - NVIDIA出品，3B参数即可实现强大的图像定位与任意目标检测，是本周多模态领域的明星模型。
- **Krea-2-Turbo** | [链接](https://huggingface.co/krea/Krea-2-Turbo)
  - `krea` | 点赞: 358 | 下载: 27,631
  - Krea公司推出的新一代文本到图像模型Turbo版本，在速度与质量上取得平衡。
- **nemotron-3.5-asr-streaming-0.6b** | [链接](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)
  - `nvidia` | 点赞: 734 | 下载: 67,419
  - NVIDIA Nemo框架下的流式语音识别模型，600M参数实现了高精度实时转录。
- **LTX-2.3-3DREAL-LoRA** | [链接](https://huggingface.co/fal/LTX-2.3-3DREAL-LoRA)
  - `fal` | 点赞: 97 | 下载: 0
  - 面向LTX视频生成模型的LoRA插件，专注于提升生成视频的真实感和三维动感。

##### 🔧 专用模型（代码、数学、医疗、嵌入）

- **Gemma-4-12B-Coder-Fable** | [链接](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)
  - `yuxinlu1` | 点赞: 2,477 | 下载: 549,926
  - 在Google Gemma-4基础上微调的代码与推理增强模型，其GGUF版本广受开发者欢迎。
- **FastContext-1.0-4B-SFT** | [链接](https://huggingface.co/microsoft/FastContext-1.0-4B-SFT)
  - `microsoft` | 点赞: 369 | 下载: 6,779
  - (此模型兼具LLM与专用模型特性，此处强调其“超长上下文”与“Explorer SubAgent”的Agent专用属性)
- **DeepSeek-v4-Fable** | [链接](https://huggingface.co/Chunjiang-Intelligence/DeepSeek-v4-Fable)
  - `Chunjiang-Intelligence` | 点赞: 124 | 下载: 1,409
  - 基于DeepSeek-V4的网络安全专用模型，通过“寓言”式微调，提升了安全场景下的推理能力。

##### 📦 微调与量化（社区微调、GGUF、AWQ）

- **HauhauCS/Qwen3.6-35B-Uncensored** | [链接](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)
  - `HauhauCS` | 点赞: 2,302 | 下载: 3,248,724
  - **本周下载量之王**，在Qwen3.6基础上进行的社区量化与无审查微调，极具争议性但需求极高。
- **Gemma-4-12B-Agentic-Fable** | [链接](https://yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)
  - `yuxinlu1` | 点赞: 801 | 下载: 225,822
  - 另一个社区微调版，将Gemma-4的能力向Agent与终端操作方向引导，验证了Gemma-4的巨大微调空间。
- **GLM-5.2-GGUF** | [链接](https://huggingface.co/unsloth/GLM-5.2-GGUF)
  - `unsloth` | 点赞: 444 | 下载: 146,023
  - unsloth团队对GLM-5.2进行的高质量GGUF量化版本，是社区部署GLM-5.2的首选方案之一。
- **nvidia/Qwen3.6-35B-A3B-NVFP4** | [链接](https://huggingface.co/nvidia/Qwen3.6-35B-A3B-NVFP4)
  - `nvidia` | 点赞: 371 | 下载: 5,235,413
  - ***本周下载量亚军**，NVIDIA官方对Qwen3.6进行NVFP4量化，在N卡上实现极致推理效率。
- **Qwythos-9B-Claude-Mythos-5-1M-GGUF** | [链接](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)
  - `empero-ai` | 点赞: 809 | 下载: 831,529
  - 前述多模态对话模型的GGUF版本，高下载量表明社区对可本地运行的多模态模型有强烈偏好。
- **Gemma4-12B-QAT-Uncensored** | [链接](https://huggingface.co/HauhauCS/Gemma4-12B-QAT-Uncensored-HauhauCS-Balanced)
  - `HauhauCS` | 点赞: 101 | 下载: 40,820
  - 另一个社区微调/量化版本的Gemma-4，采用“平衡”与“无审查”策略，继续延续Gemma-4的微调热潮。
- **Ornith-1.0-9B** | [链接](https://huggingface.co/deepreinforce-ai/Ornith-1.0-9B)
  - `deepreinforce-ai` | 点赞: 237 | 下载: 5,814
  - Ornith系列的原始非量化版本，为开发者提供了进行二次训练或研究的基础。
- **Qwen-AgentWorld-35B-A3B-GGUF** | [链接](https://huggingface.co/unsloth/Qwen-AgentWorld-35B-A3B-GGUF)
  - `unsloth` | 点赞: 96 | 下载: 79,503
  - Qwen官方Agent模型的unsolth量化版，推动了Agent模型在个人设备上的部署。

---

#### 生态信号

1. **“两大阵营”势头强劲：** 目前生态中最受关注的两个模型家族是**智谱的GLM-5.2**（含多个变体）和**阿里的Qwen3.X**（包含Ornith、Qwen3.6等衍生版），两者均形成了从原生权重到多种量化版本的完整生态链。NVIDIA的**Gemma-4**衍生模型也形成了一股不可忽视的力量，尤其在代码与Agent领域。**DeepSeek-V4**作为技术前沿的代表，虽然下载量不高，但关注度与学术影响力在显著上升。

2. **开源权重主导，量化版本为王：** 榜单中所有模型均为开源权重。**GGUF**和**NVFP4**两种量化格式几乎平分秋色，分别代表了社区（CPU/Apple Silicon/低端显卡）和企业级N卡用户的部署需求。社区微调（尤其是“无审查”和“特定风格”）、量化和Agent化是当前最活跃的三大社区活动。

3. **视觉理解与多模态是最大增量：** 本周不仅有**Krea-2**这样的高质量文生图模型，更有**LocateAnything**、**Unlimited-OCR**等将视觉理解推向实用化的模型，下载量都很高。这表明行业正从单纯的“生成”转向更深层的“理解+定位+交互”，多模态模型的下一个杀手级应用可能就在这其中。

---

#### 值得探索

1. **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*