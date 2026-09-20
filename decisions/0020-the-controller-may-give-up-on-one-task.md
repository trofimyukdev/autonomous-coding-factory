# ADR 0020 - the controller may give up on one task, and the three questions the M2 chain could not answer

Date: 2026-08-29. Context: a carrier session by foreman decision - not a block.
`main` stood at `f249562` throughout, the tree was clean, and nothing under
`src/`, `test/`, `.githooks/` or `DESIGN.md` was touched by this package.

M0-116 landed a change to DESIGN.md section 6 that it was forbidden to file a
ledger entry for: `docs/decisions/**` is in that spec's `forbidden_paths`, so the
block carried the entry out in its report as a packet and this is where the
packet stops being open. The section's own text is where the decision lives; this
ADR records that it was taken, on whose authority, and what was deliberately left
undecided beside it (discipline 12).

## 0. The sanction

The operator placed strategic decisions with the foreman on 2026-08-25. That
line is quoted in full in ADR 0018 section 0 and again in ADR 0019 section 0, and
is pointed at rather than quoted a third time.

What is new here is the reporting, and it is the foreman's account rather than
this session's measurement: the foreman reported this decision to the operator on
2026-08-29 at 13:40 and again at 15:04, and no veto stood at 17:31, when the
package that produced this document was issued. Both the report and the silence
reached this session as a relay from the foreman and not from the operator's own
terminal, which is stated rather than smoothed over - the same disclosure ADR
0018 section 0 makes about its own sanction. **[operator-confirmable]**: the
decision in section 1 stands unless the operator vetoes it.

## 1. The decision - the CONTROLLER walks the giving-up edge, and nothing else changed

Read in this checkout on 2026-08-29: `grep -n 'BLOCKED:\|DEAD_LETTER:' src/store/state-machine.ts`
prints `BLOCKED: ["READY", "DEAD_LETTER", "CANCELLED"]` and
`DEAD_LETTER: ["READY", "CANCELLED"]`. Both the state and the edge predate
M0-116. What the block changed is WHO walks the edge: until it, giving up was the
operator's act alone, and after it the controller walks `BLOCKED -> DEAD_LETTER`
when a landing would charge an infrastructure retry the task's own
`budget.infra_retries` does not grant.

The section states it in its own words and this document does not restate them:
the bullet added to "Key edges" by `ef41763` (merged as `3ade5ac` on 2026-08-29)
carries `**[operator-confirmable]**` and its date in the ratified text itself.
The digest was re-ratified in the same commit - the entry for section 6 in
`test/unit/design-ratification.test.ts` records the re-reading of the blueprint
counterpart and what was concluded from it, which is the guard's actual
requirement.

**What this decision is NOT.** No state was added, no edge was added, and the
fenced state list both DESIGN.md and the blueprint carry is untouched. Reopening
stays the operator's: `DEAD_LETTER -> READY` is walked by nothing else in this
tree, which is what keeps a given-up task a park rather than a drop. And the
route is walked in one transaction rather than widened into a third edge - the
landing goes to BLOCKED instead of where the caller asked, and the same
transaction carries it on (`GIVING_UP_ROUTE`, src/store/infra-ceiling.ts).

## 2. What this ADR does NOT decide

Three questions are open, each with an argument behind it and none of them a
block's to answer. They are written here so that the next session finds them with
their arguments rather than re-deriving them.

### (a) Should `INTEGRATING -> BUILDING` be a declared edge?

M2-12 delivered the fix cycle and left this one refused by construction. The gate
is asked inside `integrate()`, so a gate refusal leaves the row in INTEGRATING,
and `decideFixCycle` (src/controller/fix-cycle.ts) asks `canTransition` rather
than assuming: `FIX_CYCLE_TARGET` is `BUILDING`, `INTEGRATING` does not list it
(src/store/state-machine.ts), so the decision comes back `no_edge` and the row's
first refusal is its last. That is STRICTER than DESIGN.md section 9, which buys
a first failure one fix cycle. With the edge, the cycle would work from that
route with no change to the deciding code at all - the guard already consults the
table.

Against it: M2-12's own outcome records that the first attempt added exactly this
edge and that the reaper reads the same table, so an INTEGRATING row whose
evidence was not intact moved from `report_only` to a new quality attempt into
BUILDING, past any ceiling and into a state `PICKABLE_STATES` (src/controller/
dispatch.ts) does not hold. The edge is not free, and its price is paid in a
module that did not ask for it.

The question is therefore not "is the fix cycle worth reaching from INTEGRATING"
but "is the state machine the right place to say so, given that a second reader
of the table changes behaviour with it". It is a change to ratified text, which
is an operator act.

**Closed 2026-09-19** by the operator's word: the edge is declared. The word, the
decision and the row that carries it are ADR 0028 section 1 (1).

### (b) Should the factory ever revert its own merge?

M2-23 delivered the post-merge check and parks a regression rather than
reverting it. The FOR and the AGAINST are written once, in the docstring of
src/controller/post-merge.ts, with the argument attached, and are not restated
here. What that docstring cannot supply is the judgement it names: whether an
operator would rather meet a red base branch with an incident attached or a green
one with two extra commits and a task to redo, and under which task classes.
DESIGN.md section 10 offers the task-class revert policy as one branch and this
factory has no task classes yet.

### (c) "A fast smoke" against the heaviest rung - and the price has moved

DESIGN.md section 10 calls the post-merge check "a fast smoke". M2-23 selected
`full_suite`, the ladder's most expensive rung, and said plainly in the same
docstring that the two sentences cannot both be obeyed: an exclusion that is
only safe because something later runs the heavy rung is not safe if nothing
does.

That trade was taken against a measured price, and the price has since moved.
The docstring records `{ time npm run test:kill ; }` printing `real 0m16.477s` on
2026-08-29; re-run in this checkout at `f249562` later the same day,
`{ time npm run test:kill ; }` printed `real 1m44.944s`. The rung is unchanged -
`full_suite` is one check whose command is `npm run test:kill`
(factory/checks.yaml) - and so is the runner, which spawns five separate vitest
processes over `test/faultinjection/` and has not been edited since M0-05. What
moved is what it runs: on 2026-08-29 `git log --format='%h %ad' --date=short --diff-filter=A -- test/faultinjection/controller-kill.test.ts`
printed `0f44ed6 2026-08-29`, the controller kill suite M2-13 added hours before
this reading, and one of the five runs now reports `Duration 19.92s` where the
store suite alone used to be the whole of it.

Neither figure is wrong and neither block was careless: M2-23 measured its own
tree and M2-13 landed afterwards. What the pair shows is that the trade is not a
constant. The question for the operator is whether a post-merge smoke that grows
with every fault-injection test this factory writes is the right shape at all, or
whether "fast" has to become a bound the selection is held to rather than a word
the design uses. This session takes no position beyond re-running the number,
which is what discipline 1 asks of an inherited one.

## 3. What is filed elsewhere

The findings this package collected from M0-116, M2-12, M2-13 and M2-23 are in
`factory/tasks/` and are not listed here: a decision document that carries a
backlog acquires two homes for every row in it. The rows this package minted or
appended to are named in its commit messages.

## 4. Addendum, 2026-09-08 - the price has moved a third time, and four fifths of it answers a different question

Added by a carrier session (carrier #46) by foreman decision, not a block. `main`
stood at `3c6c5c8` when this section was written and the tree was clean apart
from two untracked operator handoff files in a private archive that is not published. Nothing under
`src/`, `test/`, `scripts/`, `.githooks/`, `factory/checks.yaml` or `DESIGN.md`
was touched. Section 2 (c) escalated a question to the operator and took no
position; this section answers it with a fact that was not available then, and
its recommendation is **[operator-confirmable]**.

### (i) The third reading

Section 2 (c) records two readings of `{ time npm run test:kill ; }`, both on
2026-08-29: `real 0m16.477s` in M2-23's docstring, and `real 1m44.944s` at
`f249562` after M2-13 landed the controller kill suite. Re-run in this checkout
at `bbae1f7` on 2026-09-08 at 09:54, after M3-11 landed three more processes:

```text
{ time npm run test:kill ; }
=== 5/5 kill suite runs passed
real    5m25.108s
```

That is a factor of 19.7 in ten days, and it reproduces the foreman's own
reading of `real 5m24.985s` taken at 09:40 the same day on the same commit. The
rung is still one check whose command is `npm run test:kill`
(`factory/checks.yaml`), and the runner has still not been edited since M0-05.
What moved is again what it runs: `ls test/faultinjection/*.test.ts | wc -l`
printed `6` on 2026-09-08, where M2-23 measured a tree that held the store suite
alone.

### (ii) The fact section 2 (c) did not have: the smoke pays five times for one answer

`npm run test:kill` does not run the suite. It runs `npm run build` and then the
suite **five times, in five separate processes** - `const RUNS = 5;` in
`test/faultinjection/run-kill-suite.mjs`, and the same file's docstring says
exactly what the repetition is for: "The five runs are this suite's flakiness
detector - 'passes and fails on the same commit' is a forbidden outcome for this
task".

The five `Duration` lines of the run above, from the same log:

```text
   Duration  63.73s ... 63.91s ... 63.75s ... 63.87s ... 64.05s
```

So one pass of the fault-injection suite costs about 64 seconds and the other
four minutes twenty are a flakiness ladder. **A post-merge smoke does not ask
whether the suite is flaky. It asks whether the merged SHA is broken**, and it
asks it once, after the work is already on the base branch.

That reframes section 2 (c)'s question. It read as a choice between the heavy
rung and a cheaper subset of it, and the honest answer to that choice was
uncomfortable, because M2-23's argument against a subset is correct and has only
got stronger: an exclusion that is safe only because something later runs the
heavy rung is not safe if nothing does, and the integration ladder has been
excluding more of it with every fault-injection test this factory writes. The
choice on the table now is not between rungs. It is between running one rung
once and running it five times.

### (iii) The direction of the error also favours one run, which is the part that is not about money

Five runs reduce a false GREEN - a flaky test that happens to pass - and
multiply a false RED, because five independent chances to fail is five chances
to open an incident on work that is already merged. For a CANDIDATE's ladder that
trade is right, and it is where the ladder belongs: a new fault-injection test
that passes four times out of five must not land. For a post-merge smoke the
trade inverts. This module's own docstring says why in its argument against
reverting: "a smoke whose rung is flaky reverts good work". Nothing reverts today
(section 2 (b)), so what a false RED buys is an incident and an operator's
attention at whatever hour the tick ran, which is precisely the three-in-the-
morning false alert `DESIGN.md` section 12 is written to avoid.

So one run is not the cheap answer and the five-run ladder the careful one. For
this check, one run is also the more accurate one.

### (iv) The recommendation, and it is not this carrier's to execute

**The SELECTION stays `full_suite`.** M2-23's trade is re-affirmed, not reversed,
and section 2 (c)'s worry that "fast" has to become a bound rather than a word
is answered by removing four fifths of the cost instead of by dropping tests.

**What is questioned is the command behind that rung in a post-merge context,
and nothing else.** The candidate's `full_suite` rung keeps the five runs; the
smoke runs the suite once. On the readings above that is about 64 seconds a
merge instead of five and a half minutes, with no test dropped and no exclusion
re-opened.

This carrier does not execute it. It changes what a gate runs, which lives in
`src/**` and `factory/checks.yaml`, and both are outside a carrier's paths - so
this is a recommendation and a row candidate, and the row is owed a decision
about WHERE the difference is expressed (a smoke-specific run count, a second
check entry, or an environment the runner reads), which is a design question and
not a carrier's.

### (v) Why this matters more at M4 than it does today

Today the smoke costs five and a half minutes once per merged task, on a factory
run by hand, and nobody is waiting on it. `DESIGN.md` section 12 puts the
unattended factory on `OnCalendar=*:0/15` inside a unit bounded by
`TimeoutStartSec` of 15 minutes. **A post-merge smoke of 5m25 is 36 per cent of
that unit's entire wall clock**, spent after the work is done, and it grows with
every fault-injection test the M4 row for that suite adds. ADR 0024 section 6
puts that suite's completion at slot 91 of the M4 chain draft, which means the
number in this section is going to move again before the first crontab entry -
and by then it is a rung of the soak ladder rather than a line in a report.
