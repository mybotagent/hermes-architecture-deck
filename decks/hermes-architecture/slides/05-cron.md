# ⏰ Cron Auto-Alarm

> At scheduled hours the system **auto-wakes** → works → reports → sleeps

---

## System Operations Schedule

| Window | Time | Job | Mode |
|---|---|---|---|
| Daily | 05:00 | Wiki sync | automated |
| Weekday | 08:00 | Calendar digest | automated |
| Weekday | 18:35 | Analysis chain | automated |
| Weekly | Mon 08:30 | Weekly plan | automated |
| Monthly | 1st 08:00 | Monthly report | automated |
| Monthly | 5th 08:10 | Monthly review | automated |

<div class="small">

Full cron catalog: `~/.hermes/wiki/infra/cron-jobs.md`

</div>

---

## Deliver Pattern Guide

| Pattern | Result | Recommended |
|---|---|:---:|
| `"origin"` | auto-route to current thread | ✅ most |
| `"discord:{HomeID}:{threadId}"` | explicit thread | ✅ most |
| `"local"` | local save only | ⚪ some |
| `"discord:{HomeID}"` (no thread) | **404 guaranteed** | ❌ forbidden |

---

## 🛡 Self-Healing Watchdog

> 3 consecutive 404s on a dangerous deliver pattern → automatic origin patch + Discord alert

<div class="flow-tree">
<span class="node">[Watchdog flow]</span>

    Cron runs
       │  404?
       ▼
    No  → ✅ normal
    Yes →  dangerous pattern match?
              │
              ▼
              No  → ✅ normal
              Yes →  counter +1 (.heal_404_retries.json)
                        │
                        ▼
                        count ≥ 3?
                        │         │
                        No        Yes → 🔧 atomic patch
                        │                jobs.json → "origin"
                        │                + .bak backup
                        ▼
                    📱 Discord alert
</div>

<div class="small">

**Location**: `~/.hermes/scripts/self_healing_watchdog.sh` + `trade-pipeline/_infra_backup/` (git-tracked)

</div>