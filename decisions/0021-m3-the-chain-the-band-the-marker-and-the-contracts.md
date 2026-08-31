# ADR 0021 - M3: the chain, the band, the marker, and the contracts DESIGN left open

Date: 2026-08-30. Context: a carrier session (carrier #30) by foreman decision -
not a block. `main` stood at `d67d9a1` when the package began, the tree was
clean, and nothing under `src/`, `test/`, `scripts/` or `DESIGN.md` was touched
by it.

M2 is consumed. `node dist/cli.js queue | awk '!/^#/ && $7=="open"' | wc -l`
printed 107 on 2026-08-30, and over that open set
`node dist/cli.js queue | awk '!/^#/ && $7=="open" {split($4,a,"@"); print "factory/tasks/" a[1] ".yaml"}' | xargs grep -l -E '^discovered_from: *(null|bootstrap)'`
printed exactly one file, `factory/tasks/M0-72.yaml`, on the same day. One
roadmap row, at priority 25, in a band whose top is 80. That is not drift
noticed late: it is the milestone-exit rule of ADR 0018 decision (b) firing on
schedule, and the executor said so in its own words on 2026-08-30 -

```text
node dist/cli.js doctor | grep queue.roadmap
```

printed `fail queue.roadmap ... | ordering: highest roadmap M0-72 (priority 25,
M3) vs highest finding M0-56 (priority 79, M4) - no roadmap row outranks it,
which is the drift ADR 0018 measured | existence: band top M2-28 (priority 80,
M2), so a roadmap row of M2 or M3 is owed - held by M0-72`.

G1 is REQUIRED, so the factory's own doctor is red until the next milestone is
planned. This ADR carries the decisions that plan it. The chain itself is
sixteen rows in `factory/tasks/` and this document does not restate any row's
outcome (discipline 12).

## 0. The sanction

The operator placed strategic decisions with the foreman on 2026-08-25. That
line is quoted in full in ADR 0018 section 0 and again in ADR 0019 section 0,
and is pointed at rather than quoted a third time.

What is new here is the reporting, and it is the foreman's account rather than
this session's measurement: the foreman reported the M3 planning decision and
the M0-72 default of section 1 (c) to the operator on 2026-08-30 at about 07:05
and again between 09:10 and 09:20, and no veto stood when the package that
produced this document was issued at 09:11. Both the report and the silence
reached this session as a relay from the foreman and not from the operator's own
terminal, which is stated rather than smoothed over - the same disclosure ADR
0018 section 0 and ADR 0020 section 0 make about their own sanctions.
**[operator-confirmable]**: every decision below stands unless the operator
vetoes it.

## 1. Decisions

### (a) The M3 band is 99 downward, inside the band ADR 0018 already named

`priority` takes `minimum: 0` and declares no maximum - the `priority` entry of
`FIELDS`, `src/controller/taskspec.ts`, read in this checkout on 2026-08-30 - so
a chain above 99 is available and was considered. It is refused. ADR 0018
decision (d) named "the free band from priority 99 downward" as THE planning
band, and the M2 chain has vacated it: on 2026-08-30 nothing open stood above
80, measured by the open-band command of the header. A second planning band
above 99 would give one convention two homes (discipline 12), and a band with no
ceiling invites each milestone to outbid the last, which is the drift of ADR
0018 section 1 in a form no gate reads.

So the chain occupies **99 down to 84**, in the dependency order of section 2,
and everything already filed keeps its slot: M2-28 at 80 (the completion of gate
G3, which ADR 0018 decision (d) puts directly under the chain) and the findings
at 79 and below. Nothing is re-striped.

**The floor constraint, and it is what the slots were chosen against.** After
this package the lowest OPEN roadmap row of M2 and M3 taken together is M0-72 at
84, and `roadmapFloor` (src/controller/queue.ts) takes a milestone together with
`nextMilestone` of it, so 84 is the floor every open M2 and M3 finding is
measured against. The highest open finding that does not declare an exception is
at 80. No finding is above the floor, which is what makes section 1 (b)'s four
exceptions the only ones the armed rule would ever need.

### (b) The marker: the chain is new roadmap rows, and four findings are excused where they stand

ADR 0018 decision (c) makes the roadmap marker the ABSENCE of a provenance. The
eleven rows this package mints therefore carry `discovered_from: null` and are
plan; they carry `M3-xx` ids for the same reason the M2 chain carried `M2-xx`,
which decision (c) already covers.

Four rows already filed say exactly what four slots of the chain need, and
minting a sibling beside a live owner is the defect this repository has measured
four times (discipline 12). They are raised in place - **M0-111** to 99,
**M0-133** to 98, **M0-139** to 96, **M0-112** to 89 - and each keeps its id, its
text, its paths, its resources, its budget and its dependencies. A raise is the
only field that moves, and one field is added.

**Each of the four gains `outranks_roadmap`, and it is required rather than
decorative.** All four carry a provenance, so all four are findings by the
marker, and all four now sit above the floor decision (a) sets. Without the
declaration the armed G3 would refuse the top of this repository's own plan the
day M2-28 lands, and `queue.roadmap`'s ordering half would compare the chain
against its own second row. With it, `checkRoadmapOrdering` skips them
(`src/controller/queue.ts`, the `carriesMeasurement` continue) and
`checkRoadmapBand` puts them in the `excused` partition, outside the ordering
comparison (`src/doctor/doctor.ts`). The line each of them carries is held to
M2-17's measurement rule, which is why every one of them names a command and a
date.

**The M2-30 hazard was checked and does not fire.** M2-30 records that the
existence half anchors on `topOfBand(band)` including the excused rows, so an
excused finding of a LATER milestone at the top of the band fails a queue that
has not drifted. After this package the band top is M0-111 at 99, whose
milestone is **M3**; `nextMilestone("M3")` is `M4`, and the chain's own roadmap
rows serve M3, so `serving` is non-empty and the existence half holds. No excused
row in this package carries a milestone later than M3, and a future raise into
this band owes that same check.

### (c) M0-72 takes the LAST slot of the chain, at 84

This is the foreman's default, put to the operator on 2026-08-30 at about 07:05
with no veto standing, and it closes the question ADR 0018 section 6 (iv) left
open.

The row's own comment records an operator request of 2026-08-21 that it sit
below every spec filed that day, and the reason it gives is preserved rather
than overturned: "it moves nothing in any chain". That is still true, and 84 is
still the bottom of everything planned - it is the floor of the M3 chain exactly
as 25 was the floor of the queue. What changed is the queue around it, not the
judgement about it: a row that is the ONLY open roadmap row is not at the floor
of a plan, it IS the plan, and it was holding G1 red and G3 unarmable in that
position.

The alternative was to park it, and the CLI has no verb for that: `grep -n pause
src/cli.ts` printed nothing and exited 1 on 2026-08-30, and the `KNOWN` set in
that file lists fourteen verbs, none of which parks a row. Rewriting the row's
standing by hand to clear a gate would be making a measurement true by editing
the thing it measures.

### (d) The rate-limit state file gets a contract, and the spec is where it lives

DESIGN.md section 11 says the factory "reads the rate-limit figures the
statusline channel provides - `rate_limits.five_hour.{used_percentage,
resets_at}` and `rate_limits.seven_day.{...}`, dumped atomically into a state
file the controller reads before each task". It names no path, no schema and no
producer, and `weekly_reserve_pct` appears in that prose and in no field table -
`grep -rn 'weekly_reserve\|seven_day\|PAUSE_UNTIL' src/` printed nothing and
exited 1 on 2026-08-30, and `CONFIG_FIELDS` in src/controller/config.ts gives
`[budget]` exactly two keys, `max_usd_per_tick` and `max_usd_per_day`.

**M3-06 is the one home of that contract** - the path, the schema, the producer
boundary and the `[budget]` keys - and this ADR sanctions its inventing one
rather than leaving the design's sentence unexecuted. **[operator-confirmable]**,
and NOT an edit to DESIGN.md: section 11 keeps its text, and the spec states in
its own outcome which of its decisions the design underdetermined.

### (e) The denominator of "verified merge" is DONE

DESIGN.md section 14 lists `usd_and_tokens_per_verified_merge` and
`verified_merge_rate` without saying what a verified merge is. Three readings
were available - MERGED, POST_MERGE_CHECK passed, or DONE - and the state
machine settles it: `TRANSITIONS` in `src/store/state-machine.ts`, read on
2026-08-30, gives `MERGED: ["POST_MERGE_CHECK"]` and
`POST_MERGE_CHECK: ["DONE", "BLOCKED"]`. So DONE is the state a row reaches only
by passing the post-merge check, and BLOCKED is where a regression goes. MERGED
would count a merge whose smoke has not run; POST_MERGE_CHECK is a transient the
row leaves in the same pass. **DONE, and the metric that divides by it says so
in the code that computes it** (M3-02).

The numerator's own count is contested and this decision does not touch it:
`quality_attempts` has two writers and two vocabularies, which is **M0-134**'s
subject, and a metric built on that column inherits whatever M0-134 settles.
M3-02 points at M0-134 and is forbidden to answer it.

### (f) A chain row's `dependencies` name only rows inside the chain

Three of the fourteen candidates are adjacent to a row filed below the chain -
M3-02 to M0-98 (priority 7), M3-06 to M0-81 (22), M3-10 to M2-27 (79). The
scouting package proposed a dependency edge for each. Each was refused, and the
refusal is one rule rather than three arguments.

`pickTasks` refuses a row whose dependency is not delivered (clause 4,
src/controller/dispatch.ts), so a chain row that depends on a row below the
chain's floor is unpickable for as long as that row stays there - which is the
"chain that cannot start" ADR 0018 section 4 names, and its remedy there was to
RAISE the dependency, not to declare it. Raising three more findings into this
band to satisfy three edges would be re-striping the queue to make a dependency
list true.

So adjacency is expressed the way M0-136 expressed it against M0-121: the
neighbour is named in the outcome and an anti-criterion forbids closing its
subject as a side effect. This is a deviation from the package this session was
handed and it is recorded here rather than in three spec comments.

One direction is also wrong on the merits and that is stated where it applies:
M0-81 asks whether the controller can price an attempt independently of what the
attempt reported, and its own outcome places that answer "where the weekly cap
becomes state the controller reads". M0-81 is therefore downstream of M3-06 and
not upstream of it, and an edge in the proposed direction would have been
backwards as well as unpickable.

### (g) A known limit that is recorded rather than filed

`src/verify/commit-range.ts` records in its own header that a NUL byte inside a
commit message ends the `git log -z` record early while `git rev-list --count`
still agrees, so the count cross-check does not catch it. It is reachable only
by forging an object: the header's own measurement says `git commit-tree`
refuses such a message, which leaves `git hash-object -w -t commit --literally`.
`grep -il 'NUL byte\|hash-object\|raw object' factory/tasks/*.yaml` printed
nothing on 2026-08-30, so nothing owns it.

It stays recorded and unfiled. The closure is a reader of raw objects
(`GitBytesRunner`), which is real work; the exposure is an operator deliberately
writing an object git's own porcelain refuses; and a LOW row filed today would be
the 108th open row in a queue whose planning drought is this package's subject.
Filing it would be answering ADR 0018's finding with one more finding. If a
second instance arrives, that is what buys the spec (the counting rule ADR 0018
section 7 (ii) sets for a note).

## 2. The chain, and what each slot is for

Sixteen rows, in pick order. The order is the map's and the priorities implement
it; each row's own file is the home of its outcome and its argument.

```text
99  M0-111  raised   the day's spend has one home
98  M0-133  raised   the tick reserves each seat before it opens it
97  M3-01   new      a reservation is a row, not a local
96  M0-139  raised   the model that answered is recorded
95  M3-02   new      what a verified merge costs, computed from the database
94  M3-03   new      the router is the one chooser
93  M3-04   new      the dispatch decision is acted on
92  M3-05   new      effort escalates before the model does
91  M3-06   new      the weekly cap is state the controller reads
90  M3-07   new      a weekly-limit message parks the factory
89  M0-112  raised   the sixth clause of the pick rule gets a definition
88  M3-08   new      a worker's lease is extended while it runs
87  M3-09   new      the builder runs in the background
86  M3-10   new      two builders, and the slot counts stop being decoration
85  M3-11   new      the parallel run is proved by fault injection
84  M0-72   raised   the atlas
```

**M3-05 stays in M3 rather than deferring to M5.** DESIGN.md section 17 gives M5
the LEARNED router, and section 11 separates the two in its own text: the
learning paragraph is about accumulating `(task_class, model, effort)`
statistics, while "effort escalates before the model does" and the override
rules beside it are deterministic policy that needs no history. The cheapest
economic lever in section 11's own ordered list is "cheap-first with effort
escalation", and it belongs with the router that executes it.

**M3-11 is split off M3-10 because it is a different kind of proof.** M3-10 is
the code change - raise `TASKS_PER_PASS`, read `[concurrency]` - and M3-11 is the
DoD of section 17's M3 row: a parallel run with no double merge, no worktree
collision and no shared-resource pair, under fault injection. One block does not
carry both a scheduler change and a new fault-injection suite inside one wall.

## 3. What this ADR does NOT decide

- The content of any row beyond its slot, its marker and its seam. Each spec is
  the home of its own outcome.
- `resources` versus `exclusive_resources`. The picker unions them and says so -
  the `resourcesOf` docstring in src/controller/dispatch.ts records that this
  build grants no concurrent access to anything, "so both lists mean the same
  thing here", and calls a change to that a change to the TaskSpec contract.
  M3-10 removes the premise by making two tasks run at once, and nothing in this
  package settles the contract. M0-86 is adjacent. **Open.**
- Whether DESIGN.md section 8's stage 1 row should name the
  `commit_range_hygiene` condition M0-07 landed. The row at the "Scope and
  anti-cheat" line of section 8 lists the stage's conditions and does not name
  it, read on 2026-08-30; a diff to ratified text is an operator act (ADR 0020
  section 2 (a) is the precedent). **Open, and it is an operator question.**
- DESIGN.md section 7 step 6, "builder in the background". ADR 0018 decision (e)
  already says M3 satisfies it as written and that no DESIGN edit is owed; M3-09
  is the row that does. Recorded here so the next reader finds the pointer
  rather than re-deriving it.
- The three copies of the pick ceiling. `pickCeiling`
  (src/controller/schedule.ts) and two `Math.min(TASKS_PER_PASS, ...)` call sites
  in src/doctor/readiness.ts hold the same expression, measured on 2026-08-30 by
  `grep -rn 'TASKS_PER_PASS' src/`; M2-27 deletes the doctor's copies. M3-10
  raises the constant and is forbidden to delete them.
- Nothing in ADR 0020 section 3 is reopened. Its three open questions stand where
  they are.

## 4. Addendum, 2026-08-30 - the operator answers M0-72, and stage 1's row names a condition it runs

Added by a carrier session (carrier #31) by foreman decision, not by a block.
`main` stood at `96c398a` when the package began and the tree was clean apart
from two untracked operator handoff files in a private archive that is not
`src/`, `scripts/` or `.githooks/` was touched by it. `DESIGN.md` was touched at
exactly one line, which is (ii) below, and the ratified digest for the section
was rewritten in the same commit.

### (i) M0-72 is decided by the operator, and the row takes the top of the chain

Section 1 (c) placed M0-72 at the LAST slot of the M3 chain on the foreman's
default, with the operator's answer still outstanding - section 6 (iv) of ADR
0018 is where that question was opened. The answer arrived on 2026-08-30 at
about 09:55, relayed to this session by the foreman, in Russian:

```text
я так понимаю речь о снепшоте? Делать его после полного завершения каждого шага
M1, M2, M3
```

"I take it we are talking about a snapshot? Make it after each of the steps M1,
M2, M3 is fully finished." The Russian is quoted rather than translated away
because it is the authority the raise stands on; ADR 0006 and ADR 0018 section 0
set the precedent for a verbatim Russian line inside this English repository.
This is an OPERATOR decision and is therefore not marked
**[operator-confirmable]** - the operator decided it rather than declining to
veto it.

**The row is raised 84 -> 98 and the acceptance it now owes is in the file, not
here.** What the answer changes is not the atlas but its clock. A snapshot is
owed after a milestone is fully finished; the M2 chain finished on 2026-08-30 -
`node dist/cli.js queue | awk '$1=="DONE" && $4 ~ /^M2-/ {split($4,a,"@"); print a[1]}' | sort -u | wc -l`
printed 26 that day, and the ids run M2-01 through M2-26 with no gap - and the
state a M2 snapshot renders lives in a database `.gitignore` excludes and every
later landing rewrites. At the bottom of the chain the row would have rendered
the exit of M2 after the whole of M3 had landed on top of it. So the subject
became time-critical, which is a different fact from the one section 1 (c)
weighed, and the slot follows it.

98 rather than 99: decision (a) fixes the planning band at 99 downward, and
M0-111's landing vacated 99, but the same package puts M3-12 there under a
later operator sanction whose one home is section 2 of ADR 0022 - a probe that
makes every block after it cheaper is worth one block's delay to a snapshot, and
the snapshot's own deadline is the whole of M3 rather than the next block. So
M0-72 takes the highest slot left. It ties with M0-133
and takes the tie, because `compareSpecIds` (src/controller/dispatch.ts)
compares numeric chunks and 72 is below 133; measured rather than asserted, with
`node dist/cli.js queue --next` on 2026-08-30, which selected `M0-72` at rank 1
of ceiling 1 and refused M0-133 behind it on `resource_conflict` when the raise
had landed and M3-12 had not yet been filed.

**What this raise falsifies in the sections above, named rather than edited.**
Section 1 (a) says "the lowest OPEN roadmap row of M2 and M3 taken together is
M0-72 at 84, and ... 84 is the floor every open M2 and M3 finding is measured
against"; the floor is now M3-11 at 85. The last line of section 2's chain table
puts M0-72 at 84. Both were true when they were written and both are stale from
this addendum onward. A dated ADR records what was decided when, so neither is
rewritten - this paragraph is the correction, which is the same treatment ADR
0018 section 6 gave its own predecessors.

**What the raise costs the chain: nothing.** No chain row declares a dependency
on M0-72, so the dependency order section 2 implements is untouched, and the
three dependencies M0-72 itself declares - M0-26, M0-42, M0-43 - each have a
DONE row, checked on 2026-08-30 before the raise, so clause 4 of `pickTasks`
does not refuse it at the top of the band. The highest open finding that does
not declare `outranks_roadmap` stands at 79, well under the new floor, so no
finding is disturbed; `node dist/cli.js doctor | grep queue.roadmap` printed
`pass` on 2026-08-30 after the edit, with both halves satisfied.

**The budget was re-priced, and this is an application of ADR 0018 section 7 and
not a second instance of the defect it names.** The edit adds four acceptance
items and five anti-criteria, so `wall_minutes` moves 90 -> 120 and the dollar
ceilings move with it, inside the band section 3 (g) of ADR 0018 prices for a
logic-heavy row. The count that section 7 (ii) started is for amendments that add
work WITHOUT re-pricing; this one re-priced in the same edit, so the count does
not advance.

**The standing rule "a milestone exit owes a snapshot" is recorded here as the
next step and is NOT filed as a spec.** Three reasons, and the third is the one
that decides it. The rule has exactly one attainable instance - M2 - and M0-72's
own block is the first execution of it, so what a check should assert is what
that block is about to learn. A check written today would be red on its first
run over M1, whose snapshot is unattainable by construction because the database
of that day is not recoverable, and a gate red from birth is the shape M0-134's
sixth anti-criterion already refuses in this repository. And filing it today
would add the 119th open row to a queue whose planning drought is this ADR's own
subject, which is section 1 (g)'s reasoning applied to a rule rather than to a
limit. **The count starts here**: the second milestone exit that passes with no
snapshot is what buys the executable form, in the form ADR 0018 section 7 (ii)
sets for a note.

### (ii) DESIGN.md section 8's stage 1 row names the condition M0-07 landed

Section 3 left this open and called it an operator question. The operator was
asked on 2026-08-30 at about 09:55 and delegated it, in Russian, relayed by the
foreman: "хорошенько подумай и прими правильное стратегическое решение сам" -
"think it through properly and take the right strategic decision yourself." The
foreman decided to amend and bounded the amendment to one additive clause. This
subsection is the record of that decision and of what it deliberately does not
cover.

**The defect, in one sentence.** `runStage1` (src/verify/stage1.ts) runs nine
conditions and the ratified row named the eight computed from the diff; the
ninth, `commit_range_hygiene`, is computed from the COMMITS and landed with
M0-07 in `d67d9a1`. A landed, required, merge-blocking condition of a stage that
the ratified text does not mention is the documentary form of `tested != wired`
(discipline 3), and it is an invitation to a later tidying pass to remove the
check as unaccounted for. Every block and every verifier reads DESIGN.md; M0-07
was itself a bootstrap row of the plan, so what this edit does is let the design
catch up with its own plan.

**The edit is one clause and carries no detail**: the row gains "commit-range
ASCII and identity hygiene over `base..candidate` (M0-07)" and nothing else. The
executable home stays `src/verify/stage1.ts` and `src/verify/commit-range.ts`,
and the design names the condition rather than restating what it does
(discipline 12). The counterpart, blueprint section 8, was re-read as the
ratification guard requires: its Stage 1 block lists exactly the conditions the
row listed before this edit and says nothing about the commit range or about the
messages and identities inside it, because it predates M0-07. So this is
DESIGN.md moving ahead of an archive dated 2026-08-16 rather than the two
disagreeing - the shape ADR 0006's M0-42, M0-43 and M0-116 entries already
record. The ratified digest for section 8 moved `8ef00edbe99e2769` ->
`d7c8da04da2c1b56` in the same commit, and the reasoning above is written beside
it in `test/unit/design-ratification.test.ts`, which is where a reader of the
guard meets it.

**A SECOND unnamed condition was measured in the same reading and is handed up
as a packet rather than absorbed.** `factory_admin` is the seventh entry of the
same checks array, it is landed and required, and the row does not name it
either - and it is not covered by "factory gates and config not disabled", which
is `gates_enabled`, a different check. It is not a dormant one: ADR 0018 section
3 (f) leans on its behaviour in its own words, and `node dist/cli.js doctor`
printed on 2026-08-30, inside `live.readiness`, that "stage 1's factory_admin
refuses a candidate as soon as one changed path is one of them". A diff to
ratified text is an operator act; the decision relayed to this session named one
condition, so this carrier edited one condition. **The packet**: one more
additive clause in the same row naming `factory_admin`, plus the digest, plus
the counterpart re-read - the identical shape as the edit above, and it needs
the operator's or the foreman's word.

**What the pin would be, and why it is not bought yet.** The foreman's decision
set the counting rule for this class: the first case is a note, and a second case
buys a pin asserting that the stage 1 row names every check `runStage1` runs.
The `factory_admin` finding IS that second case. It is reported and not built,
for one reason: the pin belongs in `test/unit/design-ratification.test.ts`, which
this carrier may touch only for the digest, and building it is a block's work.
Whoever authorises the second clause should authorise the pin in the same breath,
because a row corrected twice by hand and pinned by nothing is a row that drifts
a third time.
