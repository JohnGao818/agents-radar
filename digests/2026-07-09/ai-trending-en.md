# AI Open Source Trends 2026-07-09

> Sources: GitHub Trending + GitHub Search API | Generated: 2026-07-09 02:35 UTC

---

# AI Open Source Trends Report – 2026-07-09

## 1. Today's Highlights

Today marks a significant inflection point in the **Agent Skills ecosystem**, with two major frameworks—`addyosmani/agent-skills` and `superpowers`—collecting over 2,400 stars combined, signalling that the community is hungry for production-grade, reusable skill definitions that go beyond simple tool-calling. Meanwhile, **local-first AI infrastructure** continues to dominate: Tencent Cloud open-sourced two complementary projects (`TencentDB-Agent-Memory` and `CubeSandbox`) that together solve the memory and sandboxing problems for on-device agents, while `alibaba/zvec` re-emerges as a lightweight vector database contender. A notable surprise is the massive traction for `system_prompts_leaks` (1,218 stars today), revealing deep community interest in understanding how frontier labs like Anthropic, OpenAI, and Google are actually prompting their latest models. Finally, `OfficeCLI` (1,717 today) demonstrates that the **AI-for-productivity** space is moving from simple wrappers to full native binary tooling.

## 2. Top Projects by Category

### 🔧 AI Infrastructure (Frameworks, SDKs, Inference Engines, Dev Tools, CLI)

- **[addyosmani/agent-skills](https://github.com/addyosmani/agent-skills)** — ⭐0 (+1,297 today)  
  A production-grade library of reusable engineering skills for AI coding agents, providing pre-built capabilities (testing, debugging, refactoring) that agents can invoke directly.

- **[TencentCloud/CubeSandbox](https://github.com/TencentCloud/CubeSandbox)** — ⭐0 (+564 today)  
  A lightweight, concurrent sandbox system built in Rust specifically designed to run untrusted AI agent code securely and instantly.

- **[wonderwhy-er/DesktopCommanderMCP](https://github.com/wonderwhy-er/DesktopCommanderMCP)** — ⭐0 (+28 today)  
  An MCP (Model Context Protocol) server giving Claude full terminal control, file search, and diff-based editing capabilities—important for agentic IDE integration.

- **[asgeirtj/system_prompts_leaks](https://github.com/asgeirtj/system_prompts_leaks)** — ⭐0 (+1,218 today)  
  A continuously updated repository of extracted system prompts from major AI labs (Claude Opus 4.8, GPT 5.5, Gemini 3.5), offering rare transparency into how frontier models are configured.

- **[obra/superpowers](https://github.com/obra/superpowers)** — ⭐0 (+1,116 today)  
  An agentic skills framework and accompanying software development methodology, advocating for structured, composable agent behaviors.

- **[alibaba/zvec](https://github.com/alibaba/zvec)** — ⭐14,445 total (+395 today)  
  A lightweight, lightning-fast in-process vector database written in C++, designed for scenarios requiring minimal latency overhead in embedded AI applications.

### 🤖 AI Agents / Workflows (Agent Frameworks, Automation, Multi-Agent)

- **[NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent)** — ⭐211,640 total  
  The increasingly popular "agent that grows with you" — a self-improving, modular agent framework with persistent memory and skill acquisition.

- **[CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio)** — ⭐48,323 total  
  An AI productivity studio unifying smart chat, autonomous agents, and 300+ pre-built assistant personas across all major frontier LLMs.

- **[TencentCloud/TencentDB-Agent-Memory](https://github.com/TencentCloud/TencentDB-Agent-Memory)** — ⭐0 (+318 today)  
  A fully local long-term memory system for AI agents using a 4-tier progressive pipeline (transactional → episodic → semantic → procedural), zero external API calls.

- **[iOfficeAI/AionUi](https://github.com/iOfficeAI/AionUi)** — ⭐29,596 total  
  A free, local, open-source desktop companion for running Claude Code, Hermes Agent, Codex, Gemini CLI, and 20+ other agent CLIs with customizable assistant configurations.

### 📦 AI Applications (Specific Apps, Vertical Solutions)

- **[iOfficeAI/OfficeCLI](https://github.com/iOfficeAI/OfficeCLI)** — ⭐0 (+1,717 today)  
  The first purpose-built Office suite for AI agents: a single binary (no Office installation required) that reads, edits, and automates Word, Excel, and PowerPoint files programmatically.

- **[bradautomates/claude-video](https://github.com/bradautomates/claude-video)** — ⭐0 (+951 today)  
  Gives Claude the ability to watch any video by downloading, extracting frames, transcribing audio, and feeding it all into the model's context.

- **[ruvnet/RuView](https://github.com/ruvnet/RuView)** — ⭐0 (+799 today)  
  Turns commodity WiFi signals into real-time spatial intelligence, vital sign monitoring, and presence detection—no cameras needed. A novel AI-for-IoT application.

- **[mvanhorn/last30days-skill](https://github.com/mvanhorn/last30days-skill)** — ⭐0 (+352 today)  
  An AI agent skill that researches any topic across Reddit, X, YouTube, HN, Polymarket, and the web, then synthesizes a grounded, citation-based summary.

### 🧠 LLMs / Training (Model Weights, Training Frameworks, Fine-Tuning, Evaluation)

- **[open-compass/opencompass](https://github.com/open-compass/opencompass)** — ⭐7,174 total  
  Comprehensive LLM evaluation platform supporting 100+ datasets across all major models (Llama 3, Mistral, GPT-4, Qwen, Claude, etc.) — essential for model comparison.

- **[galilai-group/stable-pretraining](https://github.com/galilai-group/stable-pretraining)** — ⭐281 total  
  A minimal, reliable, and scalable library for pre-training foundation and world models, targeting reproducible training pipelines.

- **[vllm-project/vllm](https://github.com/vllm-project/vllm)** — ⭐85,741 total  
  The high-throughput, memory-efficient LLM inference engine powering most open-source deployments; continues to be the standard for serving.

- **[testtimescaling/testtimescaling.github.io](https://github.com/testtimescaling/testtimescaling.github.io)** — ⭐107 total  
  A comprehensive survey on test-time scaling in LLMs ("what, how, where, and how well") — timely as the industry shifts toward inference-compute optimization.

### 🔍 RAG / Knowledge (Vector Databases, Retrieval-Augmented Generation, Knowledge Management)

- **[run-llama/llama_index](https://github.com/run-llama/llama_index)** — ⭐50,741 total  
  The leading document agent and OCR platform for building RAG pipelines; foundational to the modern retrieval stack.

- **[milvus-io/milvus](https://github.com/milvus-io/milvus)** — ⭐45,139 total  
  High-performance, cloud-native vector database for scalable ANN search; the incumbent choice for production RAG.

- **[qdrant/qdrant](https://github.com/qdrant/qdrant)** — ⭐33,062 total  
  Rust-based vector database with massive scalability; increasingly favoured for latency-sensitive applications.

- **[topoteretes/cognee](https://github.com/topoteretes/cognee)** — ⭐27,371 total  
  Open-source AI memory platform that gives agents persistent long-term memory via a self-hosted knowledge graph engine — directly competing with the approach used in TencentDB-Agent-Memory.

- **[alibaba/zvec](https://github.com/alibaba/zvec)** — ⭐14,445 total  
  While categorised in Infrastructure, zvec also serves the RAG space as an ultra-lightweight in-process alternative to Milvus/Qdrant for edge and embedded use cases.

- **[VectifyAI/PageIndex](https://github.com/VectifyAI/PageIndex)** — ⭐33,883 total  
  A document index for "vectorless, reasoning-based RAG" — notable for challenging the assumption that vector embeddings are always necessary.

## 3. Trend Signal Analysis

**Agent Skills are the new "model weights."** The two highest-starred AI projects today (`agent-skills` and `superpowers`) share the thesis that AI coding agents need standardized, composable, and production-hardened capabilities akin to packages in npm or crates in Rust. This signals a maturation of the agent ecosystem: the community is moving past "make an agent that can call a function" toward "make a skill registry that agents can discover and import." Expect skill marketplaces to emerge within 6–12 months.

**Local-first, zero-API infrastructure is exploding.** Tencent Cloud released two projects (`TencentDB-Agent-Memory` and `CubeSandbox`) that together enable fully local agent memory and sandboxed execution without any cloud dependency. This aligns with the broader "AI that runs on your laptop" movement (AnythingLLM, Ollama). The combination of a 4-tier memory pipeline and instant sandboxing suggests Tencent is betting on enterprise adoption of local AI agents bound by strict data sovereignty requirements.

**Prompt engineering is becoming "prompt forensics."** The `system_prompts_leaks` repo (+1,218 stars) is not just a curiosity—it reveals that the community now treats system prompts as IP worth reverse-engineering. The project extracts prompts from Claude Fable 5, GPT 5.5, Gemini 3.5, and others, suggesting a growing sub-discipline of "prompt archaeology." This may pressure labs to better obfuscate or dynamically generate system prompts.

**Video and spatial AI are entering the agent context window.** `claude-video` and `RuView` both expand what agents can perceive: video comprehension (frames + transcription) and ambient WiFi signals (device-free sensing). These point to a future where agents ingest not just text and images but continuous media streams and sensor data.

**Potential connection to industry events**: The release of Claude Fable 5 (referenced in `system_prompts_leaks`) and the apparent availability of GPT 5.5 and Gemini 3.5 APIs likely happened within the past week, spurring the community to test agent capabilities on these new models and demand more sophisticated tooling.

## 4. Community Hot Spots

- **🆕 Agent Skills Registry (`addyosmani/agent-skills` and `obra/superpowers`)** — The most important emerging direction. Developers should watch for a de facto standard for skill packaging, similar to how GitHub Actions or Dockerfiles became repeatable artifacts.

- **🔐 Local Memory Architectures (`TencentDB-Agent-Memory`, `cognee`, `mem0`)** — With 3+ competing projects vying for "AI memory" dominance, the space is ripe for consolidation. The 4-tier pipeline approach (transactional → episodic → semantic → procedural) is especially novel.

- **📡 Multimodal Perception for Agents (`claude-video`, `RuView`, `browser-use`)** — Agents are breaking out of the text interface. Video understanding (1,000-minute+ context) and radio-frequency sensing represent the next frontier for autonomous agents in physical environments.

- **🪲 Prompt Forensics (`system_prompts_leaks`)** — For researchers and developers building on top of closed APIs, understanding the hidden system prompts is becoming essential for debugging and optimizing agent behavior. Expect more tools to detect, extract, and version-control prompts dynamically.

- **📝 Office Automation via Native Binary (`OfficeCLI`)** — The high star count today indicates strong pent-up demand for AI agents that can manipulate real Office documents (not just convert to Markdown). This could spark a wave of "agent-native" productivity tooling that bypasses traditional GUI automation entirely.

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*