# Agent instructions

## Scope

This repository contains the TMC Software Architecture Assignment M1 study
materials and design deliverables. Work on M1 only unless the user explicitly
asks for another scope.

## Source of truth

Read the documents in this order:

1. [`docs/overview/summary.md`](docs/overview/summary.md) — official
   requirements, traceability IDs, boundaries, and open questions.
2. [`docs/guides/rules.md`](docs/guides/rules.md) — certainty labels,
   scope rules, and consistency constraints.
3. [`docs/guides/skill.md`](docs/guides/skill.md) — workflow for analysis,
   architecture design, writing, and review.
4. [`docs/reference/knowledge.md`](docs/reference/knowledge.md) — concepts,
   trade-offs, and the local source index.

Use [`docs/guides/assignment-explained.md`](docs/guides/assignment-explained.md)
only as an explanatory aid. It contains illustrative proposals, not additional
requirements.

## Working rules

- Preserve the labels **GỐC**, **SUY RA**, **ĐỀ XUẤT**, and **CẦN XÁC NHẬN**.
- Keep traceability from requirement to design decision, view, and evaluation.
- Do not invent deadlines, benchmarks, approvals, infrastructure, or team facts.
- Keep the stated load, two-second kiosk target, normal-operation durability
  condition, and HR reconciliation deadline unchanged.
- Put a new M1 report at `docs/deliverables/report-m1.md` when no output path
  is specified.
- Update links when moving documentation and check for stale paths before
  finishing.

The automatic skill entrypoint is
`.agents/skills/tmc-m1/SKILL.md`.

