# ADR 0038 - The operator's word on an entry pointing at a stage not configured for the task: it leaves condition 2's count

Date: 2026-09-28. Context: a carrier session (carrier #80, package item K1) by
foreman decision under the standing delegation of 2026-08-25, taken by the
blocked-top-pick exception - the top pick, M5-03, cannot be built until a
consumer's journal holds a passed gate - not a block. `main` stood at `8e9dc80`
when the item was committed - `git rev-parse HEAD origin/main | cut -c1-7 | paste -sd' '`
printed `8e9dc80 8e9dc80` on 2026-09-29 at 00:54 - and `git status --short | wc -l`
printed 8 the same minute: this package's six files, uncommitted, and the
two operator handoffs in a private archive that is not published.
Nothing under `docs/decisions/` but this record's own file, and nothing under
`src/`, `test/`, `scripts/`, `.githooks/`, `.claude/`, `factory/checks.yaml`,
`factory/millwright.toml`, `CLAUDE.md`, `PRINCIPLES.md`, `DESIGN.md` or
the private archive, was touched by this item, and nothing was written in
`repo-truth`.

This is a new record and not an amendment of ADR 0035. That record holds the
word of 2026-09-28 00:34:29 - answer (2), TEMPORARY by his word - and records
answer (3) as not taken, twice: in its section 1 (1), in the sentence that
opens "Answer (3) is NOT taken:", and in its section 2, "- **Answer (3)**,
which he did not take." The word recorded here is a later word on the same
subject: it answers a later question, which the afternoon's gate verdicts
raised, and it takes that answer for one case. An amendment would give ADR
0035 a second word and a second date, and its own sentences would stop being
the record of what he said at 00:34. So this record names the sentence it
changes, and ADR 0035 is not edited.

**This document records an operator word and what it decides. It carries no
mechanism and moves no priority: the row that carries the decision out is the
home of its own content and is named in the commit message.**

## 0. The operator's words, and the question they answer

Quoted verbatim on ADR 0005's precedent, Russian as typed and with the typing
kept as it is. One transcript holds them all, the foreman session's:
`<transcript>`.
His typed lines are copied by the filter ADR 0032 section 0 gives (its
`node -e` line is quoted whole in ADR 0036 section 0), run over that
transcript on 2026-09-28 at 18:20: it printed five lines, at 08:02:03Z,
12:21:04Z, 12:44:17Z, 13:01:29Z and 14:38:30Z. The first three are not part
of this record: the first is ADR 0037's word, the second a question about what
is needed from him, the third the word for the afternoon's tick series. The
seat's messages are copied from their own assistant rows, one row by its uuid,
by the read-only printer ADR 0037 section 0 quotes whole. Every quoted line
of a seat's row below was found in the transcript by
`grep -c -F '<the line>' <transcript>`, which printed at least 1 for each on
2026-09-28 at 18:20. The two lines of the filter's output are not in the
transcript as printed - it holds them JSON-escaped, so
`grep -c -F '2026-09-28T14:38:30.051Z "Да"' <transcript>` prints 0 - and were
checked as the filter's own output, and by their words in their user rows:
the row printer prints each user row named below with the same words. Timestamps are UTC;
the times below are those timestamps plus three hours, local time.
A quoted block holds whole sentences; what a message says beyond them is not
part of this record.

### (a) The context - 16:01:29 and 16:02:34

The filter's fourth line, as printed:

```text
2026-09-28T13:01:29.748Z "Слушай, все вот эти дики которые проваливаются, из-за чего проваливаются, из-за того что большая слишком задачи? Или действительно проблемы в нашей системе?"
```

"Listen, all these ticks that fail - why do they fail: because the tasks are
too big? Or are there really problems in our system?" («дики» is his typing
of «тики», ticks.) A question; it decides nothing. Its own user row carries it
at 13:01:29.835Z.

The seat's answer, its row at 13:02:34.852Z (assistant), its opening
sentence:

```text
Не из-за размера задач, дело в нашей системе.
```

"Not because of the tasks' size; the matter is in our system." The rest of
that row carries counts that `repo-truth`'s journal owns and is not quoted.

### (b) The question - 16:19:28

The seat's row at 13:19:28.023Z (assistant), the
seat's report on the afternoon's tick series. Its question line and its
three bullets under it, whole, and the first sentence of its closing line:

```text
**Вопрос: перестать считать в условии 2 запись о стадии, которая для задачи вообще не настроена?**
- **Рекомендую «да».** Это не пропущенная проверка, а отсутствующая. DESIGN требует считать провалом обязательную проверку, которую не удалось запустить, а ненастроенная стадия не обязательна.
- **Риск:** если задаче на самом деле нужен smoke-тест, гейт этого не заметит. Это лечится отдельно: настроить smoke там, где он нужен.
- **Почему спрашиваю тебя:** это меняет твоё решение от 28.09 (ADR 0035), тогда такой вариант ты не взял.
```

"Question: should condition 2 stop counting an entry about a stage that is
not configured for the task at all? - I recommend yes. It is not a skipped
check but an absent one. DESIGN requires a required check that could not be
run to be counted as a failure, and a stage that is not configured is not
required. - Risk: if a task really does need a smoke test, the gate will not
notice. That is treated separately: configure a smoke where one is needed.
- Why I am asking you: this changes your decision of 28.09 (ADR 0035); you
did not take this option then."

```text
Ответь здесь «да» или «нет».
```

"Answer here, yes or no."

The series report above the question and its point 2 carry counts the
journal owns; they are pointed at, not quoted: the seat's run journal archive
entry "TICK 3 OF THE AFTERNOON SERIES ACCEPTED + THE SERIES STOPPED AT THREE".

### (c) The word - 17:38:30, typed in the foreman's session

The filter's fifth line, as printed:

```text
2026-09-28T14:38:30.051Z "Да"
```

"Yes." The word's own user row carries
the same word at 14:38:30.114Z with `origin` {"kind":"human"},
`entrypoint` cli and `promptSource` queued: it was typed in the foreman's
session.

## 1. The decision

**AN ENTRY OF THE REVIEWER'S LIST ABOUT A STAGE THAT IS NOT CONFIGURED FOR
THE TASK AT ALL LEAVES CONDITION 2'S COUNT.** That is the question of (b) in
its own words and his "Да" of (c); what "an entry about a stage" is, is
reading 1.

The one stage that records itself as not configured today is stage 3,
runtime_smoke, with no smoke trigger configured: `runStage3`
(src/verify/stage3.ts) records it `unrun`, with no check, carrying
`NO_SMOKE_TRIGGER` - `if (trigger === undefined) return verdict("unrun", [],
NO_SMOKE_TRIGGER);`. `git grep -n -E 'verdict\("unrun"|unrun\(' 8e9dc80 --
src/verify/` names the other writers of an `unrun` stage: the one of
src/verify/run.ts, which records a stage an earlier stage's stop kept the walk
from reaching, and src/verify/strength.ts's `NO_PROBE_TRIGGER`, which reading
3 below keeps apart.

For that case, and only that one, the word reverses what ADR 0035 section 1
(1) records under answer (3):

```text
Answer (3) is NOT taken:
an entry pointing at a stage that did not run - stage 3 with no smoke trigger
configured - still counts.
```

The why-him bullet of (b) names that decision as the one the answer changes.
The question asked about this case alone, so the rest of ADR 0035's rule
stands as that record writes it: answer (2), TEMPORARY by his word.

**THE PRICE** is the recommendation's own risk, quoted in (b): a task that
does need a smoke goes unnoticed by the gate. Its remedy is the separate step
the risk names, configuring a smoke where one is needed, and that step is not
this record's.

That step does not exist today, and what follows from it is THE SEAT'S
reading, **[operator-confirmable]**: no consumer can configure a smoke. M0-127,
"Stage 3 knows how to smoke a candidate and no repository can tell it what to
start", is an open row that is not built, and the one production call of the
DAG, `runDag(request, { git: bound, review, run })` (src/controller/schedule.ts),
passes no `smoke`. So until M0-127 lands, the rule retires every pointer at
stage 3 on every consumer, and the remedy the question named is an unbuilt
row, not a configuration step. The question of (b) implied that the step
exists; it is quoted as it was put, and this sentence is the correction.

Three readings follow. Each is **THE SEAT'S**, and each is
**[operator-confirmable]**:

1. **"An entry about a stage" is an entry that DECLARES the stage in the form
   the gate reads, and "not configured" is the stage's own record.** ADR 0029
   section 1 (3) records his confirmed reading that "the pointer is checked,
   what the entry means is not"; the seat reads this word inside that one, so
   an entry leaves on its pointer, never on its own words. "Not configured" is
   the record `runStage3` writes when no trigger is configured for the task. A
   stage 3 recorded `unrun` because an earlier stage stopped the walk, and one
   recorded `error` - a trigger that threw, or one that measured nothing -
   still count: neither is that record, and ADR 0035 section 1 (1) reads
   `error` and `unrun` as not run to a result.
2. **The change rides with ADR 0035's TEMPORARY rule and goes back to him
   with it.** He did not mark this word temporary. The seat reads it as part
   of the rule it changes, so it is put back to him together with that rule,
   on the trigger ADR 0035 section 1 (1) records (itself the seat's reading
   there), with the entries this change retired in the data.
3. **The word is read for stage 3 alone.** Stage 5 recorded `unrun` carrying
   `NO_PROBE_TRIGGER` is not a stage not configured for the task: this
   factory always configures stage 5's probe ("Stage 5's probe, OPTIONAL and
   defaulted to the real one.", src/verify/run.ts), and what leaves it unrun
   is the candidate's diff. A pointer at it still counts.

## 2. What this ADR does NOT decide

- **`DESIGN.md`.** Section 9's two sentences stand: "All seven are required,
  and a required check that cannot be run is an infrastructure or gate
  failure - never a pass." and "The verdict is schema-valid, `overall ==
  pass`, every item verified." That the unconfigured stage is not "a required
  check that cannot be run" is THE SEAT'S reading, **[operator-confirmable]**,
  the recommendation's reason put in the code's terms. Section 8's table gives stage 3 a trigger, not a
  schedule - its cell reads "triggered when startup/routes/DI/schema/CLI/lifecycle
  are touched: start it, hit it, check it, stop it by PID" - and this factory
  takes the trigger as the consumer's input: src/verify/stage3.ts's header
  calls it a "property of the consumer's repository, not of the DAG". With
  none configured the stage records `unrun` and no check at all, so its record
  holds no required check that could not be run; that is the recommendation's
  own reason, «ненастроенная стадия не обязательна» ("a stage that is not
  configured is not required"). A configured smoke whose trigger throws or
  measures nothing records a required check `smoke` as `error`, and reading 1
  keeps a pointer at it counted. The reading has a limit, and it is the
  price's: section 8's cell is a content trigger, so a candidate that touches
  what the cell names - RT-07's change to a CLI is one - is exactly the task
  for which, with no trigger configured, the gate does not notice a missing
  smoke.
- **The smoke configuration of any consumer** - the separate step the risk
  names.
- **Any priority.**
- **The row's mechanism**: how the stage's record carries the fact, and how
  the evidence names the entries that left.
- **A smoke configured for a repository whose trigger does not fire for a
  task.** `runStage3` writes no such record today: with a trigger configured,
  the stage records the trigger's checks, or `error`.
- **The permanent rule, or what replaces the temporary one.** Both wait for
  his word when the rule is put back to him.
- **That condition 2, the gate or a tick passes after the row lands.**

## 3. What is filed elsewhere

The row this item minted is named in its commit message and is not listed
here, for ADR 0020 section 3's reason: a decision document that carries a
backlog acquires two homes for every row in it.
