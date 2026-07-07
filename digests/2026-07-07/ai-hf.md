# Hugging Face 热门模型日报 2026-07-07

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-07-07 02:42 UTC

---

# Hugging Face 热门模型日报 ｜ 2026-07-07

## 📰 今日速览

本周 Hugging Face 社区热度持续攀升，**Qwen 3.5/3.6 系列** 仍然是绝对主角，多个微调版和量化版霸榜，下载量突破百万。智谱 **GLM-5.2** 以 3,535 点赞拿下周冠军，MoE 架构和多模态能力备受关注。NVIDIA 推出的 **LocateAnything-3B** 定位于通用定位任务，刚发布即获 2,635 赞。社区微调活动异常活跃，`Ornith`、`Qwythos`、`Gemma-4-Coder` 等衍生模型纷纷涌现，GGUF 量化格式几乎成为本地部署标配。此外，百度 **Unlimited-OCR** 下载量已超百万，专业OCR能力被广泛采用。

---

## 🔥 热门模型

### 🧠 语言模型（LLM / 对话 / 指令微调）

| 模型 | 作者 | 点赞 | 下载 | 一句话说明 |
|------|------|------|------|------------|
| [zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2) | zai-org | 3,535 | 231,218 | 智谱最新 MoE 对话模型，GLM 系列的重大升级，凭借强大多轮对话能力登顶本周点赞榜。 |
| [tencent/Hy3](https://huggingface.co/tencent/Hy3) | tencent | 342 | 2 | 腾讯 Hunyuan 系列第三代文本生成模型（Hy v3），主打高效推理，刚刚发布，下载量较低但关注度高。 |
| [deepseek-ai/DeepSeek-V4-Pro-DSpark](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-DSpark) | deepseek-ai | 409 | 14,276 | DeepSeek V4 Pro 版本，引入“DSpark”优化技术，支持更长上下文，受到学术界和工业界关注。 |
| [AliesTaha/fable-traces](https://huggingface.co/AliesTaha/fable-traces) | AliesTaha | 177 | 2,903 | 基于 Qwen3 的指令微调模型，专注于“fable”风格生成，适合创意写作。 |
| [mistralai/Leanstral-1.5-119B-A6B](https://huggingface.co/mistralai/Leanstral-1.5-119B-A6B) | mistralai | 143 | 106 | Mistral AI 推出的 119B 参数 MoE 模型（6B 激活），主打高效训练和推理，Apache-2.0 开源。 |
| [deepreinforce-ai/Ornith-1.0-35B](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B) | deepreinforce-ai | 351 | 231,342 | 基于 Qwen3.5 MoE 的 35B 全参版本，社区微调产物，兼顾通用对话与多模态理解。 |
| [deepreinforce-ai/Ornith-1.0-9B](https://huggingface.co/deepreinforce-ai/Ornith-1.0-9B) | deepreinforce-ai | 393 | 86,136 | Ornith 系列 9B 版本，轻量级但性能均衡，适合资源受限场景。 |
| [meituan-longcat/LongCat-2.0](https://huggingface.co/meituan-longcat/LongCat-2.0) | meituan-longcat | 117 | 43 | 美团发布的长文本对话模型，面向超长上下文应用（如文档问答），尚在早期。 |
| [Qwen/Qwen-AgentWorld-35B-A3B](https://huggingface.co/Qwen/Qwen-AgentWorld-35B-A3B) | Qwen | 556 | 57,835 | 阿里 Qwen 官方推出的 Agent 专用模型，35B MoE，专为工具调用和智能体场景优化。 |

### 🎨 多模态与生成（图像、视频、音频、文本到X）

| 模型 | 作者 | 点赞 | 下载 | 一句话说明 |
|------|------|------|------|------------|
| [empero-ai/Qwythos-9B-Claude-Mythos-5-1M](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M) | empero-ai | 702 | 149,421 | 基于 Qwen3.5 的视觉语言模型，融合 Claude 风格 Mythos 数据，擅长图像理解与描述。 |
| [baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR) | baidu | 1,797 | 1,070,230 | 百度发布的通用 OCR 模型，支持多语言、多场景文字识别，下载量已破百万。 |
| [InternScience/Agents-A1](https://huggingface.co/InternScience/Agents-A1) | InternScience | 345 | 8,766 | 结合 Qwen3.5 MoE 的多模态智能体模型，支持图像输入与任务规划，适合 agent 应用。 |
| [nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B) | nvidia | 2,635 | 1,340,559 | NVIDIA 推出的通用目标定位模型，可通过自然语言描述在图像中定位任意物体，准确度高。 |
| [krea/Krea-2-Turbo](https://huggingface.co/krea/Krea-2-Turbo) | krea | 529 | 109,470 | 基于 Krea-2-Raw 的 Turbo 版本，Diffusers 架构，快速生成高质量图像，适合创意设计。 |
| [eric-venti-seeds/Sun-Direction-Lora-Flux2Klein9B](https://huggingface.co/eric-venti-seeds/Sun-Direction-Lora-Flux2Klein9B) | eric-venti-seeds | 80 | 0 | 用于 Flux2Klein 模型的 LoRA，专门控制光照方向（太阳角度），极客向图像编辑工具。 |

### 🔧 专用模型（代码、数学、医疗、嵌入、表格、工具）

| 模型 | 作者 | 点赞 | 下载 | 一句话说明 |
|------|------|------|------|------------|
| [google/tabfm-1.0.0-pytorch](https://huggingface.co/google/tabfm-1.0.0-pytorch) | google | 257 | 7,036 | Google 发布的表格分类/回归基础模型，零样本即可处理结构化数据，工业应用潜力大。 |
| [yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF) | yuxinlu1 | 2,623 | 664,319 | 基于 Gemma-4 的代码生成模型，高度优化推理能力，在编程任务上广受好评。 |
| [yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF) | yuxinlu1 | 1,052 | 370,884 | 同一作者的另一 Gemma-4 衍生版，强化了 agentic 和终端交互能力。 |
| [nationaldesignstudio/rampart](https://huggingface.co/nationaldesignstudio/rampart) | nationaldesignstudio | 136 | 3,821 | 基于 BERT 的 PII 识别模型，支持 ONNX 和 Transformers.js，适用于隐私保护场景。 |
| [nvidia/Nemotron-Labs-TwoTower-30B-A3B-Base-BF16](https://huggingface.co/nvidia/Nemotron-Labs-TwoTower-30B-A3B-Base-BF16) | nvidia | 126 | 10,766 | NVIDIA 双塔架构 LLM 基础版，30B MoE，专门用于检索增强生成（RAG）中的双编码。 |
| [froggeric/Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates) | froggeric | 699 | 0 | 修复 Qwen 3.5 聊天模板的工具，解决 Jinja 兼容性问题，对 MLX 用户尤其实用。 |

### 📦 微调与量化（社区微调、GGUF、AWQ）

| 模型 | 作者 | 点赞 | 下载 | 一句话说明 |
|------|------|------|------|------------|
| [empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF) | empero-ai | 1,644 | 1,617,508 | Qwythos-9B 的 GGUF 量化版，专为 llama.cpp 设计，下载超 160 万，本地部署首选。 |
| [deepreinforce-ai/Ornith-1.0-35B-GGUF](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B-GGUF) | deepreinforce-ai | 759 | 436,780 | Ornith 35B 的量化版本，兼顾大模型效果与 CPU/边缘推理效率。 |
| [deepreinforce-ai/Ornith-1.0-9B-GGUF](https://huggingface.co/deepreinforce-ai/Ornith-1.0-9B-GGUF) | deep

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*