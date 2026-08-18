# ACRG Agentic AI: Practical Guidelines

**Version 0.1 (draft) — August 2026**
**Companion to: *ACRG Principles for the Use of Agentic AI***

## The three-layer structure

Our approach to AI lives in three layers. Each layer justifies the one above it.

| Layer              | What it is                                     | Where it lives            | How often it changes            |
| ------------------ | ---------------------------------------------- | ------------------------- | ------------------------------- |
| **Principles**     | Why and what we commit to                      | Public document           | Rarely (termly review)          |
| **Practice guide** | Human norms and procedures                     | This document (internal)  | Termly                          |
| **Machine layer**  | Agent instructions, hooks, CI, sandbox configs | Group template repository | Continuously (owned, versioned) |

A guiding rule for implementation: **prefer enforcement in tooling; use agent instructions for behaviours tooling can't check; use human norms for everything machines can't decide.** Agent instructions are requests, not guarantees: a principle is only as strong as the machinery around the agent, not the prompt inside it.

---

## Layer 2: Human norms and procedures

**Group meetings.**
- Presenters state the assistance level of the work in one sentence, using the shared taxonomy below. Destigmatisation is part of the procedure.
- Meetings emphasise defending decisions over showing product: *why this prior, why this parameterisation, why this baseline*, answered from your own understanding. Expect to be asked.
- Praise attaches to judgement (questions chosen, errors caught, negative results correctly killed), not to volume.

**Provenance taxonomy** (adapted from open-source practice). State which applies:
- **Agent-implemented** — the tool produced it independently from your specification; you verified it.
- **Agent-assisted** — the tool implemented under your direction and iteration.
- **Agent-advised** — the tool advised; you implemented.

Use the same labels in commit messages for substantial contributions.

**Supervision.**
- Supervision meetings periodically include walking line-by-line through code or text the student did not write by hand. This is developmental, not disciplinary.
- Supervisors and early-career members agree explicitly which skills the member is deliberately practising unassisted this term (e.g. derivation, debugging without the agent, zero-draft writing), on the evidence that AI assistance can impair learning even while boosting output.

**Deliberately AI-free spaces.**
- Journal club: the paper is read unassisted. Summaries and critiques are your own before discussion.
- Whiteboard/design sessions precede prompting, so independent priors form before they correlate.

**Writing.**
- The floor for authorship is the defensibility standard (Principle 4): every claim asserted and defensible without the tool; you can reconstruct the argument; you accept responsibility as if you had typed every word; and you follow the venue's disclosure requirements.
- A recommended (optional) practice: **the zero draft is yours** — argument skeleton, claims, and structure written unassisted, however rough; AI assists downstream. Writing is where much of our thinking happens; don't delegate the thinking.
- Stricter personal standards are legitimate and protected. So is heavy assisted drafting that meets the floor.
- The one-line test, for prose and pipelines alike: *if you couldn't defend it at group meeting without the tool, it isn't yours yet: keep working. If you can, it's yours, whatever helped you get there.*

**Peer review and confidential material.** Manuscripts, proposals, and examination materials we receive in confidence are not uploaded to AI tools where the reviewing body prohibits it (most now do). When in doubt, ask before uploading.

**Scepticism, including of ourselves.** Experts systematically overestimate their own AI productivity gains. We cultivate habits of self-scrutiny: notice when verification catches an error you would have shipped, when a task took longer with the tool than without, when fluency outran understanding. The default stance is suspicion of our own impressions, including favourable ones.

---

## Layer 3: The machine-readable layer

Maintained in the group template repository, which every new project forks. Contents:

**Shared agent instructions (`AGENTS.md` or equivalent), including:**
- A pointer to the principles: *"This project follows the ACRG AI principles [link]: verify before asserting; state provenance; flag uncertainty."*
- *Verification-first:* "After implementing any numerical routine, propose a test against an analytical solution or reference implementation before declaring it done. When modifying an analysis pipeline, run the regression suite and report diffs against the benchmark case; never assert correctness from inspection alone."
- *Epistemic behaviour:* "When asked for a judgement call (prior choice, parameterisation, interpretation of a residual), present options and trade-offs rather than a single confident answer. Flag any factual claim that would need a literature check."
- *Scope discipline:* "Do not silently expand scope. If a fix suggests a refactor, propose it and stop."
- *Provenance:* "Substantial commits state the assistance level: agent-implemented / agent-assisted / agent-advised."

**Enforcement infrastructure (does not depend on the agent obeying):**
- Template repos ship with a regression-benchmark structure in place, so the verification norm is inherited at `git init`.
- Pre-commit hooks (linting, secrets scanning) and CI that runs the reference tests, regardless of who or what wrote the code.
- Sandboxed agent execution with minimal permissions: the technical encoding of "accountability stays human". The agent cannot touch what you have not granted.

**Maintenance.** The machine layer has a named owner (a role that rotates within the group), a lightweight change process (PRs to the template repo), and is reviewed alongside the termly principles review. If the layer only works when one person maintains it, it isn't group infrastructure yet.

---

## What is deliberately not here

Some principles cannot be encoded and we do not pretend otherwise: protection of conscience, the culture of what we value, and honesty about ethical compromise live between people, not in config files. This document supports them procedurally; it cannot carry them.

---

*Authors: Matt Rigby and members of the ACRG, with Claude (Anthropic) and Kimi (Moonshot AI). Assistance level, per the taxonomy above: agent-assisted.*
