# Hermes in Production

---

# Brain
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
<div style="text-align:center; margin:1em 0;">

<p><img src="https://mybotagent.github.io/hermes-architecture-deck/decks/hermes-architecture/assets/img/compound-loop.svg?v=7" alt="Skill compound loop" style="max-width:100%;height:auto;"></p>

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
<p><img src="https://mybotagent.github.io/hermes-architecture-deck/decks/hermes-architecture/assets/img/three-loops.svg?v=7" alt="Three compound loops" style="max-width:100%;height:auto;"></p>

<p>After three months the system runs materially faster on the same inputs — not because the Brain got smarter, but because everything around the Brain got tighter. The Manual is shorter to read. The Memory is already pointed at the right thing. The Pipeline's prompts are sharper.</p>

<p>The compound is in the file system, not in the model weights.</p>

---

# How We Remember

<div style="text-align:center; margin:1em 0;">

<p><img src="https://mybotagent.github.io/hermes-architecture-deck/decks/hermes-architecture/assets/img/wiki-architecture.svg?v=7" alt="LLM Wiki + GitHub submodule architecture" style="max-width:100%;height:auto;"></p>

</div>

<p><strong>The pattern in one sentence</strong> — Karpathy's <em>LLM Wiki</em> gives every page a master <code>INDEX.md</code> + concise interlinked pages, and we deploy it as <strong>one super repo with four Git submodules</strong> so each topic gets independent history but one clone gets everything.</p>

<table>
<thead>
<tr><th>Layer</th><th>What lives there</th><th>Why it exists</th></tr>
</thead>
<tbody>
<tr><td><strong>Schema</strong></td><td><code>SCHEMA.md</code> · <code>AGENTS.md</code> · lint rules</td><td>lets an agent extend the wiki without breaking it</td></tr>
<tr><td><strong>Raw</strong></td><td>immutable copies of external sources</td><td>provenance — never edit, only quote</td></tr>
<tr><td><strong>Research</strong></td><td>typed pages: entity / concept / comparison</td><td>frontmatter enables Graph RAG queries</td></tr>
<tr><td><strong>Operational</strong></td><td>infra · analysis · code · repos · people</td><td>free-form knowledge we actually use day-to-day</td></tr>
<tr><td><strong>Logs</strong></td><td>timestamped change history (separate repo)</td><td>every meaningful edit has a diff trail</td></tr>
</tbody>
</table>

<p><strong>Why submodules, not one mega-repo</strong> — each topic lives in its own private GitHub repo (<code>hermes-wiki-claude-code</code>, <code>hermes-wiki-codex</code>, <code>hermes-wiki-super</code>, <code>harness-engineering-wiki</code>). The super repo pulls them in as submodules. Result: independent version history per topic, no merge conflicts, and one <code>git clone --recurse-submodules</code> gives the agent the full KB.</p>

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
