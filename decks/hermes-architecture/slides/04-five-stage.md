# 🔗 Five-Stage Analysis Chain

> Every analysis runs the same five stages. Each stage is an independent LLM call. The conclusion inherits the lineage of every prior agent.

<div class="flow-chart">
  <div class="flow-row">
    <div class="flow-node data">
      <span class="node-label">📥 Input</span>
      <span class="node-sub">data · scores · metrics</span>
    </div>
  </div>
  <div class="flow-arrow"></div>
  <div class="flow-row">
    <div class="flow-node long-term">
      <span class="node-label">① Context</span>
      <span class="node-sub">environment & assumptions</span>
    </div>
  </div>
  <div class="flow-arrow"></div>
  <div class="flow-group">
    <span class="flow-group-label">② ③ ④ ⑤ — Four parallel agents</span>
    <div class="flow-row">
      <div class="flow-node output">
        <span class="node-label">② Positive</span>
        <span class="node-sub">bull case</span>
      </div>
      <div class="flow-node tooling">
        <span class="node-label">③ Negative</span>
        <span class="node-sub">bear case</span>
      </div>
      <div class="flow-node compute">
        <span class="node-label">④ Risk</span>
        <span class="node-sub">downside scenarios</span>
      </div>
      <div class="flow-node data">
        <span class="node-label">⑤ Trade-off</span>
        <span class="node-sub">competing objectives</span>
      </div>
    </div>
  </div>
  <div class="flow-arrow"></div>
  <div class="flow-row">
    <div class="flow-node output" style="min-width: 200px;">
      <span class="node-label">⑥ Conclusion</span>
      <span class="node-sub">action · confidence · alternatives · rationale</span>
    </div>
  </div>
</div>

<div class="small">

Each stage is **independent and traceable**. If the conclusion looks wrong, you can inspect which stage misfired — the logs are structured JSON per stage.

</div>

---

# Conclusion Output — Structured

| Input | Output |
|---|---|
| Positive / Negative summary | recommended action |
| Risk scenarios | confidence (%) |
| Trade-off matrix | alternative options |
| Metrics / scores | rationale string |

<div class="small">

The conclusion is a structured object, not free-form text. Downstream code (allocator, reporter, notifier) parses it deterministically.

</div>

---

# Cost Optimization

| Item | Value |
|---|---:|
| **Per analysis** | **$0.054** |
| Calls per analysis | 5 – 6 |
| Daily calls (N items) | N × 6 |
| Monthly (22 business days) | $1.20 |
| **Share of monthly budget** | **4%** |

<div class="small">

💡 **V4 Flash** (DeepSeek) at temperature 0.3 = consistency at 95% lower cost vs larger models.

</div>