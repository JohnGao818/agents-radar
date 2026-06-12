# Hugging Face 热门模型日报 2026-06-12

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-06-12 03:34 UTC

---

# Hugging Face 热门模型日报（2026-06-12）

## 今日速览

本周 Hugging Face 热度由 **DeepSeek-V4-Pro** 领跑，以 4,783 赞和 400 万下载量成为绝对焦点。**NVIDIA** 与 **Google** 继续输出重磅多模态模型：NVIDIA 的 `LocateAnything-3B` 定位新范式，Google 的 `Gemma-4` 系列（12B/26B）及其 GGUF 量化版全面霸榜。社区微调异常活跃，`Qwen3.6-35B-A3B-Uncensored` 与 `Gemma-4-12B-OBLITERATED` 等“无审查”变体下载量惊人，折射出用户对开放对话体验的强烈需求。同时，**Ideogram-4**、**Bernini-R** 和 **MiMo-V2.5** 分别在图像生成、视频生成和本地化 Agent 方向带来新突破，多模态生态竞争白热化。

---

## 热门模型分类整理

### 🧠 语言模型（LLM、对话模型、指令微调）

1. **DeepSeek-V4-Pro** | [HF 链接](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro)  
   *作者*: deepseek-ai | *点赞*: 4,783 | *下载*: 4,061,006  
   *说明*: DeepSeek 最新旗舰对话模型，延续 MoE 架构，本周热度与下载量双冠，代表开源 LLM 在性能与社区信任上的新高度。

2. **HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive** | [HF 链接](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)  
   *作者*: HauhauCS | *点赞*: 1,683 | *下载*: 3,057,541  
   *说明*: 基于 Qwen3.6 的混合 MoE 模型（35B 总参/3B 激活），经无审查微调并强化“激进”风格，下载量仅次于 DeepSeek-V4-Pro，反映社区对自由对话的强烈偏好。

3. **sapientinc/HRM-Text-1B** | [HF 链接](https://huggingface.co/sapientinc/HRM-Text-1B)  
   *作者*: sapientinc | *点赞*: 750 | *下载*: 134,752  
   *说明*: 专为 HR 与人才管理场景打造的 1B 级轻量文本生成模型，企业级应用方向崭露头角。

4. **nex-agi/Nex-N2-Pro** | [HF 链接](https://huggingface.co/nex-agi/Nex-N2-Pro)  
   *作者*: nex-agi | *点赞*: 206 | *下载*: 1,185  
   *说明*: 基于 Qwen3.5 MoE 架构的高性能对话模型，侧重多模态理解，定位专业级 Agent。

5. **nex-agi/Nex-N2-mini** | [HF 链接](https://huggingface.co/nex-agi/Nex-N2-mini)  
   *作者*: nex-agi | *点赞*: 165 | *下载*: 1,222  
   *说明*: Nex-N2 系列的轻量版，平衡速度与质量，适合边缘部署。

6. **nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-BF16** | [HF 链接](https://huggingface.co/nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-BF16)  
   *作者*: nvidia | *点赞*: 198 | *下载*: 59,066  
   *说明*: NVIDIA 超大 MoE 模型（550B 总参/55B 激活），BF16 精度版本，面向高端推理场景。

7. **nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-NVFP4** | [HF 链接](https://huggingface.co/nvidia/NVIDIA-Nemotron-3-Ultra-550B-A55B-NVFP4)  
   *作者*: nvidia | *点赞*: 168 | *下载*: 91,117  
   *说明*: 同系列 NVFP4 量化版，在几乎无性能损失下大幅降低显存需求，下载量高于 BF16 版，说明社区优先选择量化部署。

8. **XiaomiMiMo/MiMo-V2.5-Pro-FP4-DFlash** | [HF 链接](https://huggingface.co/XiaomiMiMo/MiMo-V2.5-Pro-FP4-DFlash)  
   *作者*: XiaomiMiMo | *点赞*: 87 | *下载*: 660  
   *说明*: 小米推出的端侧 Agent 模型，FP4 动态闪存量化，瞄准手机与 IoT 场景。

---

### 🎨 多模态与生成（图像、视频、音频、文本到X）

1. **nvidia/LocateAnything-3B** | [HF 链接](https://huggingface.co/nvidia/LocateAnything-3B)  
   *作者*: nvidia | *点赞*: 1,878 | *下载*: 131,794  
   *说明*: NVIDIA 推出的通用目标定位模型（3B 参数量），可精准识别并定位图像中任意物体，刷新图像-文本-文本任务效率。

2. **google/gemma-4-12B-it** | [HF 链接](https://huggingface.co/google/gemma-4-12B-it)  
   *作者*: google | *点赞*: 942 | *下载*: 675,936  
   *说明*: Google 最新统一多模态模型（any-to-any），支持图像/文本混合输入，指令微调版，社区下载量极高。

3. **google/diffusiongemma-26B-A4B-it** | [HF 链接](https://huggingface.co/google/diffusiongemma-26B-A4B-it)  
   *作者*: google | *点赞*: 508 | *下载*: 0  
   *说明*: Diffusion-Gemma 系列融合扩散与 Transformer，26B 总参/4B 激活，专为图像+文本理解生成，虽然下载暂少但关注度强。

4. **ideogram-ai/ideogram-4-fp8** | [HF 链接](https://huggingface.co/ideogram-ai/ideogram-4-fp8)  
   *作者*: ideogram-ai | *点赞*: 487 | *下载*: 7,170  
   *说明*: Ideogram 最新文本到图像模型 FP8 量化版，在图像质量与布局精准度上实现 SOTA，社区热度持续上升。

5. **ideogram-ai/ideogram-4-nf4** | [HF 链接](https://huggingface.co/ideogram-ai/ideogram-4-nf4)  
   *作者*: ideogram-ai | *点赞*: 318 | *下载*: 6,124  
   *说明*: 同系列的 NF4 量化版，进一步降低显存需求，适合消费级 GPU。

6. **stepfun-ai/Step-3.7-Flash** | [HF 链接](https://huggingface.co/stepfun-ai/Step-3.7-Flash)  
   *作者*: stepfun-ai | *点赞*: 368 | *下载*: 50,187  
   *说明*: Step 系列最新视觉语言模型（Flash 版），轻量快速，兼顾图像理解与文本生成。

7. **bosonai/higgs-audio-v3-tts-4b** | [HF 链接](https://huggingface.co/bosonai/higgs-audio-v3-tts-4b)  
   *作者*: bosonai | *点赞*: 363 | *下载*: 19,948  
   *说明*: 基于 Qwen3 的多模态 TTS 模型（4B），支持高质量文本到语音合成，多语言能力强。

8. **nvidia/nemotron-3.5-asr-streaming-0.6b** | [HF 链接](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)  
   *作者*: nvidia | *点赞*: 372 | *下载*: 4,965  
   *说明*: 流式语音识别模型（0.6B），支持缓存感知实时转录，适合低延迟场景。

9. **ByteDance/Bernini-R** | [HF 链接](https://huggingface.co/ByteDance/Bernini-R)  
   *作者*: ByteDance | *点赞*: 222 | *下载*: 305  
   *说明*: 字节跳动推出的图像+文本到视频渲染模型，基于扩散架构，可生成动态角色动画，首发即获关注。

10. **zai-org/SCAIL-2** | [HF 链接](https://huggingface.co/zai-org/SCAIL-2)  
    *作者*: zai-org | *点赞*: 118 | *下载*: 0  
    *说明*: 基于姿态驱动的人物动画视频生成模型，专注角色动画控制，尚处早期但潜力大。

11. **google/magenta-realtime-2** | [HF 链接](https://huggingface.co/google/magenta-realtime-2)  
    *作者*: google | *点赞*: 178 | *下载*: 19,806  
    *说明*: Google 实时文本到音频（音乐/音效）生成模型，支持交互式创作，适合音乐人。

12. **MisoLabs/MisoTTS** | [HF 链接](https://huggingface.co/MisoLabs/MisoTTS)  
    *作者*: MisoLabs | *点赞*: 194 | *下载*: 0  
    *说明*: 新开源 TTS 模型，强调自然语音合成，纯净版无数据集污染，受研究社区关注。

13. **Comfy-Org/Ideogram-4** | [HF 链接](https://huggingface.co/Comfy-Org/Ideogram-4)  
    *作者*: Comfy-Org | *点赞*: 135 | *下载*: 0  
    *说明*: Comfy-Org 封装的 Ideogram-4 工作流版本，方便 ComfyUI 用户直接使用，降低门槛。

---

### 🔧 专用模型（代码、数学、医疗、嵌入等）

1. **CohereLabs/North-Mini-Code-1.0** | [HF 链接](https://huggingface.co/CohereLabs/North-Mini-Code-1.0)  
   *作者*: CohereLabs | *点赞*: 309 | *下载*: 1,859  
   *说明*: Cohere 推出的代码专用 MoE 模型（小型），擅长代码生成与补全，补齐 Cohere 在代码领域的短板。

2. （其他专用模型在本榜单中未单独出现，但 ASR/TTS 可视为专用，已归入多模态；医疗 HRM 归入语言模型）

---

### 📦 微调与量化（社区微调、GGUF、AWQ）

1. **unsloth/gemma-4-12b-it-GGUF** | [HF 链接](https://huggingface.co/unsloth/gemma-4-12b-it-GGUF)  
   *作者*: unsloth | *点赞*: 562 | *下载*: 711,706  
   *说明*: 基于 Google Gemma-4-12B-it 的 GGUF 量化版，由 unsloth 社区优化，下载量超 70 万，是轻量部署首选。

2. **unsloth/gemma-4-12B-it-qat-GGUF** | [HF 链接](https://huggingface.co/unsloth/gemma-4-12B-it-qat-GGUF)  
   *作者*: unsloth | *点赞*: 200 | *下载*: 148,252  
   *说明*: 同一基座的 QAT（量化感知训练）GGUF 版，精度更高，适合对质量敏感的场景。

3. **unsloth/diffusiongemma-26B-A4B-it-GGUF** | [HF 链接](https://huggingface.co/unsloth/diffusiongemma-26B-A4B-it-GGUF)  
   *作者*: unsloth | *点赞*: 184 | *下载*: 0  
   *说明*: Diffusion-Gemma 的 GGUF 量化版，虽暂无下载但已为多模态本地部署做准备。

4. **unsloth/gemma-4-26B-A4B-it-qat-GGUF** | [HF 链接](https://huggingface.co/unsloth/gemma-4-26B-A4B-it-qat-GGUF)  
   *作者*: unsloth | *点赞*: 143 | *下载*: 129,110  
   *说明*: 26B 级 Gemma 的 QAT GGUF 版，满足更大参数量场景的本地运行需求。

5. **google/gemma-4-12B-it-qat-q4_0-gguf** | [HF 链接](https://huggingface.co/google/gemma-4-12B-it-qat-q4_0-gguf)  
   *作者*: google | *点赞*: 130 | *下载*: 96,749  
   *说明*: Google 官方推出的 QAT + 4bit GGUF 版本，官方量化进一步降低部署门槛。

6. **OBLITERATUS/Gemma-4-12B-OBLITERATED** | [HF 链接](https://huggingface.co/OBLITERATUS/Gemma-4-12B-OBLITERATED)  
   *作者*: OBLITERATUS | *点赞*: 234 | *下载*: 14,838  
   *说明*: 社区热门“去审查”Gemma-4 变体，通过权重擦除技术移除安全限制，引发合规讨论。

7. **huihui-ai/Huihui-gemma-4-12B-it-abliterated** | [HF 链接](https://huggingface.co/huihui-ai/Huihui-gemma-4-12B-it-abliterated)  
   *作者*: huihui-ai | *点赞*: 144 | *下载*: 6,400  
   *说明*: 另一款 abliterated（去审查）版本，由 huihui-ai 社区制作，与 OBLITERATUS 形成竞争。

---

## 生态信号

- **Google Gemma-4 家族全面爆发**：从官方基座、指令版、QAT 量化到社区无审查变体，Gemma-4 系列占据榜单近 1/3 位置。其 unified any-to-any 能力成为多模态新标杆，社区快速跟进 GGUF 与 abliterated 微调，表明开源生态对统一多模态模型的渴望。
- **DeepSeek-V4 持续统治**：以近 5000 赞和 400 万下载量稳居第一，延续“开源最强”品牌，且无量化变体却下载量极高，说明用户更倾向直接使用原重量级模型。
- **量化格式成标配**：unsloth 的 GGUF 系列下载量（70 万+）远超官方未量化版，GGUF 已成为本地部署事实标准；QAT 与 FP4/NVFP4 等混合精度量化开始普及，用户在性能与资源间寻求平衡。
- **无审查微调活跃但争议并存**：“Uncensored”和“Abliterated”模型下载量极高，反映部分用户对自由度的高度需求，但也引发安全讨论，平台可能加强治理。

---

## 值得探索

1. **nvidia/LocateAnything-3B** — 在“任意目标定位”上实现通用性突破，3B 参数量即可处理开放集目标，对机器人、工业视觉、交互式应用有巨大潜力，值得研究其定位机制与部署效率。

2. **ByteDance/Bernini-R** — 首次将图像

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*