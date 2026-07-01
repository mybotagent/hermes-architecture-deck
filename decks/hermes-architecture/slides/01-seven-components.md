# Chatbots forget. Hermes compounds.

> A chatbot has a brain. An employee has seven organs.
> Hermes configures all seven so the system gets smarter every run.

## Side by side

| | Chatbot | Hermes |
|---|---|---|
| **Brain** (intelligence) | ✅ | ✅ |
| **Hands** (execution) | ❌ | ✅ 20+ tools |
| **Memory** (continuity) | ❌ resets per session | ✅ notebook + vector |
| **Manual** (self-improvement) | ❌ | ✅ skill.md |
| **Channel** (gateway) | web only | ✅ 20+ (Discord, Telegram, Slack) |
| **Alarm** (automation) | ❌ | ✅ cron |
| **Soul** (persona) | system prompt | ✅ soul.md |

<div class="small">

> Swap the brain, keep the memory, keep the soul — the brain is the only replaceable module.

</div>

---

# 🧠 The Seven Components

<div class="flow-tree">
<span class="node">[Long-term Organs — persist across swaps]</span>

    🧠 Brain       →  config            (replaceable AI model)
    👻 Soul        →  soul.md           (persona + tone + taboos)
    💾 Memory      →  memory.md + user  (notebook, 2KB budget)
    📖 Manual      →  skill.md          (self-written procedures)

<span class="node">[Employee-ization Devices — external interfaces]</span>

    🛠 Hands        →  tools              (terminal, file, web, delegate)
    📡 Channel     →  20+ gateway         (Discord, Telegram, Slack…)
    ⏰ Alarm       →  cron                (auto-wake, work, sleep)

<span class="node">[Flow]</span>
    User → Channel → Brain → Soul → Memory → Manual → Hands → User
                                              ↑
                                       Alarm (cron) auto-triggers Brain
</div>

<div class="small">

**Front 4 = long-term** (survive brain swap) · **Back 3 = employee-ization** (external surface)

</div>

---

# Memory in Two Layers

<div class="flow-tree">
<span class="node">[Layer 1: Notebook — always loaded, 2KB budget]</span>

    memory.md + user.md
    → distilled every turn
    → critical facts only

<span class="node">[Layer 2: Vector DB — retrieved on demand]</span>

    Honcho / pgvector
    → full history available
    → loaded when relevant

<span class="node">[Honcho memory]</span>
    End-of-session → user never said → infers preference
    → writes back to notebook automatically
</div>

| Layer | Storage | Loaded | Capacity |
|---|---|---|---|
| **Notebook** | `memory.md` + `user.md` | every session | 2K chars (compressed) |
| **Vector** | Honcho / pgvector | on demand | unlimited |

---

# 📈 The Skill Compound Loop

<div class="flow-tree">
<span class="node">[The compounding cycle]</span>

    ┌─ First run: trial-and-error ─────────────┐
    │                                            │
    │   ▼                                        │
    │  Success                                    │
    │   │                                        │
    │   ▼                                        │
    │  Manual auto-written                        │
    │   │                                        │
    │   ▼                                        │
    │  Next run: consults manual                  │
    │   │                                        │
    │   ▼                                        │
    │  Faster execution                           │
    │   │                                        │
    │   ▼                                        │
    │  More experience  ─────────────► writes manual
    │
    └───── Compounding ─────┘

<span class="node">[Chatbot vs Hermes]</span>
    Chatbot: starts from zero every run
    Hermes:  yesterday's output → today's starting point
</div>

<div class="small">

⚠️ **Overfit warning**: habits can ossify. The user must periodically audit the manual.

</div>