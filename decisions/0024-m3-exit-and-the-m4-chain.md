# ADR 0024 - the M3 exit, and the M4 chain in draft

Date: 2026-09-08. Context: a carrier session (carrier #46) by foreman decision,
not a block. `main` stood at `bbae1f7` when the package began and the tree was
clean apart from two untracked operator handoff files in a private archive
that is not published.
Nothing under `src/`, `test/`, `scripts/`, `.githooks/`, `factory/checks.yaml`
or `DESIGN.md` was touched by this package.

Two things are recorded here and they are different in kind. Sections 1 to 5 are
a READING of the M3 exit against `DESIGN.md` section 17, taken by re-running
every clause in this checkout rather than by trusting the reports that closed
the rows. Section 6 is a DRAFT of the M4 chain that mints nothing: until the
operator says the word, the queue stands on the finding band and the draft is a
document.

## 0. What sanctioned this, and why a carrier reads a milestone exit

A block reads its own row. Nobody reads the row that says a milestone is over,
because no row says it: `DESIGN.md` section 17 states the DoD of each milestone
in one sentence and nothing in this repository executes that sentence. The
foreman's standing arrangement is that the reading is a carrier's, taken once,
at the moment the last row of the chain lands - which is what the queue itself
announced on 2026-09-08 at 09:42, in the only way it can:

```text
node dist/cli.js doctor
fail           queue.roadmap          band 134 of 514 row(s), 1 open row(s) refused by a clause of the picker; M0 0 roadmap / 8 finding(s), M1 0 roadmap / 33 finding(s), M2 0 roadmap / 62 finding(s), M3 0 roadmap / 22 finding(s), M4 0 roadmap / 9 finding(s) | ordering: highest roadmap none vs highest finding M0-56 (priority 79, M4) - no roadmap row outranks it, which is the drift ADR 0018 measured | existence: band top M0-56 (priority 79, M4), so a roadmap row of M4 or M5 is owed - the band holds none
```

Both halves of `queue.roadmap` are red, and this is not the transient M2-30
records. It is the milestone-exit red: **there is no open roadmap row left in
this repository at all.** The gate is doing exactly what ADR 0018 built it to
do - a queue with nothing but findings in it has stopped planning - and the
cure is a new chain, not a fix to the gate.

Everything in this document except the operator sanctions it quotes is
**[operator-confirmable]** and stands unless the operator vetoes it.

## 1. The DoD, read clause by clause

`DESIGN.md` section 17, the M3 row, read in this checkout on 2026-09-08:

```text
| M3 economics and parallelism | budgets and reservations, router, slots, conflict-aware scheduler, two builders | $/verified merge computed from the database; parallel run without conflicts |
```

Two clauses in the "done when" column and five names in the "content" column.
They are read separately below, because they fail separately.

### (i) Clause 1 - "$/verified merge computed from the database" - MET IN FORM, AND THE NUMBER IT YIELDS IS AN ABSENCE

The verb is `millwright metrics`, and it is the one this clause names.
`src/cli.ts` describes it as "the north-star numbers of DESIGN.md section 14,
computed from the rows and never asserted", and `formatMetrics`
(src/report/views.ts) states in its own docstring that nothing is computed in
the renderer - every division happens in `buildVerifiedMergeMetrics`
(src/controller/bookkeeping.ts), so `--json` and the printed view cannot
disagree. That is the shape the clause asks for: a figure DERIVED from rows, not
a figure an author wrote down.

Run in this checkout on 2026-09-08 at `bbae1f7`, abridged only by dropping the
token rows, which all read the same:

```text
node dist/cli.js metrics
repo                                                          millwright
verified_merges                                               102
verified_merges.priced                                        0
verified_merges.unpriced                                      102
verified_merges.no_attempt_row                                102
failed_out                                                    0
verified_merge_rate                                           1
first_pass_verified_rate                                      -
priced_verified_merges.usage.cost_usd                         -
usd_and_tokens_per_verified_merge.cost_usd                    -
```

**The clause is met in its executable form and the number it produces today is
`-`.** Not zero: an absence. Every one of this repository's DONE rows was
delivered by a hand-run block, and a hand-run block writes no attempt row, so
there is no priced spend for the divisor to take. The view says this itself
rather than printing a plausible figure - "102 of 102 verified merge(s) carry no
priced attempt ... and are left OUT of the divisor rather than counted as free
(M0-111: a spend nobody measured is not a spend of zero)".

The reason is one fact and it is measured, not inferred:

```text
grep '"type":"AGENT_FINISHED"' factory/state/events.jsonl | grep -c '"run_id":"tick-'
0
```

Three paid agent runs exist in the whole event log and all three are
`shadow-*` runs on M0-25; seven ticks have started
(`grep '"type":"RUN_STARTED"' factory/state/events.jsonl | grep -c '"verb":"tick"'`
printed `7` on 2026-09-08) and not one of them ever opened a worker. So the
factory can compute the number it exists to optimise, and has never generated an
observation to put in it. That is a true statement about M3 and it is section 3's
subject, not a defect of this clause.

### (ii) Clause 2 - "parallel run without conflicts" - MET, AND PROVED BY FAULT INJECTION

M3-11 landed at `bbae1f7` on 2026-09-08, `BLOCK_RECORDED` seq 2640, with three
new fault-injection processes rather than unit tests: `parallel-integration-kill`
(two REAL controllers over one repository, the first held inside the integration
lock, the second started only once the lock file exists, killed at
after-local-integration, landings counted on the bare origin by their trailers),
`parallel-worktree-kill` (a barrier of two builders of one pass, killed during
build, asserted on `attempts.workspace` and the directories that actually exist)
and `parallel-resource-kill` (three rows ranked so the ceiling would take the
pair, the verdict read from `attempts.started_at` / `ended_at`). The three names
are registered in `test/unit/kill-suite-wiring.test.ts`, so a file that stops
running is a red test and not a silence.

The three properties are the three ways a parallel run breaks - a double merge, a
worktree collision, a shared-resource pair - and each is established by a kill at
the seam that would break it. The distinction from M3-10 is the one ADR 0021
decision (b) drew when it split the two rows: M3-10 was the code that lets two
builders run, and passing unit tests over it prove a scheduler, not a run.

### (iii) The content column, name by name, each with its landing

The one-line reader over the event log, run on 2026-09-08, filtered to the chain:

```text
node -e 'for(const l of require("fs").readFileSync("factory/state/events.jsonl","utf8").trim().split("\n")){const e=JSON.parse(l);if(e.type==="BLOCK_RECORDED")console.log(e.seq,e.payload.spec_id,e.payload.integration_sha.slice(0,7),e.payload.quality_attempts)}'
2065 M0-111 96c398a 1
2111 M3-12 fb79fca 2
2129 M0-72 3df2155 1
2142 M0-133 b2898d8 1
2177 M3-13 2fa2104 3
2210 M3-01 ea15637 2
2223 M0-139 b472c14 1
2238 M3-02 d3082b1 2
2253 M3-03 f6a7c84 2
2290 M3-04 c5383c5 2
2314 M3-05 fae2025 1
2327 M3-06 76ebefe 1
2382 M3-07 cd07c18 2
2448 M0-112 037664a 2
2463 M3-08 8ce2cc1 2
2493 M0-168 f363bdd 1
2552 M3-09 d88ea60 1
2606 M0-178 9a4f9c0 2
2629 M3-10 84e4b2f 2
2640 M3-11 bbae1f7 0
```

Against the five names of the content column:

- **budgets and reservations** - M0-133 (the tick reserves each seat before it
  opens it, seq 2142), M3-01 (the reservation is a durable row and not a local,
  seq 2210), M3-06 (the weekly cap is state the controller reads, seq 2327),
  M3-07 (a weekly-limit message parks the factory, seq 2382), and M0-111 (the
  day's spend has one home, seq 2065).
- **router** - M3-03 (the router is the one chooser, seq 2253), M3-04 (the
  dispatch decision is acted on and journalled, seq 2290), M3-05 (effort
  escalates before the model does, seq 2314), M0-139 (the model that answered is
  recorded, seq 2223).
- **slots** - M3-10 (seq 2629): `TASKS_PER_PASS` raised and `[concurrency]`
  actually read. Its own effect is visible in the queue - `node dist/cli.js queue --next`
  printed `ceiling  2 = min(TASKS_PER_PASS 4, controller.max_tasks_per_tick 3)`
  on 2026-09-08. Before that row it was 1: `git show 0e6312b:src/controller/schedule.ts | grep -n 'TASKS_PER_PASS ='`
  printed `151:export const TASKS_PER_PASS = 1;` against `src/controller/schedule.ts:169:export const TASKS_PER_PASS = 4;`
  today.
- **conflict-aware scheduler** - M0-112 (the sixth clause of the pick rule gets a
  definition, seq 2448) and M3-10, which gave that clause its number via
  `[concurrency] max_shared_paths`.
- **two builders** - M3-10 for the code and M3-11 for the proof (seq 2640).

And the queue holds no open roadmap row of M3 to contradict any of it:

```text
node dist/cli.js queue | grep -E 'M3-[0-9]+@' | grep -vc 'DONE\|SUPERSEDED'
0
```

All thirteen `M3-xx` rows reached DONE. The twenty-two rows `doctor` counts under
milestone M3 are findings carrying a `discovered_from`, which by ADR 0018
decision (c) is exactly what makes them not-plan.

## 2. The path: twenty landings, thirty-one quality attempts, and seven reissues

The chain as executed is the twenty rows above - the sixteen ADR 0021 section 2
planned, plus M3-12 and M3-13 (the mutation probe and its wiring, which preceded
the chain) and M0-168 and M0-178, which the run added while it went.

```text
node -e '...the reader above...' | grep -E ' (M3-[0-9]+|M0-(111|133|139|112|72|168|178)) ' | awk '{n++; s+=$4} END {print "landings", n, "quality_attempts", s}'
landings 20 quality_attempts 31
```

**Thirty-one quality attempts bought twenty landings**, which is the honest
price of the milestone and is 1.55 adversarial passes per landing. The figure is
the recorded `quality_attempts` column and inherits everything M0-134 says about
it: the number is written freehand by whoever ran the block, against a rule that
nothing refuses a disagreement with. It is reported here with that caveat rather
than dressed up as a measurement.

Reissues after a stop are NOT derivable from the queue. Counting versions per row
mixes two different things:

```text
node dist/cli.js queue | grep -E ' (M3-[0-9]+|M0-(111|133|139|112|72|168|178))@' | awk '{print $4}' | sed 's/@.*//' | sort | uniq -c | sort -rn | head -5
      5 M3-10
      5 M3-09
      5 M0-72
      5 M0-178
      5 M0-112
```

A SUPERSEDED version is created by a spec EDIT as much as by a stop-and-reissue -
a raise, a carrier amendment and a re-issued block all leave one - so five
versions is not five attempts. What the count does establish is that the five
rows above were re-enqueued four times each, and the foreman's own ledger names
seven of the chain's rows as successful reissues after a recorded stop: M3-12,
M3-05, M3-07, M0-112, M3-09, M0-178 and M3-10. Those stops are recorded in the foreman's own
ledger and, for M3-07 and M0-112, in the foreman memory rather than in an ADR -
the stop ADRs 0009 through 0017 all predate this chain.
**A third of this chain landed only on a second issue, and no row of it was
abandoned.** That is the shape of the milestone: expensive per row, and it
finished.

## 3. What the M3 exit did NOT verify

This is the half that matters, and every item is a measurement rather than a
worry.

**(a) Two of the four `[concurrency]` counters have no reader.** `heavy_tests`
and `opus` are declared in `CONCURRENCY_FIELDS` (src/controller/config.ts) and
read by nothing:

```text
grep -rn 'heavy_tests' src/ --include=*.ts
src/controller/config.ts:512:  heavy_tests: positive("Parallel heavy test slots.", 1),
```

One line, and it is the declaration. `builders` and `max_shared_paths` are read
by `pickCeiling` and `sharedPaths`; `integrations` is normative for the lock and
is the one number section 10 forbids raising. So the "slots" name in the content
column is delivered for the counter that binds a pass and undelivered for the two
that would bind a heavy rung and a senior-model seat. M3-10's own file records
this in its `not_done_if` and in a dated comment - the row refused to claim them -
so this is a disclosed gap and not a discovered one. Section 7 puts it to the
operator.

**(b) A paid live tick has never run.** The evidence is section 1 (i)'s zero.
Everything the M3 chain built - the router, the reservation ledger, the escalation
rule, the slot ceiling, the conflict clause - has been exercised by unit tests,
by fault injection and by hand, and never once by a tick that opened a worker and
spent money. `doctor` says the same thing from the other end:

```text
skip           auth.minimal_request   a credential is present (<home>/.claude/.credentials.json exists) but a live request spends the weekly subscription cap and nothing opted in: set MILLWRIGHT_LIVE_BACKEND=1 in the environment of the call to permit it
```

ADR 0023 section 2 puts the first paid tick in **phase 2**, behind an operator
spend sanction "asked as its own question", and that question has not been asked
and not been answered. *[SUPERSEDED 2026-09-12 by carrier #55: the question was
asked, by ADR 0027 section 5 (1), and answered. ADR 0027 section 7 records the
operator's word and the one condition it left standing. The sentence is kept
verbatim as the record of what was true when this section was written.]*
This section does not ask it either. ADR 0022 section 2
already ranks the live rung as the highest-value unproven thing this factory has,
and the M3 exit does not change that ranking - it sharpens it, because the number
the milestone exists to produce is exactly the number only a live rung can fill.

**(c) The weekly cap is readable and is not read.** M3-06 built the reader and
M3-07 built the parking behaviour; nothing writes the file they read.

```text
skip           budget.rate_limit      no rate-limit reading is recorded at <control-root>/rate-limits.json; nothing outside this repository has written one, so the weekly cap was NOT read on this pass - wire the statusline producer to write it
```

The producer is **M0-176**, open at priority 79. `DESIGN.md` section 11 makes the
subscription weekly cap the real budget, so today the factory bounds itself by the
dollar ceilings - which are a proxy - and cannot see the constraint that actually
runs out. Section 6 puts M0-176 FIRST in the M4 chain for this reason, and the
reason is ADR 0023 section 1's own sentence about trigger B: "a 24/7 clock over a
factory that cannot read its own weekly cap is a way to discover the cap by
hitting it."

**(d) One claim about the reservation room is unmeasured.** The adversarial
verifier of block97 (M3-10, attempt 2) raised, and nobody has measured, that the
room check goes stale against actual spending: at a tick cap of 18, two scouted
rows pass a $17.80 promise, the two scouts then spend about $3 each, and the two
`builder_hard` seats that follow hold $16 against a room of 12 - reachable, the
verifier argued, by one dispatch on the shipped defaults. It is filed as a
measure-first note on **M0-146**, whose findings (6) and (7) already own the room
question at exactly these call sites, rather than as a new row (discipline 12).
Nothing here asserts the claim is true; what is recorded is that it is unmeasured.

**(e) The parallel proof has no case at one of the seven kill points.** Blueprint
section 15 enumerates the kill points, and the last of them is "after push, but
before the database record". M3-11's `parallel-integration-kill` kills at
after-local-integration, where nothing has been pushed yet - so the property it
can assert there is "no double merge", and the count of merges at a seam before
the push is not falsifiable by that case. The SEQUENTIAL case at the
after-push-before-record seam is M2-14's - "The two kill points that can merge
twice", DONE at priority 83 - and the CONCURRENT one does not exist. This is a test-strength gap in the DoD's own second clause and it is
disclosed by the block that proved that clause.

**(f) The escalation case in the middle of a two-row pass is unpinned.** Also
from block97: `affordableRung` asks the room NET of what the pass has already
promised, and a mutant in that one site survives the suite. The code is landed
and correct as far as anyone has argued; what is missing is the case that would
notice if it stopped being.

Items (e) and (f) are test-only rows in the finding band and are listed in
section 6's second table.

## 4. The count this starts

**In the form ADR 0018 section 7 (ii) sets for a note**: the second time a
milestone of this repository is declared complete while the number in its own DoD
prints an absence, the pattern stops being a record and buys an executable form -
a milestone exit that names, per clause, the reading that satisfies it and the
verb that produces it, checked where the exit is checked. One occurrence is a
plan that built its instrument before it had anything to measure, which is the
right order and not a defect. **The count starts here.**

What that executable form is NOT: a gate on `millwright metrics` returning a
figure. A factory that refuses to leave a milestone until it has spent money on
itself is a factory that spends money to satisfy a gate.

## 5. ADR 0023's trigger B has fired

ADR 0023 section 1 defines **B - `cron-truth`** as the unattended clock, records
it as "decided and deferred", and gives it one trigger: **"the DoD of M3 is
met."** Sections 1 and 2 above are that reading, and by it the trigger has FIRED:
both clauses of the DoD are met, the thirteen roadmap rows of the chain are DONE,
and the queue holds no open roadmap row of M3.

**The trigger firing is not the start.** ADR 0023 records B as decided and
deferred, and what a fired trigger buys is the right to ask - it does not
authorise a seat to begin. The operator was asked on the morning of 2026-09-08
and the answer had not arrived when this document was written. Until it does,
this ADR mints nothing (section 6) and the queue stands on the finding band, with
`node dist/cli.js queue --next` selecting M0-56 at priority 79.

The relationship between B and M4 is worth one sentence, because they are not the
same thing and the draft below treats them as one chain deliberately. B is the
clock; M4 is everything that has to exist before a clock is safe to start - the
wrapper the timer calls, the breakers that stop it, the notifications that wake
somebody, and the ladder that says which rung it may run at. Starting B without
M4 is not an aggressive schedule, it is an unattended factory with no brakes.

## 6. THE M4 CHAIN, DRAFT [operator-confirmable]

**Nothing in this section is minted.** It is a plan for a package that runs only
on the operator's word, and it is written down now because the reading that
justifies it was taken now.

`DESIGN.md` section 17, the M4 row:

```text
| M4 unattended | tick wrapper, systemd timer, circuit breakers, notifications, morning report, full fault-injection suite | soak ladder through step 5 |
```

**"Step 5" has a number and it is the blueprint's.** `DESIGN.md` section 18 gives
the rungs in prose - "shadow ... -> supervised auto-merge ... -> two parallel
builders -> normal concurrency -> unattended cron by day -> cron 24/7" - and
blueprint section 15 numbers exactly that list 1 through 6. So **step 5 is
"unattended cron by day"**, and step 6, cron 24/7, is section 17's M5 row. The
DoD of M4 is therefore: the factory runs on a timer, unattended, in daylight,
with each lower rung promoted on its own measured threshold. That reading is what
the chain below is sized against.

### The band

ADR 0021 decision (a) fixes the planning band at 99 downward and refuses a second
band above it. The M3 chain has now vacated 99 to 84 exactly as the M2 chain
vacated it before, and the highest open row in this repository is a finding at
79. So the M4 chain takes **99 down to 85**, and nothing already filed is
re-striped.

Two rows in the table are RAISED IN PLACE rather than minted, because a live
owner already says what the slot needs and minting a sibling beside one is the
defect this repository has measured four times (discipline 12). Each raise gains
`outranks_roadmap` for the reason ADR 0021 decision (b) gives: without it the
armed G3 refuses the top of this repository's own plan.

**The M2-30 hazard must be re-checked by whoever mints this.** The band top would
become M0-176 at 99, whose milestone is M3; `nextMilestone("M3")` is M4 and the
chain's own roadmap rows serve M4, not M3 - which is a DIFFERENT arrangement from
ADR 0021 decision (b)'s, where the excused top and the serving chain shared a
milestone. Whether `checkRoadmapBand`'s existence half holds under that shape is
a question to answer against `src/doctor/doctor.ts` BEFORE the enqueue, not
after. If it does not hold, the fix is the slot - put a chain row of M4 at the
top - and never a change to the gate.

### The chain

| slot | id | mint / raise / done | what it owes | what already exists |
|---|---|---|---|---|
| 99 | M0-176 | **raise in place**, 79 -> 99, gains `outranks_roadmap` | the producer that writes `~/.config/millwright/rate-limits.json` | the reader, the schema and the `budget.rate_limit` doctor line all landed with M3-06; `doctor` prints `skip ... nothing outside this repository has written one` |
| 98 | M0-110 | **raise in place**, 76 -> 98, gains `outranks_roadmap` | `millwright tick --trigger cron` and the task and dollar ceilings as flags, so the invocation section 12 specifies is legal at all | the row is filed, measured and argued; `tickCommand` (src/cli.ts) parses only `--run-id` and exits 78 on anything else |
| 97 | M4-01 | **mint** | the wrapper script itself: `set -Eeuo pipefail`, `umask 077`, explicit `PATH`, flock, both STOP files with a skip log, `timeout --signal=TERM --kill-after=30s`, `|| RC=$?` before `set -e` sees it, and the 0 / 75-is-success / re-exit rule | nothing. `ls scripts/` on 2026-09-08 printed eight `.mjs` files and no wrapper; M0-110's own text says "the wrapper itself does not exist in this repository at all" |
| 96 | M4-02 | **mint** | the systemd user unit and timer: the nine directives of section 12 (`TimeoutStartSec`, `TimeoutStopSec`, `MemoryMax`/`MemoryHigh`/`MemorySwapMax=0`, `TasksMax`, `CPUQuota`, `OOMPolicy=kill`, `OnFailure=`), `OnCalendar=*:0/15` with a persistent catch-up and `RandomizedDelaySec=30`, lingering and persistent journald. **Installation is operator-only** (discipline 6): the row delivers unit files and a packet, never an `systemctl enable` | nothing |
| 95 | M0-109 | **raise in place**, 77 -> 95, gains `outranks_roadmap` | the notifier's first caller: a circuit that opens invokes `[notify] command` once, bounded, from the event the tick already wrote | the row is filed and argued down to seven anti-criteria; `[notify] command` is a validated field read by nobody |
| 94 | M4-03 | **mint** | the two breakers of section 12 as DURABLE state: the infrastructure counter (auth errors, non-zero exits, 124/137, invalid JSON; trips at two or three in a row) and the gate counter (content rejections; trips at about five), the full opening list, `HALF_OPEN` admitting one canary and not the fleet, and reset-as-a-human-act-that-alerts | exactly one opening condition, in one place: `grep -rn 'type: "CIRCUIT_OPENED"' src/ --include=*.ts` printed one line on 2026-09-08 (src/controller/tick.ts:691, `reason: "base_not_green"`), and it refuses ONE tick rather than holding a breaker open. `grep -rn 'HALF_OPEN' src/ --include=*.ts` printed nothing |
| 93 | M4-04 | **mint** | the run manifest (millwright and claude CLI versions, models, `config_hash`, tick budgets) and the three-way `compat.json` verdict: below the minimum opens the circuit, above the tested set notifies, a lost capability is caught by doctor asserting capabilities against the installed CLI | `factory/compat.json` exists and `checkClaudeCli` (src/doctor/doctor.ts) reads its `claude_cli.minimum`; the manifest and the capability assertion do not exist |
| 92 | M4-05 | **mint** | the morning report: what an operator reads once a day instead of a journal | nothing under `src/report/` produces one. M0-109's own text reserves it: "the morning report, which is its own row of that milestone" |
| 91 | M4-06 | **mint** | the fault-injection suite completed to blueprint section 15's four categories | `ls test/faultinjection/*.test.ts \| wc -l` printed `6` on 2026-09-08, and all six are kill points. **Resource failures, git races and policy violations have no file at all** - and the policy category is the one that guards a worker, which is the category an unattended run needs most |
| 90 | M4-07 | **mint** | the soak ladder as state rather than prose: the six rungs, the measured threshold that promotes each, where the current rung is recorded, and what refuses a tick that runs above it. The DoD stops at rung 5 | nothing. `grep -l 'soak' factory/tasks/*.yaml` returns eleven files on 2026-09-08 and not one of them owns the ladder - every hit is a row citing a rung in passing |

Ten slots, of which three are raises and seven are mints, in a band with room for
fifteen. The gap between 90 and 85 is deliberate: M4-06 and M4-07 are the two
rows most likely to split under their own weight once someone writes their
`not_done_if` lines, and a chain with no room below it forces the split upward
into the band it has already assigned.

### The dependency edges, and the one that is not negotiable

M0-176 first, and this is the only ordering constraint the draft treats as
binding rather than convenient: **the clock must not start over a factory that
cannot read its weekly cap.** ADR 0023 section 1 states the reason and this
document does not restate it.

After that: M4-01 depends on M0-110 (a wrapper that passes flags the tick refuses
is worth nothing), M4-02 depends on M4-01 (a unit with no script to call), M4-03
and M0-109 are independent of each other but M0-109's value is the alert that
M4-03's openings produce, M4-04 is independent, and M4-07 depends on M4-01,
M4-02, M4-03 and M0-109 because rung 5 is precisely those four working together.
M4-06 is independent of all of them and can run at any point.

Per ADR 0021 decision (f), a chain row's `dependencies` name only rows inside the
chain; the findings a chain row happens to touch are not edges.

### The rows that are NOT part of the chain

Two test-only rows, banked from the blocks that found them, belong in the finding
band and not in the chain. Both were grepped against the backlog first:

| what | where it goes | why not a chain row |
|---|---|---|
| the concurrent case at the after-push-before-record seam (section 3 (e)) | a new finding row, low band. `grep -ln 'after the push' factory/tasks/*.yaml` printed only `M2-14.yaml` on 2026-09-08 - "The two kill points that can merge twice", which owns the SEQUENTIAL case and is DONE, so it is not an owner | it strengthens a proof that has already been accepted, and no rung of the ladder waits on it |
| the escalation case in the middle of a two-row pass (section 3 (f)) | a new finding row, low band. M3-10 and M3-11 are DONE and cannot own it; M0-146 is open but its subject is the room QUESTION, not this site's coverage | same |

The unmeasured room-staleness claim (section 3 (d)) is neither: it is a
measure-first note appended to M0-146, which this package files.

## 7. Two questions for the operator

**(1) `heavy_tests` and `opus` have no reader and `DESIGN.md` names no module for
one.** Section 16 names the four counters only as a parenthesis - "`concurrency`
(builders, heavy tests, senior-model slots, `integrations = 1`)" - and
`grep -n 'heavy_tests' DESIGN.md` printed nothing on 2026-09-08. So there is no
wiring to file: a spec would have to INVENT what a heavy-test slot bounds (the
verification ladder's expensive rungs?) and what a senior-model slot bounds (the
router's model choice?), and both are policy decisions rather than plumbing.
The three answers are: wire them under a stated meaning, delete them from
`CONCURRENCY_FIELDS` as decoration, or leave them declared and readerless with the
disclosure M3-10 already wrote. **This seat's recommendation is the third until
M4-03 exists**, because the first thing a heavy-test slot would bound is the
fault-injection suite, and section 6 puts that suite's completion at slot 91.

**(2) The post-merge smoke's price has grown twenty-fold in ten days.** Recorded
as an addendum to ADR 0020, which is where the question was first asked; it is
named here only so the M4 reading does not lose it, since a smoke that costs five
and a half minutes is a smoke that shapes every rung of the soak ladder.

## 8. What this ADR does NOT decide

- **Whether the M4 chain is minted.** Section 6 is a draft and mints nothing.
  The operator's word starts it; until then `queue --next` answers from the
  finding band.
- **Whether `cron-truth` starts.** Section 5 records that its trigger fired.
  Firing a trigger and starting a phase are different acts and ADR 0023 assigns
  the second to the operator.
- **Whether a paid live tick is authorised.** ADR 0023 section 2 puts that behind
  a spend sanction asked as its own question. Section 3 (b) states the gap and
  does not ask it.
- **The content of any row in section 6 beyond its slot, its verb and its
  evidence.** Each spec is the home of its own argument, and a decision document
  that carries a backlog acquires two homes for every row in it.

## 9. Addendum, 2026-09-08 - the operator says the word, and the chain is minted

Carrier #47, the same day this ADR was written. Section 6 was a draft that
minted nothing; this addendum records what turned it into rows and the two
things that changed between the draft and the mint.

**The operator's word**, given in the Claude application at about 12:50 on
2026-09-08, answering the foreman's dashboard question 1 verbatim:

> 1. Да, раз ты уверен что стоит

("1. Yes, since you are sure it is worth it.")

Question 1 was whether to mint the M4 chain of section 6 with M0-176 first. The
answer is the sanction, and every row of the chain carries it in its own file.

### (a) The M2-30 hazard, checked before the enqueue as section 6 demanded

Section 6 obliged whoever minted this chain to answer, against
`src/doctor/doctor.ts` and BEFORE the enqueue, whether `checkRoadmapBand`'s
existence half holds when the band top and the serving chain do not share a
milestone. The answer is that **the half holds, and it holds for a reason that
is not the one section 6 worried about.**

The existence half never required them to share a milestone. It takes the band
top's milestone AND the one after it, as a union:

```text
src/doctor/doctor.ts:992  const milestone = bandTop === null ? "" : bandTop.milestone;
src/doctor/doctor.ts:993  const after = nextMilestone(milestone);
src/doctor/doctor.ts:994  const wanted = after === null ? [milestone] : [milestone, after];
src/doctor/doctor.ts:995  const serving = roadmap.filter((row) => wanted.includes(row.milestone));
src/doctor/doctor.ts:996  const existenceBroken = serving.length === 0;
```

`roadmap` is the band filtered by `isRoadmapSpec` (`src/doctor/doctor.ts:875`,
the predicate imported from `src/controller/queue.ts:428`), and `nextMilestone`
answers the succession from `MILESTONES` (`src/controller/taskspec.ts:118` and
`:131`). So an M4 roadmap row satisfies a band top of M3 exactly as it satisfies
a band top of M4. The shape section 6 called different is legal by construction.

**The real hazard is one slot lower, and it is a dependency and not a
milestone.** The band is the open rows MINUS the picker's row-local refusals:

```text
src/doctor/doctor.ts:793  const ROW_LOCAL_REFUSALS: readonly PickRefusalReason[] = ["factory_admin", "dependency_not_done"];
```

and `dependency_not_done` is decided in `pickTasks` before any ordering
(`src/controller/dispatch.ts:540` opens "the row-local clauses, before any
ordering", the refusal is pushed at `:574`), so the ceiling never shields a row
from it. **A chain row whose dependency is still open is not in the band at
all.** M4-01, M4-02 and M4-07 all wait on open rows, so none of the three can
satisfy the existence half. What satisfies it is M4-03, M4-04, M4-05 and M4-06,
which have no dependencies. Had this chain been drawn as one strand hanging off
M0-176, `serving` would have been empty and `queue.roadmap` would have gone red
on a queue that had just been planned. That is the check the next chain owes,
and it is about edges rather than milestones.

No change was made to `src/doctor/**`. The slot was the thing under discussion
and the slot is what was set.

### (b) The chain moved one slot down, and why

Between the sanction and the enqueue the foreman re-measured the consumer's
acceptance path, at 13:21 on 2026-09-08, and found it closed:

```text
node dist/cli.js record-landed CR-01 --sha c461ece... --quality-attempts 1 ... --metric-effect direct
exit 78: a task in PAUSED is not on the linear chain, so this command cannot walk it to DONE
DESIGN.md section 6: only the chain states lead to DONE; a side state is the operator's to resolve
```

Shadow parks a held candidate in PAUSED by design (`HELD_CANDIDATE_LANDING`,
src/controller/shadow.ts), the state machine declares `PAUSED: ["READY",
"CANCELLED"]` (src/store/state-machine.ts:87), and no verb walks that edge -
`grep -rn resume src/cli.ts` printed nothing at f5715f6 on 2026-09-08. So a
candidate the operator accepts by hand can never be recorded, and the first
(private) consumer's own `queue --next` printed no selection and eleven refusals, every one waiting on
CR-01. That is M0-179's defect class for the other side edge.

**M0-190 was minted at 99, above this chain**, and the chain moved one slot down
in consequence: M0-176 98, M0-110 97, M4-01 96, M4-02 95, M0-109 94, M4-03 93,
M4-04 92, M4-05 91, M4-06 90, M4-07 89. The gap to 85 is four slots rather than
five. **Section 6's table is not rewritten** - it is the draft as it was
approved, and this paragraph is the one home of the shift.

### (c) Section 7's two questions

**Question 1, `heavy_tests` and `opus` with no reader**, was put to the operator
with this seat's recommendation and came back "3. На твоё усмотрение"
("3. At your discretion.") on 2026-09-08. The recommendation therefore stands as the decision: **the third
answer - the counters stay declared and readerless, with the disclosure M3-10
already wrote, until M4-03 exists.** The reason is unchanged and is section 7's
own: the first thing a heavy-test slot would bound is the fault-injection suite,
and this chain puts that suite's completion at slot 90.

**Question 2, the post-merge smoke**, was answered "4. Не возражаю"
("4. No objection.") and is filed
as M0-191 in the finding band, not in the chain. ADR 0020 section 4 (iv) stays
the home of the reading; the row is the home of the decision it owes.
