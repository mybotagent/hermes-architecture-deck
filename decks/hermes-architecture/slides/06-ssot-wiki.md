# 🎯 SSoT — Single Source of Truth

> Every architectural choice in this system assumes one thing: there is exactly one place where a given fact lives. All other locations are derived, cached, or stale.

## Four Properties

<div class="flow-chart">
  <div class="flow-row">
    <div class="flow-node long-term" style="min-width: 180px;">
      <span class="node-label">① Centralization</span>
      <span class="node-sub">scattered data → single platform</span>
    </div>
  </div>
  <div class="flow-arrow"></div>
  <div class="flow-row">
    <div class="flow-node output" style="min-width: 180px;">
      <span class="node-label">② Consistency</span>
      <span class="node-sub">edit propagates everywhere in real time</span>
    </div>
  </div>
  <div class="flow-arrow"></div>
  <div class="flow-row">
    <div class="flow-node compute" style="min-width: 180px;">
      <span class="node-label">③ Integrity</span>
      <span class="node-sub">always access under one standard</span>
    </div>
  </div>
  <div class="flow-arrow"></div>
  <div class="flow-row">
    <div class="flow-node data" style="min-width: 180px;">
      <span class="node-label">④ Accurate Decision</span>
      <span class="node-sub">speed + accuracy both ↑</span>
    </div>
  </div>
</div>

<div class="small">

These four are not independent. Centralization enables consistency. Consistency enables integrity. Integrity enables accurate decision-making.

</div>

---

# Why Hierarchy Belongs at the Center

> Quantitative metrics show **what** happened. The hierarchical structure shows **why**. SSoT is only useful when it captures both.

| Data kind | Shows | Doesn't show |
|---|---|---|
| Quantitative metrics | outcomes | causes |
| Metadata | context · relations | absolute numbers |
| **SSoT (layered)** | **cause ↔ effect** | — |

<div class="small">

⚠️ **Collaboration-tool trap**: Notion · Slack · Docs keep event logs but lack hierarchy context — they cannot serve as decision substrate, only as memory aids.

</div>

---

# 🗂 Wiki Super Repository — The Knowledge Graph

> The wiki is itself architected as an SSoT: one super-repo with seven submodules. Adding a new domain means adding a submodule, not editing a monolith.

<div class="flow-chart">
  <div class="flow-row">
    <div class="flow-node long-term" style="min-width: 200px;">
      <span class="node-label">📚 hermes-wiki-super</span>
      <span class="node-sub">super-repo · SSoT index</span>
    </div>
  </div>
  <div class="flow-arrow"></div>
  <div class="flow-group">
    <span class="flow-group-label">Seven submodules (one per domain)</span>
    <div class="flow-row">
      <div class="flow-node data">
        <span class="node-label">hermes-wiki</span>
        <span class="node-sub">index + ops</span>
      </div>
      <div class="flow-node data">
        <span class="node-label">claude-code</span>
        <span class="node-sub">CLI wiki</span>
      </div>
      <div class="flow-node data">
        <span class="node-label">codex</span>
        <span class="node-sub">CLI wiki</span>
      </div>
    </div>
    <div class="flow-row">
      <div class="flow-node data">
        <span class="node-label">schedule</span>
        <span class="node-sub">calendar domain</span>
      </div>
      <div class="flow-node data">
        <span class="node-label">portfolio</span>
        <span class="node-sub">market domain</span>
      </div>
      <div class="flow-node data">
        <span class="node-label">slash-commands</span>
        <span class="node-sub">command catalog</span>
      </div>
      <div class="flow-node data">
        <span class="node-label">logs</span>
        <span class="node-sub">change history</span>
      </div>
    </div>
  </div>
  <div class="flow-arrow"></div>
  <div class="flow-row">
    <div class="flow-node simple">
      <span class="node-label">📁 hermes-wiki sub-layers</span>
      <span class="node-sub">architecture · analysis · infra · watchlist</span>
    </div>
  </div>
</div>

<div class="small">

**SSoT principle applied**: `hermes-wiki` is the index; submodules own their domain. Adding a new domain = new submodule. The super-repo stays a thin aggregator.

</div>