# ADR 0065 - The operator's word of 2026-11-01: rule (A), a configuration whose worst-case pass exceeds the tick cap is refused

Date: 2026-11-01. Context: a carrier session (carrier #125, package item
K1), by foreman decision under the standing delegation of 2026-08-25 -
not a block - to give a home to one word the operator typed in the
foreman seat's session on the morning of 2026-11-01, and to the question
it answers. The same commit mints the row that carries the word out,
M0-351, and raises M0-196 in place (the package's item K2, which is the
seat's and not this word's).

**This document records an operator word and what it decides. It carries
no mechanism and moves no priority. The row that carries the word out
points here (discipline 12).**

## 0. The word, and the question it answers

Quoted verbatim on ADR 0060's precedent, Russian as typed, each beside
its English translation. One transcript holds every row quoted here,
the session of the foreman seat then, `<transcript>` below. Each row
was printed by its uuid from the transcript, and each quoted
line equals a whole line of the row's text, character for character; line
numbers count the row's text lines from 1, blank lines included.
Timestamps are UTC; the time beside each is that timestamp plus two
hours, local time. The proposal below is the seat's, made in
its own row; only his row is his.

### The question - 2026-11-01 06:30:33

The seat put it in its assistant row at
2026-11-01T04:30:33.606Z
(06:30:33), its stop reason `end_turn`, a row of 20 lines. It is also the
last seat text before his word: between the two the transcript holds a `system` row,
session bookkeeping rows and the two `queue-operation` rows of his
message, and no other text. Its lines 14, 15 and 16:

```text
M0-192 оставила остаток. При штатных настройках проход с разведкой может потратить $12.80 при потолке $12, перерасход $0.80, его замерил тест. Строка M0-192 отдаёт выбор правила вам:
- **A.** Конфиг, в котором худший проход выше `max_usd_per_tick`, не принимается. Тогда штатный потолок нужно поднять хотя бы до $12.80 или снизить потолок жёсткой ступени.
- **B.** В `DESIGN.md` §11 появляется фраза, что потолок считается на одно место. Тогда эти $0.80 законны.
```

"M0-192 left a residue. At the shipped settings a pass with a scout can
spend $12.80 against a cap of $12, an overrun of $0.80, which a test
measured. The M0-192 row hands the choice of rule to you: - **A.** A
config in which the worst pass is above `max_usd_per_tick` is not
accepted. Then the shipped cap has to be raised to at least $12.80, or
the hard rung's ceiling lowered. - **B.** A sentence appears in
`DESIGN.md` section 11 saying the cap is counted per seat. Then those
$0.80 are legal."

Its line 18:

```text
Рекомендую **A**: потолок остаётся настоящим потолком, и при сомнении проверка запрещает, как все обязательные проверки фабрики. Дальше одна строка карьера и один блок.
```

"I recommend **A**: the cap stays a real cap, and in doubt the check
forbids, as all of the factory's required checks do. Then one carrier
row and one block."

### The word - 2026-11-01 06:32:35

His user row at
2026-11-01T04:32:35.500Z (06:32:35), `origin.kind` "human", typed in
the foreman seat's session, its one line whole:

```text
Да, А
```

"Yes, A."

## 1. What the word decides

Rule (A) of M0-192's paragraph "WHAT THIS ROW MAY DECIDE AND WHAT IT MAY
NOT" (factory/tasks/M0-192.yaml): a `millwright.toml` whose worst-case
pass exceeds `[budget] max_usd_per_tick` is refused when the
configuration is resolved. Rule (B), the DESIGN.md section 11 sentence
that would make the cap a per-seat cap, is not taken, and DESIGN.md is
not edited for this word. The question's own consequence is part of what
he answered: the shipped defaults cannot stay as they are, because at
them the worst-case pass is $12.80 against a cap of $12. The question
named two roads for that, the shipped cap raised to at least $12.80 or
the hard rung's ceiling lowered; which default moves is THE SEAT'S
reading of section 2 (b).

DESIGN.md section 11 already states the intent this rule serves - "hard
ceilings (`--max-budget-usd` per attempt plus tick budget reservation
before a worker starts, so parallel workers cannot jointly overrun the
till)" - and no sentence of DESIGN.md names a seat ceiling or the tick
cap's figure: `git grep -n -E 'max_usd|12\.80' c48a317 -- DESIGN.md`
printed nothing on 2026-11-01, and the broader
`git grep -n -E '\$ ?12\b|\b12 ?(USD|dollars)|per[- ]tick' c4e691e -- DESIGN.md`
printed one line, "one task per tick", which names no dollar figure.

## 2. THE SEAT'S readings beside the word **[operator-confirmable]**

Each reading below was proposed by the seat's kickoff to carrier #125 or
by that carrier, and none of them is in his word or in the question he
answered. Each is THE SEAT'S reading **[operator-confirmable]**; he may
replace any of them without reopening the word.

(a) WHAT "THE WORST-CASE PASS" MEANS. The worst set of seats ONE
dispatch opens before anything asks the room again: the largest, at the
configured `[models.*] max_usd` ceilings, of the sets the admission
prices at c48a317 (`firstSetOf`, src/controller/schedule.ts). A pass of
two dispatches is already asked for both sets at once by the admission
(M0-192 finding (10), landed at c48a317), so the rule is per dispatch.

(b) WHICH DEFAULT MOVES: `[models.scout] max_usd`, $3.00 -> $2.20. The
question named two roads, the tick cap raised to at least $12.80 or the
hard rung's ceiling lowered; this reading takes a third, the scout's
ceiling, which the seat's kickoff listed beside the other two. The
worst-case pass at the shipped tables becomes $2.20 + $8.00 + $1.50 +
$0.30 = $12.00, inside the cap of $12. Why the scout and not the other
two:
- The tick cap stays $12, so repo-truth's public sentence in its
  factory/millwright.toml - "max_usd_per_tick, keeps its default (12),
  which stays within it" - stays true; a raised default would make it
  stale, and that file is his hand.
- `builder_hard`'s $8 is stated as a figure by texts in four files
  (`git grep -l -E '\$8(\.00)?\b' c4e691e -- src scripts`), and three
  of them hold no scout figure - scripts/millwright-tick.sh's paragraph
  "The dollar default is a FLOOR as much as a ceiling", whose wrapper
  default `8.00` is derived from it, and comments in
  src/controller/reservations.ts, src/controller/schedule.ts and
  src/router/index.ts - and lowering it would make each of them stale;
  src/controller/schedule.ts states the scout's $3 as well, and M0-351
  restates its figures either way.
- The measured cost of each seat is far below either ceiling, and the
  scout's sample is the larger. Read on 2026-11-01 06:42 local time by
  `node <home>/costs2.js <repo>/factory/state/factory.db <repo-truth>/factory/state/factory.db`
  over each repository's `attempts` table, whose one query is
  `select role, model, effort, count(*) n, sum(cost_usd is not null) priced, round(avg(cost_usd),2) av, round(max(cost_usd),2) mx from attempts where role in ('builder','scout') group by role, model, effort`
  on each database opened read-only: in repo-truth, 18 scout
  attempts, all priced, the dearest $0.92 (one on claude-opus-5) and the
  other 17 on claude-opus-5-5 at most $0.41; 7 priced builder attempts on
  claude-opus-5-5, the id repo-truth's `[models.builder_hard]` names, at
  most $2.23. In millwright's own journal, 3 builder attempts, all on
  claude-sonnet-5, and no scout attempt. A scout ceiling of $2.20 stays
  more than twice the dearest scout ever measured here; the shipped
  scout id, claude-opus-5, was measured once, and the other 17 ran on
  repo-truth's override.

(c) WHAT THE RULE JUDGES, AND WHAT IT DOES NOT. It judges the resolved
configuration: `[budget] max_usd_per_tick` against the `[models.*]`
ceilings. It does not judge a tick's `--max-usd` flag, which lowers the
cap for one run, nor the day's remainder, which can make the room
smaller than the tick cap: both are run-time lowerings his word does not
name. So the residue's shape survives below either of them: at a room
smaller than the worst-case set, the first admitted dispatch still opens
its reviewer and its goal evaluator after the room was asked only for
its first seats. Whether a run-time cap below the worst-case set is
refused too is a question for him, not a reading. *[ANSWERED 2026-11-03
by carrier #130: his word of 2026-11-02T07:22:13.750Z (09:22:13 local
time), an
`attachment` row of type `queued_command` - typed while the seat's turn
ran - with `attachment.origin.kind` "human", in the foreman seat's session
of that morning, answers the seat's
question (p) with the Russian word for no, and adds that this is what
the seat recommends. The question, in the seat's row
at 2026-11-02T07:17:10.977Z, asked
whether a run is refused also when a cap lowered at run time - a flag
for one run, or the day's remainder - is smaller than the dearest pass,
and recommended no, because a set that does not fit the budget is not
taken anyway and a refusal by the day's remainder would stop
repo-truth's work after its first $3 of a $15 day. "The dearest pass"
is read here as this section's worst-case set - THE CARRIER'S reading
**[operator-confirmable]**. The seat's last text row before his word,
at 07:22:01.147Z, does not name
(p). So a run-time cap below the worst-case set is NOT refused: that is
his decision. The sentences above are kept verbatim as the record of
what was written.]*

(d) THE WRAPPER'S DOLLAR FLOOR RISES TO THE WORST-CASE SET. The
wrapper's default, `--max-usd 8.00` (scripts/millwright-tick.sh), is
such a room, and at it a scouted row never opens: since M0-192
(c48a317) its scout and `builder_hard` are asked of the room as one sum,
$11 at c48a317 and $10.20 at a scout of $2.20, so every firing refuses
it at that pair, while an escalated row opens `builder_hard` at $8 and
its reviewer and goal evaluator after it unasked. M0-351 raises the
default to 12.00, the shipped worst-case first set, so an unattended
firing at the shipped tables can open every row the rule admits, and its
room is below the worst-case set only where the day's remainder makes it
so ((c)); a firing's dollar ceiling then equals the
shipped tick cap, and a consumer whose cap is lower keeps its own,
because a flag above the configured ceiling is clamped (`Math.min` in
`tightenedCeiling`). The dollar ceiling of each unattended firing rises
from $8 to $12, which is why this is a reading for him to confirm and
not a fix. *[CONFIRMED 2026-11-03 by carrier #130: his user row at
2026-11-02T07:13:46.955Z
(09:13:46 local time), `origin.kind` "human", typed in the
foreman seat's session of that morning, answers the seat's question (o) with the Russian word for
yes. The question as the seat last put it before his word, in its row
at 2026-11-02T07:06:31.971Z, asked
to raise the ceiling of one unattended firing from $8 to $12 and
recommended yes, because without it M0-351 could not start; the seat's
last text row before his word, at
07:08:49.674Z, does not name (o). His yes spans that rise; the
reasoning of this paragraph - the room at $8, the clamp of a flag above
the configured cap - stays THE SEAT'S reading **[operator-confirmable]**.
The sentences above are kept verbatim as the record of what was
written.]*

## 3. The row that carries it

M0-351 (factory/tasks/M0-351.yaml) builds the refusal, moves the scout's
default, raises the wrapper's dollar floor by (d) and keeps every
configuration a test case writes resolving. It points here for the word
and restates none of it.
