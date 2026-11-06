# autonomous-coding-factory

The design and the operating record of an autonomous coding factory - internally
codenamed **Millwright**.

> A millwright builds and maintains the machines; it does not stand at them.

## What it is

A deterministic controller drives isolated headless coding agents. In goes a queue
of task specifications; out comes code that has been verified, gated and merged
into the base branch of a consumer repository - unattended, on a schedule.

The controller owns everything that must be repeatable, and none of it is asked of
a model:

- **queue** - one task is one YAML file with an outcome, machine-checkable
  acceptance items, anti-criteria, path scope, risk and a hard budget;
- **lease** - one task, one holder, one attempt at a time, with a heartbeat and a
  reaper for the holder that dies;
- **worktree** - each attempt runs in a fresh worktree pinned to a base SHA,
  inside an OS-level fence rather than a prompt asking for good behaviour;
- **verification DAG** - five stages, ordered so that everything costing zero
  tokens runs before an LLM is asked anything, and the stage with the highest
  historical rejection rate runs first and alone;
- **merge gate** - seven machine conditions, each answering on its own, deciding
  whether a candidate reaches the base branch;
- **integrator** - merge the candidate onto a freshly fetched base with
  `git merge --no-ff`, re-measure on that integration SHA, push it as a
  fast-forward of the remote branch, never `--force`.

The objective function is **`$` per verified merged task**, not tokens saved and
not tasks attempted. `DESIGN.md` section 1 is the home of that definition and of
the non-goals it excludes.

## Status

**At a glance, measured on 2026-11-05, and the npm line on 2026-11-06.** One
value a line, each with the command that prints it; the derivation is below
and in `TIMELINE.md`.

- **The factory's own landings: over two hundred** - `237` on the private
  `main`: `git log --format='%s' main | grep -c '^merge: '`.
- **Merges its gate made into the public second repository: over ninety** -
  `93`, in any clone of it: `git rev-list --merges --count 9eb3692..837c291`.
- **Of those, measured `passed` again after they landed: over forty** - `41`,
  past the forty that repository's roadmap set as its goal; read in its
  working directory, where the factory keeps its journal out of the
  published tree:
  `grep '"type":"POST_MERGE_CHECKED"' factory/state/events.jsonl | grep -c '"verdict":"passed"'`.
  The fifty-two before them are recorded `unmeasured`: no post-merge check
  was configured there until 2026-10-21.
- **Its version 0.1.0: tagged on GitHub on 2026-11-02, published on npm on
  2026-11-06** - in any clone, `git rev-parse 'v0.1.0^{commit}'` prints
  `837c291838de779a9ca333e5b49ebcac7d75c92f`; anywhere,
  `npm view @trofimyukdev/repo-truth version` printed `0.1.0` on 2026-11-06,
  and `npm view @trofimyukdev/repo-truth 'time[0.1.0]'` prints
  `2026-11-06T05:14:20.934Z`, the moment the registry recorded it.
- **Ticks there started by a timer: none yet** - all `237` were started by
  the operator: in its working directory,
  `grep '"type":"RUN_STARTED"' factory/state/events.jsonl | grep -c '"trigger":"operator"'`,
  as many as `grep -c '"type":"RUN_STARTED"' factory/state/events.jsonl`.
- **The second repository:**
  [github.com/trofimyukdev/repo-truth](https://github.com/trofimyukdev/repo-truth) -
  every count above that names a clone can be re-run there.

**Bootstrap. M0 to M4 landed; M5 - the first consumer in production - in
progress: every row of its chain is closed, and its definition of done is not
met.** The factory builds against its own repository and, since 2026-09-12,
drives the queue of a second one from outside its own tree. **On 2026-10-02 it
merged through its own gate for the first time: nine tasks into that second
repository's public `main`, each passed by the gate and merged and pushed by the
factory itself, under supervision - no tick was started by the timer. By the
evening of 2026-11-02 its gate had made ninety-three merges there, forty-one
of them measured `passed` after they landed, and the operator had released
that repository's version 0.1.0, tagged on GitHub, which he published on npm
on 2026-11-06. He had taken the soak ladder's fourth rung and then its fifth -
unattended cron by day - each at a moment the ladder was not offering it. No
timer has been armed, so no tick there has yet been started by one.**

Measured on the evening of **2026-11-05** against the private `main` at
`3dfc7abfadf6edcd420387f0b0fc8567b485eeb1` - thirty-four landings after the
commit the previous snapshot named on the night of 2026-10-30, every one of
them an M0 row - with `git -C <repo> ... main`. Of the rows on the second
repository, the merge count is re-run, as any clone of it prints it, and the
release's npm row was read from the registry on the morning of 2026-11-06; the rows
dated 2026-11-05 were read in its working directory at 21:38 +0200 that
evening, while no tick ran there, from the factory's journal, which that
repository does not publish; and the rows dated 2026-10-12 were read there
between 10:50 and 10:54 +0300 that morning - the factory's own `metrics`, not
run again since, and a cost sum cut at that morning's last record, which
printed the same on 2026-11-05:

| Measurement | Value | Command |
|---|---|---|
| Commits on `main` | `1905` | `git rev-list --count main` |
| Landings (subject begins `merge: `) | `237` | `git log --format='%s' main \| grep -c '^merge: '` |
| First / latest commit date | `2026-08-17` / `2026-11-05` | `git log --format='%ad' --date=short --reverse main \| head -1`; same without `--reverse` |
| M4 landings | `7` | `git log --format='%s' main \| grep -c '^merge: M4-'` |
| M5 landings | `6` | `git log --format='%s' main \| grep -c '^merge: M5-'` |
| M5 rows filed in the queue | `7` | `git ls-tree --name-only main factory/tasks/ \| grep -c 'M5-'` |
| TaskSpecs in the queue | `426` | `git ls-tree --name-only main factory/tasks/ \| wc -l` |
| ADRs | `65` | `git ls-tree --name-only main docs/decisions/ \| wc -l` |
| Landings since 2026-09-12 | `141` | `git log --format='%ad %s' --date=short main \| grep '^\S* merge: ' \| awk '$1 > "2026-09-12"' \| wc -l` |
| Of those, M5 landings - every other one is M0 | `4` | the same, with `grep -c 'merge: M5-'` in place of `wc -l` |
| Merges the gate made into the second repository's `main` | `93` | in any clone of it: `git rev-list --merges --count 9eb3692..837c291` |
| Its release: the tag `v0.1.0` names `837c291`; on npm, 2026-11-06 | `0.1.0`, published 2026-11-06 | in any clone: `git rev-parse 'v0.1.0^{commit}'`; anywhere: `npm view @trofimyukdev/repo-truth version` -> `0.1.0`, and `npm view @trofimyukdev/repo-truth 'time[0.1.0]'` -> `2026-11-06T05:14:20.934Z` |
| Soak-ladder rung there, 2026-11-05 | `5` (unattended cron by day), taken by the operator on 2026-10-25 while not offered, and not moved since | from its working directory: `grep '"type":"LADDER_RUNG_CHANGED"' factory/state/events.jsonl \| tail -1 \| jq -c '[.payload.from, .payload.to, .ts]'` -> `[4,5,"2026-10-25T21:27:56.574Z"]` |
| Timers of the factory armed on its machine, 2026-11-05 | none | `systemctl --user list-timers` |
| Ticks there started by the operator / by a timer, 2026-11-05 | `237` / `0` | from its working directory: `grep '"type":"RUN_STARTED"' factory/state/events.jsonl \| grep -c '"trigger":"operator"'`; the same with `cron` |
| Merges there that the post-merge check measured `passed`, 2026-11-05 - the repository's roadmap sets forty as its goal | `41` | from its working directory: `grep '"type":"POST_MERGE_CHECKED"' factory/state/events.jsonl \| grep -c '"verdict":"passed"'` |
| Gate verdicts on the second repository, refused / passed, 2026-11-05 | `44` / `98` | from that repository's working directory: `grep -c '"type":"GATE_FAILED"' factory/state/events.jsonl`; the same with `GATE_PASSED` |
| Of those passes, with the held-out acceptance check run and passed, 2026-11-05 | `97` | from the same directory: `grep '"type":"GATE_PASSED"' factory/state/events.jsonl \| grep -c 'holdout acceptance item(s) passed'` |
| Verified merges there, as the factory counts them, 2026-10-12 | `30` | from its working directory, the factory's `metrics`: the line `verified_merges` |
| Tasks there that failed out, blocked or given up on, 2026-10-12 | `0` | the same `metrics`: the line `failed_out` |
| `$` per verified merge there, the factory's metric - the attempts of the merged rows only, 2026-10-12 | `1.6357` | the same `metrics`: the line `usd_and_tokens_per_verified_merge.cost_usd` |
| `$` per verified merge there, all in - every worker run the journal prices, over the same thirty, 2026-10-12 | `2.9815` | from its working directory: the sum over the journal's priced `AGENT_FINISHED` records up to seq `6082`, by the command in `TIMELINE.md`, "Where the snapshot stands" -> `89.4442`, divided by `30` |

**Landed is not the same fact as done, and this repository will not let the two
blur.** Every mechanism `DESIGN.md` section 17 puts in M4 - the tick wrapper, the
systemd unit and timer, the durable circuit breakers, the morning report, the
fault-injection categories, the soak ladder - has landed. M4's definition of done
is "soak ladder through step 5", and the landings did not meet it:
`decisions/0026-m4-exit-and-the-ladder-nobody-climbed.md` is the reading that
says so, and it is published here for exactly that reason. On the second
repository the ladder now stands at the fifth of its six rungs, the one that
admits a tick started by a timer by day, and no timer has been armed: the
step the definition names has been reached and not yet run.
M5 has seven rows filed and six landings, and all seven rows are closed: its
central row - the one that runs the factory against the second repository - on
2026-10-04, on the strength of the first merge the gate made there, and its
last three on 2026-10-05. Those three land readings rather than changes: the
router's choice is computed from the database and printed but applied to no
seat, the statistic the lens order would be recomputed from is declared
unavailable, and rung 6's threshold is measured on rung 5 while the clock
around the day waits on a packet for the operator. M5's definition of done -
"30-50 real tasks; router and lens order recomputed from data" - is not met:
the gate has now made ninety-three merges in the second repository, past the
top of the range the line names, but the lens order has not been recomputed
and the router's choice is applied to no seat. That repository's own roadmap
is met up to its last stage - its goal of forty merges measured `passed`
after they land is met - and the release that stage names is tagged and,
since 2026-11-06, published on npm; but that roadmap is not the line's second half.
So M5 is not done, by the same
rule that keeps M4 open. Until 2026-10-05 the last landing of any milestone was
dated 2026-09-12: of the hundred and forty-one landings since, a hundred and thirty-seven
are M0 rows, nearly all of them repairing the mechanisms the M5 run keeps finding - the fix
cycle a bounded tick could not hold, the edge a gate refusal had no route
through, the ladder's blindness to the verdict its first rung counts, the one
worker home every seat of a pass shared, a goal evaluator whose reply the gate
could not read, a ladder that measured the consumer's working tree instead of
the commit, and since then the gate's own errors in both directions, the
candidate's code run outside the OS fence where it should not have been, and
the first pieces of unattended running - a failure alert, a dead-man ping on
every road out of the tick, a breaker that reads every seat - and, since the
previous snapshot, the rows set to land before a timer may start a tick - a
login probe that waits out a weekly limit instead of opening the circuit, an
OS fence that hides the credential stores from every fenced run, a fired wall
that stops a worker's whole process group - and a configuration refused when
its worst pass exceeds the tick's dollar cap
(`decisions/0065-the-operator-word-of-2026-11-01-rule-a-a-worst-case-pass-within-the-tick-cap.md`).
The other
four are M5-04, the written procedure a seat follows before it puts one of the
ladder's next three rungs to the operator
(`decisions/0048-the-written-procedure-for-soak-rungs-3-4-and-5.md`), and the
chain's last three rows.

**On the second repository the gate has gone from verdicts to merges.** Its
first pass is recorded as a false one: `decisions/0039-the-factory-fixes-its-own-gate-first.md`
is where the operator answered it - the factory does the work there itself, and
its gate is fixed first. The next four passes each ran the task's held-out
acceptance check and passed it; in shadow mode none of them reached the base
branch. With ten tasks judged by the gate, the ladder's first rung met its
threshold, and on 2026-10-02 the operator took the second - supervised
auto-merge, one task per tick
(`decisions/0042-the-ten-task-programme-and-its-standing-tick-word.md` left
that move to him) - and switched that repository's shadow mode off.
The same day the gate passed nine tasks on all seven conditions, each with its
held-out check run and passed, and the factory merged each candidate onto the
base it had just fetched and pushed the result: nine two-parent merge commits,
each adding one check and its tests, each carrying the trailers `DESIGN.md`
section 10 names. A tenth task, the command that runs the checks, was refused
twice that evening by its held-out check alone; reissued with that check
repaired, it was merged the next day. The factory's own metric puts a verified
merge there at under two dollars of model cost, counting every attempt of the
rows that merged, the refused ones included; with every cancelled version of a
spec added, it is about 1.8 times that, and both are the price the CLI reports
for its runs, not a bill. The ladder offered the third rung, two parallel
builders, and it was not taken; from that tenth merge the ladder read one of
the refusals in the second rung's window as overturned - a false-block rate
over the 10% the third rung allows - and stopped offering it. The operator then
deferred that repository's next task until four of the factory's own rows had
landed, with ticks there stopped meanwhile
(`decisions/0045-m0-222-behind-the-three-rt-08-waits-and-item-4-taken.md`);
they landed, and on the night of 2026-10-05 the factory merged that task, a
GitHub Action wrapper, and one more that repaired four residuals of the
earlier merges - the eleventh and twelfth merges there. On 2026-10-07, after
six new tasks were filed, the factory merged four more - the thirteenth to
the sixteenth - and gave the fifth up: an end-to-end suite that changes no
TypeScript under `src/` but tests, refused four times on the one entry its reviewer could
not verify, a stage-5 measurement that had nothing to measure in it and so
never ran. The sixth was split by the operator
into three smaller tasks. Those seven refusals left the one overturned
refusal at one in eleven, under the 10%, and the ladder offered the third rung
again. From 2026-10-10 to the morning of 2026-10-12 the factory merged thirteen
more there, the last of them the twenty-ninth merge its gate made - among them
the end-to-end suite it had given up on, offered again once the gate could
retire the entry it had been refused on
(`decisions/0049-the-tests-only-mark-on-stage-5-bound-to-the-holdout.md`),
and the three tasks of the split. The refusals of 2026-10-11 and the merges
after them took the share of refusals the ladder reads as overturned above the
10% the third rung allows, and the ladder no longer offered it; on the morning
of 2026-10-12 the operator took the third rung all the same, and the record of
the promotion names the clause he set aside (`TIMELINE.md`, "Where the
snapshot stands"). From then to the first minutes of 2026-10-31 the factory
merged fifty-four more there, the eighty-third merge its gate made among them,
and the operator took the fourth rung, normal concurrency, on 2026-10-17, and
the fifth, unattended cron by day, on the night of 2026-10-25 - each time over
the same clause, the share of refusals the ladder reads as overturned. That
repository's own roadmap sets its goal at forty merges by the factory, each
measured again after it lands; on the morning of 2026-10-30, thirty had been
measured `passed`. By the evening of 2026-11-02 the factory merged ten more
there, the ninety-third merge its gate made among them, and forty-one had
been measured `passed` - the goal met. The roadmap's last stage, the release,
is the maintainer's own act, and it followed that evening: the commit that
names the package and its version 0.1.0, tagged `v0.1.0`; the operator
published the package on npm on the morning of 2026-11-06 (`TIMELINE.md`,
"Where the snapshot stands"). The earlier series of ticks are recorded, with their
commands, in `decisions/0031-the-word-on-the-series-and-the-word-on-the-models.md` and
`decisions/0032-the-words-on-the-second-series-and-the-debug-mode.md`.
The full derivation is `TIMELINE.md`.

A number on this page without a command beside it would not be a fact
(`PRINCIPLES.md`, discipline 1). If you find one, it is a defect.

## How to read this repository

1. **`PRINCIPLES.md`** - the 13 disciplines. Every rule in it was paid for by a
   real incident, and they govern how the factory is built rather than what it is.
   Read these first; the rest of the repository only makes sense as their
   consequence.
2. **`DESIGN.md`** - the normative specification, ratified 2026-08-19: the core
   split, repository layout and consumer contract, TaskSpec, state machine, tick,
   verification DAG, merge gate, integration, economics, security, configuration,
   roadmap.
3. **`decisions/`** - the published subset of the architecture decision records:
   the things a reader of the design cannot infer from it, including the ones
   that record a task being stopped four times and an operator splitting it, a
   milestone whose mechanisms all landed and whose exit criterion was not met,
   and a place where the design's own text and the CLI it drives appear to
   disagree.
   `decisions/README.md` is the index, and says how many there are and which.
4. **`TIMELINE.md`** - the operating record: milestones, dates and counts, each
   with the command that prints it.

## The showcase consumer

[`repo-truth`](https://github.com/trofimyukdev/repo-truth) (created alongside this
repository) is the portable form of the factory's own gates - commit-range
hygiene, the measurement rule, trailer checks, a weakened-tests detector and
more - as a CLI. It is the first repository whose queue the factory drives from
outside its own tree: its tasks live in `factory/tasks/`. The onboarding command
that points the factory at a repository outside its own tree landed on
2026-09-12 (`merge: M5-01` in `TIMELINE.md`), and the first shadow run over this
repository was taken before it, by hand.

The factory took its tasks in shadow mode - verdicts, and nothing merged - until
2026-10-02, when the operator moved the soak ladder to supervised auto-merge
and, in a separate commit there, switched shadow mode off (`9eb3692`, `chore:
merge shadow off - a candidate that passes the gate is merged`). What the
factory merged after it is public: in any clone of that repository,

```sh
git log --first-parent --reverse --format='%h %ad %s' --date=short 9eb3692..8338b5a
```

prints nine merge commits, from `merge: RT-10` to `merge: RT-12`, each adding
one check and its tests; `git log -1 --format=%p <sha>` names two parents for
each, the base and the candidate. Its first task, `RT-01`, landed before them
and was accepted by hand. The task that gives the checks their single
command-line entry point, `RT-07`, is the one the gate refused twice that
evening. Reissued with its held-out check repaired, it was merged on 2026-10-03
as the tenth merge, so the command that runs the checks is on `main` now:
`git log -1 --format='%h %ad %s' --date=short fcf6d3b` prints

```text
fcf6d3b 2026-10-03 merge: RT-07 - One entry point - `repo-truth check` runs the checks and answers with records
```

`TIMELINE.md`, "Where the snapshot stands", quotes the nine lines and what the
gate recorded for each, and reads `RT-07`'s two refusals.

## What is here and what is not

This repository holds design and record. The controller's source, its tests, its
verification stages and the founding-research archive are private and not
published; the archive is mixed-language and is quoted, not reproduced. The core
is available on request.

(c) 2026 Vladimir Trofimyuk, CC BY 4.0
