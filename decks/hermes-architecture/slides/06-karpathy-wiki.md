# 🗂 GitHub Structure — Karpathy LLM Wiki Pattern

> How `hermes-wiki` applies Karpathy's five-layer knowledge graph pattern, and what's still missing.

---

## The Five Layers (Karpathy LLM Wiki)

<div class="flow-chart">
  <div class="flow-row">
    <div class="flow-node data">
      <span class="node-label">① raw/</span>
      <span class="node-sub">immutable source files</span>
    </div>
  </div>
  <div class="flow-arrow"></div>
  <div class="flow-row">
    <div class="flow-node data">
      <span class="node-label">② research/</span>
      <span class="node-sub">typed pages — entity · concept · comparison</span>
    </div>
  </div>
  <div class="flow-arrow"></div>
  <div class="flow-row">
    <div class="flow-node long-term">
      <span class="node-label">③ operational/</span>
      <span class="node-sub">free-form — infra · analysis · code · repos · people</span>
    </div>
  </div>
  <div class="flow-arrow"></div>
  <div class="flow-row">
    <div class="flow-node compute">
      <span class="node-label">④ logs/</span>
      <span class="node-sub">timestamped change history</span>
    </div>
  </div>
  <div class="flow-arrow"></div>
  <div class="flow-row">
    <div class="flow-node output">
      <span class="node-label">⑤ schema/</span>
      <span class="node-sub">rules — AGENTS.md + SCHEMA.md</span>
    </div>
  </div>
</div>

<div class="small">

Reference: <a href="https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f">karpathy/llm-wiki gist</a>

</div>

---

## Our Application Status

| Layer | Status | What's in it |
|---|---|---|
| **① raw/** | ⚪ empty | reserved for research source originals |
| **② research/** | ⚠️ **empty** | typed pages not yet created (entities/concepts/comparisons) |
| **③ operational/** | ✅ populated | analysis · architecture · code · infra · watchlist · solopreneur · repos · people |
| **④ logs/** | ✅ submodule | `hermes-logs` with `YYYY-MM-DD-HHMM.md` timestamped files |
| **⑤ schema/** | ✅ populated | `AGENTS.md` + `SCHEMA.md` (8 lint rules) |

<div class="small">

Three of five layers populated. Two gaps to close.

</div>

---

## What's NOT Applied Yet (Resolution Plan)

| Gap | Why it matters | Resolution |
|---|---|---|
| **Empty `research/`** | Typed pages enable graph RAG, structured retrieval, semantic search across entities | Create `entities/`, `concepts/`, `comparisons/` pages with frontmatter (`type: entity/concept/comparison`) |
| **Empty `raw/`** | Original sources aren't preserved — research loses traceability | Save every research source to `raw/` BEFORE writing the wiki page |
| **Frontmatter on operational/** | Lint coverage is partial (research/ only enforced) | Extend SCHEMA.md lint to validate frontmatter across operational pages too |
| **Log submodule coupling** | `hermes-logs` lives in submodule, not inside `hermes-wiki` directly | Optional: merge logs into `hermes-wiki/logs/` for atomic clone |

---

## The Three Resolutions in Detail

### 1. Populate `research/` with typed pages

Each page follows the typed schema from `SCHEMA.md`:

```yaml
---
type: entity | concept | comparison
title: Page name
created: YYYY-MM-DD
updated: YYYY-MM-DD
tags: [research, type, ...]
sources: [raw/source-file.md]
confidence: high | medium | low
---
```

**Candidates to create**:
- entities/: Codex CLI, Claude Code, Sonnet, Ollama, Honcho
- concepts/: skill compound loop, SSoT, multi-agent chain
- comparisons/: Codex vs Claude Code, Honcho vs pgvector

### 2. Save sources to `raw/` first

The ingest rule: **raw → research → log**. No page is written without its source in `raw/`.

### 3. Extend lint to all pages

Move from partial lint (research/ only) to full lint (operational/ too) — every page must pass frontmatter validation.

---

## Result After Resolution

| Layer | Before | After |
|---|---|---|
| ① raw/ | ⚪ | ✅ sources preserved |
| ② research/ | ⚠️ empty | ✅ typed pages fill graph |
| ③ operational/ | ✅ | ✅ + frontmatter lint |
| ④ logs/ | ✅ | ✅ |
| ⑤ schema/ | ✅ | ✅ + full lint |

<div class="small">

Closing these gaps transforms hermes-wiki from a notes archive into a queryable knowledge graph.

</div>