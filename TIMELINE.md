# Timeline

Every number on this page is printed by the command beside it. All of them were
re-run on **2026-09-14** against the private `main` at
`c8848460a30da990ce2eae793ee83f3a1f1dbfd7`, and none is copied from an upstream
document - a figure inherited from another file is an assumption wearing a
number's clothes (discipline 1, `PRINCIPLES.md`).

`<repo>` below stands for the private repository's checkout. The commands are run
with `git -C <repo> ... main`; they read history and write nothing.

## The shape of it

| Measurement | Value | Command |
|---|---|---|
| Commits on `main` | `934` | `git rev-list --count main` |
| Calendar days with a commit | `22` | `git log --format='%ad' --date=short main \| sort -u \| wc -l` |
| First commit | `2026-08-17` | `git log --format='%ad' --date=short --reverse main \| head -1` |
| Latest commit in this snapshot | `2026-09-12` | `git log --format='%ad' --date=short main \| head -1` |
| Landings (commits whose subject begins `merge: `) | `96` | `git log --format='%s' main \| grep -c '^merge: '` |
| ADRs | `27` | `git ls-tree --name-only main docs/decisions/ \| wc -l` |
| TaskSpecs in the queue | `277` | `git ls-tree --name-only main factory/tasks/ \| wc -l` |
| `.ts` files under `src/` | `118` | `git ls-tree -r --name-only main src/ \| grep -c '\.ts$'` |
| `.ts` files under `test/` | `73` | `git ls-tree -r --name-only main test/ \| grep -c '\.ts$'` |
| Lines of `DESIGN.md` | `795` | `git show main:DESIGN.md \| wc -l` |

Landings by milestone, from
`for p in M0 M1 M2 M3 M4 M5; do git log --format='%s' main | grep -c "^merge: $p-"; done`:

| Milestone | Landings |
|---|---|
| M0 | `48` |
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

The six milestone counts add to `96`, which is the landings row above: no landing
is outside a milestone, and none is counted twice.

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
```

Five dates between the first and the last commit are absent from that output
because no commit carries them: 2026-08-28, 2026-09-01, 2026-09-02, 2026-09-03
and 2026-09-09. Of the days that are present, the two lowest are 2026-08-31
(`6`), the day both public repositories were created, and 2026-08-27 (`10`), the
day the comparison run of ADR 0022 section 0 took. 2026-08-22 (`11`) carries the
first landing under the merge-commit convention:

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
first rung with no task run through it. The mechanisms are counted by their
landings; the DoD is not a count, and the ADR says so rather than letting the
seven landings stand in for it.

M5 has rows and two landings, which is what "M5 in progress" means here:

```sh
git ls-tree --name-only main factory/tasks/ | grep -c 'M5-'      # 7
git log --format='%s' main | grep -c '^merge: M5-'               # 2
```

Both re-run on 2026-09-14 at `c884846`.
