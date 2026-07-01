# 🚀 Three Principles

> The entire stack rests on three architectural principles. Every tool, every routing decision, every deployment choice traces back to these.

<div class="flow-chart">
  <div class="flow-row">
    <div class="flow-node compute" style="min-width: 200px;">
      <span class="node-label">① Cost Zero (Local)</span>
      <span class="node-sub">when latency or sensitivity demands</span>
    </div>
  </div>
  <div class="flow-arrow"></div>
  <div class="flow-row">
    <div class="flow-node long-term" style="min-width: 200px;">
      <span class="node-label">② Best Performance (Cloud)</span>
      <span class="node-sub">when depth or scale demands</span>
    </div>
  </div>
  <div class="flow-arrow"></div>
  <div class="flow-row">
    <div class="flow-node data" style="min-width: 200px;">
      <span class="node-label">③ Zero Data Contamination</span>
      <span class="node-sub">never let raw data leak to LLM context</span>
    </div>
  </div>
</div>

<div class="small">

These three principles are **non-negotiable**. If a task cannot be served by the stack while honoring all three, the task is reframed or rejected.

</div>

---

# Decision Tree — Which Tool When

<div class="flow-chart">
  <div class="flow-row">
    <div class="flow-decision">Q1 · Data sensitive?</div>
  </div>
  <div class="flow-arrow"></div>
  <div class="flow-row">
    <div class="flow-node compute">
      <span class="node-label">Yes · Ollama + Hermes</span>
      <span class="node-sub">💻 local, 100% private</span>
    </div>
    <div class="flow-decision">No → Q2</div>
  </div>
  <div class="flow-arrow"></div>
  <div class="flow-row">
    <div class="flow-decision">Q2 · Real-time response?</div>
  </div>
  <div class="flow-arrow"></div>
  <div class="flow-row">
    <div class="flow-node long-term">
      <span class="node-label">Yes · Codex</span>
      <span class="node-sub">💻 zero latency</span>
    </div>
    <div class="flow-decision">No → Q3</div>
  </div>
  <div class="flow-arrow"></div>
  <div class="flow-row">
    <div class="flow-decision">Q3 · Deep analysis?</div>
  </div>
  <div class="flow-arrow"></div>
  <div class="flow-row">
    <div class="flow-node tooling">
      <span class="node-label">Yes · Claude Sonnet</span>
      <span class="node-sub">☁️ large-scale reasoning</span>
    </div>
    <div class="flow-node output">
      <span class="node-label">No · Gemini + Notion</span>
      <span class="node-sub">☁️ docs & collaboration</span>
    </div>
  </div>
</div>

<div class="small">

**Rule of thumb**: sensitivity → local · latency → Codex · depth → Claude · docs/collaboration → Google/Notion.

</div>

---

# News Briefing — Architecture in Practice

> This is the most representative case. Source data is contaminated; the stack refuses to leak it.

<div class="flow-chart">
  <div class="flow-row">
    <div class="flow-node simple">
      <span class="node-label">📰 News source</span>
      <span class="node-sub">raw articles</span>
    </div>
  </div>
  <div class="flow-arrow"></div>
  <div class="flow-row">
    <div class="flow-node compute">
      <span class="node-label">🤖 Hermes</span>
      <span class="node-sub">scrapes & routes</span>
    </div>
  </div>
  <div class="flow-arrow"></div>
  <div class="flow-row">
    <div class="flow-node long-term">
      <span class="node-label">🦙 Ollama (local LLM)</span>
      <span class="node-sub">summarizes to 3 lines + tags</span>
    </div>
  </div>
  <div class="flow-arrow"></div>
  <div class="flow-row">
    <div class="flow-node data">
      <span class="node-label">📁 Obsidian</span>
      <span class="node-sub">permanent markdown store</span>
    </div>
  </div>
  <div class="flow-arrow"></div>
  <div class="flow-row">
    <div class="flow-node output">
      <span class="node-label">✅ Typed summary</span>
      <span class="node-sub">readable, searchable, tiny</span>
    </div>
  </div>
</div>

<div class="flow-chart" style="margin-top: 1.5em;">
  <div class="flow-row">
    <div class="flow-node simple" style="opacity: 0.4; text-decoration: line-through;">
      <span class="node-label">❌ Original source</span>
      <span class="node-sub">discarded</span>
    </div>
  </div>
</div>

<div class="small">

**Contamination guard**: original text never enters the LLM context. Only the 3-line summary + structured tags persist. The LLM context stays clean forever.

</div>