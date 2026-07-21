---
name: ascii-system-map
description: Create concise text-tree visualizations of what is included in a PR, feature, system, workflow, incident, or build plan. Use when the user asks for an ASCII diagram, ASCII visualization, PR map, scope map, architecture map, endpoint/call map, “what is included,” “visualize this,” or wants a clear map of live code vs docs/tests/tools/scaffolding.
---

# ASCII System Map

## Purpose

Turn scattered implementation or proposal details into a sendable text-tree map. The output should make scope, flow, ownership, and uncertainty easy to scan without pretending unsupported details are facts.

## Workflow

1. Ground the map in available evidence.
   - Inspect the PR diff, local files, docs, issue, or user-provided notes when available.
   - Do not invent components. If a node is inferred, label it as inferred or assumption.
   - If the user asks for a review-style map, separate live behavior from docs/tests/tools/scaffolding.

2. Choose the root label.
   - Use the PR number/title, feature name, endpoint name, or system name.
   - Include the current status if it matters: draft, live-impacting, scaffolding-only, telemetry-only, deferred.

3. Group by what the user needs to understand.
   - For PRs: use groups like live behavior, data model, instrumentation, tools, docs/tests, deferred work, risks.
   - For endpoints: use request entrypoint, orchestration, child calls, external services, writes, return path, failure modes.
   - For build plans: use phases, inputs, outputs, ledgers/artifacts, verification, follow-ups.

4. Draw a compact text tree.
   - Prefer tree glyphs (`│`, `├─`, `└─`) when the user’s example uses them.
   - Use strict ASCII (`|`, `+--`, `\--`) if the user explicitly says strict ASCII, terminal-safe, or no Unicode.
   - Use arrows only when they clarify data or control flow.
   - Keep branch labels short; put the explanation on the child lines.

5. Add status and evidence cues.
   - Mark behavior as `live`, `diagnostic`, `docs/tests`, `scaffolding`, `deferred`, or `assumption` when helpful.
   - Include file paths, PR links, table names, endpoint names, or command names when they anchor the map.
   - For investigations, distinguish `confirmed` from `working assumption`.

6. End with the high-signal takeaway when useful.
   - State what the map shows about scope or risk in one short paragraph.
   - If the user asked only for the diagram, skip extra commentary.

## Templates

### PR Scope Map

```text
PR #123: short title
│
├─ 1) Live Behavior
│  │
│  ├─ endpoint_or_service
│  │  ├─ old behavior changed
│  │  └─ new behavior/output
│  │
│  └─ external side effect
│     └─ table/API/task touched
│
├─ 2) Diagnostics / Observability
│  │
│  ├─ new events/logs
│  ├─ new metadata
│  └─ failure states now visible
│
├─ 3) Tools / Local Artifacts
│  │
│  └─ tool_or_script.py
│     ├─ mode A
│     ├─ mode B
│     └─ writes local output path
│
├─ 4) Docs + Tests
│  ├─ doc path
│  └─ focused tests
│
└─ 5) Not Included / Deferred
   ├─ fix not implemented yet
   └─ assumption still unproven
```

### Endpoint / Call Map

```text
POST /api/example
│
├─ auth / validation
│  ├─ checks input
│  └─ rejects invalid request
│
├─ orchestration
│  ├─ creates ledger row
│  ├─ calls service A
│  ├─ calls service B
│  └─ records terminal status
│
├─ external calls
│  ├─ provider API
│  └─ queue/task system
│
├─ writes
│  ├─ table_one
│  └─ table_two
│
└─ response
   ├─ success shape
   └─ known failure modes
```

## Quality Bar

A good map answers these questions quickly:

- What is included?
- What code or system behavior changes live behavior?
- What is only docs, tests, probes, or scaffolding?
- What calls what?
- Where are data writes or external side effects?
- What is not proven or not included?
- What should a reviewer focus on?

Avoid vague nodes like “misc changes.” Split them into real components or omit them.
