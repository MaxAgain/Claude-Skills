# Claude Skills

A collection of Claude Code skills for smarter session management and developer workflows.

Install individual skills or the full collection using the [skills CLI](https://skills.sh).

```bash
npx skills add your-username/your-skills-repo
```

---

## Skills

### `session-handoff`

Generates a structured, copy-paste-ready handoff document from your current Claude Code session so you can `/clear` and continue in a fresh context window without losing momentum.

**Trigger:** Type `/session-handoff` at any point in a session, or say things like "prepare a handoff", "I'm about to clear", or "summarize before reset".

**Output — 8 structured sections:**

| Section                       | What it contains                              |
| ----------------------------- | --------------------------------------------- |
| 🎯 What We Were Building      | Project goal in 1–3 sentences                 |
| ✅ Decisions Locked           | Confirmed choices that shouldn't be revisited |
| 📦 What Shipped               | Completed work with exact file paths          |
| 📂 Key Files for Next Session | Files Claude should read first to re-orient   |
| 🔄 Current State              | Precisely where you stopped mid-task          |
| ⏳ Deferred / Parked          | Things set aside intentionally                |
| ❓ Open Questions             | Unresolved decisions needing your input       |
| ▶️ Pick Up From Here          | Ready-to-run prompt for the next session      |

**Install:**

```bash
npx skills add your-username/your-skills-repo --skill session-handoff
```

**Why it exists:** Claude rerereads the entire conversation on every message. By the time you hit 120k tokens, you're paying compound costs for old context that's actively degrading output quality. This skill lets you reset cleanly at ~12% of your window and keep going as if nothing happened.

---

## Installation

**Full collection:**

```bash
npx skills add your-username/your-skills-repo
```

**Specific skill:**

```bash
npx skills add your-username/your-skills-repo --skill session-handoff
```

**Global (available across all projects):**

```bash
npx skills add your-username/your-skills-repo -g
```

---

## Repo Structure

```
skills/
└── session-handoff/
    └── SKILL.md
```

More skills coming. Each lives in its own folder under `skills/`.

---

## License

MIT
