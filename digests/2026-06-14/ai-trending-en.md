# AI Open Source Trends 2026-06-14

> Sources: GitHub Trending + GitHub Search API | Generated: 2026-06-14 03:37 UTC

---

# AI Open Source Trends Report – 2026-06-14

## 1. Today’s Highlights

The open-source AI ecosystem is undergoing a decisive shift toward **production-grade agent tooling**. The two hottest projects today—`addyosmani/agent-skills` (+1,514 stars) and `obra/superpowers` (+924 stars)—are both frameworks that define how AI coding agents acquire, manage, and execute skills. NVIDIA’s `SkillSpector` (+804) adds a security layer, scanning agent skills for vulnerabilities. Meanwhile, `LMCache` (+238) addresses a core infrastructure bottleneck (KV cache for LLM inference), and `kenn-io/agentsview` (+190) brings observability and analytics to agent sessions. The community is clearly moving beyond building agents toward **hardening, optimizing, and measuring** them.

## 2. Top Projects by Category

### 🔧 AI Infrastructure (frameworks, SDKs, inference engines, dev tools)

| Project | Stars (total / today) | Description |
|--------|------------------------|-------------|
| [LMCache/LMCache](https://github.com/LMCache/LMCache) | +238 today | Supercharges LLM inference with the fastest KV cache layer—critical for reducing latency in production serving. |
| [andrewyng/aisuite](https://github.com/andrewyng/aisuite) | +127 today | A unified Python interface for multiple generative AI providers, simplifying switching between OpenAI, Anthropic, etc. |
| [kenn-io/agentsview](https://github.com/kenn-io/agentsview) | +190 today | Local-first session intelligence and analytics for coding agents (Claude Code, Codex, 20+ others), marketed as 100× faster than `ccusage`. |
| [vllm-project/vllm](https://github.com/vllm-project/vllm) | 82,788 | High-throughput, memory-efficient LLM serving engine—the de facto standard for production inference. |
| [ollama/ollama](https://github.com/ollama/ollama) | 174,076 | Simplest way to run local LLMs (Kimi-K2.6, DeepSeek, Qwen, etc.), now with broader model support. |
| [langgenius/dify](https://github.com/langgenius/dify) | 145,096 | Production-ready platform for building agentic workflows, combining RAG, tools, and multi-LLM orchestration. |
| [CopilotKit/CopilotKit](https://github.com/CopilotKit/CopilotKit) | 35,017 | Frontend stack for agents and generative UI—brings agent capabilities into React, Angular, and Slack. |

### 🤖 AI Agents / Workflows

| Project | Stars (total / today) | Description |
|--------|------------------------|-------------|
| [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) | +1,514 today | Production-grade engineering skills for AI coding agents—the top trending project today. |
| [obra/superpowers](https://github.com/obra/superpowers) | +924 today | An agentic skills framework and software development methodology that “works” out of the box. |
| [NVIDIA/SkillSpector](https://github.com/NVIDIA/SkillSpector) | +804 today | Security scanner that detects vulnerabilities, malicious patterns, and risks in AI agent skills. |
| [Significant-Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT) | 184,930 | Pioneer autonomous agent platform, now evolving into a full agent ecosystem. |
| [OpenHands/OpenHands](https://github.com/OpenHands/OpenHands) | 76,915 | AI-driven development agent—turn prompts into code, debug, and ship. |
| [browser-use/browser-use](https://github.com/browser-use/browser-use) | 98,706 | Lets AI agents interact with any website, enabling web automation at scale. |
| [TauricResearch/TradingAgents](https://github.com/TauricResearch/TradingAgents) | 85,869 | Multi-agent LLM framework for financial trading, showing vertical agent specialization. |
| [CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio) | 47,287 | AI productivity studio with smart chat, autonomous agents, and 300+ pre-built assistants. |

### 📦 AI Applications (specific apps, vertical solutions)

| Project | Stars (total / today) | Description |
|--------|------------------------|-------------|
| [x1xhlol/system-prompts-and-models-of-ai-tools](https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools) | +109 today | Curated collection of system prompts and internal models for Claude Code, Cursor, Devin, Windsurf, and dozens more. |
| [CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio) | 47,287 | All-in-one AI workstation with smart chat, autonomous agents, and 300+ assistants. |
| [iOfficeAI/AionUi](https://github.com/iOfficeAI/AionUi) | 28,201 | Free, local, open-source 24/7 coworker app for Claude Code, Codex, Gemini CLI, and 20+ CLI agents. |
| [Panniantong/Agent-Reach](https://github.com/Panniantong/Agent-Reach) | 27,663 | Give your AI agent eyes to search Twitter, Reddit, YouTube, GitHub, etc.—zero API fees. |

### 🧠 LLMs / Training

| Project | Stars (total / today) | Description |
|--------|------------------------|-------------|
| [huggingface/transformers](https://github.com/huggingface/transformers) | 161,571 | The universal model-definition framework for text, vision, audio, and multimodal LLMs. |
| [pytorch/pytorch](https://github.com/pytorch/pytorch) | 100,735 | Dynamic neural networks with GPU acceleration, backbone of most modern LLM training. |
| [ultralytics/ultralytics](https://github.com/ultralytics/ultralytics) | 58,359 | YOLO-based vision models, now integrated with LLM pipelines for multimodal AI. |
| [open-compass/opencompass](https://github.com/open-compass/opencompass) | 7,083 | Comprehensive LLM evaluation platform supporting 100+ datasets and all major models. |

### 🔍 RAG / Knowledge

| Project | Stars (total / today) | Description |
|--------|------------------------|-------------|
| [infiniflow/ragflow](https://github.com/infiniflow/ragflow) | 82,663 | Leading open-source RAG engine combining retrieval with agent capabilities for superior context. |
| [run-llama/llama_index](https://github.com/run-llama/llama_index) | 50,112 | Document agent and OCR platform—the go-to for building data-aware LLM applications. |
| [mem0ai/mem0](https://github.com/mem0ai/mem0) | 58,494 | Universal memory layer for AI agents, enabling persistent long-term context across sessions. |
| [milvus-io/milvus](https://github.com/milvus-io/milvus) | 44,764 | Cloud-native vector database for scalable ANN search, powering many RAG pipelines. |
| [qdrant/qdrant](https://github.com/qdrant/qdrant) | 32,181 | High-performance vector search engine with a focus on next-gen AI workloads. |
| [thedotmack/claude-mem](https://github.com/thedotmack/claude-mem) | 82,153 | Persistent context injection across agent sessions—captures, compresses, and re-injects session data. |
| [FlowiseAI/Flowise](https://github.com/FlowiseAI/Flowise) | 53,551 | Visual builder for AI agents and RAG pipelines—drag-and-drop agent development. |

## 3. Trend Signal Analysis

The **explosive community attention** today is squarely on **agent skills and security**. `addyosmani/agent-skills` and `obra/superpowers` collectively gained over 2,400 stars in a single day, both focused on defining how coding agents acquire, version, and execute skills. This signals a maturation: developers are no longer just building agents—they are building the **plumbing** for agent behavior at scale. NVIDIA’s `SkillSpector` (+804) underscores that as agent skills proliferate, **security auditing** becomes non-negotiable.

A newer stack direction appearing prominently is **session observability for agents**. `kenn-io/agentsview` (which claims to be 100× faster than `ccusage`) provides analytics on agent sessions, reflecting a growing need to debug and optimize agent behavior in production. Meanwhile, `LMCache` targets a persistent infrastructure bottleneck—**KV cache performance**—indicating that inference optimization remains a high-priority area even as agents dominate the narrative.

The collection `system-prompts-and-models-of-ai-tools` (+109) reveals a community-driven desire for **transparency and reproducibility** of agent configurations. Combined with the rapid adoption of skill frameworks, this points toward an emerging **agent engineering discipline** where prompts, skills, and tool definitions are treated as first-class artifacts.

Connecting to recent industry events: the Ollama repository now lists support for models like Kimi-K2.6, GLM-5.1, and MiniMax—suggesting a wave of new open-weight models that the community is quickly integrating. The simultaneous rise of agent tooling (skills, security, observability) suggests that the ecosystem is **racing to productize** these models into reliable, auditable software.

## 4. Community Hot Spots

- **Agent Skill Frameworks** – `addyosmani/agent-skills` and `obra/superpowers` are the #1 growth area. Developers should explore how these frameworks define, share, and version agent skills—expect them to become the “npm of agent skills.”
- **Agent Security** – `NVIDIA/SkillSpector` is a must-watch. As agents execute arbitrary code (via skills), vulnerability scanning becomes as critical as it is for traditional software.
- **LLM Inference Optimization** – `LMCache` is pushing the frontier of KV-cache performance. For anyone running LLMs at scale, this project can directly reduce latency and cost.
- **Unified AI Provider APIs** – `andrewyng/aisuite` simplifies multi-provider workflows. Its traction (+127 today) reflects the industry’s desire to avoid vendor lock-in.
- **Agent Session Analytics** – `kenn-io/agentsview` fills a growing observability gap. Engineers building agent pipelines should evaluate it for debugging and performance monitoring.

---
*This digest is auto-generated by [agents-radar](https://github.com/JohnGao818/agents-radar).*