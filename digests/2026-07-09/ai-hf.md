# Hugging Face 热门模型日报 2026-07-09

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-07-09 02:35 UTC

---

## 🚀 Hugging Face 热门模型日报（2026-07-09）

---

### 📰 今日速览

- **GLM-5.2** 以周点赞 3,669 的绝对优势登顶本周热榜，这款基于 MoE 的国产对话模型引发社区强烈关注。
- **多模态定位模型** nvidia/LocateAnything-3B 凭借 2,667 赞成为视觉理解赛道黑马，其“指哪看哪”的能力在工业级场景极具潜力。
- **Qwen 3.6 生态持续爆发**：多款基于 Qwen 3.6 的量化版、微调版及视觉版冲入前 30，社区“用 Qwen 改模型”已成主流。
- **DeepSeek-V4 Pro** 正式发布并附带论文（arxiv:2606.19348），同时 unsloth 直出 GGUF 量化版，推理部署链迅速建立。
- **GGUF 量化热潮不减**：周下载量超百万的模型几乎全是 GGUF 格式，边缘部署和本地推理仍是最大驱动力。

---

### 🔥 热门模型分类

#### 🧠 语言模型（LLM、对话、指令微调）

1. **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)**  
   - 作者: zai-org | 点赞: 3,669 | 下载: 281,584  
   - 说明：基于 MoE 架构的对话模型，周点赞数最高，国产大模型在开源社区中的里程碑之作。

2. **[deepseek-ai/DeepSeek-V4-Pro-DSpark](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-DSpark)**  
   - 作者: deepseek-ai | 点赞: 439 | 下载: 15,538  
   - 说明：DeepSeek V4 专业版，配备分布式推理框架 DSpark，已发论文，代表前沿 MoE 路线。

3. **[mistralai/Leanstral-1.5-119B-A6B](https://huggingface.co/mistralai/Leanstral-1.5-119B-A6B)**  
   - 作者: mistralai | 点赞: 167 | 下载: 157  
   - 说明：119B 参数但仅激活 6B 的 MoE 模型，延续 Mistral 高效稀疏路线，标签含 vllm 部署。

4. **[deepreinforce-ai/Ornith-1.0-35B](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B)**  
   - 作者: deepreinforce-ai | 点赞: 366 | 下载: 280,236  
   - 说明：基于 Qwen3.5 MoE 的 35B 稠密+稀疏混合模型，社区微调热度高。

5. **[deepreinforce-ai/Ornith-1.0-9B](https://huggingface.co/deepreinforce-ai/Ornith-1.0-9B)**  
   - 作者: deepreinforce-ai | 点赞: 411 | 下载: 136,037  
   - 说明：同一家族的 9B 版本，支持图像文本多模态输入，兼具性价比。

6. **[poolside/Laguna-XS-2.1](https://huggingface.co/poolside/Laguna-XS-2.1)**  
   - 作者: poolside | 点赞: 79 | 下载: 3,385  
   - 说明：专注于代码生成的 Laguan 家族小模型，轻量开源。

7. **[AliesTaha/fable-traces](https://huggingface.co/AliesTaha/fable-traces)**  
   - 作者: AliesTaha | 点赞: 187 | 下载: 3,886  
   - 说明：基于 Qwen3 的指令微调模型，标签含“instruct”，适合对话和写作。

8. **[meituan-longcat/LongCat-2.0](https://huggingface.co/meituan-longcat/LongCat-2.0)**  
   - 作者: meituan-longcat | 点赞: 152 | 下载: 385  
   - 说明：美团发布的长上下文对话模型，安全 tensor 格式，企业级应用示例。

9. **[froggeric/Qwen-Fixed-Chat-Templates](https://huggingface.co/froggeric/Qwen-Fixed-Chat-Templates)**  
   - 作者: froggeric | 点赞: 783 | 下载: 0  
   - 说明：修复 Qwen 系列对话模板的工具模型（mlx/jinja），实用性强，下载量为 0 但点赞多说明关注度高。

---

#### 🎨 多模态与生成（图像、视频、音频、文本到X）

1. **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)**  
   - 作者: nvidia | 点赞: 2,667 | 下载: 1,424,958  
   - 说明：NVIDIA 推出的视觉定位模型，输入图像+文本可精确定位区域，周点赞第二。

2. **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)**  
   - 作者: baidu | 点赞: 1,874 | 下载: 1,084,945  
   - 说明：百度开源的通用 OCR 大模型，支持任意文字识别，下载量超百万。

3. **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M)**  
   - 作者: empero-ai | 点赞: 737 | 下载: 152,516  
   - 说明：基于 Qwen3.5 的视觉语言模型，经 Claude 数据微调，推理能力突出。

4. **[InternScience/Agents-A1](https://huggingface.co/InternScience/Agents-A1)**  
   - 作者: InternScience | 点赞: 400 | 下载: 14,723  
   - 说明：基于 Qwen3.5 MoE 的智能体模型，支持视觉理解与工具调用。

5. **[bottlecapai/ThinkingCap-Qwen3.6-27B](https://huggingface.co/bottlecapai/ThinkingCap-Qwen3.6-27B)**  
   - 作者: bottlecapai | 点赞: 143 | 下载: 46  
   - 说明：专为视觉推理优化的 Qwen3.6-27B，标签含“image-text-to-text”，适合复杂多模态任务。

6. **[krea/Krea-2-Turbo](https://huggingface.co/krea/Krea-2-Turbo)**  
   - 作者: krea | 点赞: 555 | 下载: 123,729  
   - 说明：Krea 第二代文本到图像扩散模型的加速版本，支持快速生成。

7. **[eric-venti-seeds/Sun-Direction-Lora-Flux2Klein9B](https://huggingface.co/eric-venti-seeds/Sun-Direction-Lora-Flux2Klein9B)**  
   - 作者: eric-venti-seeds | 点赞: 107 | 下载: 0  
   - 说明：用于 Flux2Klein 模型的 LoRA，控制图像中的光照方向，社区创作用。

8. **[conradlocke/krea2-identity-edit](https://huggingface.co/conradlocke/krea2-identity-edit)**  
   - 作者: conradlocke | 点赞: 100 | 下载: 0  
   - 说明：基于 Krea-2 的 LoRA，实现人物身份保持的图像编辑，ComfyUI 可加载。

9. **[Patil/Krea-2-depth-controlnet](https://huggingface.co/Patil/Krea-2-depth-controlnet)**  
   - 作者: Patil | 点赞: 73 | 下载: 0  
   - 说明：为 Krea-2 适配的深度 ControlNet，支持深度引导生成。

---

#### 🔧 专用模型（代码、数学、医疗、嵌入、表格）

1. **[google/tabfm-1.0.0-pytorch](https://huggingface.co/google/tabfm-1.0.0-pytorch)**  
   - 作者: google | 点赞: 314 | 下载: 9,458  
   - 说明：Google 开源的表格基础模型，支持零样本分类与回归，企业数据科学利器。

2. **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)**  
   - 作者: yuxinlu1 | 点赞: 2,653 | 下载: 674,977  
   - 说明：基于 Gemma-4-12B 的代码专用微调版，嵌入 fable5 合成数据，推理能力强。

3. **[yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)**  
   - 作者: yuxinlu1 | 点赞: 1,099 | 下载: 384,383  
   - 说明：同一作者的智能体版本，增强终端交互能力，适合 Agent 场景。

---

#### 📦 微调与量化（社区微调、GGUF、AWQ）

1. **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)**  
   - 作者: empero-ai | 点赞: 1,858 | 下载: 1,683,711  
   - 说明：Qwythos-9B 的 GGUF 量化版，周下载量突破 168 万，本地推理首选。

2. **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)**  
   - 作者: HauhauCS | 点赞: 2,574 | 下载: 2,823,988  
   - 说明：Qwen3.6-35B 的激进无审查微调+GGUF 量化版，周下载量近 300 万，社区争议与热度并存。

3. **[deepreinforce-ai/Ornith-1.0-35B-GGUF](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B-GGUF)**  
   - 作者: deepreinforce-ai | 点赞: 802 | 下载: 502,663  
   - 说明：Ornith-1.0-35B 的 GGUF 量化版，MIT 许可，适合商用部署。

4. **[deepreinforce-ai/Ornith-1.0-9B-GGUF](https://huggingface.co/deepreinforce-ai/Ornith-1.0-9B-GGUF)**  
   - 作者: deepreinforce-ai | 点赞: 462 | 下载: 454,944  
   - 说明：Ornith-1.0-9B 的 GGUF 量化版，同样 MIT 许可，轻量化部署佳选。

5. **[unsloth/Qwen3.6-27B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)**  
   - 作者: unsloth | 点赞: 1,013 | 下载: 2,842,118  
   - 说明：Unsloth 推出的 Qwen3.6-27B 多任务预测版本 GGUF，下载量超 280 万，推理加速明显。

6. **[unsloth/DeepSeek-V4-Flash-GGUF](https://huggingface.co/unsloth/DeepSeek-V4-Flash-GGUF)**  
   - 作者: unsloth | 点赞: 97 | 下载: 47  
   - 说明：DeepSeek-V4 的 Flash 量化版，配合原模型论文发布，但下载量尚低。

7. **[InternScience/Agents-A1-Q4_K_M-GGUF](https://huggingface.co/InternScience/Agents-A1-Q4_K_M-GGUF)**  
   - 作者: InternScience | 点赞: 85 | 下载: 11,226  
   - 说明：Agents-A1 的 Q4_K_M 量化版，兼顾视觉与工具调用能力。

8. **[tencent/Hy3](https://huggingface.co/tencent/Hy3)**  
   - 作者: tencent | 点赞: 565 | 下载: 121  
   - 说明：腾讯混元 V3 的文本生成模型，标签含“

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*