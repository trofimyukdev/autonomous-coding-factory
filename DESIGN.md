# Millwright - design

> Public copy of the ratified design (ratified 2026-08-19); snapshot of the private main at 0871ab189b6d4a89134677450fbc1a9e973191c1 taken 2026-08-31; private paths and the private consumer's name removed.
>
> References below to "the blueprint" and to the founding-research archive point
> to a private archive that is not published. Paths of the form
> `docs/decisions/NNNN-...` name files in the private repository; the eight ADRs
> reproduced in this repository are listed in `decisions/README.md`.


**Status:** ratified 2026-08-19 (M1-01). This file is the normative design; on any
conflict with the founding blueprint (private archive, not published)
this file wins.

**What the blueprint still holds.** It is an archive, but not an empty one, and the
list is closed: the rationale, the measurements and the research provenance behind
every decision here; the fault-injection enumeration (section 15); the pre-autonomy
checklist (section 20); the starting calibration values of Appendix A; the starting
model and price table (section 11); and the first (private) consumer's migration procedure
(section 19). Those are referenced from here and are not copied here, in that one
direction (discipline 12). Everything else the
blueprint says is either restated in this document as the normative rule or
superseded by a decision in `docs/decisions/`; ADR 0006 is the ledger of which is
which. The blueprint is not edited to follow this document - it is a dated archive,
and a divergence between the two is resolved here.

This document specifies *what the factory is and what it guarantees*. It does not
restate `PRINCIPLES.md` (the 13 disciplines that govern how we build it) and it
does not carry the evidence behind the design choices; the blueprint sections are
cited as `blueprint section <n>` where the reasoning lives.

---

## 1. Purpose, objective function, non-goals

Millwright is an autonomous coding factory: in goes a queue of tasks, out comes
code that is verified and merged into the base branch of a consumer repository,
unattended, on a schedule.

It optimises, in this order:

```text
$ / verified merged task
wall-clock / verified merged task
post-merge regression rate
```

subject to a quality SLO, a budget, machine resources, and the subscription rate
limits (section 11 below). It does not optimise `$ / token`.

**Non-goals.** Millwright does not deploy (merge is reversible, deploy is not; see
discipline 6). It does not replace the human-triggered phases of the Dev Engine
(`/define`, `/audit`, `/atlas`, `/weekly` remain Claude Code skills). It is not a
framework: everything the Claude Code CLI provides natively (`--json-schema`,
`--max-budget-usd`, hooks, sandboxing) is used as-is, and millwright owns only the
queue, the state machine, the gate and the integration path (blueprint section 2).
A wrapper that duplicates a vendor's roadmap is buried by the ecosystem within a
quarter, so a single-author runtime dependency is vendored or forked, never merely
depended on.

## 2. Ownership split

```text
Claude owns the intelligence inside a task.
Code owns the lifecycle of the task.
Git owns immutable code identity.
SQLite owns durable state.
Tests and checkers own machine evidence.
An independent Claude owns the semantic challenge.
One controller alone owns integration.
The human owns irreversible actions.
```

Two consequences are load-bearing and appear again in every section below: the LLM
decides *inside* a state, never *between* states; and no agent's self-report is
evidence - the controller re-runs the check itself.

## 3. Architecture

```text
factory/tasks/*.yaml ---> INTAKE (deterministic: schema, dedup, deps, NEEDS_SPEC)
                              |  TaskSpec (immutable, hashed)
                              v
 systemd timer -> MILLWRIGHT CONTROLLER (TypeScript CLI, SQLite WAL + events.jsonl)
                              |                    ^-- STOP file / budget / policy
        leases                |
        +---------------------+----------------------+
        v                     v                      v
  Worker A (worktree     Worker B (worktree     INTEGRATOR
  + cgroup, claude -p)   + cgroup, claude -p)   (the only path into the base
        |                     |                  branch; CAS push)
        +----------+----------+                      |
                   v                                 v
            VERIFY DAG (stages 0-6:            origin/<base branch>
            free checks before paid ones)      (+ post-merge smoke)
```

### Roles

| Role | Implemented by | Does | Must not |
|---|---|---|---|
| Controller | deterministic CLI | tick, queue, lease, workspace, dispatch, gate, integration, budgets, journal, recovery | write code; make semantic judgements |
| Intake / Normalizer | code (+ optional cheap model) | raw item -> valid TaskSpec, or `NEEDS_SPEC` | invent product decisions |
| Classifier | code (+ optional cheap model) | task class, risk, file-overlap prediction | pick the model (a routing table does) |
| Builder | fresh `claude -p` in a worktree | one TaskSpec: code, tests, commits on its own branch, schema-valid report | merge, push, self-assess, edit the TaskSpec or the factory |
| Semantic reviewer | fresh `claude -p`, read-only tools | findings against the TaskSpec, schema verdict | fix anything; see the builder's narrative |
| Risk lenses | fresh sessions, trigger-matrix | security / data / concurrency / doc-truth / test-strength / taste | run unconditionally |
| Refuter / adjudicator | fresh session, senior model | try to kill one specific merge-blocking finding | look for new findings |
| Goal evaluator | cheap model | yes/no on the machine-checkable acceptance items, plus which ones it could not confirm | write code |
| Integrator | controller | rebase/merge onto fresh origin base, final evidence on the integration SHA, fast-forward push | ever use `--force` |
| Operator | human | queue, product decisions, `NEEDS_SPEC`, deploy, kill switch, autonomy promotion | - |

## 4. Repository layout and the consumer contract

Millwright is a standalone product repository, laid out by concern: `src/`
(`controller`, `store`, `workspace`, `backend`, `verify`, `integrate`, `router`,
`report`, `doctor` - a module that holds no code yet states what it owns in a
one-line index file), plus `scripts/`, `schemas/`, `test/unit/` and
`test/faultinjection/`. The directories later milestones need - `prompts/`,
`plugins/`, `templates/consumer/` - are still empty and arrive with the code that
fills them. `backend` is an interface on purpose: the headless CLI worker is its
first implementation, and moving to the SDK must change neither the controller nor
the state.

A consumer repository holds configuration only:

```text
<consumer-repo>/factory/
  millwright.toml   # repo, base branch, models, budgets, slots (section 16)
  compat.json       # tested and minimum versions of millwright and the claude
                    # CLI, and the CLI capabilities the factory requires
  tasks/            # incoming TaskSpecs, one file per task
  checks.yaml       # this repository's deterministic check ladder
  policy/           # allowed/forbidden paths, risk triggers, deny lists
  state/            # factory.db + events.jsonl        (gitignored)
  runs/             # run artefacts                    (gitignored)
  generated/        # STATUS.md and other views        (gitignored)
  STOP              # secondary kill switch; the authoritative one lives
                    # outside the repository (section 13)
```

Installation is a version pin (`npm i -D millwright@<version>` or a git tag), never
a file copy: the core has exactly one home, consumers hold configuration, and an
upgrade is a version bump plus `doctor` plus a canary tick. `compat.json`
pins both versions; `doctor` refuses to run against an untested millwright,
while the Claude CLI is gated on the tested minimum (section 12).

Integration of the first consumer (private, not published) follows blueprint section 19:
`checks.yaml` from its existing test command, its proven project rules moved
into configuration, its queue converted into TaskSpecs, and shadow mode over the
real queue before any automatic merge.

## 5. TaskSpec - the contract between human and factory

One task is one YAML file in `factory/tasks/`. Fields:

| Field | Meaning |
|---|---|
| `id` | stable, immutable identifier |
| `repo`, `priority`, `title` | routing and ordering |
| `outcome` | what changes for the user or the system - never how |
| `measure` | commands, not adjectives |
| `not_done_if` | anti-criteria (e.g. "accepted but the route is not wired") |
| `acceptance[]` | the machine half of the DoD: `type: command` (with `required`, optional `holdout`) and `type: behavior` statements |
| `allowed_paths`, `forbidden_paths` | enforced by the controller against the diff, not requested in a prompt |
| `dependencies`, `discovered_from` | ordering; provenance of tasks found while doing another. `discovered_from` is a task id, `null`, or the one reserved literal `bootstrap` - what the pre-factory bootstrap session found, which has no task id to point at |
| `resources`, `exclusive_resources` | conflict-aware scheduling |
| `risk` | level and dimensions; drives lens triggers and routing |
| `budget` | `quality_attempts`, `infra_retries`, `builder_usd`, `verify_usd`, `wall_minutes` |
| `merge` | `{ mode: auto \| pull_request \| hold }` |

**Acceptance semantics.** The task's acceptance commands play the SWE-bench
`FAIL_TO_PASS` role (red before, green after); the full suite of verification
stage 2 plays `PASS_TO_PASS` (what must not break). "Resolved" means both are
green on the integration SHA.

**Intake and the Normalizer.** A raw queue item is accepted: intake runs it through
the Normalizer (a cheap model), which either fills in a TaskSpec or honestly returns
`NEEDS_SPEC` *together with the list of decisions it is missing* - a bare flag leaves
the operator nothing to act on. A YAML that already validates never reaches the
Normalizer: a valid spec must not cost a model call.

**Holdout checks.** An acceptance item marked `holdout: true` is never shown to
the builder and runs only in the gate. Its file lives *outside* the consumer
repository, under `~/.config/millwright/<repo>/holdout/`, because forbidden paths
restrict writing, not reading, and agents demonstrably find the answers in the
repository and its git history.

**Invariants.**
- `acceptance` exists before the builder starts and the builder may not rewrite it
  (verification stage 1 catches the attempt).
- Every attempt records the `spec_hash`; evidence is always bound to one exact
  version of the spec. Editing the file after capture creates a new spec version,
  it does not mutate a running task.
- A task that needs a product decision goes to `NEEDS_SPEC` and waits for the
  operator. The factory never picks something plausible instead.

## 6. State

Two layers, each on the medium it is good at (blueprint section 6):

- **Human layer - files in git.** `factory/tasks/<id>.yaml`. Editable, diffable,
  mergeable, one file per task so it rarely conflicts.
- **Runtime layer - SQLite in WAL mode.** States, leases, attempts, checks,
  metrics, events. It is a local execution journal: gitignored, never hand-edited,
  rebuildable from `tasks/` + git + `runs/`. Its column set evolves, so the store
  owns versioned schema migrations rather than create-once DDL.

Tables: `tasks` (state, priority, spec, `spec_hash`, lease owner/expiry, the two
attempt counters, base/candidate/integration SHAs, `UNIQUE(repo_id, spec_hash)` for
idempotent enqueue), `attempts` (role, model, effort, timings, cost, tokens,
branch, workspace, SHAs, prompt/config hashes, CLI version), `checks` (name,
version, candidate SHA, status, severity, duration, evidence path), `events`
(append-only sequence). Pragmas: `journal_mode=WAL`, `synchronous=FULL`,
`foreign_keys=ON`, `busy_timeout`.

`events` is mirrored into an append-only `events.jsonl` that survives any database
failure. No LLM writes to any of these tables; only the controller does, from
schema-validated role outputs.

Operators read `millwright queue` and a generated `STATUS.md`. Markdown is a view;
the canonical runtime state is never markdown.

### Task state machine

```text
QUEUED -> READY -> CLAIMED -> PREPARING -> BUILDING -> VERIFYING
       -> READY_TO_INTEGRATE -> INTEGRATING -> MERGED -> POST_MERGE_CHECK -> DONE

side states: NEEDS_SPEC | BLOCKED | RETRY_WAIT | PAUSED | DEAD_LETTER | CANCELLED
             | SUPERSEDED
```

Only the controller performs transitions, transactionally. Key edges:

- `BUILDING -> RETRY_WAIT`: infrastructure failure; spends no quality attempt, sets
  `not_before = now + backoff`.
- `VERIFYING -> BUILDING`: fix cycle with a fresh builder and a FailurePacket;
  `quality_attempts++`.
- `BUILDING|VERIFYING -> BLOCKED`: quality attempts exhausted; the branch is kept
  and an incident is raised.
- `BLOCKED -> DEAD_LETTER`: the infrastructure ceiling is spent. A landing that
  would charge an infrastructure retry the task's own `budget.infra_retries` does
  not grant is diverted - the row lands `BLOCKED` instead of where the caller
  asked, and the same transaction carries it on to `DEAD_LETTER` - so one broken
  task stops without stopping the queue behind it. No counter moves for the
  failure that ends the loop, because nothing was retried for it: the row rests
  with `infra_retries` standing exactly at the ceiling its own spec declared, and
  the events of both edges carry the count, that ceiling, and a controller-side
  name for an outcome no worker produced. Neither the state nor the edge is new.
  What this block asks the section to ratify is that the CONTROLLER now walks the
  edge, where until M0-116 giving up was the operator's act alone
  (**[operator-confirmable]**, 2026-08-29 - it stands unless the operator vetoes
  it). Reopening is unchanged and stays the operator's: `DEAD_LETTER -> READY` is
  walked by nothing else, so a task the factory has given up on is parked where an
  operator finds and reopens it, never dropped.
- `INTEGRATING -> READY_TO_INTEGRATE`: the base moved; re-integration is not an
  attempt.
- `POST_MERGE_CHECK -> BLOCKED`: regression; auto-revert only where the task class
  makes revert safely reversible.
- `QUEUED|NEEDS_SPEC -> SUPERSEDED`: a newer captured version of the same spec id
  is live, so this one is retired and the event payload names its successor.
  Only the two states a version is born in have this edge, which is what leaves a
  version that a worker already holds alone.
- `DONE -> QUEUED`: a close recorded in error is withdrawn and the row goes back
  to the head of the chain. It is the only edge that takes a record back rather
  than carrying the row anywhere, which is why DONE stays terminal: nothing
  carries a closed row further, and a withdrawal carries nothing. The named store
  operation is the only thing in the factory that walks it, and it is what makes
  the event say what was withdrawn and why; the edge itself is checked like every
  other, so nothing is special-cased past the machine.
- `SUPERSEDED -> QUEUED|NEEDS_SPEC`: the task file was reverted to this captured
  version. `UNIQUE(repo_id, spec_hash)` means it cannot be captured a second
  time, so the row itself comes back - into the state that version is born in, so
  a reverted file that does not validate is parked again rather than queued.

### Provisional rows - a capture no commit holds

`enqueue` reads the WORKING TREE, so a spec edited three times inside one block
becomes three permanent rows, and two of them capture a state that exists in no
commit. Nothing can ever check what the factory believes about such a row: no
`git show` produces the text its `spec_hash` was computed from.

The queue records that rather than hiding it. `tasks.provisional` is
three-valued: `1` when no commit reachable from the base branch holds a task file
with this `spec_hash`, `0` when one does, `NULL` when nothing has asked. Intake
still captures the row - a block that edits a spec must be able to enqueue it -
and what changes is that the row says so.

- The reproducible set is read ONCE per run and never per row: one walk of the
  base branch's history over the queue directory, and one `git cat-file --batch`
  over the blobs it names. WHICH git command that is, and why each of its flags
  is load-bearing, is `src/controller/reachability.ts`. Spelling the command line
  here as well made this document a second home for it, and the copy drifted a
  commit behind the code the first time the walk changed (discipline 12).
- A run that could not ask git marks nothing and leaves rows at `NULL`. "Not
  checked" is never spelled "reproducible".
- A provisional row becomes ordinary the moment a commit carries its `spec_hash`,
  without being rewritten: the mark changes and the event records when.
- `millwright doctor` fails when a live row the repository cannot show is not
  marked; a live row that IS marked is a normal state during a block.
- `millwright prune-provisional` removes the retired ones, and `--dry-run` is a
  rehearsal of exactly that. The store operation behind it refuses a live row, a
  row with attempts, a row it does not itself record as provisional, and any row
  that is not `SUPERSEDED`: the task file is still in `factory/tasks/`, so the
  next `enqueue` re-inserts the same content under the same row id, and that is
  only honest where the state machine already declares the way back
  (`SUPERSEDED -> QUEUED|NEEDS_SPEC`). Deleting a `DONE` or `CANCELLED` row would
  reproduce an edge `EDGES` does not have. The event carries the row as the table
  held it, because the mirror is where that row still exists afterwards.

### Lease and recovery

A claim is one transaction that sets `lease_owner = host:pid:run_id` and
`lease_until = now + TTL`; a heartbeat extends it. A dead process lets the lease
expire, and the reaper then *investigates* instead of resetting the task blindly:

- candidate commit present and evidence intact -> resume at `VERIFYING`;
- workspace touched but no trusted commit -> a new quality attempt only if LLM work
  actually started, otherwise an infra retry;
- the API call never started -> infra retry;
- origin already contains an integration SHA carrying our trailer -> reconcile to
  `MERGED`. Never merge twice.

## 7. One tick

`millwright tick` is the only command the scheduler knows; `millwright run --task`
is the operator's way to put one task through the same machinery by hand. One tick is one bounded
pass: pick up what fell, start what is ready, walk finished candidates through
integration, update reports, exit.

```text
 0. STOP file present -> exit 0 (the wrapper checks first and keeps the skip log)
 1. doctor-lite: database writable, git valid, origin reachable, claude --version
    within compat, no stray ANTHROPIC_API_KEY, subscription rate limits below the
    configured threshold
 2. janitor (start is recovery): expired leases -> the recovery above; targeted
    reaping of orphans by PID (never a pattern kill; the predicate is in section
    13); tmp older than 36 h; `git worktree prune --expire 2.days.ago`;
    delete bot branches of merged tasks
 3. base branch green? if not -> circuit OPEN, notify, exit 75
 4. budget: available = caps - spent - reservations; no room -> exit 0
 5. schedule up to max_tasks ready tasks (dependencies DONE, no resource conflict,
    low predicted file overlap, not factory-admin) whose spec is still "open" -
    no row of that spec id has reached DONE, which is what editing an already
    landed spec file leaves behind, AND some row of it is still live, so a spec
    id whose every version was superseded or cancelled is not open either - by
    priority. "Open" is `specStanding` in `src/store/state-machine.ts`: stated
    here, enforced there
 6. per task: lease -> worktree pinned to a base SHA -> builder in the background,
    in its own process group and cgroup, within the slot limits
 7. on builder completion: the verify DAG (section 8); pass -> READY_TO_INTEGRATE
 8. integrator: strictly one at a time per base branch (section 10)
 9. journal, metrics, STATUS.md, morning report, notifications
10. exit with an honest code (section 15)
```

Frequent bounded ticks (15 minutes) beat one long pass: smaller blast radius,
faster recovery, configuration is picked up naturally, an API outage does not hold
a giant hung process, and every action is anchored in the database.

### The builder packet

The builder gets one immutable message and no session history:

```text
TASK_ID, ATTEMPT_ID, BASE_SHA, TaskSpec, ALLOWED/FORBIDDEN PATHS,
TEST COMMANDS, WORKSPACE ROOT, OUTPUT SCHEMA,
FailurePacket (fix cycles only: the exact list of confirmed findings)
```

The whole brief goes in one message: splitting the same instruction across turns
costs quality and explodes variance (blueprint section 7).

Worker invocation is `claude -p` with an explicit tool allowlist, `--permission-mode
dontAsk`, `--strict-mcp-config` with an empty MCP config, `--max-turns`,
`--max-budget-usd`, `--no-session-persistence`, `--output-format json` and
`--json-schema`, wrapped in an external `timeout -k` on its own process group, with stdin closed
(`</dev/null`) so a worker can never inherit a terminal and wait on it.
Notably:

- no `--bare`: it does not read `CLAUDE_CODE_OAUTH_TOKEN`, so on a subscription it
  silently loses authentication (blueprint sections 13 and 17);
- an action that is not explicitly allowed is silently skipped in `-p` mode and the
  run continues, so the allowlist is always explicit;
- workers are stopped with SIGTERM first (it tears down the process tree and runs
  SessionEnd hooks); SIGKILL is the second step;
- subagents inside a builder are off by default - parallelism belongs to the
  controller, not to a worker spawning a hidden mini-factory - and are switched on
  only for a task the operator has explicitly marked wide;
- the builder's report is schema-valid or it is nothing: `status: candidate|blocked`,
  the commits it made, the files it changed, the tests it ran and its known risks.
  `tests_run` is diagnostics, never evidence - the controller re-runs the ladder
  itself (section 9);
- a report missing required schema fields is an infrastructure failure of
  format (so it costs an infra retry, not a quality attempt), not something to
  patch up by asking the session again;
- `--max-budget-usd` reports an overrun as exit 2, and the backend classifies that as
  a spent budget rather than a generic crash - the two feed different counters;
- the call is bounded on inactivity as well as on wall clock, because a silent stall
  is what a generous wall bound is worst at catching, and the wall bound itself
  carries slack for the known one-off startup hang of a headless session;
- stdin is truncated past ten megabytes without an error, so anything large - a
  diff, a FailurePacket - travels as a file and the prompt carries only its path.

## 8. Verification DAG

Order is fixed: everything that costs zero tokens runs first, and an LLM appears
only after the deterministic stages pass.

| Stage | Name | Cost | Content |
|---|---|---|---|
| 0 | Identity | 0 | expected task/branch/workspace; `base_sha` as recorded; candidate is a descendant of base; clean tree; no foreign refs touched |
| 1 | Scope and anti-cheat | 0 | diff within `allowed_paths`; forbidden paths untouched; no secrets; no deleted or weakened tests (`.skip`/`.only`, lowered thresholds, snapshot refreshes); factory gates and config not disabled; no unexplained lockfile drift; commit-range ASCII and identity hygiene over `base..candidate` (M0-07) |
| 2 | Deterministic ladder | 0 LLM | from `checks.yaml`: format -> focused tests -> typecheck -> lint -> unit -> build -> project truth checks -> full suite |
| 3 | Runtime smoke | 0..low | triggered when startup/routes/DI/schema/CLI/lifecycle are touched: start it, hit it, check it, stop it by PID |
| 4 | Semantic reviewer | LLM | fresh context, read-only *tools* (it walks the repo and runs read/test commands rather than reading a bare diff). Input: TaskSpec, SHA, diff, deterministic results. Not input: the builder's narrative or confidence. Output: a schema verdict - `verdict`, `findings[{severity, claim, evidence, would_block}]`, `unverified_dimensions` |
| 5 | Risk lenses | LLM, parallel | only by trigger: auth/crypto -> security; migrations -> data integrity; async/queues -> concurrency; public API -> compatibility; docs and numbers -> doc-truth; UX -> taste/a11y; weak suite -> test strength (mutation probe or reproduction test) |
| 6 | Refutation / adjudication | LLM, senior | only for merge-blocking findings: a senior model gets claim, evidence and code and tries to refute it |

Rules that make the DAG cheap and honest:

- A reviewer prompted to find gaps will usually report some even when the work is
  sound, so a lens flags only what hits correctness or a stated requirement.
  Severity filtering happens in the gate, not in the lens (report everything,
  filter downstream - discipline 9).
- Every lens must attack its own strongest finding before reporting it.
- A finding that does not survive refutation is downgraded or dropped; one that
  survives is a real blocker. A refuter that proposes a fix must verify the fix.
- An early stage failing returns the task immediately; later stages do not run,
  and their open questions go into the FailurePacket as questions, not findings.
- Lens order is per `(repo, task_class)` and is retrained from the factory's own
  statistics (`confirmed_blockers / ($ + w * seconds)`), not fixed globally.

## 9. The gate: seven machine conditions

The controller re-checks everything itself and takes no agent's word. All seven
are required, and a required check that cannot be run is an infrastructure or
gate failure - never a pass. That is the general rule; every "required" in this
document means it.

1. The deterministic ladder is green, re-run by the controller - not read from a
   report. Holdout acceptance checks run here.
2. The verdict is schema-valid, `overall == pass`, every item verified.
3. The test-change audit is clean, or the change is justified in the TaskSpec and
   the justification survived review.
4. The diff is within the task's bounds: paths, volume, no stray files.
5. The measurement measured what is being merged: every DoD number carries
   `candidate_sha` / `prompt_hash` / `config_hash`, and the gate names any
   unmeasured delta.
6. The goal evaluator confirmed the machine-checkable half of acceptance, and its
   answer is yes/no *plus what specifically was not confirmed* - a bare no names
   nothing for the FailurePacket to carry.
7. The integration candidate is what actually gets merged: final evidence is taken
   on the integration SHA, not on a stale base.

A first failure buys one fix cycle (fresh builder plus FailurePacket, same branch).
A second failure means `BLOCKED`: the branch is kept, an incident is raised, and
work continues only if the failure is isolated. When the metric
`fix_cycle_net_new_defect_rate` rises, the correct response is to stop earlier, not
to repair harder.

## 10. Integration - the only path into the base branch

While B was being built, A may have merged; evidence on `base_B` is not evidence on
`main_after_A + B`. Therefore, under a per-repo lock with `integrations = 1`:

```text
1. STOP checked; git fetch origin; remote_base = origin/<base branch>
2. fresh integration workspace on remote_base
3. merge the candidate; a conflict is an integration failure packet, not a quality
   attempt
4. record the integration SHA; run the merge-sensitive part of the deterministic
   ladder on it
5. semantic delta review only if base drift warrants it (risk rule)
6. STOP re-checked, then fast-forward push; rejection (the remote moved) -> discard
   the workspace and retry from step 1
7. atomically record the integration SHA and the origin observation in the database
```

STOP is checked three times per task, not once: at dispatch (section 7, step 0),
before integration starts (step 1 above), and again immediately before the push
(step 6). The first two are what the pre-autonomy checklist asks for; the third is
this document going further, because a switch pulled while the ladder is running
has to stop the half that is irreversible.

Never `push --force`, never `--force-with-lease`, never a push from an LLM session.
A rejected push against a moved remote is the compare-and-swap working, not an
inconvenience.

Every integration commit carries trailers:

```text
Millwright-Task-ID: <id>
Millwright-Attempt-ID: <id>
Millwright-Spec-Hash: sha256:<hex>
```

A crash after the push but before the database write is reconciled by finding the
trailer in origin. Exactly-once comes from reconciliation, not from hope.

`merge.mode = pull_request` pushes the task branch and opens a PR with the verdict
and evidence attached, auto-merging only after CI and policy; it is the recommended
trust step before `auto`, and is recommended for protected branches.

Post-merge: a fast smoke on the exact merged SHA; a regression triggers the
task-class revert policy, or a circuit plus notification. **Deploy is not merge:** a
separate deterministic adapter, run only behind an explicit operator flag.

## 11. Model routing and economics

The default is the middle model at middle effort; escalation happens on measured
failure or declared risk, and effort escalates before the model does. Roles map to
`[models.*]` blocks in the consumer config: builder default, builder hard,
reviewer, adjudicator, goal evaluator, scout. The scout is the sixth and newest,
added by operator sanction on 2026-08-25 after M0-66 landed it in code, and it
sits at the strongest tier the table has rather than at the default: it is
dispatched in place of a builder when a spec declares high risk or spans more
modules than section 16's threshold allows, and the whole value of that seat is
judgement about seams nobody has written down yet. The live home of the model ids is the
consumer's `[models.*]` config (section 16); blueprint section 11 carries the
starting table and the prices as they stood when it was written, which is
calibration and dates like any other calibration.

Override rules: a blocker raised by a cheap lens is re-checked by an expensive model
before it can fail the task; an ambiguous classification resolves upward; an
unavailable model steps up, never down, and the run report says so; every task's
classification is printed as one line so a routing mistake is visible without
reading diffs.

Levers, in order of expected return: zero-token stages first; prompt caching (a
stable role prefix, task-specific text last); cheap-first with effort escalation;
refutation only for merge-blocking findings; FailurePacket instead of full history
in fix cycles; hard ceilings (`--max-budget-usd` per attempt plus tick budget
reservation before a worker starts, so parallel workers cannot jointly overrun the
till); test slicing for builders with the full suite at the gate; tool-output
filtering so a model never reads megabytes of logs; and a strong model at low
effort as a cascade step of its own, which can match a weaker model at maximum
effort for less money - measure it, do not assume it.

Two billing-mode traps bound that list. The prompt-cache TTL is one hour on a
subscription but five minutes on usage credits, where
`ENABLE_PROMPT_CACHING_1H=1` restores it. And one lever is missing from the list above rather than ranked in it - the Batch
API discount, which stacks with caching and pays for non-latency-critical work
outside the merge path (night re-verification, mass scoring, test generation) - is
an API-key surface that does not exist on a pure subscription. Buying usage credits
is therefore a deliberate fallback, not a free speed-up: it changes the cache TTL
and moves billing per token.

The router learns: for each `(task_class, model, effort)` the database accumulates
first-pass success, success after retry, median/p95 cost and wall time, and
post-merge regressions, and the choice minimises expected cost per verified merge
under regression and latency constraints. Until roughly 30-50 tasks have
accumulated, the default table applies.

**The subscription weekly cap is the real budget.** It is not one number: a rolling
five-hour window sits under two weekly limits, a general one and a separate, much
smaller one for Opus, so a router escalating to Opus is drawing on the scarcer of
the two. All Claude surfaces draw from the same buckets, and N parallel workers
consume the week N times faster rather than producing N times the throughput. The factory therefore: reads the rate-limit
figures the statusline channel provides - `rate_limits.five_hour.{used_percentage,
resets_at}` and `rate_limits.seven_day.{...}`, dumped atomically into a state file
the controller reads before each task - and refuses to take work once
`seven_day.used_percentage` is above a configured threshold (85 to start); reacts
inside the worker session too, through a `StopFailure` hook matching `rate_limit`,
`overloaded` and `billing_error`; parses the weekly-limit message when it hits one
reactively, writing `PAUSE_UNTIL` into the database instead of burning ticks; and reserves a share of the weekly cap
for the operator's own interactive work (`weekly_reserve_pct`).

## 12. Scheduling, doctor, circuit breakers

A systemd user timer (or cron) runs a wrapper script that: fails loudly and early
(`set -Eeuo pipefail`, `umask 077`, an explicit `PATH` because cron inherits none
worth having); takes an flock so ticks never overlap; checks both STOP files and exits before the tick when either is
present, appending to a skip log; runs `millwright tick --trigger cron` with the tick's task and
dollar ceilings as flags, under `timeout --signal=TERM --kill-after=30s` with
`TICK_TIMEOUT < interval`; and reports the exit code the way the scheduler needs to
read it. That is not the same as passing it through. The tick's own return has to be
captured (`|| RC=$?`) before it can be examined at all, since `set -e` would
otherwise kill the wrapper first and turn a routine tempfail into a unit failure and
a false alert at three in the morning. Then: 0 is success, 75 is logged as TEMPFAIL
and ends the wrapper successfully - the database already carries `not_before` and the
backoff, so there is nothing for systemd to act on - and everything else re-exits
with the real code, because cron and systemd have to see a genuine failure. The unit fixes its own
environment (no reliance on shell profiles), bounds its wall clock with
`TimeoutStartSec` (15 min, with `TimeoutStopSec=2min`) - the only systemd directive
that works for a `Type=oneshot` unit, which has no default and ignores
`RuntimeMaxSec` - bounds memory *including swap* (`MemoryMax=8G`, `MemoryHigh=7G`, and
`MemorySwapMax=0` - without it `MemoryMax` is evaded through swap and the unit
legally thrashes the machine),
kills the whole control group, caps task count (`TasksMax=256`, `CPUQuota=200%`), and
sets `OOMPolicy=kill` so one OOM-killed process takes the unit down with it: a
half-dead run is worse than a dead one. `OnFailure=` points at a notify unit, which
is what makes a real failure code wake anybody. The timer is calendar-based
(`OnCalendar=*:0/15`, so the factory's clock is a quarter of an hour) with a
persistent catch-up and a fixed `RandomizedDelaySec=30`. User units require lingering
to be enabled, and journald must be persistent.

Never in the wrapper: `exit 0` for everything (a crash indistinguishable from
success breaks monitoring), or auto-stashing a dirty working tree (silently hiding
the operator's work). Millwright is indifferent to a dirty tree by construction -
the control checkout is untouched and workers live in their own worktrees; a dirty
*control* checkout opens a circuit rather than triggering a stash.

Every run writes a manifest: millwright and claude CLI versions, models,
`config_hash`, tick budgets. `claude --version` is checked against
`factory/compat.json`, which pins three things and not two: the tested version, the
minimum version, and the capabilities the factory requires of the CLI. Below the
minimum the circuit opens instead of a fleet starting; a version above the minimum
but outside the tested set notifies rather than passing in silence; and a version
that is new enough but has lost a required capability is the case a version number
alone cannot express, which is why the capabilities are pinned separately and
`doctor` asserts them against the CLI that is actually installed.

`millwright doctor` is mandatory before autonomy is enabled: database writable and
intact; repo, origin and base valid; authentication works with a minimal request;
configured models recognised; the CLI capabilities `compat.json` requires are
present in the CLI that is installed; worktree create/remove works; the test
baseline is known and green; disk, memory and directories; STOP semantics; and no stray
`ANTHROPIC_API_KEY` (it outranks OAuth and silently moves the factory from the
subscription onto per-token billing).

Two independent circuit breakers, because one counter breaks both modes: the
*infrastructure* breaker counts authentication errors, non-zero exits, timeout and
SIGKILL deaths (124, 137) and invalid JSON, and trips at two or three in a row (a
third run in a broken environment burns budget and litters the repo); the *gate*
breaker counts content rejections and trips at about five, because a rejection is a
normal outcome and a run of them signals a systematic queue problem, not an
outage. Open on: red base branch, unreachable origin, broken auth, exhausted daily
budget, either threshold, N post-merge regressions in a window, an incompatible CLI
or millwright version, a failed database integrity check, a failed doctor - the
first one from cron opens the circuit instead of starting a fleet - or a STOP
file. HALF_OPEN admits one
canary task, not the fleet. Resetting the infrastructure breaker is a human act and
must alert.

## 13. Authentication and security

**Authentication.** The operator runs on a subscription: `claude setup-token` issues
a year-long OAuth token (`sk-ant-oat01-...`) into `CLAUDE_CODE_OAUTH_TOKEN`, stored
via systemd encrypted credentials - which, unlike an environment variable, are not
inherited by the whole process tree, and `claude` has many children - or at least an
EnvironmentFile with mode 600, never in a crontab. An expired or revoked token
fails loudly in `-p` rather than hanging: `result` carries `OAuth token has expired`
or `Login expired · Please run /login` - the separator is U+00B7, not a hyphen,
and a detector built on a hyphen greps for a string the CLI never prints - and the
controller greps for those,
classifies `AUTH_FAILURE`, opens the circuit and raises an urgent alert - it is the
one failure class only a human can fix.

**Capabilities, deny by default.** Builder: read/edit/write/grep/glob plus policy-
scoped Bash; no merge, push, deploy or destructive docker, and no subagents except
on a task explicitly marked wide (section 7). Reviewer,
lens and refuter: read/grep/glob and read-only Bash; no edit or write. Normalizer
and goal evaluator: read-only context, no Bash unless explicitly needed.

**Three enforcement layers.** (1) CLI flags: `--permission-mode dontAsk` plus
explicit per-role `--allowedTools`/`--disallowedTools`. (2) The consumer's
`settings.json` deny list: pattern process kills, destructive docker, `git push
--force`, `git reset --hard`. (3) A `PreToolUse` policy hook checking capability
invariants, not just command names: paths stay inside the assigned workspace; no
writes to the control checkout or the factory database; no mutation of base-branch
refs; no push from a worker; no credential paths. The hook must be fast and carry
its own short timeout - a hung `PreToolUse` hook does not block the call, it just
delays it, so a slow hook is a fence with a hole. The second trap of this layer:
`-p` executes a project's hooks and `.mcp.json` with no trust dialog, which is a
fact for our own repositories and an attack surface in anyone else's.

**OS layer.** Every worker runs in its own process group and cgroup with memory and
CPU limits; an external `timeout -k` on the group kills it (SIGTERM, grace, SIGKILL)
and the workspace is kept for forensics. The timeout is set at two to three times the
typical duration of the call, and it is set whether or not the CLI is believed to
bound itself. Blind pattern-based process killing is forbidden to everyone,
always; workers may not kill anything outside their own children; the controller's
janitor may reap only specific PIDs selected by "parent is init, older than 120 s, command
line matches a worker".

**Sandboxing.** The built-in Claude Code sandbox is enabled for maximum autonomy,
with `failIfUnavailable`, no unsandboxed commands, a strict network allowlist whose
only member is `api.anthropic.com` (deny-by-default networking prompts
interactively, which in headless mode means death), and explicit deny rules on
credential paths - the sandbox restricts writes
by default while reads span the whole disk, `~/.ssh` and `~/.aws` included.

On a dedicated server the profile escalates: a devcontainer behind an egress
firewall, and network reachable only during the setup phase - cut before the agent
phase starts, with the setup script's secrets wiped first.

**Untrusted input.** Issue text, webhook payloads and third-party ticket fields are
*data, not instructions*, and enter a role prompt only inside an explicitly marked
untrusted wrapper.

**Kill switch.** The authoritative STOP file lives outside the repository at
`~/.config/millwright/<repo>/STOP`, where workers cannot write and `git clean`
cannot reach. `factory/STOP` is honoured too, as a convenience.

**Self-modification is a separate class.** An ordinary task may never change
`factory/**`, `.claude/settings.json`, millwright's own code, the scheduler units,
the security hooks or the merge policy - stage 1 catches it. Evolving the factory is
the `FACTORY_ADMIN` class: manual opt-in, its own branch, tests, shadow or canary
runs, independent senior review, explicit promotion. The factory must not quietly
rewrite its own gate in order to pass its own gate.

## 14. Observability

Required events: `RUN_STARTED/FINISHED`, `TASK_ENQUEUED/LEASED/DONE/BLOCKED`,
`WORKSPACE_READY`, `AGENT_STARTED/FINISHED`, `CHECK_STARTED/FINISHED`,
`FINDING_RAISED/REFUTED`, `GATE_PASSED/FAILED`, `INTEGRATION_STARTED/RETRY`,
`MERGED`, `POST_MERGE_PASSED`, `INFRA_RETRY`, `CIRCUIT_OPENED`, `NEEDS_SPEC` - into
both `events` and `events.jsonl`.

Metrics are computed from the database, never asserted:

```text
first_pass_verified_rate            usd_and_tokens_per_verified_merge
per_lens_blocker_survival           fix_cycle_net_new_defect_rate
verified_merge_rate                 queue_age p50/p95
infra_failure_rate                  integration_conflict_rate
post_merge_regression_rate          rollback_rate
cost_per_confirmed_blocker          false_blocker_rate
cache_read_share                    weekly_quota_burn
human_intervention_share            operator review time
```

A new engine rule must move one of these or it is deleted at the weekly review.

Three independent alarm echelons, because success at night is zero notifications
and failure must arrive by two independent paths: an external dead-man switch, pinged
when the tick starts and again with the code it exited on, scheduled with its own
grace period off this machine (the only thing that catches "never ran / machine
dead"); immediate urgent alerts on `AUTH_FAILURE`, circuit open, post-merge
regression and failed doctor, with a quieter channel for `BLOCKED`, `NEEDS_SPEC` and
no progress across N consecutive ticks - the one alarm that fires while the factory
runs cleanly and does nothing; and a morning
report from the database - merged hashes, blocked branches and reasons, NEEDS_SPEC,
spend in dollars, tokens and percent of the weekly cap, queue, next task, and the
wrapper's skip log, so a factory that has been paused by STOP for a fortnight is
visible rather than merely quiet - sent *always*, since a missing morning report is
itself a signal. Logs are JSONL with the
date in the filename and age-based deletion after 30 days, not logrotate. A successful tick does
not notify.

## 15. Exit codes

Defined once, in `src/controller/exit-codes.ts`, and used by every command:
`0` ok (including an empty queue), `70` internal error, `75` temporary failure
(the database already carries `not_before` and the backoff), `78` bad invocation or
configuration.

## 16. Configuration

One TOML file per consumer, `factory/millwright.toml`, carrying a top-level
`version` key - the hook every later migration hangs on - and sections for `repo`,
`controller` (tick limits, lease and heartbeat seconds, default attempt counters,
the module-span threshold above which the scheduler routes a spec to a scout
rather than a builder),
`concurrency` (builders, heavy tests, senior-model slots, `integrations = 1`),
`models.*` (id, effort, max turns, max USD per role; the id is a full model id and
never an alias, because an alias floats between releases and makes the run manifest
a lie), `budget`, `merge`, `deploy`,
`security`, `checks`, `notify`, and `reports_language` - the operator-facing report
language is a consumer parameter, while the core stays English. The starting values
in blueprint Appendix A are calibration knobs for the first 30-50 tasks, not
constants.

## 17. Roadmap

| Milestone | Content | Done when |
|---|---|---|
| M0 skeleton | TaskSpec schema, SQLite store, `enqueue`/`queue`/`status`/`doctor` | `kill -9` at any moment loses no task; doctor is honest |
| M1 one worker | workspace manager (worktree + cgroup), CLI backend, schema-driven builder, stages 0-2 | first task in shadow mode: candidate plus stage 0-2 verdicts |
| M2 full loop, one task | semantic reviewer, the seven-condition gate, serialized integration with CAS and trailers, fix cycle, reaper/lease | first-wave kill tests green; no double merge |
| M3 economics and parallelism | budgets and reservations, router, slots, conflict-aware scheduler, two builders | $/verified merge computed from the database; parallel run without conflicts |
| M4 unattended | tick wrapper, systemd timer, circuit breakers, notifications, morning report, full fault-injection suite | soak ladder through step 5 |
| M5 first consumer in production | `repo-truth` plugin, `checks.yaml`, queue migration, cron 24/7 | 30-50 real tasks; router and lens order recomputed from data |

## 18. Definition of done before the first crontab

The factory does not go into cron until its own fault-injection suite is green and
the soak ladder has been climbed. The suite lives in `test/faultinjection/` and is
the single home of those cases (kill points, resource failures, git races, policy
violations); the enumeration in blueprint section 15 is its origin and is not
restated here.

The soak ladder promotes only on measured thresholds, never on "looks fine". The
rungs, with the threshold that opens each one: shadow, build and verify with no
merge, promoted on an agreed number of tasks with zero policy violations ->
supervised auto-merge, one task per tick, promoted on zero double merges and a
false-block rate the operator accepts -> two parallel builders -> normal concurrency
-> unattended cron by day -> cron 24/7.

The pre-autonomy checklist - every guarantee that must hold before the first crontab
entry - stays in blueprint section 20 and is referenced from here, in that one
direction. It is the one part of the blueprint this document deliberately does not
absorb: a checklist restated in two places is a checklist that will be satisfied in
one of them (discipline 12).
