# Hugging Face 热门模型日报 2026-07-24

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-07-24 02:16 UTC

---

好的，以下是为您生成的《Hugging Face 热门模型日报》。

---

# Hugging Face 热门模型日报 | 2026-07-24

## 今日速览

本周 Hugging Face 生态的核心亮点集中在**多模态模型**、**超大规模语言模型**与**社区量化微调的繁荣**三大方面。智谱AI开源的 **GLM-5.2** 以绝对优势登顶周榜，验证了前沿中文 MoE 模型的强大号召力；Google 的 **Gemma-4-31B-it** 下载量突破千万，成为本周最受欢迎的“工业级”多模态模型。同时，以 **Qwen3.6** 为基座的微调模型（包括大量 Uncensored 变体）占据了热门榜的显著位置，显示出社区对“开放基座+私有化调优”模式的巨大热情。此外，百度推出的 **Unlimited-OCR** 凭借海量下载，彰显了垂直场景（如文档解析）的强刚需。

## 热门模型

### 🧠 语言模型（LLM、对话模型、指令微调）

- **zai-org/GLM-5.2** ([链接](https://huggingface.co/zai-org/GLM-5.2))  
  作者: zai-org | 点赞: 4,371 | 下载: 596,442  
  一句话说明：智谱AI最新开源MoE（混合专家）大模型，凭借强大的推理与对话能力，稳居本周热度第一。

- **google/gemma-4-31B-it** ([链接](https://huggingface.co/google/gemma-4-31B-it))  
  作者: google | 点赞: 3,347 | 下载: 12,666,488  
  一句话说明：Google发布的多模态指令模型，兼具文本与图像理解能力，堪称本周“下载王”。

- **poolside/Laguna-S-2.1** ([链接](https://huggingface.co/poolside/Laguna-S-2.1))  
  作者: poolside | 点赞: 518 | 下载: 13,285  
  一句话说明：专业级代码与文本生成模型，企业级定位，带动了Laguna系列多个量化版本的上榜。

- **upstage/Solar-Open2-250B** ([链接](https://huggingface.co/upstage/Solar-Open2-250B))  
  作者: upstage | 点赞: 455 | 下载: 362  
  一句话说明：Upstage发布的开源250B参数量级大模型，虽然刚发布下载量有限，但凭借“大参数+开源”定位引发了高度关注。

- **Nanbeige/Nanbeige4.2-3B** ([链接](https://huggingface.co/Nanbeige/Nanbeige4.2-3B))  
  作者: Nanbeige | 点赞: 323 | 下载: 4,532  
  一句话说明：新一代高效轻量级语言模型（3B），专注于高效推理与低资源部署。

- **Motif-Technologies/Motif-3-Beta** ([链接](https://huggingface.co/Motif-Technologies/Motif-3-Beta))  
  作者: Motif-Technologies | 点赞: 173 | 下载: 1,856  
  一句话说明：专注特征提取与表示学习的文本模型，在企业级向量化应用场景中有潜力。

- **fdtn-ai/antares-1b** ([链接](https://huggingface.co/fdtn-ai/antares-1b))  
  作者: fdtn-ai | 点赞: 121 | 下载: 2,747  
  一句话说明：聚焦安全领域的1B参数级小模型，采用Granite-MoE-Hybrid架构，面向垂直领域推理。

### 🎨 多模态与生成（图像、视频、音频、文本到X）

- **baidu/Unlimited-OCR** ([链接](https://huggingface.co/baidu/Unlimited-OCR))  
  作者: baidu | 点赞: 2,892 | 下载: 2,414,259  
  一句话说明：百度发布的无限制场景OCR模型，将图像文字识别提升到新高度，下载量极高，是垂直应用中的明星。

- **thinkingmachines/Inkling** ([链接](https://huggingface.co/thinkingmachines/Inkling))  
  作者: thinkingmachines | 点赞: 1,508 | 下载: 24,669  
  一句话说明：新兴的图像对话模型，支持“看图说话”功能，代表了更轻量的多模态理解方向。

- **microsoft/Mage-Flow** ([链接](https://huggingface.co/microsoft/Mage-Flow))  
  作者: microsoft | 点赞: 187 | 下载: 411  
  一句话说明：微软推出的文本生成图像模型，采用扩散架构，是图像生成领域的新势力。

- **nvidia/Cosmos3-Edge** ([链接](https://huggingface.co/nvidia/Cosmos3-Edge))  
  作者: nvidia | 点赞: 101 | 下载: 28,493  
  一句话说明：NVIDIA在物理世界理解与边缘计算场景的扩散模型，标注为Cosmos3系列。

- **nvidia/nemotron-3.5-asr-streaming-0.6b** ([链接](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b))  
  作者: nvidia | 点赞: 926 | 下载: 750,118  
  一句话说明：高性能流式语音识别（ASR）模型，0.6B参数量级，适合实时音频处理。

- **OpenMOSS-Team/MOSS-Transcribe-Diarize** ([链接](https://huggingface.co/OpenMOSS-Team/MOSS-Transcribe-Diarize))  
  作者: OpenMOSS-Team | 点赞: 320 | 下载: 111,598  
  一句话说明：新一代音频转录+说话人分离模型，面向智能会议与音频结构化分析。

- **Qwen/Qwen3-TTS-12Hz-1.7B-CustomVoice** ([链接](https://huggingface.co/Qwen/Qwen3-TTS-12Hz-1.7B-CustomVoice))  
  作者: Qwen | 点赞: 1,799 | 下载: 2,497,020  
  一句话说明：通义千问推出的定制化语音合成模型（TTS），支持12Hz音频生成与自定义音色，引爆了音频生成领域的关注。

### 🔧 专用模型（代码、数学、医疗、嵌入）

- **moonshotai/Kimi-K2.7-Code** ([链接](https://huggingface.co/moonshotai/Kimi-K2.7-Code))  
  作者: moonshotai | 点赞: 1,249 | 下载: 766,522  
  一句话说明：Kimi团队推出的代码专用模型，采用压缩技术，在代码生成与补全任务上表现优异。

- **ATH-MaaS/OvisOCR2** ([链接](https://huggingface.co/ATH-MaaS/OvisOCR2))  
  作者: ATH-MaaS | 点赞: 257 | 下载: 26,919  
  一句话说明：基于Qwen3.5架构的OCR专用模型，专注于高精度图像文字识别。

- **openbmb/MiniCPM-RobotManip** ([链接](https://huggingface.co/openbmb/MiniCPM-RobotManip))  
  作者: openbmb | 点赞: 165 | 下载: 408  
  一句话说明：面向机器人操作（操纵）的视觉-语言-动作模型，是具身智能和机器人大模型领域的前沿探索。

- **openbmb/MiniCPM-RobotTrack** ([链接](https://huggingface.co/openbmb/MiniCPM-RobotTrack))  
  作者: openbmb | 点赞: 117 | 下载: 306  
  一句话说明：与RobotManip类似，但侧重于机器人目标跟踪的专用模型。

- **conradlocke/krea2-identity-edit** ([链接](https://huggingface.co/conradlocke/krea2-identity-edit))  
  作者: conradlocke | 点赞: 517 | 下载: 0  
  一句话说明：基于Krea-2基础模型的 LoRA，专门用于AI图像编辑中的人物身份保持，虽然下载量低但类型新颖。

### 📦 微调与量化（社区微调、GGUF、AWQ）

- **DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF** ([链接](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF))  
  作者: DavidAU | 点赞: 400 | 下载: 334,847  
  一句话说明：基于Qwen3.6的极致社区微调版本，集Uncensored、多模型融合、GGUF量化于一身，是社区自定义理想的典型代表。

- **prism-ml/Ternary-Bonsai-27B-gguf** ([链接](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf))  
  作者: prism-ml | 点赞: 985 | 下载: 576,083  
  一句话说明：27B参数模型的**三进制量化**（2-bit）版本，在本地部署效率和容量之间取得了惊人平衡，好评如潮。

- **prism-ml/Bonsai-27B-gguf** ([链接](https://huggingface.co/prism-ml/Bonsai-27B-gguf))  
  作者: prism-ml | 点赞: 620 | 下载: 1,910,116  
  一句话说明：Bonsai-27B的1-bit极致量化版，虽然精度极低但下载量惊人，反映了社区对“能跑就行”的极端部署需求。

- **HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive** ([链接](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive))  
  作者: HauhauCS | 点赞: 3,033 | 下载: 2,027,080  
  一句话说明：Qwen3.6 35B MoE模型的社区“激进”微调版，以Uncensored和强风格输出著称，是社区微调方向的现象级模型。

- **empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF** ([链接](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF))  
  作者: empero-ai | 点赞: 2,439 | 下载: 2,126,755  
  一句话说明：融合了Claude（神话）风格、基于Qwen3.5的9B模型，GGUF量化版，在角色扮演和创意写作领域极受欢迎。

- **unsloth/Laguna-S-2.1-GGUF** ([链接](https://huggingface.co/unsloth/Laguna-S-2.1-GGUF))  
  作者: unsloth | 点赞: 150 | 下载: 28,542  
  一句话说明：知名微调工具Unsloth对Laguna-S-2.1的GGUF转化版本，方便社区直接部署。

- **bottlecapai/ThinkingCap-Qwen3.6-27B** ([链接](https://huggingface.co/bottlecapai/ThinkingCap-Qwen3.6-27B))  
  作者: bottlecapai |

---
*本日报由 [agents-radar](https://github.com/JohnGao818/agents-radar) 自动生成。*