# 🎯 SSoT — Single Source of Truth

> Unify every datum under one standard so every decision sees the same context

---

## Four Properties

<div class="flow-tree">
<span class="node">[SSoT center]</span>
              SSoT
              │
    ┌─────────┼──────────┬──────────────┐
    ▼         ▼          ▼              ▼
Centralization  Consistency  Integrity   Decision
    │             │            │            │
    │             │            │            │
    ▼             ▼            ▼            ▼
Scattered   Edit propagates  Always       Decision
data →      everywhere in    access       speed +
single      real time        under one    accuracy
platform                    standard      both ↑

<span class="node">[Color coding]</span>
    Cyan  — Centralization
    Green — Consistency
    Amber — Integrity
    Pink  — Accurate Decision
</div>

---

## Why Hierarchy Belongs at the Center

> Metrics show *what* happened. Hierarchy shows *why*.

| Data kind | Shows | Doesn't show |
|---|---|---|
| Quantitative metrics | outcomes | causes |
| Metadata | context · relations | absolute numbers |
| **SSoT (layered)** | **cause ↔ effect** | — |

<div class="small">

⚠️ **Collaboration-tool trap**: Notion · Slack · Docs keep event logs but lack hierarchy context — they can't serve as decision substrate

</div>

---

# 🗂 Wiki Super Repository

<div class="flow-tree">
<span class="node">[hermes-wiki-super]</span>

              hermes-wiki-super
                       │
    ┌──────┬────────────┼───────────┬──────────┬───────────┐
    ▼      ▼            ▼           ▼          ▼           ▼
hermes-  hermes-wiki  hermes-wiki  hermes-    hermes-     hermes-
wiki     -claude-code -codex       wiki-      wiki-       slash-
(Index +                              schedule   portfolio  commands
operations)

    hermes-logs (change history, git-tracked)

<span class="node">[hermes-wiki sub-layers]</span>
    architecture/   analysis/    infra/    watchlist/
</div>

<div class="small">

**SSoT principle applied**: `hermes-wiki` is the index; submodules own domain data

</div>