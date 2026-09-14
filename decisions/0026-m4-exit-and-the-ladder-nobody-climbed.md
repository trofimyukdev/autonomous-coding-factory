# ADR 0026 - the M4 exit: every mechanism the milestone names exists, and the one thing its DoD asks for has not happened

Date: 2026-09-11. Context: a carrier session (carrier #52) by foreman decision,
not a block. `main` stood at `ea95e8b` when the package began and the tree was
clean apart from two untracked operator handoff files in a private archive
that is not published.
Nothing under `src/`, `test/`, `scripts/`, `.githooks/`, `factory/checks.yaml`,
`factory/compat.json` or `DESIGN.md` was touched by this package; the two
fault-injection fixtures it mutated to take a measurement were restored from
copies taken first, and `git status --short` was clean of them afterwards.

Sections 1 to 4 are a READING of the M4 exit against `DESIGN.md` section 17,
taken by re-running every clause in this checkout rather than by trusting the
reports that closed the rows. Section 5 puts three questions to the operator and
answers none of them.

## 0. What sanctioned this, and why a carrier reads a milestone exit

The same arrangement ADR 0024 section 0 states and does not need restating here:
no row says a milestone is over, `DESIGN.md` section 17 states each DoD in one
sentence, and nothing in this repository executes that sentence - so the reading
is a carrier's, taken once, when the last row of the chain lands.

**The operator has not spoken about the M4 exit.** This package runs on the
foreman's kickoff under the standing delegation of 2026-08-25, and no operator
word about M4 being over, about the M5 chain, or about arming the timer had been
given when this was written. Everything here except the sanctions it quotes is
**[operator-confirmable]** and stands unless the operator vetoes it.

## 1. The DoD, read clause by clause

`DESIGN.md` line 773, read in this checkout on 2026-09-11:

```text
| M4 unattended | tick wrapper, systemd timer, circuit breakers, notifications, morning report, full fault-injection suite | soak ladder through step 5 |
```

Six names in the content column and one clause in the "done when" column. They
are read separately below because they answer differently.

### (i) The content column, name by name, each with its landing

Every hash below is from `git log --format='%h %ci' --grep "merge: <id> " -1`
run in this checkout on 2026-09-11, and every `quality_attempts` figure from the
event log rather than from a report:

```text
node -e 'for(const l of require("fs").readFileSync("factory/state/events.jsonl","utf8").trim().split("\n")){const e=JSON.parse(l);if(e.type==="BLOCK_RECORDED")console.log(e.seq,e.payload.spec_id,e.payload.integration_sha.slice(0,7),e.payload.quality_attempts)}' | tail -12
2706 M0-190 cf99847 0
2721 M0-176 c24403e 2
2732 M0-110 19ec8e5 0
2743 M4-01 60a533d 0
2769 M4-02 1caf753 0
2792 M0-109 c24f6c2 1
2818 M4-03 857ddc4 2
2855 M4-04 96f303e 1
2868 M4-05 3c6f47b 1
2881 M4-06 4231c71 1
2892 M0-201 ca57556 0
2905 M4-07 2a007ab 1
```

- **tick wrapper** - M4-01, `60a533d` (2026-09-08 20:59:33): `scripts/millwright-tick.sh`,
  with the STOP reading, the flock, the timeout and the exit-code table.
- **systemd timer** - M4-02, `1caf753` (2026-09-08 23:12:31): the unit and the
  timer as templates under `factory/systemd/`, a renderer, and an INSTALL packet.
  **Installation is operator-only and was not performed** (discipline 6).
- **circuit breakers** - M4-03, `857ddc4` (2026-09-10 20:14:01), with M0-201,
  `ca57556` (2026-09-11 06:17:21), which gave the terminal infrastructure breaker
  the human exit it had no verb for.
- **notifications** - M0-109, `c24f6c2` (2026-09-10 14:58:46): the first caller
  of `[notify] command`.
- **morning report** - M4-05, `3c6f47b` (2026-09-11 03:11:33), delivered from
  inside the tick and above its own STOP gate.
- **full fault-injection suite** - M4-06, `4231c71` (2026-09-11 05:16:06):
  blueprint section 15's four categories, with resource failures, git races and
  policy violations added to the kill points.

Plus the manifest row M4-04, `96f303e` (2026-09-11 01:30:34), the ladder itself
M4-07, `2a007ab` (2026-09-11 08:25:46), and the three pre-chain rows M0-190,
M0-176 and M0-110. **The content column is delivered, name for name.**

### (ii) The clause - "soak ladder through step 5" - THE MECHANISM EXISTS, THE CLIMB HAS NOT HAPPENED

"Step 5" is read the way ADR 0024 section 6 reads it and that reading is not
restated: rung 5 is "unattended cron by day", rung 6 is M5's.

What M4-07 landed is the ladder AS STATE. `RUNGS` (src/controller/ladder.ts) is
the enumeration's one home with `TOP_RUNG_IN_DOD` computed from it; migration 8
gives the current rung a row (`CREATE TABLE soak_rung`, src/store/migrations.ts)
whose `CHECK` names no upper bound deliberately, because which rungs exist is
policy and lives once; and `ladderAdmission` refuses a pass whose shape exceeds
the recorded rung at step 0d of the tick, above the manifest, doctor-lite and the
picker, returning `above_rung` which maps to `ExitCode.TEMPFAIL`
(src/controller/tick.ts, the outcome switch).

**And the factory stands on rung one.** Three measurements, taken in this
checkout on 2026-09-11:

```text
grep -c 'LADDER_RUNG_CHANGED' factory/state/events.jsonl
0

grep -rn 'promoteRung(' src/ --include=*.ts
src/controller/ladder.ts:681:export function promoteRung(

grep -n 'DEFAULT_RUNG' src/store/soak.ts
96:export const DEFAULT_RUNG = 1;
```

The rung has never moved, the only function that could move it has no caller
anywhere in `src/`, and the default is one - shadow. The verb a human would type
does not exist: M4-07's own header says so and files it upward, and this package
minted it as **M0-204** at priority 89 (section 5 (b) is the consequence).

**The verdict this reading takes: the DoD of M4 is NOT met.** `DESIGN.md`
section 18, whose title is "Definition of done before the first crontab", opens
"The factory does not go into cron until its own fault-injection suite is green
and the soak ladder **has been climbed**", and its next sentence is "The soak
ladder promotes only on measured thresholds, never on 'looks fine'". The clause
asks for a climb measured at each rung, and no rung has been climbed.

**THE REFUTATION THIS VERDICT OWES ITSELF, ATTEMPTED AND FAILED.** The generous
reading is that "soak ladder through step 5" asks for a ladder DEFINED through
step 5 - the rungs, their thresholds and the refusal, all of which exist - and on
that reading M4 is complete today. It does not survive section 18's own verb:
"has been climbed" is not satisfied by a ladder that can be climbed, and section
18 is the section 17 row's own expansion. The generous reading also makes the DoD
of M4 identical to its content column, which would leave the "done when" column
saying nothing.

**AND THE VERDICT'S OWN OPTIMISM IS WRONG TOO, WHICH IS THE PART THAT MATTERS.**
The foreman's kickoff put the reading as "rung 5 is ACHIEVABLE, not ACHIEVED".
Achievable is too strong, and the ladder's own clauses say why. `readSoakFacts`
windows every threshold by the rung's `since`, and its `tasks` field counts
"tasks of this repository that reached a gate verdict inside the window". In this
repository, on 2026-09-11:

```text
grep -c '"type":"GATE_PASSED"' factory/state/events.jsonl
0

grep -c '"type":"GATE_FAILED"' factory/state/events.jsonl
0

grep -n 'tasks_per_rung' src/controller/config.ts
807:  tasks_per_rung: positive("Tasks a rung must judge cleanly before the next rung is offered.", 10),
```

No gate verdict has ever been written, and the first clause of rung 1 wants ten.
`evaluateClauses` calls a clause whose fact is null NOT MET - "the rule that
keeps an unmeasured factory from being promoted by its own silence" - so
`promotionOffer` today reads `tasks 0 (at least 10)` and `false_block_rate
unmeasured`, and offers nothing. **The ladder cannot offer rung 2 until ten real
tasks have passed through a tick's gate, and no tick has ever opened a worker:**
`grep '"type":"AGENT_FINISHED"' factory/state/events.jsonl | grep -c '"run_id":"tick-'`
printed 0 on 2026-09-11, which is the same zero ADR 0024 section 3 (b) recorded
for the M3 exit, unchanged three days later.

So the honest verdict is narrower than the kickoff's and is this: **M4 built
every mechanism its content column names, and its "done when" column is blocked
behind exactly the gap M3's exit already named as the highest-value unproven
thing this factory has.** The ladder is not waiting on more machinery. It is
waiting on work.

## 2. The path: twelve landings, nine quality attempts, three second issues

The reader in section 1 (i), summed:

```text
node -e '...the reader above...' | tail -12 | awk '{n++; s+=$4} END {print "landings", n, "quality_attempts", s}'
landings 12 quality_attempts 9
```

**Nine adversarial rejections bought twelve landings**, 0.75 per landing, against
M3's 1.55 over twenty (ADR 0024 section 2). The figure inherits everything M0-134
says about the column, and this package added the forty-third point to that file
precisely because one of these twelve does not re-derive: M4-05 recorded 1 for a
test-only cycle that followed an accepting pass, which the rule counts as
nothing, while M0-201 recorded 0 for the same shape three hours later -
`grep -E '"seq":(2868|2892),' factory/state/events.jsonl | cut -c1-60` printed
`00:11:41.180Z` and `03:17:30.515Z` on 2026-09-11, three hours and six minutes
apart. This document and M0-134 first said seven hours; the figure was corrected
against the journal the same day.

The chain ran from `cf99847` (2026-09-08 15:02:48) to `2a007ab` (2026-09-11
08:25:46) - two days and seventeen hours of wall clock across twelve blocks.

**Three of the twelve landed only on a second issue**, and the three are named
with their parks: M0-109 (attempt 1 stopped at q2, `origin/m0-109-attempt-1-4ebd7d4`),
M4-03 (`origin/m4-03-attempt-1-df2b0ff`) and M4-04 (`origin/m4-04-attempt-1-791399b`).
Attempt 2 landed all three. **No row of the chain was abandoned.**

One landing needed a fix after its merge: `ea95e8b` (2026-09-11 08:46:32)
corrected the kill suite's merging cases, which section 4 is about.

## 3. What the M4 exit did NOT verify

Every item is a measurement taken on 2026-09-11 in this checkout, not a worry.

**(a) The timer has never been installed and has never fired.**
`systemctl --user list-units 'mw-*' --no-legend | wc -l` printed 0 on 2026-09-11
with no unit of this session running, and `ls -1 factory/systemd/` printed
INSTALL.md and the two `.in` templates - a unit and a timer that exist as text
and nowhere else. Installation is operator-only by discipline 6. Nothing in this
repository has ever been started by a clock.

**(b) The ladder has never been promoted, and cannot be.** Section 1 (ii) is the
measurement: zero `LADDER_RUNG_CHANGED`, zero callers of `promoteRung`, zero gate
verdicts to measure a threshold with.

**(c) The breakers have opened only in fixtures.** `grep -c '"type":"CIRCUIT_OPENED"'
factory/state/events.jsonl` printed 0. Both breakers, their thresholds, their
`HALF_OPEN` canary and the human reset are proved by unit tests and by fault
injection, and no live pass has ever tripped one.

**(d) The morning report has never been sent by a scheduler, and one branch could
never send it.** The report is delivered from inside `runTick`, above its own
STOP gate, which is exactly what `DESIGN.md` section 14 asks for. The wrapper's
STOP branch returns before the CLI starts at all: measured against a stub in a
temporary root, `wrapper exit 0, CLI invocations 0` with a STOP file armed and
`wrapper exit 0, CLI invocations 1` without one. Raised in place as M0-195's
eighth finding by this package.

**(e) The weekly cap producer is still unwired.** `node dist/cli.js doctor`
printed `skip  budget.rate_limit  no rate-limit reading is recorded at
<control-root>/rate-limits.json; nothing outside this repository
has written one`. M0-176 landed the reader end of it; nothing writes the file, so
the constraint `DESIGN.md` section 11 calls the real budget is still invisible to
the factory.

**(f) Three fault-injection conditions are named and uncovered**, disclosed by
block113 while it landed M4-06 rather than discovered afterwards: a task branch
deleted under a live run; a STALE worktree (`parallel-worktree-kill` covers
collision, not staleness); and a hung test. Four more are recorded there as not
reproducible without root or a paid call - a full disk, exhausted descriptors
(`ulimit -n 12` aborts node itself at `uv_loop_init`), and a worker OOM, 429 or
expired credential.

**(g) The integration lock publishes its name before its contents.** From the
same block: `create` opens with `openSync(path, "wx")` and writes the record
afterwards, so a competitor reading the gap is told the lock is unreadable.
Block113 REPORTED one occurrence in twelve runs under load; this package read the
code and did not reproduce the race, so that figure is inherited rather than
re-measured and the row says so. It cannot merge twice and cannot free a held
lock; what it costs is a wrong diagnosis. The module's own docstring says the
opposite - "it is written before the descriptor is closed, so a reader never sees
an empty lock file that was about to be filled in" - and that sentence is part of
what the fix owes. Filed by this package as **M0-206**.

**(h) One known flake stands, and its owner is filed.** `tick.test.ts:1512`
("prints past the ceiling and otherwise ends cleanly") is red under load and
green when re-run alone; the live owner is M0-82 at priority 21, and M0-203 at 76
is the detector that would stop this class landing green.

**(i) The verb `millwright ladder promote` does not exist.** Minted as M0-204 by
this package and not built.

## 4. The count this starts, and the lesson for specs

**The count, in the form ADR 0018 section 7 (ii) sets.** The second time a
milestone of this repository is declared complete while the number in its own DoD
prints an absence - ADR 0024 section 4 started that count for M3's
`$/verified merge`, and M4's "soak ladder through step 5" is the second
occurrence of the same shape: the instrument exists, is correct, and has nothing
to measure. **The count stands at two.** What it is evidence FOR is not that the
milestones were wrong to build the instruments, which was the right order; it is
that this repository has now spent two milestones' worth of blocks building
things whose DoD only a live run can satisfy, and the live run is not itself a
milestone anywhere in section 17.

**The lesson for specs, and this is its one home.** A row that adds a refusal to
the tick's PREAMBLE must name, in its own `allowed_paths`, the fixtures that
drive a tick. M4-07 added the soak ladder's refusal at step 0d; every
fault-injection child that runs a controller passes through that step; the two
children whose cases merge were refused there and left early, and the suite went
red after the merge. The repair, `ea95e8b`, edited
`test/faultinjection/controller-kill-child.mjs` and
`test/faultinjection/parallel-kill-child.mjs` - both outside M4-07's paths, both
M4-06's tree - and cost a path sanction after the fact (foreman, 2026-09-11
08:53, [operator-confirmable], in the form M4-04.yaml's own DECISION (e) set on
2026-09-10 for the same situation - ADR 0024 section 9 has addenda (a), (b) and
(c) and no (e), and an earlier version of this paragraph cited one).
The general rule is the one ADR 0024 addendum (a) reached for dependencies: what
a row must own is decided by what its change REACHES, and a change to a shared
preamble reaches every caller of it. M0-206, filed by this package, carries
`test/faultinjection/**` in its paths for exactly this reason.

**One claim this package refuted rather than filed**, recorded because a refuted
finding is worth as much as a filed one. The report that produced `ea95e8b` was
read as saying that no case fails when the fixtures' rung declaration is removed -
that the declaration was therefore untested. It was measured instead of believed:
with the declaration deleted from `controller-kill-child.mjs`,
`test/faultinjection/controller-kill.test.ts` stayed green (8 passed, 21.76 s,
started 09:52:25) and `test/faultinjection/integration-kill.test.ts` went red
(3 failed of 3, started 09:54:09); with it deleted from `parallel-kill-child.mjs`,
`test/faultinjection/parallel-integration-kill.test.ts` went red (2 failed of 2,
started 09:54:54). Both declarations are covered by a failing case. **No row was
minted for it**, and the fixtures were restored from copies taken before the
edit.

## 5. Three questions for the operator

None of these is decided here.

**(1) Is the M5 chain minted, and does it start with the repo-truth run?** The
top of this repository's queue is now M0-204 at 89 (this package's mint, a
finding with `outranks_roadmap`), then M0-202 at 88 (an M4 finding, also
outranking) and M0-198 at 88 and M0-197 at 87, which are the only two OPEN
ROADMAP ROWS in the repository and are both M5. `ls factory/tasks/M5-*.yaml`
found no file on 2026-09-11: **the M5 chain of `DESIGN.md` line 774 -
"`repo-truth` plugin, `checks.yaml`, queue migration, cron 24/7", done when
"30-50 real tasks; router and lens order recomputed from data" - is not minted,
and this package did not mint it, because that is the operator's word.**

*This seat's recommendation, with its reason.* Mint it, and put the `repo-truth`
run first. ADR 0023 section 7 records the operator's own answer of 2026-09-08 -
"! требовать прогон repo-truth"
("! require a run of repo-truth") - which makes phase 1 REQUIRED rather than
satisfied by the showcase, and phase 1's control root does not exist:
`ls -d ~/.config/millwright/repo-truth` printed "No such file or directory" on
2026-09-11. It is also the cheapest answer to section 1 (ii): phase 1 is a
shadow run with no money and no merge, and it is the only way this factory
acquires the gate verdicts its own ladder needs before any rung can be offered.
M5's own DoD - thirty to fifty real tasks - is the same requirement at scale.

**(2) Should the timer be installed now? This seat's answer is no, and the reason
is measurable.** A `millwright tick --trigger cron` on rung 1 is refused by
`ladderAdmission` at step 0d, which returns `above_rung`, which maps to exit 75.
The wrapper's exit-code table turns 75 into a successful wrapper run: the case
block writes one `TEMPFAIL tick exited 75; the database carries not_before and
the backoff, so this run ends successfully` line into the skip log and exits 0.
So a timer armed today would fire ninety-six times a day, do nothing every time,
report success to systemd every time, and leave ninety-six identical lines in a
bounded log that trims itself - and the morning report that would tell an
operator this is the report section 3 (d) shows a STOP-ed factory never receives.
**The order that follows from this is: M0-204 lands, the factory acquires real
gate verdicts (question 1), a rung is promoted on a measured threshold, and the
timer is armed at the rung that needs it - not before.**

**(3) Phase 2 of ADR 0023 - a live, paid tick on `repo-truth` - is a spend
question and is still unasked.** ADR 0023 section 2 puts it behind "an operator
spend sanction, asked as its own question". This ADR does not ask it either. It
is named here only so that the answer to question 1 is not mistaken for it:
phase 1 spends nothing.

*[SUPERSEDED 2026-09-12 by carrier #55, in both of its clauses, and kept verbatim
as the record of what this exit reading believed. "Still unasked": it was asked
by ADR 0027 section 5 (1) and answered, and ADR 0027 section 7 records the
operator's word. "Phase 1 spends nothing": ADR 0027 section 1 (v) measured the
opposite and found the clause unsatisfiable by any run that proves anything -
both runs this repository counts as phase 1 drove a real builder and spent - and
ADR 0023 section 2's boundary has since been corrected to no MERGE and no LOOP.
That correction has its one home there; this bracket points at it rather than
restating it.]*

## 6. What this ADR does NOT decide

- **Whether M4 is declared complete.** Section 1 (ii) reads the DoD as unmet and
  says what would meet it. Declaring a milestone over is the operator's.
- **Whether the M5 chain is minted, and in what order.** Section 5 (1) is a
  recommendation with its reason, and nothing in `factory/tasks/` was created for
  M5 by this package. ADR 0021 decision (a)'s one band still stands.
- **Whether the timer is installed.** Section 5 (2) recommends against it today
  and the act is operator-only regardless (discipline 6).
- **Whether a paid tick is authorised**, on this repository or on `repo-truth`.
- **The content of the rows this package filed beyond their slot and their
  argument.** Each spec is the home of its own case: M0-204 (89, the promote
  verb), M0-205 (79, two homes in src/cli.ts), M0-206 (79, the lock's window),
  M0-207 (64, the notice repeated every tick), M0-208 (12, six small things), and
  the raises into M0-195, M0-181 and M0-134.
