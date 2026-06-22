# AI Open Source Trends 2026-06-22

> Sources: GitHub Trending + GitHub Search API | Generated: 2026-06-22 03:50 UTC

---

# AI Open Source Trends Report — 2026-06-22

## 1. Today's Highlights

Token optimization and agent memory infrastructure dominate today's trending repos. **Headroom** (+2,624 ⭐ today) leads the pack with a novel approach to pre-LLM compression, slashing token usage by 60–95% without sacrificing answer quality. ByteDance’s **DeerFlow** (72,693 total ⭐, +442 today) extends the SuperAgent paradigm with sandboxed long-horizon task execution, while **Codebase-Memory-MCP** (+1,032 ⭐ today) sets a new bar for code intelligence by indexing repositories into a persistent knowledge graph in milliseconds. The explosive growth of **System Prompts Leaks** (+282 ⭐ today) and structured agent skill libraries (e.g., **Anthropic-Cybersecurity-Skills**, **mattpocock/skills**) signals a shift toward transparent, reusable agent building blocks. In the application layer, **OpenMontage** (+987 ⭐ today) claims the "world's first open-source agentic video production system," merging AI coding assistants with full video studio capabilities.

---

## 2. Top Projects by Category

### 🔧 AI Infrastructure

- **[Headroom](https://github.com/chopratejas/headroom)** — Python, 44,861 total ⭐ (+2,624 today)  
  Compresses tool outputs, logs, and RAG chunks before they reach the LLM, achieving 60–95% token reduction with identical answers. Available as a library, proxy, and MCP server.

- **[Codebase-Memory-MCP](https://github.com/DeusData/codebase-memory-mcp)** — C, total ⭐ (+1,032 today)  
  High-performance MCP server that indexes codebases into a persistent knowledge graph. Supports 158 languages, sub‑ms queries, and requires 99% fewer tokens. Single static binary, zero dependencies.

- **[Rig](https://github.com/0xPlaygrounds/rig)** — Rust, 7,705 total ⭐  
  Modular LLM application framework in Rust, enabling scalable and type‑safe agent pipelines.

- **[OpenCompass](https://github.com/open-compass/opencompass)** — Python, 7,109 total ⭐  
  Comprehensive LLM evaluation platform supporting 100+ datasets and model families (Llama, Mistral, GPT‑4, Qwen, etc.).

- **[vllm-project/vllm](https://github.com/vllm-project/vllm)** — Python, 83,507 total ⭐  
  High‑throughput, memory‑efficient LLM inference and serving engine.

- **[System Prompts Leaks](https://github.com/asgeirtj/system_prompts_leaks)** — JavaScript, total ⭐ (+282 today)  
  Curated collection of extracted system prompts from Claude, GPT‑5.5, Gemini, Grok, and many more – updated regularly.

### 🤖 AI Agents / Workflows

- **[DeerFlow](https://github.com/bytedance/deer-flow)** — Python, 72,693 total ⭐ (+442 today)  
  ByteDance’s open‑source SuperAgent harness for long‑horizon tasks (research, coding, creation). Uses sandboxes, memories, tools, subagents, and a message gateway. Tasks span minutes to hours.

- **[OpenMontage](https://github.com/calesthio/OpenMontage)** — Python, total ⭐ (+987 today)  
  World's first open‑source agentic video production system: 12 pipelines, 52 tools, 500+ agent skills. Turns any AI coding assistant into a full video studio.

- **[NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent)** — Python, 199,142 total ⭐  
  A growable agent framework that supports persistent memory, skill learning, and multi‑model routing.

- **[Anthropic-Cybersecurity-Skills](https://github.com/mukul975/Anthropic-Cybersecurity-Skills)** — Python, total ⭐ (+361 today)  
  754 structured cybersecurity skills for AI agents, mapped to MITRE ATT&CK, NIST CSF 2.0, D3FEND, and more. Compatible with Claude Code, Copilot, Cursor, Gemini CLI, and 20+ platforms.

- **[CowAgent](https://github.com/zhayujie/CowAgent)** — Python, 45,521 total ⭐  
  Lightweight, open‑source super AI assistant and agent harness with task planning, tool use, memory, and self‑evolution. Multi‑model, multi‑channel.

- **[TradingAgents](https://github.com/TauricResearch/TradingAgents)** — Python, 87,853 total ⭐  
  Multi‑agent LLM framework for financial trading, combining research, analysis, and execution agents.

- **[browser-use/browser-use](https://github.com/browser-use/browser-use)** — Python, 99,966 total ⭐  
  Makes websites accessible for AI agents, enabling autonomous online task automation.

### 📦 AI Applications

- **[Palmier Pro](https://github.com/palmier-io/palmier-pro)** — Swift, total ⭐ (+1,834 today)  
  macOS video editor purpose‑built for AI; integrates agentic video production workflows natively on Apple Silicon.

- **[Daily Stock Analysis](https://github.com/ZhuLinsen/daily_stock_analysis)** — Python, 44,779 total ⭐ (+568 today)  
  LLM‑driven multi‑market stock analysis system with real‑time news, decision dashboards, and automated push notifications. Runs cost‑free on schedule.

- **[WorldMonitor](https://github.com/koala73/worldmonitor)** — TypeScript, total ⭐ (+163 today)  
  Real‑time global intelligence dashboard with AI‑powered news aggregation, geopolitical monitoring, and infrastructure tracking.

- **[CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio)** — TypeScript, 47,635 total ⭐  
  AI productivity studio with smart chat, autonomous agents, and 300+ assistants. Unified access to frontier LLMs.

- **[Career-Ops](https://github.com/santifer/career-ops)** — JavaScript, 55,081 total ⭐  
  AI‑powered job search system built on Claude Code. Includes 14 skill modes, Go dashboard, PDF generation, batch processing.

### 🧠 LLMs / Training

- **[HuggingFace Transformers](https://github.com/huggingface/transformers)** — Python, 161,781 total ⭐  
  De‑facto standard library for state‑of‑the‑art ML models across text, vision, audio, and multimodal domains.

- **[OpenHands](https://github.com/OpenHands/OpenHands)** — Python, 77,946 total ⭐  
  AI‑driven development environment – a coding agent that plans, writes, debugs, and deploys code autonomously.

- **[ollama/ollama](https://github.com/ollama/ollama)** — Go, 174,689 total ⭐  
  Local LLM runner supporting Kimi‑K2.6, GLM‑5.1, DeepSeek, Qwen, Gemma, and many more models.

- **[Stable-Pretraining](https://github.com/galilai-group/stable-pretraining)** — Python, 266 total ⭐  
  Minimal, scalable library for pretraining foundation and world models with reproducible pipelines.

- **[Awesome-LLM-Unlearning](https://github.com/chrisliu298/awesome-llm-unlearning)** — 598 total ⭐  
  Curated resource for machine unlearning in large language models – a rapidly growing research area.

### 🔍 RAG / Knowledge

- **[RAGFlow](https://github.com/infiniflow/ragflow)** — Python, 83,309 total ⭐  
  Leading open‑source RAG engine combining retrieval, agent capabilities, and a superior context layer for LLMs.

- **[Milvus](https://github.com/milvus-io/milvus)** — Go, 44,878 total ⭐  
  High‑performance, cloud‑native vector database for scalable ANN search. Core component for production RAG.

- **[Mem0](https://github.com/mem0ai/mem0)** — Python, 59,067 total ⭐  
  Universal memory layer for AI agents – persists and retrieves contextual knowledge across sessions.

- **[Cognee](https://github.com/topoteretes/cognee)** — Python, 18,715 total ⭐ (+347 today)  
  Self‑hosted knowledge graph engine providing persistent long‑term memory for agents. Also trending today.

- **[Qdrant](https://github.com/qdrant/qdrant)** — Rust, 32,535 total ⭐  
  Massive‑scale vector database and search engine, built for next‑gen AI workloads.

- **[Claude-Mem](https://github.com/thedotmack/claude-mem)** — JavaScript, 83,601 total ⭐  
  Captures agent session context, compresses it with AI, and injects relevant context into future sessions. Works with Claude Code, OpenClaw, Codex, and more.

- **[Graphify](https://github.com/safishamsi/graphify)** — Python, 70,365 total ⭐  
  AI coding assistant skill that turns any codebase, SQL schema, or documents into a queryable knowledge graph. Supports Claude Code, Codex, Cursor, Gemini CLI.

---

## 3. Trend Signal Analysis

Today’s hot list reveals three converging trends: **token economy**, **agent memory as infrastructure**, and **standardized agent skills**.

**Token compression** has exploded into the spotlight with **Headroom** (+2,624 ⭐), targeting the single biggest cost in LLM pipelines: context window waste. Its 60–95% reduction claim, validated by community testing, suggests a commoditization path for pre-processing layers – expect similar tools to proliferate as MCP servers and proxy middleware.  

**Agent memory** is no longer an afterthought. **Codebase-Memory-MCP** (sub‑ms code graph), **Cognee** (knowledge graph engine), and **Claude-Mem** (session compression) each offer distinct persistence strategies, all trending strongly. Their emergence indicates that the community sees ephemeral chat‑based agents as insufficient; persistent, structured memory is becoming a baseline requirement for production agents.  

**Structured agent skills** – exemplified by **Anthropic-Cybersecurity-Skills** (754 skills, framework‑mapped) and **mattpocock/skills** (from `.claude` directories) – point to a maturing ecosystem where skills are versioned, shareable, and platform‑agnostic. The `agentskills.io` standard mentioned in the cybersecurity repo may become a de‑facto interchange format.  

Finally, **System Prompts Leaks** (+282 ⭐ today) reflects growing demand for transparency into how top labs (Anthropic, OpenAI, Google, xAI) configure their models. This public benchmarking of system prompts enables the community to reverse‑engineer behaviors and build better agents.  

Notable absence: pure model‑weight releases. Today’s energy is overwhelmingly on tooling, agents, and memory – not new foundation models. The release of **DeerFlow** from ByteDance also signals that large tech companies are investing in agent orchestration frameworks rather than keeping them proprietary.

---

## 4. Community Hot Spots

- **[Headroom](https://github.com/chopratejas/headroom)** — Token compression is the most actionable optimization for anyone running LLM pipelines. Watch for its MCP server becoming a default plugin in agent frameworks.
- **[Codebase-Memory-MCP](https://github.com/DeusData/codebase-memory-mcp)** — With sub‑ms queries and 158 language support, this could redefine how coding agents understand repositories. Its zero‑dependency single binary makes adoption trivial.
- **[Anthropic-Cybersecurity-Skills](https://github.com/mukul975/Anthropic-Cybersecurity-Skills)** — The first attempt to map enterprise security frameworks (MITRE, NIST) into a reusable skill set for AI agents. Expect similar “curriculum” projects for other domains (finance, healthcare, legal) to follow.
- **[System Prompts Leaks](https://github.com/asgeirtj/system_prompts_leaks)** — A living reference for developers to understand model capabilities and constraints. Essential reading for anyone building prompt‑dependent applications.
- **[OpenMontage](https://github.com/calesthio/OpenMontage)** — Merges the worlds of AI agents and video production. Its 500+ agent skills and pipeline architecture could inspire similar creative‑tool integrations (audio, 3D, design).

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*