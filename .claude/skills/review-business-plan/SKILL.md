---
name: review-business-plan
description: BUSINESS-REVIEWER — pressure-test a business plan, pitch, or strategy document. Runs four lenses — challenge (devil's advocate), steelman (optimist), validate (check technical claims against the codebase), and adjudicate (verdict + priority fix list). Read-only; produces findings, never edits the document.
argument-hint: "[challenge | steelman | validate | adjudicate | all] <path-to-document>   (blank = all, ask for the doc)"
allowed-tools: Bash Agent AskUserQuestion Read Grep Glob
---

# BUSINESS-REVIEWER — stress-test a business document

You drive business-document review through the `business-reviewer` subagent
(`.claude/agents/business-reviewer.md`). It is read-only — it produces findings and
verdicts, it never edits the document.

First, resolve the **document path** from `$ARGUMENTS` (or ask the user for it). Then parse
the lens:
- `challenge` → devil's advocate: steelman every weakness, gap, and risk
- `steelman` → optimist: steelman the genuine strengths and upside
- `validate` → check each **technical claim** against the codebase → CONFIRMED /
  PARTIALLY CONFIRMED / NOT FOUND / UNVERIFIABLE with `file:line` evidence
- `adjudicate` → weigh both sides into a verdict + **prioritized fix list**
- `all` or empty → run all four in order (this is the default)

## How to run
Spawn the `business-reviewer` subagent with the document path and the requested lens.
For `all`, run challenge and steelman (they can go in parallel), then validate against
the code, then adjudicate over the combined output. Keep the lenses **distinct** — don't
let the optimist soften the devil's advocate.

## Output
For one lens, that lens's findings. For `all`: four sections (Challenge / Steelman /
Claim-validation table / Adjudication) ending in the prioritized fix list, split into
"must fix before the meeting" vs "strengthen later". Always state what was read and what
couldn't be verified.
