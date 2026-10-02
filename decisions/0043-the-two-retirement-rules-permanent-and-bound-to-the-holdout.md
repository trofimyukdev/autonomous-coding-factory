# ADR 0043 - The operator's word of 2026-10-01 08:47:18: condition 2's two retirement rules permanent and bound to the holdout, the list's scope permanent, M0-277 next and M0-272 before rung 2

Date: 2026-10-01. Context: a carrier session (carrier #87, package item K1)
by foreman decision under the standing delegation of 2026-08-25, opened off
cadence by exception - not a block - to carry into its record the operator's
word that orders the next blocks. Merge blocks since carrier #86's last
commit:
`git log --oneline --first-parent 91813d7..origin/main | grep -c ' merge:'`
printed 2 on 2026-10-01 at 15:14. `main` stood at `0fce515 0fce515` when this
record was committed - `git rev-parse HEAD origin/main | cut -c1-7 | paste -sd' '`
printed `0fce515 0fce515` on 2026-10-01 at 15:14.
Nothing under `src/`, `test/`, `scripts/`, `.githooks/`, `.claude/`,
`factory/policy/`, `factory/checks.yaml`, `factory/millwright.toml`,
`CLAUDE.md`, `PRINCIPLES.md`, `DESIGN.md` or the private archive was touched by
this package, nothing under `docs/decisions/` but this record's own file, and
nothing was written in `repo-truth`; the package writes this record and
`factory/tasks/`.

This is a new record and not an amendment. ADR 0035, ADR 0036 and ADR 0038
each leave the permanent rule to his word when the rule is put back to him -
the bullets of ADR 0035's section 2 and of ADR 0038's section 2 that open
"The permanent rule, or what replaces the temporary one", and the bullet of
ADR 0036's section 2 that opens "The permanent rule for the list's scope" -
and this record adds that word. None of the three is edited.

**This document records an operator word and what it decides. It carries no
mechanism and moves no priority: the rows that carry anything out are the
homes of their own content and are named in the commit messages.**

## 0. The word, and the message it answers

Quoted verbatim on ADR 0005's precedent, Russian as typed. One transcript
holds them, the session of the foreman seat that heard the word (closed):
`<transcript>`. It was read only through the read-only tools named below, on 2026-10-01
between 14:31 and 14:33; it does not grow - `stat -c '%s %y'` printed
`4842158 2026-10-01 09:36:32.604310119 +0300` at 14:31.

The filter ADR 0032 section 0 gives (its `node -e` line is quoted whole in
ADR 0036 section 0) printed two lines over the transcript at 14:33:

```text
2026-10-01T05:02:54.605Z "Да"
2026-10-01T05:47:18.282Z "Да"
```

The two lines are the filter's own output and not lines of the transcript,
which holds the timestamp and the words in separate fields, so
`grep -c -F` prints 0 for each; the rows that carry each word are named
below. The second is the word recorded here. The first, at 08:02:54, is not part of
this record: it sanctioned the research the recommendation of (a) rests on -
a spend, done - as ADR 0042 section 0 leaves out «Да» ("Yes") at 13:27:18
and ADR 0041 section 0 «Да, делай» ("Yes, do it").

The tools, each read-only and each over one transcript. A window lister
prints the uuid, type, timestamp and first characters of each user or
assistant row in a time window that carries text (ADR 0040 section 0
describes it). The row printer ADR 0037 section 0 quotes whole prints one row
by its uuid. A user row's fields are printed by
`grep -F '"uuid":"<uuid>"' <transcript> | grep -o -E '"entrypoint":"[a-z]*"|"origin":\{[^}]*\}|"promptSource":"[a-z]*"'`,
and an attachment row's by
`grep -F '"uuid":"<uuid>"' <transcript> | grep -o -E '"type":"queued_command"|"source_uuid":"[0-9a-f-]*"|"origin":\{[^}]*\}|"humanTurn":[a-z]*|"entrypoint":"[a-z]*"'`.
Every quoted line below was found in the transcript by
`grep -c -F -e '<the line>' <transcript>`, which printed at least 1 for each
on 2026-10-01 at 14:33. Timestamps are UTC; the times below are those
timestamps plus three hours, local time. A quoted block holds whole
lines; what a message says beyond them is not part of this record.

### (a) The recommendation and the question - 08:34:32

The seat's row at 05:34:32.720Z (assistant), the seat's decisive
recommendation after two researchers. Its opening sentences, the one that
opens «Оба исследования готовы» ("Both studies are ready"), and its bullets
under «**Что нашли исследователи**» ("What the researchers found") carry
figures that `repo-truth`'s journal and the two researchers own; they are
pointed at and not quoted, as ADR 0041 section 0 (a) points at a report's
opening paragraph. The two reports are
`<control-root>/briefs/research-cond2-D-report.txt` and
`<control-root>/briefs/research-cond2-E-report.txt`. Its recommendation
block, whole, as the row printer prints it:

```text
**Моя рекомендация** — то, в чём сходятся оба:
1. **Правила ADR 0035 и 0038 сделать постоянными, но привязать к holdout.** Пункт снимается, только если holdout кандидата прогнался и прошёл. Это закрывает единственный наблюдавшийся путь ложного прохода. Программе это сейчас ничего не стоит: из оставшихся задач holdout нет только у RT-08.
2. **Рамки списка ревьюера (ADR 0036)** сделать постоянными как есть.
3. **M0-272** (holdout-правило на repo-truth) построить до перехода на ступень 2: там проход уже означает слияние.
4. **M0-277** (бриф ревьюера называет разрешённые git-команды) построить следующим. Твоего слова для этого не нужно, он бьёт по причине ложных отказов.
5. **O3 сейчас не брать.** Вернусь к нему с данными, если после M0-277 ложных отказов останется много.
```

"My recommendation - what both agree on: (1) Make the rules of ADR 0035 and
0038 permanent, but bind them to the holdout. An item is taken off only if
the candidate's holdout ran and passed. This closes the one observed road to
a false pass. It costs the programme nothing now: of the remaining tasks
only RT-08 has no holdout. (2) Make the scope of the reviewer's list (ADR
0036) permanent as it is. (3) Build M0-272 (the holdout rule on repo-truth)
before the move to rung 2: there a pass already means a merge. (4) Build
M0-277 (the reviewer's brief names the permitted git commands) next. Your
word is not needed for this; it strikes at the cause of the false refusals.
(5) Do not take O3 now. I will come back to it with data if many false
refusals remain after M0-277."

The sentence after the five items, whole:

```text
После твоего «да» следующий carrier запишет решение в ADR, заведёт строку на привязку к holdout и снимет пометки «временное».
```

"After your 'yes' the next carrier will record the decision in an ADR, file
a row for the binding to the holdout, and take off the 'temporary' marks."

The question line, whole:

```text
**Вопрос: делаю так?** Рекомендую: да.
```

"Question: do I do it this way? I recommend: yes." `grep -c -F` printed 3
for this line in the transcript: the seat's later messages quote it.

### (b) The window between the question and the word

The window lister over the transcript from 2026-10-01T05:34:32Z to
05:47:40Z printed two rows at 14:31: a user row at 05:45:18.365Z, a message
from another session carrying a block's report - not a human row - and an
assistant row at 05:45:43.568Z, the seat beginning that block's acceptance,
which asks nothing. Neither is a question; the question of (a) is the only one put
between the recommendation and the word.

### (c) His word - 08:47:18, typed while the seat's turn ran

His word has NO user row: it was typed while the seat's turn ran, and the
transcript holds it in three other rows, printed at 14:31 by a node print of
the rows other than user and assistant rows from 05:47:00Z to 05:47:40Z. A
`queue-operation` row with `"operation":"enqueue"`, timestamp
05:47:18.282Z, `"content":"Да"`; a `queue-operation` row with
`"operation":"remove"`, timestamp 05:47:34.315Z, `"content":"Да"`,
`"reason":"absorbed_mid_turn"` and
`"commandUuid":"<command>"`; and an `attachment` row, timestamp
05:47:18.282Z, whose attachment's `prompt` is:

```text
Да
```

"Yes." Its fields, as the attachment field grep above printed them at 14:31:
`"type":"queued_command"`,
`"source_uuid":"<command>"`,
`"origin":{"kind":"human"}`, `"humanTurn":true` and `"entrypoint":"cli"`.
Its `source_uuid` is the remove row's `commandUuid`.

A filter over user rows misses such a word, and a filter that matches the
substring "human" anywhere in a row prints messages from other sessions whose
bodies quote it: `grep -c human <transcript>` printed 32 over the transcript
at 14:31. The exact
filter, which reads `origin.kind` at a row's top or inside its attachment,
quoted whole:
`node -e 'const fs=require("fs");for(const l of fs.readFileSync(process.argv[1],"utf8").split("\n")){if(!l)continue;let e;try{e=JSON.parse(l)}catch{continue}const o=(e.origin&&e.origin.kind)||(e.attachment&&e.attachment.origin&&e.attachment.origin.kind);if(o==="human")console.log(e.uuid,e.type,e.timestamp,(e.attachment&&e.attachment.type)||"",JSON.stringify((e.attachment&&e.attachment.prompt)||(e.message&&typeof e.message.content==="string"?e.message.content:"")).slice(0,80))}' <transcript>`
printed two rows over the transcript at 14:31: the user row of the word of
08:02:54 left out above, and the attachment row of the word recorded here.

## 1. The decision

«Да» ("Yes") of (c), to the question of (a), takes the recommendation's five
items whole - THE SEAT'S reading, **[operator-confirmable]**, on the
precedent of ADR 0039's reading 1 and ADR 0042's reading 1, which read a «Да» to a
recommendation as taking it whole:

1. **ADR 0035'S AND ADR 0038'S RETIREMENTS ARE PERMANENT AND BOUND TO THE
   HOLDOUT.** An entry either rule would retire leaves condition 2's count
   only on a candidate whose holdout ran and passed. What "bound" means for
   the machine is reading 1, and how it is read is reading 2.
2. **ADR 0036'S SCOPE OF THE REVIEWER'S LIST IS PERMANENT AS IT STANDS.**
3. **M0-272 IS BUILT BEFORE RUNG 2.**
4. **M0-277 IS BUILT NEXT.** The item itself says no word is needed for it;
   his «Да» covers it all the same.
5. **O3 - COUNTING ONLY THE ENTRIES THAT POINT AT A STATED REQUIREMENT - IS
   NOT TAKEN NOW.** The seat comes back with data if condition 2's false
   refusals stay frequent after M0-277 (reading 6).

Seven readings follow. Each is **THE SEAT'S**, and each is
**[operator-confirmable]**:

1. **"Bound to the holdout" (item 1).** Condition 2 counts an entry either
   rule would retire on a candidate whose spec declares no holdout item, or
   whose declared holdout item did not run, or did not pass; on a candidate
   whose every declared holdout item ran and passed it retires the entry as
   the rule does today. The sentence «Пункт снимается, только если holdout
   кандидата прогнался и прошёл» ("An item is taken off only if the
   candidate's holdout ran and passed") is read inside its item, which names
   the rules of ADR 0035 and ADR 0038: an entry ADR 0029's confirmed rule
   retires - a declared check that PASSED - is not bound. The scope by
   consumer is EVERYWHERE - the foreman
   seat's choice at the package's open - and not only where a consumer's
   policy asks for a holdout. Its price: on a consumer whose specs declare no
   holdout item, condition 2 counts as ADR 0029's confirmed rule alone
   counts, and a refusal on condition 2's `error` alone takes the road it
   takes today - an infrastructure retry and a fresh build, the road M0-275
   landed for one whose only other non-pass is advisory.
2. **The binding reads the declared items and their answers, never condition
   1's status.** Condition 1 answers `pass` both for a declared holdout item
   that passed and for a spec that declares none, so its status cannot tell
   the two apart; the row that carries the binding names the code.
3. **"PERMANENT" answers the revisit** that ADR 0035 section 1 (1), ADR 0036
   section 1 and ADR 0038's reading 2 recorded as the seat's reading. The
   trigger's count that opened the revisit is the seat's and is pointed at:
   the seat's run journal, archive entry "OPERATOR WORD 2026-10-01 08:02:54 -
   THE CONDITION 2 REVISIT RESEARCH".
4. **"Built next" orders M0-277 and then M0-272 ahead of millwright's other
   rows** under ADR 0042 section 1's reading 1, which takes a millwright row
   when a tick exposes a gate defect. The priorities that carry the order
   are the rows' footers.
5. **"Before rung 2" (item 3) reaches `repo-truth` only through his hand.**
   M0-272's rule binds a consumer only once the consumer key it builds -
   its form is that row's, named and not prescribed in its paragraph that
   opens "THE ROAD" - is written into that consumer's factory/policy/, which
   on `repo-truth` is his hand. So item 3 asks the seat to bring him that
   key as a packet when M0-272 lands, before rung 2's question.
6. **O3's return "with data" (item 5) is the seat's undertaking, not a
   rule.**
7. **The sentence after the five items is the seat's undertaking, and its
   act on the «временное» ("temporary") marks is carried by a row.** A
   carrier writes no file under `src/`, so the TEMPORARY marks in the code
   are dropped by the row that carries item 1, in its own diff, by pointer to this record; the marks in rows are
   those rows' history.

## 2. What this ADR does NOT decide

- **Any priority or row.** Those are the rows' footers, each
  **[operator-confirmable]**.
- **`DESIGN.md`**, untouched. Section 9's two sentences stand: "All seven
  are required, and a required check that cannot be run is an infrastructure
  or gate failure - never a pass." and "The verdict is schema-valid,
  `overall == pass`, every item verified."
- **The binding's mechanism.** The row that carries item 1 is its home.
- **The TEMPORARY marks in the code.** Reading 7.
- **`repo-truth`'s policy key for M0-272.** His hand (reading 5).
- **Rung 2 and its timing.** His - ADR 0042 section 1 item 4.
- **O3**, and the count M0-234's requirement pointer would feed.
- **That any tick, task, condition or the gate passes after any row lands.**

## 3. What is filed elsewhere

The rows this package minted or raised are named in its commit messages and
are not listed here, for ADR 0020 section 3's reason: a decision document that
carries a backlog acquires two homes for every row in it.
