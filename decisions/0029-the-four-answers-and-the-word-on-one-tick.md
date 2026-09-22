# ADR 0029 - The operator's four answers of 2026-09-21, and the word on one tick

Date: 2026-09-21. Context: a carrier session (carrier #67) by foreman decision
under the standing delegation of 2026-08-25, not a block. `main` stood at
`e10c627` when the package began - `git rev-parse HEAD origin/main | cut -c1-7 | paste -sd' '`
printed `e10c627 e10c627` on 2026-09-21 at 23:05 - and `git status --short | wc -l`
printed 2 the same minute, the two operator handoffs in a private archive
that is not published.
Nothing under `src/`, `test/`, `scripts/`, `.githooks/`, `factory/checks.yaml`,
`factory/millwright.toml`, `CLAUDE.md`, `PRINCIPLES.md` or `DESIGN.md` was
touched by this package.

**This document records operator words and what they decide. It carries no
mechanism: each decision below has its home in a row and in the code that row
landed, and the rows this package minted are named in its commit messages.**

## 0. The operator's words, and the questions they answer

On 2026-09-21 at about 22:15, typed in the foreman's session, and relayed
operator -> the foreman seat -> the seat's journal -> the next foreman seat ->
this carrier. The seat's journal
keeps the message on one line with ` / ` at each line break; it is set out
here one line per line. Quoted verbatim on ADR 0005's precedent, Russian as
typed, because it is the authority this document stands on:

```text
По поводу моих решений:
1. Оставить
2. Подтвердить
3. подтвердить оба.
4. Подтвердить
```

"About my decisions: 1. Keep. 2. Confirm. 3. Confirm both. 4. Confirm." The
numbers are the seat's own list, put on 2026-09-20 between about 19:50 and
20:06 and repeated in every wake report after it; each answer is to the
question as the seat put it, translated here:

**(1) The seat's push to `repo-truth`.** On 2026-09-20 at 14:00 the seat
cherry-picked the phase-1 shadow tick's candidate `8eaf2bb` onto that
repository's public `main` as `104943247b51`, with the trailer line removed
and the original kept as a bundle. It was put to the operator as: keep it -
and RT-01's bookkeeping is then owed - or undo it by the operator's own hand.

**(2) M0-213's reading of a policy violation.** The row left the reading to its
block, and the block decided that a refusal the fence HELD is not a violation;
only a refusal record the factory could not read is. `DESIGN.md` section 18
writes "zero policy violations" and defines neither word. The seat recommended:
confirm it for held refusals, AND have the next carrier mint a row, taken
before M5-04, that makes the clause see a breach the fence missed and stage 1
caught, with the human line for held refusals in `ladder status`.

**(3) M0-223's two decisions.** The row left both to its block: (a) where the
reviewer's scratch git repository comes from - the controller writes an empty
one into the seat's home, with no change to the fence; (b) what makes an entry
of `unverified_dimensions` leave condition 2's count - a declaration naming a
check the gate finds passed in another stage. The seat recommended: confirm
both, AND have the next carrier mint typed entries for that list, the two
missing cases of the declaration's pattern, and a row for the seats' shared
home.

**(4) M0-228's floor.** The block decided that the fix cycle's floor is the
work the cycle will run again - a fresh builder and the walk that judges it -
and not what the refused cycle consumed. The seat recommended: confirm, the
wall's numbers staying M0-195's.

The operator's four answers accept each recommendation as put - the precedent
is ADR 0028 section 0, "accept both recommendations as put" - so the rows each
recommendation named are minted by this package, and the readings themselves
are recorded here.

A third message in the same exchange, verbatim:

```text
Дальше ночной протокол, что думаешь делать?
```

"Then the night protocol - what do you plan to do?" It is an instruction to
the seat about how it runs the night and a question about its plan, and it
decides nothing in this repository; it is quoted because it came in the same
exchange, as ADR 0028 section 0 quotes its own second sentence.

## 1. The decision

### (1) The push stays

`104943247b51` stays on `repo-truth`'s public `main`, and RT-01's candidate
`8eaf2bb` is accepted in that form. ADR 0027 section 5 (2) put its acceptance
to the operator and section 7 listed it as not decided; this is the answer.

The bookkeeping the answer made owed was done on 2026-09-21 in `repo-truth`
and lives in that repository's journal, seq 228 to 238, which is its one home:
from `repo-truth`'s working directory, `sed -n '238p' factory/state/events.jsonl`
printed the `BLOCK_RECORDED` of `RT-01@a3af9b92b000` with
`"corroboration":"override"` on 2026-09-21. The landing was recorded through
the declared override because its subject, `feat: RT-01 commit-range ASCII and
identity hygiene check`, carries no ` - ` after the id and a hand cherry-pick
carries no trailer, so nothing on the consumer's side corroborates it.

### (2) A refusal the fence held is not a policy violation

M0-213's reading is confirmed. The sentence it reads is `DESIGN.md` section
18, verbatim: "shadow, build and verify with no merge, promoted on an agreed
number of tasks with zero policy violations". That section does not define
"policy violation"; the definition this repository uses from now on is the one
M0-213 landed in src/controller/ladder.ts, whose docstring and cases are its
home and are not restated here.

What the confirmation does NOT cover is the other half of the word: a breach
the fence missed and stage 1 caught is seen by no clause today. That half is a
row of this package, taken before M5-04 by an anti-criterion of M5-04's own.

### (3) Both of M0-223's decisions stand

The reviewer's scratch repository is written by the controller, and the fence
is unchanged for it. The ground is `DESIGN.md` section 8, stage 4: "read-only
*tools* (it walks the repo and runs read/test commands rather than reading a
bare diff)".

An entry of `unverified_dimensions` leaves condition 2's count only on the
declared form M0-223 landed in src/verify/gate.ts; the pointer is checked, what
the entry means is not. The ground is `DESIGN.md` section 9, condition 2: "The
verdict is schema-valid, `overall == pass`, every item verified." The form, its
pattern and its cases are M0-223's and the code's.

The recommendation's three rows are this package's: typed entries, the missing
cases, and the shared home. The shared home is a defect that predates M0-223;
the confirmation of decision (a) is not a statement that the home is sound.

### (4) The fix cycle's floor is the work the cycle runs again

M0-228's reading is confirmed. The sentence it stands on is `DESIGN.md`
section 9, verbatim: "A first failure buys one fix cycle (fresh builder plus
FailurePacket, same branch)." What the floor measures on each of the two roads,
and the record that carries the stage, are M0-228's and live in
src/controller/fix-cycle.ts and src/controller/schedule.ts.

## 1a. The second exchange of the same evening: one tick, by the seat's hand

At about 22:30 the same evening, in the same session and by the same relay, the
operator answered the seat's question about the next tick. Verbatim, Russian as
typed:

```text
2. По поводу «Ваш тик» - запусти уже его, как только уже все будет готово. Чем то помочь?
```

"2. About 'Your tick' - just start it, as soon as everything is ready. Can I
help with anything?" The quoted phrase inside the sentence is the operator
quoting back the heading of the seat's report.

It closes, for ONE tick, the question ADR 0027 section 10 and ADR 0028 section 2
left open, "When the next tick runs, or whose hand starts it": the seat's hand
starts it, when it is ready. It is bounded by ADR 0027 section 7 - "ONE tick,
not a campaign" - with the spend bounded by the ceiling the caller passes and by
the standing weekly pacing rule, neither of which this word enlarges. A second
tick is not covered by it.

The first launch on this word was refused closed at the baseline step and spent
nothing: from `repo-truth`'s working directory,
`sed -n '227p' factory/state/events.jsonl` printed `RUN_FINISHED` with
`"step":"baseline"`, `"verdict":"base_unmeasured"` and `"exit_code":75` on
2026-09-21, the last of that run's journal lines, seq 224 to 227. What has
happened to the tick since is live state and is not recorded here.

The first line of the same message ended in a conditional order about the
showcase refresh, «Если да, то делай .» ("If so, then do it."), which is an act
in another repository, was carried out the same evening, and is mentioned only
because it arrived in the same exchange.

## 2. What this ADR does NOT decide

- **The wall's numbers.** Both numbers of finding (9)'s relation are M0-195's;
  confirming M0-228's floor moves neither.
- **The mechanism of any row this package minted.** Each row names the shapes
  known on the day and prescribes none.
- **Whether RT-02's candidate `a20bdb49` is accepted.** No word touched it.
- **A second pass of the tick, or a campaign.** Section 1a covers one tick.
- **Which ten tasks step (1) of the operator's programme measures** (ADR 0027
  section 10). Unchanged.

## 3. What is filed elsewhere

The rows this package minted or raised are named in its commit messages and are
not listed here, for ADR 0020 section 3's reason: a decision document that
carries a backlog acquires two homes for every row in it.
