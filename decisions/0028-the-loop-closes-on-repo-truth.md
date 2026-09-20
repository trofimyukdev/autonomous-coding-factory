# ADR 0028 - The loop closes on repo-truth: the INTEGRATING -> BUILDING edge, and the seats carried across ticks

Date: 2026-09-19. Context: a carrier session (carrier #64) by foreman decision,
not a block. `main` stood at `2efd6dd` when the package began -
`git rev-parse HEAD origin/main | cut -c1-7 | paste -sd' '` printed
`2efd6dd 2efd6dd` on 2026-09-19 at 23:04 - and `git status --short | wc -l`
printed 2 the same minute, the two operator handoffs in a private archive
that is not published.
Nothing under `src/`, `test/`, `scripts/`, `.githooks/`, `factory/checks.yaml`,
`CLAUDE.md`, `PRINCIPLES.md` or `DESIGN.md` was touched by this package.

**This document records one operator word and what it decides. The rows that
carry it out are named in section 1 and are the homes of their own content.**

## 0. The operator's words, and the question they answer

Two sentences, on 2026-09-19 at about 22:05, relayed
operator -> the foreman seat -> this carrier. Quoted verbatim on
ADR 0005's precedent, Russian as typed:

```text
1 — да, 2 — B
```

```text
И дальше, ночью, продолжай по ночному протоколу
```

"1 - yes, 2 - B" and "And further, at night, carry on under the night
protocol." The second sentence is an instruction to the seat about how it runs
the night, and decides nothing in this repository; it is quoted because it came
in the same exchange.

The first answers ONE question the seat put to the operator at
about 20:30 and again at about 21:50 - how the loop closes on `repo-truth` - in
two parts. In the seat's words, translated:

**(1) The `INTEGRATING -> BUILDING` edge.** A gate refusal buys no fix cycle
today at any quality attempt, because the state machine declares no such edge.
The question with its arguments for and against is ADR 0020 section 2 (a), its
home; the live instance is `FIX_CYCLE_BLOCKED` at seq 220 of `repo-truth`'s
journal, and ADR 0027 section 10 listed it as not decided. The seat's
recommendation: declare the edge, and protect the reaper's path in the same row.

**(2) The wall against three seats.** On RT-02 the builder, the reviewer and the
goal evaluator do not fit in the default wall of 840 seconds - the timelines of
both gated ticks are M0-195's finding (10), their one home. Three ways out:
(A) raise the wall's default, which runs against `DESIGN.md` section 7 and
against M0-195's finding (9), which needs the wall LOWER; (B) carry the seats
after the builder across ticks, the way M0-217 carries a fix cycle; (C) bound
the builder harder. The seat's recommendation: B.

The operator's "1 - yes" and "2 - B" accept both recommendations as put.

## 1. The decision

### (1) The edge is declared, and its price is paid in the same row

ADR 0020 section 2 (a) is CLOSED by the word above. That section called the
edge "a change to ratified text, which is an operator act"; the act is the word
of 22:05, and this document is its ledger entry.

The price ADR 0020 section 2 (a) names - the reaper reads the same table, so
the edge changes what a recovery from INTEGRATING may do - is paid in the SAME
row that declares the edge, and not later; what that price is, read against
the code rather than inherited from M2-12, is that row's outcome. The row
is **M0-224**; what it must and must not do, the ratified text included, is its
own `outcome` and `not_done_if`.

What the edge buys is `DESIGN.md` section 9's "A first failure buys one fix
cycle (fresh builder plus FailurePacket, same branch)" on the gate's route,
which today it does not. It does not change the outcome of RT-02's stop: that
row had spent its quality attempts (2 of a ceiling of 2), and the reason that
would stop it with the edge is M0-224's datum.

### (2) Way B: the seats after the builder are carried across ticks

When a pass cannot hold a seat after the builder - the reviewer of stage 4 or
the goal evaluator of condition 6 - on the reading of the wall that seat runs
on, the seat is deferred and resumed by a later pass over the same candidate,
in the form M0-217 gave the fix cycle. **M0-225** is the row; the mechanism, its record and its ceiling are the
block's, within that row's `not_done_if`.

The ground is `DESIGN.md` section 7, verbatim: "One tick is one bounded pass:
pick up what fell, start what is ready, walk finished candidates through
integration, update reports, exit", and "Frequent bounded ticks (15 minutes)
beat one long pass". A seat carried to the next pass is what fell, picked up.

**The wall's default does not rise, and section 7 is not touched.** Way A is
refused; M0-195's finding (9) stands, and the wall it needs lowered is still
lowered by that row. Way C is refused: it buys the later seats their time by
degrading the seat that writes the code.

M0-220's share, `goal_reserve_seconds`, stays; how a deferral meets it is
M0-225's to state.

## 2. What this ADR does NOT decide

- **The mechanism of either row.** The edge's reaper guard and the carried
  seat's record, event names and ceiling are the blocks' (M0-224, M0-225).
- **The wall's numbers.** Both numbers of finding (9)'s relation, and whether
  the builder and the walk before stage 4 fit the wall they leave, are
  M0-195's.
- **When the next tick runs, or whose hand starts it.** Unchanged from ADR 0027
  section 10.
- **Which ten tasks step (1) of the operator's programme measures** (ADR 0027
  section 10). This decision closes the loop that step needs; it does not pick
  the tasks.
- **Whether RT-02's candidate `a20bdb49` is accepted.** No word touched it.

## 3. What is filed elsewhere

The rows this package minted or raised are named in its commit messages and are
not listed here beyond the two above, for ADR 0020 section 3's reason: a
decision document that carries a backlog acquires two homes for every row in it.
