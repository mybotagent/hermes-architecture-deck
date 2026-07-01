# Hermes — How We Use It

<p class="small">A walkthrough of the seven components in production. What they do, how they're configured, and the compound they generate.</p>

---

# The Whole System

<div class="flow-chart">

<div class="flow-row">
  <div class="flow-node simple"><span class="node-label">👤 User</span></div>
</div>
<div class="flow-arrow"></div>
<div class="flow-row">
  <div class="flow-node tooling"><span class="node-label">📡 Channel</span><span class="node-sub">Discord gateway</span></div>
</div>
<div class="flow-arrow"></div>

<div class="flow-group">
  <span class="flow-group-label">Long-term Organs — configured once, survive every brain swap</span>
<div class="flow-row">
  <div class="flow-node long-term"><span class="node-label">🧠 Brain</span><span class="node-sub">config</span></div>
  <div class="flow-arrow right"></div>
  <div class="flow-node long-term"><span class="node-label">👻 Soul</span><span class="node-sub">soul.md</span></div>
  <div class="flow-arrow right"></div>
  <div class="flow-node long-term"><span class="node-label">💾 Memory</span><span class="node-sub">memory + user</span></div>
  <div class="flow-arrow right"></div>
  <div class="flow-node long-term"><span class="node-label">📖 Manual</span><span class="node-sub">skill.md</span></div>
</div>
</div>

<div class="flow-arrow"></div>
<div class="flow-row">
  <div class="flow-node tooling"><span class="node-label">🛠 Hands</span><span class="node-sub">20+ tools</span></div>
</div>
<div class="flow-arrow"></div>
<div class="flow-row">
  <div class="flow-node simple"><span class="node-label">👤 User</span></div>
</div>

<div class="flow-arrow"></div>
<div class="flow-row">
  <div class="flow-node compute"><span class="node-label">⏰ Alarm</span><span class="node-sub">cron auto-wakes Brain</span></div>
</div>

</div>

<div class="small">Everything below zooms into one piece at a time. The wiring stays the same; the depth changes.</div>

---

# 🧠 Brain in Production

<p>Our <code>config</code> pins down the AI model and the operational parameters. The Brain is the only piece we hot-swap; everything else below it stays put.</p>

<pre><code># brain — AI model configuration
model: deepseek-chat
temperature: 0.3
max_tokens: 4096
fallback_chain:
  - claude-sonnet-4.5
  - gpt-5
  - gemini-2.5-pro

# swap history (last 6 months)
- 2026-01 .. 2026-04 → claude-sonnet-4.5
- 2026-05 .. 2026-06 → gpt-5
- 2026-07 .. now    → deepseek-chat  (cost + latency)</code></pre>

<p>The fallback chain is the part that matters: when the primary model degrades or is unavailable, the Brain rolls over without losing <strong>Memory</strong>, <strong>Soul</strong>, or <strong>Manual</strong>.</p>

---

# 👻 Soul in Production

<p>The persona lives in <code>soul.md</code>. It's not the system prompt — those change with the Brain. The Soul is what stays.</p>

<pre><code># soul.md — persona and rules of engagement

## identity
- name: 채니봇 (Chani)
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

<p>The Soul has been edited seven times in the last quarter. Each edit is a small behavioural calibration, not a rewrite. The audit trail lives in <code>hermes-logs</code>.</p>

---

# 💾 Memory in Production

<p>Two layers, both actively used.</p>

<div class="flow-chart">
<div class="flow-row">
<div class="flow-node data"><span class="node-label">📓 Notebook</span><span class="node-sub">memory.md + user.md</span><span class="node-sub">2KB · always loaded</span></div>
<div class="flow-arrow right"></div>
<div class="flow-node data"><span class="node-label">🗄 Vector store</span><span class="node-sub">Honcho / pgvector</span><span class="node-sub">unlimited · on demand</span></div>
</div>
</div>

<pre><code># user.md (excerpt — actual file is 1,847 chars)
- prefers value investing, single-position sizing 0–20%
- trades US + KR markets, no crypto, no leveraged ETFs
- weekly review on Sunday, monthly on the 5th
- despises filler phrases ("certainly", "I'd be happy to")
- timezone: Asia/Seoul, working hours 09:00–18:00 KST
- has a Korail-style ticker naming preference (alphabetic)</code></pre>

<p>Honcho runs end-of-session: it digests the conversation, infers preferences the user never stated, and writes them back. The Notebook is what loads every turn. The Vector store is what loads when the Notebook says "look this up".</p>

---

# 📖 Manual in Production

<p><code>skill.md</code> is the engine of compounding. Every successful workflow writes a procedure here; the next time, the procedure is read instead of rediscovered.</p>

<div class="flow-chart">
<div class="flow-row">
<div class="flow-node simple">① run workflow</div>
<div class="flow-arrow right"></div>
<div class="flow-node data">② write procedure to skill.md</div>
<div class="flow-arrow right"></div>
<div class="flow-node output">③ next run reads it → faster</div>
</div>
<div class="flow-arrow"></div>
<div class="flow-row">
<div class="flow-node simple">④ more experience</div>
<div class="flow-arrow up"></div>
<div class="flow-node data">back to ②</div>
</div>
</div>

<p><strong>Concrete example</strong> — this very deck started as a skill.md procedure:</p>

<pre><code># skills/wikihow-to-deck.md
1. take wiki section (h1 + paragraphs)
2. extract mermaid blocks → render to PNG via mmdc
3. apply Apple design tokens (SF Pro, Action Blue, white bg)
4. write Reveal.js deck with inline CSS
5. deploy to github.io via git push
6. verified: deck renders identically on iPhone Safari</code></pre>

<p>The skill was written the first time we made a deck. The second deck (this one) followed the same procedure end-to-end. Manual cost: a few minutes. Brain cost without manual: a few hours.</p>

---

# 🛠 Hands in Production

<p>Four tool families, each used daily.</p>

<table>
<thead>
<tr><th>Family</th><th>What it does</th><th>Used for</th></tr>
</thead>
<tbody>
<tr><td><strong>Terminal</strong></td><td>shell exec, scripts, git, curl</td><td>cron jobs, file ops, repo syncs</td></tr>
<tr><td><strong>File</strong></td><td>read/write markdown, JSON, YAML</td><td>wiki edits, config updates, log writes</td></tr>
<tr><td><strong>Web</strong></td><td>search, fetch, scrape</td><td>news briefings, market data, doc lookup</td></tr>
<tr><td><strong>Delegate</strong></td><td>spawn Claude Code / Codex subagents</td><td>deep code work, large refactors</td></tr>
</tbody>
</table>

<p>The four families are wired through <code>tools</code> in the config — each one is a function the Brain can call. When a workflow needs more than one, they chain:</p>

<div class="flow-chart">
<div class="flow-row">
<div class="flow-node simple">fetch news</div>
<div class="flow-arrow right"></div>
<div class="flow-node data">summarize via Ollama</div>
<div class="flow-arrow right"></div>
<div class="flow-node output">write to Obsidian</div>
</div>
</div>

---

# 📡 Channel in Production

<p>The Discord gateway is the front door. One bot, one user, three active channels.</p>

<table>
<thead>
<tr><th>Channel</th><th>Purpose</th><th>Cron?</th></tr>
</thead>
<tbody>
<tr><td><code>#portfolio</code></td><td>daily portfolio report at 08:10 KST</td><td>yes</td></tr>
<tr><td><code>#briefing</code></td><td>US market close briefing at 19:00 KST</td><td>yes</td></tr>
<tr><td><code>#knowledge</code></td><td>direct conversation, ad-hoc threads</td><td>no</td></tr>
</tbody>
</table>

<p>Every cron job uses <code>deliver: "origin"</code> for routing — the webhook default caused three consecutive 404s on the Home channel, which is what prompted the self-healing watchdog.</p>

---

# ⏰ Alarm in Production

<p>Eight cron jobs run on weekdays. Five more run weekly or monthly.</p>

<div class="flow-chart">
<div class="flow-row">
<div class="flow-node compute"><span class="node-label">⏰ 05:00 KST</span><span class="node-sub">wiki sync</span></div>
<div class="flow-arrow right"></div>
<div class="flow-node compute"><span class="node-label">⏰ 08:00</span><span class="node-sub">calendar digest</span></div>
<div class="flow-arrow right"></div>
<div class="flow-node compute"><span class="node-label">⏰ 08:10</span><span class="node-sub">morning portfolio</span></div>
<div class="flow-arrow right"></div>
<div class="flow-node compute"><span class="node-label">⏰ 18:35</span><span class="node-sub">analysis chain</span></div>
<div class="flow-arrow right"></div>
<div class="flow-node compute"><span class="node-label">⏰ 23:30</span><span class="node-sub">backup</span></div>
</div>
</div>

<p>Each job triggers the Brain with a fresh context, runs the chain, and reports back. The Brain doesn't sit idle waiting — it gets woken, works, reports, and goes back to sleep.</p>

<pre><code># /etc/cron.d/hermes
30 20 * * 1-5  hermes-agent run briefing_macro.py
35 20 * * 1-5  hermes-agent run langgraph_pipeline.py
0 23 * * 1-5  hermes-agent run backup_housekeeping.py
0 4  * * 1-5  bash /home/hermes/scripts/wiki_sync.sh</code></pre>

---

# The Three Compound Loops

<p>Every long-term organ is fed by a loop. The loops are what make the system compound instead of stagnate.</p>

<div class="flow-chart">

<div class="flow-group">
<span class="flow-group-label">Loop 1 · Skill Compound</span>
<div class="flow-row">
<div class="flow-node simple">workflow run</div>
<div class="flow-arrow right"></div>
<div class="flow-node data">procedure written</div>
<div class="flow-arrow right"></div>
<div class="flow-node output">next run is faster</div>
</div>
</div>

<div class="flow-arrow"></div>

<div class="flow-group">
<span class="flow-group-label">Loop 2 · Memory Compound</span>
<div class="flow-row">
<div class="flow-node simple">session ends</div>
<div class="flow-arrow right"></div>
<div class="flow-node data">Honcho digests</div>
<div class="flow-arrow right"></div>
<div class="flow-node output">preferences written</div>
</div>
</div>

<div class="flow-arrow"></div>

<div class="flow-group">
<span class="flow-group-label">Loop 3 · Pipeline Compound</span>
<div class="flow-row">
<div class="flow-node simple">monthly review</div>
<div class="flow-arrow right"></div>
<div class="flow-node data">analysis of past calls</div>
<div class="flow-arrow right"></div>
<div class="flow-node output">prompts refined</div>
</div>
</div>

</div>

<p>All three loops write back to long-term organs. After three months the system runs materially faster on the same inputs — not because the Brain got smarter, but because everything around the Brain got tighter.</p>

---

# 🗂 Wiki SSoT in Practice

<p><code>hermes-wiki</code> is the single source of truth. <code>INDEX.md</code> is the entry point. Every page has <code>related:</code> frontmatter that the Brain follows to walk the graph.</p>

<div class="flow-chart">
<div class="flow-row">
<div class="flow-node long-term"><span class="node-label">📚 hermes-wiki</span><span class="node-sub">SSoT index</span></div>
</div>
<div class="flow-arrow"></div>

<div class="flow-row">
<div class="flow-node data"><span class="node-label">INDEX.md</span><span class="node-sub">all pages · 1-line desc</span></div>
</div>
<div class="flow-arrow"></div>

<div class="flow-row">
<div class="flow-node simple"><span class="node-label">architecture/</span></div>
<div class="flow-node simple"><span class="node-label">analysis/</span></div>
<div class="flow-node simple"><span class="node-label">infra/</span></div>
<div class="flow-node simple"><span class="node-label">watchlist/</span></div>
<div class="flow-node simple"><span class="node-label">repos/</span></div>
<div class="flow-node simple"><span class="node-label">people/</span></div>
</div>

</div>

<p>When we ask the Brain a question about how a cron job works, it follows the chain: <code>INDEX.md → infra/cron-jobs.md → related: analysis/langgraph-pipeline.md</code>. The wiki isn't decoration — it's the actual retrieval substrate.</p>

---

# What This Deck Is

<p>This deck itself is a worked example of every component above. The components it exercises:</p>

<table>
<thead>
<tr><th>Component</th><th>How this deck used it</th></tr>
</thead>
<tbody>
<tr><td><strong>Brain</strong></td><td>drafted content with Claude Sonnet, rendered with DeepSeek fallback</td></tr>
<tr><td><strong>Soul</strong></td><td>applied the persona — calm, precise, no filler</td></tr>
<tr><td><strong>Memory</strong></td><td>Honcho inferred "white bg Apple design, no stock content" → written to user.md</td></tr>
<tr><td><strong>Manual</strong></td><td>followed <code>wikihow-to-deck</code> skill.md procedure verbatim</td></tr>
<tr><td><strong>Hands</strong></td><td>terminal (git push), file (md edits), web (Apple HIG docs), delegate (Claude)</td></tr>
<tr><td><strong>Channel</strong></td><td>delivered through this Discord thread</td></tr>
<tr><td><strong>Alarm</strong></td><td>none — this was interactive, not cron-triggered</td></tr>
</tbody>
</table>

<p>Six of seven components were exercised to produce this artifact. The seventh is reserved for the next batch.</p>

---

# 🔗 Links

<div class="card">

**Live deck**
`https://mybotagent.github.io/hermes-architecture-deck/decks/hermes-architecture/`

**Source**
- [mybotagent/hermes-wiki](https://github.com/mybotagent/hermes-wiki) — SSoT
- [mybotagent/hermes-wiki-super](https://github.com/mybotagent/hermes-wiki-super) — all submodules
- [mybotagent/hermes-logs](https://github.com/mybotagent/hermes-logs) — change history

**Pipeline**
- [mybotagent/trade-pipeline](https://github.com/mybotagent/trade-pipeline) — LangGraph + cron code

**This portfolio**
- [mybotagent/hermes-architecture-deck](https://github.com/mybotagent/hermes-architecture-deck) — repo + Pages

</div>

<div class="small">🤖 Generated by Hermes Agent · July 2026 · Apple-inspired white-mode design</div>