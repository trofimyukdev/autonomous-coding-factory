# ADR 0039 - The operator's word on repo-truth: the factory does the work there, its gate is fixed first, and the seat's order and rule are taken

Date: 2026-09-29. Context: a carrier session (carrier #82, package item K2)
opened BY EXCEPTION, on the operator's word and off the standing cadence of
2026-08-25 - not a block. Merge blocks since carrier #81's rework:
`git log --oneline --first-parent fa19f1c..origin/main | grep -c ' merge:'`
printed 2 on 2026-09-29 at 20:22. `main` stood at `9da5f9c` when this
record was committed - `git rev-parse HEAD origin/main | cut -c1-7 | paste -sd' '`
printed `9da5f9c 9da5f9c` on 2026-09-29 at 20:22.
Nothing under `src/`, `test/`, `scripts/`, `.githooks/`, `.claude/`,
`factory/checks.yaml`, `factory/millwright.toml`, `CLAUDE.md`, `PRINCIPLES.md`,
`DESIGN.md` or the private archive was touched by this package, and nothing was
written in `repo-truth`.

This is a new record and not an amendment. It records new words on a new
subject: what the factory does on `repo-truth`, and what it does with a
measurement it did not finish. ADR 0035's rule stands as that record writes it:
under the rule recorded here, as the seat reads it in section 1 (readings 3
and 4, **[operator-confirmable]**), an unfinished measurement is never handed
to condition 2, so ADR 0035 section 1's reading of `error` stays true of every
other incompletion. ADR 0037 is where a carry to the next pass has its
precedent. Neither record is edited.

**This document records an operator word and what it decides. It carries no
mechanism and moves no priority: the rows that carry the decision out are the
homes of their own content and are named in the commit messages.**

## 0. The operator's words, and the messages they answer

Quoted verbatim on ADR 0005's precedent, Russian as typed and with the typing
kept as it is («По этому» for «Поэтому», "that is why"; «чего-оо» for
«чего-то», "something"). One transcript holds them all, the foreman seat's
session: `<transcript>`.
It was read only through read-only tools, on 2026-09-29 between 19:52 and
19:54. The filter ADR 0032 section 0 gives (its `node -e` line is quoted whole
in ADR 0036 section 0) printed six lines, at 14:13:20Z, 14:15:43Z, 14:44:30Z,
14:57:17Z, 15:44:54Z and 15:55:40Z; the last two are the words recorded here,
and the first four - earlier words of the evening and a question about
`repo-truth`'s purpose - are not part of this record. A window lister over
15:15:00Z to 15:56:00Z, which prints the uuid, type, timestamp and first
characters of each user or assistant row that carries text, found the rows
below; each is then printed whole, by its uuid, with the read-only row printer
ADR 0037 section 0 quotes whole. Every quoted line below was found in the
transcript by `grep -c -F '<the line>' <transcript>`, which printed at least 1
for each on 2026-09-29 at 19:53. The row printer prints each of his two words
on two lines; the first line of the 18:44:54 word ends in a space after
«фабрики» ("of the factory"), kept below. Timestamps are UTC; the times below are those
timestamps plus three hours, local time. A quoted block holds whole
sentences; what a message says beyond them is not part of this record.

### (a) The recommendation - 18:24:37

The seat's row at 15:24:37.261Z (assistant), the
seat's report after the second tick of the evening's second series. Its
question and the two options under it, whole:

```text
**Вопрос: что делаем с кандидатом `415ab82`?**
1. **Рекомендую: влить руками сейчас.** Это push двух коммитов в repo-truth плюс запись в журнал фабрики «закрыто вручную», как с RT-01. Пакет сначала прогоню на копии, push — по твоему «делай». Доводы:
   - код проверен всем, что доступно без гейта;
   - repo-truth пока в теневом режиме, так что даже с пройденным гейтом кандидат остался бы на паузе и вливался бы руками;
   - RT-08 сразу разблокируется.
   Минус: в статистику гейта этот merge не попадёт.
2. Держать RT-07 до починки гейта: пересмотр ADR 0035 плюс блок. Это часы работы, и всё это время RT-08 стоит.
```

"Question: what do we do with candidate 415ab82? (1) I recommend: merge it by
hand now. That is a push of two commits to repo-truth plus a record in the
factory's journal, 'closed by hand', as with RT-01. I will first rehearse the
package on a copy; the push on your 'do it'. Reasons: the code is checked by
everything available without the gate; repo-truth is still in shadow mode, so
even with a passed gate the candidate would stay paused and be merged by hand;
RT-08 is unblocked at once. Minus: this merge does not enter the gate's
statistics. (2) Hold RT-07 until the gate is fixed: a revision of ADR 0035
plus a block. That is hours of work, and all that time RT-08 stands."

The report above the question carries figures the journal owns; they are
pointed at, not quoted: the seat's run journal archive entry "TICK 2 OF THE
SECOND SERIES ACCEPTED".

### (b) His first word - 18:44:54, typed in the seat's session

The filter printed it, at 15:44:54.032Z. Its own user row, at 15:44:54.122Z, as the row printer
prints it:

```text
repo-truth у нас, как доказательство работы фабрики 
По этому именно она должна все делать, значит сначала починим гейт? Просто будь собой, подумай глубоко, ты же где-то в глубине знаешь правильный ответ. Просто найди его. Цели мои ты знаешь
```

"repo-truth is ours as the proof of the factory's work. That is why it is she
who must do everything, so we fix the gate first? Just be yourself, think
deeply, somewhere deep down you know the right answer. Just find it. You know
my goals." The row's own fields, printed by
`grep -F '"uuid":"<row>"' <transcript> | grep -o -E '"entrypoint":"[a-z]*"|"origin":\{[^}]*\}|"promptSource":"[a-z]*"'`:
`"origin":{"kind":"human"}`, `"promptSource":"queued"` and
`"entrypoint":"cli"`. It was typed in the seat's session.

### (c) The seat's answer - 18:48:35

The seat's row at 15:48:35.968Z (assistant), the
message his second word follows. Its opening paragraph and the paragraph on
the hand merge, whole:

```text
Ты прав, а я ошибся. Влить руками значило бы продвинуть продукт, но ничего не доказать про фабрику. Правильный ответ даже жёстче, чем «сначала починить гейт».

**Почему ручной merge был ошибкой.** repo-truth — доказательство, что фабрика сама доводит задачу до проверенного merge. Слияние руками даёт ноль в метрике «$ за проверенный merge» и прячет дефекты фабрики за человеком. RT-01, влитая руками, была инцидентом, а не образцом. Этот урок записал в память.
```

"You are right, and I was wrong. Merging by hand would have moved the product
forward but proved nothing about the factory. The right answer is even
stricter than 'fix the gate first'. Why the hand merge was a mistake: repo-truth is the
proof that the factory itself takes a task to a verified merge. A merge by
hand gives zero in the metric '$ per verified merge' and hides the factory's
defects behind a human. RT-01, merged by hand, was an incident, not a model. I
wrote this lesson to memory."

Its heading on the gate and the first sentence of the bullet under it, and
the second bullet, whole:

```text
**Что сегодня показал repo-truth: гейт ошибается в обе стороны.**
- **Пропускает брак — это опаснее всего.**
- **Отказывает хорошему.** Фабрика засчитала кандидату файлы, которые оставил ревьюер, и это стоило попытку. А недомеренную стадию мутаций она считает отказом при каждом тике.
```

"What repo-truth showed today: the gate errs in both directions. - It lets
defects through; that is the most dangerous. - It refuses good work. The
factory charged the candidate with files the reviewer left, and that cost an
attempt. And it counts an under-measured mutation stage as a refusal on every
tick." The rest of the first bullet, and a third bullet on the ladder's rung,
carry figures the journal and the queue own, and are not quoted.

Its order, whole:

```text
**Порядок:**
1. **Carrier сейчас, вне обычной очереди.** Две новые строки: «оставленные ревьюером файлы» и «незаконченное измерение». Правило для второй: незаконченное измерение не судится — фабрика доводит его до конца в следующем проходе. M0-59 (исполнитель holdout-проверок) поднять выше финишной черты.
2. **Блоки строят эти три вещи.** Я пишу для RT-07 holdout-пробу из её приёмки и `not_done_if` — те самые 7 случаев, что сегодня гонял руками. Лежать она будет вне репозитория, билдер её не увидит.
3. **RT-07 сама проходит починенный гейт.** Кандидат `415ab82` сохранён и ждёт.
4. **M5-03 закрываем на этом честном пропуске, а не на сегодняшнем частично ложном.**
5. **Растим очередь repo-truth до 10 задач**, прошедших гейт → переход на ступень 2 → первый merge, который фабрика делает сама.
```

"Order: (1) A carrier now, outside the usual queue. Two new rows: 'files left
by the reviewer' and 'the unfinished measurement'. The rule for the second:
an unfinished measurement is not judged - the factory finishes it in the next
pass. M0-59 (the runner of holdout checks) raised above the finish line. (2)
Blocks build these three things. I write a holdout probe for RT-07 from its
acceptance and `not_done_if` - the same seven cases I ran by hand today. It
will lie outside the repository; the builder will not see it. (3) RT-07
passes the fixed gate by itself. Candidate 415ab82 is kept and waits. (4) We
close M5-03 on that honest pass, not on today's partly false one. (5) We grow
repo-truth's queue to ten tasks that passed the gate -> the move to rung 2 ->
the first merge the factory makes by itself." The seven cases of the line
that opens «Блоки строят эти три вещи» ("Blocks build these three things") are the seat's own smoke, relayed in the archive entry named in (a); the ten
tasks of the line that opens «Растим очередь repo-truth» ("We grow repo-truth's queue") are the ladder's threshold for rung 2. Neither figure is
re-taken here.

Its price, and the question his word answers, whole:

```text
**Цена:**
- С утра Weekly вырос с 59 до 72 %: четыре блока, carrier и тики. План «carrier и три блока» примерно того же масштаба и упирается в потолок фабрики 85 %.
- Скорее всего, на этой неделе успеем carrier и два блока, а тики на RT-07 — после сброса 3 октября.
**Вопрос: утверждаешь этот порядок?** Рекомендую: да. Если да, сейчас готовлю и открываю carrier.
```

"Price: since the morning Weekly has risen from 59 to 72 %: four blocks, a
carrier and ticks. The plan 'a carrier and three blocks' is about the same
scale and runs into the factory's ceiling of 85 %. Most likely this week we
manage the carrier and two blocks, and the ticks on RT-07 after the reset on
3 October. Question: do you approve this order? I recommend: yes. If yes, I
prepare and open the carrier now." The Weekly figures are the seat's readings
of its statusline and are not re-taken here.

### (d) His second word - 18:55:40, typed in the seat's session

The filter printed it, at 15:55:40.095Z. Its own user row, at 15:55:40.164Z, as the row printer
prints it:

```text
Да, но когда достигнешь 85% лимитов приостановись, потом возможно продолжим
Возможно лимиты будут нужны для чего-оо еще
```

"Yes, but when you reach 85% of the limits, pause; then perhaps we will
continue. Perhaps the limits will be needed for something else." The row's
own fields, printed by
`grep -F '"uuid":"<row>"' <transcript> | grep -o -E '"entrypoint":"[a-z]*"|"origin":\{[^}]*\}|"promptSource":"[a-z]*"'`:
`"origin":{"kind":"human"}`, `"promptSource":"queued"` and
`"entrypoint":"cli"`. It was typed in the seat's session.

## 1. The decision

1. **ON `repo-truth` THE FACTORY DOES THE WORK.** «именно она должна все
   делать» ("it is she who must do everything") of (b), with «она» ("she")
   read as the factory, and the hand merge the
   seat recommended in (a) not taken - both are reading 8 below, THE SEAT'S,
   **[operator-confirmable]**, since his sentence does not name the factory
   or say no in words.
2. **THE GATE IS FIXED FIRST.** «сначала починим гейт?» ("we fix the gate
   first?") of (b), and his «Да» ("Yes") of (d) to the answer of (c).
3. **THE ORDER of the answer (c) is taken**, by that «Да».
4. **THE RULE of the answer (c) is taken**, by the same «Да» read as taking
   the answer whole - reading 1 below, THE SEAT'S,
   **[operator-confirmable]**: an unfinished measurement is not judged, and
   the factory finishes it in the next pass.
5. **THE PAUSE.** «когда достигнешь 85% лимитов приостановись, потом
   возможно продолжим» ("when you reach 85% of the limits, pause; then
   perhaps we will continue") of (d).

THE CORRECTION the record carries: the order's line that opens «RT-07 сама
проходит починенный гейт» ("RT-07 passes the fixed gate by itself") says «Кандидат `415ab82` сохранён и ждёт»
("candidate 415ab82 is kept and waits"). The code at `9da5f9c` keeps it as
evidence and does not judge it again - in `landUnmeasuredRefusal`'s docstring
(src/controller/fix-cycle.ts), "and it is kept as EVIDENCE: the next pass does
not re-verify this candidate.", and the docstring goes on to say that
`dispatchOne` prepares a fresh workspace on the base branch and opens a
builder again. This record promises no judgement of 415ab823; what RT-07
passing "by itself" then means is reading 6 below, THE SEAT'S,
**[operator-confirmable]**.

Eight readings follow. Each is **THE SEAT'S**, and each is
**[operator-confirmable]**:

1. **His «Да» takes the answer (c) whole** - its order and its rule, not
   the order alone - as ADR 0037 section 1's reading 1 read "the recommended
   option" as the recommendation whole. The answer's closing question asks
   about the order; the rule sits inside it, on the order's line that opens
   «Carrier сейчас, вне обычной очереди» ("A carrier now, outside the usual
   queue").
2. **"The gate" is fixed in both directions.** The answer says in words that
   the gate errs both ways («гейт ошибается в обе стороны»): a false pass - the
   first gate pass on `repo-truth`, on a candidate its own spec's `not_done_if`
   forbade, found by the seat's hand-run and not by the gate - and false
   refusals, on files a verification seat left and on an unfinished
   measurement. That the order's rows are the fix for both is the seat's
   reading of his «Да».
3. **"Unfinished" is a stage-5 measurement the probe's time budget cut** -
   what the probe records as `time_ceiling`, wherever in its list the cut
   fell. Every other way the probe can fail to finish is judged as today.
4. **"In the next pass" is the next pass that takes the row, over the same
   candidate, base and probe configuration, with a ceiling.** A measurement
   that no pass can finish ends as the infrastructure failure it is today and
   is never judged.
5. **The order's "M0-59 raised above the finish line" is two rows.** M0-59's
   own acceptance is one half, and the runner the answer's parenthesis names
   is M0-131's by its title. So both are raised, and each row says which half
   it builds. At `9da5f9c` nothing runs holdout acceptance at all -
   src/controller/gate-input.ts says so in a comment:
   `// Nothing runs holdout acceptance yet (M0-59), and the gate answers that`
   - and hands the gate `holdout: null`. The seat's holdout probe for RT-07,
   on the order's line that opens «Блоки строят эти три вещи», reaches RT-07's
   gate only through what that runner reads: if it reads a `holdout: true`
   item of the spec, that item needs a cancel of RT-07's live row and then a
   new version of its spec on `repo-truth` - intake defers a new version while
   the live one sits in RETRY_WAIT - which is the operator's hand and not this
   package's.
6. **"RT-07 passes the fixed gate by itself" is RT-07's next pass**, which
   builds afresh, as the correction above says; 415ab823 is evidence.
7. **«85% лимитов» ("85% of the limits") is the Weekly figure on the seat's
   statusline**, the one the answer's price names beside «потолок фабрики 85 %»
   ("the factory's ceiling of 85 %"); and «приостановись» ("pause") is: the seat starts nothing new at or above it and asks anything in flight
   to stop at its nearest clean boundary, then reports. Resuming is his word
   («потом возможно продолжим», "then perhaps we will continue"). This record says when he gave the word and
   does not decide whether it binds a seat after a handover: the seat's run
   journal holds that it does not, as the seat's own rule, which is neither his
   word nor this record's.
8. **«она» ("she") is the factory and «все» ("everything") is every step a
   task takes there, the merge among them.** «она» is read as «фабрики», the feminine noun before it
   in (b); so the hand merge is not taken, on a sentence that does not say no
   in words.

## 2. What this ADR does NOT decide

- **Any priority, or the order of the rows.** Those are the rows' footers,
  each **[operator-confirmable]**.
- **The rows' mechanisms**, the carry's record and its ceiling among them.
  The rows are their homes.
- **ADR 0035's rule and its revisit.**
- **M0-127's priority**, which is his open question.
- **The reviewer's model and the factory's model defaults** (M0-242).
- **The factory's own weekly ceiling**, `budget.rate_limit`, which
  `repo-truth`'s tick log prints as "against a ceiling of 85 =
  min(weekly_threshold_pct 85, 100 - weekly_reserve_pct 10)": the same number,
  another mechanism.
- **`DESIGN.md`**, untouched. Section 9's opening sentence stands: "All seven
  are required, and a required check that cannot be run is an infrastructure or
  gate failure - never a pass." Under the rule an unfinished measurement is
  finished, never passed, and stage 5 is advisory (`ADVISORY_STAGES`,
  src/verify/run.ts); that the rule does not touch the sentence is THE SEAT'S
  reading, **[operator-confirmable]**.
- **The holdout probe's content and RT-07's new spec version**, the seat's
  and his hand.
- **The tick series**, which waits for his separate word.
- **That RT-07, a condition, the gate or a tick passes after any row lands.**

## 3. What is filed elsewhere

The rows this package minted or raised are named in its commit messages and
are not listed here, for ADR 0020 section 3's reason: a decision document that
carries a backlog acquires two homes for every row in it.
