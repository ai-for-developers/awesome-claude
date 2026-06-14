# ✦ Awesome Claude [![Awesome](https://awesome.re/badge-flat2.svg)](https://awesome.re) ![2026 Edition](https://img.shields.io/badge/2026-Edition-orange?style=flat-square) [![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen?style=flat-square)](https://github.com/ai-for-developers/awesome-claude/pulls)

> A curated list of tools, SDKs, prompts, tutorials, and community projects for working with **Claude** — Anthropic's AI assistant. Updated for 2026 with Claude 4, extended context, computer use (GA), and the MCP connector ecosystem.

---

## Contents

- [Official SDKs & Libraries](#official-sdks--libraries)
- [Models & API Reference](#models--api-reference)
- [Tools & Applications](#tools--applications)
- [Model Context Protocol (MCP)](#model-context-protocol-mcp)
- [Prompt Engineering](#prompt-engineering)
- [Agentic Patterns](#agentic-patterns)
- [Community Projects](#community-projects)
- [Tutorials & Learning](#tutorials--learning)
- [Research & Papers](#research--papers)
- [Contributing](#contributing)

---

## Official SDKs & Libraries

> Maintained by Anthropic or deeply integrated into major AI frameworks.

| Name | Language | Stars | Notes |
|------|----------|-------|-------|
| [anthropic-sdk-python](https://github.com/anthropics/anthropic-sdk-python) | Python | ★ 41.2k | Official. Streaming, tool use, vision, async/await, auto-retry |
| [anthropic-sdk-typescript](https://github.com/anthropics/anthropic-sdk-typescript) | TypeScript | ★ 38.8k | Official. Full type safety, streaming helpers, Edge Runtime |
| [anthropic-sdk-java](https://github.com/anthropics/anthropic-sdk-java) | Java | ★ 9.1k | Official. Spring Boot integration, Project Reactor support |
| [anthropic-sdk-go](https://github.com/anthropics/anthropic-sdk-go) | Go | ★ 7.3k | Official. Idiomatic error handling, zero external dependencies |
| [anthropic-sdk-rust](https://github.com/anthropics/anthropic-sdk-rust) | Rust | ★ 4.2k | Official. Async via Tokio, zero-copy streaming |
| [langchain-anthropic](https://github.com/langchain-ai/langchain) | Python | ★ 22.4k | Chains, agents, LCEL, RAG pipelines, memory |
| [llama-index-anthropic](https://github.com/run-llama/llama_index) | Python | ★ 18.7k | Document loaders, knowledge graphs, query engines |
| [vercel-ai-sdk](https://github.com/vercel/ai) | TypeScript | ★ 31.5k | `useChat`, `useCompletion`, RSC streaming, tool rendering |
| [haystack-claude](https://github.com/deepset-ai/haystack) | Python | ★ 6.9k | Pipeline components for retrieval and summarization |
| [instructor](https://github.com/jxnl/instructor) | Python | ★ 24.1k | Structured outputs from Claude using Pydantic schemas |
| [litellm](https://github.com/BerriAI/litellm) | Python | ★ 19.8k | Unified API wrapper across 100+ LLM providers incl. Claude |

---

## Models & API Reference

> Current Claude 4 model family (2025–2026). All models support tool use, vision, and computer use.

### Model Lineup

| Model ID | Context | Best For | Speed |
|----------|---------|----------|-------|
| `claude-opus-4-20260101` | 1M tokens | Complex reasoning, research, agentic tasks | Slower |
| `claude-sonnet-4-20260101` | 200k tokens | Coding, analysis, balanced production use | Fast |
| `claude-haiku-4-20260101` | 200k tokens | Real-time apps, classification, high-volume | Fastest |

### Key API Features (2026)

- **Extended Thinking** — Budget-controlled internal reasoning via `thinking.budget_tokens`. Available on Opus 4 and Sonnet 4. Best for math, logic, and multi-step problems.
- **Computer Use (GA)** — Claude controls GUI applications via screenshot + action loop. Now generally available with sub-second action latency improvements.
- **1M Token Context** — Opus 4 supports 1M tokens for processing entire codebases, books, or long document collections in a single request.
- **Prompt Caching** — Cache system prompts up to 90% cost reduction on repeated large-context calls. Cache TTL is 5 minutes (Ephemeral) or 1 hour (Persistent).
- **Batch API** — Process up to 100k prompts asynchronously with 50% cost reduction. Results delivered within 24 hours.
- **Streaming Tool Use** — Stream tool call deltas in real time, enabling live UX during agentic task execution.
- **Video Understanding** — Opus 4 can process video frames for temporal reasoning, UI walkthroughs, and video QA (beta).
- **Citations API** — Claude can return structured source attribution from documents, grounding responses in specific passages.

### Quickstart

```python
import anthropic

client = anthropic.Anthropic()

message = client.messages.create(
    model="claude-sonnet-4-20260101",
    max_tokens=1024,
    messages=[
        {"role": "user", "content": "Explain extended thinking in Claude 4."}
    ]
)
print(message.content[0].text)
```

**With Extended Thinking:**

```python
message = client.messages.create(
    model="claude-opus-4-20260101",
    max_tokens=16000,
    thinking={
        "type": "enabled",
        "budget_tokens": 10000  # Claude reasons internally before answering
    },
    messages=[{"role": "user", "content": "Solve this step by step..."}]
)
```

---

## Tools & Applications

### Official Tools by Anthropic

- **[Claude.ai](https://claude.ai)** — Web, iOS, Android. Personal AI assistant. Pro, Team, and Enterprise tiers.
- **[Claude Code](https://docs.anthropic.com/en/docs/claude-code)** `CLI` — Agentic coding assistant in your terminal. Full repo context, edit + run loops, git integration, MCP tool use.
- **[Claude in Chrome](https://chrome.google.com/webstore)** `beta` — Browsing agent. Summarize pages, fill forms, run multi-step web workflows.
- **[Claude in Excel / PowerPoint](https://www.anthropic.com)** `beta` — Native Office add-ins. Generate formulas, analyze data, build presentations with natural language.
- **[Cowork](https://www.anthropic.com)** `beta` — Desktop automation for non-developers. Drag-and-drop workflows using computer use.
- **[Anthropic Workbench](https://console.anthropic.com/workbench)** — Browser-based prompt IDE. Compare models, test system prompts, visualize tokens, export API code.

### Third-Party Coding Tools

- **[Cursor](https://cursor.sh)** — AI code editor with Claude 4 support. Codebase-aware completions, multi-file edits.
- **[Aider](https://github.com/paul-gauthier/aider)** `★ 22k` — AI pair programming in the terminal. Multi-file edits, git history. Claude Sonnet 4 is the recommended default.
- **[Cline (VS Code)](https://github.com/cline/cline)** `★ 18.4k` — Autonomous coding agent in VS Code. File system access, browser control, terminal execution, MCP.
- **[Zed AI](https://zed.dev)** — High-performance editor with native Claude integration and inline assistant.
- **[Continue](https://github.com/continuedev/continue)** `★ 14.2k` — Open-source VS Code & JetBrains extension. Custom context providers and fine-tuned slash commands.
- **[Windsurf](https://codeium.com/windsurf)** — Agentic IDE by Codeium with Claude 4 support and Cascade agent flow.

### Automation & Workflow

- **[n8n](https://n8n.io)** — No-code workflows with native Claude nodes. Connect to 400+ apps without writing code.
- **[Make (Integromat)](https://make.com)** — Visual automation platform with Claude modules for document processing and content workflows.
- **[Zapier AI](https://zapier.com)** — Claude-powered Zaps. Natural language workflow creation and automated content pipelines.
- **[Activepieces](https://github.com/activepieces/activepieces)** `★ 9.8k` — Open-source automation. Self-hostable with Claude AI pieces.

### Observability & Evaluation

- **[LangSmith](https://smith.langchain.com)** — Trace Claude API calls, visualize chains, run evals, monitor production apps.
- **[Braintrust](https://braintrustdata.com)** — Eval platform with dataset management, scoring, and regression tracking for Claude.
- **[PromptLayer](https://promptlayer.com)** — Prompt versioning, A/B testing, and analytics for Claude API calls.
- **[Helicone](https://helicone.ai)** — Open-source LLM observability. One-line Claude proxy with logging, caching, and rate limiting.

### Skill Marketplaces

- **[CreatorSkills](https://creatorskills.co)** — Marketplace of 30+ downloadable AI skills for content creators covering YouTube scripting, sponsorship analysis, and audience growth. Works with Claude and ChatGPT.

---

## Model Context Protocol (MCP)

> **MCP** is an open standard that lets Claude securely connect to external data sources, tools, and services. Think of it as a USB-C port for AI — standardized, composable, and bidirectional.

- **[MCP Specification](https://spec.modelcontextprotocol.io)** — Official protocol spec and schema reference.
- **[MCP TypeScript SDK](https://github.com/modelcontextprotocol/typescript-sdk)** — Build MCP servers in TypeScript/Node.js.
- **[MCP Python SDK](https://github.com/modelcontextprotocol/python-sdk)** — Build MCP servers in Python.

### Official Anthropic MCP Servers

| Server | Description |
|--------|-------------|
| `filesystem` | Read/write local files with path permission controls |
| `github` | Repos, issues, PRs, code search via GitHub API |
| `google-drive` | Search and read Google Drive documents |
| `slack` | Send messages, read channels, search Slack workspaces |
| `postgres` | Read-only SQL queries against PostgreSQL databases |
| `sqlite` | Local SQLite query and inspection |
| `brave-search` | Web search via Brave Search API |
| `fetch` | Fetch and convert web pages to Markdown for Claude |
| `memory` | Persistent key-value store across conversations |
| `puppeteer` | Browser automation and web scraping |

### Community MCP Servers

- **[mcp-server-obsidian](https://github.com/MarkusPfundstein/mcp-obsidian)** — Read/write Obsidian vaults. Let Claude reason over your notes.
- **[mcp-server-notion](https://github.com/makenotion/notion-mcp-server)** — Official Notion MCP. Query, create, and update pages and databases.
- **[mcp-server-linear](https://github.com/linear/linear-mcp)** — Official Linear MCP. Issue tracking, project management.
- **[mcp-server-stripe](https://github.com/stripe/agent-toolkit)** — Stripe API via MCP. Process payments, manage customers in Claude Code.
- **[mcp-server-aws](https://github.com/awslabs/mcp)** `★ 3.1k` — AWS services via MCP. CloudFormation, S3, Lambda, CloudWatch.
- **[mcp-server-kubernetes](https://github.com/manusa/kubernetes-mcp-server)** — Kubernetes cluster management through Claude.
- **[mcp-atlas-docs](https://github.com/mongodb-developer/mongodb-mcp-server)** — Official MongoDB MCP. Query Atlas clusters and manage collections.
- **[mcp-server-raycast](https://developers.raycast.com)** — Connect Claude Code to your entire Raycast extension ecosystem.

### Building an MCP Server

```typescript
import { Server } from "@modelcontextprotocol/sdk/server/index.js";
import { StdioServerTransport } from "@modelcontextprotocol/sdk/server/stdio.js";

const server = new Server(
  { name: "my-server", version: "1.0.0" },
  { capabilities: { tools: {} } }
);

server.setRequestHandler("tools/list", async () => ({
  tools: [{
    name: "get_weather",
    description: "Get current weather for a location",
    inputSchema: {
      type: "object",
      properties: { location: { type: "string" } },
      required: ["location"]
    }
  }]
}));

server.setRequestHandler("tools/call", async (request) => {
  // handle tool execution
  return { content: [{ type: "text", text: `Weather for ${request.params.arguments.location}` }] };
});

await server.connect(new StdioServerTransport());
```

---

## Prompt Engineering

> Techniques, libraries, and reference resources for getting the best results from Claude.

### Core Techniques

- **[Anthropic Prompt Engineering Guide](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/overview)** — Official comprehensive guide. Start here.
- **[Prompt Library](https://docs.anthropic.com/en/prompt-library)** — Anthropic's curated collection of production-ready prompts across dozens of use cases.

### Prompting Tips for Claude 4

```
# Use XML tags for structured inputs
<document>{{content}}</document>
<task>Summarize the key findings and list action items.</task>

# Chain of thought — ask Claude to reason before answering
Think through this step by step before giving your final answer.

# Specify the output format explicitly
Respond in JSON with keys: summary, confidence (0-1), sources (list).

# For extended thinking — let Claude allocate its own reasoning budget
This is a complex problem. Use your full reasoning capacity before answering.

# Prefilling — start the assistant turn to constrain output format
Human: Extract the JSON...
Assistant: ```json
{
```

### Recommended Prompts

**System prompt for a coding assistant:**
```
You are an expert software engineer. When writing code:
- Default to modern, idiomatic patterns for the language
- Include error handling unless told otherwise
- Explain non-obvious decisions in brief inline comments
- Ask clarifying questions before making large architectural changes
```

**System prompt for document analysis:**
```
You are a precise document analyst. Extract only information explicitly present 
in the provided documents. If something is unclear or absent, say so directly. 
Do not infer or speculate beyond what is written. Format your output as requested.
```

**Meta-prompt for evaluating responses:**
```
Review your previous response for:
1. Factual accuracy — flag any uncertain claims
2. Completeness — did you miss anything important?
3. Conciseness — remove anything that doesn't add value
Provide a revised version if improvements are needed.
```

### Prompt Libraries & Tools

- **[Promptfoo](https://github.com/promptfoo/promptfoo)** `★ 5.2k` — Test and evaluate prompts against Claude. Red teaming, regression testing, output comparison.
- **[Priompt](https://github.com/anysphere/priompt)** `★ 2.1k` — JSX-based prompt templating with priority-based token allocation.
- **[LMQL](https://lmql.ai)** — Query language for LLMs. Constrained decoding, typed outputs, and scripted interactions with Claude.
- **[Outlines](https://github.com/outlines-dev/outlines)** `★ 11.3k` — Structured generation with regex, JSON Schema, and grammar constraints.

---

## Agentic Patterns

> Architectures and patterns for building reliable multi-step Claude agents.

### Patterns

**ReAct (Reason + Act)**
```python
# Claude reasons about what tool to use, uses it, observes the result, repeats
while not done:
    thought = claude.think(context)
    action = claude.decide_action(thought, available_tools)
    observation = execute_tool(action)
    context.add(thought, action, observation)
```

**Orchestrator–Subagent**
```
Orchestrator Claude (Opus 4)
├── Plans the overall task, delegates subtasks
├── Subagent: Research Claude (Sonnet 4) — web retrieval
├── Subagent: Code Claude (Sonnet 4) — implementation
└── Subagent: Review Claude (Sonnet 4) — validation
```

**Prompt Chaining with Validation**
```python
# Break complex tasks into verifiable sequential steps
step1 = claude.complete("Extract all requirements from this spec", doc)
validated = validate_extraction(step1)
step2 = claude.complete("Write tests for each requirement", validated)
step3 = claude.complete("Implement code to pass these tests", step2)
```

**Parallel Specialization**
```python
import asyncio

async def parallel_analysis(document):
    results = await asyncio.gather(
        claude.analyze(document, role="security expert"),
        claude.analyze(document, role="performance engineer"),
        claude.analyze(document, role="UX designer")
    )
    return claude.synthesize(results)
```

### Agent Frameworks

- **[LangGraph](https://github.com/langchain-ai/langgraph)** `★ 7.4k` — Stateful multi-agent graphs. Best for complex, cyclical agentic workflows with Claude.
- **[AutoGen](https://github.com/microsoft/autogen)** `★ 35.2k` — Multi-agent conversation framework. Supports Claude as participant agent.
- **[CrewAI](https://github.com/crewAIInc/crewAI)** `★ 22.8k` — Role-based agent teams. Define crews of specialized Claude agents with shared goals.
- **[Agno](https://github.com/agno-agi/agno)** `★ 4.1k` — Lightweight agent framework with first-class Claude support and built-in memory.
- **[Smolagents](https://github.com/huggingface/smolagents)** `★ 8.6k` — HuggingFace's minimal agent library. Code-first agents with Claude backend.
- **[Pydantic AI](https://github.com/pydantic/pydantic-ai)** `★ 6.3k` — Type-safe agent framework. Schema-validated tool calls and structured outputs with Claude.

---

## Community Projects

> Noteworthy open-source projects built with Claude.

### Productivity & Knowledge

- **[NotebookLM-OSS](https://github.com/example/notebooklm-oss)** `★ 8.1k` — Open-source alternative to NotebookLM using Claude for document Q&A and podcast generation.
- **[Quivr](https://github.com/QuivrHQ/quivr)** `★ 37.2k` — "Second brain" for documents. RAG with Claude over your personal knowledge base.
- **[Khoj](https://github.com/khoj-ai/khoj)** `★ 15.9k` — Self-hosted personal AI. Search notes, PDFs, org files with Claude as the reasoning backend.
- **[mem0](https://github.com/mem0ai/mem0)** `★ 23.4k` — Memory layer for AI agents. Persistent, structured memories across Claude conversations.
- **[Markprompt](https://github.com/motifland/markprompt)** `★ 2.9k` — AI-powered docs search and assistant using Claude over your Markdown documentation.

### Coding & Development

- **[Claude Engineer](https://github.com/Doriandarko/claude-engineer)** `★ 12.4k` — Full-featured CLI agent with file management, code execution, and self-improvement loops.
- **[claude-coder](https://github.com/arnaud-eb/claude-coder)** `★ 3.2k` — Minimal but powerful code generation agent with test execution feedback.
- **[repomix](https://github.com/yamadashy/repomix)** `★ 7.8k` — Pack entire repositories into a single file optimized for Claude's 1M context window.
- **[SWE-agent](https://github.com/SWE-agent/SWE-agent)** `★ 13.1k` — Claude solves real GitHub issues end-to-end. Top performer on SWE-bench.
- **[OpenHands](https://github.com/All-Hands-AI/OpenHands)** `★ 41.7k` — Open-source Devin alternative. Claude-powered software engineering agent with sandbox execution.

### Research & Analysis

- **[Storm](https://github.com/stanford-oval/storm)** `★ 9.6k` — Wikipedia-style report generation from scratch using multi-agent Claude research.
- **[GPT-Researcher](https://github.com/assafelovic/gpt-researcher)** `★ 16.2k` — Autonomous deep research agent. Now supports Claude as the reasoning model.
- **[Perplexica](https://github.com/ItzCrazyKns/Perplexica)** `★ 18.3k` — Open-source Perplexity. Self-hosted web research with Claude-powered synthesis.
- **[AutoSurvey](https://github.com/AutoSurveys/AutoSurvey)** `★ 2.4k` — Automated academic literature review generation using Claude 4.

### Creative & Multimodal

- **[Ebook-GPT](https://github.com/rajeshdavidbabu/pdf-chat)** `★ 4.1k` — Chat with entire books. Optimized for Claude's large context window.
- **[Bedrock-Claude-Chat](https://github.com/aws-samples/bedrock-claude-chat)** `★ 5.7k` — Full-stack Claude chat app deployable to AWS with multi-modal support.
- **[ClaudeSync](https://github.com/jahwag/ClaudeSync)** `★ 1.8k` — Sync local files to Claude Projects for persistent, context-aware workflows.

---

## Tutorials & Learning

### Official Resources

- **[Anthropic Documentation](https://docs.anthropic.com)** — Complete API docs, guides, and examples.
- **[Anthropic Courses](https://github.com/anthropics/courses)** `★ 9.4k` — Official free courses: Prompt Engineering, Tool Use, RAG, Multiagent Systems.
- **[Anthropic Cookbook](https://github.com/anthropics/anthropic-cookbook)** `★ 12.1k` — Practical recipes: embeddings, citations, structured outputs, computer use, MCP.
- **[Claude's Constitution](https://www.anthropic.com/claude/constitutional-ai)** — How Claude's values and behaviors are defined via Constitutional AI.

### Community Guides

- **[Claude Prompt Engineering Patterns](https://github.com/brexhq/prompt-engineering)** `★ 8.2k` — Real-world patterns from Brex's production Claude deployment.
- **[Prompt Injection Defense](https://learnprompting.org/docs/prompt_hacking/defensive_measures)** — Techniques to make Claude-powered apps robust against adversarial inputs.
- **[Building Production RAG with Claude](https://www.pinecone.io/learn/claude-rag)** — End-to-end guide using Claude + Pinecone with citations and chunking strategies.
- **[Claude for Enterprise](https://www.anthropic.com/solutions/enterprise)** — Use cases, compliance overview, and integration patterns for enterprise deployments.

### Videos & Courses

- **[Free Anthropic Courses on GitHub](https://github.com/anthropics/courses)** — Four free structured courses from Anthropic covering the full stack.
- **[DeepLearning.AI: Prompt Engineering with Claude](https://deeplearning.ai)** — Andrew Ng + Anthropic. Covers prompting, tool use, and production best practices.
- **[LLM Bootcamp](https://fullstackdeeplearning.com/llm-bootcamp)** — Comprehensive course featuring Claude for building production LLM apps.

---

## Research & Papers

> Key papers from Anthropic and the broader research community.

### Anthropic Research

- **[Constitutional AI: Harmlessness from AI Feedback](https://arxiv.org/abs/2212.08073)** (2022) — The training methodology behind Claude's values and behaviors.
- **[Claude's Character](https://www.anthropic.com/research/claude-character)** (2023) — How stable identity and values emerge in large language models.
- **[Scaling Monosemanticity](https://transformer-circuits.pub/2024/scaling-monosemanticity/index.html)** (2024) — Interpretability research: finding meaningful features in Claude's activations at scale.
- **[Alignment Faking in Large Language Models](https://arxiv.org/abs/2412.14093)** (2024) — Safety-relevant behavior observed in frontier models including Claude.
- **[Model Specification](https://www.anthropic.com/claude/model-spec)** (2025) — Full public specification of Claude's intended values, priorities, and behaviors.
- **[Extended Thinking Technical Report](https://www.anthropic.com/research/extended-thinking)** (2025) — How budget-forced reasoning improves Claude's performance on hard tasks.
- **[Many-shot Jailbreaking](https://www.anthropic.com/research/many-shot-jailbreaking)** (2024) — Safety research on adversarial few-shot prompting in long-context models.

### External Research on Claude

- **[SWE-bench Verified](https://arxiv.org/abs/2405.15793)** (2024) — Benchmark where Claude 3.5 Sonnet set state-of-the-art on real GitHub issues.
- **[AgentBench](https://arxiv.org/abs/2308.03688)** (2023) — Evaluation of LLMs as agents across diverse environments. Claude leads several categories.
- **[MMLU Performance Analysis](https://arxiv.org/abs/2009.03300)** — Massive Multitask Language Understanding; tracking Claude improvements over generations.

---

## Contributing

Contributions are welcome! Please follow these guidelines:

1. **Fork** the repository and create a branch: `git checkout -b add/tool-name`
2. **Add your resource** in the appropriate section, following the existing format
3. **Check your link** is working and the project is actively maintained (last commit within 12 months)
4. **Write a clear description** — one sentence, starting with a verb, describing what it does
5. **Open a pull request** at [ai-for-developers/awesome-claude](https://github.com/ai-for-developers/awesome-claude/pulls) with the title `Add: [Tool Name]`

### Quality Standards

- ✅ Open-source projects should have a clear license
- ✅ Commercial tools should have a free tier or trial
- ✅ No pure promotional content or abandoned projects (0 commits in 12 months)
- ✅ Descriptions should be neutral and factual, not marketing language
- ✅ Add `[NEW]` tag only for resources added in the last 3 months

### Maintainers

This list is community-maintained. If you spot something outdated, please [open an issue](https://github.com/ai-for-developers/awesome-claude/issues).

---

## License

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)

To the extent possible under law, the contributors have waived all copyright and related rights to this work. See [LICENSE](https://github.com/ai-for-developers/awesome-claude/blob/main/LICENSE) for details.

---

<p align="center">
  <sub>Last updated: February 2026 · <a href="https://github.com/ai-for-developers/awesome-claude">↑ Back to top</a></sub>
</p>
