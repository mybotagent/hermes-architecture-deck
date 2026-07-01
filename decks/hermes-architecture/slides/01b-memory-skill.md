# Memory in Two Layers

> Two-tier memory architecture: a tight notebook that's always loaded, plus a deep vector store that's queried on demand.

<div class="flow-chart">
  <div class="flow-group">
    <span class="flow-group-label">Layer 1 · Notebook — always loaded</span>
    <div class="flow-row">
      <div class="flow-node data">
        <span class="node-label">💾 memory.md</span>
        <span class="node-sub">environment facts</span>
      </div>
      <div class="flow-node data">
        <span class="node-label">👤 user.md</span>
        <span class="node-sub">user preferences</span>
      </div>
    </div>
    <div class="flow-label">Budget: 2,000 chars (auto-compressed every turn)</div>
  </div>

  <div class="flow-arrow"></div>

  <div class="flow-group">
    <span class="flow-group-label">Layer 2 · Vector store — on demand</span>
    <div class="flow-row">
      <div class="flow-node data">
        <span class="node-label">🗄 Honcho</span>
        <span class="node-sub">inferred preferences</span>
      </div>
      <div class="flow-node data">
        <span class="node-label">🗄 pgvector</span>
        <span class="node-sub">full session history</span>
      </div>
    </div>
    <div class="flow-label">Capacity: unlimited · retrieved via similarity search</div>
  </div>

  <div class="flow-arrow"></div>

  <div class="flow-row">
    <div class="flow-node output">
      <span class="node-label">→ Next session</span>
      <span class="node-sub">continuity preserved</span>
    </div>
  </div>
</div>

<div class="small">

**Honcho memory** runs end-of-session: it digests the conversation, infers preferences the user never explicitly stated, and writes them back into `user.md` automatically.

</div>

---

# 📈 The Skill Compound Loop

> The skill manual is the engine of compounding. Each run writes to it; the next run reads from it.

<div class="flow-chart">
  <div class="flow-row">
    <div class="flow-node simple">
      <span class="node-label">① First run</span>
      <span class="node-sub">trial and error</span>
    </div>
  </div>
  <div class="flow-arrow"></div>
  <div class="flow-row">
    <div class="flow-node simple">
      <span class="node-label">② Success path</span>
      <span class="node-sub">identified</span>
    </div>
  </div>
  <div class="flow-arrow"></div>
  <div class="flow-row">
    <div class="flow-node data">
      <span class="node-label">③ Manual</span>
      <span class="node-sub">auto-written to skill.md</span>
    </div>
  </div>
  <div class="flow-arrow"></div>
  <div class="flow-row">
    <div class="flow-node simple">
      <span class="node-label">④ Next run</span>
      <span class="node-sub">consults manual</span>
    </div>
  </div>
  <div class="flow-arrow"></div>
  <div class="flow-row">
    <div class="flow-node output">
      <span class="node-label">⑤ Faster</span>
      <span class="node-sub">execution speed ↑</span>
    </div>
  </div>
  <div class="flow-arrow"></div>
  <div class="flow-row">
    <div class="flow-node simple">
      <span class="node-label">⑥ More experience</span>
      <span class="node-sub">feeds back into ③</span>
    </div>
  </div>
</div>

<div class="small">

> **Chatbot**: starts from zero every run.
> **Hermes**: yesterday's output is today's starting point.

⚠️ **Overfit warning**: skills can ossify. The user must periodically audit the manual.

</div>