# ADR 0036 - The operator marks M0-253's scope of the reviewer's list TEMPORARY

Date: 2026-09-28. Context: a carrier session (carrier #78, package item K8) by
foreman decision under the standing delegation of 2026-08-25, not a block.
`main` stood at `8778865` when the item began -
`git rev-parse HEAD origin/main | cut -c1-7 | paste -sd' '` printed
`8778865 8778865` on 2026-09-28 at 07:27 - and `git status --short | wc -l`
printed 2 the same minute, the two operator handoffs in a private archive
that is not published.
Nothing under `src/`, `test/`, `scripts/`, `.githooks/`, `.claude/`,
`factory/checks.yaml`, `factory/millwright.toml`, `CLAUDE.md`, `PRINCIPLES.md`,
`DESIGN.md` or the private archive was touched by this item, and nothing was
written in `repo-truth`.

This is a new record and not an amendment of ADR 0035: that record's rule is
condition 2's count of a pointer at another stage, and its section 2 leaves
the rest of condition 2 undecided; the word recorded here is about a different
change, the scope of what the reviewer is asked to list, and an amendment
would give ADR 0035 a second subject.

**This document records an operator word and what it decides. It carries no
mechanism and moves no priority: the change his word marks has its home in
M0-253, and the row this item raised is named in its commit message.**

## 0. The operator's word, and the notice it answers

Quoted verbatim on ADR 0005's precedent, Russian as typed. The word was typed
in the foreman's session and relayed operator -> that session's transcript
-> this carrier. It is copied from the transcript by the filter ADR 0032
section 0 gives, run over that transcript:
`node -e 'const fs=require("fs");for(const l of fs.readFileSync(process.argv[1],"utf8").split("\n")){if(!l)continue;let e;try{e=JSON.parse(l)}catch{continue}if(e.type==="queue-operation"&&e.operation==="enqueue"&&typeof e.content==="string"&&!e.content.startsWith("<")&&!e.content.startsWith("["))console.log(e.timestamp,JSON.stringify(e.content))}' <transcript>`,
where `<transcript>` is that session's transcript file, printed four lines on 2026-09-28 at 07:27:11; the last of them is the answer.
Its timestamps are UTC; the times below are those timestamps plus three hours,
local time. The answer's own row in the transcript is a user row
that carries the same words
at 04:24:59.428Z; the filter's row carries them at 04:24:59.375Z. The seat's
notice is quoted from the seat's assistant message in the same transcript.
A quoted block holds
whole sentences of the seat's message; the rest of that message - the login,
the tick wall's research, the factory's state and four later questions - is
not part of this record.

### (a) The seat's notice - 07:20:07

The last paragraph of the seat's message, whole:

```text
**Одно уведомление без вопроса:** M0-253 сужает то, что ревьюер записывает как непроверенное, до требований спеки. Это моё решение. Если хочешь, как с ADR 0035, пометить его временным — скажи.
```

"One notice, not a question: M0-253 narrows what the reviewer records as
unverified to the spec's requirements. It is my decision. If you want, as with
ADR 0035, to mark it temporary - say so."

### (b) The answer - 07:24:59

The filter's line, as printed:

```text
2026-09-28T04:24:59.375Z "* Да, пометь его временным\n* но ночью тики уже запускались? Есть результат? Только коротко и по делу \n* жду всего остального и результатов исследования \n* основная метрика фабрики сдвинулась?"
```

The first bullet, "Да, пометь его временным", is the word: "Yes, mark it
temporary." The other three bullets are questions to the seat - whether the
night's ticks ran, the research he is waiting for, whether the factory's main
metric moved - and they are not part of this record.

## 1. The decision

**M0-253's road one is TEMPORARY by his word.** Road one is the scope of the
reviewer's list of unverified dimensions: what an entry of
`unverified_dimensions` names is scoped to what the spec states - its
acceptance items, its not_done_if lines, its outcome - in both texts the
reviewer reads, the rule of `REVIEWER_RULES` and the schema's description of
the field. That is the narrowing the notice of (a) named, and "it" in his
answer is that decision.

**Road two is not marked.** M0-253's road two - a pointer written in the
brief's own head for a `focused:<n>` check resolving in the gate's pattern - is
a defect fix: the brief prints a line the gate cannot read. The notice did not
ask about it and his word does not reach it. That reading is THE SEAT'S, and it
is recorded as such.

**The revisit condition is not in his words.** What follows is THE SEAT'S
READING, **[operator-confirmable]**: the seat puts road one back to him
together with ADR 0035's temporary rule, on the same trigger - ten gate
verdicts, GATE_PASSED and GATE_FAILED together, recorded in a consumer's
journal after M0-253's change lands, or sooner on his word - with the data:
for each of those verdicts, the reviewer's list and which of its entries a
stated requirement of that verdict's spec asks for.

## 2. What this ADR does NOT decide

- **The permanent rule for the list's scope, or what replaces the temporary
  one.** Both wait for his word when the rule is put back to him.
- **ADR 0035's rule**, which stands as that record writes it; this record
  changes neither its rule nor its revisit reading.
- **`DESIGN.md`**, which is untouched; M0-253's outcome is where the row argues
  that no sentence of it changes.
- **The declaration's form**, which is M0-234's.
- **That condition 2, the gate or a tick passes after M0-253 lands.** M0-253's
  "WHAT THIS ROW DOES NOT PROMISE" makes the same reservation.
- **Any priority.**

## 3. What is filed elsewhere

The row this item raised is named in its commit message and is not listed
here, for ADR 0020 section 3's reason: a decision document that carries a
backlog acquires two homes for every row in it.
