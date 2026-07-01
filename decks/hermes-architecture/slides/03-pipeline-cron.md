# ⚙️ Automation Pipeline — End to End

> From cron trigger to deliverable, every step is a deterministic transformation. The agent is one node in a larger pipeline, not the whole thing.

<div class="flow-chart">
  <div class="flow-row">
    <div class="flow-node compute">
      <span class="node-label">⏰ Cron trigger</span>
      <span class="node-sub">scheduled fire</span>
    </div>
  </div>
  <div class="flow-arrow"></div>
  <div class="flow-row">
    <div class="flow-node data">
      <span class="node-label">📥 capture.py</span>
      <span class="node-sub">parse → snapshot.json</span>
    </div>
  </div>
  <div class="flow-arrow"></div>
  <div class="flow-row">
    <div class="flow-node data">
      <span class="node-label">🔍 filter.py</span>
      <span class="node-sub">threshold filter → filtered_topN.json</span>
    </div>
  </div>
  <div class="flow-arrow"></div>
  <div class="flow-row">
    <div class="flow-node long-term">
      <span class="node-label">🧠 main.py</span>
      <span class="node-sub">multi-agent chain · N LLM calls</span>
    </div>
  </div>
  <div class="flow-arrow"></div>
  <div class="flow-group">
    <span class="flow-group-label">Two parallel outputs</span>
    <div class="flow-row">
      <div class="flow-node data">
        <span class="node-label">📊 logs/analysis/</span>
        <span class="node-sub">structured trace</span>
      </div>
      <div class="flow-arrow right"></div>
      <div class="flow-node data">
        <span class="node-label">📦 allocator.py</span>
        <span class="node-sub">resource decision (1 call)</span>
      </div>
    </div>
  </div>
  <div class="flow-arrow"></div>
  <div class="flow-row">
    <div class="flow-node output">
      <span class="node-label">📤 report.py → 📱 Notify</span>
      <span class="node-sub">Discord / Telegram / Slack</span>
    </div>
    <div class="flow-node output">
      <span class="node-label">📈 current.json</span>
      <span class="node-sub">daily snapshot</span>
    </div>
  </div>
</div>

<div class="small">

**Storage layout**: `~/.hermes/{snapshot, filtered, analysis, alloc, daily}/` — every stage persists. Nothing is computed twice.

</div>

---

# Cron Schedule — When the System Wakes

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

**KST = CST + 1h**. Weekday-focused. `deliver: "origin"` recommended everywhere to avoid 404.

</div>

---

# 🛡 Self-Healing Watchdog

> Three consecutive 404s on a dangerous deliver pattern trigger an automatic origin patch. The system heals itself.

<div class="flow-chart">
  <div class="flow-row">
    <div class="flow-node simple">
      <span class="node-label">⏰ Cron fires</span>
    </div>
  </div>
  <div class="flow-arrow"></div>
  <div class="flow-decision">404 returned?</div>
  <div class="flow-arrow"></div>
  <div class="flow-row">
    <div class="flow-node output">
      <span class="node-label">✅ No → normal exit</span>
    </div>
    <div class="flow-decision">Yes → dangerous pattern?</div>
  </div>
  <div class="flow-arrow"></div>
  <div class="flow-row">
    <div class="flow-decision">counter ≥ 3?</div>
  </div>
  <div class="flow-arrow"></div>
  <div class="flow-row">
    <div class="flow-node data">
      <span class="node-label">🔧 Atomic patch</span>
      <span class="node-sub">jobs.json → "origin"</span>
      <span class="node-sub">+ .bak backup</span>
    </div>
  </div>
  <div class="flow-arrow"></div>
  <div class="flow-row">
    <div class="flow-node output">
      <span class="node-label">📱 Discord alert</span>
      <span class="node-sub">"auto-fixed N jobs"</span>
    </div>
  </div>
</div>

<div class="small">

**Location**: `~/.hermes/scripts/self_healing_watchdog.sh` — runtime · `trade-pipeline/_infra_backup/` — git-tracked double-safety.

</div>