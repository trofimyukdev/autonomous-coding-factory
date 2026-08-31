# ADR 0018 - the second drift: a queue that files findings and plans nothing, and the gates that end it

Date: 2026-08-25. Context: a carrier session by foreman decision - not a block.
`main` stood at `5baa63c` throughout, the tree was clean, and nothing under
`src/` or `test/` was touched by this package.

The queue drifted a second time, in a shape ADR 0004 named once and could not
prevent, because the rule it wrote against that shape has no executor. This ADR
carries the measurement, the diagnosis, the sanction, and the decisions the
sanction authorises. The M2 chain and the three gates it mints live in
`factory/tasks/`; this document is the reason they exist and does not restate
them (discipline 12).

## 0. The sanction

The operator answered the foreman's drift assessment on 2026-08-25 at about
11:05, in Russian, and the foreman relayed it to this session
verbatim: 'Одобряю твои находки и приоритеты, закрепи в гейтах и правилах то что
считаешь нужным. Продолжаем?' - "I approve your findings and your priorities;
fix in gates and rules whatever you think needs fixing. Shall we continue?"

The Russian is quoted rather than translated away because the sanction is the
authority this whole package stands on and a translation is a paraphrase; ADR
0006 sets the precedent for a verbatim Russian line inside this English
repository. **[operator-confirmable]**: every decision below stands unless the
operator vetoes it.

## 1. What was measured

**The inflow of specs, by class and by the day the file first appeared.** A spec
whose `discovered_from` is `null` or the reserved literal `bootstrap` is roadmap
work - somebody decided the factory should have it. Any other value is a
finding - the queue noticing itself. Taken on 2026-08-25 in this checkout at
`5baa63c`:

```text
for f in factory/tasks/*.yaml; do
  d=$(git log --diff-filter=A --follow --format=%ad --date=short -- "$f" | tail -1)
  df=$(grep -E '^discovered_from:' "$f" | head -1 | sed 's/^discovered_from: *//')
  case "${df:-null}" in null|bootstrap) k=ROADMAP;; *) k=FINDING;; esac
  echo "$d $k"
done | sort | uniq -c

      9 2026-08-17 FINDING          7 2026-08-17 ROADMAP
     15 2026-08-18 FINDING          8 2026-08-18 ROADMAP
      4 2026-08-19 FINDING          2 2026-08-19 ROADMAP
     18 2026-08-20 FINDING          1 2026-08-20 ROADMAP
     15 2026-08-21 FINDING          1 2026-08-21 ROADMAP
      3 2026-08-22 FINDING          1 2026-08-22 ROADMAP
     11 2026-08-23 FINDING
     10 2026-08-24 FINDING
     10 2026-08-25 FINDING
```

(the two columns are the same output, re-laid so the shape is readable; the
command prints one line per pair). The totals are visible in one line each, on
the same day and in the same checkout: `grep -L -E '^discovered_from: *(null|bootstrap)' factory/tasks/*.yaml | wc -l`
printed 95 findings and `grep -l -E '^discovered_from: *(null|bootstrap)' factory/tasks/*.yaml | wc -l`
printed 20 roadmap entries, over a directory in which every spec states the
field - `grep -L -E '^discovered_from:' factory/tasks/*.yaml | wc -l` printed 0
on 2026-08-25, so nothing is classified by a default. Three days have passed since the last roadmap entry was
filed and the inflow in each of them is findings alone. That is the drift, and
it is a rate rather than a state: findings arrive as a by-product of the block
ritual, so their inflow is automatic, while roadmap work arrives only when
somebody sits down and plans - and nobody owns that.

**The band the pick rule actually reads.** On 2026-08-25, `node dist/cli.js
queue | awk '!/^#/ && ($1=="QUEUED"||$1=="PAUSED") && $7=="open"' | wc -l`
printed 74, and classifying each of those rows by its spec's `discovered_from`
the same way printed 68 findings against 6 roadmap entries. Their milestones,
from the same run's third column, were M0 9, M1 33, M2 23, M3 2 and M4 7.

**There is no spec file whose id names M2 or anything above it.** On 2026-08-25
`ls factory/tasks/ | grep -cE '^M[2-5]-'` printed 0, and the milestone the
factory is supposed to be building - `millwright tick` - is not built: on the
same day `node dist/cli.js help | tail -5` printed "Commands specified but not
built yet:" followed by `tick`.

**ADR 0004 diagnosed this once and its remedy has no executor.** ADR 0004
section 2 wrote five rules against exactly this shape on 2026-08-18. Rule 4 -
every block report answers "what did this do for M2" - is prose and nothing
else: on 2026-08-25 `grep -rn -i -E 'what did this do|metric_effect|did this do
for M2' src/ scripts/ .githooks/` printed nothing and exited 1, and the
`BLOCK_RECORDED` payload the ritual actually writes carries only `spec_id`,
`integration_sha`, `base_sha`, `quality_attempts`,
`quality_attempts_provenance` and `quality_attempts_source` (the object literal
in `recordLanded`, `src/controller/bookkeeping.ts`, section "The provenance is a
fact about the count"). Rule 3 - hygiene never outranks an open spec of its own
milestone or the next one - is vacuous whenever the next milestone has no spec
at all, which has been the case since M1's chain was consumed.

**The pick rule executed the drift faithfully.** Every local argument for a
priority was sound; the input to those arguments was unconstrained. That is the
whole finding, and it is why the remedy below is three executables and not a
sixth rule.

## 2. Two claims of the scouting pass that the code refuted

Both are recorded because the package this session was handed asserted them and
a spec written on either would have been wrong (discipline 1, discipline 2).

**"Every open row carries `discovered_from`; rows without it are 0."** It is
6, not 0, measured by the classification command of section 1 restricted to the
open band on 2026-08-25. The rows are M0-34 (priority 68, milestone M2), M0-07
(64, M2), M0-56 (41, M4), M0-33 (34, M0), M0-76 (28, M1) and M0-72 (25, M3).

**Therefore the gate the package specified would not have caught the drift it
was written for.** A check that fails when the band holds no roadmap row of the
current or the next milestone would have PASSED all week: M0-34 and M0-07 are
roadmap rows of M2 by the marker, and both were open throughout. The predicate
that does fire is an ORDERING predicate, not an existence one - the highest
open roadmap row stood at priority 68 while the top of the band stood at 74, so
plan work was outranked by findings, which is the drift stated exactly. G1 in
section 3 (b) is specified on the ordering predicate for this reason, and this
paragraph is the refutation that moved it.

**A weakness of the marker, filed rather than fixed here.** `discovered_from`
defaults to `null` (`FIELDS.discovered_from`, `src/controller/taskspec.ts`), so
a finding whose author simply omits the field is indistinguishable from planned
work. M0-34 is that shape: its own `outcome` describes an incident of
2026-08-19 and it carries no provenance. This package does NOT re-mark it -
choosing a provenance id for somebody else's finding is a claim this session
cannot make - and G3 is specified to name the hole rather than to pretend the
marker is sound.

## 3. Decisions

**(a) ADR 0004's two unexecuted rules get executors.** Rule 3 gets G3, an
intake refusal in `readQueueDirectory`. Rule 4 gets G2, a value recorded at
`record-landed` time and a counter that reads it back. Both are specs in
`factory/tasks/`; neither is restated here.

**(b) A new standing rule - milestone exit.** The roadmap specs of milestone
N+1 exist in `factory/tasks/`, and outrank the findings, BEFORE the band below
milestone N's chain is consumed. Its executor is G1, a doctor check named
`queue.roadmap`, and its predicate is the ordering one section 2 derived: the
check fails when the highest-priority open roadmap row does not outrank the
highest-priority open finding, and fails separately when no open roadmap row
exists for the milestone of the band's top row or for the next milestone in
`MILESTONES`. The second half is the existence rule the package asked for; the
first half is the one that would have fired.

**(c) The roadmap marker is the ABSENCE of a provenance**, that is
`discovered_from: null` or `bootstrap`, and NOT the id prefix - ADR 0004 section
2 rule 2 keeps ids as filing counters and this ADR does not disturb it. The M2
chain nevertheless carries `M2-xx` ids, exactly as the M1 chain carried `M1-xx`:
a reader scanning `ls factory/tasks/` should be able to see that a milestone was
planned, and that convenience costs nothing as long as the marker, and not the
prefix, is what the gates read.

**(d) The band's shape from this package onward.** The M2 chain occupies the
free band from priority 99 downward in dependency order; the three drift gates
sit directly below the chain; findings sit below the gates unless they declare
G3's exception. Every priority from 75 to 120 was free of open rows before
this package - measured on 2026-08-25 by comparing `seq 1 120` against the
second column of `node dist/cli.js queue | awk '!/^#/ &&
($1=="QUEUED"||$1=="PAUSED") && $7=="open" {print $2}'`, whose output runs from
0 to 74 with a single gap at priority 13 and nothing above - so nothing below is
re-striped and no open row changes its slot except the four this package raises
by name.

**(e) The first tick is SYNCHRONOUS, and the deviation is stated rather than
hidden.** DESIGN.md section 7 step 6 says "builder in the background, in its own
process group and cgroup". The M2 row of section 17 says "full loop, one task",
and the soak ladder in section 18 makes rung 2 "supervised auto-merge, one task
per tick". A first tick that awaits one builder inside `tick_wall_seconds`
delivers that row; backgrounding and the heartbeat that goes with it belong to
M3, whose row is "economics and parallelism". So the M2 chain builds the
synchronous form and says so in its own specs. **[operator-confirmable]**, and
NOT an edit to DESIGN.md: section 7 keeps its text, and the milestone that
satisfies step 6 as written is M3.

**(f) FACTORY_ADMIN, and why no M2 spec declares it.** `FACTORY_SOURCE_PATHS`
is `["src"]` and `factoryCorePaths()` adds it to `GATE_PATHS` for any spec whose
repo is millwright's own (`src/verify/stage1.ts`), so every diff in this chain is
factory-core. Stage 1's `factoryAdminClass` refuses such a diff unless the spec
declares the class AND a promotion from a different party exists, and nothing
produces a promotion - that producer is open spec M0-101. The consequence, and
this section is its one home: **bootstrap blocks on millwright's own source are
hand-run by an operator-supervised session, their specs do NOT declare
`FACTORY_ADMIN`, and no spec of this chain restates this paragraph - they point
at it.** The rule is not new; it is what every block since M0-75 has actually
done, M0-75 itself included, and it has never been written down. A spec that
edits `GATE_PATHS` itself is the one exception and says so in its own text.

**(g) Budgets for a logic-heavy block.** M0-90 - a logic fix with a mandatory
second independent pass - ran about 145 minutes against a spec that authorised
`wall_minutes: 45`. The figure is the foreman's stopwatch over that block and
not a command's output, which is precisely why it is quoted here as an
order of magnitude and not as a measurement: the number this repository can
reproduce is the ceiling in the spec file, `grep -A 6 '^budget:'
factory/tasks/M0-90.yaml` on 2026-08-25. The decision it drives: logic-heavy M2
specs carry `wall_minutes` between 90 and 120 with `quality_attempts: 2`, each
spec saying in its priority comment why it sits where it does in that range.

**(h) Four open rows are raised in place, none is cloned.** M0-107, M0-34,
M0-65 and M0-60. Each keeps its id, its text and its hash-bearing fields except
`priority`, and each carries the reason and the date in the comment beside that
field. M0-107 and M0-34 are raises this session decided and the foreman's
package did not ask for; both are the direct consequence of a decision it did
ask for, and section 4 is the argument.

## 4. The two raises this session decided

**M0-107 is raised above the pick function because its own text says so.** The
M2 chain's third block builds `pickTasks`, and M0-107's subject is the word that
function is named after: whether a PAUSED row is `open`. Its `outcome` closes
with "the word is cheaper to fix before there is a second reader of it than
after", and the picker is exactly that second reader. So the chain's picker
declares `dependencies: [M0-107]`, and M0-107 moves to the slot directly above
it - a dependency that sits at the floor is a chain that cannot start. The
alternative the package offered, absorbing M0-107 into the picker, was refused:
M0-107's home is the standings vocabulary and the report, the picker's home is
the controller, and merging them would put one word in two places.

**M0-34 keeps its edge into M0-65 and is raised above it.** M0-65's own
`not_done_if` forbids re-opening M0-34's subject rather than depending on it,
and what the reaper needs from M0-34 is concrete: a named, recorded way to
reverse a row that was closed wrongly. Without it the reaper's
QUEUED-while-BLOCKED reconciliation would have to invent a transition, which
another line of the same `not_done_if` forbids. Dropping the edge would have
meant editing the dependency list of a spec whose text leans on it; raising the
dependency is the cheaper and the more honest of the two.

## 5. What this ADR does NOT decide

- The content of any M2 spec beyond its block size and its seam. Each spec is
  the home of its own outcome.
- The tick's parallel form - backgrounded builders, heartbeat, more than one
  builder at a time. That is M3 by section 3 (e).
- Whether `discovered_from` should become a required field, which would close
  the marker hole of section 2. G3 names the hole; closing it is a change to the
  TaskSpec contract and belongs to a spec of its own that nobody has filed.
- Which of M0-34's or M0-29's rule the trailer-derived landing belongs to beyond
  what this package settled: the fact went to M0-60 and the argument is in that
  file, not here.

## 6. Addendum, 2026-08-30 - G3 is built, what it would refuse, and four rows re-marked

Added by a carrier session (carrier #28) by foreman decision under section 0 as
relayed, not by a block. `main` stood at `9e95712` when the package began, the
tree was clean, and nothing under `src/`, `test/`, `scripts/`, `.githooks/` or
`DESIGN.md` was touched by it. Each decision below is
**[operator-confirmable]** and stands unless the operator vetoes it. The four
spec files carry the argument for their own row and point here; this section
carries what is common to them and is not restated in any of them
(discipline 12).

### (i) G3 applies rule 3 to EVERY spec that carries a provenance

M2-17 landed as `9e95712` and built the executor section 3 (a) promised: the
roadmap floor in `src/controller/queue.ts`. The gate reads the marker decision
(c) sets - `discovered_from` absent, `null` or `bootstrap` is planned work,
anything else is a finding - and refuses a finding priced above the lowest OPEN
roadmap spec of its own milestone and of the next entry of `MILESTONES`, the two
taken together.

The M2-17 verifier asked whether that is wider than ADR 0004 section 2 rule 3
authorises, since rule 3 says "discovered *hygiene*" and the gate says
"discovered anything". It is not, and the reading is fixed here rather than left
to the next reader: in rule 3 the load-bearing word is **discovered**, and
`discovered_from` is the executable spelling of it that decision (c) minted.
"Hygiene" names what a discovered row typically is, not a second condition a row
must also meet - and there is no field, and no proposal for one, that would let
a gate tell a "hygiene" finding from any other kind. A gate narrowed to a class
nothing records is a gate that refuses nothing. **The gate is not narrowed.**

### (ii) The first measurement: the gate is built and NOT armed

Two seams, both in `src/controller/intake.ts`, both pinned by the case "is built
and NOT armed, and arming it means TWO edits to intake, not one" in
`test/unit/queue-commands.test.ts` rather than by prose. `runIntake` does not
supply `QueueOptions.openSpecIds`, so the rule is vacuous in production; and
neither `outranks-roadmap` nor `unbacked-exception` is in `BLOCKING_ISSUE_KINDS`,
so a supplied open set would make intake REPORT rather than refuse. Arming it is
therefore a spec of its own, filed by this package.

What arming it would have cost, before this addendum's re-striping. The M2-17
block projected it with a one-liner carried whole in the body of `93fa5db`,
which reads the open set out of `node dist/cli.js queue` and asks `roadmapFloor`
about every spec file: on 2026-08-30 it printed `ALL 90` and `OPEN 49`. That
pair is the BLOCK's reading and this carrier did not re-take it - the re-striping
in (iii) and the two specs this package files had already moved both inputs by
the time the one-liner was run here, so re-running it would have measured a
different tree and reported it under the block's number. What was re-run is the
pair below, which is the one that governs the arming.

What it costs over the tree this package leaves behind - after the re-striping
in (iii) and after the two specs it files - re-run on 2026-08-30 and reported as
the precondition of the arming spec: over the live open set, 39; over the same
set with `M0-72` removed from it, 0. Asked of the rule itself rather than of the
projection, by calling `validateQueue` with the same open set on the same day and
counting the `outranks-roadmap` and `unbacked-exception` issues it returns, the
two answers are 38 and 0 - one fewer, because the arming spec declares the
exception M2-17 minted and the projection one-liner does not model exceptions.
Every refusal is against one row, `M0-72` at priority 25 in milestone M3, which
is the floor of M2 because the rule takes a milestone and the one after it
together. So the catalogue is one row away from being armable, and that row is
(iv).

The open roadmap rows themselves, which is the fact the rest of this section
follows from. On 2026-08-30, before any edit,
`node dist/cli.js queue | awk '!/^#/ && $7=="open" {split($4,a,"@"); print "factory/tasks/" a[1] ".yaml"}' | xargs grep -l -E '^discovered_from: *(null|bootstrap)'`
printed six files - M2-16, M0-56, M0-76, M0-07, M0-33 and M0-72 - at priorities
81 (M2), 79 (M4), 78 (M1), 64 (M2), 34 (M0) and 25 (M3). The block that built
the gate measured seven, itself included, before it landed. Five of the six sat
inside or below the findings band, which is the drift of section 1 seen from the
other end: not "no plan is filed" but "the plan that is filed is not the floor".

### (iii) Four rows re-marked, and what the marker is a record of

One raise and three re-markings. Every one of them is a decision about the
MARKER or the SLOT and about nothing else: no `outcome`, no `allowed_paths`, no
`resources`, no `budget` and no `dependencies` moved anywhere in this package.

- **M0-07, priority 64 -> 80.** Planned work by the marker
  (`discovered_from: bootstrap`) whose subject is not built: on 2026-08-30
  `grep -rn -i ascii src/verify/stage1.ts` printed nothing and exited 1, and
  `test/unit/commit-range.test.ts` does not exist. It keeps its marker and takes
  the planning band decision (d) sets, directly under M2-16 at 81.
- **M0-76, provenance `null` -> `M0-27`.** A finding whose subject is the
  measurement rule M0-27 authored; priority 78 untouched.
- **M0-56, provenance `null` -> `M0-27`.** A finding whose subject is the guard
  M0-27's own fix commit `2393c6f` added; priority 79 untouched. Two stale
  claims in its priority comment - the raise it records, and the row it says it
  sits below - were corrected in the same edit without moving a field.
- **M0-33, provenance `null` -> `M1-07`.** Re-measured first, because a spec
  that has stopped being true is withdrawn rather than re-marked: its own
  `measure` command, run on 2026-08-30, still names fourteen files whose
  `# Priority` comment disagrees with their `priority:` field, two of them
  created by raises this repository has made since the row was filed. Its filing
  commit `4f927c8` says in its own first line that the M1-07 verifier found it;
  priority 34 untouched.

**The marker is not a record of who noticed a row.** Two of the three
re-markings replace a comment that argued the opposite - that a carrier session
or an operating session finding something keeps the row unmarked - and that
argument was reasonable before there was an executor. It is not now. Decision
(c) makes `discovered_from` the roadmap-versus-finding classification the gates
read, and an unmarked finding does not merely mis-file itself: it becomes the
FLOOR every other row of its milestone is measured against. That is the marker
hole section 2 filed and declined to close, met from the inside. Closing it
properly - making the field required - is still a change to the TaskSpec
contract and still belongs to a spec nobody has filed.

### (iv) M0-72 is an open question with the operator and is not decided here

`M0-72`, at priority 25 in M3, is the last legacy roadmap row and the only
reason the armed projection of (ii) is not zero. It was left at the floor of the
queue by an operator request, the foreman put the question to the operator on
2026-08-30, and the answer was still outstanding when this package was written.
This carrier therefore did not touch it - not its priority, not its marker, not
its text. Re-striping it is the operator's, and the spec that arms G3 states the
projection as a precondition its block must re-run rather than as a number it
may make true by editing `factory/tasks/`.

## 7. Addendum, 2026-08-30 - an amendment that adds work re-prices the budget, or says why it does not

Added by a carrier session (carrier #29) by foreman decision under section 0 as
relayed, not by a block. `main` stood at `393c34a` when the package began, the
tree was clean, and nothing under `src/`, `test/`, `scripts/`, `.githooks/` or
`DESIGN.md` was touched by it. This decision is **[operator-confirmable]** and
stands unless the operator vetoes it.

### (i) What M2-16 measured about its own budget

M2-16 was filed on 2026-08-25 with `wall_minutes: 60`. Later the same day it was
amended, and its own priority comment says what the amendment did and what it
deliberately did not do: "this amendment adds the schedulable-band paragraph and
the not_done_if line that goes with it, and not a raise". The sentence is about
the PRIORITY. The budget is not mentioned anywhere in that comment, and the
paragraph the amendment added is the one that turned the row from a comparison
over a priority list into a comparison over the band `pickTasks` would admit -
which is the logic that took the block its three passes.

What the block then cost, re-run here on 2026-08-30 in this checkout:

```text
git log --format='%h %ad %s' --date=format:%H:%M:%S 2c4a0e5..393c34a

393c34a 06:43:41 merge: M2-16 - the factory can say that its own queue has stopped planning
d3e4788 06:43:10 docs: M2-16 - two sentences this block wrote that measurement refuted
41ef43a 06:13:58 fix: M2-16 - the open half of the band is pinned, and the excused case says so
55d5f2c 05:36:34 fix: M2-16 - the band is the OPEN band, and an exception has to be one
9a32229 04:55:58 feat: M2-16 - doctor reads the shape of the band, not only whether the disk has room
```

That span - first commit to merge - is 107 minutes, and it is a FLOOR rather
than the block's duration: it excludes everything before the build commit, which
section 2 of `.claude/commands/block.md` requires to be the orientation, the
build and the tests. The ceiling the spec authorised was 60. Two of the commits
in that span are the fix cycles ADR 0002 makes mandatory for a logic fix, each
followed by an independent pass, and section 3 (g) of this ADR already prices a
logic-heavy M2 row at 90 to 120. The row was never re-priced against the
paragraph that made it one.

### (ii) The rule, and why it is a note and not a gate

**An amendment that adds a `not_done_if` line or an `acceptance` item to an open
spec re-prices that spec's `budget`, or states in the same dated comment why the
budget is unchanged.** Adding an anti-criterion adds a test the block owes;
adding an acceptance item adds a proof it owes. Either can turn a row into the
logic-heavy class section 3 (g) prices separately, and a comment that argues only
about the slot has answered a different question.

Discipline 4 says a recurring lesson becomes a test, hook or gate and never
another paragraph of prose. This is the first measured instance, so it is a
dated note and not a gate - the executable form would be an intake check that
compares a spec's `budget` against its own amendment history, and nothing in
this repository reads that history yet. The second instance is what buys the
gate, and this paragraph is where the count starts.

### (iii) Applied once, immediately

M0-07 is the next row the picker takes and its `wall_minutes` was 45. The same
package that adds this note adds an acceptance item to M0-07 - the wiring point
into stage 1, which is work that row did not previously owe - and re-prices it
to 90 under section 3 (g), with this subsection as the argument. The edit and
its own reasoning are in `factory/tasks/M0-07.yaml`, which this section points at
rather than restating (discipline 12).
