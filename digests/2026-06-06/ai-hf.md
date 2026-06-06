# Hugging Face 热门模型日报 2026-06-06

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-06-06 02:47 UTC

---

# Hugging Face 热门模型日报  
**日期：2026-06-06**  

---

## 🔥 今日速览  
本周 Hugging Face 榜单被 **DeepSeek-V4-Pro** 以 4,658 点赞断层领跑，下载量突破 556 万，证明开源超大规模 MoE 模型仍是社区焦点。**Sulphur-2-base**（1.5k 赞）和 **NVIDIA Cosmos3** 系列引爆视频生成赛道，多模态模型从“文本 + 图像”向“视频 + 音频”全面扩展。量化与微调生态持续活跃：**unsloth** 和 **HauhauCS** 分别推出 Gemma-4 和 Qwen3.6 的 GGUF 版本，**NVIDIA** 则用 NVFP4 格式将 550B 模型压缩至可部署尺寸。此外，非审查（Uncensored）模型热度攀升，反映出社区对内容自由的强烈需求。

---

## 📊 热门模型分类  

### 🧠 语言模型（LLM、对话、指令微调）  
- **[deepseek-ai/DeepSeek-V4-Pro](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)**  
  *作者*：deepseek-ai | 👍 4,658 | ⬇️ 5,562,821  
  *一句话*：当前最强开源 MoE 对话模型，海量下载证明其商业级泛化能力。  

- **[LiquidAI/LFM2.5-8B-A1B](https://huggingface.co/LiquidAI/LFM2.5-8B-A1B)**  
  *作者*：LiquidAI | 👍 526 | ⬇️ 82,709  
  *一句话*：8B 总参数激活仅 1B 的 MoE 语言模型，平衡效率与性能。  

- **[sapientinc/HRM-Text-1B](https://huggingface.co/sapientinc/HRM-Text-1B)**  
  *作者*：sapientinc | 👍 702 | ⬇️ 159,014  
  *一句话*：面向人力资源场景的 1B 轻量文本生成模型，垂直落地潜力突出。  

- **[JetBrains/Mellum2-12B-A2.5B-Thinking](https://huggingface.co/JetBrains/Mellum2-12B-A2.5B-Thinking)**  
  *作者*：JetBrains | 👍 225 | ⬇️ 14,709  
  *一句话*：JetBrains 推出的推理增强型 MoE 模型，12B 激活 2.5B，代码与逻辑推理出众。  

- **[openbmb/MiniCPM5-1B](https://huggingface.co/openbmb/MiniCPM5-1B)**  
  *作者*：openbmb | 👍 771 | ⬇️ 91,235  
  *一句话*：仅 1B 参数的高效语言模型，端侧部署的新选择。  

- **[nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-BF16](https://huggingface.co/nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-BF16)**  
  *作者*：nvidia | 👍 118 | ⬇️ 9,125  
  *一句话*：550B 总参、55B 激活的文本生成怪兽，BF16 精度专为高端算力设计。  

- **[nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-NVFP4](https://huggingface.co/nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-NVFP4)**  
  *作者*：nvidia | 👍 109 | ⬇️ 7,419  
  *一句话*：同上模型的 NVFP4 量化版，大幅降低显存需求。  

### 🎨 多模态与生成（图像、视频、音频、文本到 X）  
- **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)**  
  *作者*：nvidia | 👍 1,379 | ⬇️ 101,823  
  *一句话*：通用目标定位模型，输入图像+文本即可高精度定位任意物体。  

- **[google/gemma-4-12B-it](https://huggingface.co/google/gemma-4-12B-it)**  
  *作者*：google | 👍 553 | ⬇️ 142,851  
  *一句话*：Gemma 4 的指令调优版，支持任意到任意模态转换（文本/图像/音频）。  

- **[google/gemma-4-12B](https://huggingface.co/google/gemma-4-12B)**  
  *作者*：google | 👍 339 | ⬇️ 53,525  
  *一句话*：Gemma 4 基础版，多模态原生统一架构的轻量开源代表。  

- **[stepfun-ai/Step-3.7-Flash](https://huggingface.co/stepfun-ai/Step-3.7-Flash)**  
  *作者*：stepfun-ai | 👍 332 | ⬇️ 27,948  
  *一句话*：阶跃星辰的视觉语言模型，兼顾文本生成与图像理解。  

- **[ideogram-ai/ideogram-4-fp8](https://huggingface.co/ideogram-ai/ideogram-4-fp8)**  
  *作者*：ideogram-ai | 👍 270 | ⬇️ 1,246  
  *一句话*：下一代文本到图像模型，FP8 量化保持质量同时减少显存占用。  

- **[ideogram-ai/ideogram-4-nf4](https://huggingface.co/ideogram-ai/ideogram-4-nf4)**  
  *作者*：ideogram-ai | 👍 192 | ⬇️ 1,594  
  *一句话*：Ideogram 4 的 NF4 量化版，适配消费级 GPU 运行。  

- **[nvidia/Cosmos3-Nano](https://huggingface.co/nvidia/Cosmos3-Nano)**  
  *作者*：nvidia | 👍 176 | ⬇️ 21,625  
  *一句话*：NVIDIA 全模态宇宙模型的小尺寸版本，支持文本/图像/音频/视频生成。  

- **[nvidia/Cosmos3-Super](https://huggingface.co/nvidia/Cosmos3-Super)**  
  *作者*：nvidia | 👍 142 | ⬇️ 19,227  
  *一句话*：Cosmos3 超级版，多模态生成能力最强，适合高质量创作。  

- **[ByteDance/Bernini-R](https://huggingface.co/ByteDance/Bernini-R)**  
  *作者*：ByteDance | 👍 142 | ⬇️ 175  
  *一句话*：字节跳动发布的图像+文本到视频渲染器，从静态图生成动态视频。  

- **[nvidia/PiD](https://huggingface.co/nvidia/PiD)**  
  *作者*：nvidia | 👍 310 | ⬇️ 901  
  *一句话*：基于扩散模型的图像超分辨率与修复模型。  

- **[bosonai/higgs-audio-v3-tts-4b](https://huggingface.co/bosonai/higgs-audio-v3-tts-4b)**  
  *作者*：bosonai | 👍 120 | ⬇️ 408  
  *一句话*：4B 参数的文本到语音模型，合成质量接近真人。  

- **[meituan-longcat/LongCat-Video-Avatar-1.5](https://huggingface.co/meituan-longcat/LongCat-Video-Avatar-1.5)**  
  *作者*：meituan-longcat | 👍 519 | ⬇️ 1,675  
  *一句话*：音频+文本驱动的数字人视频生成，美团出品，直播/客服场景潜力大。  

- **[nvidia/Cosmos3-Super-Text2Image](https://huggingface.co/nvidia/Cosmos3-Super-Text2Image)**  
  *作者*：nvidia | 👍 116 | ⬇️ 1,194  
  *一句话*：Cosmos3 超级版文本到图像专用分支。  

- **[SulphurAI/Sulphur-2-base](https://huggingface.co/SulphurAI/Sulphur-2-base)**  
  *作者*：SulphurAI | 👍 1,566 | ⬇️ 1,691,633  
  *一句话*：基于 LTX-2.3 的视频生成基础模型，下载量超 169 万，社区视频创作新宠。  

- **[MisoLabs/MisoTTS](https://huggingface.co/MisoLabs/MisoTTS)**  
  *作者*：MisoLabs | 👍 111 | ⬇️ 0  
  *一句话*：全新 TTS 模型，尚未有下载但已获关注

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*