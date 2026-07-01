# 🗂 GitHub Structure — Karpathy LLM Wiki Pattern

> How `hermes-wiki` is organized today. What we have, where it lives.

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

## What `hermes-wiki` Has Today

| Layer | Status | What lives there |
|---|---|---|
| **① raw/** | empty | — |
| **② research/** | empty | — |
| **③ operational/** | populated | `analysis/` · `architecture/` · `code/` · `infra/` · `watchlist/` · `solopreneur/` · `repos/` · `people/` |
| **④ logs/** | submodule | `hermes-logs` with `YYYY-MM-DD-HHMM.md` timestamped files |
| **⑤ schema/** | populated | `AGENTS.md` (Karpathy 5-layer rules) + `SCHEMA.md` (8 lint rules) |

---

## `operational/` in Detail

This is the layer we actively use. Eight sub-domains, each with its own folder:

<div class="flow-chart">
  <div class="flow-group">
    <span class="flow-group-label">③ operational/ — what we write today</span>
    <div class="flow-row">
      <div class="flow-node long-term">
        <span class="node-label">analysis/</span>
        <span class="node-sub">5 pages — methodology, rating, valuation, langgraph, pipeline</span>
      </div>
      <div class="flow-node long-term">
        <span class="node-label">architecture/</span>
        <span class="node-sub">3 pages — hermes-vs-chatbot, hybrid-stack, ssot</span>
      </div>
    </div>
    <div class="flow-row">
      <div class="flow-node long-term">
        <span class="node-label">infra/</span>
        <span class="node-sub">cron, env, gh-token, gateway, etc.</span>
      </div>
      <div class="flow-node long-term">
        <span class="node-label">code/</span>
        <span class="node-sub">script catalog</span>
      </div>
    </div>
    <div class="flow-row">
      <div class="flow-node long-term">
        <span class="node-label">watchlist/</span>
        <span class="node-sub">stock universe</span>
      </div>
      <div class="flow-node long-term">
        <span class="node-label">repos/</span>
        <span class="node-sub">repo documentation</span>
      </div>
    </div>
    <div class="flow-row">
      <div class="flow-node long-term">
        <span class="node-label">solopreneur/</span>
        <span class="node-sub">freelancing strategy</span>
      </div>
      <div class="flow-node long-term">
        <span class="node-label">people/</span>
        <span class="node-sub">user profile (aiprofit)</span>
      </div>
    </div>
  </div>
</div>

---

## `logs/` and `schema/` — Supporting Layers

**`logs/`** lives as a git submodule (`hermes-logs`). Each significant change writes a timestamped file:

```
logs/
├── index.md                        ← chrono index of all events
├── YYYY/                           ← year directories
│   └── YYYY-MM-DD-HHMM.md          ← one file per significant change
└── archive/                        ← 6mo+ old logs
```

**`schema/`** (root of repo) defines the rules every page must follow:

- `AGENTS.md` — Karpathy 5-layer structure, Wiki-First rule, Memory discipline, 8 lint rules
- `SCHEMA.md` — frontmatter taxonomy (research/ requires `type/title/created/updated/tags/sources/confidence`)

---

## `INDEX.md` — The Single Entry Point

Every page in the wiki is listed in `index.md` with one-line descriptions. Wiki-First rule: read INDEX first, follow `related:` frontmatter for graph traversal, then load specific pages.

<div class="small">

**Total**: ~31 pages across 8 operational sub-domains, 5 timestamped log entries, 2 schema files. Empty `raw/` and `research/` layers are present as folders but contain no pages.

</div>