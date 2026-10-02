# ADR 0034 - The operator's words of the night of 2026-09-26/27: the fast mode, pipelined acceptance, the finish line and the night protocol

Date: 2026-09-27. Context: a carrier session (carrier #74) by foreman decision
under the standing delegation of 2026-08-25, not a block, and off the cadence
of one carrier per four blocks by the blocked-top-pick exception: the top pick
after M0-243 landed, M0-138, could not be built inside its paths, and the row
is raised in place by the same package. `main` stood at `0bc25c8` when the
package began - `git rev-parse HEAD origin/main | cut -c1-7 | paste -sd' '`
printed `0bc25c8 0bc25c8` on 2026-09-27 at 05:12 - and `git status --short | wc -l`
printed 2 the same minute, the two operator handoffs in a private archive
that is not published.
Nothing under `src/`, `test/`, `scripts/`, `.githooks/`, `factory/checks.yaml`,
`factory/millwright.toml`, `CLAUDE.md`, `PRINCIPLES.md`, `DESIGN.md` or
the private archive was touched by this package, and nothing was written in
`repo-truth`.

**This document records operator words and what they decide. It carries no
mechanism and moves no priority: each decision below has its home in a row, in
the seat's practice or in a later package, and the rows this package raised are
named in its commit messages.**

## 0. The operator's words, and the questions they answer

Quoted verbatim on ADR 0005's precedent, Russian as typed and with the typing
kept as it is. Every word below was typed in the foreman's session and
relayed operator -> that session's transcript -> this carrier. Each is copied from the transcript and not from the seat's
journal, by the filter ADR 0032 section 0 gives, run over this night's
transcript:
`node -e 'const fs=require("fs");for(const l of fs.readFileSync(process.argv[1],"utf8").split("\n")){if(!l)continue;let e;try{e=JSON.parse(l)}catch{continue}if(e.type==="queue-operation"&&e.operation==="enqueue"&&typeof e.content==="string"&&!e.content.startsWith("<")&&!e.content.startsWith("["))console.log(e.timestamp,JSON.stringify(e.content))}' <transcript>`,
where `<transcript>` is that night's session transcript file, printed six
lines on 2026-09-27 at 05:17. Its timestamps are UTC; the times
below are those timestamps plus three hours, local time. The seat's
questions that two of the words answer are quoted from the seat's assistant
messages in the same transcript, each at the time named beside it. A quoted
block holds whole sentences of the seat's message; a sentence left out is
marked [...] in the translation.

One journal marker carries another time than the typing: the entry "OPERATOR
WORD 2026-09-27 03:5x" holds the word of (c), typed at 04:01. The entry
"OPERATOR QUESTION 2026-09-27 03:5x" holds the question of (b) and quotes (a)
beside it.

### (a) The first question - 03:45

```text
Я так понимаю, мы продвинулись хорошо по фабрике за последние 24 часа, да?
```

"As I understand it, we made good progress on the factory over the last 24
hours, right?" A question, deciding nothing.

### (b) The second question - 03:51, journal entry "OPERATOR QUESTION 2026-09-27 03:5x"

```text
Мы можем запустить что-то выполняться и строиться из этого параллельно?
```

"Can we start something of this running and building in parallel?" A
question, deciding nothing. The seat answered it at 03:54 with a measurement
and one offer, whose operative sentences are:

```text
**Два блока одновременно — сейчас нет**, по двум причинам:
```

```text
Подготовить уже сейчас вопрос по M0-245, то есть по условию 2 — главному блокеру: варианты и мою рекомендацию.
```

```text
Запустить подготовку вопроса по M0-245? Я рекомендую — да.
```

"Two blocks at once - not now, for two reasons. [...] Prepare now the question
on M0-245, that is on condition 2, the main blocker: the options and my
recommendation. [...] Start preparing the question on M0-245? I recommend yes."

### (c) The M0-245 question prepared - 04:01, journal entry "OPERATOR WORD 2026-09-27 03:5x"

```text
Да
```

"Yes."

### (d) The third question - 04:02

As typed, two lines, with the space before the comma kept:

```text
Я просто думаю , что мы можем сделать для ускорения готовности фабрики 
Мы уже долго ее пишем, да?
```

"I am just thinking what we can do to speed up the factory's readiness. We
have been writing it for a long time, right?" A question. The seat answered it
at 04:03 with three proposals and one question, whose operative sentences are:

```text
1. **Критический путь первым.** После M0-243 сразу взять M0-245 (условие 2 — единственная причина отказа в обоих последних вердиктах), затем серию тиков. Остальной debug-пакет (M0-138, M0-212, M0-244) и M0-185 — после.
```

```text
2. **Черта готовности.** Выше неё поднимать только находки, которые блокируют первое оплаченное слияние. Остальное копить ниже M5-03 и не останавливать ради него цепочку.
```

```text
3. **Конвейер вместо очереди.** Драфтер следующего блока уже работает параллельно. Можно ещё запускать следующий блок сразу после моего машинного перемера, а мой верификатор (~55 мин) пускать параллельно в отдельном worktree. Цикл сократится примерно с 3 часов до 1,5–2. Риск небольшой: находки после посадки и так уходят в строки.
```

```text
**Вопрос:** включаем быстрый режим — пункты 1 и 3 сейчас, а пункт 2 я оформлю следующим carrier-пакетом? Рекомендую **да**. Для пункта 1 ещё понадобится ваше решение по M0-245 — вопрос с рекомендацией как раз готовится.
```

"1. The critical path first. Right after M0-243 take M0-245 (condition 2, the
only reason for refusal in both latest verdicts), then a series of ticks. The
rest of the debug package (M0-138, M0-212, M0-244) and M0-185 after. [...]
2. The finish line. Above it raise only findings that block the first priced merge.
Accumulate the rest below M5-03 and do not stop the chain for it. 3. A pipeline
instead of a queue. The next block's drafter already works in parallel. The
next block can also be started right after my machine re-run, with my verifier
(~55 min) run in parallel in a separate worktree. The cycle will shrink from
about 3 hours to 1.5-2. The risk is small: findings after a landing go to rows
anyway. [...] Question: do we turn on the
fast mode - points 1 and 3 now, and point 2 I will write up as the next carrier
package? I recommend yes. Point 1 will also need your decision on M0-245 - the
question with a recommendation is being prepared."

The same message says of point 1 that the order it changes was set by the
operator's word of 2026-09-26, so changing it is his; that word is ADR 0032
section 0 (f).

### (e) The fast mode - 04:10, journal entry "OPERATOR WORD 2026-09-27 04:1x"

It answered the question of (d). Between the two, at 04:09, the seat relayed a
block's status and closed that message by asking again:

```text
Ваш ответ на мой прошлый вопрос про быстрый режим ещё жду. Напомню его суть: M0-245 сразу после этого блока плюс приёмка параллельно со стартом следующего блока. Я рекомендую «да».
```

"I am still waiting for your answer to my previous question about the fast
mode. To recall its gist: M0-245 right after this block, plus acceptance in
parallel with the start of the next block. I recommend yes."

```text
Да
```

"Yes."

### (f) The night protocol - 04:11, journal entry "OPERATOR WORD 2026-09-27 04:1x (night)"

```text
И включи «ночной протокол» 🤗
```

"And turn on the 'night protocol'."

## 1. The decisions

### (1) The fast mode: the critical path first

The word of (e) accepts point 1 of the question it answered. After M0-243,
M0-245 - condition 2, the one refusal of both gate verdicts `repo-truth`
reached on 2026-09-26 (ADR 0032 section 1 (2), where the verdicts are read) -
goes first, then a series of ticks; the other rows of the debug package,
M0-138, M0-212 and M0-244, and M0-185 come after. This changes the order the
word of ADR 0032 section 0 (f) set, which put the debug package first after the
series.

The word does not carry itself into the queue. M0-138, M0-212, M0-244 and
M0-245 share priority 97, and the picker orders a tie by id (ADR 0003's
lower-id tie-break), so M0-245 is the last of the four until a raise moves it.
That raise lands WITH the operator's answer on M0-245's question, which the
seat prepared under the word of (c) and puts to him in the morning; so THIS
PACKAGE MOVES NO PRIORITY, and until that raise the pick stands as the queue
gives it.

### (2) Pipelined acceptance

The word of (e) accepts point 3. The next block opens right after the seat's
machine re-run of a landing, while the seat's own verifier over that landing
runs in parallel in its own worktree. Findings after a landing become rows as
before, as the seat's point 3 said.

### (3) The finish line

The word of (e) accepts point 2, and its question gave it to the next carrier
package to write up, which is this one. A finding is raised above the roadmap
only if it blocks the first priced verified merge - the first of the ten
PRICED verified merges that step (1) of the programme ADR 0027 section 10
records asks for; any other finding is filed below M5-03.

### (4) The night protocol

The word of (f) turns on the night protocol for the night of 2026-09-26/27, in
the form of the earlier nights (the seat's journal archive, entries "OPERATOR
WORD 2026-09-19 22:0x" and "OPERATOR WORDS 2026-09-21 22:1x"): no questions to
the operator until morning; the chain runs serially by the pick; the day's ceiling of the
weekly cap holds.

## 2. What this ADR does NOT decide

- **M0-245's answer.** The options, the recommendation and the question are the
  seat's decision brief's, and the answer is the operator's; nothing here reads
  or anticipates it.
- **Any priority.** The raise of M0-245 lands with that answer (section 1 (1)).
- **Any tick.** The series after M0-245 is placed on the path by the word of (e) in the
  form of ADR 0031 section 1 (1); its size is the operator's word before the
  first tick. The words of this night gave no size, and both earlier series
  carried the operator's own count (ADR 0031 section 1 (1); ADR 0032 section 0
  (b)).
- **Worktree-per-block parallelism.** Not taken: one shared control checkout.
  The seat's measurement at 03:5x, quoted from its journal entry "OPERATOR
  QUESTION 2026-09-27 03:5x" and not re-run here, because M0-243 has since
  landed and the picker's input changed: "`queue --next` admits only 44 M0-24
  beside M0-243 - M0-138 / M0-212 / M0-244 / M0-185 refused resource_conflict
  (millwright:controller), M0-245 / M5-03 predicted_file_overlap
  (test/unit/**)".
- **The three prunable registrations in `repo-truth`.** Still the operator's
  hand, as ADR 0032 section 2 left them.

## 3. What is filed elsewhere

The rows this package raised are named in its commit messages and are not
listed here, for ADR 0020 section 3's reason: a decision document that carries
a backlog acquires two homes for every row in it.

## 4. Rework

Reworked 2026-09-27 on the seat's verifier: section 2 no longer makes the size
of the tick series the seat's to state - it is the operator's word - and
section 1 (3) no longer adds a rule the words did not give about rows filed
before it.
