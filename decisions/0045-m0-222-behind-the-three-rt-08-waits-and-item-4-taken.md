# ADR 0045 - The operator's words of 2026-10-03 14:35:04, 14:45:49 and 19:26:20: M0-222 right behind the three rows above the line, the reviewer stays, RT-08 waits, item 4 taken and the plan taken

Date: 2026-10-03. Context: a carrier session (carrier #90, package item K4)
by foreman decision under the standing delegation of 2026-08-25, BY EXCEPTION
and not at cadence, on his words (1) and (3) below. Merge blocks since carrier
#89's last commit:
`git log --oneline --first-parent 015aba0..origin/main | grep -c ' merge:'`
printed 0 on 2026-10-03 at 20:44. `main` stood at `015aba0 015aba0` when
this record was committed - `git rev-parse HEAD origin/main | cut -c1-7 | paste -sd' '`
printed `015aba0 015aba0` on 2026-10-03 at 20:44.
By word (3) this package touches `DESIGN.md`, two files under `.claude/`
(`.claude/commands/block.md` and `.claude/agents/operator-brief.md`) and one
test file (`test/unit/design-ratification.test.ts`, the digests of `DESIGN.md`
sections 7, 8 and 13 and their comments); under `docs/` it writes this record
and four dated corrections into ADR 0044, which are named in section 3 and not
repeated here; the rest of it is `factory/tasks/`. Nothing under `src/`,
`scripts/`, `.githooks/`, `factory/policy/`, `factory/checks.yaml`,
`factory/millwright.toml`, `CLAUDE.md`, `PRINCIPLES.md` or the private archive
was touched by this package. Nothing was written in `repo-truth` or in the
showcase repository.

This is a new record and not an amendment: no earlier record holds these
words. ADR 0027 section 10 names M0-222 as step (4) of the programme it
reads as M5's order of work; this record adds the word that puts that row
right behind the three rows above the line. ADR 0027 is not edited.

**This document records operator words and what they decide. It carries no
mechanism and moves no priority: the rows that carry anything out are the
homes of their own content and are named in the commit messages.**

## 0. The words, and the messages they answer

Quoted verbatim on ADR 0005's precedent, Russian as typed (in (c), his first
line with the space before its comma as typed). Two transcripts hold them,
each the session of the foreman seat that heard the word:
T1 = `<transcript-1>` (the earlier foreman seat's, closed), and
T2 = `<transcript-2>` (the next foreman seat's, its live session then, which
grows while it is read). They were read only
through the read-only tools named below, on 2026-10-03 between 20:15 and
20:18; `stat -c '%s %y'` printed
`4679396 2026-10-03 17:39:00.841631262 +0300` for T1 and
`2223398 2026-10-03 20:14:26.407792948 +0300` for T2 at 20:15.

The tools, each read-only and each over one transcript. The exact filter
ADR 0043 section 0 quotes whole, which reads `origin.kind === "human"` at a
row's top or inside its `attachment`, lists the human rows. A window lister
of the form ADR 0040 section 0 describes prints the uuid, type, timestamp and
first characters of each user or assistant row in a time window that carries
text, here with each assistant row's stop reason beside it. The row printer
ADR 0037 section 0 quotes whole prints one row by its uuid. A user row's
fields are printed by the field grep ADR 0043 section 0 quotes for a user
row. Every quoted line below was found in its transcript by
`grep -c -F -e '<the line>' <transcript>`, which printed at least 1 for each
on 2026-10-03 at 20:19. Timestamps are UTC; the times below are those
timestamps plus three hours, local time. A quoted block holds whole
lines; what a message says beyond them is not part of this record.

The exact filter printed eight human rows over T1 and two over T2 at 20:15.
Three of them are the words below. None of the others is part of this record -
each is a request, a question, a git line of his own or an act for one
occasion, the reason ADR 0044 section 0 gives for the rows it leaves out: in
T1, his rows at 11:20:14Z (his request to check an audit),
at 11:27:49Z (a `queued_command` attachment, his request to walk through the
audit's six items one step at a time - the walk words (1) and (2) are items
of), at 11:30:43Z (his `!` lines), at 14:22:44Z (a question), at 14:30:04Z
(acts for that hour) and at 14:32:42Z (his `!` lines); and in T2, his row at
16:21:16Z (his request, quoted in (c) as the context of word (3), which
decides nothing).

### (a) Word (1) - 14:35:04, item 2 of his walk

The window lister over T1 from 11:27:00Z to 11:36:00Z printed, after his `!`
lines of 11:30:43Z and the seat's row that ran them, the seat's row at
11:32:52.916Z (assistant, stop reason
`end_turn`), then his word - so that row is both the question his word answers
and the last seat text before it. The row printer prints its text as 24
lines: the facts for item 2, the models as they stand, a numbered
recommendation, the question, and one closing line on another item. The
recommendation, whole:

```text
**Моя рекомендация, по порядку:**
1. **Ревьюера пока не трогать.** Все 11 мержей прошли с ревьюером `claude-sonnet-5`. Если сменить его сейчас, сравнение «Sonnet против Opus в роли строителя» смешается со сменой ревьюера, и мы не поймём, что дало разницу. Его очередь — после замера.
2. **Сначала построить M0-222, метрику по модели и роли.** В ADR она названа «дешёвым шагом сейчас», но так и не построена. Без неё смена модели будет «ощущаться, а не измеряться», это слова самой строки. Поднять её надо сразу за тремя строками над чертой (M0-281, M0-283, M0-117). Поднимет следующий carrier.
3. **Потом шаг 2, как он записан: те же десять задач.** Они уже слиты в repo-truth, поэтому прогоняются на локальной копии repo-truth от базы до мержей (`9eb3692`) с локальным origin, без GitHub, со строителем `claude-opus-5-5` в её TOML.
   - **Оценка цены:** около $35 по цене CLI. Расчёт: десять задач на Sonnet стоили около $17,9, а сравнение моделей 23.09 дало Opus примерно вдвое дороже ($1,19 против $0,60). Это оценка, а не замер.
   - **Это трата,** поэтому на неё нужно твоё отдельное слово, когда M0-222 сольётся. Подготовку копии и TOML я принесу пакетом.
```

"My recommendation, in order: (1) Do not touch the reviewer for now. All 11
merges passed with the reviewer `claude-sonnet-5`. If it is changed now, the
comparison 'Sonnet against Opus in the builder's role' gets mixed with the
change of reviewer, and we will not understand what made the difference. Its
turn is after the measurement. (2) First build M0-222, the metric by model and
role. In the ADR it is called 'a cheap step now', but it was never built.
Without it a change of model will be 'felt rather than measured' - the row's
own words. It should be raised right behind the three rows above the line
(M0-281, M0-283, M0-117). The next carrier will raise it. (3) Then step 2, as
it is written: the same ten tasks. They are already merged in repo-truth, so
they are run on a local copy of repo-truth from the base to the merges
(`9eb3692`) with a local origin, without GitHub, with the builder
`claude-opus-5-5` in its TOML. - Estimate of the price: about $35 at the CLI
price. Calculation: ten tasks on Sonnet cost about $17.9, and the model
comparison of 23.09 put Opus at about twice the price ($1.19 against $0.60).
This is an estimate, not a measurement. - This is a spend, so it needs your
separate word when M0-222 merges. I will bring the preparation of the copy and
the TOML as a packet."

Its question line, whole:

```text
**Вопрос: поднимаем M0-222 (метрика по моделям) сразу за тремя строками над чертой, а ревьюера оставляем до замера?** Рекомендую: да.
```

"Question: do we raise M0-222 (the metric by models) right behind the three
rows above the line, and leave the reviewer until the measurement? I
recommend: yes."

His user row in T1 at 11:35:04.265Z, as the row printer prints it:

```text
Пункт 2: да
```

"Item 2: yes." Its fields: `"origin":{"kind":"human"}`,
`"promptSource":"queued"` and `"entrypoint":"cli"`.

The seat's reply after it, the seat's row at 11:36:46.330Z (assistant), opens
with this line, whole:

```text
Твоё слово записано: пункт 33 в разделе 6 дашборда (в нём теперь 299 строк из 300 допустимых), отметка в цепочке вопросов, полная запись в журнале со строками вопроса и ответа. M0-222 поднимет carrier #90 вне каденции, сразу после приёмки #89 и до блока M0-281.
```

"Your word is recorded: item 33 in section 6 of the dashboard (it now holds
299 lines of the 300 allowed), a mark in the chain of questions, a full entry
in the journal with the lines of the question and the answer. M0-222 will be
raised by carrier #90 outside the cadence, right after #89's acceptance and
before the M0-281 block."

### (b) Word (2) - 14:45:49, item 3 of his walk

The same row of 11:36:46Z (stop reason `end_turn`) puts the next question. Its
recommendation's head line, whole:

```text
**Моя рекомендация: отложить RT-08 до конца четырёх строк фабрики** (M0-281, M0-283, M0-117, M0-222):
```

"My recommendation: defer RT-08 until the end of the factory's four rows
(M0-281, M0-283, M0-117, M0-222):". Its last bullet and its question line, the
row's two last lines that carry text, whole:

```text
- **Что будет потом.** Когда последняя из четырёх будет на подходе, кресло подготовит пакет перевыпуска RT-08 и принесёт тебе одним вопросом. До тех пор на repo-truth стоит STOP.

**Вопрос: откладываем RT-08 до этих четырёх строк?** Рекомендую: да.
```

"What comes after. When the last of the four is on its way, the seat will
prepare RT-08's reissue packet and bring it to you as one question. Until then
STOP stands on repo-truth. / Question: do we defer RT-08 until these four
rows? I recommend: yes."

The window lister over T1 from 11:35:05Z to 11:46:00Z printed two more seat
texts between that row and his word: the seat's row at 11:41:25.239Z
(assistant, stop reason `tool_use`), a working note about the post's variant
B, and the seat's row at 11:42:26.951Z (assistant, stop reason `end_turn`),
which hands him the final variant of a post. The second is the LAST seat text before
his word, and its last line, whole, restates the pending question:

```text
По пункту 3 (RT-08) жду твоего ответа: я рекомендую отложить её до четырёх строк фабрики.
```

"On item 3 (RT-08) I am waiting for your answer: I recommend deferring it
until the factory's four rows."

His user row in T1 at 11:45:49.311Z, as the row printer prints it:

```text
откладываем RT-08 - да
```

"We defer RT-08 - yes." Its fields: `"origin":{"kind":"human"}`,
`"promptSource":"queued"` and `"entrypoint":"cli"`.

### (c) Word (3) - 19:26:20

The question was first put in T2, in the seat's row at 14:42:12.810Z
(assistant, stop reason `end_turn`), the seat's readiness report. The block under its bold heading, whole - the
decision brief's section 1 question as the seat pasted it into the row,
which differs from the brief's file in its dashes and one bold span:

```text
**Вопрос (пункт 4 записки решений):**

> Пункт 4 одним словом: carrier по исключению (лучше внутри #90) вносит ровно эти правки, тексты — как в файле брифа: `.claude/commands/block.md` — четыре места (E1 «leaves no trace», E2 фраза про M0-60, E4 мутанты по каждой клаузе, E5 юниты верификатора); `.claude/agents/operator-brief.md` — три (E6 не запускать `doctor`, пока в чекауте кто-то работает, и поправка «all read-only»; E11 отчёт о гейте — числом совпадений, не выводом); `DESIGN.md` — четыре (E7 выключатель транскрипта пунктом списка, по умолчанию выключен; E8 janitor без `git worktree prune`; E9 «kept for forensics» — пока строка стоит или до срока janitor; E10 focused-тесты из TaskSpec) — с новыми дайджестами §7, §8, §13 в `test/unit/design-ratification.test.ts` после перечитывания парных разделов blueprint и с твоим словом в ADR. Правило `fix:` прозой не пишем (дорога — гейт M0-134), фразу про exit 2 (:396) не трогаем до живого замера M0-215. Делаем? **Рекомендую: да.**
```

"Question (item 4 of the decision brief): > Item 4 in one word: a carrier by
exception (better inside #90) makes exactly these edits, the texts as in the
brief's file: `.claude/commands/block.md` - four places (E1 'leaves no trace',
E2 the sentence about M0-60, E4 mutants per clause, E5 the verifier's units);
`.claude/agents/operator-brief.md` - three (E6 do not run `doctor` while
someone works in the checkout, and the correction 'all read-only'; E11 the
gate's report as a number of matches, not as output); `DESIGN.md` - four (E7
the transcript switch as a list item, off by default; E8 the janitor without
`git worktree prune`; E9 'kept for forensics' - while the row stands or until
the janitor's term; E10 focused tests from the TaskSpec) - with new digests of
sections 7, 8 and 13 in `test/unit/design-ratification.test.ts` after
re-reading the paired sections of the blueprint, and with your word in an
ADR. The `fix:` rule is not written in prose (its road is the gate of M0-134);
the sentence about exit 2 (:396) is not touched until the live measurement of
M0-215. Do we do it? I recommend: yes."

His request, his user row in T2 at 16:21:16.478Z, as the row printer prints
it:

```text
Какой-то сложный вопрос , можешь проще его задать?
И в конце прошлой сессии, план следующих шагов тоже был?
```

"Some complicated question , can you ask it more simply? / And at the end of
the last session, was there a plan of the next steps too?"

The seat re-asked in its row at 16:22:12.912Z (assistant, stop reason
`end_turn`), which the window lister over T2 from
16:21:17Z to 16:26:20Z prints as the only seat text between his request and
his word - so it is both the question his word answers and the last seat text
before it. Its text from its bold question line to its end, whole:

```text
**Вопрос:** в трёх файлах-инструкциях накопилось 11 устаревших мест. Это `block.md` (правила блока), `operator-brief.md` (как готовится твой бриф) и `DESIGN.md`. В одних местах текст разошёлся с кодом. Например, `DESIGN.md` пишет, что уборщик чистит старые рабочие копии командой `git worktree prune`, а код этого намеренно не делает. В других не хватает двух правил для проверяющего, и я каждый раз вписываю их в задание вручную. Без твоего слова фабрика эти файлы не трогает.

Предлагаю поправить их в ближайшем пакете carrier #90, который ты уже разрешил для подъёма M0-222. Меняется только текст, код фабрики в `src/` не трогаем, тиков и блоков нет. Две спорные правки (правило про `fix:` и фразу про exit 2) оставляем на потом, у них своя дорога.

**Исправляем? Рекомендую: да.**

**План был.** [Предыдущий форман] закончил последнее сообщение пятью шагами, то же написано в письме передачи. Состояние я перемерил, ничего не изменилось, план в силе:

1. **Carrier #90.** Поднимает M0-222 по твоему «Пункт 2: да», а если скажешь «да» на вопрос выше, то вносит и эти правки. Запускаю сразу после твоего ответа.
2. **Блоки по очереди:** M0-281 → M0-283 → M0-117 → M0-222. Твоего слова не нужно, я открываю их по одному.
3. **Пункты 5.1–5.10 записки.** Буду задавать по одному вопросу, каждый с рекомендацией.
4. **Шаг 2 сравнения моделей:** те же десять задач на Opus. Это после M0-222, и на эту трату нужно твоё отдельное слово.
5. **Перевыпуск RT-08 и снятие STOP.** Сделаешь своими `!`-строками, когда четыре блока из шага 2 будут почти готовы.
```

"Question: in three instruction files 11 out-of-date places have accumulated.
These are `block.md` (the block's rules), `operator-brief.md` (how your brief
is prepared) and `DESIGN.md`. In some places the text has drifted from the
code. For example, `DESIGN.md` writes that the janitor cleans old working
copies with the command `git worktree prune`, while the code deliberately does
not do that. In others two rules for the verifier are missing, and I write them
into the assignment by hand every time. Without your word the factory does not
touch these files. / I propose to fix them in the nearest package, carrier #90,
which you have already allowed for M0-222's raise. Only text changes; the
factory's code in `src/` is not touched; there are no ticks and no blocks. Two
disputed edits (the rule about `fix:` and the sentence about exit 2) are left
for later; they have their own road. / Shall we fix? I recommend: yes. / There
was a plan. [The previous foreman] ended its last message with five steps; the same is
written in the handover letter. I re-measured the state, nothing has changed,
the plan stands: (1) Carrier #90. It raises M0-222 on your 'Item 2: yes', and
if you say 'yes' to the question above, it also makes these edits. I launch it
right after your answer. (2) The blocks one at a time: M0-281 -> M0-283 ->
M0-117 -> M0-222. Your word is not needed; I open them one by one. (3) Items
5.1-5.10 of the brief. I will ask one question at a time, each with a
recommendation. (4) Step 2 of the model comparison: the same ten tasks on
Opus. This is after M0-222, and this spend needs your separate word. (5) The
reissue of RT-08 and the removal of STOP. You will do it with your `!` lines
when the four blocks of step 2 are nearly ready."

His user row in T2 at 16:26:20.560Z, as the row printer prints it:

```text
Да, идем по твоим рекомендациям, и потом по плану
```

"Yes, we go by your recommendations, and then by the plan." Its fields:
`"origin":{"kind":"human"}`, `"promptSource":"queued"` and
`"entrypoint":"cli"`.

### (d) The facts beside word (1)

From `repo-truth`'s checkout on 2026-10-03 at 20:17,
`grep -n -E '^\[models\.' factory/millwright.toml` printed four sections -
`[models.builder_hard]`, `[models.adjudicator]`, `[models.scout]` and
`[models.builder_default]` - and no `[models.reviewer]`; so the reviewer is
the controller's default,
`git grep -n -F 'reviewer: { id: "claude-sonnet-5"' 015aba0 -- src/controller/config.ts`
printing `reviewer: { id: "claude-sonnet-5", effort: "medium", max_turns: 35, max_usd: 1.5 },`
at 20:14. ADR 0027 section 10 names M0-222 as its step (4):
`grep -c -F '**M0-222**. Steps (2) and (3)' docs/decisions/0027-the-m5-chain-and-the-run-on-the-second-repository.md`
printed 1 at 20:14.

## 1. The decision

1. **M0-222 RIGHT BEHIND THE THREE ROWS ABOVE THE LINE, AND THE REVIEWER
   STAYS.** Word (1), to the question of (a): M0-222, the metric by model and
   role, is raised right behind M0-281, M0-283 and M0-117; the reviewer is
   left as it is until the measurement. Four things beside it are THE SEAT'S,
   **[operator-confirmable]**: the figure the row carries, 97 with
   `outranks_roadmap` (his word names no figure, and the figure is the row's
   footer); the road - carrier #90 by exception, after carrier #89's
   acceptance and before the M0-281 block - which is the seat's reply after
   the word, quoted in (a), and is also the first step of the plan word (3)
   took; that "the measurement" is ADR 0027 section 10's step (2), so the
   reviewer stays `claude-sonnet-5` (the default of (d)) until that step is
   measured; and that step (2) runs after M0-222 lands, as the seat's packet,
   its spend on his separate word - the recommendation's item 3.
2. **RT-08 DEFERRED.** Word (2), to the question of (b): `RT-08` on
   `repo-truth` waits for the factory's four rows M0-281, M0-283, M0-117 and
   M0-222, and STOP stands on `repo-truth` until then
   (`<control-root>/repo-truth/STOP`); the seat brings RT-08's reissue
   packet to him as one question - the question row's last bullet. That
   "until the end of the four rows" means until they land is THE SEAT'S
   reading, **[operator-confirmable]**; the bullet itself has the packet
   prepared when the last of the four is on its way.
3. **ITEM 4 TAKEN, AND THE PLAN TAKEN.** Word (3), to the simplified question
   of (c). That "your recommendations" means item 4's one recommendation is
   THE SEAT'S reading, **[operator-confirmable]**: the simplified question
   closes on one recommendation, "Shall we fix? I recommend: yes.", and the
   plan the row gives after that line asks nothing. Read so,
   it takes E1, E2 and E4 to E11 of the decision brief's section 1 into this
   package, leaves E3 out (the `fix:` rule, whose road is M0-134's gate) and
   E12 for later (the exit-2 sentence, until M0-215's live reading); and E7
   puts the transcript switch into `DESIGN.md` section 7 as a list item with
   its default OFF - what ADR 0032 section 2 left to him. "Then by the plan" is
   read as the five steps of (c) - THE SEAT'S reading,
   **[operator-confirmable]**: carrier #90; the blocks M0-281 -> M0-283 ->
   M0-117 -> M0-222; items 5.1 to 5.10, one question at a time; step (2) after
   M0-222 on his separate spend word; RT-08's reissue and the STOP's removal on
   his `!` lines. This word decides NONE of items 5.1 to 5.10: the plan it
   took says the seat asks them one by one.

## 2. What this ADR does NOT decide

- **Any priority figure or row.** Those are the rows' footers, each
  **[operator-confirmable]**.
- **Items 5.1 to 5.10** of the decision brief. Each is its own question.
- **The model step (2) and its spend.** His separate word.
- **The reviewer's model after step (2).** Not asked.
- **RT-08's reissue, its holdout and the STOP's removal.** His `!` lines.
- **The ticks.** None is sanctioned here.
- **`DESIGN.md` beyond E7 to E10**, and E12's sentence, which stays as it is.
- **The pause**, which ADR 0040 records.
- **His repositories** and the showcase.
- **The harness** and its classifier.
- **That any tick, task, condition, the gate or the ladder passes after any
  row lands.**

## 3. What is filed elsewhere

The rows this package raised or touched are named in its commit messages and
are not listed here, for ADR 0020 section 3's reason: a decision document that
carries a backlog acquires two homes for every row in it. The texts of E1, E2
and E4 to E11 live in the files they edit. The same package corrects ADR
0044's own account of the words it records, in place and dated, each
correction where its sentence lives: section 0 (a), section 0 (c), and items
3 and 5 of its section 1. Their content is in ADR 0044 and is not repeated
here.
