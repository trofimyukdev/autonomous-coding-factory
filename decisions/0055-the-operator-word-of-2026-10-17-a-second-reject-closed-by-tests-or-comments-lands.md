# ADR 0055 - The operator's word of 2026-10-17: a second REJECT that concerns only tests or comments lands at q 2

Date: 2026-10-18. Context: a carrier session (carrier #109, package item
K1), by foreman decision under the standing delegation of 2026-08-25 - not a
block - to give a home to a word the operator typed in the foreman seat's
session on 2026-10-17, and to the messages it answers. Until this record the
word lived in the seat's memory and run journal alone, and no file of the
repository carried it: `grep -ci 'second reject' .claude/commands/block.md docs/decisions/*.md`
printed 0 for every file on 2026-10-18 at 05:3x (the seat's reading, which
this package re-ran before its first edit). `main` and `origin/main` both
stood at `e27d033` when this package began -
`git rev-parse HEAD origin/main | cut -c1-7 | paste -sd' '` printed
`e27d033 e27d033` on 2026-10-18 at 05:44. This package touched nothing under
`src/`, `test/`, `scripts/`, `schemas/`, `.githooks/`, `CLAUDE.md`,
`PRINCIPLES.md`, `DESIGN.md` or the private archive, and nothing under
`docs/decisions/` but this record's own file; its other files are named in
its commit messages.

**This document records an operator word and what it decides. It carries no
mechanism and moves no priority. `.claude/commands/block.md` section 4 points
here and restates none of it (discipline 12).**

## 0. The word, and the messages it answers

Quoted verbatim on ADR 0005's precedent, Russian as typed. One transcript
holds them, the session of the foreman seat then, `<transcript>` below.
His rows were
listed by the seat's read-only lister of the rows whose `origin.kind` is
exactly `human`, at the row's top or inside a `queued_command` attachment
(`<lister>` below, run as
`node <lister> <transcript> 300`); over the transcript
`node <lister> <transcript> 300 | grep -c -E '^HUMAN [0-9a-f-]+ 2026-10-17T1[01]:'`
printed 2 on 2026-10-18 at 05:47 - his rows typed between 13:00 and 14:59
local time on 2026-10-17. The first of them, the row at
2026-10-17T11:53:10.373Z, asks the
seat what is needed from him and what came of the research, and decides
nothing; this record quotes the other. Every row below was printed by its
uuid from the transcript, and every quoted line equals a whole line of the row it is
quoted from, character for character. Line numbers count the row's text
lines from 1, blank lines included. Timestamps are UTC; the times beside
them are those timestamps plus three hours, local time. A quoted
block holds whole lines; what a message says beyond them is not part of this
record.

**WHOSE PROPOSAL IT IS.** Only his row is his. The rule is a proposal of the
stops study of 2026-10-17 (`<control-root>/briefs/research-stops-2026-10-17.md`,
an operator-local file pointed at and not copied: its section 4,
recommendation 1, the paragraph that opens "**Форма.**"), put to him by
the foreman seat in the rows of (a) and (b). Two rows put it: (a) first put the
question, and (b) - the last assistant row carrying text before his word by
timestamp in the transcript - put it again, and his word quotes (b)'s opening line.

### (a) The question first put - 2026-10-17 13:28:36

The seat's row at 2026-10-17T10:28:36.459Z (assistant), the foreman
seat's report of block220's stop. Its lines 7
to 11, whole:

```text
**Вопрос — та самая рекомендация 1 из исследования остановок.** Сегодняшний блок — точный её пример. Предлагаю: если второй отказ проверяющего касается только тестов или комментариев, блок исправляет это в той же попытке и сливает с честным q=2. Если второй отказ по логике кода, остановка остаётся как сейчас.
- **Выигрыш:** примерно половина остановок, около 3–4 часов в неделю. Без курьера и новой попытки.
- **Цена:** иногда в main уйдёт неточность в тексте или тесте, которую поймала бы попытка 2. Код по-прежнему проходит полную проверку.

**Рекомендую — да, начиная с блока M0-146, который я сейчас открываю.** Это решение только твоё: по сути это сверх бюджета попыток, а такие решения кресло само не принимает.
```

"**The question - that very recommendation 1 of the stops study.** Today's
block is its exact example. I propose: if the verifier's second rejection
concerns only tests or comments, the block fixes it within the same attempt
and merges with an honest q=2. If the second rejection is on the code's
logic, the stop stays as it is now.
- **Gain:** about half of the stops, about 3-4 hours a week. No carrier and
  no new attempt.
- **Price:** now and then an inaccuracy in a text or a test that attempt 2
  would have caught will reach main. The code still passes the full
  verification.
**I recommend yes, starting with the block for M0-146 that I am opening
now.** This decision is yours alone: in substance it goes beyond the
attempts budget, and the seat does not take such decisions by itself."

### (b) The question put again - 2026-10-17 14:54:37

The seat's row at 2026-10-17T11:54:37.383Z (assistant), the foreman
seat's answer to his row of 11:53:10 named above, and the last assistant row carrying text before his word. Its lines
1 to 8, whole:

```text
**От тебя сейчас нужно одно решение — по второму отказу проверяющего.**

Если второй отказ касается только тестов или комментариев, блок исправляет их в той же попытке и сливает работу с q=2. Если второй отказ по логике кода, блок останавливается, как сейчас.

- **Плюс:** уходит примерно половина остановок, около 3–4 часов в неделю. Не нужны курьер и вторая попытка.
- **Минус:** изредка в main попадёт неточность в тесте или тексте, которую поймала бы вторая попытка. Код по-прежнему проходит полную проверку.
- **Рекомендую — да.** Если согласен, сразу передам это block221, он сейчас работает.
- **Если нет**, всё остаётся как есть. Блок и так работает по нынешнему правилу, так что ответ не срочный.
```

"**What is needed from you now is one decision - on the verifier's second
rejection.**
If the second rejection concerns only tests or comments, the block fixes
them within the same attempt and merges the work with q=2. If the second
rejection is on the code's logic, the block stops, as now.
- **Plus:** about half of the stops go away, about 3-4 hours a week. No
  carrier and no second attempt are needed.
- **Minus:** now and then an inaccuracy in a test or a text that a second
  attempt would have caught will reach main. The code still passes the
  full verification.
- **I recommend yes.** If you agree, I will pass it to block221 at once; it
  is working now.
- **If not**, everything stays as it is. The block works by the current
  rule anyway, so the answer is not urgent."

Its lines 19 and 20, whole - where the study's recommendations stand:

```text
Исследование остановок дало три рекомендации, вот где каждая:
1. **Второй отказ только по тестам или комментариям** — это твоё решение, о котором выше.
```

"The stops study gave three recommendations; here is where each stands:
1. **A second rejection on tests or comments only** - this is your decision,
   the one above."

Its lines 21 to 26 place the study's recommendations 2 and 3 elsewhere and
ask nothing of him.

### (c) His word - 2026-10-17 14:58:22

His user row at 2026-10-17T11:58:22.186Z, `origin` kind `human`, typed
in the foreman seat's session:

```text
По поводу «по второму отказу проверяющего.»-да,  по твоим рекомендациям
```

"About 'on the verifier's second rejection.' - yes, by your
recommendations"

## 1. The evidence

**WHY IT WAS HIS.** Row (a) line 11 says it: a landing past a second REJECT
goes beyond the attempts budget, and the seat takes no such decision by
itself; the study's recommendation 1 names the choice the operator's (its
section 4: it is his metric and his standing ban on an over-budget sanction
from the seat). Before his word a hand-run block stopped on its second
REJECT (row (b) line 3: "as now").

**ITS FIRST LANDING.** block221, M0-146 attempt 2, merged as `e27d033`:
`node dist/cli.js queue | grep -E ' M0-146@cd563882b437 '` printed the row
`DONE` with `q2/i0` on 2026-10-18 at 05:4x, and the journal's event of seq
4989 (`grep '"seq":4989,' factory/state/events.jsonl`) is its
`BLOCK_RECORDED` with `"quality_attempts":2` and the basis
`verifier-rejections`. The seat's archive entry that opens "- BLOCK221'S
SECOND REJECT" (the seat's run journal, operator-local) holds how that REJECT's one finding was closed and
classed, and the entry that opens "- HIS WORD ON THE STOP STUDY'S
RECOMMENDATION 1" holds the rule as the seat relayed it to block221; both
are pointed at and not copied.

## 2. The decision

His word of (c), to the question of (b), in the words of (b)'s line 3: **if
the verifier's second rejection concerns only tests or comments, the block
fixes them within the same attempt and merges the work with q=2; if the
second rejection is on the code's logic, the block stops, as now.** Which
blocks that covers, and what "concerns only tests or comments" admits, are
readings 5 and 2.

Six readings follow. Each is **THE SEAT'S**, and each is
**[operator-confirmable]** - it stands unless the operator names another.

1. **"By your recommendations" is recommendation 1 of the stops study in
   its main form.** His word quotes a fragment of (b)'s line 1, and both rows (a)
   and (b) recommended yes to the form the study's section 4 gives
   recommendation 1. The study names an alternative - `quality_attempts: 3`
   in hand-run specs - which neither row put to him; the seat reads his word
   as the main form and not that alternative. The plural "recommendations"
   is read as the seat's two recommendations of yes, not as a word on the
   study's recommendations 2 and 3, which row (b) lines 21 to 26 placed
   elsewhere.
2. **"Only tests or comments" is the two lanes block.md section 4 accepts
   without a second pass.** A finding counts as one that concerns only tests
   or comments when it is closed by block.md section 4's test-only fix (ADR
   0002) - changes confined to `test/**` that strengthen what is asserted,
   with ADR 0002's evidence per killed mutant in the commit message - or by
   its own-diff comment fix (ADR 0004 section 3), text this block's diff
   introduced. A finding that neither lane can close counts as a logic
   finding and stops the block, and a mixed fix is a logic fix by ADR 0002's
   "Mixed fix - logic class". So a fix to a comment or a doc OUTSIDE the
   block's own diff is a stop under this reading, although ADR 0002 gives
   doc and comment changes no gate of their own and his word says
   "comments" with no such limit: the narrowing is the seat's.
3. **The landing road.** Each fix is its own commit on the block branch
   after the verdict, never an amend; the commits that close a second REJECT
   get no further verifier pass, which is what ADR 0002's two lanes already
   allow; then section 5's gate, the merge, and `millwright record-landed`
   with a count of 2 and the basis `verifier-rejections`, in the flags
   block.md section 6 and the verb's usage text name. How the
   count is taken is not changed: its one home is the section that opens
   "THE RULE, DECIDED 2026-09-07" in `factory/tasks/M0-134.yaml`.
4. **A doubt is a stop.** Where the block's class of a finding and its
   verifier's closing class differ, the stricter one decides; a finding
   whose class is in doubt stops the block. The block's report names the
   road it took, finding by finding.
5. **Hand-run blocks only, from block221 on.** Rows (a) and (b) spoke of the
   block ritual - (a) from the block for M0-146, (b) by passing the word to
   block221 - and the seat relayed it to block221 on 2026-10-17 at 15:00.
   The factory's controller keeps its own edge: `DESIGN.md` section 6's
   bullet that opens "`BUILDING|VERIFYING -> BLOCKED`" (quality attempts
   exhausted), which the study itself left standing until the operator
   decides otherwise.
6. **It is a rule about the second REJECT of a row whose ceiling is 2.**
   Both rows spoke of the second REJECT and of q=2; the seat reads the word
   as covering a hand-run row whose `quality_attempts` is 2 - most rows, not
   all: `grep -h -E '^\s*quality_attempts:' factory/tasks/*.yaml | sort | uniq -c`
   printed 1 row at 1, 359 at 2 and 13 at 3 on 2026-10-18 at 06:14, this
   package's new M0-308 among the 359 - and as
   leaving the first REJECT's road where block.md section 4 puts it.

## 3. What this ADR does NOT decide

- **The controller.** `DESIGN.md` section 6 and the gate refusal's charge of
  ADR 0028 are untouched; a factory pass that spends its quality ceiling
  still lands `BLOCKED`.
- **The study's alternative**, `quality_attempts: 3` in hand-run specs, nor
  the `quality_attempts` value of any spec.
- **How the attempts are counted** - its home is M0-134's section named in
  reading 3.
- **What a REJECT does in a row whose ceiling is not 2**, and anything about
  a third REJECT.
- **The study's recommendations 2 and 3.** Row (b) lines 21 to 26 place
  them: a row of carrier #108's, and the block's own rules.
- **Any priority or row**, and that any block lands after this record.

## 4. Where it is pointed at

`.claude/commands/block.md` section 4 (the section whose heading opens
"## 4. Fix cycle") carries one line that points at this record and restates
none of it.
