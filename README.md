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
- **integrator** - rebase onto a freshly fetched base, re-measure on the
  integration SHA, fast-forward push, never `--force`.

The objective function is **`$` per verified merged task**, not tokens saved and
not tasks attempted. `DESIGN.md` section 1 is the home of that definition and of
the non-goals it excludes.

## Status

**Bootstrap. M0 to M4 landed; M5 - the first consumer in production - in
progress.** The factory builds against its own repository and, since 2026-09-12,
drives the queue of a second one from outside its own tree.

Measured on **2026-09-22** against the private `main` at
`260cc4a051bdba2779b10e6698606aa0c8ac2a5d`, with `git -C <repo> ... main`:

| Measurement | Value | Command |
|---|---|---|
| Commits on `main` | `1051` | `git rev-list --count main` |
| Landings (subject begins `merge: `) | `106` | `git log --format='%s' main \| grep -c '^merge: '` |
| First / latest commit date | `2026-08-17` / `2026-09-22` | `git log --format='%ad' --date=short --reverse main \| head -1`; same without `--reverse` |
| M4 landings | `7` | `git log --format='%s' main \| grep -c '^merge: M4-'` |
| M5 landings | `2` | `git log --format='%s' main \| grep -c '^merge: M5-'` |
| M5 rows filed in the queue | `7` | `git ls-tree --name-only main factory/tasks/ \| grep -c 'M5-'` |
| TaskSpecs in the queue | `300` | `git ls-tree --name-only main factory/tasks/ \| wc -l` |
| ADRs | `29` | `git ls-tree --name-only main docs/decisions/ \| wc -l` |

**Landed is not the same fact as done, and this repository will not let the two
blur.** Every mechanism `DESIGN.md` section 17 puts in M4 - the tick wrapper, the
systemd unit and timer, the durable circuit breakers, the morning report, the
fault-injection categories, the soak ladder - has landed. M4's definition of done
is "soak ladder through step 5", and the ladder stands at its first rung with no
task promoted through it. `decisions/0026-m4-exit-and-the-ladder-nobody-climbed.md`
is the reading that says so, and it is published here for exactly that reason.
M5 has seven rows filed and two landings, and the last landing of any milestone
is dated 2026-09-12: the ten landings since are all M0 rows repairing the
mechanisms the M5 run keeps finding - the fix cycle a bounded tick could not
hold, the edge a gate refusal had no route through, the ladder's blindness to the
verdict its first rung counts, the one worker home every seat of a pass shared.
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
3. **`decisions/`** - twelve architecture decision records: the things a reader
   of the design cannot infer from it, including the ones that record a task
   being stopped four times and an operator splitting it, and a milestone whose
   mechanisms all landed and whose exit criterion was not met.
   `decisions/README.md` is the index.
4. **`TIMELINE.md`** - the operating record: milestones, dates and counts, each
   with the command that prints it.

## The showcase consumer

[`repo-truth`](https://github.com/trofimyukdev/repo-truth) (created alongside this
repository) is the portable form of the factory's own gates - commit-range
hygiene, the measurement rule, trailer checks, a weakened-tests detector - as a
CLI. It is the first repository whose queue the factory drives from outside its
own tree: its tasks live in `factory/tasks/`, and the factory takes them in shadow
mode before any live merge. The onboarding command that points the factory at a
repository outside its own tree landed on 2026-09-12 (`merge: M5-01` in
`TIMELINE.md`), and the first shadow run over this repository was taken before
it, by hand.

## What is here and what is not

This repository holds design and record. The controller's source, its tests, its
verification stages and the founding-research archive are private and not
published; the archive is mixed-language and is quoted, not reproduced. The core
is available on request.

(c) 2026 Vladimir Trofimyuk, CC BY 4.0
