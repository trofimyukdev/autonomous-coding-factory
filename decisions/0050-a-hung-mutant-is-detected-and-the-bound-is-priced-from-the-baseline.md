# ADR 0050 - The operator's word of 2026-10-10 21:07:07: a mutant run past its bound is a detected mutant and the bound is priced from the file's baseline, with the seat's binding of a stage-5 pass that leans on it to the holdout

Date: 2026-10-10. Context: a carrier session (carrier #97, package item K1)
by foreman decision under the standing delegation of 2026-08-25, opened off
cadence by exception - not a block - to carry into its record the operator's
word on the mutation probe's bound per mutant and on how a mutant run past
that bound counts, the wall RT-21 met on 2026-10-10. Merge blocks since
carrier #96's last commit:
`git log --oneline --first-parent 6a0591c..origin/main | grep -c ' merge: '`
printed 0 on 2026-10-10. `main` stood at `6a0591c 6a0591c` when this record was
committed - `git rev-parse HEAD origin/main | cut -c1-7 | paste -sd' '`
printed `6a0591c 6a0591c` on 2026-10-10 at 22:06.
Nothing under `src/`, `test/`, `scripts/`, `.githooks/`, `.claude/`,
`factory/policy/`, `factory/checks.yaml`, `factory/millwright.toml`,
`CLAUDE.md`, `PRINCIPLES.md`, `DESIGN.md` or the private archive was touched by
this package, nothing under `docs/decisions/` but this record's own file and
the end of ADR 0049, and nothing was written in `repo-truth`; the package's
other files are named in its commit messages.

This is a new record and not an amendment. ADR 0039's reading 3 judges every
way the probe can fail to finish but its time ceiling "as today"; M3-12's
acceptance and M0-276's `not_done_if` pin a mutant run past its bound as a
gap that is never a kill, and M0-278's `not_done_if` pins it as neither
killed nor survived. Section 1's reading 4 names the sentence of each that
the word recorded here changes, for two kinds of run past its bound only;
that it changes them is THE SEAT'S reading, **[operator-confirmable]**, and
ADR 0039's reading 3 is itself the seat's reading of an earlier word. None
of ADR 0039, M3-12, M0-276 or M0-278 is edited.

**This document records an operator word and what it decides. It carries no
mechanism and moves no priority: the row that carries the decision out is the
home of its own content and is named in the commit message.**

## 0. The words, and the messages they answer

Quoted verbatim on ADR 0005's precedent, Russian as typed. One transcript
holds them, the session of the foreman seat that heard them (its live
session then): `<transcript>`.
His rows were listed by the read-only lister of the user rows whose
`origin.kind` is exactly `human`, at the row's top or inside a
`queued_command` attachment (the filter ADR 0043 section 0 (c) quotes whole
reads the same field), and every row below - his and the seat's - was
printed by its uuid with `jq` over the transcript on 2026-10-10. Every quoted line
below was found in the transcript by `grep -c -F -e '<the line>' <transcript>`, which
printed at least 1 for each on 2026-10-10. Timestamps are UTC; the times
below are those timestamps plus three hours, local time. A quoted
block holds whole lines; what a message says beyond them is not part of this
record.

**WHOSE PROPOSAL IT IS.** The proposal this record decides on - a bound per
mutant run priced from the file's ordinary test run, and a hang counted as a
caught defect - is THE SEAT'S. It is first put in the seat's question row of
(a), and no row of his names a bound, a hang or the probe on 2026-10-09 or
2026-10-10 in the transcripts of the two foreman seats of those days, the
session that ran the ticks or carrier #96: over each, the lister's output
filtered to his rows of those two days and then by a case-insensitive count
of five Russian stems - hang, second, mutation, probe, timeout - printed 0,
over 7, 4, 2 and 0 such rows, re-run by this carrier on 2026-10-10 at
21:23. The command is quoted whole in the seat's run
journal, in its archive entry that opens "- CARRIER #97 OPENED ON HIS"; it is
not quoted here, because this record carries non-ASCII text in its
quotations only. The seat's reply of
(e) and its run journal's entry that opens "- THE PROBE RESEARCH RETURNED"
called the proposal his, and so does the research report's own opening,
its line that reads "Take both parts of the operator's idea, in one row,
with five changes:"; this record corrects all three. The five
changes to the proposal are the research's (d). His words on the subject are
two, each a one-word yes: the first commissioned the research (c), the
second decided (f).

### (a) The first question - 12:38:55

The seat's row at 09:38:55.285Z (assistant). Its question line, whole:

```text
**Вопрос: поручаю проверяющему разобрать, как починить мутационную проверку — ждать зависшую ошибку по времени обычного прогона тестов, а не 60 секунд, и засчитывать зависание как пойманную ошибку, — и принести рекомендацию?** Рекомендую: да.
```

"Question: do I commission the verifier to work out how to repair the
mutation check - to wait for a hung defect by the time of the ordinary test
run and not 60 seconds, and to count a hang as a caught defect - and to bring
a recommendation? I recommend: yes."

### (b) The question put again - 13:26:52

The seat's row at 10:26:52.364Z (assistant), a
report on carrier #96's landing that closes on the same question. Its last
line, whole:

```text
Открытым остаётся прежний вопрос: **поручаю проверяющему разобрать починку мутационной проверки (стена RT-21) и принести рекомендацию?** Рекомендую: да.
```

"The earlier question stays open: do I commission the verifier to work out
the repair of the mutation check (RT-21's wall) and to bring a
recommendation? I recommend: yes." It is the last seat row carrying text
before his word of (c): the seat rows with text between 10:20:00Z and his
word are two earlier ones and this one.

### (c) His first word - 13:49:01

His user row at 10:49:01.461Z, `origin` kind `human`:

```text
Да
```

"Yes." It commissioned the research of (d) - a spend, done - and decided
nothing about the probe, as ADR 0043 section 0 leaves out the word that
sanctioned the research its recommendation rests on.

### (d) The research

The seat's research, a fresh-context subagent's report, saved verbatim at
`<control-root>/briefs/research-probe-2026-10-10-report.md`:
`wc -l -c` printed 225 lines and 20525 bytes, and `sha256sum | cut -c1-16`
printed 1e28609ed0c20efa, on 2026-10-10. Its verdict line reads
"## (1) RECOMMENDATION: RIGHT WITH CHANGES", and its changes are five: the
shorter bound and the count of a hang shipped together, because the bound
alone turns slow kills into gaps and the count alone moves no throughput; a
floor of about 15 s in place of 60 s, its exact value argued by the row from
a measurement; two guards against a false kill, the run's own JSON report
and a control run of the unmutated file; timed-out mutants counted apart
from kills, a baseline timeout kept "could not measure", the probe's
version moved to 2 and each file's baseline time and bound carried in the
record; and his word recorded in a new ADR with no `DESIGN.md` amendment.
Its section "### Q4" names what his word must cover. The report is pointed
at, not copied.

The seat re-ran its top findings; the run journal's archive entry that opens
"- THE PROBE RESEARCH RETURNED" lists what survived and what it did not
re-run (the report's projections for RT-21 and RT-19, and its inference of
slow kills, which the report itself gives medium confidence). The tally this
carrier re-ran from `repo-truth`'s working directory,
`jq -r 'select(tostring | contains("\"kind\":\"timeout\"")) | .payload as $p | $p.measurement.record.incomplete[]? | select(.kind=="timeout") | [($p.candidate_sha[0:8]), .detail] | @tsv' factory/state/events.jsonl | sort -u | wc -l`,
printed 69 distinct timed-out mutants on 2026-10-10, and
`grep -F '"task_id":"RT-21@79981b993d4e"' factory/state/events.jsonl | grep -c '"type":"MEASUREMENT_CARRY_ENDED"'`
printed 1: RT-21's measurement ended at journal seq 4427 with 134 mutants
left.

### (e) The question - 14:13:27

The seat's row at 11:13:27.235Z (assistant), the seat's report of the
research. Its first line names the report's file.
Which of its lines the question calls "described above" is THE SEAT'S
reading 1 and 2 below: the seat reads them as its proposal block and, one
paragraph further down, the seat's addition, each quoted whole here. Its
other lines above the question - the paragraph that says both parts are
needed together, and the block on price and consequences, which says among
other things that one task and a decision record are needed and that DESIGN
does not change -
are pointed at and not quoted. An earlier seat row with text, at
11:12:32.048Z, had already shown him
the research's summary: the bound as the research's formula
`max(15 s, 5 x baseline)` in its own notation, the hang counted as detected
apart from kills, the two guards, the probe's version 2 with a new ADR, and
that DESIGN does not change. It is pointed at and not quoted; readings 2
and 5 rest on it as well. The lines of (e) the question calls "described
above", as the seat reads them:

```text
**Что предлагается — одной задачей:**
- ждать зависание около 15 секунд вместо 60, считая от времени обычного прогона тестов;
- считать зависание пойманной ошибкой, отдельно от обычных пойманных;
- две защиты от ложной поимки. Если тесты успели оставить отчёт, судить по нему. После каждого зависания делать контрольный прогон без подложенной ошибки: если и он не успел, значит, тормозит машина, и зависание не засчитывается.
```

"What is proposed - as one task: wait for a hang about 15 seconds instead of
60, counted from the time of the ordinary test run; count a hang as a caught
defect, apart from the ordinary caught ones; two guards against a false
catch. If the tests managed to leave a report, judge by it. After each hang
make a control run without the planted defect: if it did not make it either,
the machine is slow, and the hang is not counted."

```text
**Одно добавлю от себя.** Если «тесты сильные» держится на зависаниях, засчитывать это только при пройденной скрытой пробе. Так устроены и ваши прошлые решения, от 01.10 и сегодняшнее.
```

"I will add one thing of my own. If 'the tests are strong' rests on hangs,
count it only when the hidden probe passed. Your earlier decisions, of 01.10
and today's, are built the same way."

Its question line, whole:

```text
**Вопрос: чиним проверку одной задачей так, как описано выше, и записываем это решением (ADR)?** Рекомендую: да.
```

"Question: do we repair the check as one task, as described above, and
record it as a decision (ADR)? I recommend: yes." The session was
compacted while idle at 12:08:28Z, between this row and his word, and no
seat or human row carrying text came between them. It is the last seat row
carrying text before his word of (f): the window from 11:10:00Z to his word
holds one other seat row with text, the one at 11:12:32.048Z, which is
earlier.

### (f) His word - 21:07:07

His user row at 18:07:07.176Z, `origin` kind `human`, typed in the seat's
own session:

```text
Да
```

"Yes." It is the word recorded here.

## 1. The decision

The word of (f), to the question of (e), on the research of (d):

1. **A MUTANT RUN PAST ITS BOUND IS A DETECTED MUTANT**, counted apart from
   the mutants its tests killed. A baseline run past its bound stays what it
   is today: the file could not be measured.
2. **THE BOUND PER MUTANT RUN IS PRICED FROM THE FILE'S BASELINE RUN** in
   `perRunBound`'s form - the baseline's duration times the factor, raised
   to a floor and capped at `perRunTimeoutMs` as today - with a floor of
   about 15 seconds in place of 60. The floor's exact value is the row's to
   argue from a measurement.
3. **TWO GUARDS AGAINST A FALSE CATCH.** A run past its bound that left its
   JSON report is scored from that report. After each run past its bound,
   one control run of the unmutated file under the same bound: a control
   past the bound leaves that mutant's timeout a gap, as today.
4. **THE RECORD** names the count of mutants detected past their bound apart
   from the kills, carries each file's baseline time and the bound it was
   given, and the probe's version moves to 2.
5. **THE GATE.** A stage-5 pass that leans on timeouts retires the
   reviewer's pointer at stage 5 only when `holdoutShortfall`
   (src/verify/gate.ts) answers null - ADR 0043's binding.

Items 1 to 3 are the bullets of (e) as he was asked them. What items 1 to 4
add to those bullets - the baseline timeout kept a gap, "about 15 seconds"
read as a floor under the factor's product, the cap kept, the control run
under the same bound and a gap as today when it too runs out, the record's
fields and the version - is the research's form of the same change, and
that it rides his word is reading 2. Item 5 is the seat's own
addition, put to him above the question of (e), and that his word covers it
is reading 1.

Five readings follow. Each is **THE SEAT'S**, and each is
**[operator-confirmable]**:

1. **His word covers item 5.** The second quoted line of (e), which opens
   "I will add one thing of my own", stood above the question, framed as the
   seat's own addition,
   and the question asks about the repair "as described above"; the seat
   reads the line as inside that phrase. It binds this one retirement as
   ADR 0043 bound ADR 0035's and ADR 0038's and as ADR 0049 bound the
   tests-only mark, which the line itself names. That the evidence names
   this retirement apart from the others is the form ADR 0049's reading 3
   gave the tests-only mark, carried here as the seat's form and not as a
   word of his or a line he was asked.
2. **"As described above" carries the research's form of the bullets.** The
   question's row opens by naming the report of (d), and the bullets
   summarise its changes; so the parts of items 1 to 4 the bullets do not
   say - a baseline run past its bound kept "could not measure", the
   fifteen seconds read as a floor under the baseline times the factor
   (`max(15 s, 5 x baseline)` in the research's words, so a slow file's
   bound stays above fifteen seconds), the cap at `perRunTimeoutMs` kept, the
   control run under the mutant's own bound with a gap as today when it too
   runs out, each file's baseline time and bound in the record, version 2 -
   are read as part of the repair he took. Nothing else
   of the report is: its later options stay its reading (section 2).
3. **"Leans on timeouts" is a stage-5 pass whose record counts at least one
   mutant detected past its bound.** Every such pass is one today's rule
   could not give: today any run past its bound leaves a `timeout` gap, and
   `probeStatus` (src/verify/mutation.ts) answers `error` for a record with
   a gap and no survivor, and `fail` when a mutant survived - never `pass`
   while a gap is left. The score-based form - a pass the kills alone would not reach -
   is named and not taken: under today's `probeStatus` the two forms select
   the same passes, and the count form reads a field the record carries by
   item 4 rather than a rule that may change.
4. **The word amends four sentences for two kinds of run past its bound,
   and their text stays as written.** The two kinds: a mutant run past its
   bound whose control run finished inside it, counted detected (item 1);
   and a run past its bound that left its JSON report, scored from that
   report as killed or survived (item 3's first guard, the third bullet of
   (e)). ADR 0039's reading 3, "Every other way the probe can fail to
   finish is judged as today.", no longer covers either: each is an
   answer, not a way the probe failed to finish. M3-12's acceptance
   sentence that opens "A tool failure, a timeout and a per-file ceiling
   each produce a record that", M0-276's `not_done_if` line that opens "a
   timed-out mutant is scored as killed or as survived, or `probeStatus`
   answers otherwise than it does today" and M0-278's `not_done_if` line "a
   timed-out mutant is scored as killed or as survived, or is run again by a
   carry" are each read as amended for those two kinds and stand as written
   for every other run past its bound; no carry runs a mutant again under
   either kind. M3-12, M0-276 and M0-278 are DONE.
5. **No `DESIGN.md` amendment.** Section 8's table gives stage 5 its content
   "only by trigger" and sets no bound per run and no score, and stage 5's
   checks are advisory, so no required check changes. Section 9's second
   sentence, quoted in ADR 0049's reading 5, governs `every_item_verified`,
   the check item 5 touches, and stands by ADR 0049's argument: what
   condition 2 counts as an item lives in the gate's docstring "WHAT
   CONDITION 2 COUNTS", where ADR 0035, ADR 0038 and ADR 0043 each changed
   it and ADR 0049's row is to change it, and item 5 changes it there the
   same way. The seat row of 11:12:32.048Z in section 0 (e) had told him
   that DESIGN does not change.

## 2. What this ADR does NOT decide

- **Any priority or row.** Those are the rows' footers, each
  **[operator-confirmable]**.
- **The mechanism**: the floor's exact value, the field that carries the
  count, the home of the "leans on timeouts" predicate and the evidence
  clause's words. The row that carries the decision is their home.
- **The research's later options**, which are ITS reading and not his
  decision, **[operator-confirmable]**: its option (v-d), a projection of a
  carried measurement on its cumulative rate, and its option (v-e), judging
  an ended measurement on its measured part when that part already holds
  survivors, which its own text says contradicts ADR 0039's reading 4. Its
  option (iv), a long-bound confirmation of each timeout, it rejected. This
  package files no row for any of them.
- **Files the size of RT-19's**, which the research leaves at seven or eight
  of the eight carries - a later question.
- **`maxTotalMs` and `perRunTimeoutMs`**, unchanged; M0-240's and M0-283's
  `not_done_if` lines refuse a raise of either.
- **RT-21's candidate `ec3d58b`.** It is not rescued: its next pass builds
  afresh, because `owedSeat` (src/controller/deferred-seat.ts) reads only
  SEAT_DEFERRED and SEAT_RESUMED and nothing is owed - the research's Q5, a
  fact of the code and not a decision. When the tick series runs again is
  the seat's control.
- **`DESIGN.md`**, untouched (reading 5).
- **That any tick, task, condition or the gate passes after any row lands.**

## 3. What is filed elsewhere

The row this package minted is named in its commit messages and is not
listed here, for ADR 0020 section 3's reason: a decision document that
carries a backlog acquires two homes for every row in it.
