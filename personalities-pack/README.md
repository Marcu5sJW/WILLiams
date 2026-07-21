# Claude Code personalities pack

Five reusable "personalities" (AI teammates) for any coding project, each available both
as a **subagent** (Claude delegates to it) and as a **slash command** you can run.

| Command | Personality | What it does |
|---|---|---|
| `/archi` | **ARCHI** | Architecture guardrail — reviews changes, tracks drift, writes/updates `docs/architecture.md`. Never edits your code. |
| `/standly` | **STANDLY** | Standards authority — checks changes against code standards + OWASP security. Never edits your code. |
| `/dev` | **DEV** | Delivery engineer — the one that actually writes code + tests, inside the standards & architecture. |
| `/product` | **PRODUCT** | Product manager — tracks features, risk-assesses them, plans sprints with pointed tasks. |
| `/review-business-plan` | **BUSINESS-REVIEWER** | Stress-tests a business plan / pitch: challenge, steelman, validate claims vs code, adjudicate. |

## Install (per project)

Copy the `.claude/` folder from this pack into the **root of your project**:

```bash
# from inside your project folder
cp -R /path/to/personalities-pack/.claude .
```

If your project already has a `.claude/` folder, copy the contents of `.claude/agents/`
and `.claude/skills/` into your existing ones instead of overwriting.

Then open the project in Claude Code and type `/` — you'll see `/archi`, `/dev`,
`/product`, `/standly`, `/review-business-plan` in the list. You can also just ask Claude
things like *"get ARCHI to review my changes"* and it will use the subagent.

## How they work together

`PRODUCT` decides **what** to build and plans it → `DEV` **builds** it → `ARCHI` guards the
**architecture** and `STANDLY` guards the **standards & security**. `DEV` is the only one
that edits code; the others review and govern. `BUSINESS-REVIEWER` is separate — point it
at a business/strategy document when you want it pressure-tested.

## Customising

These are deliberately generic. To make them yours:
- Run `/archi regen` once in a project to have ARCHI write a `docs/architecture.md` from
  your actual code — after that, `/archi` reviews against it.
- Edit any `.claude/agents/*.md` file to change a personality's rules or tone. The text in
  each file *is* the personality — plain English, edit freely.
