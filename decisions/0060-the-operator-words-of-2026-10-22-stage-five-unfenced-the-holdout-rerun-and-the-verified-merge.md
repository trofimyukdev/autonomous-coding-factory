# ADR 0060 - The operator's words of 2026-10-22: a stage 5 handed no fence starts nothing, a merged task's holdout is re-run after later merges, and what a verified merge is

Date: 2026-10-22. Context: a carrier session (carrier #114, package item
K1), by foreman decision under the standing delegation of 2026-08-25 -
not a block - to give a home to four words the operator typed in the
foreman seat's session on the morning of 2026-10-22, and to the questions
they answer. One commit writes this record, DESIGN.md's sentences in
sections 6, 10 and 14 that the words need, and those three sections'
digests, each with its dated paragraph, in
test/unit/design-ratification.test.ts.

**This document records operator words and what they decide. It carries
no mechanism and moves no priority. ADR 0021 is not edited by it;
section 3 below amends that ADR's decision (e). Each row that carries a
word out points here (discipline 12).**

## 0. The words, and the questions they answer

Quoted verbatim on ADR 0059's precedent, Russian as typed, each beside
its English translation. One transcript holds every row of (a) to (d),
the session of the foreman seat then, `<transcript>` below. Each row
was printed by its uuid from the transcript, and each
quoted line equals a whole line of the row's text, character for
character; line numbers count the row's text lines from 1, blank lines
included. Timestamps are UTC; the time beside each is that timestamp
plus three hours, local time. Every proposal below is the
seat's, made in its own question row; only his rows are his.

### (a) Stage 5 handed no fence - 2026-10-22 08:58:27

The question. The seat first put it in its assistant row at
2026-10-22T04:27:29.548Z (07:27:29), its last line, line 21:

```text
Один вопрос, первый из утренних. Блок 239 изменил старое решение M3-13 о пятой стадии проверки. Раньше, если её вызвать без ограды, она молча гоняла бы тесты кандидата с твоими правами. Теперь она в таком случае ничего не запускает и отвечает «ошибка». Тик ограду передаёт, так что на работе фабрики это не сказывается. Рекомендую подтвердить. Подтверждаешь?
```

"One question, the first of the morning's. Block 239 changed M3-13's old
decision on the fifth stage of verification. Before, if it was called
with no fence, it would silently run the candidate's tests with your
rights. Now in that case it starts nothing and answers 'error'. The tick
hands it the fence, so the factory's work is not affected. I recommend
confirming. Do you confirm?"

The seat's assistant row at
2026-10-22T05:18:11.370Z (08:18:11), its stop reason `end_turn`, is the
last seat text before his word, and it repeats the question in its last
line, line 17: between the two rows the transcript holds one `system` row and two
`queue-operation` rows, the enqueue and dequeue of his message, and no
other text.

```text
И жду ответа про решение 4: пятая стадия без ограды отвечает «ошибка» и ничего не запускает. Подтверждаешь?
```

"And I am waiting for your answer on decision 4: the fifth stage with no
fence answers 'error' and starts nothing. Do you confirm?"

The word. His row at
2026-10-22T05:58:27.284Z (08:58:27), `origin.kind` `human`, its one line:

```text
Да
```

"Yes"

### (b) A merged task's holdout fails after later merges - 2026-10-22 09:05:38

The question. The seat's assistant row at
2026-10-22T06:01:31.185Z (09:01:31), its stop reason `end_turn`, is the last seat text before his
word and the row that put the question: between the two rows the transcript holds
one `system` row and two `queue-operation` rows, the enqueue and dequeue
of his message, and no other text. Its lines 5, 7, 8 and 10:

```text
**Что делать, если скрытый экзамен уже принятой задачи начал падать.** Сейчас скрытый экзамен задачи (holdout) прогоняется один раз, перед её слиянием. Если потом другая задача сломает уже принятую, этого никто не заметит: проверка после слияния гоняет быстрый smoke-прогон, а не экзамены прошлых задач. Предложение такое: после новых слияний заново прогонять экзамены уже принятых задач. Вопрос в том, что делать при провале:
- **(а) Только сигнал тебе**, задача остаётся в «сделанных». Так предлагал Codex.
- **(б) Как DESIGN уже велит для регрессий после слияния.** Откатывать ничего не надо: задача возвращается в BLOCKED, инцидент записывается, тебе приходит сообщение.
Рекомендую (б). Задача, чей экзамен больше не проходит, уже не проверена, и оставлять её в «сделанных» значит завышать главную метрику. К тому же это не новое решение, а действующее правило DESIGN §10. Цена — только прогоны тестов, без вызовов модели. Как и сколько экзаменов прогонять, решит автор задачи, с ограничением.
```

"**What to do if the hidden exam of an already accepted task starts to
fail.** Today a task's hidden exam (the holdout) is run once, before its
merge. If another task later breaks an accepted one, nobody will notice:
the check after the merge runs a fast smoke, not the exams of earlier
tasks. The proposal: after new merges, re-run the exams of tasks already
accepted. The question is what to do on a failure: / - **(a) Only a
signal to you**, the task stays among the done ones. This is what Codex
proposed. / - **(b) As DESIGN already orders for regressions after a
merge.** Nothing needs to be reverted: the task goes back to BLOCKED, an
incident is written, a message comes to you. / I recommend (b). A task
whose exam no longer passes is no longer verified, and leaving it among
the done ones inflates the main metric. Besides, this is not a new
decision but DESIGN section 10's standing rule. The price is test runs
only, with no model call. How and how many exams to run, the task's
author will decide, with a ceiling."

The word. His row at
2026-10-22T06:05:38.981Z (09:05:38), `origin.kind` `human`, its one line:

```text
б
```

"b"

### (c) What a verified merge is - 2026-10-22 09:29:02

The question. The seat's assistant row at
2026-10-22T06:07:47.186Z (09:07:47), its stop reason `end_turn`, is the last seat text before his
word and the row that put the question: between the two rows the transcript holds
one `system` row, the session's bookkeeping rows (among them the echo of
the last prompt and the session's name), and two `queue-operation` rows,
the enqueue and dequeue of his message, and no assistant or user text. Its lines 5, 8, 9, 10 and 12:

```text
Сейчас по ADR 0021 проверенной считается любая задача в DONE. Но я пересчитал по журналу repo-truth: из 56 слияний фабрики только 4 последних (RT-54…RT-57) прошли настоящую проверку после слияния. У 52 более ранних такая проверка просто не была настроена. До слияния они прошли все проверки, но после слияния их никто не перепроверил.
- **(а)** Считать, как сейчас, все DONE, но всегда печатать рядом, сколько из них прошли проверку после слияния. Под это уже заведена задача M0-327.
- **(б)** В главной метрике считать только задачи, прошедшие проверку после слияния. Остальные идут отдельной строкой «слито, не перепроверено».
- **(в)** Отдельная настройка для каждого потребителя.
Рекомендую сейчас (а), а на (б) перейти, когда в repo-truth пять слияний подряд пройдут проверку после слияния. Сейчас таких подряд четыре, пятым может стать RT-58 из ближайшего пакета. Так метрика задним числом не рухнет с 56 до 4, но и непроверенное за проверенное не выдаст: разбивка будет видна всегда.
```

"Today, by ADR 0021, any task in DONE counts as verified. But I
re-counted over repo-truth's journal: of the factory's 56 merges only
the last 4 (RT-54 to RT-57) passed a real check after the merge. For the
52 earlier ones no such check was configured at all. Before the merge
they passed every check, but after it nobody re-checked them. / - **(a)**
Count, as now, every DONE, but always print beside it how many of them
passed the check after the merge. Task M0-327 is already filed for this.
/ - **(b)** In the main metric count only the tasks that passed the check
after the merge. The rest go on a line of their own, 'merged, not
re-checked'. / - **(c)** A separate setting per consumer. / I recommend
(a) now, and moving to (b) when five merges in a row in repo-truth pass
the check after the merge. Today there are four such in a row; RT-58 from
the next packet may become the fifth. That way the metric does not
collapse after the fact from 56 to 4, and it does not pass off the
unchecked as checked either: the split will always be visible."

The word. His row at
2026-10-22T06:29:02.267Z (09:29:02), `origin.kind` `human`, its one line:

```text
Согласен с твоими рекомендациями
```

"I agree with your recommendations"

### (d) The edge DONE -> BLOCKED - 2026-10-22 10:42:18

The question. After the carrier reported that two premises of (b)'s
question were wrong (section 2), the seat put a corrected question in its
assistant row at
2026-10-22T06:46:35.942Z (09:46:35), its stop reason `end_turn`. Its
lines 5, 6, 9, 12 and 14:

```text
1. **Задачу в DONE сейчас нельзя вернуть в BLOCKED.** По DESIGN задача в DONE окончательна. Единственный обратный путь — снять ошибочное закрытие, и тогда задача уходит в начало очереди, а не в BLOCKED. Правило про BLOCKED, на которое я ссылался, срабатывает раньше: на проверке сразу после слияния, пока задача ещё не в DONE.
2. **Уведомления о регрессии после слияния в коде нет.** Задача паркуется, инцидент записывается, а сообщение тебе не уходит. Эта часть правила так и не построена.
- **(б), с добавлением в DESIGN.** Разрешить второй обратный переход: DONE → BLOCKED, когда экзамен уже принятой задачи провалился на более поздней базе. В остальном DONE остаётся окончательным. Уведомление построит та же новая задача.
Рекомендую (б) с добавлением. Уведомление нужно строить в обоих вариантах, так что вся разница в одном переходе. Зато задача с проваленным экзаменом перестаёт считаться проверенной и сама не пересобирается: снимать BLOCKED будешь ты.
Делаем (б) с новым переходом в DESIGN или переходим на (а)?
```

"1. **A task in DONE cannot be returned to BLOCKED today.** By DESIGN a
task in DONE is final. The only way back is to withdraw a close made in
error, and then the task goes to the head of the queue, not to BLOCKED.
The rule about BLOCKED I referred to fires earlier: at the check right
after the merge, while the task is not yet in DONE. / 2. **There is no
notification of a regression after a merge in the code.** The task is
parked and the incident written, but no message goes to you. That part
of the rule was never built. / - **(b), with an addition to DESIGN.**
Allow a second backward transition: DONE -> BLOCKED, when the exam of an
already accepted task failed on a later base. Otherwise DONE stays
final. The same new task will build the notification. / I recommend (b)
with the addition. The notification has to be built in both options, so
the whole difference is one transition. In return a task with a failed
exam stops counting as verified and does not rebuild itself: you will be
the one to clear BLOCKED. / Do we do (b) with the new transition in
DESIGN, or move to (a)?"

The seat's assistant row at
2026-10-22T07:21:00.629Z (10:21:00), its stop reason `end_turn`, is the
last seat text before his word, and its lines 8 and 10 add to the
question and repeat it: between the two rows the transcript holds one `system` row,
the session's bookkeeping rows, and two `queue-operation` rows, the
enqueue and dequeue of his message, and no assistant or user text.

```text
- **Дополнение к моему вопросу.** Верификатор курьера нашёл ещё одну тонкость варианта (б). Если задача уходит из DONE в BLOCKED, её ждущие новые версии без отдельной меры стали бы доступны для сборки, и фабрика пересобрала бы их без тебя. Поэтому в (б) они в тот же момент ставятся на паузу. Тогда моё «сама не пересобирается» остаётся правдой.
Вопрос тот же: делаем (б) с новым переходом DONE → BLOCKED в DESIGN или (а), только сигнал? Если ответа не будет до 11:30, курьер оформит всё остальное без этого пункта, а его возьмёт следующий курьер.
```

"- **An addition to my question.** The courier's verifier found one more
subtlety of option (b). If a task leaves DONE for BLOCKED, its waiting
new versions would, without a separate measure, become available to
build, and the factory would rebuild them without you. So in (b) they
are paused at the same moment. Then my 'does not rebuild itself' stays
true. / The question is the same: do we do (b) with the new transition
DONE -> BLOCKED in DESIGN, or (a), a signal only? If there is no answer
by 11:30, the courier will file everything else without this item, and
the next courier will take it."

The word. His row at
2026-10-22T07:42:18.262Z (10:42:18), `origin.kind` `human`, its one line:

```text
Делаем (б) с новым переходом
```

"We do (b) with the new transition"

## 1. What the first word decides

His word is a yes to the question of (a): a stage 5 that is handed no
fence starts no test of the candidate and answers `error`. Block239
(M0-268, merge 440bd57) wrote that reading into decision 4 of
src/verify/strength.ts's header, the paragraph that opens "4. **The
production probe is wired in code, and never quietly absent.**", and
recorded it as its own reading, which M3-13's earlier wording had
decided otherwise - the decision's heading read "the production probe is
the default" from cb2d38f (M3-13) until ca23117 (M0-268), by
`git log -S'production probe is the default' --oneline -- src/verify/strength.ts`
on 2026-10-22; his yes makes it his decision. That header paragraph, with `NO_FENCE` in the same
file, is the decision's one home, and this record restates none of it.

No sentence of DESIGN.md or of docs/decisions/ states the old reading:
`git grep -n -i -F 'production probe is the default' -- DESIGN.md docs/decisions`
printed nothing and exited 1 on 2026-10-22 09:43 local time, so no sentence is
edited for this word. DESIGN.md section 8's stage 5 row names the test
strength lens ("mutation probe or reproduction test") and says nothing of
what it does with no fence.

## 2. What the second and fourth words decide

His word is (b) of the seat's question: a merged task's holdout is
re-run after later merges, and a failure takes the rule DESIGN.md
section 10 holds for a regression after a merge - the row goes to
BLOCKED, an incident is written, he is notified, and nothing is
reverted. src/controller/post-merge.ts's header already takes that
branch for the post-merge smoke ("A regression parks; it never
reverts"). The proposal of a re-run is the seat's, its line 5; (a) was
Codex's, as line 7 says; only the choice of (b) is his.

**Two premises of the question were wrong, and the carrier found them
before this record was written.** The question said the task "goes back
to BLOCKED" as section 10 orders, and that a message comes to him; but a
DONE row had no edge to BLOCKED - DESIGN.md section 6 called `DONE ->
QUEUED` "the only edge that takes a record back" - and a parked
post-merge regression notifies nobody today, no post-merge alert being
routed. M0-333's THE PREMISES holds both facts with their anchors. The
seat put the corrected question to him, (d), and his answer to (d) takes
(b) with the new transition: DONE -> BLOCKED, a second withdrawal edge,
DONE otherwise terminal, and the notification built by the row that
carries the word out.

**What the record writes.** DESIGN.md section 10's post-merge sentence
gains the re-run: the holdouts of tasks merged earlier are re-run after
later merges, and a failure takes the circuit-plus-notification branch,
never a revert - the row leaves DONE for BLOCKED, an incident is
written and he is notified, not built yet. Section 6 gains the edge
`DONE -> BLOCKED` as a second withdrawal edge, so DONE stays terminal,
walked by one named store operation, and its sentence on `DONE ->
QUEUED` now names both. The wording of both sentences is THE SEAT'S
READING **[operator-confirmable]**: he chose (b); the seat wrote the
sentences.

How often and over which rows a holdout is re-run, what an unmeasured
re-run does, and how a newer version of a parked row's spec is kept from
being rebuilt are M0-333's, which marks each as a reading beyond his
words, as the seat's question left the bound to the row ("with a
ceiling"). That row builds the notification too, which (a) would also
have needed. Section 6's clause that a waiting newer version is paused
with the parked row is THE CARRIER'S READING **[operator-confirmable]**:
without it the row's leaving DONE would reopen its spec id, while the
seat told him the row does not rebuild by itself. The seat put that
pause to him inside the question his word of (d) answers (its row of
10:21:00, line 8); his words name the transition and not the pause, so the mark
stays.

## 3. What the third word decides, and the amendment of ADR 0021 (e)

His word takes the seat's recommendations of (c) together: (a) now, and
(b) once repo-truth has five merges in a row measured `passed`.

**ADR 0021 (e)'s premise no longer holds.** That decision chose DONE as
the denominator of "verified merge" because "DONE is the state a row
reaches only by passing the post-merge check". Since a check that
measured nothing also ends at DONE, the premise is false for most of
repo-truth's factory merges: over repo-truth's journal read as a file,
`node <home>/rt-done.js <repo-truth>/factory/state/events.jsonl`
(a read-only count of `TASK_DONE` events by the opening of their
`reason`) printed `{"other: bookkeeping: block RT-01 landed as 104943247b514c0":1,"unmeasured":52,"passed":4}`
on 2026-10-22 09:43 local time - 52 rows whose reason opens "the post-merge
check was unmeasured", 4 whose reason opens "the post-merge check
passed", and one landing recorded by hand with no post-merge check.
The false sentences in the code are M0-323's to correct; this record
does not restate them.

**The amendment.** ADR 0021 (e) is amended, not edited: (1) now, a
verified merge stays a DONE row - every DONE row, whether its post-merge check
passed, measured nothing or never ran - and M0-327, once it lands,
prints beside it how many of those rows carry each post-merge verdict;
(2) once
repo-truth's journal holds five consecutive factory merges whose
post-merge check passed, a verified merge becomes a DONE row whose
check passed, and every other DONE row - unmeasured or never checked -
is printed on a line of its own, his option's "the rest". DESIGN.md section 14 now says both in one sentence below its
metrics block.

Readings beyond his words, each THE SEAT'S READING
**[operator-confirmable]**:

- The four `passed` merges standing today (RT-54 to RT-57) count toward
  the five, as the seat's question says ("Today there are four such in a
  row").
- The trigger is measured on repo-truth alone, as his word names it, and
  the switch then changes what the factory's metric counts as a verified
  merge for every consumer, since (c)'s option of a setting per consumer was not
  taken.
- The definition is the one both figures DESIGN.md section 14 names for
  a verified merge use, `usd_and_tokens_per_verified_merge` and
  `verified_merge_rate`.

The row for (2) is not filed by this record: the foreman seat raises it
when the fifth consecutive `passed` lands in repo-truth's journal.

## 4. What this record does not decide

- Whether the factory ever reverts its own merge: src/controller/
  post-merge.ts's header records that question for the operator, and his
  word (b) takes the branch that does not revert; the question itself
  stays his.
