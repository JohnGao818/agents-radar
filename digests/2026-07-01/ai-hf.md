# Hugging Face 热门模型日报 2026-07-01

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-07-01 03:26 UTC

---

好的，作为AI模型生态分析师，以下是基于2026年7月1日Hugging Face榜单生成的日报。

---

### 《Hugging Face 热门模型日报》—— 2026年7月1日

#### 今日速览

本周Hugging Face社区异常活跃，**GLM-5.2系列**以压倒性点赞数登顶，展现了强大的社区号召力。**DeepSeek V4**新系列（Pro/Flash/DSpark）正式发布，标志着MoE推理架构的又一次进化。同时，以**yuxinlu1**和**empero-ai**为代表的社区微调与量化活动极其活跃，围绕**Gemma 4**、**Qwen 3.5/3.6**以及**Ornith**等模型产出了大量高质量GGUF版本。值得注意的是，**NVIDIA**通过NVFP4量化技术持续输出企业级优化模型，与社区开源量化工具形成互补。

#### 热门模型

##### 🧠 语言模型（LLM、对话模型、指令微调）

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)**
  - 作者: zai-org | 点赞: 3,067 | 下载: 142,547
  - 说明：智谱AI的下一代MoE大模型，以超过3000点赞的绝对优势领跑本周榜单，体现了其在中文社区和对话领域的强大影响力。

- **[deepreinforce-ai/Ornith-1.0-35B](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B)**
  - 作者: deepreinforce-ai | 点赞: 267 | 下载: 69,048
  - 说明：基于Qwen 3.5 MoE架构的35B参数级模型，是Ornith系列的核心成员，展示了社区对高质量MoE变体的持续需求。

- **[deepreinforce-ai/Ornith-1.0-9B](https://huggingface.co/deepreinforce-ai/Ornith-1.0-9B)**
  - 作者: deepreinforce-ai | 点赞: 312 | 下载: 26,151
  - 说明：Ornith系列的9B版本，以更小的尺寸提供接近35B的性能，成为资源受限环境下的热门选择。

- **[deepreinforce-ai/Ornith-1.0-397B](https://huggingface.co/deepreinforce-ai/Ornith-1.0-397B)**
  - 作者: deepreinforce-ai | 点赞: 181 | 下载: 2,564
  - 说明：Ornith系列的旗舰级别模型，397B的参数量使其成为追求极致性能的用户的首选，但下载量低表明部署门槛较高。

- **[deepseek-ai/DeepSeek-V4-Pro-DSpark](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-DSpark)**
  - 作者: deepseek-ai | 点赞: 254 | 下载: 6,939
  - 说明：DeepSeek V4系列的Pro版本，采用DSpark推理加速技术，代表了新一代高效能推理模型的趋势。

- **[deepseek-ai/DeepSeek-V4-Flash-DSpark](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-DSpark)**
  - 作者: deepseek-ai | 点赞: 113 | 下载: 4,446
  - 说明：V4系列的Flash版本，进一步优化推理速度，与Pro版本一同构建了高性价比的模型组合。

- **[LiquidAI/LFM2.5-230M](https://huggingface.co/LiquidAI/LiquidAI/LFM2.5-230M)**
  - 作者: LiquidAI | 点赞: 169 | 下载: 17,839
  - 说明：Liquid AI的轻量级模型，以230M参数获得关注，证明小模型在特定任务上的高效潜力依然吸引开发者。

##### 🎨 多模态与生成（图像、视频、音频、文本到X）

- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)**
  - 作者: baidu | 点赞: 1,501 | 下载: 429,056
  - 说明：百度的通用OCR模型，在图像到文本生成任务上表现卓越，高下载量表明其在文档处理等场景的广泛应用。

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)**
  - 作者: empero-ai | 点赞: 1,063 | 下载: 970,663
  - 说明：结合了Qwen 3.5与Claude Mythos风格的多模态模型，其GGUF量化版本下载量极高，是社区对“风格化+量化”组合的强烈需求证明。

- **[krea/Krea-2-Turbo](https://huggingface.co/krea/Krea-2-Turbo)**
  - 作者: krea | 点赞: 423 | 下载: 45,668
  - 说明：Krea推出的图像生成加速版模型，在文生图领域持续保持热度，是专业创作者和爱好者的常用工具。

- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)**
  - 作者: nvidia | 点赞: 2,524 | 下载: 800,597
  - 说明：NVIDIA的图像定位与特征提取模型，以超800K的惊人下载量和2524点赞量成为本周现象级模型，凸显了工业级视觉理解工具的巨大需求。

- **[fal/LTX-2.3-3DREAL-LoRA](https://huggingface.co/fal/LTX-2.3-3DREAL-LoRA)**
  - 作者: fal | 点赞: 128 | 下载: 0
  - 说明：用于图像到视频生成的LoRA模块，专注于3D写实风格，代表了视频生成领域的精细化和专业化趋势。

- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)**
  - 作者: HauhauCS | 点赞: 2,364 | 下载: 3,017,678
  - 说明：基于Qwen 3.6的“无审查”多模态MoE模型，以超过300万的周下载量高居下载榜前列，表明未经审查的开源模型依然拥有巨大的社区市场。

##### 🔧 专用模型（代码、数学、医疗、嵌入）

- **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)**
  - 作者: yuxinlu1 | 点赞: 2,532 | 下载: 575,255
  - 说明：基于Gemma 2B的代码专用模型，结合fable5与composer2.5技术，是本周代码领域最热门的量化模型。

- **[Chunjiang-Intelligence/DeepSeek-v4-Fable](https://huggingface.co/Chunjiang-Intelligence/DeepSeek-v4-Fable)**
  - 作者: Chunjiang-Intelligence | 点赞: 134 | 下载: 1,519
  - 说明：基于DeepSeek V4的网络安全专用模型，代表了大型模型在垂直安全领域的具体应用趋势。

- **[meituan-longcat/LongCat-2.0](https://huggingface.co/meituan-longcat/LongCat-2.0)**
  - 作者: meituan-longcat | 点赞: 106 | 下载: 0
  - 说明：美团的LongCat项目2.0版本，目前信息较少，但引发了社区对美团在基础大模型领域动态的关注。

##### 📦 微调与量化（社区微调、GGUF、AWQ）

- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)**（已在多模态分类中出现，因具有多重属性再此列出）
  - 下载量近百万，是量化模型传播最广的范例。

- **[yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)**
  - 作者: yuxinlu1 | 点赞: 891 | 下载: 257,216
  - 说明：Gemma 4的Agent方向微调量化版，是社区向Agent应用进军的典型代表。

- **[unsloth/GLM-5.2-GGUF](https://huggingface.co/unsloth/GLM-5.2-GGUF)**
  - 作者: unsloth | 点赞: 486 | 下载: 180,394
  - 说明：Unsloth团队对GLM-5.2的GGUF量化版，使用其高效工具链，极大降低了部署门槛。

- **[nvidia/GLM-5.2-NVFP4](https://huggingface.co/nvidia/GLM-5.2-NVFP4)**
  - 作者: nvidia | 点赞: 184 | 下载: 104,746
  - 说明：NVIDIA对GLM-5.2的NVFP4量化版，代表了企业级、高精度量化方案。

- **[nvidia/Qwen3.6-35B-A3B-NVFP4](https://huggingface.co/nvidia/Qwen3.6-35B-A3B-NVFP4)**
  - 作者: nvidia | 点赞: 391 | 下载: 5,495,402
  - 说明：NVIDIA量化版模型的下载量冠军，是Qwen 3.6在NVIDIA优化下的最佳实践，展示了NVFP4技术在高并发场景的成功应用。

- **[huihui-ai/Huihui-GLM-5.2-abliterated-GGUF](https://huggingface.co/huihui-ai/Huihui-GLM-5.2-abliterated-GGUF)**
  - 作者: huihui-ai | 点赞: 102 | 下载: 65
  - 说明：对GLM-5.2进行“abliterated”（移除特定内容限制）处理的社区版本，反映了用户对模型安全边界的持续探索。

#### 生态信号

本周生态呈现三大趋势：**1. 模型家族化竞争白热化**：从**GLM-5.2**到**DeepSeek V4**，再到**Qwen 3.5/3.6**和**Ornith**系列，头部玩家均以多尺寸、多版本（Pro/Flash/Agent）构建完整生态，形成矩阵式竞争。**2. 量化生态高度繁荣**：GGUF与NVIDIA的NVFP4形成双轨。社区方面，**yuxinlu1**、**unsloth**、**empero-ai**等个人/小团队贡献了大量高质量GGUF模型，是开源量化的核心力量；企业方面，NVIDIA则以高精度的NVFP4量化方案占据下载量高位，两者各有千秋。**3. 从“基座”到“特化”**：模型微调方向日益垂直化，如代码（gemma-4-coder）、Agent（gemma-4-agentic）、网络安全（DeepSeek-v4-Fable）和风格化（Qwythos），预示着通用大模型正在向专业领域的快速渗透。

#### 值得探索

1.  **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)**：其高点赞和高下载量验证了工业级视觉理解工具的刚需。如果你的工作涉及图像识别、定位或特征提取，这是一个不可错过的生产力模型。

2.  **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)**：该模型是当前社区代码微调与量化的集大成者。对于希望部署本地代码助手、研究Gemma 4微调技巧的开发者而言，它是极佳的研究与使用样本。

3.  **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)**：以超过300万的周下载量成为下载榜冠军，其“无审查”属性是社区讨论的焦点。如果你对AI安全、模型对齐策略或“未经审查”模型的真实表现感兴趣，这个模型是一个必须研究的极端案例。

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*