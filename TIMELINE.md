# Timeline

Every number on this page is printed by the command beside it. All of them were
re-run on **2026-08-31** against the private `main` at
`0871ab189b6d4a89134677450fbc1a9e973191c1`, and none is copied from an upstream
document - a figure inherited from another file is an assumption wearing a
number's clothes (discipline 1, `PRINCIPLES.md`).

`<repo>` below stands for the private repository's checkout. The commands are run
with `git -C <repo> ... main`; they read history and write nothing.

## The shape of it

| Measurement | Value | Command |
|---|---|---|
| Commits on `main` | `550` | `git rev-list --count main` |
| Calendar days with a commit | `13` | `git log --format='%ad' --date=short main \| sort -u \| wc -l` |
| First commit | `2026-08-17` | `git log --format='%ad' --date=short --reverse main \| head -1` |
| Latest commit in this snapshot | `2026-08-30` | `git log --format='%ad' --date=short main \| head -1` |
| Landings (commits whose subject begins `merge: `) | `51` | `git log --format='%s' main \| grep -c '^merge: '` |
| ADRs | `22` | `git ls-tree --name-only main docs/decisions/ \| wc -l` |
| TaskSpecs in the queue | `201` | `git ls-tree --name-only main factory/tasks/ \| wc -l` |
| `.ts` files under `src/` | `94` | `git ls-tree -r --name-only main src/ \| grep -c '\.ts$'` |
| `.ts` files under `test/` | `46` | `git ls-tree -r --name-only main test/ \| grep -c '\.ts$'` |
| Lines of `DESIGN.md` | `788` | `git show main:DESIGN.md \| wc -l` |

Landings by milestone, from
`for p in M0 M1 M2 M3; do git log --format='%s' main | grep -c "^merge: $p-"; done`:

| Milestone | Landings |
|---|---|
| M0 | `26` |
| M1 | `1` |
| M2 | `24` |
| M3 | `0` |

M1 shows one landing and not seven because most M1 blocks predate the
merge-commit convention: the first `merge: ` subject is dated 2026-08-22 (command
below), while the M1 work runs 2026-08-19 to 2026-08-23. So this table counts
landings, not blocks, and the earlier blocks are visible only as their `feat: `
commits in the last table on this page. The milestones themselves are in
`DESIGN.md` section 17.

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
  51 2026-08-30
```

2026-08-28 is absent from the output: no commit carries that date. Of the two
lowest days, 2026-08-27 (`10`) is the day the comparison run of ADR 0022 section 0
took, and 2026-08-22 (`11`) carries the first landing under the merge-commit
convention:

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
| 2026-08-30 | `merge: M2-16 - the factory can say that its own queue has stopped planning` | The last M2 landing in this snapshot. |
| 2026-08-30 | `chore: ADR 0021 - M3 gets a chain, and the band, marker and contracts it needs` | M3 is planned as an ordered chain. |
| 2026-08-30 | `chore: the M3 chain - eleven new rows for economics and parallelism` | The M3 queue is filed. |

## Where the snapshot stands

M2's last landing is dated 2026-08-30:

```sh
git log --format='%ad %s' --date=short main | grep '^\S* merge: M2-' | head -1
# 2026-08-30 merge: M2-16 - the factory can say that its own queue has stopped planning
```

M3 has rows and no landings, which is what "M3 in progress" means here:

```sh
git ls-tree --name-only main factory/tasks/ | grep -c 'M3-'      # 13
git log --format='%s' main | grep -c '^merge: M3-'               # 0
```

Both re-run on 2026-08-31 at `0871ab1`.
