# AI Open Source Trends 2026-07-26

> Sources: GitHub Trending + GitHub Search API | Generated: 2026-07-26 02:25 UTC

---

# AI Open Source Trends Report – 2026-07-26

## 1. Today’s Highlights

Today’s GitHub trending data reveals a strong community appetite for **agentic tooling and developer productivity** in the AI space. The most explosive star gains belong to two agent‑framework projects: `alphamoon/ECC` (+377 today) and `mattpocock/skills` (+1 740), both of which define skill‑execution harnesses for CLI‑based coding agents like Claude Code and Codex. Meanwhile, `citrolabs/ego-lite` (+986) – a browser purpose‑built for AI agents to share logged‑in state – signals a shift toward infrastructure that treats agents as first‑class web users. On the model side, `shiyu-coder/Kronos` (+319) introduces a dedicated foundation model for financial markets, and `andrewyng/aisuite` (+77) solidifies a unified provider abstraction. The overall trend points to a maturing open‑source ecosystem where agent contexts, memory, and browser control are becoming essential primitives.

## 2. Top Projects by Category

### 🔧 AI Infrastructure
- **[aisuite](https://github.com/andrewyng/aisuite)** – Python, ⭐77 (+77 today)  
  Simple, unified interface to multiple Generative AI providers – reduces vendor lock‑in for developer workflows.  
- **[alibaba/open-code-review](https://github.com/alibaba/open-code-review)** – Go, ⭐431 (+431 today)  
  Battle‑tested hybrid code review tool combining deterministic pipelines with LLM agents; outputs line‑level NPE, XSS, SQL injection findings.  
- **[vllm-project/vllm](https://github.com/vllm-project/vllm)** – Python, ⭐87,153  
  High‑throughput, memory‑efficient LLM inference engine – the de‑facto serving layer for many open‑source models.  
- **[ollama/ollama](https://github.com/ollama/ollama)** – Go, ⭐176,893  
  Get up and running with frontier models (Kimi‑K2.6, DeepSeek, Qwen, etc.) locally – now supports 30+ model families.  
- **[firecrawl/firecrawl](https://github.com/firecrawl/firecrawl)** – TypeScript, ⭐156,017  
  Turn‑key web scraping and search API designed for LLM data ingestion – used by thousands of AI agents.

### 🤖 AI Agents / Workflows
- **[affaan-m/ECC](https://github.com/affaan-m/ECC)** – JavaScript, ⭐233,339 (+377 today)  
  Agent harness with skills, instinct, memory, and security – integrated with Claude Code, Codex, Cursor, and OpenCode.  
- **[mattpocock/skills](https://github.com/mattpocock/skills)** – Shell, ⭐1,740 (+1 740 today)  
  Curated `.agents` directory of reusable skills for real‑world engineering tasks, directly importable into agent CLIs.  
- **[citrolabs/ego-lite](https://github.com/citrolabs/ego-lite)** – JavaScript, ⭐986 (+986 today)  
  The fastest browser for AI agents – shares your logged‑in browser state so agents can automate web tasks without disturbing you.  
- **[obra/superpowers](https://github.com/obra/superpowers)** – Shell, ⭐479 (+479 today)  
  An agentic skills framework and software development methodology that treats agent interaction as a first‑class practice.  
- **[NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent)** – Python, ⭐220,492  
  The agent that grows with you – a general‑purpose, memory‑aware agent built for long‑running sessions.  
- **[CopilotKit/CopilotKit](https://github.com/CopilotKit/CopilotKit)** – TypeScript, ⭐36,278  
  Frontend stack for building generative UI and agentic chat into React, Angular, and mobile apps – makers of the AG‑UI Protocol.

### 📦 AI Applications
- **[shiyu-coder/Kronos](https://github.com/shiyu-coder/Kronos)** – Python, ⭐319 (+319 today)  
  A foundation model for the language of financial markets, fine‑tuned to understand trading patterns and sentiment.  
- **[OtterMind/Chat2DB](https://github.com/OtterMind/Chat2DB)** – Java, ⭐360 (+360 today)  
  AI‑driven SQL client supporting MySQL, PostgreSQL, ClickHouse, and more – natural language to database queries.  
- **[palmier-io/palmier-pro](https://github.com/palmier-io/palmier-pro)** – Swift, ⭐412 (+412 today)  
  macOS video editor designed around AI – automates cutting, transitions, and audio narration.  
- **[Automattic/harper](https://github.com/Automattic/harper)** – Rust, ⭐503 (+503 today)  
  Offline, privacy‑first grammar checker powered by a lightweight neural model – fast and runs entirely on device.  
- **[CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio)** – TypeScript, ⭐48,986  
  AI productivity studio with smart chat, autonomous agents, and 300+ pre‑built assistants – unified access to frontier LLMs.  
- **[hugohe3/ppt-master](https://github.com/hugohe3/ppt-master)** – Python, ⭐41,093  
  AI turns documents into native PowerPoint decks with animations, charts, and audio narration – uses OpenAI/Claude.

### 🧠 LLMs / Training
- **[Lordog/dive-into-llms](https://github.com/Lordog/dive-into-llms)** – Jupyter Notebook, ⭐408 (+408 today)  
  Hands‑on Chinese‑language tutorial series for building LLMs from scratch – covers pre‑training, fine‑tuning, and inference.  
- **[jingyaogong/minimind](https://github.com/jingyaogong/minimind)** – Python, ⭐53,841  
  Train a 64M‑parameter LLM from scratch in 2 hours – a practical guide to understanding model internals.  
- **[skyzh/tiny-llm](https://github.com/skyzh/tiny-llm)** – Python, ⭐4,408  
  Systems‑engineering course: build a tiny vLLM + Qwen inference server on Apple Silicon – excellent for learning serving stacks.  
- **[open-compass/opencompass](https://github.com/open-compass/opencompass)** – Python, ⭐7,236  
  Comprehensive LLM evaluation platform supporting 100+ datasets and models (Llama, Qwen, GPT‑4, Claude).  
- **[thinkwee/AgentsMeetRL](https://github.com/thinkwee/AgentsMeetRL)** – HTML, ⭐1,723  
  Awesome list for agentic reinforcement learning – links recent work on RL for multi‑step reasoning and tool use.

### 🔍 RAG / Knowledge
- **[RyanCodrai/turbovec](https://github.com/RyanCodrai/turbovec)** – Python, ⭐86 (+86 today)  
  A vector index built on TurboQuant (Rust) – brings high‑performance quantized indexing to Python AI pipelines.  
- **[milvus-io/milvus](https://github.com/milvus-io/milvus)** – Go, ⭐45,381  
  Cloud‑native vector database for scalable ANN search – the backbone of many production RAG systems.  
- **[qdrant/qdrant](https://github.com/qdrant/qdrant)** – Rust, ⭐33,585  
  High‑performance vector search engine with rich filtering and payload support – both self‑hosted and cloud.  
- **[infiniflow/ragflow](https://github.com/infiniflow/ragflow)** – Go, ⭐85,996  
  Leading open‑source RAG engine combining retrieval with agent capabilities – used for deep document QA.  
- **[Graphify-Labs/graphify](https://github.com/Graphify-Labs/graphify)** – Python, ⭐95,894  
  Turn any codebase (docs, SQL, PDFs) into a queryable knowledge graph – no vector store needed, uses deterministic AST parsing.  
- **[cognee](https://github.com/topoteretes/cognee)** – Python, ⭐29,332  
  Open‑source AI memory platform for agents – persistent long‑term memory via a self‑hosted knowledge graph engine.

## 3. Trend Signal Analysis

Today’s data confirms that **agentic skill frameworks** are the breakout category, with projects like `ECC` and `mattpocock/skills` amassing thousands of stars in a single day. These harnesses define how AI coding tools (Claude Code, Codex, Cursor) discover, load, and execute reusable capabilities – turning ephemeral agent sessions into composable, stateful workflows. The explosive growth of `ego-lite` (+986 stars) underscores the community’s recognition that **browser‑aware agents** are the next frontier: giving agents the power to interact with real web interfaces (not just APIs) without user interruption.

A second clear trend is the **commoditisation of multimodal reading tools**. `Graphify-Labs/graphify` (95k+ stars) and `PaddleOCR` (86k+) are moving beyond simple vector search to make any structured data (code, PDFs, images) directly queryable by LLMs. This aligns with the rise of “vectorless” RAG – using deterministic parsing and graphs rather than dense embeddings – which may reduce costs and improve accuracy for enterprise knowledge bases.

On the model side, financial domain‑specific LLMs (`Kronos`) and ultra‑lightweight training guides (`dive-into-llms`, `minimind`) show that **specialisation and education** remain strong drivers. The absence of any new foundation model release on the trending list suggests the market is now focused on **operational tooling** rather than raw model announcements.

Finally, the “agent harness” pattern seen in `ECC`, `superpowers`, and `skills` points toward a standardised `.agents` directory convention – a potential de‑facto ecosystem standard for packaging agent capabilities. This is reminiscent of how `npm` packages transformed JavaScript, and could be the next major platform shift in open‑source AI development.

## 4. Community Hot Spots

- **`affaan-m/ECC` and `mattpocock/skills`** – The two top‑rising repositories today; define the emerging “agent skill” packaging standard. Developers building for Claude Code/Codex should study their `.agents` directory structures.
- **`citrolabs/ego-lite`** – A browser designed for AI agents that can share logged‑in state without disturbing users. A critical component for automating SaaS workflows and e‑commerce.
- **`Graphify-Labs/graphify`** – A “vectorless” knowledge graph that deterministically parses codebases and docs. Represents a new RAG paradigm that avoids embedding costs and hallucination risks.
- **`shiyu-coder/Kronos`** – A dedicated financial foundation model signals the growing appetite for domain‑specific LLMs trained on proprietary data, likely driven by hedge funds and trading desks.
- **`Lordog/dive-into-llms`** – Hands‑on Chinese tutorial series with high daily traction; indicates strong global demand for practical LLM engineering education, especially in Asia.

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*