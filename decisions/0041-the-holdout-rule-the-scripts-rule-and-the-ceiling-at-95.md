# ADR 0041 - The operator's three morning words of 2026-09-30: the holdout rule on repo-truth, M0-69's scripts rule, and repo-truth's weekly ceiling at 95

Date: 2026-09-30. Context: a carrier session (carrier #85, package item K6)
by foreman decision under the standing delegation of 2026-08-25, opened off
cadence by exception - not a block - to carry into their record the operator's
words that have waited for one since he typed them. Merge blocks since carrier
#84's last commit:
`git log --oneline --first-parent f420448..origin/main | grep -c ' merge:'`
printed 2 on 2026-09-30 at 22:51. `main` stood at `a2c6ee4` when
this record was committed - `git rev-parse HEAD origin/main | cut -c1-7 | paste -sd' '`
printed `a2c6ee4 a2c6ee4` on 2026-09-30 at 22:51.
Nothing under `src/`, `test/`, `scripts/`, `.githooks/`, `.claude/`,
`factory/checks.yaml`, `factory/millwright.toml`, `CLAUDE.md`, `PRINCIPLES.md`,
`DESIGN.md` or the private archive was touched by this package, and nothing was
written in `repo-truth`.

This is a new record and not an amendment. ADR 0040 section 2 recorded the
holdout question as his and open, and its section 3 left `repo-truth`'s weekly
ceiling to his hand; this record adds his answers. ADR 0040 is not edited.

**This document records operator words and what they decide. It carries no
mechanism and moves no priority: the rows that carry anything out are the
homes of their own content and are named in the commit messages.**

## 0. The words, and the messages they answer

Quoted verbatim on ADR 0005's precedent, Russian as typed and with the typing
kept as it is (in (g), «85 %» with a space and «95%» without). Two transcripts
hold them, both of closed foreman sessions:
T1 = `<transcript-1>` (the earlier foreman seat's) and
T2 = `<transcript-2>` (the next foreman seat's). They were read only through
read-only tools, on 2026-09-30 between 22:22 and 22:26.

The filter ADR 0032 section 0 gives (its `node -e` line is quoted whole in
ADR 0036 section 0) printed one line over T1, at 06:30:46.289Z, and seven
over T2, at 07:15:50.271Z, 07:28:48.506Z, 07:39:23.935Z, 08:03:59.487Z,
09:19:16.157Z, 09:20:49.158Z and 09:22:56.375Z. The words recorded here are
the T1 line and the T2 lines at 07:15:50, 07:39:23 and 08:03:59; the other
four - «Да, делай» ("Yes, do it") at 07:28:48 (the RT-07 holdout packet's
run, an outward act already done) and his report at 09:19 to 09:22 that he
had reset the limits, with «Круто, продолжай» ("Great, carry on") - are not
part of this record. Each filter line
carries the same words as the user row named below, whose own timestamp is
35 to 98 milliseconds later; the row's timestamp is the one given here.

A window lister over a transcript prints the uuid, type, timestamp and first
characters of each user or assistant row in a time window that carries text;
the one used here is the one ADR 0040 section 0 describes. Each row below is
printed by its uuid with the read-only row printer ADR 0037 section 0 quotes
whole, and each user row's fields by
`grep -F '"uuid":"<uuid>"' <transcript> | grep -o -E '"entrypoint":"[a-z]*"|"origin":\{[^}]*\}|"promptSource":"[a-z]*"'`.
Every quoted line below was found in its transcript by
`grep -c -F -e '<the line>' <transcript>`, which printed at least 1 for each
on 2026-09-30 at 22:26. Timestamps are UTC; the times below are those
timestamps plus three hours, local time. A quoted block holds whole
sentences; what a message says beyond them is not part of this record.

### (a) The holdout question - 05:12:57, the earlier foreman seat's readiness report

The seat's row in T1 at 02:12:57.147Z (assistant). Its question paragraph,
whole, as the row printer prints it:

```text
**Вопрос: должна ли каждая строка `not_done_if` в спеках repo-truth закрываться скрытой (holdout) проверкой?** Сейчас гейт эти строки не запускает, а спека без holdout-пункта проходит условие 1 как «pass». Так получился частично ложный первый GATE_PASSED. **Рекомендую: да.** Каждую строку должна покрывать либо holdout-проверка, либо названная детерминированная проверка. Условие 1 больше не ставит «pass» спеке, которая ничего не объявила. Цена в том, что спеки писать дольше. Зато закрывается единственный измеренный путь ложного пропуска.
```

"Question: must every `not_done_if` line in repo-truth's specs be closed by a
hidden (holdout) check? Today the gate does not run these lines, and a spec
without a holdout item passes condition 1 as 'pass'. That is how the partly
false first GATE_PASSED came about. I recommend: yes. Every line must be
covered either by a holdout check or by a named deterministic check.
Condition 1 no longer gives 'pass' to a spec that declared nothing. The price
is that specs take longer to write. In exchange, the one measured road to a
false pass is closed."

The report's opening paragraph, the one that opens «Подтверждено на
526baa7» ("Confirmed at 526baa7"), carries the gate's line and a count over
`repo-truth`'s verdicts; it is pointed at, and its figures are the gate's and the seat's journal's,
not re-taken here.

### (b) The message his word follows - 09:30:00

The seat's row in T1 at 06:30:00.128Z (assistant), the earlier seat's
closing message; its opening paragraph says the handover to the next seat
was delivered. Its last paragraph, whole:

```text
Ответь, пожалуйста, на вопрос из моего доклада в 05:1x, он остаётся твоим: закрывать ли каждую строку `not_done_if` в спеках repo-truth скрытой (holdout) проверкой. Я рекомендую «да».
```

"Please answer the question from my report at 05:1x; it stays yours: whether
to close every `not_done_if` line in repo-truth's specs with a hidden
(holdout) check. I recommend 'yes'." It repeats the question's first half
only: neither the named deterministic check nor the sentence on condition 1
is in it. The window lister over T1 from 06:25:00Z to 06:40:00Z printed
that row and then his row of (c), with no row between them.

### (c) His word - 09:30:46, typed in the earlier foreman seat's session

His user row in T1 at 06:30:46.324Z, as the row printer prints it:

```text
Да
```

"Yes." Its fields: `"origin":{"kind":"human"}`, `"promptSource":"queued"`
and `"entrypoint":"cli"`. It was typed in the earlier foreman seat's session,
after that seat's message saying the handover was delivered; the row says
nothing about where he sat.

### (d) The scripts question - 09:35:19, the next foreman seat's readiness report

The seat's row in T2 at 06:35:19.639Z (assistant). Its question paragraph,
whole:

```text
**Вопрос на подтверждение: строим M0-69 с таким правилом для package.json?** Гейт отказывает кандидату, который меняет поле `scripts`. Правку других полей, например `bin` у RT-07, он проверяет как обычно. **Рекомендую: да.** Выигрыш: кандидат не сможет подменить команды, которыми проверяют его самого. Цена: задачу, которой действительно нужен новый npm-скрипт, фабрика на repo-truth пока влить не сможет. Сначала нужен M0-101, а у него приоритет 4.
```

"Question for confirmation: do we build M0-69 with this rule for
package.json? The gate refuses a candidate that changes the `scripts` field.
A change to other fields, for example RT-07's `bin`, it checks as usual. I
recommend: yes. The gain: a candidate cannot substitute the commands that
check it. The price: a task that really needs a new npm script cannot be
merged by the factory on repo-truth for now. M0-101 is needed first, and its
priority is 4."

### (e) The message his word follows - 10:05:32

The seat's row in T2 at 07:05:32.382Z (assistant). Its last paragraph,
whole:

```text
**Вопрос к тебе прежний:** подтверждаешь правило `scripts` для M0-69? Гейт отклоняет правку поля `scripts`, а `bin` проверяет как обычно. Я рекомендую «да».
```

"My question to you stands: do you confirm the `scripts` rule for M0-69? The
gate refuses a change to the `scripts` field and checks `bin` as usual. I
recommend 'yes'." The same question was repeated 43 seconds earlier, in a
bullet of the seat's row at 07:04:49.509Z, whole:

```text
- Weekly 90 %. Вопрос прежний: подтверждаешь правило `scripts` для M0-69?
```

"Weekly 90 %. The question stands: do you confirm the `scripts` rule for
M0-69?" The Weekly figure is the seat's reading. The window lister over T2
from 06:26:00Z to 07:16:30Z printed the row of 07:05:32 and then his row of
(f), with no row between them.

### (f) His word - 10:15:50, typed in the next foreman seat's session

His user row in T2 at 07:15:50.335Z, as the row printer prints it:

```text
Да
```

"Yes." Its fields: `"origin":{"kind":"human"}`, `"promptSource":"queued"`
and `"entrypoint":"cli"`.

### (g) His proposal - 10:39:24, typed in the next foreman seat's session

His user row in T2 at 07:39:24.016Z, as the row printer prints it:

```text
Давай тогда сменим потолок repo-truth: с 85 % на 95% и всё равно запустим, так это сработает?
```

"Then let's change repo-truth's ceiling: from 85 % to 95%, and launch anyway -
will that work?" Its fields: `"origin":{"kind":"human"}`,
`"promptSource":"queued"` and `"entrypoint":"cli"`.

### (h) The seat's answer and question - 10:41:56

The seat's row in T2 at 07:41:56.472Z (assistant). Its bullet on the two
keys and its question paragraph, whole:

```text
- **Ключей два, а не один.** Потолок — это меньшее из двух чисел: «порог» и «100 − резерв». Сейчас это min(85, 100 − 10) = 85. Если поднять только порог до 95, потолок станет 90, то есть ровно наш текущий Weekly, и уже на 91 % тик снова откажет. Нужны оба ключа: порог 95 и резерв 5. Секции `[budget]` в TOML repo-truth пока нет, я её добавлю. Тик отказывает, когда Weekly строго выше потолка, и проверяет это в начале каждого прохода. Цена: доля недели, которую фабрика оставляет тебе, падает с 10 % до 5 %.
```

"There are two keys, not one. The ceiling is the lesser of two numbers: the
'threshold' and '100 - reserve'. Now it is min(85, 100 - 10) = 85. If only
the threshold is raised to 95, the ceiling becomes 90, which is exactly our
Weekly now, and at 91 % the tick refuses again. Both keys are needed:
threshold 95 and reserve 5. repo-truth's TOML has no `[budget]` section yet;
I will add it. The tick refuses when Weekly is strictly above the ceiling,
and checks it at the start of every pass. The price: the share of the week
the factory leaves you falls from 10 % to 5 %." The Weekly figure is the
seat's reading of that minute and is not re-taken here.

```text
**Вопрос: делаю так?** Сейчас меняю потолок (95 и 5) и перезаписываю baseline. Тики на RT-07 запускаю по одному сразу после приёмки M0-69 и каждый принимаю, пока гейт не вынесет вердикт. Остановлюсь раньше, если Weekly дойдёт до 95 %, сработает брейкер или откажет классификатор. **Рекомендую: да.**
```

"Question: do I do it this way? Now I change the ceiling (95 and 5) and
rewrite the baseline. The ticks on RT-07 I launch one at a time right after
M0-69's acceptance, and I accept each, until the gate gives a verdict. I stop
earlier if Weekly reaches 95 %, a breaker trips or the classifier refuses. I
recommend: yes."

### (i) The message his word follows - 10:53:36

His word does not follow (h) directly. The window lister over T2 from
07:28:00Z to 08:05:00Z printed the row of (h), then a message from another
session (not a human row), two assistant rows, then his row of (j). The
second of the two assistant rows, at 07:53:36.701Z, is the seat's relay of a
block's STATUS; its last paragraph, whole:

```text
Мой вопрос про потолок repo-truth по-прежнему ждёт ответа. Предлагаю поднять два ключа до 95 % и 5 %, а тики запускать после приёмки M0-69. Рекомендую: да.
```

"My question about repo-truth's ceiling still waits for an answer. I propose
raising the two keys to 95 % and 5 %, and launching the ticks after M0-69's
acceptance. I recommend: yes." The seat's run journal names only the row of
(h) as the question (archive entry "OPERATOR WORD 2026-09-30 11:03:59 + repo-truth's
CEILING AT 95"); this record names both.

### (j) His word - 11:03:59, typed in the next foreman seat's session

His user row in T2 at 08:03:59.585Z, as the row printer prints it:

```text
Да
```

"Yes." Its fields: `"origin":{"kind":"human"}`, `"promptSource":"queued"`
and `"entrypoint":"cli"`.

## 1. The decision

1. **THE HOLDOUT RULE ON `repo-truth`.** «Да» ("Yes") of (c), to the
   question and recommendation of (a): every `not_done_if` line of a spec on
   `repo-truth` is covered by a holdout check or by a named deterministic check, and
   condition 1 no longer gives «pass» to a spec that declared nothing. ADR
   0040 section 2's question is answered for `repo-truth`. That «Да» takes
   both halves of (a)'s recommendation is reading 1 below; what the rule
   means for the machine is readings 3 and 4.
2. **M0-69'S SCRIPTS RULE.** «Да» of (f), to (d) and (e): the gate refuses a
   candidate that changes the `scripts` field of `package.json`, and a change
   to any other field - RT-07's `bin` - is checked as before, at the price (d)
   names: a task that needs a new npm script cannot be merged by the factory
   on `repo-truth` until M0-101, priority 4. M0-69 carried it out and is DONE
   (its merge is 82f51a3); its footer's paragraph that opens "THE SCRIPTS
   RULE:" names this record as the next carrier's and restates none of it.
   A pointer.
3. **`repo-truth`'S WEEKLY CEILING AT 95, BY BOTH KEYS** (threshold 95,
   reserve 5). «Да» of (j), to (h) as (i) repeats it, and to his own proposal
   (g). Done in `repo-truth` as its commit 8a76f79 - from its checkout,
   `git show -s --format='%h %ad %s' --date=format:'%Y-%m-%d %H:%M:%S' 8a76f79`
   printed "8a76f79 2026-09-30 11:04:58 chore: the weekly ceiling to 95 on the
   operator's word" on 2026-09-30 at 22:24. A pointer.
4. **THE TICKS ON RT-07 AFTER M0-69'S ACCEPTANCE**, one at a time, each
   accepted, until the gate's verdict, stopping earlier at Weekly 95 %, a
   breaker or a classifier refusal - the same «Да» of (j). They did not run
   under it: the seat that heard it handed over before M0-69's acceptance,
   and the ticks on RT-07 ran on his later word of 16:27:18, typed in
   a later foreman seat's session (archive entries "OPERATOR WORD 2026-09-30 16:27:18 +
   TICK 1 LAUNCHED" and "TICK 1 ACCEPTED - RT-07 GATE_PASSED"). A pointer;
   that later word is not this record's.

Seven readings follow. Each is **THE SEAT'S**, and each is
**[operator-confirmable]**:

1. **«Да» of (c) takes (a)'s recommendation whole** - both the covering rule
   and the sentence on condition 1 - although (b), the message it follows,
   repeats the question's first half only. ADR 0039's reading 1 is the
   precedent: a «Да» to a recommendation takes it whole.
2. **«в спеках repo-truth» ("in repo-truth's specs") scopes the rule to that
   consumer.** It narrows ADR 0040 section 2's "a showcase consumer" to the one consumer it names,
   and no other consumer's specs are touched.
3. **«названная детерминированная проверка» ("a named deterministic check")
   is a command acceptance item of the spec, or a rung of the consumer's
   `checks.yaml`, that the spec names beside the line.** No TaskSpec field names which check covers which line
   (`DESIGN.md` section 5's fields table is his), so until one exists the
   naming is an authoring rule the seat keeps when it writes `repo-truth`'s
   specs.
4. **For the machine, condition 1's half reads: on `repo-truth`, condition 1
   does not pass a spec that declares no holdout item.** This is NARROWER
   than the word, which also accepts a named deterministic check, because no
   field lets the machine see a named check (reading 3). A row this package
   mints carries it out; what condition 1 answers is that row's, bounded so
   that the spec's omission is never charged as the candidate's.
5. **THE `DESIGN.md` AMENDMENT IS NOT READ INTO THE WORD.** The seat's run
   journal (archive entry "OPERATOR WORD 2026-09-30 09:30:46") reads his «Да»
   as the authority for an amendment of `DESIGN.md` section 5, and the next
   foreman seat told him twice that the next carrier would write one - in
   (d)'s row, the sentence «Запишет следующий carrier: ADR, строки и поправка
   DESIGN §5.» ("The next carrier will record it: an ADR, rows and an
   amendment of DESIGN section 5."),
   and in (e)'s row, «Записывает его следующий carrier: ADR, строки и
   поправка DESIGN §5.» ("The next carrier records it: an ADR, rows and an
   amendment of DESIGN section 5.") - and his next word, «Да» of (f),
   answered the scripts question those messages asked, not that sentence.
   That reading is the seat's. The question of (a) named no `DESIGN.md`
   sentence and offered no wording. The carriers' `DESIGN.md` edits since
   ratification are the five lines
   `git log --oneline --since=2026-08-19 a2c6ee4 -- DESIGN.md | grep -v -E ' (feat|fix|test|docs): M[0-9]'`
   printed on 2026-09-30 at 23:47 - 3d05265, 340add2, eb0390a, 2edb743 and
   39ff2eb; the filter drops the blocks' commits, whose subjects open with a
   task id. Three of the five answered a word that asked for the edit:
   340add2 (ADR 0025 section 0), 3d05265 (his word of 2026-09-14 to a packet
   that was the edit) and 39ff2eb (its body: "Operator sanction 2026-08-25,
   relayed through [a foreman seat]"). 2edb743 rested on the delegation ADR 0021
   section 4 (ii) records, and eb0390a's authority is its own commit's
   record, not read here. Under reading 2 both
   `DESIGN.md` sentences stay true - section 5's fields table makes
   `holdout` optional, and a consumer's own rule asks for one - so this
   record amends nothing, and whether the design text names a consumer's
   rule is his question, open.
6. **«Да» of (f) confirms the rule (d) states in its two sentences** - the
   `scripts` field refused, every other field checked as before. How M0-69
   built it is that row's, and the word does not confirm it.
7. **«Да» of (j) takes (h) whole** - the ceiling and the tick half. The tick
   half bound the seat that heard it; that it does not carry across a
   handover is the seat's journal rule and is not decided here.

## 2. What this ADR does NOT decide

- **Any priority or row.** Those are the rows' footers, each
  **[operator-confirmable]**.
- **The coverage rule's machine form and any TaskSpec field.** His -
  `DESIGN.md` section 5.
- **`DESIGN.md`**, untouched (reading 5).
- **M0-101's priority.**
- **The ticks** - his separate words: the word of 16:27:18, and the standing
  word ADR 0042 records.
- **The pause**, which ADR 0040 records.
- **The seat's day rule** (a rule in the seat's own memory).
- **RT-08's spec**, which declares no holdout item - from `repo-truth`'s
  checkout, `/usr/bin/grep -L -E '^[[:space:]]*holdout:[[:space:]]*true' factory/tasks/RT-*.yaml`
  printed factory/tasks/RT-01.yaml and factory/tasks/RT-08.yaml on
  2026-09-30 at 22:23; RT-01 is DONE by hand and RT-08's reissue is his hand.
- **That any tick, task, condition or the gate passes after any row lands.**

## 3. What is filed elsewhere

The rows this package minted or raised are named in its commit messages and
are not listed here, for ADR 0020 section 3's reason: a decision document that
carries a backlog acquires two homes for every row in it.
