# Decisions (ADRs) - the published subset

The private repository carries 43 ADRs, measured on 2026-10-02 with
`git -C <repo> ls-tree --name-only main docs/decisions/ | wc -l` -> `43`.
Twenty-six of them are reproduced here: the ones that decide something a reader of
`DESIGN.md` cannot infer from the design itself. The numbering is the private
repository's and is left unrenumbered, so the gaps below are real gaps and not
lost files.

Cross-references of the form `docs/decisions/NNNN-...` inside these files and
inside `DESIGN.md` name files in the private repository. Only the twenty-six
listed here are published.

Where an ADR quotes the operator in Russian, the Russian is kept verbatim - it is
the authority a decision stands on, and a translation is a paraphrase - with the
English translation beside it.

A name in angle brackets inside a command or a quoted output line - `<repo>`,
`<repo-truth>`, `<home>`, `<control-root>`, `<claude-install>`, `<transcript>`,
`<subagent>`, `<command>` and the like - stands for a path or an identifier on
the private machine that is not published. The command is otherwise as it was
run, and its output is otherwise quoted as it printed.
Inside a quoted message, a seat's own name is replaced by a description in
square brackets, and a row of a session transcript is named by its time
rather than by its identifier.

| ADR | Filed | What it decides |
|---|---|---|
| [0002](0002-fix-cycle-verification.md) | 2026-08-17 | A fix cycle answering a verifier earns a second independent verification pass; when that is mandatory rather than optional. |
| [0004](0004-m0-exit-and-queue-composition.md) | 2026-08-18 | The M0 exit review: five measured defects, what holds the milestone open and what does not, and the third fix lane. |
| [0005](0005-model-layout-and-the-foreman-seat.md) | 2026-08-19 | Which model and effort each seat runs on, and the acceptance seat (the foreman) that ADR 0001 had no row for. |
| [0017](0017-m0-62-fourth-stop-and-the-split.md) | 2026-08-24 | One task stopped four times: the operator splits it rather than re-issuing it a fifth time. |
| [0018](0018-the-roadmap-drift-and-the-three-gates.md) | 2026-08-25 | The queue filed findings and planned nothing; three gates end that drift, and a finding may not outrank the roadmap silently. |
| [0020](0020-the-controller-may-give-up-on-one-task.md) | 2026-08-29 | The controller is allowed to give up on one task, and the three questions the M2 chain could not answer. |
| [0021](0021-m3-the-chain-the-band-the-marker-and-the-contracts.md) | 2026-08-30 | M3 as an ordered chain: the planning band, the provenance marker, and the contracts the design left open. |
| [0022](0022-the-comparison-reconciled.md) | 2026-08-30 | The factory's own output compared against a separate research pass, reconciled to what has practical value. |
| [0024](0024-m3-exit-and-the-m4-chain.md) | 2026-09-08 | The M3 exit: what the milestone proved, the cost-per-verified-merge figure that could not be computed and why, and M4 as an ordered chain. |
| [0025](0025-the-opus-weekly-cap-has-no-channel.md) | 2026-09-10 | The bigger model's own weekly window is not readable by anything the factory can call, so an escalation is bounded by the general cap instead. |
| [0026](0026-m4-exit-and-the-ladder-nobody-climbed.md) | 2026-09-11 | Every M4 mechanism landed and M4's definition of done was not met: a milestone exits on a reading, not on a count of landings. |
| [0028](0028-the-loop-closes-on-repo-truth.md) | 2026-09-19 | A gate refusal buys a fix cycle - the edge the state machine did not declare - and the seats a bounded tick cannot hold are carried to the next pass rather than killed by it. |
| [0029](0029-the-four-answers-and-the-word-on-one-tick.md) | 2026-09-21 | Four operator answers on what a policy breach is, who writes a read-only seat's scratch repository, and what a fix cycle's floor covers - plus the rule that a sanction to run the factory against a live repository covers one run and not a campaign. |
| [0030](0030-the-word-on-the-tick-and-the-two-decisions-delegated.md) | 2026-09-22 | One more word, one more tick; and two decisions the operator handed to the seat under a single criterion - a working factory - with the seat's answers: a home of its own for every seat of a pass, and a policy breach read by the stage-1 rule it breaks rather than by the fence that held it. |
| [0031](0031-the-word-on-the-series-and-the-word-on-the-models.md) | 2026-09-23 | A bounded series of five ticks and what it measured; every seat named by a full model id, never by a tier or an alias that can move under it; builder subagents kept on the cheaper model on bench data; the factory's main builder and reviewer left open, with its first ten priced merges as the next data point. |
| [0032](0032-the-words-on-the-second-series-and-the-debug-mode.md) | 2026-09-26 | A second series of five, a named and reversible exception that moved the factory's own leftovers out of the second repository, and a debug mode in the factory itself: the evidence a later question needs is kept by default, and only a worker's transcript waits behind a switch that is off. |
| [0033](0033-the-budget-exit-the-design-names-is-not-the-clis.md) | 2026-09-26 | The exit code `DESIGN.md` section 7 gives a budget overrun appears not to be the one the CLI produces: the intent of the sentence stands, the mechanism moves to what the CLI writes in its envelope, and the design's own text waits for the operator's word. |
| [0034](0034-the-words-of-the-night-on-the-fast-mode.md) | 2026-09-27 | The fast mode: the critical path first, the next block opened while the seat's own verifier of the previous landing still runs, and a finish line - only a finding that blocks the first priced merge may outrank the roadmap. |
| [0035](0035-the-temporary-answer-on-condition-2.md) | 2026-09-28 | Gate condition 2, by the operator's word and marked temporary by it: an entry of the reviewer's unverified list that points at a stage or check which ran - passed or failed - leaves the count; one pointing at a stage that did not run still counts, and so does prose. |
| [0036](0036-the-temporary-mark-on-the-reviewers-list-scope.md) | 2026-09-28 | The scope of the reviewer's unverified list - only what the spec itself states - is marked temporary by the operator's word. |
| [0037](0037-the-wall-stays-and-the-fix-walk-is-carried.md) | 2026-09-28 | The tick's wall is not raised; instead a fix cycle's opening pass must hold only its builder, and a fix walk the pass cannot hold is carried to the next pass - and, by the seat's reading of the word, an operator verb that releases a blocked row. |
| [0038](0038-the-unconfigured-stage-leaves-condition-2.md) | 2026-09-29 | A later word on 0035's rule, for one case: an entry pointing at a stage not configured for the task at all leaves condition 2's count - with the record's own correction that the remedy the question named, configuring a smoke, is an unbuilt row. |
| [0039](0039-the-factory-fixes-its-own-gate-first.md) | 2026-09-29 | On the second repository the factory does the work itself - no merge by hand, since a hand merge proves nothing about the factory - its gate is fixed first, and a mutation measurement its time budget cut is finished in a later pass rather than judged. |
| [0041](0041-the-holdout-rule-the-scripts-rule-and-the-ceiling-at-95.md) | 2026-09-30 | Three operator words: on the second repository every `not_done_if` line of a spec is covered by a held-out check or a named deterministic one, and condition 1 stops passing a spec that declares none; the gate refuses a candidate that changes the `scripts` field of `package.json`; and that repository's weekly ceiling moves to 95 by both of its keys. |
| [0042](0042-the-ten-task-programme-and-its-standing-tick-word.md) | 2026-09-30 | A ten-task programme on the second repository, run one tick at a time under a standing word at the ladder's first rung, its task packet approved by the operator and the move to rung 2 left to him - and the fact that the successor seat's first tick under that standing word was refused by the agent harness before it ran. |
| [0043](0043-the-two-retirement-rules-permanent-and-bound-to-the-holdout.md) | 2026-10-01 | The temporary rules of 0035 and 0038 become permanent but bound to the holdout: an unverified entry either rule would retire leaves condition 2's count only on a candidate whose held-out checks ran and passed; 0036's scope is made permanent as it stands. |

Fourteen ADRs were filed since the previous published snapshot of 2026-09-22
(0030 to 0043). Thirteen of them are added above. 0040 is held: its one
decision is the figure at which the seats that build the factory pause their
own spending - an operating budget of the build, not a decision about the
design - and the open question it recorded, whether a spec must declare a
held-out check for its `not_done_if` lines, is published inside 0041, which
quotes the question whole and records the answer.
Two older ones are still deliberately not reproduced.
0023 (the public showcase and the second repository) is the decision that defines
this repository's own publication boundary, and its load-bearing half is the list
of what is never published; publishing that list would publish the shape of what
it excludes. 0027 (the M5 chain and the run on the second repository) records a
chain that is still in flight - its central row has not landed - and this
repository does not carry a claim ahead of the commit that proves it
(`PRINCIPLES.md`, discipline 3). Both are candidates for a later snapshot.

0020 is reproduced with one paragraph it did not carry at the 2026-09-14
snapshot: the question its section 2 (a) left open was closed on 2026-09-19, and
0028 is where it was closed. 0005 is reproduced with the amendment its original
gained on 2026-09-23 - every seat named by a full model id - which 0031 records
the words for. 0035, 0036 and 0038 are reproduced as their originals stand,
with the marks "temporary" they carry: 0043 is the later record that answers
them, and none of the three was edited by it.

The `Filed` column is the date of the commit that added the file, measured on
2026-10-02 with, for each file:

```sh
git -C <repo> log --diff-filter=A --format='%ad' --date=short main -- docs/decisions/<file> | tail -1
```
