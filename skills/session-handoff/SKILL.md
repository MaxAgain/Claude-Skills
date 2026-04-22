---
name: session-handoff
description: >
  Generates a structured session handoff summary to enable clean context resets without losing progress.
  Use this skill whenever the user types /session-handoff, asks to "wrap up the session", "prepare a handoff",
  "summarize before clearing", "compact the session", or says they're about to reset context.
  Also trigger proactively when the user mentions their token count is getting high (e.g. above 100k),
  or when they say things like "I'm going to /clear soon" or "let's reset". The goal is to produce
  a copy-paste-ready output the user can drop into a fresh session and immediately continue working.
---

# Session Handoff Skill

Produces a structured, copy-paste-ready handoff document from the current session so the user can `/clear` and continue in a fresh context window without losing momentum.

---

## When This Skill Triggers

- User types `/session-handoff`
- User says they're about to clear, compact, or reset
- User asks for a session summary before starting fresh
- Token usage is visibly high and user wants to preserve progress

---

## Your Job

Read back through the **entire current conversation**, extract what matters, and output a single structured handoff block. The output should be:

- **Complete** — the next Claude session should need nothing else to re-orient
- **Concise** — no padding, no re-explaining what's already obvious
- **Opinionated** — make it clear what the next task is, don't leave it ambiguous
- **File-aware** — reference exact file paths and artifact names that were created or modified
- **Copy-paste ready** — formatted so the user can paste it directly into a new `/clear` session

---

## Output Format

Output the handoff inside a clearly labelled block the user can copy wholesale. Use this exact structure:

---

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
SESSION HANDOFF — [Project/Topic Name]
[Date if known, otherwise omit]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

## 🎯 What We Were Building
[1–3 sentences. What is the project/task and what's the end goal.]

## ✅ Decisions Locked
[Bulleted list of confirmed decisions, approaches, or choices that should NOT be revisited.
Be specific. Include why if it's non-obvious.]
- ...

## 📦 What Shipped
[Bulleted list of completed work — files created, features built, tasks finished.
Include exact file paths where relevant.]
- ...

## 📂 Key Files for Next Session
[List of files Claude should read at the start of the next session to re-orient.
Exact paths only. One line each with a brief note on what it contains.]
- path/to/file.ext — [what it is]
- ...

## 🔄 Current State
[Short paragraph. Where exactly are we right now? What's in progress, half-done, or pending?
Be precise — "halfway through implementing X" is better than "working on X".]

## ⏳ Deferred / Parked
[Things that came up but were intentionally set aside. Not forgotten, just not now.]
- ...

## ❓ Open Questions
[Unresolved decisions or things that need the user's input before proceeding.]
- ...

## ▶️ Pick Up From Here
[This is the most important section. Write it as a direct instruction to the next Claude session.
Paste-in prompt style. E.g.: "Read [file]. The next task is to [specific action]. Approach it by [method].
Avoid [known pitfall]."]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Paste this into a fresh session after /clear.
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## Section Guidance

### Decisions Locked

Include architecture choices, rejected approaches (and why), tool selections, naming conventions, confirmed scope. If the user debated something and landed on an answer — lock it here.

### What Shipped

Be granular. "Built the product card component" is weak. "Created `src/components/ProductCard.jsx` with variant selector, price formatting, and Klaviyo add-to-cart event" is strong.

### Key Files for Next Session

Include: main output files, plan/task docs, tracker sheets, config files that were touched, any decision log. Do NOT list every file in the repo — only what Claude needs to read to understand the current state.

### Current State

Write this as if handing off to a colleague who just walked in. They need to know exactly where you stopped mid-sentence.

### Pick Up From Here

This should be a ready-to-run prompt. Write it in second person directed at the next Claude ("You are continuing work on..."). Include:

- What to read first
- What the immediate next action is
- Any gotchas or pitfalls discovered this session
- The desired output of the next task

---

## Tone & Style

- Terse and precise. No filler.
- Use exact names, paths, and values — never vague references.
- If something is uncertain, flag it explicitly rather than glossing over.
- The "Pick Up From Here" section should read like a confident handoff brief, not a vague to-do.

---

## After Output

Once you've produced the handoff block, tell the user:

> "Ready to hand off. Copy the block above, run `/clear`, paste it in, and continue. You won't miss a beat."

Do not add anything else after this — keep the signal clean.
