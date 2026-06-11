# AI Open Source Trends 2026-06-11

> Sources: GitHub Trending + GitHub Search API | Generated: 2026-06-11 03:33 UTC

---

# AI Open Source Trends Report — 2026-06-11

## Today’s Highlights

The open-source AI ecosystem is pivoting rapidly toward **agent skill marketplaces** and **agent orchestration frameworks**. Three of today’s top trending repos (agent-skills, pm-skills, last30days-skill) each gained 800+ stars in a single day, signaling that the community is hungry for plug-and-play, production-grade capabilities for coding agents. Meanwhile, **Apple’s container tool** (1611 ★ today) and **MoneyPrinterTurbo** (1389 ★ today) show that infrastructure for AI workloads and generative media remain strong attractors. The topic-search results reveal that **RAG and vector databases** continue to dominate long-tail interest, with several new entries focusing on persistent memory and knowledge graphs for agents.

## Top Projects by Category

### 🔧 AI Infrastructure (Frameworks, SDKs, Inference Engines, Dev Tools)

- **[tensorflow/tensorflow](https://github.com/tensorflow/tensorflow)** — ⭐195,630  
  The foundational ML framework, still the most starred project in the ecosystem.

- **[vllm-project/vllm](https://github.com/vllm-project/vllm)** — ⭐82,476  
  High-throughput inference engine for LLMs, essential for production deployments.

- **[ollama/ollama](https://github.com/ollama/ollama)** — ⭐173,809  
  Local model runner now supporting Kimi, GLM, DeepSeek, and more; key to edge AI.

- **[open-webui/open-webui](https://github.com/open-webui/open-webui)** — ⭐141,022  
  User-friendly interface for Ollama and OpenAI; bridges inference with end users.

- **[firecrawl/firecrawl](https://github.com/firecrawl/firecrawl)** — ⭐131,197  
  Scalable web scraping API designed for AI agents; gained traction as a core tool.

- **[0xPlaygrounds/rig](https://github.com/0xPlaygrounds/rig)** — ⭐7,583  
  Rust-native LLM application framework; growing fast in the systems community.

### 🤖 AI Agents / Workflows (Agent Frameworks, Automation, Multi-Agent Systems)

- **[langgenius/dify](https://github.com/langgenius/dify)** — ⭐144,771  
  Production-ready agentic workflow platform; one of the most complete agent harnesses.

- **[OpenHands/OpenHands](https://github.com/OpenHands/OpenHands)** — ⭐76,418  
  AI-driven development agent; direct competitor to Claude Code and Codex.

- **[browser-use/browser-use](https://github.com/browser-use/browser-use)** — ⭐98,179  
  Makes websites accessible to AI agents; critical for web-based automation.

- **[addyosmani/agent-skills](https://github.com/addyosmani/agent-skills)** — +821 today  
  A curated library of production-grade engineering skills for AI coding agents – the most notable “skills marketplace” repo today.

- **[mvanhorn/last30days-skill](https://github.com/mvanhorn/last30days-skill)** — +2535 today  
  An agent skill that researches any topic across Reddit, X, YouTube, HN, and more; explosive growth shows demand for grounded research agents.

- **[obra/superpowers](https://github.com/obra/superpowers)** — +1104 today  
  Agentic skills framework + software development methodology; introduces structured agent workflows.

- **[activeloopai/hivemind](https://github.com/activeloopai/hivemind)** — +64 today  
  Centralized “brain” for orchestrating multiple agents; a new pattern in multi-agent coordination.

### 📦 AI Applications (Specific Apps, Vertical Solutions)

- **[harry0703/MoneyPrinterTurbo](https://github.com/harry0703/MoneyPrinterTurbo)** — +1389 today  
  One-click AI short video generation; massively popular for content creation.

- **[maziyarpanahi/openmed](https://github.com/maziyarpanahi/openmed)** — +527 today  
  Open-source healthcare AI; represents growing vertical specialization.

- **[roboflow/supervision](https://github.com/roboflow/supervision)** — +695 today  
  Reusable computer vision tools; the go-to library for CV practitioners.

- **[ruvnet/RuView](https://github.com/ruvnet/RuView)** — +420 today  
  WiFi-based spatial intelligence and vital sign monitoring; novel sensor-fusion AI.

### 🧠 LLMs / Training (Model Weights, Training Frameworks, Fine-Tuning)

- **[hiyouga/LlamaFactory](https://github.com/hiyouga/LlamaFactory)** — ⭐72,056  
  Unified fine-tuning framework for 100+ LLMs/VLMs; standard for custom model training.

- **[FareedKhan-dev/train-llm-from-scratch](https://github.com/FareedKhan-dev/train-llm-from-scratch)** — +247 today  
  Straightforward method to train an LLM from data collection to generation; educational hit.

- **[open-compass/opencompass](https://github.com/open-compass/opencompass)** — ⭐7,080  
  Comprehensive LLM evaluation platform; vital for model comparison.

- **[skyzh/tiny-llm](https://github.com/skyzh/tiny-llm)** — ⭐4,267  
  Hands-on course for building a tiny vLLM on Apple Silicon; systems education.

### 🔍 RAG / Knowledge (Vector Databases, Retrieval-Augmented Generation, Knowledge Management)

- **[infiniflow/ragflow](https://github.com/infiniflow/ragflow)** — ⭐82,423  
  Leading open-source RAG engine with agent capabilities; de facto standard.

- **[Mintplex-Labs/anything-llm](https://github.com/Mintplex-Labs/anything-llm)** — ⭐61,408  
  Local-first RAG platform; emphasizes data ownership.

- **[run-llama/llama_index](https://github.com/run-llama/llama_index)** — ⭐50,069  
  Document agent and OCR platform; evolving beyond simple indexing.

- **[mem0ai/mem0](https://github.com/mem0ai/mem0)** — ⭐58,293  
  Universal memory layer for AI agents; bridges RAG and persistent context.

- **[NirDiamant/RAG_Techniques](https://github.com/NirDiamant/RAG_Techniques)** — ⭐27,843  
  Comprehensive notebook-based tutorial on advanced RAG methods.

- **[milvus-io/milvus](https://github.com/milvus-io/milvus)** — ⭐44,724  
  High-performance vector database; cloud-native and scalable.

## Trend Signal Analysis

**Explosion of “Agent Skills” as a new category**  
Today’s trending list is dominated by repos that package discrete capabilities (“skills”) for AI coding agents. The top three – `agent-skills` (+821), `pm-skills` (+804), and `last30days-skill` (+2535) – all define standardized interfaces for agents to call external tools or perform research tasks. This mirrors the early days of npm/pip: the community is building a universal skill registry. Google’s official `skills` repo (+211) validates the pattern. Expect to see a “skills package manager” emerge soon.

**RAG is now table stakes, but memory is the new frontier**  
Vector databases and RAG frameworks (RAGFlow, LlamaIndex, Milvus) remain the most starred topic-search category, but the exciting shift is toward **persistent, agent-native memory**. Projects like `mem0ai/mem0` (58k★) and `thedotmack/claude-mem` (81k★) propose a universal memory layer that survives across agent sessions. This suggests that the bottleneck is no longer retrieval accuracy but **context continuity**.

**Training from scratch and fine-tuning tools gain renewed attention**  
`train-llm-from-scratch` (+247 today) and `tiny-llm` (4k★) indicate that the community wants to understand and reproduce LLMs, not just consume APIs. Combined with the continued dominance of LlamaFactory (72k★), the ecosystem is maturing toward **decentralized model building**.

**Agent orchestration goes “one brain to rule them all”**  
`hivemind` (+64) and `superpowers` (+1104) introduce a centralized controller that coordinates multiple sub-agents. This mirrors enterprise multi-agent architectures and suggests that the next wave of AI tools will treat agent swarms as first-class citizens.

**Connection to recent industry events**  
The surge in agent skills correlates with the release of Claude Code, Codex, and similar coding agents that support plugin-like extensibility. The community is rapidly filling the gap for reusable, tested capabilities. Additionally, Apple’s container tool (+1611) – while not AI itself – lowers the barrier for running AI workloads on macOS, potentially enabling local LLM deployments on consumer hardware.

## Community Hot Spots

- **Agent Skills & Skills Marketplaces** — The `agent-skills`, `pm-skills`, and `last30days-skill` repos are the hottest new pattern. Developers should watch for standardisation (e.g., a skills descriptor format) and experiment with writing their own skills for Claude Code / Codex.

- **Agent-Native Memory Systems** — `mem0` and `claude-mem` are pioneering persistent context. Any developer building conversational AI or long-running agents should evaluate these as a replacement for ad-hoc context windows.

- **RAG + Knowledge Graphs** — Projects like `graphify` (65k★) and `cognee` (17k★) blend RAG with graph-based reasoning. This hybrid approach improves multi-hop question answering and is gaining traction in enterprise settings.

- **On-Device LLM Inference** — `picollm` (312★) and the iOS-focused `tiny-llm` course highlight a push toward running LLMs on edge devices. With Apple’s container tool enabling Linux VMs on Macs, the infrastructure for local AI is converging.

- **AI for Vertical Domains** — `openmed` (healthcare, +527 today) and `RuView` (WiFi sensing, +420 today) show that specialised AI applications are attracting significant attention. Developers with domain expertise can find underserved niches.

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*