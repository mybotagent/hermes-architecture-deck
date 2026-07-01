# ⚙️ The Automation Pipeline

> Cron wakes the system at scheduled hours → captures data → runs a multi-agent chain → notifies → sleeps

---

## Daily Schedule (KST)

| Window | Time | Job | Mode |
|---|---|---|---|
| Pre-dawn | 05:00 | Wiki sync | automated |
| Morning | 08:00 | Calendar digest | automated |
| Morning | 08:30 | System check | automated |
| Evening | 18:35 | Analysis chain | automated |
| Night | 23:30 | Backup + housekeeping | automated |
| Weekly | Mon 08:30 | Weekly plan | automated |
| Monthly | 1st 08:00 | Monthly report | automated |
| Monthly | 5th 08:10 | Monthly review | automated |

<div class="small">

**KST = CST + 1h** · Weekday-focused · `deliver: "origin"` recommended (avoids 404)

</div>

---

## Data Flow (generalized)

<div class="flow-tree">
<span class="node">[Pipeline stages]</span>

    cron output (collected data)
       │  capture.py
       ▼
    snapshot.json
       │  filter.py  (threshold filter)
       ▼
    filtered_topN.json
       │  main.py   (multi-agent chain, N calls)
       ▼
    logs/analysis/YYYYMMDD_HHMM.json
       │           │  report.py
       │           ▼
       │        notify channel
       │           (Discord / Telegram / Slack)
       │
       │  allocator.py (1 call)
       ▼
    current.json + daily snapshot
</div>

<div class="small">

**Storage**: `~/.hermes/{snapshot, filtered, analysis, alloc, daily}/` — every stage persisted

</div>

---

## Cost Structure (monthly budget ₩30,000)

| Item | Cost | Share |
|---|---:|---:|
| Multi-agent chain (N calls) | $1.20 | 9% |
| Resource allocator (1 call) | $0.02 | 0.2% |
| Monthly evaluation (1 call) | $0.05 | 0.4% |
| Other cron (briefings, macro) | $7.68 | 59% |
| **Total** | **$8.95 (₩12,978)** | **43%** |

<div class="small">

💡 **V4 Flash** (DeepSeek) keeps the chain under $0.054/run — 95% cheaper at equivalent quality

</div>