# ADR 0031 - The operator's word on a series of five ticks, and the operator's words on the seats' models

Date: 2026-09-23. Context: a carrier session (carrier #72) by foreman decision
under the standing delegation of 2026-08-25, not a block. `main` stood at
`759a756` when the package began - `git rev-parse HEAD origin/main | cut -c1-7 | paste -sd' '`
printed `759a756 759a756` on 2026-09-23 at 11:40 - and `git status --short | wc -l`
printed 2 the same minute, the two operator handoffs in a private archive
that is not published.
Nothing under `src/`, `test/`, `scripts/`, `.githooks/`, `factory/checks.yaml`,
`factory/millwright.toml`, `factory/compat.json`, `CLAUDE.md`, `PRINCIPLES.md`,
`DESIGN.md` or the private archive was touched by this package, and nothing was
written in `repo-truth`.

**This document records operator words and what they decide. It carries no
mechanism: each decision below has its home in a row, in the code that row
lands, or in ADR 0005's table, and the rows this package minted or raised are
named in its commit messages.**

## 0. The operator's words, and the questions they answer

Quoted verbatim on ADR 0005's precedent, Russian as typed and with the typing
kept as it is, because they are the authority this document stands on. Each is
copied from the seat's journal entry named beside it; where that entry wraps a
line, the wrap is the journal's and is joined here by one space.

### (a) The series - 2026-09-22, journal entry "OPERATOR WORD 2026-09-22 16:40"

Typed in the foreman's session at 16:39-16:40, and relayed operator -> the
foreman seat, the session that carried the word out -> the seat's journal ->
this carrier. It answered the seat's two
standing items: the word on the retry tick, and the campaign of ticks.

```text
Разрешаю тебе запустить несколько тиков посмотрим что будет
```

"I permit you to launch several ticks; let us see what happens."

A second message followed at 16:4x in the same session:

```text
Поправь меня если я ошибаюсь, мы сейчас упёрлись в реальный прогон фабрики на реальном проекте? Если да то тогда давай запускай эти тики штук пять там например и потом остановимся подведём итоги
```

"Correct me if I am wrong: are we now up against a real run of the factory on
a real project? If so, launch these ticks, five or so, and then we stop and
take stock."

### (b) The seats - 2026-09-23, journal entry "OPERATOR WORDS 2026-09-23 08:2x"

Typed in the foreman's session between 08:2x and 08:3x, and relayed operator ->
the foreman seat -> the seat's journal -> this carrier. Two questions about the models came first, and
the seat answered each with a recommendation before the decision arrived:

```text
И, получается, что формана лучше запускать на опус 5.5? Или лучше все же чтобы он оставался на Fable?
```

"So it turns out the foreman is better started on Opus 5.5? Or is it better
after all that it stays on Fable?"

```text
Ну и тогда сами блочные и другие сессии которые он подымает тоже на 5.5?
```

"And then the block sessions and the other sessions it opens - also on 5.5?"

Then the decision, two lines:

```text
Да, переводим все на опус 5.5, может и Билдеры-субагенты?
Хочешь, сравни 5.5 с сонетом 5, вероятно что окажется что они сопоставимы по цене но 5.5 лучше в разы
```

"Yes, we move everything to Opus 5.5 - maybe the builder subagents too?" "If
you like, compare 5.5 with Sonnet 5; it will probably turn out that they are
comparable in price but 5.5 is several times better."

### (c) The factory's roles - 2026-09-23, journal entry "OPERATOR WORD 2026-09-23 09:0x"

Typed in the same foreman's session and relayed the same way. It answered the
operator's own question of 08:5x,

```text
Так, значит, и сонет мы меняем на опус 5.5?
```

("So, then, we replace Sonnet with Opus 5.5 too?"), to which the seat had
answered that Sonnet runs in two places - the hand-run blocks' builder
subagents, and the factory's own workers - and recommended keeping the
factory's `builder_default` and `reviewer` on Sonnet for now while its Opus 5
roles move. The operator's answer:

```text
Да, но не забудь решить что мы используем потом в основном билдере и ревьюере фабрики
```

"Yes, but do not forget to decide what we use later in the factory's main
builder and reviewer."

## 1. The decisions

### (1) A series of five ticks, by the seat's hand, and what it measured

The first word of (a) authorises SEVERAL ticks on `repo-truth`; the second
fixes the number at five and asks for a stop and a summing-up after them. The
seat's reading, stated back to the operator in the same minute and kept in the entry
named in (a): five ticks, serial, each accepted by the seat before the next,
stopping earlier at the first infrastructure breaker or on the operator's word; after the
fifth the seat stops and sums up; a sixth is a further word. Nothing else is
enlarged: the spend per tick stays the ceiling the caller passes, the standing
weekly pacing rule stands, and a passed gate would have parked at the merge
policy of rung 1. ADR 0027 section 7 and ADR 0030 section 1 (1) each covered
one tick; this word covers exactly five.

The five ran as `M5-03-20260922T135908Z`, `...T141215Z`, `...T142130Z`,
`...T143329Z` and `...T144616Z`, and their results are facts of
`repo-truth`'s journal, which is their one home. Every figure below was re-run
from `repo-truth`'s working directory on 2026-09-23 at 11:42, with the run ids
abbreviated in the prose above and written out in the commands:

- Each of the five ended in the same verdict:
  `grep '"type":"RUN_FINISHED"' factory/state/events.jsonl | grep -E 'M5-03-20260922T1(35908|41215|42130|43329|44616)Z' | grep -o '"verdict":"[a-z_]*","exit_code":[0-9][0-9]*' | sort | uniq -c`
  printed `5 "verdict":"dispatch_tempfail","exit_code":75`.
- One gate verdict was reached, at seq 392: the same run filter over
  `"type":"GATE_FAILED"` piped to `grep -c .` printed 1, and
  `sed -n '392p' factory/state/events.jsonl | grep -o '"condition":"[a-z_]*","number":[0-9],"status":"[a-z]*"'`
  printed `"status":"error"` for `reviewer_verdict_clean` (condition 2) and
  for `goal_evaluator` (condition 6), and `"status":"pass"` for the other five.
  No candidate has passed the gate in that repository:
  `grep -c '"type":"GATE_PASSED"' factory/state/events.jsonl` printed 0.
- The stage-5 figure of tick 2's candidate (cb342b067743, the one the gate
  verdict judged) is carried by seq 393, the `FIX_CYCLE_DEFERRED` event that
  follows the verdict:
  `sed -n '393p' factory/state/events.jsonl | grep -o '[0-9]* mutant(s) over [0-9]* file(s) in [0-9]*s: [0-9]* killed, [0-9]* survived'`
  printed `52 mutant(s) over 1 file(s) in 204s: 38 killed, 14 survived`.
  The series built a second candidate in tick 5, whose stage 5 also failed
  and whose event carries no mutant count.
- The refusals the fence held, per run in the order above:
  `for r in 135908 141215 142130 143329 144616; do grep "\"run_id\":\"M5-03-20260922T${r}Z\"" factory/state/events.jsonl | grep -c '"type":"POLICY_REFUSED"'; done | paste -sd' '`
  printed `23 1 9 6 13`.
- The seats opened:
  `grep '"type":"AGENT_STARTED"' factory/state/events.jsonl | grep -E 'M5-03-20260922T1(35908|41215|42130|43329|44616)Z' | grep -o '"role":"[a-z_]*"' | sort | uniq -c`
  printed builder 4, goal_evaluator 1, resumed_seat 1, reviewer 3, scout 1.
  The `resumed_seat` row is "a row no worker is called on" (the docstring over
  `RESUMED_ROLE` in src/controller/deferred-seat.ts), so NINE WORKERS opened:
  the same command with `grep -v resumed_seat | grep -c .` in place of the
  last three stages printed 9.
- What they cost: the same run filter over `"type":"AGENT_FINISHED"` piped to
  `grep -o '"cost_usd":[0-9.]*' | cut -d: -f2 | awk '{s+=$1} END {printf "%.4f\n", s}'`
  printed 3.5420, in dollars as the CLI priced them. The rows with no price:
  that filter with `grep -v resumed_seat | grep -c '"cost_usd":null'` printed
  4, and with `grep '"cost_usd":null' | grep -v resumed_seat | grep -o '"exit_class":"[a-z_]*"' | sort | uniq -c`
  printed `3 "exit_class":"infra_timeout"` and `1 "exit_class":"infra_stalled"` -
  every unpriced worker was stopped by the working wall or by the silence
  bound. So the priced sum is a floor on what the series spent, not its total.
- `repo-truth`'s heads were not moved by the series:
  `git rev-parse HEAD origin/main | cut -c1-7 | paste -sd' '` printed
  `1049432 1049432`.

The seat's journal summed the series up in figures of its own (entry "THE
TICK SERIES, TICK 5 ACCEPTED AND THE SERIES SUMMED UP"); THREE of them do not
survive the commands above and are not carried here. Its count of agents
opened, and of agents left unpriced, included the `resumed_seat` row, which is
no worker - the counts are nine and four as above. Its "45 of 45 measured"
for tick 2 matches no command: tick 2's candidate printed 52 mutants (above),
and the one run that counted 45 mutants, the morning tick on the earlier
candidate, measured two of them
(`grep -o '[0-9]* of 45 mutant(s) run' <control-root>/briefs/tick-20260922T033306Z-evidence.txt`
printed `2 of 45 mutant(s) run` on 2026-09-23). And its reading of seq 544 as a reply counted
against the breaker is not carried: that event is a `CIRCUIT_COUNTED` whose
counter reads zero after a pass that ended `reply` -
`sed -n '544p' factory/state/events.jsonl | grep -o '"type":"[A-Z_]*"\|"consecutive":[0-9]*' | paste -sd' '`
printed `"type":"CIRCUIT_COUNTED" "consecutive":0`, and the same command over
line 487, tick 4's timeout and the breaker's previous event, printed
`"type":"CIRCUIT_COUNTED" "consecutive":1` - the reply reset the counter, and
the event's name spells a reset the way it spells an increment.

A further tick is a further word. The five ticks' findings are rows.

### (2) The seats on `claude-opus-5-5`

The decision of (b) moves the foreman seat, the block sessions and the carrier
sessions to `claude-opus-5-5`: the foreman at effort max, as before; block and
carrier sessions at effort high, the effort the seat's bench measured.
Adversarial verification is pinned to the same full id. The table that says
which model each seat runs on is ADR 0005's, and its amendment of this date
names the new rows; this ADR holds only the words.

### (3) Builder subagents stay on `claude-sonnet-5`

The operator's "может и Билдеры-субагенты?" ("maybe the builder subagents
too?") put the builder-subagent row as a question, and the "Хочешь, сравни"
("if you like, compare") sanctioned the comparison that answers it. The
decision is therefore the SEAT's, taken on its data on 2026-09-23 and recorded
in the journal entry "THE MODEL BENCH SUMMED UP"; the operator's word is its
mandate and not its content, and it stays [operator-confirmable].

The data enter by pointer and command only. `node report.mjs`, run on
2026-09-23 at 11:42 in `<bench-t6>` (task T6, the hard
builder task: twelve hidden acceptance cases plus eight single-rule variants
the model's own tests must catch, two replicates per model), printed a
primary score of 20 of 20 for each of the four runs - `claude-opus-5-5` high
r1 and r2, `claude-sonnet-5` high r1 and r2 - and a mean CLI price of $1.190
for `claude-opus-5-5` against $0.603 for `claude-sonnet-5`. On the code task
the two models are equal at the ceiling and Sonnet costs half. The operator's guess that
5.5 is "лучше в разы" (several times better) is NOT what these rows show: at
n = 2 both models reached the maximum on every run, so the bench cannot tell
them apart on quality at all, and a difference it cannot see is not a
multiple.

The lighter tasks T1 to T5 are one run per model (n = 1). `node report.mjs`,
run the same minute in `<bench-t1-t5>`, printed a CLI total of
$1.127 for `claude-opus-5-5` high against $1.112 for `claude-sonnet-5` high
over the five, which is the half of the operator's guess that holds - comparable price on
the light tasks. The journal's T1-T5 table is the seat's READING of those
runs, and three of its cells differ from the script's primary scores; it is
not quoted here, and a reader who wants it goes to "THE MODEL BENCH SUMMED UP".

### (4) The factory's own roles

The factory's `builder_hard`, `adjudicator` and `scout` move to
`claude-opus-5-5` in `repo-truth` by that repository's own `[models.*]`
tables and its `compat.json` `model_ids` - the operator's hand, through the
packet `<control-root>/briefs/packet-rt-models-2026-09-23.md`. Whether
the operator has applied it is live state and is not written here. `builder_default`
and `reviewer` stay on `claude-sonnet-5`.

That packet is the operator's MODEL CHOICE, resting on the words in section 0
(b) and (c), and it takes the form the M5 programme already sanctioned for a
model change in the consumer - ADR 0027 section 10's step (2), "then the same
ten tasks with the builder on Opus through `[models.*]` in the consumer's TOML,
with no code" - though it is not that step, which comes after the first ten
priced merges and moves the default builder. It is not an edit made to let a
tick pass; so neither M5-03's
anti-criterion "the second repository is edited to make the tick pass" nor
ADR 0023 section 2's "a gap discovered between the contract and the code is a
FINDING and a spec, never a workaround in the second repository" is read
against it.

What they run AFTER that is OPEN, and the operator's "не забудь" ("do not forget") is the reason it is
recorded as open rather than dropped: its next data point is ADR 0027 section
10's programme - the first ten priced verified merges on the default builder,
then the same ten tasks with the builder on Opus through the consumer's
`[models.*]`.

## 2. What this ADR does NOT decide

- **A sixth tick.** Section 1 (1) covers five.
- **The factory's main builder and reviewer after the ten merges.** Open, by
  the operator's own word; section 1 (4).
- **The goal evaluator's model.** No word touched it.
- **A Fable verifier for risky `src/` landings.** The seat recommended it for
  after the weekly reset; a recommendation is not a word.
- **Millwright's own shipped defaults.** Which model ids its configuration
  names and makes canonical is a row's subject, not this ADR's.
- **Anything the series' findings imply.** Those are rows.

## 3. What is filed elsewhere

The rows this package minted or raised are named in its commit messages and are
not listed here, for ADR 0020 section 3's reason: a decision document that
carries a backlog acquires two homes for every row in it.
