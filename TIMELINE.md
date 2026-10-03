# Timeline

Every number on this page is printed by the command beside it. All of them were
re-run on **2026-10-03** against the private `main` at
`1f0b09f93172e4fa709ae6ead59fb33e4e666958`, and none is copied from an upstream
document - a figure inherited from another file is an assumption wearing a
number's clothes (discipline 1, `PRINCIPLES.md`). The previous snapshot named
`31f5491`; one landing has reached the private `main` since, `merge: M0-136`,
in three commits (`git log --oneline 31f5491..main | wc -l` -> `3`), and the
rest of what moved is the run on the second repository, in the last section.

`<repo>` below stands for the private repository's checkout. The commands are run
with `git -C <repo> ... main`; they read history and write nothing.

## The shape of it

| Measurement | Value | Command |
|---|---|---|
| Commits on `main` | `1280` | `git rev-list --count main` |
| Calendar days with a commit | `37` | `git log --format='%ad' --date=short main \| sort -u \| wc -l` |
| First commit | `2026-08-17` | `git log --format='%ad' --date=short --reverse main \| head -1` |
| Latest commit in this snapshot | `2026-10-03` | `git log --format='%ad' --date=short main \| head -1` |
| Landings (commits whose subject begins `merge: `) | `138` | `git log --format='%s' main \| grep -c '^merge: '` |
| ADRs | `43` | `git ls-tree --name-only main docs/decisions/ \| wc -l` |
| TaskSpecs in the queue | `347` | `git ls-tree --name-only main factory/tasks/ \| wc -l` |
| `.ts` files under `src/` | `124` | `git ls-tree -r --name-only main src/ \| grep -c '\.ts$'` |
| `.ts` files under `test/` | `77` | `git ls-tree -r --name-only main test/ \| grep -c '\.ts$'` |
| Lines of `DESIGN.md` | `801` | `git show main:DESIGN.md \| wc -l` |

Landings by milestone, from
`for p in M0 M1 M2 M3 M4 M5; do git log --format='%s' main | grep -c "^merge: $p-"; done`:

| Milestone | Landings |
|---|---|
| M0 | `90` |
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

The six milestone counts add to `138`, which is the landings row above: no
landing is outside a milestone, and none is counted twice.

**M0 carries 90 landings and is again the only count that moved since the
previous snapshot** (it stood at `89` on 2026-10-02, with `137` landings in
total; at `58` on 2026-09-22, with `106`; at `57` on 2026-09-20, with `105`; at
`48` on 2026-09-14, with `96`).
That is not M0 being re-opened: M0 is where this repository files the rows that
repair a mechanism a later milestone leans on, and all forty-two landings since
2026-09-12 are of that kind - the fix cycle, the tick's wall, the ladder's sight
of a gate verdict, one worker home per seat of a pass, the mutant ceiling inside
a tick, the base a pass builds on, the goal evaluator's reply, the debug mode the
operator asked for in the factory itself
(`decisions/0032-the-words-on-the-second-series-and-the-debug-mode.md`), and
since then the gate itself: what condition 2 counts, what condition 4 charges a
candidate for, holdout acceptance kept from the builder and run in the gate
phase, and a mutation measurement finished rather than judged
(`decisions/0035-the-temporary-answer-on-condition-2.md` to
`decisions/0039-the-factory-fixes-its-own-gate-first.md`); and then a spec
that declares no held-out check refused where the consumer asks for one, and
condition 2's retirements bound to the held-out checks having run and passed
(`decisions/0041-the-holdout-rule-the-scripts-rule-and-the-ceiling-at-95.md`,
`decisions/0043-the-two-retirement-rules-permanent-and-bound-to-the-holdout.md`).
The last table on this page names thirty-seven of the forty-two.

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
      3 2026-10-03
```

Eleven dates between the first and the last commit are absent from that output
because no commit carries them: 2026-08-28, 2026-09-01, 2026-09-02, 2026-09-03,
2026-09-09, 2026-09-13, 2026-09-16, 2026-09-17, 2026-09-18, 2026-09-24 and
2026-09-25. The last row is part of a day and not a whole one: the snapshot was
taken in the morning of 2026-10-03, so `2026-10-03` counts the hours before it -
the three commits of M0-136's landing, the last of them at
`2026-10-03 03:41:17 +0300` (`git log -1 --format='%ad' --date=iso main`).
2026-10-02 is a whole day: its last commit is the merge of M0-279 at 07:19
(`git log --format='%ad %s' --date=iso main | grep '^2026-10-02' | head -1`),
and the merges the gate made later that day, in the last section, are commits
of the second repository and not of this one. Of the whole days that are
present, the four lowest are 2026-09-23 (`5`), 2026-08-31 (`6`), 2026-10-02
(`7`) and 2026-09-21 (`8`). 2026-08-31 is the day both public repositories were
created, and the seven commits of 2026-10-02 are the work and the merges of the
landings M0-278 and M0-279 in the last table. Each of the other two is one
package of queue and decision records, committed within a single minute:

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

Every row is a line of `git log --format='%ad %s' --date=short --reverse main`,
quoted rather than summarised. All but four are lines that
`grep -E '^\S+ (merge|feat): M'` keeps of it; the four are commit one, the
skeleton, and the two `chore:` commits that planned and filed the M3 chain.

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
| 2026-10-03 | `merge: M0-136 - doctor reads the base branch as origin's remote-tracking ref, so the factory's own landing no longer turns queue.landings and checks.baseline red` | The doctor reads the base branch at origin, where a pass has read it since M0-239, so a landing the factory pushed no longer reads as two red checks. |

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
section 17 ends M4 at "soak ladder through step 5", and the ladder stands at the
second of the six rungs section 18 names. On the second repository it was set to
rung 1 on 2026-09-14 and moved to rung 2 on 2026-10-02: from that repository's
working directory, `grep -c '"type":"LADDER_RUNG_CHANGED"' factory/state/events.jsonl`
printed `2` on 2026-10-03 - the setting, from rung 1 to rung 1, on 2026-09-14,
and the operator's promotion from rung 1 to rung 2 on 2026-10-02. The mechanisms
are counted by their landings; the DoD is not a count, and the ADR says so rather
than letting the seven landings stand in for it.

**The second rung was taken on 2026-10-02; the third was offered and not taken,
and since RT-07's merge on 2026-10-03 it is not offered.**
`DESIGN.md` section 18 promotes shadow "on an agreed number of tasks with zero
policy violations"; the first rung met that on ten tasks, as the previous
snapshot of this page recorded, and the promotion was the operator's
(`decisions/0042-the-ten-task-programme-and-its-standing-tick-word.md`).
The rung alone merges nothing: that repository's `factory/millwright.toml` keeps
shadow mode under `[merge]` as a switch of its own, and the operator threw it the
same day in a separate commit there - `9eb3692`, `chore: merge shadow off - a
candidate that passes the gate is merged`. Each rung counts over its own window.
From the second repository's working directory early on 2026-10-03, the
factory's `ladder status` printed `2 (supervised auto-merge)` for `rung` and
`2026-10-02T07:12:08.357Z` for `since`, and over the window since then `10` for
`fact.tasks` - the ten tasks the gate judged that day - `0` for
`fact.policy_violations` and for `fact.double_merges`, `3` for
`fact.gate_refusals`, `0` for `fact.overturned_refusals`, and `yes` for
`offered`: rung 3, two parallel builders, could be climbed, its three clauses -
at least ten tasks, no double merge, a false-block rate of at most 10% - each
`met`. It was not taken. At 13:50 +0300 the same day, after RT-07 merged, the same
`ladder status` printed `10` for `fact.tasks`, `0` for `fact.policy_violations`
and for `fact.double_merges` and `3` for `fact.gate_refusals` as before, but `1`
for `fact.overturned_refusals`, `33.33333333333333` for
`fact.false_block_percent` and `no` for `offered`; its `offer` line lists the
three clauses, and the one that fails is
`false_block_rate 33.33333333333333 (at most 10% ([ladder] max_false_block_percent))`.
Rung 2 is supervised, and up to early on 2026-10-03 no tick on that repository
had been started by the timer, whose wrapper runs
`millwright tick --trigger cron` (`DESIGN.md` section 12):
`grep '"type":"RUN_STARTED"' factory/state/events.jsonl | grep -c '"trigger":"operator"'`
printed `69` there then, as many as
`grep -c '"type":"RUN_STARTED"' factory/state/events.jsonl`. The ladder reads a
refusal as overturned only once the refused task has merged, and not every such
refusal. Of the three refusals it counts, two are RT-07's, below, and one is
RT-02's, on condition 2 with no confirmed
finding: the factory's own record of it opens "nothing was measured false"
(`jq -r 'select(.seq==2060) | .payload.reason' factory/state/events.jsonl`), it
charged no quality attempt and briefed no builder, and the candidate the gate
then passed and the factory merged is a fresh build on the same base, not a fix
of the refused one (`git log -1 --format=%p e108475` and the same for `7e9c5aa`
both print `c83d135`). The ladder does not read it as overturned: its
`fact.overturned_refusals` was `0` early on 2026-10-03, with RT-02 merged since
the day before. The one refusal it reads as overturned since RT-07's merge is
therefore one of RT-07's two - one false block in three refusals, over the 10%
the third rung allows.

M5 has rows and two landings, which is what "M5 in progress" means here:

```sh
git ls-tree --name-only main factory/tasks/ | grep -c 'M5-'      # 7
git log --format='%s' main | grep -c '^merge: M5-'               # 2
```

Both re-run on 2026-10-03 at `1f0b09f`.

**No milestone landing is dated later than 2026-09-12, and the forty-two
landings since are all M0** (`git log --format='%ad %s' --date=short main | grep '^\S*
merge: ' | awk '$1 > "2026-09-12"' | wc -l` -> `42`, 2026-10-03). That is the
honest shape of the weeks since 2026-09-12: the M5 chain's central row runs the
factory against the second repository, and until 2026-10-02 each attempt at it
returned a defect in a mechanism M0 owns - the fix cycle a bounded tick
could not hold, the edge a gate refusal had no route through, the seats a wall
killed after they were paid for, the ladder's blindness to the verdict its first
rung counts, the single worker home every seat of a pass shared, a mutant
ceiling that stopped a mutation run at 2 of 45, a goal evaluator that ended
without a reply the gate could read, a ladder that measured the consumer's
working tree instead of the commit, a gate that charged a candidate for files
its own verification seats wrote, a mutation run its time budget cut and the
gate read as a refusal, holdout acceptance that nothing ran, an advisory
survivor charged as a confirmed finding, a hung mutant run that outlived its
bound, and a gate that passed a spec declaring no held-out check. Those are the
landings above. The milestone does not advance until they stop arriving, and
this page will not move it earlier by counting them as M5. What the same central
row produced later on 2026-10-02 is in the second repository, not in this one,
and the rest of this section reads it there.

Early on 2026-10-03, before RT-07 was reissued, the run on the second repository
had reached thirty gate verdicts: sixteen refusals and fourteen passes. Every
journal count from here up to the paragraphs on RT-07 was printed then, and what
RT-07's merge changed is read at 13:50 +0300, in those paragraphs and the one
after them. From that repository's working directory,
`grep -c '"type":"GATE_FAILED"' factory/state/events.jsonl` printed `16` and
`grep -c '"type":"GATE_PASSED"' factory/state/events.jsonl` printed `14` on
2026-10-03. The first pass, dated 2026-09-29, is not counted here as the
factory's first success: `decisions/0039-the-factory-fixes-its-own-gate-first.md`
records it, as the seat reads it, as a false pass - on a candidate its own
spec's `not_done_if` forbade, which a hand-run found and the gate did not - and
in shadow mode it merged nothing. The operator's answer is in the same record:
on the second repository the factory does the work itself, and its gate is
fixed first. The four passes dated 2026-09-30 and 2026-10-01 and the nine dated
2026-10-02 are each on a candidate whose held-out acceptance check ran in the
gate phase and passed; the first pass's spec declared none:

```sh
grep '"type":"GATE_PASSED"' factory/state/events.jsonl | grep -c 'holdout acceptance item(s) passed'     # 13
grep '"type":"GATE_PASSED"' factory/state/events.jsonl | grep -c 'declares no holdout acceptance item'  # 1
grep '"type":"GATE_PASSED"' factory/state/events.jsonl | grep -c '"ts":"2026-10-02'                     # 9
```

All three printed on 2026-10-03 in that repository's working directory. The five
passes before 2026-10-02 merged nothing: shadow mode parks a passed candidate.
The nine of 2026-10-02 were merged, and the journal tells the two kinds of
merge apart by the reason it records:

```sh
grep -c '"type":"MERGED"' factory/state/events.jsonl                                  # 10
grep '"type":"MERGED"' factory/state/events.jsonl | grep -c '"reason":"bookkeeping'   # 1
grep '"type":"MERGED"' factory/state/events.jsonl | grep -c '"reason":"pushed '       # 9
```

The one "bookkeeping:" merge is the first task's, dated 2026-09-21, a landing
recorded by hand and not one the integrator made. The nine "pushed" ones are the
integrator's: for each, it merged the candidate onto the base it had just
fetched, ran the merge-sensitive checks again on the result and pushed it as a
fast-forward. They are public. In any clone of the second repository, from the
commit that switched shadow mode off to the ninth merge,
`git log --first-parent --reverse --format='%h %ad %s' --date=short 9eb3692..8338b5a`
prints:

```text
c83d135 2026-10-02 merge: RT-10 - Portable paths - no name the range introduces breaks a checkout on another system
830571a 2026-10-02 merge: RT-02 - The measurement rule over commit bodies and changed documentation
5453fba 2026-10-02 merge: RT-03 - Trailer check - a landing says which task it closes, in a machine-readable line
b07c7f8 2026-10-02 merge: RT-04 - Weakened-tests detector - the suite got greener and nothing got better
df26ebd 2026-10-02 merge: RT-05 - Stray files - what the range added that nobody meant to keep
9d1c227 2026-10-02 merge: RT-06 - Lockfile drift - the manifest and the lockfile stopped agreeing
fc7c857 2026-10-02 merge: RT-09 - Conflict markers - the lines a range adds hold no leftover merge conflict
376bd35 2026-10-02 merge: RT-11 - Symlinks - no link the range adds or changes points outside the repository
8338b5a 2026-10-02 merge: RT-12 - Large blobs - what the range adds to the history stays under a stated size
```

For each of the nine, `git log -1 --format=%p <sha>` names two parents, the base
as fetched and then the candidate; `git diff --name-status <sha>^1 <sha>` lists
two added files and nothing else, one check and its unit test; and the commit
body carries the three trailers `DESIGN.md` section 10 names. In the journal,
`jq -c 'select(.type=="GATE_PASSED" and (.ts|startswith("2026-10-02"))) | [.payload.conditions[].status] | unique' factory/state/events.jsonl`
prints `["pass"]` for each of the nine gate passes: all seven conditions passed.
They are the first merges the factory's gate has made. In the private
repository's working directory,
`grep -c '"type":"GATE_PASSED"' factory/state/events.jsonl` prints `0`, and so
does `grep '"type":"MERGED"' factory/state/events.jsonl | grep -c '"reason":"pushed '`:
its own landings are bootstrap blocks, recorded by hand.

The tenth task the gate judged that day, RT-07, was not merged that day. Its
subject is the CLI's single entry point, and it is the one task of the ten whose candidate
changes a file already in the repository rather than only adding its own: in
that repository's checkout, `git diff --name-status 8338b5a 482b9d3` marks
`package.json` modified (`M`) beside four added files (`A`). The gate refused
it twice that evening
(`grep '"type":"GATE_FAILED"' factory/state/events.jsonl | grep '"ts":"2026-10-02' | grep -c '"task_id":"RT-07"'`
prints `2`), both times on its held-out acceptance check alone: in both
refusals the ladder, the reviewer's verdict, the test-change audit, the bounds,
the measurement, the goal evaluator and the integration evidence passed, and
condition 2 read `error` only because a held-out item had failed, the binding
`decisions/0043-the-two-retirement-rules-permanent-and-bound-to-the-holdout.md`
records. Between the two, the fix cycle repaired a defect the first refusal had
found, and the reviewer had passed both candidates. Both refusals ran on the
same base, the ninth merge: in any clone, no commit follows `8338b5a` on
`main`'s first-parent line until one dated the next morning -
`git log --first-parent --format='%h %ci' -2 fd4e6fb` prints
`fd4e6fb 2026-10-03 09:46:20 +0300` and `8338b5a 2026-10-02 21:43:58 +0300` -
and in that repository's checkout the two integration commits, each a refused
candidate merged onto the base and neither ever pushed, name `8338b5a` as
their first parent:
`git log -1 --format='%h %p %ci' b06a106` prints
`b06a106 8338b5a 776c1ef 2026-10-02 21:51:45 +0300`, and the same for `596e1d9`
prints `596e1d9 8338b5a 482b9d3 2026-10-02 22:00:02 +0300`. The held-out check was
written when the base held a single check (`git ls-tree --name-only 8a76f79 src/`
in a clone of the second repository prints `src/commit-range.ts` and
`src/index.ts`), and it no longer fits the ten checks of `8338b5a`
(`git ls-tree --name-only 8338b5a src/ | grep -vc index.ts` prints `10`), so the
seat reads the check as stale at both refusals, not only at the second: the
first candidate also carried the defect the fix cycle repaired, and the second
was refused by the stale check alone. That reading rests on the check's output,
which is not published; on 2026-10-03 the seat re-ran a copy of the check over
the second candidate, which reproduced the refusal, and a repaired copy passed it
while still refusing the first candidate's defect.

The operator then cancelled that version of the task and reissued it with the
held-out check repaired outside the repository - `a355722` there, `chore:
reissue RT-07 - its holdout was stale, not its last candidate` - and on
2026-10-03 the factory rebuilt it, the gate passed it and the factory merged
it, the tenth merge: in any clone,
`git log -1 --format='%h %ci %p' fcf6d3b` prints
`fcf6d3b 2026-10-03 13:46:11 +0300 a355722 231fb30`, and
`git rev-list --merges --count 9eb3692..fcf6d3b` prints `10`. The command that
runs the checks is on that repository's `main` now. From its working directory
at 13:50 the factory's `queue` printed the new version `DONE`, and `metrics`
printed `0` for `failed_out` and `1` for `verified_merge_rate`.

`DESIGN.md` section 1 makes `$` per verified merged task the objective, and on
the second repository ten of the eleven verified merges it divides by are the
gate's. From that repository's working directory at 13:50 on 2026-10-03, after
RT-07's merge, the factory's `metrics` printed `11` for `verified_merges` - the
ten merges above and the first task's - and `1.7906` for
`usd_and_tokens_per_verified_merge.cost_usd`, which is
`priced_verified_merges.usage.cost_usd`, `19.6967615`, over the eleven. That
numerator is every attempt of the eleven merged rows, the refused ones included,
and nothing else. Every worker run the journal prices, with every cancelled
version of a spec added, comes to more than twice as much per verified merge.
In the same directory at the same minute:

```sh
node -e 'const fs=require("fs");let n=0,s=0;for(const l of fs.readFileSync("factory/state/events.jsonl","utf8").split("\n")){if(!l.includes("\"type\":\"AGENT_FINISHED\""))continue;const c=JSON.parse(l).payload.cost_usd;if(typeof c==="number"){n++;s+=c;}}console.log("AGENT_FINISHED priced",n,"sum",s.toFixed(4))'
# AGENT_FINISHED priced 114 sum 49.3092 - over the 11, 4.48
```

Not every attempt record carries a cost. Early on 2026-10-03, before RT-07 was
reissued, when `metrics` printed `10` and `1.8779`, the same journal held these:

```sh
jq -s '[.[] | select(.type=="AGENT_FINISHED") | .payload.cost_usd // 0] | add' factory/state/events.jsonl             # 48.39120730000001; over the 10, 4.84
jq -s '[.[] | select(.type=="AGENT_FINISHED")] | length' factory/state/events.jsonl                                   # 150
jq -s '[.[] | select(.type=="AGENT_FINISHED" and .payload.cost_usd == null)] | length' factory/state/events.jsonl  # 39
jq -c -s '[.[] | select(.type=="AGENT_FINISHED" and .payload.cost_usd == null) | .payload.role] | group_by(.) | map({(.[0]): length}) | add' factory/state/events.jsonl
# {"builder":4,"goal_evaluator":1,"resumed_seat":30,"reviewer":4}
```

All four printed then, in that repository's working directory. The 150
are attempt records. Of the 39 with no cost, 30 are seats resumed from a
carried reply, on which no worker is called, and 9 are worker runs that a
crash, a stall or a timeout ended before a cost was recorded - so both figures
are lower bounds. Both are the price the CLI reports for its runs, not a bill:
the workers authenticate with a subscription (`DESIGN.md` section 13).

The ten-task programme behind the later passes is
`decisions/0042-the-ten-task-programme-and-its-standing-tick-word.md`, whose
standing word covered ticks at rung 1 and which left the move to rung 2 to the
operator; the two
series of five ticks that reached the earlier verdicts are recorded, with their
commands, in `decisions/0031-the-word-on-the-series-and-the-word-on-the-models.md`
and `decisions/0032-the-words-on-the-second-series-and-the-debug-mode.md`.
