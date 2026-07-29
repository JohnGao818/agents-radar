# Hugging Face 热门模型日报 2026-07-29

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-07-29 02:10 UTC

---

# Hugging Face 热门模型日报 | 2026-07-29

## 今日速览

本周最大亮点是 **月之暗面（moonshotai）** 发布的 **Kimi-K3** 以 8,035 点赞强势登顶，成为单周最受关注的多模态模型。**百度** 的 **Unlimited-OCR** 凭借 3420 点赞与 269 万次下载紧随其后，彰显 OCR 场景的刚需热度。**阿里通义 Qwen3.6 系列** 持续爆发，其 35B MoE 基座（Qwen3.6-35B-A3B）下载量突破 615 万，且衍生出大量 uncensored 量化变体，社区微调生态极为活跃。此外，**微软** 的 **Mage-Flow** 系列（文生图/编辑）和 **poolside** 的 **Laguna-S-2.1**（代码生成）也进入前列，多模态与代码生成成为本周两大核心赛道。

---

## 热门模型

### 🧠 语言模型（LLM、对话模型、指令微调）

| 模型 | 作者 | 点赞 | 下载 | 一句话说明 |
|------|------|------|------|------------|
| [**poolside/Laguna-S-2.1**](https://huggingface.co/poolside/Laguna-S-2.1) | poolside | 801 | 67,286 | 面向代码与推理的 2.1 版本语言模型，支持长上下文生成 |
| [**upstage/Solar-Open2-250B**](https://huggingface.co/upstage/Solar-Open2-250B) | upstage | 646 | 4,804 | 250B 参数开源语言模型，专注高效推理与指令跟随 |
| [**Nanbeige/Nanbeige4.2-3B**](https://huggingface.co/Nanbeige/Nanbeige4.2-3B) | Nanbeige | 529 | 18,933 | 3B 轻量级中文 LLM，适合资源受限场景 |
| [**zai-org/GLM-5.2**](https://huggingface.co/zai-org/GLM-5.2) | zai-org | 4,607 | 1,267,198 | 智谱 GLM 系列最新 MoE 架构对话模型，周点赞排名第十却下载超百万 |
| [**fdtn-ai/antares-1b**](https://huggingface.co/fdtn-ai/antares-1b) | fdtn-ai | 222 | 7,666 | 1B 参数安全领域专用 LLM，采用 Granite MoE 混合架构 |

### 🎨 多模态与生成（图文理解、图像生成、语音合成）

| 模型 | 作者 | 点赞 | 下载 | 一句话说明 |
|------|------|------|------|------------|
| [**moonshotai/Kimi-K3**](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | **8,035** | 99,214 | 月之暗面最新多模态模型，图文理解与压缩特征提取，本周冠军 |
| [**baidu/Unlimited-OCR**](https://huggingface.co/baidu/Unlimited-OCR) | baidu | 3,420 | **2,694,935** | 百度开源通用 OCR 模型，不限场景文字识别，下载量全场最高 |
| [**DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF**](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 854 | 736,692 | 基于 Qwen3.6 的 uncensored 多模态版，压缩至 GGUF 格式 |
| [**thinkingmachines/Inkling**](https://huggingface.co/thinkingmachines/Inkling) | thinkingmachines | 1,626 | 39,052 | 多模态对话模型，采用 Inkling MM 架构，长对话表现优异 |
| [**microsoft/Mage-Flow**](https://huggingface.co/microsoft/Mage-Flow) | microsoft | 418 | 2,007 | 微软最新扩散模型，文生图与图像编辑一体化 |
| [**microsoft/Mage-Flow-Edit-Turbo**](https://huggingface.co/microsoft/Mage-Flow-Edit-Turbo) | microsoft | 109 | 1,260 | Mage-Flow 的快速编辑版本，支持基于指令的图像修改 |
| [**owensong/Inflect-Micro-v2**](https://huggingface.co/owensong/Inflect-Micro-v2) | owensong | 266 | 645 | 超轻量文本转语音模型，可在 CPU 和边缘设备上运行 |
| [**owensong/Inflect-Nano-v2**](https://huggingface.co/owensong/Inflect-Nano-v2) | owensong | 104 | 434 | Nano 级别 TTS，专为本地低功耗场景设计 |
| [**ATH-MaaS/OvisOCR2**](https://huggingface.co/ATH-MaaS/OvisOCR2) | ATH-MaaS | 340 | 47,129 | 基于 Qwen3.5 的 OCR 模型，多语言文本识别 |
| [**Qwen/Qwen3.6-35B-A3B**](https://huggingface.co/Qwen/Qwen3.6-35B-A3B) | Qwen | 2,570 | **6,158,876** | 阿里最新 MoE 多模态模型，35B 参数但仅激活 3B，下载量突破 600 万 |
| [**empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF**](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF) | empero-ai | 2,502 | 1,262,662 | 基于 Qwen3.5 的推理增强模型，GGUF 量化版 |
| [**microsoft/Fara1.5-27B**](https://huggingface.co/microsoft/Fara1.5-27B) | microsoft | 179 | 1,543 | 多模态计算机操控助手，可理解屏幕并执行操作 |
| [**baseten/GLM-5.2-Vision-NVFP4**](https://huggingface.co/baseten/GLM-5.2-Vision-NVFP4) | baseten | 131 | 2,756 | GLM-5.2 视觉版，采用 NVFP4 量化，高效多模态推理 |
| [**moonshotai/Kimi-K2.7-Code**](https://huggingface.co/moonshotai/Kimi-K2.7-Code) | moonshotai | 1,332 | 681,111 | Kimi 代码专用版，压缩特征提取，面向代码理解与生成 |

### 🔧 专用模型（代码、数学、图像编辑、安全）

| 模型 | 作者 | 点赞 | 下载 | 一句话说明 |
|------|------|------|------|------------|
| [**Kwaipilot/KAT-Coder-V2.5-Dev**](https://huggingface.co/Kwaipilot/KAT-Coder-V2.5-Dev) | Kwaipilot | 289 | 6,275 | 基于 Qwen3.5 MoE 的代码生成模型，支持多模态代码理解 |
| [**conradlocke/krea2-identity-edit**](https://huggingface.co/conradlocke/krea2-identity-edit) | conradlocke | 565 | 0 | ComfyUI 专属 LoRA，用于 Krea-2 模型的身份保持图像编辑 |

### 📦 微调与量化（GGUF、社区微调、各种变体）

| 模型 | 作者 | 点赞 | 下载 | 一句话说明 |
|------|------|------|------|------------|
| [**unsloth/Laguna-S-2.1-GGUF**](https://huggingface.co/unsloth/Laguna-S-2.1-GGUF) | unsloth | 232 | 129,601 | Laguna-S-2.1 的 GGUF 量化版，由 unsloth 提供，兼容 vLLM |
| [**prism-ml/Ternary-Bonsai-27B-gguf**](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf) | prism-ml | 1,085 | 665,427 | 2-bit 三进制量化 27B 模型，极低资源下保留对话能力 |
| [**prism-ml/Bonsai-27B-gguf**](https://huggingface.co/prism-ml/Bonsai-27B-gguf) | prism-ml | 680 | 2,339,098 | 1-bit 量化 27B 模型，极致压缩，下载量超 233 万 |
| [**HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive**](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive) | HauhauCS | 3,159 | 1,855,505 | Qwen3.6-35B 的无审查激进微调版，GGUF 格式 |
| [**LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V6-GGUF**](https://huggingface.co/LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V6-GGUF) | LuffyTheFox | 198 | 99,660 | 另一款 Qwen3.6 无审查量化版，融合 Heremes 指令风格 |
| [**poolside/Laguna-S-2.1-GGUF**](https://huggingface.co/poolside/Laguna-S-2.1-GGUF) | poolside | 160 | 90,106 | 官方提供的 Laguna-S-2.1 GGUF 版本，兼容 endpoints |
| [**unsloth/Kimi-K3**](https://huggingface.co/unsloth/Kimi-K3) | unsloth | 148 | 410 | Kimi-K3 的 unsloth 优化版，保留压缩特征提取能力 |
| [**unsloth/Kimi-K3-GGUF**](https://huggingface.co/unsloth/Kimi-K3-GGUF) | unsloth | 90 | 0 | Kimi-K3 的 GGUF 量化版，面向本地推理 |
| [**poolside/Laguna-S-2.1-NVFP4**](https://huggingface.co/poolside/Laguna-S-2.1-NVFP4) | poolside | 153 | 180,545 | Laguna-S-2.1 的 NVIDIA FP4 量化版，专为 vLLM 优化 |

---

## 生态信号

**1. 模型家族势头正旺：**  
- **Kimi 系列**（K3 / K2.7-Code）以最大单体点赞数（8,035）证明月之暗面在多模态与代码方向的领先地位。  
- **Qwen3.6-35B-A3B** 基座下载突破 600 万，MoE 激活 3B 参数的设计使其成为社区微调首选，衍生出大量 uncensored 与量化版本。  
- **GLM-5.2** 系列（含视觉版）下载超 126 万，展现智谱开源生态的持续吸引力。  
- **Laguna-S-2.1** 与 **Mage-Flow** 分别代表代码生成与图像生成两大垂直方向。

**2. 开源 vs 闭源：**  
本周榜单 30 个模型全部为开源权重或量化版，无一闭源 API 模型。社区对可本地部署、可微调的“开放权重”模型需求强烈。百度、微软、月之暗面、阿里等大厂均贡献了旗舰级权重，开源阵营持续壮大。

**3. 量化与微调活动

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*