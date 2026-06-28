# AI Open Source Trends 2026-06-28

> Sources: GitHub Trending + GitHub Search API | Generated: 2026-06-28 03:25 UTC

---

# AI Open Source Trends Report – 2026-06-28

## Step 1: AI Relevance Filter

**Excluded as non-AI** (from Trending list):
- simplex-chat, CasaOS, free-for-dev, microsoft/PowerToys, NanmiCoder/MediaCrawler, dbt-core, keycloak, every-app/open-seo, ripienaar/free-for-dev

**Excluded from Topic Search** (general CS resources, non-AI tools):
- Developer-Y/cs-video-courses (general education list)

All other projects in the combined data are retained as AI/ML related.

---

## Step 2: Categorization

### 🔧 AI Infrastructure (frameworks, SDKs, inference engines, dev tools, CLI)
- vllm-project/vllm – high-throughput LLM inference
- ollama/ollama – local model runner
- langchain-ai/langchain – agent engineering platform
- langchain4j/langchain4j – Java LLM app library
- open-webui/open-webui – AI interface layer
- firecrawl/firecrawl – web data API for agents
- browser-use/browser-use – website accessibility for agents
- rig (0xPlaygrounds/rig) – Rust LLM framework
- samchon/nestia – NestJS + AI chatbot
- raw-labs/mxcp – data-to-AI infrastructure
- LancerLab/croqtile – AI-native kernel DSL

### 🤖 AI Agents / Workflows
- NousResearch/hermes-agent – general-purpose agent
- shareAI-lab/learn-claude-code – Claude Code harness
- santifer/career-ops – AI job search system
- CherryHQ/cherry-studio – multi-assistant studio
- zhayujie/CowAgent – super AI assistant
- HKUDS/nanobot – lightweight agent
- CopilotKit/CopilotKit – frontend agent stack
- anomalyco/opencode – open-source coding agent
- garrytan/gstack – opinionated Claude Code toolchain
- jackwener/OpenCLI – website-to-CLI for agents
- iOfficeAI/AionUi – cowork app for multiple CLI agents
- Significant-Gravitas/AutoGPT – autonomous agent
- OpenHands/OpenHands – AI-driven development
- bytedance/deer-flow – long-horizon SuperAgent
- TauricResearch/TradingAgents – multi-agent trading
- xbtlin/ai-berkshire – multi-agent value investing
- HKUDS/Vibe-Trading – personal trading agent
- ZhuLinsen/daily_stock_analysis – LLM stock analysis
- googleworkspace/cli – Google Workspace with AI skills
- HRI-EU/tulip_agent – autonomous agent with tool library
- luongnv89/claude-howto – visual Claude Code guide
- Fission-AI/OpenSpec – spec-driven development for AI assistants
- google-labs-code/design.md – design system specification for agents

### 📦 AI Applications
- hugohe3/ppt-master – AI PowerPoint generation
- JCodesMore/ai-website-cloner-template – one-command website cloning
- Anil-matcha/Open-Generative-AI – unrestricted AI video/image studio
- commaai/openpilot – robotics OS for driver assistance
- OpenBB-finance/OpenBB – financial data platform for AI agents
- ultralytics/ultralytics – YOLO object detection
- deepfakes/faceswap – deepfake software
- ScrapeGraphAI/Scrapegraph-ai – AI-based web scraper
- Panniantong/Agent-Reach – web reading agent for 8 platforms
- Gitlawb/openclaude – universal agent runner

### 🧠 LLMs / Training
- pytorch/pytorch – tensor computation & neural networks
- tensorflow/tensorflow – ML framework
- keras-team/keras – deep learning API
- scikit-learn/scikit-learn – classic ML
- huggingface/transformers – state-of-the-art model framework
- vllm-project/vllm – LLM inference engine (also infra)
- open-compass/opencompass – LLM evaluation
- llm-jp/awesome-japanese-llm – Japanese LLM overview
- zjunlp/LightThinker – step-by-step compression for LLMs
- thinkwee/AwesomeOPD – on-policy distillation
- galilai-group/stable-pretraining – foundation model pretraining
- Anil-matcha/Awesome-GPT-5.6-API-and-Prompts – GPT-5.6 API guide
- testtimescaling/testtimescaling.github.io – test-time scaling survey
- R-D-BioTech-Alaska/Qelm – quantum-enhanced language models
- AmirMotefaker/Create-your-own-ChatGPT – DIY ChatGPT
- affaan-m/ECC – agent harness performance optimization
- f/prompts.chat – prompt sharing platform
- langgenius/dify – agentic workflow platform

### 🔍 RAG / Knowledge
- infiniflow/ragflow – RAG engine with agents
- milvus-io/milvus – vector database
- qdrant/qdrant – vector search engine
- weaviate/weaviate – cloud-native vector database
- lancedb/lancedb – embedded multimodal retrieval
- meilisearch/meilisearch – hybrid search engine
- oramasearch/orama – browser-based search/RAG
- alibaba/zvec – lightweight vector DB
- mem0ai/mem0 – universal memory layer
- topoteretes/cognee – AI memory platform with knowledge graphs
- thedotmack/claude-mem – persistent context across sessions
- safishamsi/graphify – code-to-knowledge graph
- VectifyAI/PageIndex – document index for reasoning RAG
- StarTrail-org/LEANN – private, storage-saving RAG
- zilliztech/claude-context – code search MCP
- headroomlabs-ai/headroom – token compression for RAG
- neuml/txtai – all-in-one AI framework
- FlowiseAI/Flowise – visual agent builder
- Mintplex-Labs/anything-llm – local-first agent experience
- datawhalechina/hello-agents – agent tutorial
- jeecgboot/JeecgBoot – AI low-code platform
- PaddlePaddle/PaddleOCR – OCR for document-to-structured-data
- run-llama/llama_index – document agent & OCR
- siyuan-note/siyuan – privacy-first knowledge management

---

## Step 3: Output Report

### 1. Today's Highlights

The AI open-source ecosystem is experiencing explosive growth in **coding agent toolchains** and **persistent memory layers**. `opencode` (392 stars today) and `design.md` (1,541 stars today) represent two emerging paradigms: open-source agent building and specification-driven development for AI coders. Meanwhile, `cognee` (780 stars today) and `claude-mem` (84,760 total, trending) signal a community-wide shift toward **long-term memory** as a first-class primitive for agents. The intersection of finance and multi-agent systems is also red-hot, with `ai-berkshire` (685 stars today) and `Vibe-Trading` (92 stars today) bringing structured investment frameworks to agent research. A notable newcomer is `garrytan/gstack` (674 stars today), packaging 23 opinionated Claude Code tools into a CEO-in-a-box workflow.

### 2. Top Projects by Category

#### 🔧 AI Infrastructure

- **[ollama/ollama](https://github.com/ollama/ollama)** – ⭐175,008 total. Local model runner now supporting Kimi-K2.6, GLM-5.1, and other frontier models; the de facto standard for local LLM deployment.
- **[vllm-project/vllm](https://github.com/vllm-project/vllm)** – ⭐84,593 total. High-throughput inference engine powering most production LLM deployments.
- **[langchain-ai/langchain](https://github.com/langchain-ai/langchain)** – ⭐140,349 total. The premier agent engineering platform; continues to evolve as the LLM application backbone.
- **[firecrawl/firecrawl](https://github.com/firecrawl/firecrawl)** – ⭐140,073 total. The API that makes web data accessible to agents at scale; essential infrastructure for agent-based web interaction.
- **[browser-use/browser-use](https://github.com/browser-use/browser-use)** – ⭐100,993 total. Making websites AI-agent-friendly; critical for automating browser-based workflows.
- **[google-labs-code/design.md](https://github.com/google-labs-code/design.md)** – ⭐0 (+1,541 today). A format specification giving coding agents persistent design system understanding; today's breakout infrastructure project.
- **[0xPlaygrounds/rig](https://github.com/0xPlaygrounds/rig)** – ⭐7,768 total. Modular LLM application framework in Rust; gaining traction for performance-sensitive agent workloads.

#### 🤖 AI Agents / Workflows

- **[NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent)** – ⭐204,412 total. "The agent that grows with you" — the most-starred dedicated agent project; embodies the self-evolving agent philosophy.
- **[CopilotKit/CopilotKit](https://github.com/CopilotKit/CopilotKit)** – ⭐35,581 total. Frontend stack for agents and generative UI across React, Angular, Mobile; makers of the AG-UI Protocol.
- **[OpenHands/OpenHands](https://github.com/OpenHands/OpenHands)** – ⭐78,519 total. AI-driven development platform; one of the most active coding agent communities.
- **[anomalyco/opencode](https://github.com/anomalyco/opencode)** – ⭐0 (+392 today). Open-source coding agent; positioned as a direct alternative to Claude Code and Codex.
- **[garrytan/gstack](https://github.com/garrytan/gstack)** – ⭐0 (+674 today). 23 opinionated Claude Code tools packaged as CEO, Designer, Eng Manager, Release Manager, Doc Engineer, and QA — a complete software development agent team.
- **[bytedance/deer-flow](https://github.com/bytedance/deer-flow)** – ⭐75,069 total. Long-horizon SuperAgent from ByteDance; handles tasks spanning minutes to hours with sandboxes, memory, and subagents.
- **[xbtlin/ai-berkshire](https://github.com/xbtlin/ai-berkshire)** – ⭐0 (+685 today). Multi-agent value investing framework built on four master methodologies; demonstrates agents as structured financial analysts.
- **[TauricResearch/TradingAgents](https://github.com/TauricResearch/TradingAgents)** – ⭐89,175 total. Multi-agent financial trading framework; the leading open-source project for agent-based quantitative strategies.

#### 📦 AI Applications

- **[hugohe3/ppt-master](https://github.com/hugohe3/ppt-master)** – ⭐33,174 total (+589 today). AI generates real, editable PowerPoint files from any document with native shapes, animations, and audio narration — a concrete productivity win.
- **[commaai/openpilot](https://github.com/commaai/openpilot)** – ⭐0 (+322 today). Operating system for robotics upgrading driver assistance on 300+ supported cars; the most mature open-source autonomous driving project.
- **[Anil-matcha/Open-Generative-AI](https://github.com/Anil-matcha/Open-Generative-AI)** – ⭐0 (+255 today). Unrestricted alternative to AI video platforms with 200+ models; self-hosted, MIT-licensed.
- **[Ultralytics/ultralytics](https://github.com/ultralytics/ultralytics)** – ⭐58,887 total. YOLO object detection — the foundation for countless real-world computer vision applications.
- **[OpenBB-finance/OpenBB](https://github.com/OpenBB-finance/OpenBB)** – ⭐69,767 total. Financial data platform for analysts, quants, and AI agents; bridges quantitative finance with agentic workflows.

#### 🧠 LLMs / Training

- **[huggingface/transformers](https://github.com/huggingface/transformers)** – ⭐161,977 total. The model-definition framework for state-of-the-art ML models; an ecosystem unto itself.
- **[pytorch/pytorch](https://github.com/pytorch/pytorch)** – ⭐101,067 total. De facto training framework for most modern LLM research.
- **[open-compass/opencompass](https://github.com/open-compass/opencompass)** – ⭐7,126 total. Comprehensive LLM evaluation platform supporting 100+ datasets; essential for model benchmarking.
- **[galilai-group/stable-pretraining](https://github.com/galilai-group/stable-pretraining)** – ⭐269 total. Minimal, scalable pretraining library for foundation and world models; represents emerging research infrastructure.
- **[zjunlp/LightThinker](https://github.com/zjunlp/LightThinker)** – ⭐164 total. EMNLP 2025 paper implementing step-by-step compression for LLMs; addresses the reasoning-efficiency tradeoff.

#### 🔍 RAG / Knowledge

- **[infiniflow/ragflow](https://github.com/infiniflow/ragflow)** – ⭐83,749 total. Leading open-source RAG engine combining retrieval with agent capabilities; the most comprehensive RAG system.
- **[milvus-io/milvus](https://github.com/milvus-io/milvus)** – ⭐44,983 total. Cloud-native vector database for scalable ANN search; production standard for vector storage.
- **[topoteretes/cognee](https://github.com/topoteretes/cognee)** – ⭐24,064 total (+780 today). Open-source AI memory platform with knowledge graph engine; addresses the critical gap of persistent long-term memory for agents.
- **[mem0ai/mem0](https://github.com/mem0ai/mem0)** – ⭐59,601 total. Universal memory layer for AI agents; the most popular standalone memory solution.
- **[thedotmack/claude-mem](https://github.com/thedotmack/claude-mem)** – ⭐84,760 total. Captures, compresses, and injects session context across agents; solves context persistence for Claude Code, Codex, Hermes, and more.
- **[safishamsi/graphify](https://github.com/safishamsi/graphify)** – ⭐73,008 total. Converts code, SQL schemas, docs, and media into queryable knowledge graphs; bridges code understanding with RAG.
- **[headroomlabs-ai/headroom](https://github.com/headroomlabs-ai/headroom)** – ⭐52,640 total. Compresses tool outputs and RAG chunks by 60-95% with minimal answer degradation; addresses the token budget bottleneck.

### 3. Trend Signal Analysis

**Explosive attention centers on coding agent orchestration and persistent memory.** The simultaneous rise of `opencode`, `design.md`, `gstack`, and `claude-mem` signals a community embracing **specification-driven agent workflows**. Rather than treating agents as chatbots, developers are defining precise protocols (DESIGN.md, OpenSpec, AG-UI Protocol) that govern how AI interacts with codebases, design systems, and user interfaces. This represents a maturation of the agent paradigm from "chat with code" to "structured collaboration with defined roles and outputs."

**Memory as infrastructure** is the most significant emerging direction. `cognee` (780 stars today) and `claude-mem` (84,760 total) both attack the same fundamental limitation: agents forget between sessions. The knowledge graph approach in `cognee` and the compression-based approach in `claude-mem` represent two competing architectures, suggesting this will be a vibrant debate in coming months.

**The AI + finance vertical is exploding.** `ai-berkshire`, `Vibe-Trading`, `TradingAgents` (89,175 total), and `ZhuLinsen/daily_stock_analysis` all reflect a pattern: multi-agent systems applying structured investment methodologies. The combination of Claude Code capabilities, real-time market data, and agentic reasoning is producing a new class of "analyst agents" that may fundamentally change how quantitative research is conducted.

**Token optimization is becoming critical infrastructure.** `headroom` (52,640 total) and `LightThinker` (164, but research signal) both address the same constraint: context windows are finite, and agent loops are token-expensive. Expect token compression and selective recall to become standard components in every agent stack.

**Multi-agent "teams" with defined roles** are replacing monolithic agents. `gstack`'s 23 tools acting as CEO, Designer, QA, etc., and `deer-flow`'s subagent architecture both demonstrate that the field is converging on specialized, cooperating agents rather than single-generalist agents.

### 4. Community Hot Spots

- **🤖 [opencode](https://github.com/anomalyco/opencode) (+392 today)** – The open-source coding agent directly challenging Claude Code and Codex. Its rapid growth suggests strong demand for a transparent, community-governed alternative to proprietary coding assistants. Developers should watch its plugin system and model-agnostic design.

- **🧠 [cognee](https://github.com/topoteretes/cognee) (+780 today)** – The AI memory platform using knowledge graphs for persistent agent memory. With knowledge graphs gaining traction as the preferred memory architecture (vs. simple vector embeddings), cognee's self-hosted, graph-native approach is a bet worth evaluating for any agent-heavy stack.

- **📐 [design.md](https://github.com/google-labs-code/design.md) (+1,541 today)** – Google Labs' format specification for visual identity description to coding agents. This is the most explosive new project today. It codifies a new pattern: giving agents structured, persistent design system awareness. Could become the standard for how agents understand visual consistency.

- **💼 [gstack](https://github.com/garrytan/gstack) (+674 today)** – Garry Tan's opinionated Claude Code setup with 23 specialized tools. This "startup-in-a-box" approach is notable for defining agent roles (CEO, Designer, Eng Manager) rather than just tools. Developers building multi-agent systems should study how role specialization improves output quality.

- **🔥 [headroomlabs-ai/headroom](https://github.com/headroomlabs-ai/headroom) (52,640 total)** – Token compression for agents, reducing costs 60-95%. As agent loops grow more complex, token management becomes a bottleneck. Headroom's approach of compressing before the LLM sees context is pragmatic and immediately applicable. Every agent developer should evaluate this for cost control.

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*