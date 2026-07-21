# ascii-system-map

An agent skill for Claude Code and Codex that turns any PR, endpoint, feature, or incident into a scannable ASCII scope map.

![ascii-system-map in an agent session](docs/demo.png)

Instead of a wall of prose, it draws a plain-text tree: live behavior separated from docs, tests, and scaffolding, confirmed facts marked apart from assumptions. Paste it into a PR description, Slack thread, or review comment; it renders everywhere.

## Why

Reviewing a change means answering the same questions every time: what actually changes in production, what is just tests and tooling, and what got quietly left out. Prose buries those answers; a tree surfaces them.

- **Scope at a glance.** Live behavior, diagnostics, docs/tests, and deferred work land in separate branches, so the shape of the change is visible before any file is opened.
- **Honest by design.** The skill grounds every node in the diff, the docs, or your notes. It refuses to invent components; anything inferred is labeled as an assumption, and investigations separate confirmed from working theory.
- **Reviewer-first.** Each map can end with a one-paragraph takeaway: where the risk is, what deserves attention, what is explicitly out of scope.
- **Plain text travels.** No rendering, no image uploads. The same map works in a PR body, a commit message, a Slack thread, or a terminal.

## Install

```bash
git clone https://github.com/aviju888/ascii-system-map.git
```

Claude Code:

```bash
mkdir -p ~/.claude/skills/ascii-system-map
cp ascii-system-map/SKILL.md ~/.claude/skills/ascii-system-map/
```

Codex:

```bash
mkdir -p ~/.codex/skills/ascii-system-map
cp -R ascii-system-map/SKILL.md ascii-system-map/agents ~/.codex/skills/ascii-system-map/
```

## Use

The skill activates whenever you ask your agent for a scope map, PR map, ASCII diagram, or "what is included" breakdown:

```
map out what's in this PR
give me an ascii map of the /api/export call chain
visualize this incident: what's confirmed vs assumed
draw the build plan as a tree: phases, artifacts, verification
```

It adapts the grouping to the subject: PRs get live-behavior / diagnostics / docs-tests / deferred branches, endpoints get entrypoint / orchestration / external-calls / writes / response branches, and build plans get phases with inputs, outputs, and verification steps.

Ships with templates for PR scope maps and endpoint/call maps, plus a quality bar the output has to meet: every node anchored to a file, table, or command where possible, and no vague "misc changes" nodes allowed. Ask for strict ASCII (`|`, `+--`) if your destination cannot render Unicode tree glyphs.

## License

MIT
