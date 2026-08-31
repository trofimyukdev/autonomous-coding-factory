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
