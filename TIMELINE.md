# Timeline

Every number on this page is printed by the command beside it. All of them were
re-run on the afternoon of **2026-10-09** against the private `main` at
`886b98d68e24df0d38337343d23d204c6399f263`, but for the readings dated otherwise
where they appear, and none is copied from an upstream document - a figure
inherited from another file is an assumption wearing a number's clothes
(discipline 1, `PRINCIPLES.md`). The previous snapshot named `b2019e1`, the
morning of 2026-10-06. Nine commits have reached the private `main`
since (`git log --oneline b2019e1..main | wc -l` -> `9`), and two of them are
landings (`git log --format='%s' b2019e1..main | grep -c '^merge: '` -> `2`):
M0-215 and M0-114, both in the milestone table below. The other seven are
those two landings' own work, and none of the nine touches a TaskSpec, an ADR,
`DESIGN.md` or `PRINCIPLES.md`
(`git log --oneline b2019e1..main -- factory/tasks/ docs/decisions/ DESIGN.md PRINCIPLES.md | wc -l`
-> `0`). On the second repository the factory ran again on 2026-10-07 -
twenty-six ticks, four more merges, one task given up on and one split by the
operator - and no tick has run there since; its journal is read in the last
section.

`<repo>` below stands for the private repository's checkout. The commands are run
with `git -C <repo> ... main`; they read history and write nothing.

## The shape of it

| Measurement | Value | Command |
|---|---|---|
| Commits on `main` | `1373` | `git rev-list --count main` |
| Calendar days with a commit | `41` | `git log --format='%ad' --date=short main \| sort -u \| wc -l` |
| First commit | `2026-08-17` | `git log --format='%ad' --date=short --reverse main \| head -1` |
| Latest commit in this snapshot | `2026-10-07` | `git log --format='%ad' --date=short main \| head -1` |
| Landings (commits whose subject begins `merge: `) | `151` | `git log --format='%s' main \| grep -c '^merge: '` |
| ADRs | `48` | `git ls-tree --name-only main docs/decisions/ \| wc -l` |
| TaskSpecs in the queue | `356` | `git ls-tree --name-only main factory/tasks/ \| wc -l` |
| `.ts` files under `src/` | `128` | `git ls-tree -r --name-only main src/ \| grep -c '\.ts$'` |
| `.ts` files under `test/` | `82` | `git ls-tree -r --name-only main test/ \| grep -c '\.ts$'` |
| Lines of `DESIGN.md` | `830` | `git show main:DESIGN.md \| wc -l` |

Landings by milestone, from
`for p in M0 M1 M2 M3 M4 M5; do git log --format='%s' main | grep -c "^merge: $p-"; done`:

| Milestone | Landings |
|---|---|
| M0 | `99` |
| M1 | `1` |
| M2 | `25` |
| M3 | `13` |
| M4 | `7` |
| M5 | `6` |

M1 shows one landing and not seven because most M1 blocks predate the
merge-commit convention: the first `merge: ` subject is dated 2026-08-22 (command
below), while the M1 work runs 2026-08-19 to 2026-08-23. So this table counts
landings, not blocks, and the earlier blocks are visible only as their `feat: `
commits in the last table on this page. The milestones themselves are in
`DESIGN.md` section 17.

The six milestone counts add to `151`, which is the landings row above: no
landing is outside a milestone, and none is counted twice.

**M0 carries 99 landings, two more than at the previous snapshot; no other
count has moved** (M0 stood at `97` on the morning of 2026-10-06, with `149`
landings in total, and M5 at `6` then too; at `95` on the morning of
2026-10-05, with `144`; at `90` on the evening of 2026-10-03, with `138`; at
`89` on 2026-10-02, with `137`; at `58` on 2026-09-22, with `106`; at `57` on
2026-09-20, with `105`; at `48` on 2026-09-14, with `96`).
That is not M0 being re-opened: M0 is where this repository files the rows that
repair a mechanism a later milestone leans on, and fifty-one of the
fifty-five landings since 2026-09-12 are M0 rows, nearly all of that kind - the fix cycle, the tick's wall, the ladder's sight
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
`decisions/0043-the-two-retirement-rules-permanent-and-bound-to-the-holdout.md`);
and between the snapshots of 2026-10-03 and 2026-10-05, the notifier and
doctor's own invocation bounded on their whole process group, a carried
mutation measurement held to its count of carries, a verified row that no
integration claimed returned to the retry queue and the loop that opened
bounded per row
(`decisions/0046-the-m0-117-ledger-decided-and-the-spend-loop-row-above-the-line.md`),
and the objective split by model and by role, the measurement the operator put
before the builder's model is compared
(`decisions/0045-m0-222-behind-the-three-rt-08-waits-and-item-4-taken.md`).
The two M0 landings between the snapshots of 2026-10-05 and 2026-10-06 were of
another kind: comment and docstring lines only, sentences that earlier landings
had left describing what the code no longer does, now pointing at the symbols
that do it. The two since are of the first kind again: an attempt's cost
record, what the objective's `$` is summed from, now reads a budget overrun
from the reply envelope the CLI writes rather than from an exit code it never
printed - the move
`decisions/0033-the-budget-exit-the-design-names-is-not-the-clis.md` made for
the mechanism - and the doctor now walks every row's journal of state events
against the state the database holds.
The other four of the fifty-five are M5: M5-04, a written procedure rather
than a mechanism
(`decisions/0048-the-written-procedure-for-soak-rungs-3-4-and-5.md`), and
M5-05 to M5-07, the chain's last three rows, read in "Where the snapshot
stands". The last table on this page names forty-eight of the fifty-five.

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
     16 2026-10-03
     38 2026-10-04
     27 2026-10-05
     11 2026-10-06
      4 2026-10-07
```

Eleven dates between the first and the last commit are absent from that output
because no commit carries them: 2026-08-28, 2026-09-01, 2026-09-02, 2026-09-03,
2026-09-09, 2026-09-13, 2026-09-16, 2026-09-17, 2026-09-18, 2026-09-24 and
2026-09-25. The last row is a whole day: no commit has reached `main` since
M0-114's merge at `2026-10-07 03:04:38 +0300`
(`git log -1 --format='%ad' --date=iso main`), and the snapshot was taken on
the afternoon of 2026-10-09. 2026-10-06, a part of a day at the previous
snapshot, is whole now: to the six commits of one package of queue and decision
records it adds the five of M0-215's landing, the last of them its merge at
22:59.
2026-10-02 is a whole day: its last commit is the merge of M0-279 at 07:19
(`git log --format='%ad %s' --date=iso main | grep '^2026-10-02' | head -1`),
and the merges the gate made later that day, in the last section, are commits
of the second repository and not of this one. Of the whole days that are
present, the five lowest are 2026-10-07 (`4`), 2026-09-23 (`5`), 2026-08-31
(`6`), 2026-10-02 (`7`) and 2026-09-21 (`8`). The four commits of 2026-10-07
are the work and the merge of one landing, M0-114, in the last table;
2026-08-31 is the day both public repositories were created, and the seven
commits of 2026-10-02 are the work and the merges of the landings M0-278 and
M0-279 in the last table. Each of the other two is one package of queue and
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
| 2026-10-03 | `merge: M0-281 - the notifier and doctor's synchronous invocation are bounded on their whole process group` | The notifier and doctor's synchronous invocation now run under the same supervisor as a probe run since M0-276, and end with their whole process group at their bound. |
| 2026-10-04 | `merge: M0-283 - the carry cap holds a pass that measured from the start to the count, not to its one rate` | A carried mutation measurement that measured from its start is held to the cap of eight carries M0-278 set, and is no longer ended on its own rate alone. |
| 2026-10-04 | `merge: M0-117 - the reaper moves the row it used to report: READY_TO_INTEGRATE gets its RETRY_WAIT edge, and an outcome with no edge lands through RETRY_WAIT` | A verified row that no integration claimed returns to the retry queue instead of being reported on every sweep; the edge `DESIGN.md` section 6 gained for it is the operator's word ADR 0046 records. |
| 2026-10-04 | `merge: M0-222 - metrics prints the cost per verified merge per asked model and per role, beside totals that do not move` | The objective, `$` per verified merge, split by the model each seat asked for and by its role - the measurement ADR 0045 puts before the builder's model is compared. |
| 2026-10-04 | `merge: M0-286 - a refusal at the integration lock costs one infra retry, so a lock that stays held ends at the spec's ceiling` | The loop the new edge opened under a lock that stays held now ends at the row's own retry ceiling - the row ADR 0046 put above every roadmap row before any tick resumed. |
| 2026-10-05 | `merge: M5-04 - ADR 0048, the written procedure for soak rungs 3 to 5, its climb lists pinned to RUNGS` | The first M5 landing since 2026-09-12: the procedure a seat follows to put the soak ladder's third, fourth and fifth rungs to the operator - ADR 0048. It takes no promotion. |
| 2026-10-05 | `merge: M5-05 - the router's statistics read from the database, and a choice computed, recorded and printed, applied to no seat` | The learning router of `DESIGN.md` section 11, as a reading: the choice that minimises expected cost per verified merge is computed per task class from the attempts the database already holds, recorded and printed - and every seat still opens on the configured table until the operator's word says otherwise. |
| 2026-10-05 | `merge: M5-06 - the lens runs counted per (repo, task_class, lens), the lens statistic declared unavailable, and the declared order disclosed` | The lens order `DESIGN.md` section 8 says is retrained from the factory's own statistics: the lens runs are counted, the statistic is declared unavailable, since no recorded fact answers its numerator yet and its weight `w` is not defined, and the order in force is disclosed as the declared one. The walk and the gate are untouched. |
| 2026-10-05 | `merge: M5-07 - rung 6's threshold measured on rung 5 and withheld, what rung 6 admits stated in one place, and the operator packet that would arm a 24/7 clock` | The last row of the M5 chain. Rung 6, cron around the clock, stays refused: rung 5 carries its threshold, measured and printed and offering nothing while rung 6 is outside the definition of done, and arming the clock is a packet for the operator that no block ran. A row filed the same night corrects the packet's sentences that say more than the code, before the packet is put to him. |
| 2026-10-06 | `merge: M0-215 - an overrun is budget_spent by its subtype, and the token totals read modelUsage` | The record the objective's `$` is summed from: a worker run that hits its budget is recorded as spent budget from the subtype the CLI writes in its reply envelope, not from an exit code the CLI never printed, and the run's token totals are read from the CLI's per-model counters when every model served carries one - on the overrun captured live, the only place they were - which is the mechanism `decisions/0033-the-budget-exit-the-design-names-is-not-the-clis.md` moved. |
| 2026-10-07 | `merge: M0-114 - a state written with no event fails doctor, and M1-07's break is the one recorded known divergence` | The doctor walks every row's journal of state events against the state the database holds, and a state with no event behind it fails a required check; the one break the walk finds, on M1-07's row, is recorded as a known divergence rather than written over, so the journal stays append-only. |

## Where the snapshot stands

M4's last landing is dated 2026-09-11 and M5 is in progress:

```sh
git log --format='%ad %s' --date=short main | grep '^\S* merge: M4-' | head -1
# 2026-09-11 merge: M4-07 - the soak ladder is state, and a tick above its rung is refused
git log --format='%ad %s' --date=short main | grep '^\S* merge: M5-' | head -1
# 2026-10-05 merge: M5-07 - rung 6's threshold measured on rung 5 and withheld, what rung 6 admits stated in one place, and the operator packet that would arm a 24/7 clock
```

**Every M4 mechanism has landed and the milestone's own definition of done has
not been met**, which is the distinction ADR 0026 exists to make: `DESIGN.md`
section 17 ends M4 at "soak ladder through step 5", and the ladder stands at the
second of the six rungs section 18 names. On the second repository it was set to
rung 1 on 2026-09-14 and moved to rung 2 on 2026-10-02: from that repository's
working directory, `grep -c '"type":"LADDER_RUNG_CHANGED"' factory/state/events.jsonl`
printed `2` on 2026-10-09 - the setting, from rung 1 to rung 1, on 2026-09-14,
and the operator's promotion from rung 1 to rung 2 on 2026-10-02. The mechanisms
are counted by their landings; the DoD is not a count, and the ADR says so rather
than letting the seven landings stand in for it.

**The second rung was taken on 2026-10-02; the third was offered and not taken,
was not offered from RT-07's merge on 2026-10-03, and is offered again since
the ticks of 2026-10-07 - not by an overturned refusal undone, but by seven
new refusals, none of them read as overturned. It has not been taken.**
`DESIGN.md` section 18 promotes shadow "on an agreed number of tasks with zero
policy violations"; the first rung met that on ten tasks, as an earlier
snapshot of this page recorded, and the promotion was the operator's
(`decisions/0042-the-ten-task-programme-and-its-standing-tick-word.md`).
The rung alone merges nothing: that repository's `factory/millwright.toml` keeps
shadow mode under `[merge]` as a switch of its own, and the operator threw it the
same day in a separate commit there - `9eb3692`, `chore: merge shadow off - a
candidate that passes the gate is merged`. Each rung counts over its own window.
From the second repository's working directory on the afternoon of
2026-10-09, the factory's `ladder status` printed `2 (supervised auto-merge)`
for `rung` and `2026-10-02T07:12:08.357Z` for `since`, and over the window
since then `17` for `fact.tasks` - the seventeen tasks the gate has judged in
it - `0` for `fact.policy_violations` and for `fact.double_merges`, `11` for
`fact.gate_refusals`, `1` for `fact.overturned_refusals`,
`9.090909090909092` for `fact.false_block_percent` and `yes` for `offered`;
its `offer` line opens `rung 3 (two parallel builders) MAY be climbed by a
human` and lists the three clauses of rung 3 - at least ten tasks, no double
merge, a false-block rate of at most 10% - each of them met.
On the morning of 2026-10-06 the same command printed `12` for `fact.tasks`,
`4` for `fact.gate_refusals`, `25` for `fact.false_block_percent` and `no` for
`offered`; on the evening of 2026-10-03, after RT-07 merged, `3` for
`fact.gate_refusals` and `33.33333333333333` for `fact.false_block_percent`;
early that day, before RT-07 merged, `0` for `fact.overturned_refusals` and
`yes` for `offered` - readings earlier snapshots of this page record. The one
overturned refusal has been the same one since RT-07 merged: what moved the
rate is the divisor, eleven refusals now against four on 2026-10-06.
Rung 2 is supervised, and up to the afternoon of 2026-10-09 no tick on that
repository had been started by the timer, whose wrapper runs
`millwright tick --trigger cron` (`DESIGN.md` section 12):
`grep '"type":"RUN_STARTED"' factory/state/events.jsonl | grep -c '"trigger":"operator"'`
printed `105` there then, as many as
`grep -c '"type":"RUN_STARTED"' factory/state/events.jsonl`. The ladder reads a
refusal as overturned only when the task has merged and a row of that task
still carries the very candidate the gate refused - not when a fix cycle or a
fresh build replaced that candidate with the one that merged - so not every
refusal of a task that later merged is read as overturned. Of the eleven
refusals it counts, two are RT-07's, below, one is RT-02's, one is RT-13's, a
task refused once on the night of 2026-10-05 and merged the same night, one
each is RT-14's, RT-16's and RT-18's, and four are RT-17's, all seven dated
2026-10-07 and read further down. RT-02's was on condition 2 with no confirmed
finding: the factory's own record of it opens "nothing was measured false"
(`jq -r 'select(.seq==2060) | .payload.reason' factory/state/events.jsonl`), it
charged no quality attempt and briefed no builder, and the candidate the gate
then passed and the factory merged is a fresh build on the same base, not a fix
of the refused one (`git log -1 --format=%p e108475` and the same for `7e9c5aa`
both print `c83d135`). The ladder does not read it as overturned: its
`fact.overturned_refusals` was `0` early on 2026-10-03, with RT-02 merged since
the day before. RT-13's is the same case: condition 2 again, with no
confirmed finding. The record the factory wrote after it opens the same way
(`jq -r 'select(.seq==3200) | .payload.reason' factory/state/events.jsonl`),
the refusal went the infrastructure road and charged no quality attempt, and
the candidate the gate then passed and the factory merged is a fresh build on
the same base (`git log -1 --format=%p b64057a` and the same for the refused
`bc2b195` both print `07ab827`). RT-14's, RT-16's and RT-18's, of 2026-10-07,
are condition 2 again, each on one dimension the reviewer left unverified, and
each of the three tasks merged later that morning as a candidate other than
the refused one: the refused candidate a record names
(`jq -r 'select(.seq==3352) | .payload.candidate_sha' factory/state/events.jsonl`,
and the same for seq `3630` and `3997`) begins `7a754dd`, `e387af5` and
`1bbaaf1`, while each merge names as its second parent, the candidate
(`git log -1 --format=%p 8d854fd`, and the same for `fd186a6` and `dac3668`),
`b5fea00`, `62817e6` and `17b0683`. RT-17's four never reached a merge.
The one refusal the ladder reads as overturned is therefore one of RT-07's
two - one false block in eleven refusals, under the 10% the third rung allows.

M5 has seven rows and six landings, and every one of the seven rows is closed;
"M5 in progress" means here that its definition of done is not met:

```sh
git ls-tree --name-only main factory/tasks/ | grep -c 'M5-'      # 7
git log --format='%s' main | grep -c '^merge: M5-'               # 6
```

Both re-run on 2026-10-09 at `886b98d`. Of the seven rows, M5-03 - the chain's
central row, the one that runs the factory against the second repository -
was closed on 2026-10-04 as done, by an override the seat had recommended and
reads the operator's answer as taking, which cites the first merge the gate
made there, `c83d135`, as the one crossing it rests on. The closure is a record
in the private queue, not a commit, so it adds no landing to the count above:
in the private repository's checkout the factory's `status` printed
`landings.last_direct M5-03 at 2026-10-04T13:55:55.540Z` on 2026-10-09.
The last three rows landed on 2026-10-05, in the milestone table above, and
each lands a reading rather than a change: the router's choice is printed and
applied to no seat, the statistic the lens order would be recomputed from is
declared unavailable, and the clock around the day in M5's content column
waits on an operator packet that is corrected before it is put to him.
`DESIGN.md` section 17 ends M5 at "30-50 real tasks; router and lens order
recomputed from data", and that is not met: the lens order has not been
recomputed, and the second repository has seventeen verified merges, below,
against the thirty to fifty the line names. So M5's rows are closed and M5 is
not done - the distinction
`decisions/0026-m4-exit-and-the-ladder-nobody-climbed.md` drew for M4.

**Until 2026-10-05 no milestone landing was dated later than 2026-09-12: of
the fifty-five landings since, fifty-one are M0 and four are M5, M5-04 to
M5-07, all four dated 2026-10-05**
(`git log --format='%ad %s' --date=short main | grep '^\S* merge: ' | awk '$1 > "2026-09-12"' | wc -l`
-> `55`, and the same with `grep -c 'merge: M5-'` in place of `wc -l` -> `4`,
2026-10-09). That is the
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
this page will not move it earlier by counting them as M5. Of the four M5
landings among them, M5-04 adds no mechanism: it is the written procedure a
seat follows before it puts one of the ladder's next three rungs to the
operator (`decisions/0048-the-written-procedure-for-soak-rungs-3-4-and-5.md`).
M5-05, M5-06 and M5-07 add readings - a choice printed, a statistic declared
unavailable, a threshold measured - and none of them changes the model a seat
runs on, the order of the lenses or the rung a tick runs at. What the
same central row produced from 2026-10-02 on is in the second repository, not
in this one, and the rest of this section reads it there.

By the morning of 2026-10-05 the run on the second repository had reached
thirty-four gate verdicts, seventeen refusals and seventeen passes; the ticks
of 2026-10-07 added eleven, seven refusals and four passes, and no tick has run
there since. Every count of that repository's journal from here to the end of
this page was printed on the afternoon of 2026-10-09, at 15:16 +0300, in its
working directory, where the journal's last record is the enqueue that filed
the split read below: `tail -1 factory/state/events.jsonl | jq -r .ts` printed
`2026-10-07T09:32:02.189Z`. From that directory,
`grep -c '"type":"GATE_FAILED"' factory/state/events.jsonl` printed `24` and
`grep -c '"type":"GATE_PASSED"' factory/state/events.jsonl` printed `21`.
The first pass, dated 2026-09-29, is not counted here as the factory's first
success: `decisions/0039-the-factory-fixes-its-own-gate-first.md`
records it, as the seat reads it, as a false pass - on a candidate its own
spec's `not_done_if` forbade, which a hand-run found and the gate did not - and
in shadow mode it merged nothing. The operator's answer is in the same record:
on the second repository the factory does the work itself, and its gate is
fixed first. The four passes dated 2026-09-30 and 2026-10-01, the nine dated
2026-10-02, RT-07's of 2026-10-03, the two of the night of 2026-10-05,
which the journal stamps 2026-10-04 in UTC, and the four of 2026-10-07 are
each on a candidate whose held-out acceptance check ran in the gate phase and
passed; the first pass's spec declared none:

```sh
grep '"type":"GATE_PASSED"' factory/state/events.jsonl | grep -c 'holdout acceptance item(s) passed'     # 20
grep '"type":"GATE_PASSED"' factory/state/events.jsonl | grep -c 'declares no holdout acceptance item'  # 1
grep '"type":"GATE_PASSED"' factory/state/events.jsonl | grep -c '"ts":"2026-10-02'                     # 9
grep '"type":"GATE_PASSED"' factory/state/events.jsonl | grep -c '"ts":"2026-10-03'                     # 1
grep '"type":"GATE_PASSED"' factory/state/events.jsonl | grep -c '"ts":"2026-10-04'                     # 2
grep '"type":"GATE_PASSED"' factory/state/events.jsonl | grep -c '"ts":"2026-10-07'                     # 4
```

All six printed then. The five passes before 2026-10-02 merged nothing: shadow
mode parks a passed candidate. The sixteen since were merged, and the journal
tells the two kinds of merge apart by the reason it records:

```sh
grep -c '"type":"MERGED"' factory/state/events.jsonl                                  # 17
grep '"type":"MERGED"' factory/state/events.jsonl | grep -c '"reason":"bookkeeping'   # 1
grep '"type":"MERGED"' factory/state/events.jsonl | grep -c '"reason":"pushed '       # 16
```

The one "bookkeeping:" merge is the first task's, dated 2026-09-21, a landing
recorded by hand and not one the integrator made. The sixteen "pushed" ones are the
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
`grep -c '"type":"GATE_PASSED"' factory/state/events.jsonl` printed `0` on
2026-10-09, and so did
`grep '"type":"MERGED"' factory/state/events.jsonl | grep -c '"reason":"pushed '`:
its own landings are bootstrap blocks, recorded by hand, and none has reached
its `main` through its own gate.

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
that evening the factory's `queue` printed the new version `DONE`, and `metrics`
printed `0` for `failed_out` and `1` for `verified_merge_rate`. The operator
then deferred the repository's next task, RT-08, until four of the factory's
own rows had landed, with ticks there stopped meanwhile
(`decisions/0045-m0-222-behind-the-three-rt-08-waits-and-item-4-taken.md`).

The four landed on 2026-10-03 and 2026-10-04 (the milestone table above), and
the last two merges there followed. RT-08 - a GitHub Action wrapper that
resolves the range a pull request actually is - was reissued with a held-out
item and its action file moved out of `.github`, beside a new task, RT-13, for
four residuals of the earlier merges. On the night of 2026-10-05 eight ticks,
run one at a time on the operator's word and each accepted by the seat before
the next, merged both. In any clone,
`git log --first-parent --reverse --format='%h %ad %s' --date=short fcf6d3b..825cfbf`
prints three commits that carry no merge - the README note on RT-07, RT-08's
reissue (`1537a99`, `chore: reissue RT-08 - a holdout item, and the action
file out of .github`) and RT-13's task - and then:

```text
07ab827 2026-10-05 merge: RT-08 - A GitHub Action wrapper that resolves the range a pull request actually is
825cfbf 2026-10-05 merge: RT-13 - Four residuals - RT-03 reads the factory's merge trailer, and three evidence lines say what is true
```

`git rev-list --merges --count 9eb3692..825cfbf` prints `12`, and the `jq`
above with `2026-10-04` in place of `2026-10-02` prints `["pass"]` for both
gate passes - all seven conditions passed. RT-13 was refused once on the way,
one of the refusals the ladder counts, above. From that repository's working
directory on the morning of 2026-10-06 the factory's `queue` printed both
tasks `DONE` and `queue --next` printed `0 selected, 0 refused`: no task was
open there then. Its `main` then took a README note on the two merges,
`60ce4cd`.

Six new tasks followed, RT-14 to RT-19, each with a held-out item, filed in
one commit there - `d5f01a1`, `chore: RT-14 to RT-19 - six new tasks, each
with a holdout item` - and on the morning of 2026-10-07 twenty-six ticks, run
one at a time and each accepted by the seat before the next, judged five of
them: `grep '"type":"RUN_STARTED"' factory/state/events.jsonl | grep -c '"ts":"2026-10-07'`
prints `26` in that repository's working directory. Four were merged. In any
clone, `git log --first-parent --reverse --format='%h %ad %s' --date=short 825cfbf..15befcd`
prints the README note and the six tasks' commit, then:

```text
8d854fd 2026-10-07 merge: RT-14 - Lowered thresholds - a coverage minimum the range moves down or removes
b980ba9 2026-10-07 merge: RT-15 - The human output escapes control characters - a record cannot rewrite the terminal or the log that prints it
fd186a6 2026-10-07 merge: RT-16 - Snapshot refreshes - a stored expectation the range rewrites or deletes
dac3668 2026-10-07 merge: RT-18 - Dependency sources - a dependency the range adds or changes that does not come from the registry
```

and last `15befcd`, the commit of the split read below, which is that
repository's `main` at this snapshot.
`git rev-list --merges --count 9eb3692..dac3668` prints `16`, and the `jq`
above with `2026-10-07` in place of `2026-10-02` prints `["pass"]` for each of
the four gate passes - all seven conditions passed. Each of the four merges
names two parents, the base as fetched and the candidate, and carries the three
trailers; and each changes a file already in the repository -
`git diff --name-status <sha>^1 <sha>` marks `src/registry.ts` modified for
RT-14, RT-16 and RT-18, the one list every new check enters, beside the module
and the unit test each adds, and marks `src/cli.ts` and its test modified, and
nothing added, for RT-15, which adds no check and makes the human output escape
the control characters a record carries.

The fifth task the gate judged, RT-17, is a suite that runs the built command
end to end, and it was not merged. The gate refused it four times that morning, each time on
condition 2 alone and each time on the same entry of the reviewer's
unverified list: stage 5's test-strength measurement had not run, because the
candidate changes no TypeScript under `src/` that is not a test, so there was
nothing for it to measure. In the same four records the gate retired an entry
pointing at a smoke stage the task does not configure, under
`decisions/0038-the-unconfigured-stage-leaves-condition-2.md`, and counted this
one. No refusal confirmed a finding, so none charged a quality attempt; the
fourth came after the three infrastructure retries `budget.infra_retries`
grants were spent, and the controller gave the task up - the road
`decisions/0020-the-controller-may-give-up-on-one-task.md` opened:
`jq -r 'select(.seq==4045) | .payload.reason' factory/state/events.jsonl` opens
`nothing was measured false` and ends
`the factory gives up, INTEGRATING -> BLOCKED -> DEAD_LETTER`. From that
directory the factory's `metrics` prints `1` for `failed_out` and `0.9444` for
`verified_merge_rate`: the seventeen verified merges over themselves and the
one row that failed out.

The sixth, RT-19, never reached the gate: the commit that split it says the
candidate built to it was too large for the factory's mutation probe to finish
measuring within the passes the probe allows. On the operator's word it was
split into three - `15befcd`, `chore: RT-19 split - RT-20 plans a replay,
RT-21 reads the claims, RT-19 runs them` - and its first version was
cancelled. From that directory the factory's `queue` prints RT-19, RT-20 and
RT-21 `QUEUED`, and `queue --next` prints `1 selected, 2 refused`: RT-20 is
selected, RT-21 is refused a resource the same pass gives RT-20, and the new
RT-19 waits on both of them.

`DESIGN.md` section 1 makes `$` per verified merged task the objective, and on
the second repository sixteen of the seventeen verified merges it divides by
are the gate's. From that repository's working directory on the afternoon of
2026-10-09, the factory's `metrics` printed `17` for `verified_merges` - the
sixteen merges above and the first task's - and `1.747` for
`usd_and_tokens_per_verified_merge.cost_usd`, which is
`priced_verified_merges.usage.cost_usd`, `29.699095200000002`, over the
seventeen. That numerator is every attempt of the seventeen merged rows, the
refused ones included, and nothing else. Every worker run the journal prices,
with every cancelled version of a spec added, comes to more than twice as much
per verified merge. In the same directory at the same time:

```sh
node -e 'const fs=require("fs");let n=0,s=0;for(const l of fs.readFileSync("factory/state/events.jsonl","utf8").split("\n")){if(!l.includes("\"type\":\"AGENT_FINISHED\""))continue;const c=JSON.parse(l).payload.cost_usd;if(typeof c==="number"){n++;s+=c;}}console.log("AGENT_FINISHED priced",n,"sum",s.toFixed(4))'
# AGENT_FINISHED priced 161 sum 63.7193 - over the 17, 3.7482
```

Not every attempt record carries a cost. At the same time, the same journal held
these:

```sh
jq -s '[.[] | select(.type=="AGENT_FINISHED") | .payload.cost_usd // 0] | add' factory/state/events.jsonl             # 63.719292300000006; over the 17, 3.7482
jq -s '[.[] | select(.type=="AGENT_FINISHED")] | length' factory/state/events.jsonl                                   # 220
jq -s '[.[] | select(.type=="AGENT_FINISHED" and .payload.cost_usd == null)] | length' factory/state/events.jsonl  # 59
jq -c -s '[.[] | select(.type=="AGENT_FINISHED" and .payload.cost_usd == null) | .payload.role] | group_by(.) | map({(.[0]): length}) | add' factory/state/events.jsonl
# {"builder":4,"goal_evaluator":1,"resumed_seat":50,"reviewer":4}
```

All four printed then, in that repository's working directory. The 220
are attempt records. Of the 59 with no cost, 50 are seats resumed from a
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
