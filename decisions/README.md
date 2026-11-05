# Decisions (ADRs) - the published subset

The private repository carries 65 ADRs, measured on the evening of 2026-11-05 with
`git -C <repo> ls-tree --name-only main docs/decisions/ | wc -l` -> `65`.
Thirty-six of them are reproduced here: the ones that decide something a reader of
`DESIGN.md` cannot infer from the design itself. The numbering is the private
repository's and is left unrenumbered, so the gaps below are real gaps and not
lost files.

Cross-references of the form `docs/decisions/NNNN-...` inside these files and
inside `DESIGN.md` name files in the private repository. Only the thirty-six
listed here are published.

Where an ADR quotes the operator in Russian, the Russian is kept verbatim - it is
the authority a decision stands on, and a translation is a paraphrase - with the
English translation beside it.

A name in angle brackets inside a command or a quoted output line - `<repo>`,
`<repo-truth>`, `<home>`, `<control-root>`, `<claude-install>`, `<transcript>`,
`<subagent>`, `<command>`, `<lister>`, `<first-consumer>` and the like - stands for a path or an identifier on
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
| [0045](0045-m0-222-behind-the-three-rt-08-waits-and-item-4-taken.md) | 2026-10-03 | Three operator words: the metric by model and role is built right after the three rows already above the roadmap line, before the builder's model is compared, and the reviewer keeps its model until that comparison; the second repository's next task waits for those four rows, with ticks there stopped meanwhile; and a batch of edits to the factory's procedures and to `DESIGN.md` sections 7, 8 and 13 is taken - among them the default 0032 left to the operator: a worker's transcript stays off. |
| [0046](0046-the-m0-117-ledger-decided-and-the-spend-loop-row-above-the-line.md) | 2026-10-04 | The operator's word on a state-machine edge a landing had added and asked him for: a verified row that no integration claimed returns to the retry queue instead of being reported on every sweep, a recovery with no edge of its own comes back the same way, and the loop that edge opens under a lock that stays held gets a row of its own, above every roadmap row, before any tick resumes. |
| [0048](0048-the-written-procedure-for-soak-rungs-3-4-and-5.md) | 2026-10-05 | The written procedure for the soak ladder's third, fourth and fifth rungs: which clauses each climb reads and whose they are - the design's, the code's or the operator's - what a seat prints before it puts a climb to him, and what refuses a promotion in code and what does not. It takes no promotion. |
| [0049](0049-the-tests-only-mark-on-stage-5-bound-to-the-holdout.md) | 2026-10-10 | A candidate that changes only tests: stage 5 writes a positive mark on its record when every changed path is a test path, and the reviewer's pointer at that record leaves condition 2's count only when the candidate's held-out checks ran and passed; the other half of the question - an unverified entry blocking only when it is about a stated requirement - is set aside, because the controller cannot yet tell. |
| [0050](0050-a-hung-mutant-is-detected-and-the-bound-is-priced-from-the-baseline.md) | 2026-10-10 | A mutant run past its bound counts as a detected mutant, apart from the kills, when a control run of the unmutated file finishes inside the same bound; the bound per mutant is priced from the file's own baseline run with a floor of about 15 seconds in place of 60; and a stage-5 pass that leans on such a count is bound to the held-out checks. The proposal is recorded as the seat's, not the operator's. |
| [0051](0051-a-candidate-set-aside-with-no-finding-is-resumed-and-the-lock-loser-waits.md) | 2026-10-12 | The operator's words on the rows his freeze of 2026-10-11 keeps: a candidate the gate refused with nothing measured false is checked again by the next pass instead of rebuilt; a candidate refused at the integration lock its own pass holds waits for its sibling's integration and lands on top of it in the same pass; and the uncharged carry of one candidate is bounded before the fourth rung. |
| [0055](0055-the-operator-word-of-2026-10-17-a-second-reject-closed-by-tests-or-comments-lands.md) | 2026-10-18 | A rule of the hand-run blocks that build the factory: when an independent verifier's second rejection concerns only tests or comments, the block fixes them within the same attempt and lands with two quality attempts counted; a second rejection on the code's logic still stops the block. |
| [0059](0059-the-operator-word-of-2026-10-21-a-tick-refuses-an-untested-cli.md) | 2026-10-21 | A tick refuses, before any worker, a version of the coding agent's CLI other than the one the consumer has tested; and the janitor's test for an orphaned worker process accepts the user's service manager as well as init as its parent, with every other clause unchanged. |
| [0060](0060-the-operator-words-of-2026-10-22-stage-five-unfenced-the-holdout-rerun-and-the-verified-merge.md) | 2026-10-22 | A test-strength stage handed no fence starts nothing and answers `error`; a merged task whose held-out check fails after later merges goes from DONE to BLOCKED by a second withdrawal edge, with an incident and a notification and no revert; and what counts as a verified merge: how many merges the post-merge check measured is printed beside the count, and once the second repository has five merges in a row measured `passed`, the objective divides only by those. The first decision was built when it was taken; the rows that build the other two were still queued at the snapshot of 2026-10-30. |
| [0065](0065-the-operator-word-of-2026-11-01-rule-a-a-worst-case-pass-within-the-tick-cap.md) | 2026-11-01 | A configuration whose worst-case pass - the dearest set of seats one dispatch opens, at the configured ceilings - exceeds the tick's dollar cap is refused when it is resolved, so the cap stays a real cap rather than one read per seat; the shipped scout ceiling moves so that the shipped tables pass, a cap lowered at run time is left outside the rule, and the tick wrapper's dollar floor rises to the worst-case set. |

Two ADRs were filed after the previous published snapshot, of the night
of 2026-10-30: 0064 on 2026-10-31 and 0065 on 2026-11-01. Two earlier ones
changed: `git -C <repo> diff --name-only b72a2ba..main -- docs/decisions/ | wc -l`
printed `4` on the evening of 2026-11-05 - the two new files, 0026 and
0062. Each of those two gained a dated note of 2026-11-03 on what M0-347's
landing covered; 0026's copy above carries its note under the same
substitutions as before, and 0062 stays held, its note pointing at
0026's. 0065 is reproduced above, sanitized as 0060 is: the transcript's
path and name and the row and session identifiers removed, rows named by
their time, seat names removed, local times written as such, and the
paths of a command written as `<home>`, `<repo>` and `<repo-truth>`. 0064
is held: its words are on the factory's plans, the seats' night routine,
a research the operator asked for and a spending word for a pilot -
material this repository does not publish, the reasons 0040, 0062 and
0063 are held. Its one decision a reader of this repository needs, two
more rows to land before a timer is armed - M0-316 and M0-334 - is in
`TIMELINE.md`'s milestone table as what was done.

Thirteen ADRs were filed between the snapshots of the morning of
2026-10-12 and the night of 2026-10-30, between 2026-10-12 and
2026-10-26: 0051 to 0063.
No earlier ADR changed: `git -C <repo> diff --name-only 378c366..main -- docs/decisions/ | wc -l`
printed `13` on the night of 2026-10-30, the thirteen new files and no other,
so every earlier copy here stands as it was published. Four of the thirteen
are reproduced above - 0051, 0055, 0059 and 0060 - sanitized as 0049 and
0050 are: transcript paths and row identifiers removed, rows named by their
time, seat and session names removed, a private configuration path written
as `<control-root>`, the tool that lists a transcript's rows as `<lister>`,
the first consumer's checkout as `<first-consumer>`, and the private archive
named as such. Nine are held:

- 0052 (2026-10-13) records five decisions of one night; two of them - a
  spending word for the seats that build the factory, and a documentation
  agent the operator runs across his own projects split from the factory's
  own - concern material this repository does not publish, the reason 0040
  and 0047 are held. Its rule on gate condition 2 is built by M0-297, in `TIMELINE.md`'s
  milestone table.
- 0053 (2026-10-15) records a day of the operator's words, several of them
  on the seats' spending and on the session tooling, which this repository
  does not publish. The count of overturned refusals it decides is built by
  M0-238, in the same table, and the ladder readings that rest on it are in
  `TIMELINE.md` with their dates.
- 0054 (2026-10-17): the optional TaskSpec field it takes is in `DESIGN.md`
  section 5, and its other word, how often the foreman seat is replaced, is
  an operating rule of the seats that build the factory, held for the reason
  0040 is.
- 0056 (2026-10-19): its word answers a message that also carries the
  operator's session tooling; what it decides - one exit code for a refusal
  to spend, a queue row cancelled, and `DESIGN.md` section 7 brought to the
  order the tick runs in - is readable in `DESIGN.md` sections 7 and 15 and
  in M0-153's row of the milestone table.
- 0057 (2026-10-20): two of its three words are the same operating rule of
  the foreman seat as 0054's; the third, a silence bound that does not take
  a silent but working worker for a hung one, is built by M0-313, in the
  milestone table.
- 0058 (2026-10-21) records fourteen answers of one evening, several of
  them on the operator's private tooling; the version protection it leads
  to is 0059, reproduced above.
- 0061 (2026-10-24): its argument for the soak ladder's fifth rung on the
  second repository as the factory's next proof rests on a comparison with
  the first (private) consumer, which this repository does not publish -
  the reason 0027 is held. The promotion that followed is in `TIMELINE.md`,
  "Where the snapshot stands".
- 0062 (2026-10-24) and 0063 (2026-10-26) record the operator's words on the
  factory's plans beyond the second repository, on an audit of how the seats
  work and on the seats' night routine - none of which this repository
  publishes. The order of work they set for the fifth rung is in
  `TIMELINE.md` as what was done.

Two ADRs were filed between the snapshots of the afternoon of 2026-10-09
and the morning of 2026-10-12, both on 2026-10-10: 0049 and 0050, the operator's words on
two of the gate's false refusals - a tests-only candidate's empty mutation
measurement, and a mutant run that hangs. Both are reproduced above,
sanitized as 0041 to 0048 are: transcript paths and row identifiers removed,
rows named by their time, seat and session names removed, a private
configuration path written as `<control-root>`, and the private archive
named as such. No other ADR changed:
`git -C <repo> diff --name-only 886b98d..main -- docs/decisions/` printed
those two files and no other on 2026-10-12, so every earlier copy here stands
as it was published.
No ADR had been filed or changed between the snapshots of the morning of
2026-10-06 and the afternoon of 2026-10-09
(`git -C <repo> log --oneline b2019e1..886b98d -- docs/decisions/ | wc -l`
-> `0` on 2026-10-12), and none had been filed between that of 2026-10-06
and the one of the morning of 2026-10-05. 0048 is reproduced with the five dated corrections its
original gained on 2026-10-06; each keeps the sentence it corrects verbatim, as
the record of what was written.
Three ADRs were filed between the snapshots of 2026-10-03 and 2026-10-05, on
2026-10-04 and 2026-10-05: 0046, 0047 and 0048. 0046 and 0048 are added above. 0047 is
held, for the reason 0023 is (below): one of its five decisions, and the words
it quotes for it, concern material this repository does not publish. Its
other decisions a reader of this repository needs - the stage-1 row of
`DESIGN.md` section 8 rewritten to name every condition stage 1 runs, the
second repository's last task reissued with the interface the operator chose,
and the M5 chain's central row closed - are in `DESIGN.md` itself and in
`TIMELINE.md`, "Where the snapshot stands".
Two ADRs were filed on 2026-10-03: 0044 and 0045. 0045 is reproduced above.
0044 is held, for the reason 0023 is (below): one of its five decisions sets
a rule for what the factory's public outputs may carry, and publishing it
would describe what the rule keeps out. Of its other decisions, the two a
reader of this repository needs - the second rung of the soak ladder taken on
the second repository, with shadow mode off, and the third left waiting - are
stated with their facts in `TIMELINE.md`, "Where the snapshot stands".
Of the fourteen filed between the snapshots of 2026-09-22 and 2026-10-02
(0030 to 0043), thirteen are reproduced. 0040 is held: its one
decision is the figure at which the seats that build the factory pause their
own spending - an operating budget of the build, not a decision about the
design - and the open question it recorded, whether a spec must declare a
held-out check for its `not_done_if` lines, is published inside 0041, which
quotes the question whole and records the answer.
Two older ones are still deliberately not reproduced.
0023 (the public showcase and the second repository) is the decision that defines
this repository's own publication boundary, and its load-bearing half is the list
of what is never published; publishing that list would publish the shape of what
it excludes. 0027 (the M5 chain and the run on the second repository) was held
while its chain was in flight, because this repository does not carry a claim
ahead of the commit that proves it (`PRINCIPLES.md`, discipline 3). That
reason has lapsed: every row of the chain is closed - its central row on
2026-10-04, on the strength of the first merge the gate made in the second
repository, and its last three on 2026-10-05 - while the milestone the chain
plans is not done (`TIMELINE.md`, "Where the snapshot stands"). It stays held
for now for another reason: its argument rests in several places on the run of
the first (private) consumer and on 0023, neither of which this repository
publishes, and a copy without those passages would not carry the argument.
Both are candidates for a later snapshot.

0020 is reproduced with one paragraph it did not carry at the 2026-09-14
snapshot: the question its section 2 (a) left open was closed on 2026-09-19, and
0028 is where it was closed. 0005 is reproduced with the amendment its original
gained on 2026-09-23 - every seat named by a full model id - which 0031 records
the words for. 0035, 0036 and 0038 are reproduced as their originals stand,
with the marks "temporary" they carry: 0043 is the later record that answers
them, and none of the three was edited by it. 0026 is reproduced with the
dated note its original gained on 2026-11-03, on what M0-347 covered of the
three conditions its section 3 (f) names; the paragraph the note follows is
kept as the exit reading wrote it.

The `Filed` column is the date of the commit that added the file, measured on
the evening of 2026-11-05, for all thirty-six, with, for each file:

```sh
git -C <repo> log --diff-filter=A --format='%ad' --date=short main -- docs/decisions/<file> | tail -1
```
