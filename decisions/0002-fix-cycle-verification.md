# ADR 0002 — Fix cycles: when a re-verification is mandatory

Date: 2026-08-17. Context: M0-01 shipped in two commits — the block itself
(`48adfa3`) and a fix cycle answering the verifier (`98acd9b`). The fix cycle was
accepted without a second independent verifier pass, and nothing recorded whether
that was a rule or a one-off. This ADR makes it a rule, because the alternative is
either a re-verification tax on every typo fix or a silent hole through which
logic reaches `main` unverified.

## Decision

A fix cycle is the work done on a block branch **after** the adversarial verifier
has reported. It is classified before it is written, and its class decides the
gate:

**Logic fix — mandatory second independent verifier pass.** Any change that alters
what the code decides, computes, stores, or refuses: production sources, schemas
and generated artefacts, migrations, gate/DAG conditions, exit codes, default
values, CLI surface. The re-verification is a **fresh-context subagent** (no memory
of the first pass) and it verifies the branch as it now stands — not a diff review
of the fix. It may be scoped to the touched area plus everything the first pass
found, but it must be free to reject the whole branch.

**Test-only fix — accepted on mutation evidence, no second pass.** Changes confined
to `test/**` that only strengthen what is already asserted: a new test, a sharper
assertion, a fixture that closes a hole the verifier found. Acceptance requires,
in the commit message, for **each** killed mutant: the mutation in one line, the
exact command, and the before/after counts. "Tests still pass" is not evidence —
the claim is that the test now *fails* against a mutant it used to accept, and
only a failing run proves it (discipline 1: a number without a reproducible
command is not a fact).

**Mixed fix — logic class.** A commit that touches both is a logic fix. Splitting a
mixed fix into two commits does not change this; the class follows the branch, not
the commit boundary.

Doc/comment-only changes carry no gate of their own and ride with whatever else the
fix cycle contains.

## Why the asymmetry

The two classes have different failure modes. A logic fix is written under the
verifier's pressure, usually late in a block, against code the author has stopped
reading adversarially — the exact conditions the first verify pass exists for, so
it earns another one. A test-only fix cannot make the product wrong: its worst case
is a test that does not pin what it claims, and that failure mode is *directly
measurable* by mutating the source and watching the test fail. Where evidence is
mechanical and complete, a second opinion adds cost and no information (discipline
13: effort follows the measured failure distribution).

## Precedent, stated accurately

`98acd9b` is the precedent for the test-only lane: three surviving mutants were
killed and the commit message carries each mutation, the command
(`npx vitest run test/unit/taskspec.test.ts`) and the counts (`1 failed (was 0)`).
That is the evidence standard this ADR now requires by name.

The same commit also changed logic — `nodeSchema` began emitting `pattern: "\\S"`
alongside a positive `minLength` (`src/controller/taskspec.ts`), so a third-party
validator would stop accepting values the millwright validator rejects. Under this
ADR that change alone puts the fix cycle in the logic class and would have required
a second pass. Recording this is the point: the precedent is being narrowed, not
ratified whole.

## Consequences

- The verifier's report ends with an explicit classification line for the fix
  cycle it triggers, so the class is fixed before the fix is written and cannot be
  argued down afterwards by the party doing the writing.
- A block may run several fix cycles; each is classified on its own.
- Cost: at most one extra verify pass per block that needed a logic fix. Priced in
  the TaskSpec `budget.verify_usd`, and cheap next to the measured alternative —
  four fix cycles ran during bootstrap (ADR 0001 decision 6) with no gate on any
  of them.
- This is a bootstrap-phase rule for supervised operator sessions. When the
  factory runs blocks itself (M2), it moves out of prose and into the controller:
  the fix-cycle class becomes a field on the attempt and the re-verify becomes a
  DAG edge, per discipline 4 — a recurring lesson becomes a gate, never another
  paragraph.
