# Token Saver — a Claude Code plugin

Makes Claude Code work **token-efficiently** so your credits/context last longer:
read less, search precisely, cap output, respond terse.

It ships a single skill (`token-saver`) with strict working rules. When the skill
is active, Claude stops the common token-wasters:

- reading whole files when it needs one line (uses `rg` + small ranges instead)
- re-reading files it already read
- `cat`-ing big files / logs / whole directories
- over-explaining and restating the request
- running commands whose output it won't read
- exploring "just in case" after the task is done

---

## Install

### A) As a Claude Code plugin (recommended)

In a Claude Code session:

```
/plugin marketplace add deepuyrf-blip/claude-token-saver
/plugin install token-saver@claude-token-saver
```

Or from your shell:

```bash
claude plugin marketplace add deepuyrf-blip/claude-token-saver
claude plugin install token-saver@claude-token-saver
```

### B) Manual (just the skill)

```bash
mkdir -p ~/.claude/skills/token-saver
curl -fsSL https://raw.githubusercontent.com/deepuyrf-blip/claude-token-saver/main/skills/token-saver/SKILL.md \
  -o ~/.claude/skills/token-saver/SKILL.md
```

### C) Inside this repo's container (web UI setup)

```bash
docker exec -it claude-code-web sh -lc '
  mkdir -p /home/agent/.claude/skills/token-saver &&
  curl -fsSL https://raw.githubusercontent.com/deepuyrf-blip/claude-token-saver/main/skills/token-saver/SKILL.md \
    -o /home/agent/.claude/skills/token-saver/SKILL.md'
```

(Persisted under `data/claude` on the host.)

---

## Use

- **Auto:** the skill loads when relevant (e.g. "explore this codebase", "save
  tokens"). Its description tells Claude when to apply it.
- **Explicit:** run `/token-saver:token-saver` at the start of a session to
  activate the rules.

---

## Make it always-on (recommended)

A skill loads when relevant. To apply the rules to **every** session, paste the
rules into your project's `CLAUDE.md` (or `~/.claude/CLAUDE.md` for all
projects). You can copy the body of
[`skills/token-saver/SKILL.md`](skills/token-saver/SKILL.md) directly.

---

## Honest notes

- This plugin changes **how the agent works** (habits), not the model. It reduces
  wasted tokens; it can't beat a fundamentally expensive task.
- Biggest wins come from **exploration/reading** tasks and long sessions; for a
  one-line change there's little to save.
- If you use a **codebase knowledge graph** (e.g. Graphify), combine it with this —
  query the graph instead of re-reading files.

## License

MIT
