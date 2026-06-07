# Hugging Face 热门模型日报 2026-06-07

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-06-07 03:30 UTC

---

# Hugging Face 热门模型日报（2026-06-07）

## 今日速览

- **DeepSeek-V4 系列强势登顶**：DeepSeek-V4-Pro（周 +4,681 赞）和 DeepSeek-V4-Flash（+1,421 赞）分别占据下载量前两名，总下载量超 890 万，成为本周现象级模型。
- **视频生成赛道爆发**：SulphurAI 的文本到视频模型（+1,581 赞）基于 Lightricks LTX-2.3 微调，下载量超 170 万；NVIDIA Cosmos3 系列（Nano/Super/Text2Image/Image2Video）多款上榜，显示多模态视频能力已成竞争热点。
- **MoE 架构全面渗透**：本周 Top 30 中有 8 个模型采用混合专家架构（MoE），包括 Qwen3.6-35B-A3B 系列、LiquidAI LFM2.5-8B-A1B、NVIDIA Nemotron-3 Ultra 550B-A55B 等，稀疏激活高效推理成为主流选择。
- **量化与社区微调活跃**：Unsloth 为 Gemma-4 提供 GGUF 量化版（+423 赞），NVIDIA 推出 Qwen3.6 和 Nemotron 的 NVFP4 精度版；社区 Unleashed（HauhauCS）的 Uncensored 微调版下载量达 277 万，反映用户对定制化模型的强烈需求。

## 热门模型

### 🧠 语言模型（LLM、对话模型、指令微调）

- **DeepSeek-V4-Pro** ([HF](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro))  
  作者: deepseek-ai | 👍 4,681 | 📥 5,510,611  
  本周最热大语言模型，基于 MoE 架构，在对话和推理任务上表现出色，是社区首选基座模型。

- **DeepSeek-V4-Flash** ([HF](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash))  
  作者: deepseek-ai | 👍 1,421 | 📥 3,436,213  
  DeepSeek-V4 的轻量快速版，兼顾性能与推理速度，适合资源受限场景。

- **JetBrains/Mellum2-12B-A2.5B-Thinking** ([HF](https://huggingface.co/JetBrains/Mellum2-12B-A2.5B-Thinking))  
  作者: JetBrains | 👍 240 | 📥 16,395  
  JetBrains 推出的思考链增强对话模型，专注逻辑推理与代码理解。

- **nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-BF16** ([HF](https://huggingface.co/nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-BF16))  
  作者: nvidia | 👍 145 | 📥 47,285  
  550B 总参数、55B 激活参数的 MoE 巨模型，代表 NVIDIA 在 LLM 领域的最新旗舰。

- **nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-NVFP4** ([HF](https://huggingface.co/nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-NVFP4))  
  作者: nvidia | 👍 119 | 📥 17,225  
  同款模型的 NVFP4 4-bit 量化版，极大降低显存占用。

- **LiquidAI/LFM2.5-8B-A1B** ([HF](https://huggingface.co/LiquidAI/LFM2.5-8B-A1B))  
  作者: LiquidAI | 👍 534 | 📥 95,440  
  8B 总参、1B 激活的 MoE 语言模型，侧重高效推理与可扩展性。

- **openbmb/MiniCPM5-1B** ([HF](https://huggingface.co/openbmb/MiniCPM5-1B))  
  作者: openbmb | 👍 775 | 📥 100,575  
  1B 参数级轻量模型，延续 MiniCPM 家族高性价比路线，适合端侧部署。

### 🎨 多模态与生成（图像、视频、音频、文本到X）

- **nvidia/LocateAnything-3B** ([HF](https://huggingface.co/nvidia/LocateAnything-3B))  
  作者: nvidia | 👍 1,459 | 📥 111,078  
  图像+文本输入任意定位的通用模型，支持语义/实例分割，在视觉问答和指代表达任务中表现亮眼。

- **google/gemma-4-12B-it** ([HF](https://huggingface.co/google/gemma-4-12B-it))  
  作者: google | 👍 621 | 📥 315,131  
  Google 全新多模态模型，支持任意输入任意输出（any-to-any），是 Gemini 的开源对应。

- **unsloth/gemma-4-12b-it-GGUF** ([HF](https://huggingface.co/unsloth/gemma-4-12b-it-GGUF))  
  作者: unsloth | 👍 423 | 📥 458,174  
  Gemma-4 的 GGUF 量化版，由社区 Unsloth 优化，大幅降低本地推理门槛。

- **google/gemma-4-12B** ([HF](https://huggingface.co/google/gemma-4-12B))  
  作者: google | 👍 380 | 📥 84,549  
  Gemma-4 基础版（不含指令微调），适合研究者进行二次开发。

- **HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive** ([HF](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive))  
  作者: HauhauCS | 👍 1,491 | 📥 2,771,843  
  社区基于 Qwen3.6 MoE 的“无审查”激进微调版，下载量极高，反映用户对内容自由的追求。

- **stepfun-ai/Step-3.7-Flash** ([HF](https://huggingface.co/stepfun-ai/Step-3.7-Flash))  
  作者: stepfun-ai | 👍 343 | 📥 38,716  
  中阶视觉语言模型，兼顾图像理解与文本生成，适合多模态对话应用。

- **ideogram-ai/ideogram-4-fp8** ([HF](https://huggingface.co/ideogram-ai/ideogram-4-fp8))  
  作者: ideogram-ai | 👍 311 | 📥 2,818  
  Ideogram 第四代文生图模型，FP8 量化版在精度与速度间取得平衡。

- **ideogram-ai/ideogram-4-nf4** ([HF](https://huggingface.co/ideogram-ai/ideogram-4-nf4))  
  作者: ideogram-ai | 👍 213 | 📥 2,671  
  同模型的 NF4 量化版，进一步降低显存需求。

- **nvidia/Cosmos3-Nano** ([HF](https://huggingface.co/nvidia/Cosmos3-Nano))  
  作者: nvidia | 👍 183 | 📥 24,820  
  NVIDIA Cosmos3 系列轻量版，支持图像/文本到多种模态的生成。

- **nvidia/Cosmos3-Super** ([HF](https://huggingface.co/nvidia/Cosmos3-Super))  
  作者: nvidia | 👍 149 | 📥 20,403  
  Cosmos3 旗舰版，具备更强的多模态理解与生成能力。

- **nvidia/Cosmos3-Super-Text2Image** ([HF](https://huggingface.co/nvidia/Cosmos3-Super-Text2Image))  
  作者: nvidia | 👍 120 | 📥 1,634  
  专为文本到图像设计的 Cosmos3 子模型。

- **nvidia/Cosmos3-Super-Image2Video** ([HF](https://huggingface.co/nvidia/Cosmos3-Super-Image2Video))  
  作者: nvidia | 👍 111 | 📥 1,295  
  图像到视频生成，Cosmos3 的又一创新分支。

- **nvidia/PiD** ([HF](

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*