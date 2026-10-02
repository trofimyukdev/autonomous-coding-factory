# ADR 0035 - The operator's answer on M0-245, TEMPORARY by his word: a pointer to a stage that ran leaves condition 2's count

Date: 2026-09-28. Context: a carrier session (carrier #77) by foreman decision
under the standing delegation of 2026-08-25, not a block, and off the cadence
of one carrier per four blocks by the blocked-top-pick exception: the top pick,
M0-245, waited on the operator's answer to the question the seat put to him,
and the answer came. `main` stood at `5f7d41d` when the package began -
`git rev-parse HEAD origin/main | cut -c1-7 | paste -sd' '` printed
`5f7d41d 5f7d41d` on 2026-09-28 at 00:41 - and `git status --short | wc -l`
printed 2 the same minute, the two operator handoffs in a private archive
that is not published.
Nothing under `src/`, `test/`, `scripts/`, `.githooks/`, `.claude/`,
`factory/checks.yaml`, `factory/millwright.toml`, `CLAUDE.md`, `PRINCIPLES.md`,
`DESIGN.md` or the private archive was touched by this package, and nothing was
written in `repo-truth`.

This is a new record and not an amendment of ADR 0034: that record's section 2
says of this very answer "the answer is the operator's; nothing here reads or
anticipates it", and an amendment would make it read what it says it does not.

**This document records operator words and what they decide. It carries no
mechanism and moves no priority: the change his answer allows has its home in
M0-245, and the rows this package raised are named in its commit messages.**

## 0. The operator's words, and the question they answer

Quoted verbatim on ADR 0005's precedent, Russian as typed and with the typing
kept as it is. Every word below was typed in the foreman's session and
relayed operator -> that session's transcript -> this carrier. Each is copied from the transcript and not from the seat's
journal, by the filter ADR 0032 section 0 gives, run over that transcript:
`node -e 'const fs=require("fs");for(const l of fs.readFileSync(process.argv[1],"utf8").split("\n")){if(!l)continue;let e;try{e=JSON.parse(l)}catch{continue}if(e.type==="queue-operation"&&e.operation==="enqueue"&&typeof e.content==="string"&&!e.content.startsWith("<")&&!e.content.startsWith("["))console.log(e.timestamp,JSON.stringify(e.content))}' <transcript>`,
where `<transcript>` is that session's transcript file, printed three lines on 2026-09-28 at 00:41:42. Its timestamps are UTC; the
times below are those timestamps plus three hours, local time, to
the second. The first of the three lines asks about the day, not about
M0-245, and is not part of this record. The answer's own row in the transcript
is a user row of that transcript; the filter's
rows and the transcript's user rows carry the same words at the same second,
and differ only by tens of milliseconds, which is the row type and not a
different word. The seat's question is quoted from the seat's assistant
message in the same transcript, at the time named beside it. A quoted block
holds whole sentences of the seat's message; a sentence left out is marked
[...] in the translation.

### (a) The operator's question - 00:31:26

As typed, two lines, with the stray guillemet kept:

```text
То есть от меня нужно только решение по «M0-245 «?
Что это такое? О чем оно?
```

"So all that is needed from me is a decision on M0-245? What is it? What is it
about?" A question, deciding nothing; it is quoted as the context of the
answer.

### (b) The seat's question - 00:32:07

The seat answered at 00:32:07 with a message that opens «Почти. Срочно нужны
две вещи» ("Almost. Two things are needed urgently") and explains M0-245. The part that asks and recommends:

```text
**Вопрос к тебе.** Снимать ли со счёта ссылку на проверку, которая **отработала** (прошла или упала)? Результат стадии 5 тогда учитывается там, где ему место: как свидетельство для общего вердикта ревьюера. Ссылка на проверку, которая вообще **не запускалась** (стадия 3, smoke-тест, ни у одного потребителя не настроен), по-прежнему блокирует.
```

```text
**Моя рекомендация — «да»** (с одним уточнением: ссылка может называть и стадию, как ревьюер и пишет).
- Риск: выжившие мутанты, которых ревьюер счёл безвредными, перестанут останавливать гейт.
- Смягчает то, что repo-truth пока в теневом режиме: даже прошедший гейт там не ведёт к настоящему merge.
```

```text
**Почему спрашиваю тебя.** Нынешнее правило ты сам подтвердил 21 сентября, и оно записано в ADR 0029. Менять его без тебя кресло не вправе.
```

"Question for you. Should a pointer to a check that RAN (passed or failed)
leave the count? Stage 5's result is then weighed where it belongs: as
evidence for the reviewer's overall verdict. A pointer to a check that did not
RUN at all (stage 3, the smoke test, configured for no consumer) still blocks.
My recommendation is yes (with one refinement: the pointer may name the
stage as well, as the reviewer writes it). Risk: surviving mutants the
reviewer judged harmless will stop halting the gate. What softens it is that
repo-truth is still in shadow mode: even a passed gate there leads to no real
merge. [...] Why I am asking you. You confirmed the current rule yourself on
21 September, and it is recorded in ADR 0029. The seat has no right to change
it without you."

### (c) The answer - 00:34:29

```text
Да, но нужно пометить это как временное решение
```

"Yes, but it must be marked as a temporary decision."

## 1. The decision

### (1) Answer (2), with a stage-name pointer, and TEMPORARY by his word

The word of (c) accepts the recommendation of (b), refinement included, and
adds one thing of his own: the decision is TEMPORARY.

Of the answers M0-245's outcome names ("ANSWERS NAMED, NOT PRESCRIBED"), he
took answer (2): an entry that opens by pointing at another stage's work
leaves condition 2's count when what it points at RAN, whether it passed or
failed; the pointer may name that stage's own name as well as the name of one
of its checks, which is how the reviewer writes it. RAN is read as the two
results the question named, passed or failed («прошла или упала»): a stage or
check recorded `error` or `unrun` did not run to a result, and an entry
pointing at it still counts. That reading is the seat's: his word answered a
question that named those two results and no other.
Answer (3) is NOT taken:
an entry pointing at a stage that did not run - stage 3 with no smoke trigger
configured - still counts. Prose still counts, whatever it says.

Against the reading ADR 0029 confirmed - its section 0 put condition 2's rule
to him, in question (3), as "a declaration naming a check the gate finds
passed in another stage", and its section 1 (3) records the decision as "the
pointer is checked, what the entry means is not" - the answer changes what the pointed-at record must show: a
check or stage that RAN, not one that PASSED. The pointer is still checked
against the verify result the gate is answering about; an entry that names
nothing the stages carry retires nothing. Naming a stage rather than a check
is the refinement the recommendation he accepted spelled out.

**TEMPORARY is his word**, not the seat's reading, and this record marks the
rule so; M0-245 carries the mark into what it builds. His words
give no condition for revisiting it. What follows is THE SEAT'S READING,
**[operator-confirmable]**: the seat puts the rule back to him, with the data,
once ten gate verdicts - GATE_PASSED and GATE_FAILED together, in a
consumer's journal - have been recorded after M0-245's change lands, or sooner
on his word. The data is, for each of those verdicts, the entries the new rule
retired and the verdict itself, and which passed candidates carried surviving
mutants.

### (2) What the rule's owner builds

The change is M0-245's to build, inside that row's paths, and the row carries
it; this record states no code.

## 2. What this ADR does NOT decide

- **The permanent rule, or what replaces the temporary one.** Both wait for
  his word when the rule is put back to him.
- **That condition 2, the gate or a tick passes after the row lands.** M0-245's
  "WHAT THIS ROW DOES NOT PROMISE" makes the same reservation.
- **`DESIGN.md` section 9**, whose two sentences stand untouched: "All seven
  are required, and a required check that cannot be run is an infrastructure
  or gate failure - never a pass." and "The verdict is schema-valid,
  `overall == pass`, every item verified."
- **The declaration's form**, which is M0-234's.
- **Answer (3)**, which he did not take.
- **The `DESIGN.md` sentences the seat's bank carries about this condition.**
  They are findings, not his words, and a finding gets its own record, as
  ADR 0033 did.
- **Any priority.** ADR 0034 section 1 (1) expected M0-245's raise above a
  tie to land with this answer; the tie is gone, and the row says why its
  priority stands.

## 3. What is filed elsewhere

The rows this package raised are named in its commit messages and are not
listed here, for ADR 0020 section 3's reason: a decision document that carries
a backlog acquires two homes for every row in it.
