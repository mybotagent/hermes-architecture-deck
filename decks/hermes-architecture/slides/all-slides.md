# ⚡ Hermes

# Configuration Architecture

<div class="small">Seven components. One architecture. Zero re-learning cost.</div>

---

<div class="tldr">

**Long-term** (survive brain swap): 🧠 Brain · 👻 Soul · 💾 Memory · 📖 Manual

**Employee-ization** (external interface): 🛠 Hands · 📡 Channel · ⏰ Alarm

</div>

---

# 🧠 Long-term Organs

> The four components that survive a brain swap.

<div class="flow-chart">
  <div class="flow-node long-term">
    <span class="node-label">🧠 Brain</span>
    <span class="node-sub">config · replaceable AI model</span>
  </div>
  <div class="flow-arrow"></div>
  <div class="flow-node long-term">
    <span class="node-label">👻 Soul</span>
    <span class="node-sub">soul.md · persona, tone, taboos</span>
  </div>
  <div class="flow-arrow"></div>
  <div class="flow-node long-term">
    <span class="node-label">💾 Memory</span>
    <span class="node-sub">memory.md + user.md</span>
  </div>
  <div class="flow-arrow"></div>
  <div class="flow-node long-term">
    <span class="node-label">📖 Manual</span>
    <span class="node-sub">skill.md · self-written procedures</span>
  </div>
</div>

---

# 🛠 Employee-ization

> The three components that turn a brain into an employee.

<div class="flow-chart">
  <div class="flow-node tooling">
    <span class="node-label">🛠 Hands</span>
    <span class="node-sub">20+ tools · terminal, file, web, delegate</span>
  </div>
  <div class="flow-arrow"></div>
  <div class="flow-node tooling">
    <span class="node-label">📡 Channel</span>
    <span class="node-sub">20+ gateway · Discord, Telegram, Slack</span>
  </div>
  <div class="flow-arrow"></div>
  <div class="flow-node tooling">
    <span class="node-label">⏰ Alarm</span>
    <span class="node-sub">cron · auto-wake, work, sleep</span>
  </div>
</div>

---

# 💾 Memory — Two Layers

<div class="flow-chart">
  <div class="flow-node data">
    <span class="node-label">📓 Notebook</span>
    <span class="node-sub">memory.md + user.md</span>
    <span class="node-sub">2KB · always loaded</span>
  </div>
  <div class="flow-arrow right"></div>
  <div class="flow-node data">
    <span class="node-label">🗄 Vector store</span>
    <span class="node-sub">Honcho / pgvector</span>
    <span class="node-sub">unlimited · on-demand</span>
  </div>
</div>

<div class="small">Honcho runs end-of-session and writes inferred preferences back to user.md.</div>

---

# 📖 Manual — Skill Compound Loop

<div class="flow-chart">
  <div class="flow-row">
    <div class="flow-node simple">① run</div>
    <div class="flow-arrow right"></div>
    <div class="flow-node data">② manual written</div>
    <div class="flow-arrow right"></div>
    <div class="flow-node output">③ faster</div>
  </div>
  <div class="flow-arrow"></div>
  <div class="flow-node simple">④ more experience → loops back to ②</div>
</div>

<blockquote>

> Chatbot starts from zero every run.
> Hermes: yesterday's output is today's starting point.

</blockquote>

---

# 🔗 Links

**Live deck**
`https://mybotagent.github.io/hermes-architecture-deck/decks/hermes-architecture/`

- [mybotagent/hermes-wiki](https://github.com/mybotagent/hermes-wiki) — source wiki
- [mybotagent/hermes-wiki-super](https://github.com/mybotagent/hermes-wiki-super) — super repo
- [mybotagent/trade-pipeline](https://github.com/mybotagent/trade-pipeline) — pipeline code
- [mybotagent/hermes-architecture-deck](https://github.com/mybotagent/hermes-architecture-deck) — this portfolio