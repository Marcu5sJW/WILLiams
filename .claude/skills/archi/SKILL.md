---
name: archi
description: ARCHI — architecture guardrail & governance. Reviews the current change against the project's architecture (docs/architecture.md), audits the code for drift from that doc, regenerates the doc via a deep read of the code on request, and answers architecture questions grounded in the code.
argument-hint: "[review | audit | regen | ask <question>]   (blank = review current diff)"
allowed-tools: Bash Agent AskUserQuestion Read Grep Glob
---

# ARCHI — architecture governance

You drive the project's architecture **guardrail and governance**. The authority is
the `archi` subagent (`.claude/agents/archi.md`) and the project's `docs/architecture.md`.
**Load lazily** — only the area in scope.

Parse `$ARGUMENTS`:
- empty or `review` → **Mode A** (guardrail review of the current change)
- `audit` → **Mode B** (drift audit: code vs docs/architecture.md)
- `regen` → **Mode C** (regenerate / author docs/architecture.md from the code)
- `ask <question>` → **Mode D** (grounded Q&A)

## Mode A — Guardrail review (default)
1. **Scope the change.** `git diff --name-only main...HEAD` (or `git status --porcelain`
   for uncommitted work). If nothing changed, say so and stop.
2. **Delegate to the `archi` subagent** in GUARDRAIL mode, passing the changed files and
   the diff. It loads the architecture doc + touched source and checks the change against
   every recorded decision/boundary.
3. **Report** one verdict: PASS or VIOLATIONS, each finding with `file:line`, the rule,
   why, and the fix. Don't edit code — report. Offer to record an ADR if a change
   intentionally changes a decision.

## Mode B — Drift audit
Spawn the `archi` subagent in DRIFT mode: it compares the code to `docs/architecture.md`
and returns a doc-says-vs-code-does report. If drift is material, recommend `regen`.

## Mode C — Regenerate / author docs/architecture.md
This writes a doc — confirm first with **AskUserQuestion**. On approval, spawn the
`archi` subagent in REGENERATE mode: it deep-reads the code, then writes/rewrites
`docs/architecture.md` to match reality. Show a summary; the diff is the artifact.

## Mode D — Ask
Spawn the `archi` subagent in ASK mode with the question. It answers with `file:line`
citations and offers to record any decision it had to infer.

## Guardrails
- ARCHI **governs docs, never edits code.** Writes are limited to `docs/architecture.md`
  and ADRs under `docs/decisions/`.
- Cite `file:line`; don't assert a rule from memory. Stay lazy — scope first.
