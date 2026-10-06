# ADR 0048 - The written procedure for the soak ladder's rungs 3, 4 and 5: the clauses each climb reads, what a seat prints, and what refuses it

Date: 2026-10-05. Context: a block's record - block #183, the row
M5-04@fb8521337975, hand-run under `.claude/commands/block.md` - and not an
operator word: no word of his is recorded or read anew here. `main` stood at
`054b668 054b668` when this record was written -
`git rev-parse HEAD origin/main | cut -c1-7 | paste -sd' '` printed
`054b668 054b668` on 2026-10-05 at 01:36. The block's diff is this record
and one case under `test/unit/`; nothing under `src/`, `factory/`,
`scripts/`, `.githooks/`, `.claude/`, `DESIGN.md`, `CLAUDE.md`,
`PRINCIPLES.md` or the private archive was touched, and nothing was written in
`repo-truth`.

**This record is a procedure a seat follows and it takes no promotion.** The
row's outcome is its one home: "any of them is taken only by a seat on the
operator's word, and this row takes none." The rule the procedure executes
is `DESIGN.md` section 18's sentence, quoted as that file writes it:

    The soak ladder promotes only on measured thresholds, never on "looks fine".

Every statement below says whose it is: the design's (a quoted sentence of
`DESIGN.md` section 18), the code's (a quoted anchor in a file this block may
not edit), or his (pointed at, never restated). Code is cited by quoted
anchor and never by line number.

## 0. Which ladder, and where the procedure starts

THE LADDER IS PER REPOSITORY. `  soakRung(repoId: string): SoakRungRow {`
(src/store/store.ts) and
`export function readSoakFacts(source: FactSource, repoId: string, since: string): SoakFacts {`
(src/controller/ladder.ts) both take a repository id, and both `ladder`
verbs resolve the repository from the working directory they are run in. A
reading of a repository's ladder is therefore a verb run from that
repository's own checkout - a seat's act, and never this block's.

WHICH OF THE THREE IS NEXT, AS A DATED RECORD. Rung 3 is next on repo-truth
per its LADDER_RUNG_CHANGED seq 1946 (2026-10-02T07:12:08Z, rung 1 -> 2, by
operator; ADR 0044 section 0 (f)). This block's own file read of
repo-truth's journal, `factory/state/events.jsonl` read as a file and never
through a verb, printed 2 at 01:40 on 2026-10-05 for
`grep -c '"type":"LADDER_RUNG_CHANGED"' factory/state/events.jsonl` - seq
47 (2026-09-14T12:11:12.840Z, rung 1 to rung 1, the verb opening the
window) and seq 1946. That reading is a record of that minute and not of
the ladder's state: an event says a rung was written, and the `soak_rung`
row is the state. Before any climb a seat re-reads both, with its own date.

This repository's own journal held no such event at the same minute -
`grep -c 'LADDER_RUNG_CHANGED' factory/state/events.jsonl` printed 0 at 01:40
on 2026-10-05 in millwright's checkout - so no store write had recorded a
rung there by then. A repository with no rung row reads as the rung the
store synthesizes, `export const DEFAULT_RUNG = 1;` (src/store/soak.ts); the
event count says no write happened through the store, and it is not a
reading of the row. The lists of section 1 cover the climbs to rungs 3, 4
and 5 only; the form of sections 2 to 4 is the form of any climb.

## 1. The clauses each climb reads

THE ONE HOME IS `RUNGS`. `export const RUNGS: readonly Rung[] = [`
(src/controller/ladder.ts) holds every rung, and a rung's `promotion` list
is what a promotion OFF that rung reads -
`   * Every clause that must hold before a promotion OFF this rung is offered.`
So the climb to rung 3 reads rung 2's list, the climb to rung 4 reads rung
3's, and the climb to rung 5 reads rung 4's. The clause names are
`export const CLAUSE_NAMES = ["tasks", "no_policy_violations", "no_double_merges", "false_block_rate"] as const;`.

The three lists, as read at 054b668 on 2026-10-05. They are a copy of
`RUNGS`, and the case
`it("keeps ADR 0048's three climb lists equal to RUNGS, by name and order, one rung at a time", ...)`
in test/unit/soak-ladder.test.ts reads this block from disk and fails when
any line of it and the rung it names disagree - so a later change of a list
meets that case, and the record then needs a dated correction by a row or a
carrier that may write `docs/decisions/**`. That is the cost of keeping the
lists here, and it is paid on purpose: no other case pins rungs 3 and 4's
lists by name.

<!-- climb-lists:begin -->
- climb to rung 3 reads rung 2's list: tasks, no_double_merges, false_block_rate
- climb to rung 4 reads rung 3's list: tasks, no_policy_violations, no_double_merges, false_block_rate
- climb to rung 5 reads rung 4's list: tasks, no_policy_violations, no_double_merges, false_block_rate
<!-- climb-lists:end -->

WHOSE CLAUSES THEY ARE.

- The climb to rung 3 reads `DESIGN.md` section 18's second arrow - "promoted
  on zero double merges and a false-block rate the operator accepts" - plus
  `tasks`, one clause more than the design states there. Rung 2's `note` in
  `RUNGS` gives the code's reason: "zero double merges over zero tasks is a
  promotion on silence, and section 18's own first sentence forbids that."
  *[CORRECTED 2026-10-06 by carrier #95: "first" is the code's ordinal and
  not the design's. `DESIGN.md` section 18 opens with the sentence that
  begins "The factory does not go into cron until its own fault-injection
  suite is green and", and the threshold sentence, "The soak ladder promotes
  only on measured thresholds, never on "looks fine".", opens its second
  paragraph. This record corrects no code: the quote stays as the code's
  reason at 054b668. The bullet is kept verbatim as the record of what was
  written.]*
- The climbs to rungs 4 and 5 read lists the design never states. The
  `RUNGS` docstring says so -
  ` * THE DESIGN STATES A THRESHOLD FOR THE FIRST TWO ARROWS AND FOR NO OTHER, and`
  - and rung 3's `note` repeats it: "The design names no new threshold above
  rung two, so this rung carries every clause it has already stated". Those
  four-clause lists are the code's decision, landed by M4-07 (merged
  2a007ab); they are neither the design's sentence nor his word.

WHERE THE PROCEDURE STOPS. The code offers no promotion off rung 5, because two of
the three disjuncts of one condition in `promotionOffer` hold there,
`  if (rung.promotion.length === 0 || next === null || !next.withinDoD) {`:
rung 5's own list is empty (`    promotion: [],`), AND rung 6
(`    name: "cron 24/7",`) carries `    withinDoD: false,`, outside the
definition of done that `TOP_RUNG_IN_DOD` derives from the table. Rung 6's
threshold - in `RUNGS`' terms, rung 5's list - is M5-07's subject and not
this record's.
*[CORRECTED 2026-10-06 by carrier #95: rung 5's own list is no longer
empty. Since 8da69af (M5-07, merged 7cb3e31) its entry under
`    name: "unattended cron by day",` (src/controller/ladder.ts) carries the
four clauses -
`git log -S'promotion: ["tasks", "no_policy_violations", "no_double_merges", "false_block_rate"],' --format='%h %ad' --date=short 5bbff03 -- src/controller/ladder.ts`
printed 8da69af 2026-10-05 (rung 5's list) and ead4813 2026-09-11 (M4-07,
rungs 3 and 4) on 2026-10-06. So one disjunct of the three holds there -
rung 6's `withinDoD: false` - and the code still offers no promotion off
rung 5. That list is rung 6's threshold, M5-07's, written down in
factory/systemd/RUNG-6.md. The paragraph is kept verbatim as the record of
what was written.]*

## 2. The clauses, their facts and their bounds

`evaluateClauses` (src/controller/ladder.ts) is the one home of every
comparison; the table below is a reading of it.

| clause | the fact, as `ladder status` prints it | met when (the code) | the bound, as the verb spells it |
|---|---|---|---|
| `tasks` | `fact.tasks` - the distinct task stems with a gate verdict in the window (`    if (GATE_EVENTS.includes(event.type)) judged.add(stem);`) | `          met: facts.tasks >= tasks,` | "at least <n> ([ladder] tasks_per_rung)" |
| `no_policy_violations` | `fact.policy_violations` plus `fact.policy_breaches` - unreadable refusal records and stage-1 breaches of `BREACH_CONDITIONS`; `fact.refusals_held` is counted apart and is no violation | `          met: facts.policyViolations + facts.policyBreaches === 0,` | "exactly 0 unreadable refusal record(s) and stage-1 breach(es)" |
| `no_double_merges` | `fact.double_merges` (`  const doubleMerges = [...merges.values()].filter((count) => count > 1).length;`) | `          met: facts.doubleMerges === 0,` | "exactly 0" |
| `false_block_rate` | `fact.false_block_percent`, over `fact.gate_refusals` and `fact.overturned_refusals` | `          met: facts.falseBlockPercent !== null && facts.falseBlockPercent <= maxPercent,` | "at most <n>% ([ladder] max_false_block_percent)" |

THE FIGURES ARE HIS. Two bounds carry a configurable figure, and this record names each
by its configuration key and its code default and states no figure as his:

- `[ladder] max_false_block_percent`, code default 10
  (`  max_false_block_percent: percent("The highest share of gate refusals the operator accepts as false.", 10),`,
  src/controller/config.ts). The figure is the one `DESIGN.md` section 18
  calls "a false-block rate the operator accepts".
- `[ladder] tasks_per_rung`, code default 10
  (`  tasks_per_rung: positive("Tasks a rung must judge cleanly before the next rung is offered.", 10),`).
  The figure is the one section 18 calls "an agreed number of tasks".

*[CORRECTED 2026-10-06 by carrier #95: "THE FIGURES ARE HIS." stands bare
here, while section 7's bracket of 2026-10-05 - the one under its bullet
that opens "- **The figures** of `[ladder] tasks_per_rung` and" - marks the
same claim THE SEAT'S reading, **[operator-confirmable]**. This bracket
points at that one and answers nothing of the rung-3 research's section 7
item 9. The heading
is kept verbatim as the record of what was written.]*

A consumer's `factory/millwright.toml` may set either key; a default is not
a figure anybody agreed to. As a dated reading only: repo-truth's
`factory/millwright.toml` held no `[ladder]` block on 2026-10-05 at 01:40 -
`grep -n -A4 '^\[ladder\]' factory/millwright.toml` over it printed nothing,
rc 1 - so a measurement there at that minute compared against the code
defaults.
*[CORRECTED 2026-10-05 by carrier #93: this paragraph's first sentence has
two halves. That a consumer's file may set either key is the schema's, the
one the loader reads (`const LADDER_FIELDS = {`, src/controller/config.ts).
That a default is not a figure anybody agreed to is a reading of 2026-10-05
and THE SEAT'S, **[operator-confirmable]**, neither the code's nor his:
whether the two code defaults are figures he agreed to is the question the
rung-3 research of 2026-10-03 puts to him in its section 7 item 9 ("The
thresholds for 3 -> 4."), which stays open and his, and this record does not
answer it. The sentence is kept verbatim as the record of what was
written.]*

THE WINDOW. Every fact is counted from the current rung's own `since`
(`    if (Number.isNaN(at) || Number.isNaN(windowStart) || at < windowStart) continue;`),
and a climb restarts it (`    const changed = !existing || previous.rung !== input.rung;`,
`recordSoakRung` in src/store/store.ts). The tasks that earned one rung are
not the tasks that earn the next.
*[CORRECTED 2026-10-06 by carrier #95: the window is a time filter over
events. `readSoakFacts` (src/controller/ladder.ts) skips an event older
than the rung's `since` (the line quoted above) and adds a task's stem for
every gate event inside the window
(`    if (GATE_EVENTS.includes(event.type)) judged.add(stem);`), so a task
judged on both sides of a climb counts in both windows: verdicts, not
tasks, separate them (block #183's NIT-1). The sentence is kept verbatim as
the record of what was written.]*

THE CLAUSE THAT CAN BE UNMEASURED. The rule is the code's:
` * A clause whose fact is null is NOT MET, and that is the rule that keeps an`.
Of the four clauses' facts only the false-block rate can be null
(`  readonly falseBlockPercent: number | null;`); the verb prints it
"unmeasured", and this procedure never counts an unmeasured clause as met.
The other three facts are counts and are never null: over an empty window
`no_policy_violations` and `no_double_merges` print 0 and "met", and of
these three only `tasks` refuses the silence - the fourth, the false-block
rate, is null there and NOT MET by the rule above. A seat therefore reports a zero-count "met"
as evidence only beside a met `tasks` clause, never alone.

THE OVERTURN. The false-block fact counts a gate refusal in the window as
overturned when three things hold together: the refusal names a SHA, its
stem recorded a MERGED in the same window
(`    if (refusal.candidateSha === null || !mergedStems.has(refusal.stem)) continue;`),
and some row of the stem still carries the refused SHA
(`    if (refusal.rows.some((row) => row.candidate_sha === refusal.candidateSha)) overturned += 1;`).
A refused task that has not merged in the window is not counted, whatever
its row still carries.
Which reading of "overturned" is taken is his - M0-238's outcome
paragraph that opens "THE OVERTURN RULE, 2026-10-03" holds the question, and
this record decides nothing about it.

## 3. What a seat prints before it puts a climb to the operator

1. **The offer, whole.** `millwright ladder status`, run from the checkout of
   the repository whose ladder is climbed, printed whole with the command,
   the working directory and `date`: `rung`, `since`, `next`, the eight
   `fact.*` lines, every `clause.<name>` line, `offer` and `offered`
   (`function formatLadderStatus(offer: PromotionOffer): string {`, src/cli.ts).
   Each clause line is the verb's own, spelled by `ladderOfferFields`:
   "<fact or unmeasured>, wants <bound> - met" or "- NOT MET". That line
   carries each clause, its measured value AND its bound, and a report of a
   promotion that quotes the values without the bounds does not meet this
   procedure - nobody could check the arithmetic. The record of the climb
   of 2026-10-02 is that case: the row's outcome says its archive entry
   "quotes each clause with its value and the verb's own lines, and no
   bound".
2. **The arithmetic, checked.** For each clause the seat compares the fact
   with the bound as printed, and says where the verb's "met" or "NOT MET"
   comes from.
3. **One rung.** The offer speaks only about `next`. For a `--to` that is not
   `next`, `ladder promote` prints that the offer "says nothing about rung"
   the target (`function offerAboutTarget(offer: PromotionOffer, to: number): string {`).
4. **Every NOT MET clause named.** The question the seat puts to the operator
   names each clause the offer printed NOT MET or unmeasured, by its line.
5. **The readings beside the offer, each with its source and its date, as
   readings and never as conditions this record sets:** ADR 0044 section 1
   item 3 and its readings 2 and 3, each marked there as THE SEAT'S reading,
   **[operator-confirmable]**; the rung-3 research of 2026-10-03 that the
   row's datum of 2026-10-03 names as an input, its list of what the
   operator's word would have to cover put as questions; for the climb to
   rung 3, M0-289's queue state with its date - QUEUED at priority 79 in
   millwright's `node dist/cli.js queue` at 01:40 on 2026-10-05 - carrying
   that row's own footer words, that a seat reads it before it puts rung 3
   to the operator is THE SEAT'S reading, **[operator-confirmable]**; and
   M0-238's overturn question (section 2).
6. **On his word, the one road.** `millwright ladder promote --to <n> --by <who> --reason <text>`,
   run from that repository's checkout - the verb M0-204 landed. Its output
   is printed whole: `was` and `measured_since`, the clause lines and `offer`
   ABOVE the act, then `target`, `rung`, `direction`, `since`, `by`, `reason`, `event`,
   `offered`, `notify`, `notify_detail` and `detail`. Then the journal is
   re-read as a file - the LADDER_RUNG_CHANGED count and the new seq - and
   the report carries both readings with their dates.

What the procedure never contains: an edit of the `soak_rung` row; a flag
that skips the offer - none exists, the verb parses
`  const parsed = parseArgs(argv, new Set(["--to", "--by", "--reason"]));`;
and a lowered `[ladder]` figure in a consumer's `factory/millwright.toml`
to make an offer appear.

## 4. What refuses a promotion

IN CODE - the `ladder` verb exits 78 (`  CONFIG: 78,`,
src/controller/exit-codes.ts) and writes nothing on: a subcommand other
than `promote` and `status`; a positional argument; a missing or empty
`--to`; a `--to` that is not an integer; a missing or empty `--reason`
(`function ladderCommand(resolved: ResolvedConfig, options: CliOptions, argv: readonly string[]): CliResult {`);
and, in the parse that verb shares with the rest of the CLI
(`function parseArgs(`, src/cli.ts), an option given twice, an option with
no value after it, and an unknown option.
`promoteRung` (src/controller/ladder.ts) writes nothing for a number no rung
declares and for a rung outside the definition of done - rung 6 - and the
verb throws each as 78. A failed alert exits 75 with the rung WRITTEN.
`ladder status` refuses `--to`, `--by` and `--reason` by name.

NOT IN CODE - an unmet offer. `promoteRung` records the offer beside the
act and does not gate on it:
` * THE OFFER IS RECORDED BESIDE THE ACT and does not gate it: the payload says`;
the event's `offered` field is false for an act taken on an unmet offer, and
a tick's RUN_FINISHED payload carries
`                promotion_offered: run.ladder.offer.offered,` (src/controller/tick.ts). The verb says
the same of itself: ` * IT MEASURES AND IT DOES NOT GATE, and the two halves of that are one`
(src/cli.ts). Neither verb reads the STOP file: a promotion goes through
under an armed STOP.

THE DESIGN'S SENTENCE - section 18's "promotes only on measured thresholds,
never on "looks fine"" - is what this procedure answers by printing:
the offer whole, every NOT MET clause named in the question, and the
`offered` field read back from the event after the act. This record does
not say that he may promote past an unmet clause, and it does not say that
he may not. `promoteRung`'s comment calls a promotion ahead of its
threshold "a decision an operator is allowed to make", while section 18
says "never on "looks fine""; which of the two governs is a question of
his ratified text, named here and decided nothing about.

HIS WORD - every promotion is taken only by a seat on the operator's word
(the row's outcome); for rung 3, ADR 0044 sections 1 and 2.

## 5. What the next rung changes in a tick

Step 0d of a tick (`    /* -- Step 0d: the soak ladder, beside the breakers --------------- */`,
src/controller/tick.ts) reads the rung and refuses a pass the rung does not
admit, naming one of the six tokens of `export const LADDER_RULES = {`.
The shapes, from `RUNGS`:

- climb to rung 3: `    shape: { merge: true, builders: 2, unattended: false, hours: "day" },` -
  the one token it loosens is `builders_above_rung`, from one builder to two.
- climb to rung 4: `    shape: { merge: true, builders: null, unattended: false, hours: "day" },` -
  null is the configured ceiling, and the rung is still attended.
- climb to rung 5: `    shape: { merge: true, builders: null, unattended: true, hours: "day" },` -
  a cron pass is no longer refused as `cron_below_unattended_rung`, and a cron
  pass outside `[ladder] day_start_hour_utc` to `day_end_hour_utc` (code
  defaults 6 and 18, UTC, half-open) is refused as `night_above_rung`.
  *[CORRECTED 2026-10-05 by carrier #93: the climb to rung 5 is the first
  after which a cron pass is admitted, and `DESIGN.md` section 18 opens with
  the sentence that bears on it, quoted as that file writes it: "The factory
  does not go into cron until its own fault-injection suite is green and the
  soak ladder has been climbed." The procedure did not point at that
  sentence; this bracket points at it as the design's, and decides nothing
  about what it asks of a seat before that climb is put to him - a reading of
  his ratified text, as section 4 leaves its own such question. The bullet is
  kept verbatim as the record of what was written.]*

What a two-builder tick needs beyond the rung is the rung-3 research's
section 2.2, a dated lead and not a condition this record sets.

## 6. Findings against the ladder

Handed up with their files and anchors; none is fixed here, because nothing
under `src/` is this row's.

1. **No fact counts how many builders a pass ran** (medium). `SoakFacts`
   holds tasks, violations, breaches, held refusals, double merges, gate
   refusals, overturns and the false-block rate, and no count of passes or
   builders; so a rung-3 window can offer rung 4 without one two-builder pass
   in it - the rung-3 research's R5, named and not fixed.
2. **`Rung.promotion`'s docstring is false** (low). It says an empty list
   "is true of" `   * exactly one rung: the last one inside the current definition of done has`,
   and rungs 5 AND 6 both carry `    promotion: [],`. The rows that own
   src/controller/ladder.ts by name are its homes.
   *[CORRECTED 2026-10-06 by carrier #95: closed by M5-07's landing
   (8da69af, merged 7cb3e31). The docstring now reads
   "   * from here, which is true of exactly one rung: the sixth, the top of the"
   (src/controller/ladder.ts); rung 6 alone carries `    promotion: [],` -
   `git grep -c -F '    promotion: [],' 5bbff03 -- src/controller/ladder.ts`
   printed 1 on 2026-10-06 - and the item's quoted anchor is gone:
   `git grep -c -F 'exactly one rung: the last one inside the current definition of done has' 5bbff03 -- src`
   printed nothing, rc 1, the same day. The item is kept verbatim as the
   record of what was written.]*
3. **The ladder verbs do not read the STOP file** (low, a fact and not a
   judgement). Whether a promotion under an armed STOP is wanted is nowhere
   stated; this record states the fact and decides nothing.

## 7. What this ADR does NOT decide

- **Any promotion, and its timing.** Each is taken only by a seat on his
  word (the row's outcome); for rung 3, ADR 0044 section 2.
- **The figures** of `[ladder] tasks_per_rung` and
  `[ladder] max_false_block_percent`. His, in a consumer's
  `factory/millwright.toml`.
  *[CORRECTED 2026-10-05 by carrier #93: "His, in a consumer's
  `factory/millwright.toml`." reads two things as settled - that the figures
  are his, and that his road to them is a consumer's TOML. Both are THE
  SEAT'S reading of 2026-10-05, **[operator-confirmable]**; the rung-3
  research's section 7 item 9 stays his and open. The bullet is kept
  verbatim as the record of what was written.]*
- **Whether he may promote past an unmet clause** (section 4).
- **The reading of an overturned refusal.** M0-238's question.
- **The ticks and their form.**
- **Cron and rung 6.** M5-07's.
  *[CORRECTED 2026-10-05 by carrier #93: M5-07's outcome reads "Rung 5,
  unattended cron by day, is M4's DoD; rung 6 is this one, and it is the"
  (factory/tasks/M5-07.yaml): cron by day is rung 5, whose climb sections 1
  to 5 of this record cover, and M5-07's subject is rung 6, cron 24/7, not
  cron as a whole. The bullet is kept verbatim as the record of what was
  written.]*
- **Any row, `DESIGN.md` or any earlier record.** None is edited.
- **That any tick, task, condition, the gate or the ladder passes after any
  row lands.**
