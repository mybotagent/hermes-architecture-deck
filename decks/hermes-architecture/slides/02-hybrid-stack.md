# 🚀 Three Principles

> **Cost zero (local) + Best performance (cloud) + Zero data contamination**

---

## Twelve Tasks × Four Categories

| Category | Examples | Optimal combo | Decision driver |
|---|---|---|---|
| **📄 Content** | PPT, card news, marketing, video | Gemini · Hermes+Canva · Higgsfield | structure & visual |
| **💻 Development** | daily coding, system design, vision | Codex · Claude Sonnet | latency vs depth |
| **🔒 Security · Compute** | tax/finance, on-prem monitoring | OpenClaw + Ollama (100% local) | data isolation |
| **🧠 Knowledge · Automation** | ERP, news briefings, wiki | Notion · Hermes+Obsidian | summary vs source |

---

## Decision Matrix

<div class="flow-tree">
<span class="node">[Q1: Data sensitivity?]</span>
    High  → 💻 Ollama local + Hermes
    Low   → Q2

<span class="node">[Q2: Real-time response?]</span>
    Yes   → 💻 Codex (Cursor)
    No    → Q3

<span class="node">[Q3: Deep analysis?]</span>
    Yes   → ☁️ Claude Sonnet
    No    → ☁️ Google Gemini + Notion
</div>

<div class="small">

**Rule of thumb**: sensitivity → local · latency → Codex · depth → Claude · docs/collaboration → Google/Notion

</div>

---

## Tool Ecosystem (eight tools)

| Tool | Role | Used in |
|---|---|---|
| **Ollama** | local LLM | security · knowledge |
| **Hermes Agent** | agent orchestration | content · automation |
| **Obsidian** | markdown store | vision · knowledge |
| **Notion** | frontend / PM | marketing · ERP |
| **Codex** | real-time coding | daily coding |
| **Claude Code** | large-scale analysis | design · refactor |
| **Google Gemini** | PPT / docs | content |
| **Higgsfield** | video generation | marketing |

---

## Case Study: News Briefing

<div class="flow-tree">
<span class="node">[Pipeline]</span>

    News source
       │  (scraped)
       ▼
    Hermes
       │  (3-line summary + tags)
       ▼
    Ollama (local LLM)
       │  (typed output only)
       ▼
    Obsidian (permanent store)
       │
       ▼
    Original source  ──x── discarded
</div>

<div class="small">

**Contamination guard**: original is discarded, only summary + tags persist — keeps the LLM context clean

</div>