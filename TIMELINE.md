# Timeline

Every number on this page is printed by the command beside it. All of them were
re-run on **2026-10-02** against the private `main` at
`31f54917bb2ec0c5a59c58b56fdf5718c61be744`, and none is copied from an upstream
document - a figure inherited from another file is an assumption wearing a
number's clothes (discipline 1, `PRINCIPLES.md`).

`<repo>` below stands for the private repository's checkout. The commands are run
with `git -C <repo> ... main`; they read history and write nothing.

## The shape of it

| Measurement | Value | Command |
|---|---|---|
| Commits on `main` | `1277` | `git rev-list --count main` |
| Calendar days with a commit | `36` | `git log --format='%ad' --date=short main \| sort -u \| wc -l` |
| First commit | `2026-08-17` | `git log --format='%ad' --date=short --reverse main \| head -1` |
| Latest commit in this snapshot | `2026-10-02` | `git log --format='%ad' --date=short main \| head -1` |
| Landings (commits whose subject begins `merge: `) | `137` | `git log --format='%s' main \| grep -c '^merge: '` |
| ADRs | `43` | `git ls-tree --name-only main docs/decisions/ \| wc -l` |
| TaskSpecs in the queue | `347` | `git ls-tree --name-only main factory/tasks/ \| wc -l` |
| `.ts` files under `src/` | `124` | `git ls-tree -r --name-only main src/ \| grep -c '\.ts$'` |
| `.ts` files under `test/` | `77` | `git ls-tree -r --name-only main test/ \| grep -c '\.ts$'` |
| Lines of `DESIGN.md` | `801` | `git show main:DESIGN.md \| wc -l` |

Landings by milestone, from
`for p in M0 M1 M2 M3 M4 M5; do git log --format='%s' main | grep -c "^merge: $p-"; done`:

| Milestone | Landings |
|---|---|
| M0 | `89` |
| M1 | `1` |
| M2 | `25` |
| M3 | `13` |
| M4 | `7` |
| M5 | `2` |

M1 shows one landing and not seven because most M1 blocks predate the
merge-commit convention: the first `merge: ` subject is dated 2026-08-22 (command
below), while the M1 work runs 2026-08-19 to 2026-08-23. So this table counts
landings, not blocks, and the earlier blocks are visible only as their `feat: `
commits in the last table on this page. The milestones themselves are in
`DESIGN.md` section 17.

The six milestone counts add to `137`, which is the landings row above: no
landing is outside a milestone, and none is counted twice.

**M0 carries 89 landings and is again the only count that moved since the
previous snapshot** (it stood at `58` on 2026-09-22, with `106` landings in
total; at `57` on 2026-09-20, with `105`; at `48` on 2026-09-14, with `96`).
That is not M0 being re-opened: M0 is where this repository files the rows that
repair a mechanism a later milestone leans on, and all forty-one landings since
2026-09-12 are of that kind - the fix cycle, the tick's wall, the ladder's sight
of a gate verdict, one worker home per seat of a pass, the mutant ceiling inside
a tick, the base a pass builds on, the goal evaluator's reply, the debug mode the
operator asked for in the factory itself
(`decisions/0032-the-words-on-the-second-series-and-the-debug-mode.md`), and
since then the gate itself: what condition 2 counts, what condition 4 charges a
candidate for, holdout acceptance kept from the builder and run in the gate
phase, and a mutation measurement finished rather than judged
(`decisions/0035-the-temporary-answer-on-condition-2.md` to
`decisions/0039-the-factory-fixes-its-own-gate-first.md`); and last, a spec
that declares no held-out check refused where the consumer asks for one, and
condition 2's retirements bound to the held-out checks having run and passed
(`decisions/0041-the-holdout-rule-the-scripts-rule-and-the-ceiling-at-95.md`,
`decisions/0043-the-two-retirement-rules-permanent-and-bound-to-the-holdout.md`).
The last table on this page names thirty-six of the forty-one.

## Commits per day

From `git log --format='%ad' --date=short main | sort | uniq -c | sort -k2`:

```text
     30 2026-08-17
     21 2026-08-18
     38 2026-08-19
     52 2026-08-20
     32 2026-08-21
     11 2026-08-22
     50 2026-08-23
     21 2026-08-24
     97 2026-08-25
     69 2026-08-26
     10 2026-08-27
     68 2026-08-29
     54 2026-08-30
      6 2026-08-31
     30 2026-09-04
     33 2026-09-05
     12 2026-09-06
     72 2026-09-07
     73 2026-09-08
     52 2026-09-10
     31 2026-09-11
     72 2026-09-12
     16 2026-09-14
     24 2026-09-15
     24 2026-09-19
     38 2026-09-20
      8 2026-09-21
     33 2026-09-22
      5 2026-09-23
     15 2026-09-26
     39 2026-09-27
     33 2026-09-28
     33 2026-09-29
     38 2026-09-30
     30 2026-10-01
      7 2026-10-02
```

Eleven dates between the first and the last commit are absent from that output
because no commit carries them: 2026-08-28, 2026-09-01, 2026-09-02, 2026-09-03,
2026-09-09, 2026-09-13, 2026-09-16, 2026-09-17, 2026-09-18, 2026-09-24 and
2026-09-25. The last row is part of a day and not a whole one: the snapshot was
taken in the morning of 2026-10-02, so `2026-10-02` counts the hours before
it. Of the whole days that are present, the three lowest are 2026-09-23 (`5`),
2026-08-31 (`6`) and 2026-09-21 (`8`). 2026-08-31 is the day both public
repositories were created. Each of the other two is one package of queue and
decision records, committed within a single minute:

```sh
git log --format='%ad %s' --date=iso main | grep -c '^2026-09-23 12:04'   # 5
git log --format='%ad %s' --date=iso main | grep -c '^2026-09-21 23:40'   # 8
```

2026-08-22 (`11`) carries the first landing under the merge-commit convention:

```sh
git log --format='%ad %s' --date=short --reverse main | grep '^\S* merge: ' | head -1
# 2026-08-22 merge: M0-64 - the authorisation to spend is asked where the process starts
```

## The milestones, by the commit that carries each

Every row is a line of
`git log --format='%ad %s' --date=short --reverse main | grep -E '^\S+ (merge|feat): M'`,
quoted rather than summarised.

| Date | Commit subject | What it is |
|---|---|---|
| 2026-08-17 | `docs: import the founding research corpus` | Commit one. |
| 2026-08-17 | `feat: repo skeleton, CLI entry point and ASCII commit-msg gate` | The commit-message gate exists before anything it guards. |
| 2026-08-17 | `feat: M0-01 - TaskSpec validation, spec_hash and queue integrity` | The contract between human and factory becomes executable. |
| 2026-08-17 | `feat: M0-02 - SQLite store, numbered migrations, events.jsonl mirror` | State stops living in documents. |
| 2026-08-19 | `feat: M0-27 - a number carries its command and its date, enforced not asserted` | Discipline 1 stops being prose and becomes a check. |
| 2026-08-19 | `feat: M1-01 - DESIGN.md is ratified, and the agreement is a test` | The design is ratified; a test holds the document and the code to each other. |
| 2026-08-20 | `feat: M1-02 - a worktree pinned to a base SHA, in its own cgroup` | The isolation an agent runs inside. |
| 2026-08-20 | `feat: M1-03 - one headless claude -p worker behind one interface` | The first backend implementation. |
| 2026-08-21 | `feat: M1-05 - verification stages 0, 1 and 2, everything that costs zero tokens` | The cheap half of the verification DAG, first. |
| 2026-08-23 | `merge: M1-07 - shadow mode, and the first live task this factory ever built and verified` | First task built and verified by the factory, with merging switched off. |
| 2026-08-24 | `merge: M0-62 - the witness a hook can honestly be` | Four stops on one task, then the split - ADR 0017. |
| 2026-08-25 | `merge: M2-04 - the factory runs a task without an operator typing a command` | The tick picks, leases and runs a task unattended. |
| 2026-08-26 | `merge: M2-07 - seven machine conditions decide a merge, and each answers alone` | The merge gate. |
| 2026-08-26 | `merge: M2-09 - the only path into the base branch stops being an empty module` | The integrator. |
| 2026-08-26 | `merge: M2-10 - the base branch moves, and the row records what the remote said` | The push, and the compare-and-swap behind it. |
| 2026-08-29 | `merge: M2-12 - a first failure buys one fix cycle, and this factory now spends it` | The fix cycle becomes something the controller spends. |
| 2026-08-29 | `merge: M2-13 - the kill suite kills a controller, and the row it dropped stops being permanent` | Crash safety, tested by killing the controller. |
| 2026-08-30 | `merge: M2-16 - the factory can say that its own queue has stopped planning` | The last M2 landing before the 2026-08-31 snapshot; M2 rows kept landing after it. |
| 2026-08-30 | `chore: ADR 0021 - M3 gets a chain, and the band, marker and contracts it needs` | M3 is planned as an ordered chain. |
| 2026-08-30 | `chore: the M3 chain - eleven new rows for economics and parallelism` | The M3 queue is filed. |
| 2026-09-05 | `merge: M3-05 - effort escalates before the model, and a pass that cannot climb takes nothing` | The router: a retry buys thinking before it buys a bigger model. |
| 2026-09-05 | `merge: M3-06 - the weekly cap is readable, and a factory over it now stops with a reason` | The subscription cap becomes a number the controller can refuse on. |
| 2026-09-07 | `merge: M3-07 - a limit that arrives during a pass parks the factory, and it now reaches every seat and the hook the CLI actually calls` | A rate limit mid-pass parks the row instead of burning the tick. |
| 2026-09-07 | `merge: M2-28 - gate G3 refuses, because intake now knows which rows are open` | The last M2 landing: the third drift gate of ADR 0018 starts refusing. |
| 2026-09-08 | `merge: M3-10 - one pass takes what [concurrency] allows, and the sixth clause gets a number` | The conflict-aware scheduler takes more than one row per pass. |
| 2026-09-08 | `merge: M3-11 - two builders that pass a unit test, now proven not to collide` | The last M3 landing: two builders, no collision. |
| 2026-09-08 | `merge: M4-01 - the timer now has something to call` | The tick wrapper a scheduler can invoke. |
| 2026-09-08 | `merge: M4-02 - the systemd user unit, its timer, and the packet that installs them` | Unattended operation becomes an install packet for the operator. |
| 2026-09-10 | `merge: M4-03 - two durable breakers, and the one that is only left by a human` | Circuit breakers that survive the process that opened them. |
| 2026-09-11 | `merge: M4-05 - the morning report, and the tick sends it before it stops` | The unattended run reports, above the STOP gate. |
| 2026-09-11 | `merge: M4-07 - the soak ladder is state, and a tick above its rung is refused` | The last M4 landing: autonomy is a ladder with rungs, not a switch. |
| 2026-09-12 | `merge: M5-01 - millwright onboard, one entrance for pointing the factory at a repository` | One command points the factory at a repository that is not its own. |
| 2026-09-12 | `merge: M5-02 - no loading seam is owed, and the contract is configuration` | The consumer contract turns out to need configuration, not a plugin seam. |
| 2026-09-15 | `merge: M0-217 - a fix cycle the tick's wall cannot hold waits for the next pass, uncharged` | A bounded tick stops destroying the work it cannot finish. |
| 2026-09-20 | `merge: M0-224 - a gate refusal buys its fix cycle through INTEGRATING -> BUILDING, and the reaper is kept off the edge` | The edge the state machine had never declared - ADR 0028. |
| 2026-09-20 | `merge: M0-225 - a seat after the builder the tick's wall cannot hold is carried to the next pass over the same candidate` | The reviewer and the goal evaluator are carried across ticks instead of being paid for twice. |
| 2026-09-20 | `merge: M0-213 - the ladder names the act that opens its first window, counts a violation as a record it could not read, and finds a task under either spelling of its id` | The soak ladder can see a gate verdict, which is what its first rung counts. |
| 2026-09-22 | `merge: M0-231 - every seat of a pass runs in a home of its own` | One home per seat, not one per pass: what a seat leaves behind stops being input the next seat's tools act on. |
| 2026-09-22 | `merge: M0-232 - the ladder's policy clause sees a breach stage 1 caught` | The ladder's first rung counts a policy breach by the stage-1 rule it broke - the reading ADR 0030 records. |
| 2026-09-22 | `merge: M0-236 - the per-file mutant ceiling inside a tick is priced by the file's own baseline run` | A tick's gate had refused with its mutation run stopped by the ceiling at 2 of 45 mutants (ADR 0030); the ceiling is now priced per file. |
| 2026-09-22 | `merge: M0-239 - a pass builds on, and step 3 judges, the base fetched from origin` | A pass builds on the base branch as the remote holds it, not as a local copy last saw it. |
| 2026-09-26 | `merge: M0-241 - goal evaluator turn ceiling 10 -> 20 with its source` | Gate condition 6's evaluator gets twice the turns, with the figure's source beside it. |
| 2026-09-26 | `merge: M0-88 - the classifier reads structured_output and a markdown-wrapped result, and names the CLI's own ending` | A worker's reply is read where the CLI puts it. The two gate verdicts of that evening were the first in which condition 6 answered and passed - ADR 0032. |
| 2026-09-27 | `merge: M0-193 - a baseline walk leaves an attempt, keeps its rung output, and walks a checkout of the commit` | The first row of the debug mode (ADR 0032): the ladder measures a checkout of the commit it records, not the consumer's working tree, and keeps a red rung's output. |
| 2026-09-27 | `merge: M0-243 - millwright trace <run id> reads one run back from the store` | One run read back from the journal as a human view, instead of line by line by hand. |
| 2026-09-27 | `merge: M0-138 - the janitor reclaims expired trees under the runs directory` | A tick removes the factory's own run trees once they expire, instead of leaving them for a person to clear. |
| 2026-09-27 | `merge: M0-212 - each ladder rung keeps its duration and output file per run, and the sentence names both sources` | Every ladder run keeps its rungs' evidence in a directory of its own, so a later run no longer overwrites an earlier one's. |
| 2026-09-27 | `merge: M0-244 - a worker call keeps its own output in the seat home, and a switch lets it keep its transcript` | Part of the same debug mode: a worker call's raw output is kept by default, and its transcript only behind a switch that is off. |
| 2026-09-27 | `merge: M0-185 - no builder opens past the working wall, a walk the reviewer's guard stopped keeps its stages and its candidate, and the gate phase's wall stop is on the row` | A pass stops opening a builder it cannot finish inside the tick's wall, and a walk stopped before the reviewer keeps what it had measured. |
| 2026-09-27 | `merge: M0-202 - a merge files the new base's baseline from the walks it already ran` | After a merge the next tick finds the new base already measured, instead of refusing it as unmeasured. |
| 2026-09-28 | `merge: M0-245 - condition 2 retires a pointer at a stage or check that ran, marked temporary by ADR 0035` | The operator's temporary answer on gate condition 2, built: an unverified entry that points at a check which ran no longer blocks by itself. |
| 2026-09-28 | `merge: M0-253 - the reviewer's list is scoped to what the spec states, and a focused rung's head resolves` | The reviewer lists as unverified only what the spec asks for - the scope ADR 0036 marks temporary. |
| 2026-09-28 | `merge: M0-254 - the goal evaluator is shown the ladder's run of each command item and confirms a command item from it` | Gate condition 6's evaluator confirms a command item from the ladder's own run of it, where before it had no road to confirm one. |
| 2026-09-29 | `merge: M0-262 - condition 2 retires a pointer at stage 3 recorded with no smoke trigger, on the record's mark, under ADR 0038` | ADR 0038's one case, built: a pointer at a smoke stage no repository configured stops counting against the candidate. |
| 2026-09-29 | `merge: M0-257 - a fix cycle opens on its builder's share, and a fix walk the pass cannot hold goes to the next pass over the fix candidate` | ADR 0037's answer, built: the tick's wall stays, and a fix cycle's walk that does not fit is carried to the next pass. |
| 2026-09-29 | `merge: M0-263 - the reviewer's FORM rule asks for the head on a stage or a check recorded not run` | The reviewer is asked to point, in the form the gate reads, at a stage or check that measured nothing. |
| 2026-09-29 | `merge: M0-258 - millwright unblock releases a BLOCKED row under its quality ceiling` | The operator's verb that returns a blocked task to work, within the attempts its spec allows. |
| 2026-09-29 | `merge: M0-265 - condition 4 reads the workspace as it stood when the first verification seat opened` | The gate stops charging a candidate for files a verification seat left in its workspace - one of the false refusals ADR 0039 names. |
| 2026-09-30 | `merge: M0-59 - withhold holdout acceptance items from the builder's packet` | The builder no longer sees the acceptance items held out to judge its work. |
| 2026-09-30 | `merge: M0-266 - a mutation measurement its time ceiling stopped is carried to the next pass, not judged` | ADR 0039's rule, built: a mutation run its time budget cut is finished in a later pass instead of being read as a refusal. |
| 2026-09-30 | `merge: M0-131 - condition 1's holdout half answers from a run in the gate phase, and neither the seats nor a fix builder are shown a holdout item` | Holdout acceptance gets its runner: the held-out items run in the gate phase, out of sight of every seat and of a fix builder. |
| 2026-09-30 | `merge: M0-69 - read the guarded list from the consumer's policy, guard the manifest's scripts field, close four stage 1 holes, and pin each arm of the condition evaluator` | Stage 1, the zero-token lens every candidate crosses, reads its guarded paths from the consumer's policy and refuses a change to the manifest's scripts field. |
| 2026-09-30 | `merge: M0-267 - audit a fix candidate's tests against the refused candidate as well as the base, on every road a fix walk takes` | A fix builder can no longer get past the gate by deleting or weakening a test the refused candidate had added: stage 1 reads that change too. |
| 2026-10-01 | `merge: M0-275 - an advisory stage's survivor is no longer a confirmed finding` | A refusal whose only non-passing lines are an advisory mutation survivor and checks nobody could measure stops spending a quality attempt and a fix builder. |
| 2026-10-01 | `merge: M0-276 - a probe run past its bound ends with its whole process group, and a mutant run's bound is priced by its file's baseline` | A hung mutant run is ended with its whole process group at its bound, and each mutant's bound is priced from its own file's baseline run. |
| 2026-10-01 | `merge: M0-277 - the reviewer's scratch block names the fence's git subcommands and the repository's identity` | The reviewer is told what its fenced scratch repository lets it run - a cause of false refusals, by the recommendation ADR 0043 records. |
| 2026-10-01 | `merge: M0-272 - condition 1 refuses a spec that declares no holdout item where the consumer's policy asks, and the BLOCKED road names cancel first` | ADR 0041's holdout rule, built: where a consumer's policy asks for it, a spec with no held-out check is refused at condition 1, and the candidate is not charged for the spec's omission. |
| 2026-10-02 | `merge: M0-278 - a carried measurement's ceiling follows what its passes answer under a cap of eight, and a change of the time bounds alone resumes the record` | A mutation measurement carried across passes ends on what its passes actually answer, under a cap of eight, and a change of its time bounds alone no longer restarts it. |
| 2026-10-02 | `merge: M0-279 - condition 2 binds ADR 0035's and ADR 0038's retirements to the holdout, and the TEMPORARY marks leave src` | ADR 0043's word, built: an unverified entry either temporary rule would retire leaves condition 2's count only on a candidate whose held-out checks ran and passed. |

## Where the snapshot stands

M4's last landing is dated 2026-09-11 and M5 is in progress:

```sh
git log --format='%ad %s' --date=short main | grep '^\S* merge: M4-' | head -1
# 2026-09-11 merge: M4-07 - the soak ladder is state, and a tick above its rung is refused
git log --format='%ad %s' --date=short main | grep '^\S* merge: M5-' | head -1
# 2026-09-12 merge: M5-02 - no loading seam is owed, and the contract is configuration
```

**Every M4 mechanism has landed and the milestone's own definition of done has
not been met**, which is the distinction ADR 0026 exists to make: `DESIGN.md`
section 17 ends M4 at "soak ladder through step 5", and the ladder stands at its
first rung with no task promoted through it. On the second repository it was set
to rung 1 on 2026-09-14 and has not moved since: from that repository's working
directory, `grep -c '"type":"LADDER_RUNG_CHANGED"' factory/state/events.jsonl`
printed `1` on 2026-10-02, and that one event is the setting, from rung 1 to
rung 1, on 2026-09-14. The mechanisms are counted by their
landings; the DoD is not a count, and the ADR says so rather than letting the
seven landings stand in for it.

**The first rung's threshold is now met, and the climb is offered, not taken.**
`DESIGN.md` section 18 promotes shadow "on an agreed number of tasks with zero
policy violations". From the second repository's working directory, the
factory's `ladder status` printed `10` for `fact.tasks`, `met` for the clause
that `wants at least 10 ([ladder] tasks_per_rung)`, `0` for
`fact.policy_violations` and `yes` for `offered` on 2026-10-02. The next rung is
supervised auto-merge, one task per tick, and the promotion is the operator's
(`decisions/0042-the-ten-task-programme-and-its-standing-tick-word.md`). The
rung alone merges nothing: that repository's `factory/millwright.toml` says
under `[merge]` that "shadow mode is on by default and nothing is merged while
it is", and switching it off is a separate commit there, the operator's.

M5 has rows and two landings, which is what "M5 in progress" means here:

```sh
git ls-tree --name-only main factory/tasks/ | grep -c 'M5-'      # 7
git log --format='%s' main | grep -c '^merge: M5-'               # 2
```

Both re-run on 2026-10-02 at `31f5491`.

**No milestone landing is dated later than 2026-09-12, and the forty-one
landings since are all M0** (`git log --format='%ad %s' --date=short main | grep '^\S*
merge: ' | awk '$1 > "2026-09-12"' | wc -l` -> `41`, 2026-10-02). That is the
honest shape of the last twenty days: the M5 chain's central row runs the
factory against the second repository, and each attempt at it has returned a
defect in a mechanism M0 owns - the fix cycle a bounded tick could not hold, the
edge a gate refusal had no route through, the seats a wall killed after they
were paid for, the ladder's blindness to the verdict its first rung counts, the
single worker home every seat of a pass shared, a mutant ceiling that stopped a
mutation run at 2 of 45, a goal evaluator that ended without a reply the gate
could read, a ladder that measured the consumer's working tree instead of the
commit, a gate that charged a candidate for files its own verification seats
wrote, a mutation run its time budget cut and the gate read as a refusal,
holdout acceptance that nothing ran, an advisory survivor charged as a
confirmed finding, a hung mutant run that outlived its bound, and a gate that
passed a spec declaring no held-out check. Those are the landings above. The
milestone does not advance until they stop arriving, and this page will not
move it earlier by counting them as M5.

The run on the second repository has now reached eighteen gate verdicts:
thirteen refusals and five passes. From that repository's working directory,
`grep -c '"type":"GATE_FAILED"' factory/state/events.jsonl` printed `13` and
`grep -c '"type":"GATE_PASSED"' factory/state/events.jsonl` printed `5` on
2026-10-02. The first pass, dated 2026-09-29, is not counted here as the
factory's first success: `decisions/0039-the-factory-fixes-its-own-gate-first.md`
records it, as the seat reads it, as a false pass - on a candidate its own
spec's `not_done_if` forbade, which a hand-run found and the gate did not - and
in shadow mode it merged nothing. The operator's answer is in the same record:
on the second repository the factory does the work itself, and its gate is
fixed first. The four later passes, dated 2026-09-30 and 2026-10-01, are each
on a candidate whose held-out acceptance check ran in the gate phase and
passed; the first pass's spec declared none:

```sh
grep '"type":"GATE_PASSED"' factory/state/events.jsonl | grep -c 'holdout acceptance item(s) passed'     # 4
grep '"type":"GATE_PASSED"' factory/state/events.jsonl | grep -c 'declares no holdout acceptance item'  # 1
```

Both printed on 2026-10-02 in that repository's working directory. None of the
five reached its base branch: shadow mode parks a passed candidate, and
`grep -c '"type":"MERGED"' factory/state/events.jsonl` printed `1` there on
2026-10-02 - the first task's, dated 2026-09-21, whose reason opens
"bookkeeping:", a landing recorded by hand and not one the integrator made. The
ten-task programme the later passes ran under is
`decisions/0042-the-ten-task-programme-and-its-standing-tick-word.md`; the two
series of five ticks that reached the earlier verdicts are recorded, with their
commands, in `decisions/0031-the-word-on-the-series-and-the-word-on-the-models.md`
and `decisions/0032-the-words-on-the-second-series-and-the-debug-mode.md`.
