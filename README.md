# ascii-system-map

A Claude Code skill that turns any PR, endpoint, feature, or incident into a scannable ASCII scope map.

Instead of a wall of prose about what a change includes, you get a text tree that separates live behavior from docs, tests, tools, and scaffolding, and marks what is confirmed versus assumed. Paste it straight into a PR description, Slack thread, or review comment; it is plain text, so it renders everywhere.

```text
PR #123: rate-limit the export endpoint
│
├─ 1) Live Behavior
│  │
│  ├─ POST /api/export
│  │  ├─ old: unlimited concurrent exports
│  │  └─ new: 3 per user, 429 + Retry-After beyond that
│  │
│  └─ side effect
│     └─ export_jobs table gains status column
│
├─ 2) Diagnostics / Observability
│  ├─ rate_limit_hit event
│  └─ queue depth now visible in logs
│
├─ 3) Docs + Tests
│  ├─ docs/exports.md
│  └─ 6 focused tests (limit, burst, retry header)
│
└─ 4) Not Included / Deferred
   ├─ per-org limits (assumption: per-user is enough)
   └─ admin override UI
```

## Why

- **Scope at a glance.** What changes live behavior, what is just tooling, what is deferred.
- **Honest by design.** The skill refuses to invent components; inferred nodes are labeled as assumptions.
- **Reviewer-first.** A good map answers "what should I focus on?" before anyone opens a file.

## Install

```bash
git clone https://github.com/aviju888/ascii-system-map.git
mkdir -p ~/.claude/skills/ascii-system-map
cp ascii-system-map/SKILL.md ~/.claude/skills/ascii-system-map/
```

## Use

The skill activates whenever you ask Claude Code for a scope map, PR map, ASCII diagram, or "what is included" breakdown:

```
map out what's in this PR
give me an ascii map of the /api/export call chain
visualize this incident: what's confirmed vs assumed
```

Ships with templates for PR scope maps and endpoint/call maps, plus a quality bar the output has to meet (no vague "misc changes" nodes allowed).

## License

MIT
