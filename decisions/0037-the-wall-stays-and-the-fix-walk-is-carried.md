# ADR 0037 - The operator keeps the tick's wall and takes B+: a fix cycle's walk can be carried to the next pass

Date: 2026-09-28. Context: a carrier session (carrier #79, package item K1) by
foreman decision under the standing delegation of 2026-08-25, taken by the
blocked-top-pick exception - the top pick, M5-03, cannot be built until a
consumer's journal holds a passed gate - not a block. `main` stood at `21eafd7` when the
item began - `git rev-parse HEAD origin/main | cut -c1-7 | paste -sd' '`
printed `21eafd7 21eafd7` on 2026-09-28 at 13:26 - and `git status --short | wc -l`
printed 2 the same minute, the two operator handoffs in a private archive
that is not published.
Nothing under `src/`, `test/`, `scripts/`, `.githooks/`, `.claude/`,
`factory/checks.yaml`, `factory/millwright.toml`, `CLAUDE.md`, `PRINCIPLES.md`,
`DESIGN.md` or the private archive was touched by this item, and nothing was
written in `repo-truth`.

This is a new record and not an amendment of ADR 0028: that record's word of
2026-09-19 is how the loop closes - the `INTEGRATING -> BUILDING` edge, and way
B, under which a seat after the builder is carried "When a pass cannot hold" it
(its section 1 (2)) - and its section 2 leaves the wall's
numbers, and whether the builder and the walk before stage 4 fit the wall they
leave, to M0-195. The word recorded here answers a later question, raised by
the fix cycles the wall stopped on 2026-09-28 in `repo-truth`'s journal: raise
the wall, or carry a fix cycle's walk the way ADR 0028 carries the seats. That
the carry of ADR 0028 leaves a fix cycle the pass opened out is not his word of
2026-09-19: it is the boundary the blocks of M0-185 (bea72a2, the carry
filter's `openedFix !== null`) and M0-225 (dc4b584, `wallStoppedFix` asked
before `deferSeat`) drew. An amendment would give ADR 0028 a second subject
and a second date.

**This document records an operator word and what it decides. It carries no
mechanism and moves no priority: the rows that carry the decision out are the
homes of their own content and are named in the commit messages.**

## 0. The operator's words, and the recommendation they answer

Quoted verbatim on ADR 0005's precedent, Russian as typed and with the typing
kept as it is. Two transcripts hold them, each of a foreman session. The
question and the seats' messages are in the earlier session's transcript,
`<transcript-1>`; the restatement and the word are in the next foreman
session's, `<transcript-2>`.
His typed lines are copied by the filter ADR 0032 section 0 gives (its
`node -e` line is quoted whole in ADR 0036 section 0), run over each
transcript on 2026-09-28 at 13:24: it printed three lines over `<transcript-1>`
(04:16:29Z, 04:16:59Z, 04:24:59Z) and one line over `<transcript-2>` (08:02:03Z).
The seats' messages are copied from their own assistant rows, one row by its
uuid, by this read-only printer:
`node -e 'const fs=require("fs");const [f,u]=process.argv.slice(1);for(const l of fs.readFileSync(f,"utf8").split("\n")){if(!l.includes(u))continue;let e;try{e=JSON.parse(l)}catch{continue}if(e.uuid!==u)continue;const c=e.message.content;console.log(e.type,e.timestamp);console.log(typeof c==="string"?c:c.filter(x=>x.type==="text").map(x=>x.text).join("\n"))}' <transcript> <uuid>`
Timestamps are UTC; the times below are those timestamps plus three hours,
local time. A quoted block holds whole sentences; what a message says
beyond them is not part of this record.

### (a) The question - 07:16:29, in the earlier foreman session

The filter's first line over `<transcript-1>`, as printed:

```text
2026-09-28T04:16:29.357Z "По поводу решения по стене тика\nЗапусти параллельно исследование, так как твоя рекомендация и рекомендация предыдущего формана не совпадают \nИ потом дай решающую рекомендацию с обоснованием"
```

"On the decision about the tick's wall: run a research in parallel, because
your recommendation and the previous foreman's do not agree, and then give a
decisive recommendation with its grounds." A question to the seat; it decides
nothing.

### (b) The label - the two researchers' picks, 07:37:50 and 07:44:19

The seat's row at 04:37:50.456Z (assistant), its
second sentence:

```text
Его выбор: **B+** (переносить проход проверок цикла исправлений в следующий тик) вместе с **F1** (глагол разблокировки для BLOCKED-строк); A — только если ты сам отменишь своё решение 2-B.
```

"His pick: B+ (carry the fix cycle's checking pass to the next tick) together
with F1 (an unblock verb for BLOCKED rows); A only if you yourself reverse your
decision 2-B." "His" is researcher D.

The seat's row at 04:44:19.755Z (assistant), its first
two sentences:

```text
Исследователь T вернулся. Его выбор тоже **B+**, делать после M0-253 и M0-254; дешёвые дополнения — не звать scout в проходе возобновления и кешировать стадию 5 по SHA.
```

"Researcher T is back. His pick is B+ too, to be built after M0-253 and M0-254;
cheap additions - no scout in a resume pass, and stage 5 cached per SHA."

### (c) The recommendation - 07:45:38, in the earlier foreman session

The seat's row at 04:45:38.528Z (assistant), the
seat's decisive recommendation. Its opening two sentences and its two change
bullets, whole:

```text
**Рекомендация: стену тика не поднимать.** Вместо этого нужны две доработки:
- **Перенос проверки после исправления в следующий тик.** Сейчас исправление (builder) и проверка результата должны уместиться в один тик. Их надо разнести: исправление в одном тике, проверка — в следующем, так же как уже переносится ревьюер.
- **Команда, которая возвращает заблокированную задачу в работу.**
```

"Recommendation: do not raise the tick's wall. Two changes are needed instead:
(1) the check after a fix is carried to the next tick - today the fix (the
builder) and the check of its result must fit one tick; they are to be split,
the fix in one tick and the check in the next, the way the reviewer is already
carried; (2) a command that returns a blocked task to work."

Its point 4, whole:

```text
4. **Твоего слова не нужно.** Это продолжение твоего же выбора «2 — B», распространённое на цикл исправлений.
```

"Your word is not needed. This continues your own choice '2 - B', extended to
the fix cycle."

Its price paragraph, whole:

```text
**Цена.** Задача, которой гейт один раз отказал, пройдёт за 4 тика вместо 2 (около 60 минут против 40). Если после M0-253 и M0-254 такие отказы окажутся частыми, вернусь с данными к надёжному подъёму стены. Только он увеличивает стену для круглосуточного режима.
```

"The price: a task the gate refused once needs 4 ticks instead of 2 (about 60
minutes against 40). If, after M0-253 and M0-254, such refusals prove frequent,
I will come back with data to the robust raise of the wall. Only that raises
the wall for round-the-clock running."

And its next-to-last paragraph, whole - the pair of sentences before the
closing line on the weekly usage:

```text
От тебя сейчас ничего не нужно, кроме `/login`. Если всё же хочешь поднять стену, нужно твоё явное слово: это отмена решения от 19 сентября, и тики станут 20-минутными.
```

"Nothing is needed from you now but `/login`. If you do want to raise the wall,
your explicit word is needed: it reverses the decision of 19 September, and the
ticks become 20-minute ones."

Its points 1 to 3 carry figures the research owns and are not quoted here:
they live in the two researchers' reports -
`<control-root>/briefs/research-wall-D-report.txt` and
`<research-t-scratch>/report.txt` - and in the seat's run journal
archive entry "THE WALL RESEARCH RESULTS + THE SEAT'S DECISIVE RECOMMENDATION".

### (d) The restatement shown in the session where he answered - 10:48:22

A row of `<transcript-2>` (assistant,
07:48:22.716Z), the next foreman seat's readiness report, 13.7 minutes before the word. Its
bullet on the wall, whole:

```text
- **Решение за тобой — стена тика:** рекомендация [предыдущего формана] остаётся в силе: стену не поднимать, строить B+ и команду разблокировки для BLOCKED-строк. Если не скажешь «поднимай стену», это уйдёт в следующий carrier.
```

"The decision is yours - the tick's wall: [the previous foreman's] recommendation stands: do
not raise the wall, build B+ and the unblock command for BLOCKED rows. Unless
you say 'raise the wall', it goes to the next carrier."

### (e) The word - 11:02:03, typed in the next foreman session

The filter's one line over `<transcript-2>`, as printed:

```text
2026-09-28T08:02:03.852Z "по поводу рекомендации стены тика - берём рекомендованные вариант B+\nОт меня что-то ещё нужно?"
```

The first sentence, "по поводу рекомендации стены тика - берём рекомендованные
вариант B+", is the word: "About the tick wall's recommendation - we take the
recommended option B+." The second, "От меня что-то ещё нужно?" ("Is anything
else needed from me?"), is a question to the seat and not part of this record.
The word's own user row carries
the same words at 08:02:03.937Z with `origin` {"kind":"human"} and
`entrypoint` cli: it was typed in that foreman session.

## 1. The decision

**THE WALL STAYS.** ADR 0028 section 1 (2) stands as written - "The wall's
default does not rise, and section 7 is not touched." Option A, a raise of the
wall's default, is not taken, in its robust form either (the recommendation's
20-minute ticks). `DESIGN.md` sections 7 and 12 are untouched.

**B+ IS BUILT.** A fix cycle's opening pass must hold its builder; its walk and
the seats after it can be carried to the next pass over the fix candidate, the
way ADR 0028 section 1 (2) carries the seats after a builder. That is the first
change bullet of (c) and the label of (b) and (d). WHEN the walk is carried is
reading 4 below. The row that carries it is named in this package's commit
messages and not here.

Four readings follow. Each is **THE SEAT'S**, and each is
**[operator-confirmable]**:

1. **"The recommended option" is the recommendation whole, so the unblock verb
   rides with B+.** The verb is the recommendation's second change (section
   0 (c)), and the restatement shown in his session before he answered
   names it beside B+ (section 0 (d)). Only a raise needed his word, because a
   raise reverses ADR 0028; the recommendation's point 4 says so of B+, and the
   verb changes no ratified text. That "only" is itself THE SEAT'S reading, the
   recommendation's point 4, and not his. Researcher D's options table had
   flagged B+ as a seat reading on M0-228's confirmed floor
   [operator-confirmable] - a flag the recommendation did not put to him, and
   reading 2 carries it.
2. **ADR 0029 section 1 (4)'s floor stands as what a fix cycle runs again.**
   That section confirmed M0-228's reading, which ADR 0029 section 0 (4)
   states as "a fresh builder and the walk that judges it". B+ does not change what a cycle runs again; it
   changes only the part of it that the pass which opens the cycle must hold.
3. **F2 and F3 are not attributed to his word.** Neither the recommendation's
   text (section 0 (c)) nor the restatement (section 0 (d)) names them; they were
   named 79 seconds before the recommendation, in the row of 04:44:19.755Z
   that section 0 (b) quotes, as researcher T's cheap additions - no scout on a resume pass, stage 5 cached per SHA.
   They change no ratified text, and they are filed by the seat's decision
   under the standing delegation.
4. **The carry is conditional.** A pass that can hold the fix walk runs it;
   only a fix walk that does not fit is carried to the next pass. This is read
   from the bullet's own "так же как уже переносится ревьюер" ("the way the
   reviewer is already carried") and from ADR 0028 section 1 (2), which carries
   a seat only "When a pass cannot hold" it. The bullet he took ("Их надо
   разнести: исправление в одном тике, проверка — в следующем" - "they are
   to be split: the fix in one tick, the check in the next") and the
   recommendation's price ("пройдёт за 4 тика вместо 2" - "needs 4 ticks
   instead of 2") read unconditionally, so he is asked about this reading when it is put to him.

**THE PRICE** is the recommendation's own, quoted in section 0 (c), and so is
its condition for bringing the robust raise back: that is a commitment the seat
made, not a revisit condition of his.

## 2. What this ADR does NOT decide

- **The wall's numbers.** They are M0-195's, as ADR 0028 section 2 leaves them.
- **Any priority.**
- **`DESIGN.md`**, which is untouched.
- **The rows' mechanisms.** The carry's record, its fallback for records
  written before it, and the verb's name and refusals are their rows' own.
- **Whether, and when, a BLOCKED row of `repo-truth` is released.** What a
  release of each of them meets is the unblock verb's row's datum, and a
  release is not a promise of a verdict.
- **The tick series**, which waits for his separate word.
- **The forms of F2 and F3.**

## 3. What is filed elsewhere

The rows this package minted or raised are named in its commit messages and
are not listed here, for ADR 0020 section 3's reason: a decision document that
carries a backlog acquires two homes for every row in it.
