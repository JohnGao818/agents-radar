# AI Open Source Trends 2026-06-29

> Sources: GitHub Trending + GitHub Search API | Generated: 2026-06-29 03:31 UTC

---

# AI Open Source Trends Report – 2026-06-29

## 1. Today’s Highlights

The open-source AI ecosystem is surging with **agent‑first infrastructure** and **vertical applications**. Today’s trending list is dominated by projects that connect LLMs to real‑world workflows: a code intelligence MCP server (*codebase‑memory‑mcp*) gained over 2,190 stars in a single day, while a multi‑agent value‑investing framework (*ai‑berkshire*) jumped 1,445 stars. The broader topic search reveals an explosion of **agent harnesses** (Hermes, Claude Code clones, OpenClaude) and **memory / RAG tooling** (Graphify, Headroom, Cognee). Finance AI agents (Vibe‑Trading, ai‑berkshire) and local‑first dictation (FluidVoice) also signal that the community is rapidly moving beyond chat to domain‑specific agent deployments.

## 2. Top Projects by Category

### 🔧 AI Infrastructure

| Project | Stars (total / today) | What & Why |
|--------|-----------------------|------------|
| [DeusData/codebase‑memory‑mcp](https://github.com/DeusData/codebase-memory-mcp) | 2,190 today | High‑performance MCP server that indexes codebases into a persistent knowledge graph in milliseconds, supporting 158 languages – a breakthrough for AI‑powered code intelligence. |
| [NousResearch/hermes‑agent](https://github.com/NousResearch/hermes-agent) | 205,074 | The fastest‑growing agent framework; fully integrated with Claude Code, Codex, and Gemini CLI, offering a “grows with you” skill‑based architecture. |
| [ollama/ollama](https://github.com/ollama/ollama) | 175,089 | Already the standard for local LLM serving; now supports Kimi‑K2.6, GLM‑5.1, and DeepSeek – the easiest way to run frontier models offline. |
| [cupy/cupy](https://github.com/cupy/cupy) | +174 today | NumPy/SciPy on GPU – essential for high‑performance ML computation, still actively maintained. |
| [vllm‑project/vllm](https://github.com/vllm-project/vllm) | 84,711 | High‑throughput inference engine for LLMs; the backbone of many cloud and on‑prem deployments. |

### 🤖 AI Agents / Workflows

| Project | Stars (total / today) | What & Why |
|--------|-----------------------|------------|
| [shareAI‑lab/learn‑claude‑code](https://github.com/shareAI-lab/learn-claude-code) | 68,840 | A “nano” agent harness built from scratch to mirror Claude Code – ideal for understanding agent internals. |
| [HKUDS/Vibe‑Trading](https://github.com/HKUDS/Vibe-Trading) | +492 today | Personal trading agent that leverages LLMs for market analysis; reflects growing finance AI interest. |
| [browser‑use/video‑use](https://github.com/browser-use/video-use) | +196 today | Edit videos using coding agents – a novel application of browser automation for creative tasks. |
| [bytedance/deer‑flow](https://github.com/bytedance/deer-flow) | 75,289 | Long‑horizon SuperAgent that researches, codes, and creates; uses sandboxed sub‑agents for tasks lasting minutes to hours. |
| [zhayujie/CowAgent](https://github.com/zhayujie/CowAgent) | 45,659 | Lightweight multi‑model agent harness with memory, skills, and self‑evolution – one‑line install (formerly chatgpt‑on‑wechat). |

### 📦 AI Applications

| Project | Stars (total / today) | What & Why |
|--------|-----------------------|------------|
| [xbtlin/ai‑berkshire](https://github.com/xbtlin/ai-berkshire) | +1,445 today | A multi‑agent value‑investing research framework using Claude Code / Codex – integrates four legendary investors’ methodologies. |
| [altic‑dev/FluidVoice](https://github.com/altic-dev/FluidVoice) | +365 today | Fastest macOS offline dictation app; 100% local, voice‑to‑text – a practical local‑first AI app. |
| [opendatalab/MinerU](https://github.com/opendatalab/MinerU) | +380 today | Transforms PDFs and Office docs into LLM‑ready markdown/JSON – critical for RAG pipelines. |
| [usestrix/strix](https://github.com/usestrix/strix) | +122 today | Open‑source AI hackers that find and fix app vulnerabilities – an automated security agent. |
| [Robbyant/lingbot‑map](https://github.com/Robbyant/lingbot-map) | +372 today | Feed‑forward 3D foundation model for reconstructing scenes from streaming data – advancing spatial AI. |

### 🧠 LLMs / Training

| Project | Stars (total / today) | What & Why |
|--------|-----------------------|------------|
| [jingyaogong/minimind](https://github.com/jingyaogong/minimind) | 52,295 | Train a 64M‑parameter LLM from scratch in just 2 hours – democratizing model training. |
| [hiyouga/LlamaFactory](https://github.com/hiyouga/LlamaFactory) | 72,704 | Unified fine‑tuning framework for 100+ LLMs and VLMs (ACL 2024) – the go‑to tool for custom models. |
| [Significant‑Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT) | 185,203 | The original autonomous agent project; still actively developed and inspiring new agent architectures. |
| [galilai‑group/stable‑pretraining](https://github.com/galilai-group/stable-pretraining) | 271 | Minimal, scalable library for pretraining foundation and world models – a research‑focused newcomer. |

### 🔍 RAG / Knowledge

| Project | Stars (total / today) | What & Why |
|--------|-----------------------|------------|
| [infiniflow/ragflow](https://github.com/infiniflow/ragflow) | 83,802 | Leading open‑source RAG engine that combines retrieval with agent capabilities for superior LLM context. |
| [safishamsi/graphify](https://github.com/safishamsi/graphify) | 73,779 | Turn any codebase, SQL schema, or docs into a queryable knowledge graph – bridges code and RAG. |
| [mem0ai/mem0](https://github.com/mem0ai/mem0) | 59,643 | Universal memory layer for AI agents; enables persistent context across sessions. |
| [headroomlabs‑ai/headroom](https://github.com/headroomlabs-ai/headroom) | 53,193 | Compress tool outputs, logs, and RAG chunks by 60–95% without losing answer quality – vital for cost‑efficient agents. |
| [milvus‑io/milvus](https://github.com/milvus-io/milvus) | 44,998 | Cloud‑native vector database for scalable ANN search; the infrastructure backbone for many RAG systems. |
| [topoteretes/cognee](https://github.com/topoteretes/cognee) | 24,957 | Self‑hosted knowledge graph engine providing persistent long‑term memory for AI agents – a rising RAG alternative. |

## 3. Trend Signal Analysis

The most explosive community attention today is around **agent infrastructure that bridges LLMs and developer tooling**. The MCP (Model Context Protocol) ecosystem is clearly emerging as a hot layer: *codebase‑memory‑mcp* (+2,190 stars) is a pure MCP server that turns codebases into queryable knowledge graphs, while *headroom* and *claude‑mem* focus on compressing and persisting agent context. This points to a growing desire for **standardized protocols** to connect agents with tools and data, similar to how LSP standardized language servers.

A new direction appearing for the first time in this data is **“agent harness” frameworks** that are model‑agnostic and skill‑centric. Projects like *learn‑claude‑code*, *CowAgent*, and *hermes‑agent* all expose a common pattern: a CLI‑first agent able to use multiple models, execute skills/tools, and maintain memory. The abundance of clones of Claude Code (OpenClaude, OpenCode, etc.) suggests that the community is rapidly commoditizing the agent interface.

In the finance vertical, both *Vibe‑Trading* and *ai‑berkshire* show that **multi‑agent adversarial analysis** for stock research is gaining traction. These projects leverage Claude Code / Codex to orchestrate multiple agents that debate and critique each other – a pattern that may soon spread to other domains (legal, medical).

Finally, the rise of **local‑first, private AI** continues: *FluidVoice* (offline dictation), *anywhere‑LLM* (local agent experience), and *cognee* (self‑hosted memory) all cater to the growing demand for privacy‑preserving AI without sacrificing functionality. This trend is reinforced by industry events like recent LLM releases (Kimi‑K2.6, GLM‑5.1) that are optimized for local deployment in Ollama.

## 4. Community Hot Spots

- **[codebase‑memory‑mcp](https://github.com/DeusData/codebase-memory-mcp)** – Explosive growth (+2,190 today) signals the MCP protocol is a critical new standard for code intelligence. Developers should watch how MCP servers evolve into a plug‑and‑play ecosystem.

- **[hermes‑agent](https://github.com/NousResearch/hermes-agent)** – At 205K stars, it’s the fastest‑scaling agent framework. Its “grows with you” philosophy and deep integration with multiple CLI agents make it a must‑follow for anyone building production agents.

- **[ai‑berkshire](https://github.com/xbtlin/ai-berkshire)** – The top trending project today (+1,445 stars) demonstrates the appetite for domain‑specific, multi‑agent financial analysis. Expect more “agent swarm” patterns in other verticals.

- **[headroomlabs‑ai/headroom](https://github.com/headroomlabs-ai/headroom)** – Token compression (60–95% fewer tokens) is a game‑changer for cost and latency in RAG and agent loops. A key tool for scaling LLM applications.

- **[Graphify](https://github.com/safishamsi/graphify)** – Turning entire codebases into knowledge graphs is becoming a must‑have for AI‑assisted development. Its integration with multiple agent CLIs positions it as a universal knowledge layer.

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*