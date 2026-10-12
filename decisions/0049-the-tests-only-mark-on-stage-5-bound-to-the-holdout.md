# ADR 0049 - The operator's word of 2026-10-10 12:30:45: a stage-5 pointer on a tests-only candidate leaves condition 2's count on a positive mark and a passed holdout, and (a) set aside

Date: 2026-10-10. Context: a carrier session (carrier #96, package item K1)
by foreman decision under the standing delegation of 2026-08-25, opened off
cadence by exception - not a block - to carry into its record the operator's
word on condition 2 for a candidate that changes only tests. Merge blocks
since carrier #95's last commit:
`git log --oneline --first-parent b2019e1..origin/main | grep -c ' merge: '`
printed 2 on 2026-10-10. `main` stood at `886b98d 886b98d` when this record was
committed - `git rev-parse HEAD origin/main | cut -c1-7 | paste -sd' '`
printed `886b98d 886b98d` on 2026-10-10 at 13:08.
Nothing under `src/`, `test/`, `scripts/`, `.githooks/`, `factory/policy/`,
`factory/checks.yaml`, `factory/millwright.toml`, `CLAUDE.md`,
`PRINCIPLES.md`, `DESIGN.md` or the private archive was touched by this
package, nothing under `docs/decisions/` but this record's own file, and
nothing was written in `repo-truth`; the package writes this record, two
files under `factory/tasks/`, and two files under `.claude/` committed as
they stood on the operator's earlier word of 2026-10-07, which is not this
record's.

This is a new record and not an amendment. ADR 0038 section 1's reading 3
says a pointer at stage 5 recorded `unrun` with `NO_PROBE_TRIGGER` still
counts, and ADR 0043 made ADR 0038's retirement permanent and bound to the
holdout; the word recorded here changes that reading for one record, and
section 1 below names the sentence it changes. None of ADR 0035, ADR 0036,
ADR 0038 or ADR 0043 is edited.

**This document records an operator word and what it decides. It carries no
mechanism and moves no priority: the row that carries the decision out is the
home of its own content and is named in the commit message.**

## 0. The words, and the messages they answer

Quoted verbatim on ADR 0005's precedent, Russian as typed and with the typing
kept as it is. Two transcripts hold them, the sessions of the two foreman
seats that heard them: the earlier seat's (closed), called the first
transcript below, and its successor's, called the second transcript;
`<transcript>` stands for either. His rows were listed by a read-only lister of the user rows
whose `origin.kind` is exactly `human`, at the row's top or inside a
`queued_command` attachment (the filter ADR 0043 section 0 (c) quotes whole
reads the same field), and every row below - his and the seats' - was
printed by its uuid with `jq` over its transcript on 2026-10-10. Every
quoted line below was found in its transcript by
`grep -c -F -e '<the line>' <transcript>`, which printed at least 1 for each
on 2026-10-10. Timestamps are UTC; the times below are those timestamps
plus three hours, local time. A quoted block holds whole lines;
what a message says beyond them is not part of this record.

### (a) The question - the first transcript, 11:30:07 and 11:34:53

The seat's row at 08:30:07.710Z (assistant) in the first transcript put
the question; it is the row's last line, whole:

```text
**Вопрос: готовим решение по условию 2 — вариант O3 и правило ADR 0038 для пустого stage 5 у задач без `src/**`?** Рекомендую: да. Это самый большой рычаг к финишу.
```

"Question: do we prepare a decision on condition 2 - option O3 and ADR
0038's rule for an empty stage 5 on tasks without `src/**`? I recommend:
yes. It is the largest lever toward the finish." O3 is the option ADR 0043
section 1 item 5 did not take.

His row at 08:34:33.235Z asked the seat to bring him up to date in plain
words, and the seat's row at 08:34:53.607Z (assistant) answered with a
numbered list. Its first item, whole:

```text
1. **Сейчас.** Разрешить починить проверку, чтобы она не браковала хороший код из-за пометок «не проверял» и не валила задачи, где меняются только тесты. Это вернёт и выпавшую из очереди RT-17. Рекомендую: да.
```

"1. Now. Allow the check to be fixed, so that it does not reject good code
over 'did not check' notes and does not fail tasks in which only tests
change. This also brings back RT-17, which dropped out of the queue. I
recommend: yes."

The last seat text before his answer below is a third row, at
08:40:45.054Z, the seat's handover note, whose third bullet points back at
the same item:

```text
- **Ваш открытый вопрос остаётся тем же: пункт 1, починка проверки, рекомендация «да».** Можно ответить уже новому форману. Если ответите здесь, он увидит ответ в моём транскрипте до того, как закроет сессию.
```

"Your open question stays the same: item 1, the repair of the check,
recommendation yes. You can already answer the new foreman. If you answer
here, he will see the answer in my transcript before he closes the session."

### (b) His first answer - the first transcript, 11:41:53

His user row in the first transcript at 08:41:53.680Z, `origin` kind
`human`. As typed, two lines:

```text
1. По большому счету да, ну как-то это странно, как можно понять что это хороший код если он ещё не проверен ?
И если тесты поменялись, то по сути поменялось и покрытие участка который был покрыт ними? Просто кажется это расхождение с методикой проверки тому подобное, разве нет? Разве хороший код не должен получать подтверждение что он хороший? Даже тесты как раз не делают то что ты сейчас будешь отменить? Объясни если я чего-то не понимаю
```

"1. By and large yes, but it is somehow strange: how can one tell this is
good code if it has not been checked yet? And if the tests changed, then in
effect the coverage of the part they covered changed too? It just seems a
departure from the method of checking and the like, doesn't it? Shouldn't
good code get a confirmation that it is good? Don't the tests do exactly what
you are now going to cancel? Explain if I am missing something." The seat
reads it as a yes with doubts and a request that decides nothing on its own,
**[operator-confirmable]**.

### (c) The refined question - the first transcript, 11:43:43

The seat's row at 08:43:43.793Z (assistant) in the first transcript, the
seat's answer to (b): an explanation the record points at and does not
quote, then the refined question. Its question block, whole:

```text
**Вопрос: готовим решение в таком виде?**
- (а) Пометка «не проверил» блокирует, только если она про требование задачи. Остальные такие пометки записываются кандидатами в будущие задачи.
- (б) Пустая мутационная проверка у задачи только из тестов не считается провалом, если скрытая проверка с подложенными ошибками прошла.
```

"Question: do we prepare the decision in this form? - (a) A 'did not check'
note blocks only if it is about a requirement of the task. The other such
notes are recorded as candidates for future tasks. - (b) An empty mutation
check on a task made only of tests does not count as a failure, if the
hidden check with planted defects passed."

The seat's run journal renders this question in other words - its archive
entry that opens "- HIS ANSWER TO QUESTION (1)" - and the row decides: the
words above are the row's.

### (d) His second answer - the first transcript, 11:47:20

His user row in the first transcript at 08:47:20.709Z, `origin` kind
`human`, the next row of his after (c):

```text
Да, но убедись ещё раз, что архитектурно это правильное решение.
```

"Yes, but make sure once more that architecturally this is the right
decision." The seat reads it as a conditional yes, **[operator-confirmable]**:
nothing was filed until the verification of section 0 (e) returned and was
reported to him.

### (e) The verification

The seat's architectural verification, a fresh-context subagent's report,
saved verbatim at
`<control-root>/briefs/arch-cond2-2026-10-10-report.md`:
`wc -l -c` printed 277 lines and 28841 bytes, and `sha256sum | cut -c1-16`
printed 7c636734f7e011e9, on 2026-10-10. Its verdict line reads
"## (1) VERDICT: RIGHT WITH CHANGES": (b) right and to be taken now, on a
new POSITIVE mark stage 5 writes, never on today's `NO_PROBE_TRIGGER`
record, which a diff touching only a README or a configuration file earns as
well; (a) not right today, because the controller cannot decide whether a
free-text entry is about a stated requirement, and the retiring fact would
be the reviewer's own label. Its table under "### Q8" lists the rows. The
report is pointed at, not copied.

The seat re-ran its top findings; the run journal's archive entry that opens
"- THE ARCHITECTURAL VERIFICATION OF QUESTION (1) RETURNED" is where what
survived is listed, and what it did not re-run: seq 940's defect (the
report's own medium confidence) and the report's line citations into the
ADRs. The tally this carrier re-ran from `repo-truth`'s working directory,
`grep '"type":"GATE_FAILED"' factory/state/events.jsonl | jq -c 'select(.ts|startswith("2026-10-07")) | {seq, task: .task_id, notpass: [.payload.conditions[] | select(.status!="pass") | "\(.number):\(.status)"]}'`,
printed seven rows on 2026-10-10, each with condition 2 at `error` and no
other condition below `pass`: seq 3352 (RT-14), 3630 (RT-16), 3728, 3854,
3946 and 4043 (RT-17), and 3997 (RT-18).

### (f) The question and the word - the second transcript, 12:15:37 and 12:30:45

The seat's row at 09:15:37.199Z (assistant) in the second transcript
reported the verification to him in plain words and asked. Its question
line, whole:

```text
**Вопрос: берём (б) в уточнённом виде — машинная отметка «изменены только тесты» плюс условие «скрытая проба прошла» — а (а) откладываем?** Рекомендую: да.
```

"Question: do we take (b) in the refined form - a machine mark 'only tests
changed' plus the condition 'the hidden probe passed' - and set (a) aside?
I recommend: yes."

The last seat text before his word is a later row, at 09:22:34.277Z, a
report on the tick series that ends by putting the same question again. Its last line, whole:

```text
**Открыт прежний вопрос: берём (б) в уточнённом виде — машинная отметка «изменены только тесты» плюс условие «скрытая проба прошла» — а (а) откладываем?** Рекомендую: да.
```

"The earlier question is open: ..." and the same words. Between that row
and his word no other seat row carries text.

His user row in the second transcript at 09:30:45.686Z, `origin` kind
`human`, typed in the seat's own session:

```text
Да
```

"Yes." It is the word recorded here.

## 1. The decision

The word of (f), to the question of (f), on the conditional yes of (d) and
the verification of (e):

1. **(b) IS TAKEN IN ITS REFINED FORM.** A candidate's stage-5 record that
   carries a machine mark "only tests changed" no longer makes a pointer at
   it count in condition 2, on the condition that the hidden probe - the
   candidate's holdout - passed.
2. **(a) IS SET ASIDE.**

For the one record it names, the word changes ADR 0038 section 1's reading
3, the sentence that opens "The word is read for stage 3 alone." A pointer
at a stage-5 record that carries the mark leaves the count under the
binding of item 1; a pointer at any other stage-5 record recorded `unrun`
still counts, as that reading says.

Eight readings follow. Each is **THE SEAT'S**, and each is
**[operator-confirmable]**:

1. **"A machine mark 'only tests changed'" is a positive mark on stage 5's
   own record.** Stage 5 writes it on the record it writes when the probe has
   nothing to mutate, and only when the candidate's list of changed paths
   is not empty and every path on it, deleted paths included, is a test path
   by `isTestPath` (src/verify/stage1.ts), which is the one home of what a
   test path is; the record carries a detail sentence of its own, and no
   other record carries the mark. The verification's row 1 is the source of
   this form. The mark is positive because the record `NO_PROBE_TRIGGER`
   names is earned by every diff that changes nothing the probe can mutate:
   the gate's own fixture `probeUntriggered` in test/unit/gate.test.ts builds
   that record from a diff that changes only README.md. `NO_PROBE_TRIGGER`
   stays as it is, and a pointer at a record carrying it and no mark still
   counts.
2. **"The hidden probe passed" is ADR 0043's binding, unchanged.** The mark
   retires a pointer only when `holdoutShortfall` (src/verify/gate.ts)
   answers null, which is ADR 0043's readings 1 and 2 as they stand: every
   declared holdout item ran and passed, read from the declared items and
   their answers and never from condition 1's status. A spec that declares
   no holdout item retires nothing under this rule.
3. **The evidence names this retirement apart** from the three rules that
   retire entries today, both where it retires and where the holdout keeps
   the entry counted, as ADR 0035's and ADR 0038's are named apart, so what
   it retired can be read back from a consumer's journal on its own.
4. **ADR 0038's mark `unconfigured` stays the stage-3 mark.** The new mark is
   stage 5's, and a stage-5 record carrying `unconfigured` still retires
   nothing. ADR 0035, ADR 0036 and ADR 0043 are otherwise unchanged, and so
   is ADR 0038 for every record but this one.
5. **No `DESIGN.md` amendment.** Section 8's table gives stage 5 its content
   "only by trigger", and stage 5's checks are advisory, so an untriggered
   stage 5 holds no required check that could not be run; what condition 2
   counts as an item lives in the gate's docstring "WHAT CONDITION 2 COUNTS",
   where ADR 0035, ADR 0038 and ADR 0043 each changed it. Section 9's two
   sentences stand: "All seven are required, and a required check that
   cannot be run is an infrastructure or gate failure - never a pass." and
   "The verdict is schema-valid, `overall == pass`, every item verified."
6. **THE AUTHORING RULE.** For a candidate that changes only tests, the
   holdout is the only evidence that the new tests are strong, and the gate
   cannot see what a holdout does: a holdout result is a command, a status
   and its evidence. So a spec for a tests-only task carries a holdout that
   plants defects into the built program and demands that the new tests turn
   red on them, with a negative control and a guard against a vacuous run -
   the form the held-out check of `repo-truth`'s RT-17, kept outside that
   repository, already has. It is a rule for the seat's
   drafters and not a gate check, on the precedent of ADR 0041's reading 3;
   the verification's row 4 is its source.
7. **"Set aside" (item 2) holds until M0-234's typed entries land.** The
   question line says only that (a) is set aside; the message it closes
   names M0-234 as when (a) can come back, and the seat reads the word
   inside that message. The conditions the verification gives for a later
   revisit are ITS reading and not his decision: its row 6 - after M0-234's
   typed entries, a requirement pointer, entries that point at no stage
   only, an entry labelled out of scope leaving only when `holdoutShortfall`
   answers null and named apart, the old string form still counted - and its
   needs: his word, a record that reverses ADR 0029 section 1 (3)'s "only"
   and amends ADR 0036's sentence, and a carrier that amends M0-234. This
   package files no row for (a).
8. **One row carries items 1 to 3 of the verification's table.** The message
   of (f) told him that four tasks would follow - the mark, the gate's rule,
   the cases and the rule for holdouts. The mark, the rule and their cases
   share their files and one set of cases, so one row carries the three, and
   the fourth is reading 6 above, a rule for drafters with no code to change.
   That split is the seat's.

## 2. What this ADR does NOT decide

- **Any priority or row.** Those are the rows' footers, each
  **[operator-confirmable]**.
- **The mechanism**: the mark's field, its detail sentence, the retirement
  rule's name and the evidence clause's words. The row that carries the
  decision is their home.
- **`DESIGN.md`**, untouched (reading 5), and any TaskSpec field that would
  declare what a holdout plants - `DESIGN.md` section 5's fields table is his.
- **(a)**, and the count M0-234's requirement pointer would feed (reading 7).
- **RT-17's return** to `repo-truth`'s queue after the row lands - the
  verification's row 7 - which is his hand in his repository.
- **The mutation probe's bound per mutant and the count of a timed-out
  mutant**, met at RT-21's wall of 2026-10-10 (the seat's run journal, archive
  entry that opens "- TICK 38 ACCEPTED") - his next question.
- **The refusals neither (a) nor (b) reaches**, seq 3352 (RT-14) and 3997
  (RT-18), where the reviewer verified a stated requirement only by reading.
- **That any tick, task, condition or the gate passes after any row lands.**

## 3. What is filed elsewhere

The row this package minted is named in its commit messages and is not
listed here, for ADR 0020 section 3's reason: a decision document that
carries a backlog acquires two homes for every row in it.

## 4. Addendum, 2026-10-10 - the change of ADR 0038's reading 3 is the seat's reading, and the history of 2026-10-01

Added by a carrier session (carrier #97, package item K3) by foreman
decision under the standing delegation of 2026-08-25, not by a block, on two
findings of the foreman seat's verifier over carrier #96. No line above this
section is changed; this section qualifies two of them and adds one
paragraph carrier #96's kickoff asked for and the record left out.

**(i) Whose reading the change of ADR 0038's reading 3 is.** Two sentences
above attribute that change to the word: the header's sentence that reads
"the word recorded here changes that reading for one record", and section
1's paragraph that opens "For the one record it names, the word changes ADR
0038 section 1's reading 3". The question of section 0 (a) asked about ADR
0038's rule for an empty stage 5; the refined question of section 0 (c)
names an empty mutation check on a tests-only task and a passed hidden
check, and the question of section 0 (f), which the word answered, names a
machine mark and a passed hidden probe. Neither of the two names ADR 0038
or its reading 3. That reading is itself one of ADR 0038's readings, each
of them THE SEAT'S. So that the mark's retirement changes reading 3 for
the one marked record is THE SEAT'S reading,
**[operator-confirmable]**, as carrier #96's kickoff asked it to be written.
It does not widen his decision: item 1 retires a pointer at a marked record,
which reading 3's last sentence would have counted, and section 1's reading
4 keeps ADR 0038 "for every record but this one". The two sentences stand as
written and are read with this mark.

**(ii) The history of 2026-10-01.** The binding this record's item 1 names
is not new to it. On 2026-10-01 the operator's word of 08:47:18, recorded in
ADR 0043, made the retirements of ADR 0035 and ADR 0038 permanent and bound
both to the holdout. How the binding is read - an entry either rule would
retire leaves condition 2's count only on a candidate whose every declared
holdout item ran and passed, read from the declared items and their answers
and never from condition 1's status - is ADR 0043's readings 1 and 2, THE
SEAT'S, **[operator-confirmable]**, and so is ADR 0043's reading of his yes
as taking the recommendation whole. The seat's recommendation he took that
day named the one false pass on record as the reason, and his earlier word
of 08:02:54 had sanctioned the research it rested on; both are in ADR 0043's
section 0. The refined
question of section 0 (c) above and the question of section 0 (f) put the
tests-only mark to him in that same form, and section 1's reading 2 keeps
ADR 0043's binding unchanged for it.
