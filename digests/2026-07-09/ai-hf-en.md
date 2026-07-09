# Hugging Face Trending Models Digest 2026-07-09

> Source: [Hugging Face Hub](https://huggingface.co/) | 30 models | Generated: 2026-07-09 02:35 UTC

---

Here is the structured digest for the Hugging Face trending models as of 2026-07-09.

---

## Hugging Face Trending Models Digest — 2026-07-09

### 1. Today's Highlights

The Hugging Face ecosystem this week is defined by an explosive growth in **multimodal** and **quantized** models. The **Qwen 3.5/3.6** family continues to dominate as the foundational base for dozens of fine-tunes, GGUF versions, and experimental variants, with models like **Qwen3.6-35B-A3B-Uncensored** and **unsloth/Qwen3.6-27B-MTP-GGUF** showing massive download counts. Two specialized models offer standout innovation: **NVIDIA's LocateAnything-3B** (2,667 likes) redefines zero-shot object localization, while **Baidu's Unlimited-OCR** (1,874 likes) brings a vast, unified OCR pipeline to the open-weight community. The week also saw the emergence of the **Gemma-4-12B** family as a hot new base for agentic and coding GGUF variants, and the appearance of **DeepSeek-V4-Pro-DSpark** signals a new frontier in safety-guided reasoning models.

---

### 2. Trending Models by Category

#### 🧠 Language Models
- **[GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — *zai-org* — 3,669 likes / 281k downloads  
  A leading conversational MoE model that dethroned many larger models this week due to its efficient architecture and strong reasoning benchmarks.  
- **[DeepSeek-V4-Pro-DSpark](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-DSpark)** — *deepseek-ai* — 439 likes / 15.5k downloads  
  DeepSeek's latest flagship text-generation model featuring an integrated "DSpark" safety reasoning layer, backed by a new arXiv paper.  
- **[Ornith-1.0-35B](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B)** — *deepreinforce-ai* — 366 likes / 280k downloads  
  A powerful Qwen3.5-MoE derivative optimized for strong general reasoning with a permissive MIT license.  
- **[Leanstral-1.5-119B-A6B](https://huggingface.co/mistralai/Leanstral-1.5-119B-A6B)** — *mistralai* — 167 likes / 157 downloads  
  A massive 119B-parameter model with only 6B active parameters, showcasing Mistral's continued commitment to efficient MoE architectures.

#### 🎨 Multimodal & Generation
- **[NVIDIA/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — *nvidia* — 2,667 likes / 1.42M downloads  
  A state-of-the-art vision model for zero-shot object localization and segmentation, driving huge interest from robotics and image editing communities.  
- **[Baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** — *baidu* — 1,874 likes / 1.08M downloads  
  A comprehensive OCR pipeline model that handles unlimited-length text recognition in images, making it the go-to open-source OCR solution.  
- **[Krea-2-Turbo](https://huggingface.co/krea/Krea-2-Turbo)** — *krea* — 555 likes / 123k downloads  
  The fast inference version of the popular Krea-2 text-to-image model, offering higher quality outputs with reduced latency.

#### 🔧 Specialized Models
- **[google/tabfm-1.0.0-pytorch](https://huggingface.co/google/tabfm-1.0.0-pytorch)** — *google* — 314 likes / 9.5k downloads  
  Google's first-of-its-kind foundation model for tabular data, enabling zero-shot classification and regression on structured datasets.  
- **[meituan-longcat/LongCat-2.0](https://huggingface.co/meituan-longcat/LongCat-2.0)** — *meituan-longcat* — 152 likes / 385 downloads  
  Meituan's conversational long-context model, purpose-built for customer service and document-heavy workflows.

#### 📦 Fine-tunes & Quantizations
- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** — *HauhauCS* — 2,574 likes / 2.82M downloads  
  An aggressive, uncensored fine-tune of the Qwen3.6 MoE model, quantized to GGUF for efficient local use—the most downloaded model this week.  
- **[unsloth/Qwen3.6-27B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)** — *unsloth* — 1,013 likes / 2.84M downloads  
  Unsloth's GGUF quantization of Qwen3.6-27B with multi-turn prediction support, setting a new standard for efficient vision-language inference.  
- **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)** — *yuxinlu1* — 2,653 likes / 675k downloads  
  A highly performant GGUF variant of the Gemma-4-12B model, fine-tuned for coding and reasoning with the fable5 dataset—a breakout hit among developer tools.

---

### 3. Ecosystem Signal

The ecosystem this week reinforces two dominant themes: **Qwen as the foundation of the open-weight fleet** and **quantization as the primary driver of adoption**. Every major Qwen release (3.5, 3.6) immediately spawns dozens of GGUF, MoE, and uncensored variants, which collectively amass millions of downloads—indicating that the community prefers powerful models that run locally on consumer hardware. The **Gemma-4-12B** family, released just recently, is already overtaking older 7B leaders, proving that Google’s token-efficient approach (12B with new Gemma architecture) is winning over developers who need coding and agentic capabilities. On the proprietary side, **NVIDIA, Baidu, and Tencent** are releasing highly polished, specialized tools (LocateAnything, Unlimited-OCR, Hy3) that blur the line between research and production-ready APIs. The surge of **GGUF uploads from unsloth** and the **Ornith-1.0** family (MIT-licensed) suggests the community is voting for permissive licensing and local-first deployment over cloud-only models.

---

### 4. Worth Exploring

- **[NVIDIA/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** — This is the most innovative model on the list: a 3B-parameter vision model that can localize any object without training. Its high like-to-download ratio suggests early adopters are finding real utility in robotics, data labeling, and creative workflows.

- **[mistralai/Leanstral-1.5-119B-A6B](https://huggingface.co/mistralai/Leanstral-1.5-119B-A6B)** — A glimpse into the future of extremely efficient MoE models. With only 6B active parameters out of 119B, it tries to compete with dense 30B-70B models while using a fraction of the FLOPs. Researchers and efficiency enthusiasts should study its architecture and benchmark reports.

- **[yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-coder-fable5-composer2.5-v1-GGUF)** — With 2,653 likes and over 650k downloads, this GGUF merge of Gemma-4 and the fable5 dataset is the most popular coding model this week. It represents the new sweet spot: small enough to run on-device, powerful enough for complex agentic tasks. Worth trying for anyone building local coding assistants.

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*