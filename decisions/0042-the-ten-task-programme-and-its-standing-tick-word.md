# ADR 0042 - The operator's words of 2026-09-30 17:16:03, 19:11:02 and 23:36:07: the ten-task programme on repo-truth, its standing tick word, and the packet; the successor seat's first tick under that word was refused by the harness

Date: 2026-09-30. Context: a carrier session (carrier #85, package item K4)
by foreman decision under the standing delegation of 2026-08-25, opened off
cadence by exception - not a block - to carry into their record the operator's
words that have waited for one since he typed them. Merge blocks since carrier
#84's last commit:
`git log --oneline --first-parent f420448..origin/main | grep -c ' merge:'`
printed 2 on 2026-09-30 at 22:51. `main` stood at `b4196e7` (`origin/main` at `a2c6ee4`) when
this record was committed - `git rev-parse HEAD origin/main | cut -c1-7 | paste -sd' '`
printed `b4196e7 a2c6ee4` on 2026-09-30 at 22:51.
Nothing under `src/`, `test/`, `scripts/`, `.githooks/`, `.claude/`,
`factory/checks.yaml`, `factory/millwright.toml`, `CLAUDE.md`, `PRINCIPLES.md`,
`DESIGN.md` or the private archive was touched by this package, and nothing was
written in `repo-truth`.

This is a new record and not an amendment. ADR 0039 section 1 takes the
order whose line that opens «Растим очередь repo-truth до 10 задач» ("We
grow repo-truth's queue to 10 tasks") grows `repo-truth`'s queue to ten
tasks, and ADR 0040
the pause at 95 %; this record adds the later words on how that step runs.
Neither is edited.

**This document records operator words and what they decide, and one fact
about the first act under them. It carries no mechanism and moves no
priority: the rows that carry anything out are the homes of their own content
and are named in the commit messages.**

## 0. The words, and the messages they answer

Quoted verbatim on ADR 0005's precedent, Russian as typed and with the typing
kept as it is (in (a), three spaces before «И проджект» ("And project"),
«А по этому, я акты в итоге статус?» as typed - a garbled line, rendered in
(a) below - and «rt-07» in lower case). Two transcripts hold them:
T1 = `<transcript-1>` (the earlier foreman seat's, closed), and
T2 = `<transcript-2>` (the next foreman seat's, its live session then, which
grows while it is read).
They were read only through read-only tools, on 2026-09-30 between 22:22 and
22:28, and T2 again at 23:47 for (h).

The filter ADR 0032 section 0 gives (its `node -e` line is quoted whole in
ADR 0036 section 0) printed six lines over T1, at 12:33:34.254Z
(a command line, not a word), 13:27:18.905Z, 13:56:15.815Z, 14:16:03.625Z,
16:11:02.497Z and 17:09:42.091Z. Over T2 it printed none at 22:22 and one
at 23:47, at 20:36:06.968Z. The words recorded here are the lines at
13:56:15, 14:16:03 and 16:11:02 over T1 and the line over T2. Not part of
this record: «Да» ("Yes") at 13:27:18 (16:27:18 local time, the ticks on
RT-07 - a spend, done) and his questions at 17:09:42 (20:09:42 local time),
which decide nothing.
Each filter line carries the same words as the user row named below, whose
own timestamp is 52 to 101 milliseconds later; the row's timestamp is the
one given here.

A window lister prints the uuid, type, timestamp and first characters of each
user or assistant row in a time window that carries text (ADR 0040 section 0
describes it). Each row below is printed by its uuid with the read-only row
printer ADR 0037 section 0 quotes whole; the two rows of (g) that carry no
text block are printed by a tool-row printer of the same form, which prints a
row's `tool_use` input and `tool_result` content instead. Each user row's
fields are printed by
`grep -F '"uuid":"<uuid>"' <transcript> | grep -o -E '"entrypoint":"[a-z]*"|"origin":\{[^}]*\}|"promptSource":"[a-z]*"'`.
Every quoted line below was found in its transcript by
`grep -c -F -e '<the line>' <transcript>`, which printed at least 1 for each
on 2026-09-30 at 22:28, and for (h) at 23:47. Timestamps are UTC; the times below are those
timestamps plus three hours, local time. A quoted block holds whole
sentences; what a message says beyond them is not part of this record.

### (a) His questions - 16:56:15, typed in the earlier foreman seat's session

His user row in T1 at 13:56:15.916Z, as the row printer prints it:

```text
Не совсем понял, наша фабрика должна делать и пуш, верно?
Тогда что от меня нужно?
И кроме этого, задание rt-07, оно разве не первое в списке этой репо для фабрики?
Я ожидаю от тебя более проективного архитектурного   И проджект менеджерского подхода
А по этому, я акты в итоге статус? Куда мы движемся?
Мне казалось уже есть давно обусловленная дорога к цели, разве нет? Где мы сейчас?
И в итоге, чем я действительно могу помочь?
Подумай хорошо, и ответь полноценно но коротко на все эти вопросы. Без воды, по делу
```

"I did not quite understand: our factory must do the push as well, right?
Then what is needed from me? And besides that, task rt-07 - isn't it the
first in this repository's list for the factory? I expect from you a more
forward-looking architectural and project-management approach. And so -
[a line garbled as typed, which the seat read as asking] what is the status
in the end? Where are we heading? It seemed to me there has long been an
agreed road to the goal, hasn't there? Where are we now? And in the end, how
can I really help? Think well, and answer all these questions fully but
briefly. No filler, to the point." Its fields: `"origin":{"kind":"human"}`,
`"promptSource":"queued"` and `"entrypoint":"cli"`. Questions; they decide
nothing by themselves.

### (b) The seat's answer and question - 16:59:05

The seat's row in T1 at 13:59:05.450Z (assistant). Its first paragraph says
the classifier gave no verdict on Bash three times in a row, so the figures
below it are readings taken earlier that day with their times; they are the
seat's readings and are not re-taken here. Its sections 1 to 3 - the push, RT-07's place, and the road - carry figures the journal and
the queue own, and are pointed at. Its section 4, whole:

```text
**4. Что меняю.** Признаю: я вёл очередь реактивно — 34 посадки подряд ушли на ремонт гейта (бриф). После M0-267 (он уже идёт, доведу) следующие строки millwright по приоритету не беру. Веду программу «10 задач»:
- **RT-04…06** освободить глаголом, влитым в M0-258 (у них попытки не исчерпаны).
- **RT-02 и RT-03** перевыпустить новой версией спеки: у них бюджет попыток кончился.
- **3–4 новые независимые задачи RT-09+** дописать без зависимостей, чтобы ступень 1 их не блокировала.
- **Тики** — по одной задаче. Сегодняшний стоил $0.98 и занял 7 минут.

Строки millwright беру только тогда, когда тик вскроет дефект гейта. Оценка: 10 задач — день-два и несколько процентов Weekly.
```

"4. What I am changing. I admit it: I ran the queue reactively - 34 landings
in a row went on repairing the gate (the brief). After M0-267 (it is already
running; I will see it through) I do not take the next millwright rows by
priority. I run the '10 tasks' programme: release RT-04...06 with the verb
merged in M0-258 (their attempts are not exhausted); reissue RT-02 and RT-03
as a new version of their specs (their attempt budget is spent); write 3-4
new independent tasks, RT-09 on, with no dependencies, so that rung 1 does
not block them; ticks - one task each. Today's cost $0.98 and took 7
minutes. I take millwright rows only when a tick exposes a gate defect.
Estimate: 10 tasks - a day or two and a few percent of Weekly."

Its section 5 and its closing line, whole:

```text
**5. Чем ты реально помогаешь** — это можешь только ты:
1. **Постоянное слово на тики repo-truth на ступени 1** (в `main` ничего не уходит), в пределах паузы 95 % и дневного лимита. Без нового слова на каждую серию и после передачи кресла; я оформлю его ADR.
2. **Утвердить пакет задач для repo-truth** — это твой публичный репозиторий, пуш идёт по твоему слову.
3. **Решение о переходе на ступень 2**, когда лестница его предложит: это и будет первое автослияние.

**Вопрос: запускаю программу «10 задач» на этих условиях?** Рекомендую: да. Если да, после M0-267 готовлю пакет задач и приношу его одним сообщением.
```

"5. How you really help - only you can do this: (1) A standing word for
ticks on repo-truth at rung 1 (nothing goes into `main`), within the 95 %
pause and the day limit. No new word for each series, and after a seat
handover; I will record it in an ADR. (2) Approve the task packet for
repo-truth - it is your public repository; the push goes on your word.
(3) The decision to move to rung 2, when the ladder proposes it: that will be
the first auto-merge. Question: do I launch the '10 tasks' programme on these
conditions? I recommend: yes. If yes, after M0-267 I prepare the task packet
and bring it in one message."

### (c) The message his word follows - 17:01:14

His word does not follow (b) directly. The window lister over T1 from
13:40:00Z to 14:17:00Z printed the row of (b), then a harness idle notice
(not a human row), two assistant rows, then his row of (d). The second of
the two assistant rows is at 14:01:14.970Z; its last paragraph, whole:

```text
Действий не нужно. Жду отчёт блока; таймер его STATUS стоит на 17:46:11. От тебя жду ответа на вопрос о программе «10 задач».
```

"No action is needed. I am waiting for the block's report; the timer for its
STATUS is set for 17:46:11. From you I am waiting for an answer to the
question about the '10 tasks' programme." It points at (b)'s question and
adds nothing to it.

### (d) His word - 17:16:03, typed in the earlier foreman seat's session

His user row in T1 at 14:16:03.702Z, as the row printer prints it:

```text
Да
```

"Yes." Its fields: `"origin":{"kind":"human"}`, `"promptSource":"queued"`
and `"entrypoint":"cli"`.

### (e) The packet's question - 18:47:18

The seat's row in T1 at 15:47:18.114Z (assistant). What the packet holds -
its tasks, reissues and probes - is the packet's own home,
`<control-root>/briefs/packet-rt-ten-2026-09-30.md`, pointed at.
Its list of what follows the answer, whole:

```text
**Как пойдёт после «да»:**
1. **Сейчас.** Ставлю пробы на место, коммичу 9 спек в repo-truth и **пушу** — это внешний шаг. Затем отменяю 5 заблокированных строк, делаю `enqueue` и записываю baseline, когда у блока не будут идти тесты. Всё это отрепетировано на копии.
2. **После приёмки M0-267.** Он ещё идёт, а тики используют сборку фабрики, которую блок сейчас пересобирает. Дальше 4 тика RT-09…RT-12 по твоему постоянному слову: около $1 каждый, около $4 всего.
3. **Когда задач станет 10**, лестница предложит ступень 2, то есть первое автослияние. Решение твоё.
```

"How it goes after 'yes': (1) Now. I put the probes in place, commit 9 specs
in repo-truth and push - that is an outward step. Then I cancel the 5
blocked rows, run `enqueue` and record the baseline when the block has no
tests running. All of this is rehearsed on a copy. (2) After M0-267's
acceptance. It is still running, and the ticks use the factory's build,
which the block is rebuilding now. Then 4 ticks, RT-09...RT-12, on your
standing word: about $1 each, about $4 in all. (3) When the tasks reach 10,
the ladder will propose rung 2, that is the first auto-merge. The decision is
yours."

Its risk bullet on condition 2, and its closing line, whole:

```text
- Условие 2 иногда требует повторного прохода, попытка при этом не списывается.
**Вопрос: запускаю пакет, включая пуш в repo-truth?** Рекомендую: да.
```

"Condition 2 sometimes asks for a repeated pass, and no attempt is charged
for it. Question: do I launch the packet, the push to repo-truth included? I
recommend: yes." The window lister over T1 from 15:30:00Z to 16:12:00Z
printed that row and then his row of (f), with no row between them.

### (f) His word - 19:11:02, typed in the earlier foreman seat's session

His user row in T1 at 16:11:02.568Z, as the row printer prints it:

```text
Да
```

"Yes." Its fields: `"origin":{"kind":"human"}`, `"promptSource":"queued"`
and `"entrypoint":"cli"`. What it ran is the seat's run journal's (archive
entry "OPERATOR WORD 2026-09-30 19:11:02 + THE TEN-TASK PACKET RUN, STEPS
1-3"), pointed at.

### (g) The denial - 21:21:14 to 21:31:00, in the next foreman seat's session

The earlier foreman seat handed over to the next. In T2, the seat's row at
18:21:14.562Z (assistant) is a Bash tool call whose command runs a start
guard (it counts live ticks, baselines, vitest runs and `mw-*` units) and,
when all four are zero, the tick line
`<control-root>/bin/mw-live --detach tick --trigger operator --max-tasks 1 --max-usd 9.00 --run-id M5-03-$(date -u +%Y%m%dT%H%M%SZ)`.
The user row at 18:21:42.806Z is its `tool_result` for the same call, with
`"is_error":true`; its opening sentences, whole:

```text
Permission for this action was denied by the Claude Code auto mode classifier. Reason: [Modify Shared Resources].
```

Nothing ran: `ls <control-root>/logs/ | grep -c '20260930T18[2-5]'`
printed 0 on 2026-09-30 at 22:26, the newest log there is
mw-live-20260930T180426Z.log (the tick before the handover), and the last
line of `repo-truth`'s factory/state/events.jsonl is seq 1417 of run
M5-03-20260930T180426Z. The seat's row at 18:31:00.250Z (assistant)
followed; its sentence on the reason as the seat reads it, and its question
line with the list the line opens, whole:

```text
Но классификатор учитывает только то, что набрано в этой сессии.
**Вопрос: запускаю тики по программе «10 задач» здесь, в кресле [нового формана]?** Рекомендую: да. Нужна одна фраза, набранная прямо здесь, например «Да, тикай по программе». Строка с `!` из приложения придёт просто текстом и не выполнится. Условия прежние:
- по одному тику, каждый принимаю до следующего;
- ступень 1 (shadow), в `main` ничего не уходит;
- стоп на Weekly 95 % (сейчас 7 %).
```

"But the classifier counts only what is typed in this session. Question: do
I launch the ticks under the '10 tasks' programme here, in [the new
foreman's] seat? I recommend: yes. One sentence typed right here is needed,
for example 'Yes, tick under the programme'. A line with `!` sent from the app arrives as plain
text and does not run. The conditions as before: one tick at a time, each
accepted before the next; rung 1 (shadow), nothing goes into `main`; stop at
Weekly 95 % (7 % now)." The filter printed no line over T2 at 22:22: no
answer had arrived then.

### (h) His word in the successor seat - 23:36:07, typed in the next foreman seat's session

The seat's row in T2 at 20:18:27.431Z (assistant) is the message his word
follows: the window lister over T2 from 20:00:00Z to 20:37:00Z printed that
row and then his row, with no row between them. Its question line, whole:

```text
**Вопрос к тебе прежний: запускаю тики по программе «10 задач» здесь, в кресле [нового формана]?** Рекомендую: да. Достаточно одной фразы в этой сессии.
```

"My question to you stands: do I launch the ticks under the '10 tasks'
programme here, in [the new foreman's] seat? I recommend: yes. One sentence
in this session is enough." His user row in T2 at 20:36:07.020Z, as the row
printer prints it:

```text
Да
```

"Yes." Its fields: `"origin":{"kind":"human"}`, `"promptSource":"queued"`
and `"entrypoint":"cli"`. It was typed in the next foreman seat's session.
What the ticks under it did is the seat's run journal's, not this record's.

## 1. The decision

1. **THE «10 задач» ("10 tasks") PROGRAMME ON `repo-truth`, ON THE
   CONDITIONS OF THE QUESTION.** «Да» ("Yes") of (d), to (b)'s «запускаю
   программу «10 задач» на этих условиях?» ("do I launch the '10 tasks'
   programme on these conditions?"), as (c) points at it. What the
   conditions and the course are is reading 1 below.
2. **A STANDING WORD FOR TICKS on `repo-truth` at ladder rung 1 (shadow),
   within the 95 % pause and the day limit, with no new word for each series
   and after a seat handover** - the first item of (b)'s section 5, as he
   took it with the same «Да». "The day limit" is reading 2; the series form
   reading 3; the handover clause reading 5.
3. **THE PACKET IS HIS TO APPROVE** - the second item; and he approved the
   ten-task packet, its push to his public repository included, by «Да» of
   (f) to (e)'s question.
4. **RUNG 2 IS HIS DECISION** - the third item, restated in (e)'s list.

**THE FACT THE RECORD CARRIES.** The first tick the successor seat ran under
the word of item 2 was refused by the harness before it ran (g). The record
states that fact from the rows and decides nothing about the harness. The
reason the seat gives in (g) is the seat's reading; what a seat does about it
is the seat's rule (a rule in the seat's own memory).

**THE CORRECTION the record carries** (ADR 0039's form): (e)'s risk bullet
says a repeated pass on condition 2 is not charged an attempt. Programme tick
1 charged one: from `repo-truth`'s checkout,
`grep -E '"seq":1362,' factory/state/events.jsonl | grep -o 'fix cycle 1 of 2: the gate refused [0-9a-f]* with [0-9]* confirmed finding(s)'`
printed `fix cycle 1 of 2: the gate refused d3246b9cd3e2d83640c833388d4a92740161a287 with 1 confirmed finding(s)`
on 2026-09-30 at 22:23, on RT-09's candidate, whose one non-passing gate
condition was condition 2's `error`. The row that owns the charge is named in
the commit message, not here (ADR 0020 section 3).

Six readings follow. Each is **THE SEAT'S**, and each is
**[operator-confirmable]**:

1. **«Да» of (d) takes (b) whole** - the three items of its section 5 and the
   course of its section 4: after M0-267 the seat takes no millwright row by
   priority, and takes a millwright row only when a tick exposes a gate
   defect. ADR 0039's reading 1 is the precedent for taking a recommendation
   whole; the question asks about «этих условиях» ("these conditions"), and
   the course sits in the same answer.
2. **"The day limit" of item 1 is the day rule the seat's own memory
   holds.** That memory records it as the operator's rule of 2026-09-06,
   «30 % недельного лимита в сутки, так как иногда дни просто выпадают»
   ("30 % of the weekly limit a day, since some days simply drop out"),
   while ADR 0040 section 3 calls the day rule "the seat's rule, not his
   word". This record names the memory and settles neither
   characterization.
3. **A tick series runs one tick at a time, each accepted by the seat before
   the next** - the form (g)'s list states («по одному тику, каждый принимаю
   до следующего», "one tick at a time, I accept each before the next") and
   (b)'s section 4 implies («Тики — по одной задаче.», "Ticks - one task
   each.");
   each tick runs by the tick line of the seat's run dashboard (its section
   6, item 14).
4. **"A gate defect" includes a defect of the fix cycle a gate refusal
   opens.** The charge of the correction above is the first the programme
   exposed.
5. **«после передачи кресла» ("after a seat handover") is his word and
   stands as his.** That it does not pass the harness is (g)'s fact; whether
   a later seat asks him again is the seat's rule, not decided here.
6. **«Да» of (h) runs the programme's ticks in the successor seat, on a word
   typed there**, as the seat's message of 18:31:00 in (g) asked; this word,
   which answered a question about «здесь, в кресле [нового формана]» ("here,
   in [the new foreman's] seat"), does not outlive that seat. The general
   question of reading 5 stays the seat's rule.

## 2. What this ADR does NOT decide

- **Any priority or row.** Those are the rows' footers, each
  **[operator-confirmable]**.
- **The move to rung 2 and its timing.** His.
- **The packet's content and the tasks' specs.** The packet file and
  `repo-truth`'s factory/tasks/ are their homes.
- **The harness** and its classifier.
- **The pause**, which ADR 0040 records.
- **The words ADR 0041 records.**
- **That any tick, task, condition or the ladder passes.**
- **The showcase repository.**

## 3. What is filed elsewhere

The rows this package minted or raised are named in its commit messages and
are not listed here, for ADR 0020 section 3's reason: a decision document that
carries a backlog acquires two homes for every row in it.
