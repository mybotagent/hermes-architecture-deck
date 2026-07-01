# Chatbots forget. Hermes compounds.

> A chatbot has a brain. An employee has seven organs. Hermes configures all seven so the system gets smarter with every run.

## Comparison: Chatbot vs Hermes

| Capability | Chatbot | Hermes |
|---|---|---|
| **Brain** (intelligence) | ✅ | ✅ |
| **Hands** (execution) | ❌ | ✅ 20+ tools |
| **Memory** (continuity) | ❌ resets every session | ✅ notebook + vector |
| **Manual** (self-improvement) | ❌ | ✅ skill.md |
| **Channel** (gateway) | web only | ✅ 20+ (Discord, Telegram, Slack) |
| **Alarm** (automation) | ❌ | ✅ cron |
| **Soul** (persona) | system prompt | ✅ soul.md |

<div class="small">

> **Key insight**: swap the brain, keep the memory, keep the soul. The brain is the only replaceable module. Everything else survives a model upgrade.

</div>

---

<div class="section-opener">

<span class="section-num">S1 · The Seven Components</span>

# 🧠 Long-Term Organs
### The four components that survive a brain swap

</div>

<div class="flow-chart">
  <div class="flow-row">
    <div class="flow-node long-term">
      <span class="node-label">🧠 Brain</span>
      <span class="node-sub">config</span>
    </div>
  </div>
  <div class="flow-arrow"></div>
  <div class="flow-row">
    <div class="flow-node long-term">
      <span class="node-label">👻 Soul</span>
      <span class="node-sub">soul.md</span>
    </div>
  </div>
  <div class="flow-arrow"></div>
  <div class="flow-row">
    <div class="flow-node long-term">
      <span class="node-label">💾 Memory</span>
      <span class="node-sub">memory.md + user.md</span>
    </div>
  </div>
  <div class="flow-arrow"></div>
  <div class="flow-row">
    <div class="flow-node long-term">
      <span class="node-label">📖 Manual</span>
      <span class="node-sub">skill.md</span>
    </div>
  </div>
</div>

<div class="small">

**These four are persistent** — they don't get re-trained when you swap the underlying model. Only the brain is hot-swappable.

</div>

---

<div class="section-opener">

<span class="section-num">S1 · The Seven Components</span>

# 🛠 Employee-ization Devices
### The three components that turn a brain into an employee

</div>

<div class="flow-chart">
  <div class="flow-row">
    <div class="flow-node tooling">
      <span class="node-label">🛠 Hands</span>
      <span class="node-sub">terminal · file · web · delegate</span>
    </div>
  </div>
  <div class="flow-arrow"></div>
  <div class="flow-row">
    <div class="flow-node tooling">
      <span class="node-label">📡 Channel</span>
      <span class="node-sub">20+ gateway</span>
    </div>
  </div>
  <div class="flow-arrow"></div>
  <div class="flow-row">
    <div class="flow-node tooling">
      <span class="node-label">⏰ Alarm</span>
      <span class="node-sub">cron scheduler</span>
    </div>
  </div>
</div>

<div class="small">

**These three are interfaces** — they connect the agent to the outside world (you, your channels, your schedule). The brain has no idea who you are without these.

</div>

---

# The Wiring — How the Seven Connect

<div class="flow-chart">
  <div class="flow-row">
    <div class="flow-node simple">
      <span class="node-label">👤 User</span>
    </div>
  </div>
  <div class="flow-arrow"></div>
  <div class="flow-row">
    <div class="flow-node tooling">
      <span class="node-label">📡 Channel</span>
      <span class="node-sub">gateway</span>
    </div>
  </div>
  <div class="flow-arrow"></div>
  <div class="flow-group">
    <span class="flow-group-label">Long-term organs</span>
    <div class="flow-row">
      <div class="flow-node long-term">
        <span class="node-label">🧠 Brain</span>
      </div>
      <div class="flow-arrow right"></div>
      <div class="flow-node long-term">
        <span class="node-label">👻 Soul</span>
      </div>
      <div class="flow-arrow right"></div>
      <div class="flow-node long-term">
        <span class="node-label">💾 Memory</span>
      </div>
      <div class="flow-arrow right"></div>
      <div class="flow-node long-term">
        <span class="node-label">📖 Manual</span>
      </div>
    </div>
  </div>
  <div class="flow-arrow"></div>
  <div class="flow-row">
    <div class="flow-node tooling">
      <span class="node-label">🛠 Hands</span>
      <span class="node-sub">tools</span>
    </div>
  </div>
  <div class="flow-arrow"></div>
  <div class="flow-row">
    <div class="flow-node simple">
      <span class="node-label">👤 User</span>
    </div>
  </div>
</div>

<div class="small">

**Parallel path**: `⏰ Alarm` (cron) auto-triggers `🧠 Brain` at scheduled hours — no user prompt required.

</div>