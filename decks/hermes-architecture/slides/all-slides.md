# How We Run It

<p>The seven components, in production. What each one does, what files back it, and what we observed after months of use.</p>

---

# Brain

<p>The Brain is the only replaceable piece. Everything below it survives a swap.</p>

<pre><code># config — the Brain
model: deepseek-chat
temperature: 0.3
max_tokens: 4096

fallback_chain:
  - claude-sonnet-4.5
  - gpt-5
  - gemini-2.5-pro

# swap history (last six months)
- 2026-01 .. 2026-04 → claude-sonnet-4.5
- 2026-05 .. 2026-06 → gpt-5
- 2026-07 .. now      → deepseek-chat  (cost + latency)</code></pre>

<p>The fallback chain is what matters. When the primary model degrades, the Brain rolls over without losing Memory, Soul, or Manual. Three swaps in six months, none of them user-visible beyond a slight tone shift on the first few responses after each swap.</p>

---

# Soul

<p>The persona lives in <code>soul.md</code>. It is not the system prompt — the system prompt changes with the Brain. The Soul is what stays across swaps.</p>

<pre><code># soul.md — persona and rules of engagement

## identity
- name: the assistant
- role: investment analyst + systems engineer
- voice: precise, calm, occasionally dry
- language: Korean default, English when source is English

## taboos
- never invent numbers — if you don't know, say so
- never recommend a ticker without showing the gap math
- never push urgency — decisions are the user's, not mine

## edge cases
- when the user is wrong, push back with the data, not the tone
- when the data is ambiguous, surface the ambiguity
- when the user hasn't asked, don't volunteer</code></pre>

<p>Edited seven times in the last quarter. Each edit is a small behavioural calibration, not a rewrite. The audit trail lives in the change log.</p>

---

# Memory

<p>One layer. The notebook. It is loaded every turn and compressed when it grows past 2KB.</p>

<pre><code># user.md (excerpt — actual file is 1,847 chars)
- prefers value investing, single-position sizing 0–20%
- trades US + KR markets, no crypto, no leveraged ETFs
- weekly review on Sunday, monthly on the 5th
- despises filler phrases ("certainly", "I'd be happy to")
- timezone: Asia/Seoul, working hours 09:00–18:00 KST
- has a Korail-style ticker naming preference (alphabetic)</code></pre>

<p>The notebook holds preferences the user has stated, preferences we have inferred, and operational facts (timezone, working hours, deliver format). It is the only Memory the Brain reads every turn. There is no second layer.</p>

---

# Manual

<p><code>skill.md</code> is the engine of compounding. Every successful workflow writes a procedure here; the next time, the procedure is read instead of rediscovered.</p>

<div style="text-align:center; margin:1em 0;">

1. workflow run
   →
2. procedure written to skill.md
   →
3. next run reads it (faster)
   ↑
4. more experience
   → loops back to 2

</div>

<p><strong>Concrete example</strong> — this very deck started as a skill procedure:</p>

<pre><code># skills/wikihow-to-deck.md
1. take wiki section (h1 + paragraphs)
2. extract flow blocks → render as HTML/CSS divs
3. apply Apple design tokens (SF Pro, Action Blue, white bg)
4. write Reveal.js deck with inline CSS
5. deploy to github.io via git push
6. verified: deck renders identically on iPhone Safari</code></pre>

<p>The skill was written the first time we made a deck. The second deck (this one) followed the same procedure end-to-end. Manual cost: a few minutes. Brain cost without manual: a few hours.</p>

---

# Hands, Channel, Alarm

<p>The three employee-ization devices, working together.</p>

<table>
<thead>
<tr><th>Device</th><th>Backing</th><th>What it actually does</th></tr>
</thead>
<tbody>
<tr><td><strong>Hands</strong></td><td><code>tools</code> in config</td><td>terminal (shell, git, curl), file (read/write md/json/yaml), web (search, fetch), delegate (spawn subagent for deep work)</td></tr>
<tr><td><strong>Channel</strong></td><td>Discord gateway</td><td>One bot, one user, three active channels. Every cron job uses <code>deliver: "origin"</code> after the Home-channel 404 incident.</td></tr>
<tr><td><strong>Alarm</strong></td><td>cron</td><td>Eight jobs on weekdays. Each one wakes the Brain with a fresh context, runs the workflow, reports back, and the Brain goes back to sleep.</td></tr>
</tbody>
</table>

<pre><code># /etc/cron.d/the-assistant
30 20 * * 1-5  run briefing_macro.py
35 20 * * 1-5  run langgraph_pipeline.py
 0 23 * * 1-5  run backup_housekeeping.py
 0  4 * * 1-5  bash scripts/wiki_sync.sh</code></pre>

<p>The Hands+Channel+Alarm trio is what turns the long-term organs into a working employee instead of a brain in a jar.</p>

---

# The Compound Effect

<p>Three loops, all writing back to the long-term organs.</p>

<div style="text-align:center; margin:1em 0;">

<strong>Loop 1 · Manual</strong>
workflow run → procedure written → next run faster

<strong>Loop 2 · Memory</strong>
session ends → notebook updated → next turn starts warmer

<strong>Loop 3 · Pipeline</strong>
monthly review → past calls analysed → prompts refined

</div>

<p>After three months the system runs materially faster on the same inputs — not because the Brain got smarter, but because everything around the Brain got tighter. The Manual is shorter to read. The Memory is already pointed at the right thing. The Pipeline's prompts are sharper.</p>

<p>The compound is in the file system, not in the model weights.</p>

---

# What This Deck Used

<table>
<thead>
<tr><th>Component</th><th>How this deck used it</th></tr>
</thead>
<tbody>
<tr><td><strong>Brain</strong></td><td>drafted content with Claude Sonnet, fallback to DeepSeek for cheaper passes</td></tr>
<tr><td><strong>Soul</strong></td><td>applied the persona — calm, precise, no filler</td></tr>
<tr><td><strong>Memory</strong></td><td>the user.md preference for white-background Apple design carried over</td></tr>
<tr><td><strong>Manual</strong></td><td>followed the <code>wikihow-to-deck</code> procedure verbatim</td></tr>
<tr><td><strong>Hands</strong></td><td>terminal (git push), file (md edits), web (Apple HIG docs), delegate (subagent for layout)</td></tr>
<tr><td><strong>Channel</strong></td><td>delivered through this thread</td></tr>
<tr><td><strong>Alarm</strong></td><td>not used — this was interactive, not cron-triggered</td></tr>
</tbody>
</table>

<p>Six of seven components were exercised to produce this artifact. The seventh is reserved for the next batch.</p>

---

# Links

<div style="text-align:center; margin:1em 0;">

**Live deck**

`https://org-a.example.io/project-a/decks/hermes-architecture/`

**Knowledge**

- project-i — operational wiki
- project-b — super-repo, all submodules
- project-h — change logs

**Code**

- project-j — pipeline + cron runners

**This portfolio**

- project-a — repo + Pages

</div>

# Discord Three-Way Meeting

<p>Three bots share one Discord thread. The user posts once; the three of them figure out who does what.</p>

<h3>The cast</h3>

<ul>
<li><strong>Hermes</strong> (the assistant) — owns Memory and Soul, coordinates dispatch, always speaks first.</li>
<li><strong>Claude Bot A</strong> (Plannerbot) — code and planning. Long context, large file analysis, refactors.</li>
<li><strong>Claude Bot B</strong> (Verifierbot) — research and verification. External lookups, cross-checks numbers, quotes sources.</li>
</ul>

<h3>The flow</h3>

<pre><code>User → Discord thread
        │
        ▼
       Hermes (orchestrator)
        │
        ├── if code touches &gt;200 lines     ──► Claude Bot A
        ├── if claim needs evidence          ──► Claude Bot B
        ├── if both at once                  ──► parallel, then merge
        └── otherwise                        ──► Hermes alone
        │
        ▼
   synthesize
        │
        ▼
   User (one merged reply, not three)</code></pre>

<h3>When each bot speaks</h3>

<table>
<thead>
<tr><th>Bot</th><th>Speaks when</th><th>Stays silent when</th></tr>
</thead>
<tbody>
<tr><td>Hermes</td><td>always, as orchestrator</td><td>—</td></tr>
<tr><td>Claude Bot A</td><td>code is on the table</td><td>task is research-only</td></tr>
<tr><td>Claude Bot B</td><td>facts need cross-checking</td><td>the answer is in Memory already</td></tr>
</tbody>
</table>

<h3>The rule</h3>

<p>Whoever has the most relevant context for the next sentence takes it. No bot speaks for the sake of speaking. Silence is allowed — and preferred — when the orchestrator can answer alone.</p>

---

# Linear + Hermes Kanban

<p>Linear is the source of truth for tickets across the team. Hermes Kanban is the local mirror we actually touch. They sync in both directions via webhooks.</p>

<h3>The topology</h3>

<pre><code>Linear (source of truth, shared with team)
   │
   │ webhook on issue / status / comment
   ▼
Hermes Kanban (local mirror, local-first)
   │
   │ webhook on card move / comment / close
   ▼
Linear (reconciled)</code></pre>

<h3>Why two systems</h3>

<ul>
<li><strong>Linear</strong> — shared with collaborators, public to the team, lives at org-a. The canonical ticket.</li>
<li><strong>Hermes Kanban</strong> — local-first, fast to update, fits the cron rhythm, no round-trip latency.</li>
<li><strong>Each side reflects what the other side did.</strong> We never have to ask "which is up to date" because both are.</li>
</ul>

<h3>What triggers a sync</h3>

<table>
<thead>
<tr><th>Direction</th><th>Trigger</th><th>Field-level conflict resolution</th></tr>
</thead>
<tbody>
<tr><td>Linear → Kanban</td><td>issue created, status changed, comment added</td><td>Linear wins</td></tr>
<tr><td>Kanban → Linear</td><td>card moved, comment added, card closed</td><td>Linear wins on ties</td></tr>
</tbody>
</table>

<h3>The mapping file</h3>

<p>The webhook endpoints and field mappings live in a single config file, kept under version control:</p>

<pre><code># config/kanban_linear_mapping.json
{
  "linear_workspace": "org-a",
  "kanban_board_id": "kanban-main",
  "field_map": {
    "linear.status": "kanban.column",
    "linear.assignee": "kanban.owner",
    "linear.priority": "kanban.priority"
  },
  "webhook_secret_env": "LINEAR_WEBHOOK_SECRET"
}</code></pre>

<h3>Failure mode</h3>

<p>If the webhook is down for more than ten minutes, the cron nightly reconciliation re-syncs both sides from the union of last-known states. We never lose a card to a missed webhook — we may lose five minutes of latency.</p>

---

<div style="text-align:center; font-size:0.7em; color:#6e6e73; margin-top:2em;">

Generated by the assistant. White-mode Apple-inspired design.

</div>