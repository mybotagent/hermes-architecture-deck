# 💾 Memory — Two Layers

<div class="flow-chart">
  <div class="flow-row">
    <div class="flow-node data">
      <span class="node-label">📓 Notebook</span>
      <span class="node-sub">memory.md + user.md</span>
      <span class="node-sub">2KB budget, always loaded</span>
    </div>
    <div class="flow-arrow right"></div>
    <div class="flow-node data">
      <span class="node-label">🗄 Vector store</span>
      <span class="node-sub">Honcho / pgvector</span>
      <span class="node-sub">unlimited, on-demand</span>
    </div>
  </div>
</div>

<div class="small">

Honcho runs end-of-session, digests the conversation, infers preferences the user never stated, and writes them back to user.md automatically.

</div>

---

# 📖 Manual — Skill Compound

<div class="flow-chart">
  <div class="flow-row">
    <div class="flow-node simple">① run</div>
    <div class="flow-arrow right"></div>
    <div class="flow-node data">② manual</div>
    <div class="flow-arrow right"></div>
    <div class="flow-node output">③ faster</div>
  </div>
  <div class="flow-arrow"></div>
  <div class="flow-row">
    <div class="flow-node simple">④ more experience</div>
    <div class="flow-arrow up"></div>
    <div class="flow-arrow right"></div>
    <div class="flow-node data">→ loops back to ②</div>
  </div>
</div>

> **Chatbot**: starts from zero every run.
> **Hermes**: yesterday's output is today's starting point.