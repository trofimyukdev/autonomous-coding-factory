# ADR 0032 - The operator's words on the second series, on the factory's leftovers, and on a debug mode in the factory itself

Date: 2026-09-26. Context: a carrier session (carrier #73) by foreman decision
under the standing delegation of 2026-08-25, not a block, and off the cadence
of one carrier per four blocks by the operator's word in section 0 (f). `main`
stood at `71618eb` when the package began - `git rev-parse HEAD origin/main | cut -c1-7 | paste -sd' '`
printed `71618eb 71618eb` on 2026-09-26 at 22:16 - and `git status --short | wc -l`
printed 2 the same minute, the two operator handoffs in a private archive
that is not published.
Nothing under `src/`, `test/`, `scripts/`, `.githooks/`, `factory/checks.yaml`,
`factory/millwright.toml`, `CLAUDE.md`, `PRINCIPLES.md`, `DESIGN.md` or
the private archive was touched by this package, and nothing was written in
`repo-truth`.

**This document records operator words and what they decide. It carries no
mechanism: each decision below has its home in a row or in the code that row
lands, and the rows this package minted or raised are named in its commit
messages.**

## 0. The operator's words, and the questions they answer

Quoted verbatim on ADR 0005's precedent, Russian as typed and with the typing
kept as it is, because they are the authority this document stands on. Every
word below was typed in the foreman's session and relayed operator -> that
session's transcript -> the seat's journal entry named beside it -> this
carrier. Each is copied from the transcript and not
from the journal: among the transcript's entries that carry a typed message,
its queued-prompt entries (`queue-operation`, `enqueue`) hold each one exactly
once with its own timestamp, and
`node -e 'const fs=require("fs");for(const l of fs.readFileSync(process.argv[1],"utf8").split("\n")){if(!l)continue;let e;try{e=JSON.parse(l)}catch{continue}if(e.type==="queue-operation"&&e.operation==="enqueue"&&typeof e.content==="string"&&!e.content.startsWith("<")&&!e.content.startsWith("["))console.log(e.timestamp,JSON.stringify(e.content))}' <transcript>`,
where `<transcript>` is that session's transcript file, printed seven lines on
2026-09-26 at 22:16. Its timestamps are UTC; the times
below are those timestamps plus three hours, local time.

Four journal markers carry another time than the typing: three because each
carries the time of the seat's question or answer the word responded to - the
entry "OPERATOR WORDS 2026-09-26 17:2x" holds the words of (b), typed at 18:33;
"OPERATOR WORD 2026-09-26 18:3x" holds the word of (c), typed at 19:47; and
"OPERATOR WORD 2026-09-26 19:5x" holds the word of (d), typed at 20:27 - and
"OPERATOR WORDS 2026-09-26 20:3x", which holds the two messages of (e), the
first of them typed at 20:29.

### (a) The question - 17:20, journal entry "OPERATOR QUESTION 2026-09-26 17:2x"

```text
Ещё раз объясни по полочкам разложи что от меня требуется
И потом вкратце статус разработки нашей фабрики
Какие приоритетные следующие шаги
```

"Once more, lay out point by point what is required of me. And then, briefly,
the state of our factory's development. What are the priority next steps."
A question, deciding nothing; the seat answered it with two steps - the models
packet for the second repository, then a series of ticks - and the next words
answer that answer.

### (b) The packet and the series - 18:33, journal entry "OPERATOR WORDS 2026-09-26 17:2x"

```text
1. применяй пакет сам
2. запускай серию из 5 тиков
```

"1. Apply the packet yourself. 2. Launch a series of 5 ticks."

### (c) The one stale run directory - 19:47, journal entry "OPERATOR WORD 2026-09-26 18:3x"

It answered the seat's one question: move the one stale run directory,
`factory/runs/RT-03-M5-03-20260922T142130Z`, out of `repo-truth` to an archive
outside the repository, record a baseline again, then run the series.

```text
Да
```

"Yes."

### (d) The superseded leftovers - 20:27, journal entry "OPERATOR WORD 2026-09-26 19:5x"

It answered the seat's next question: move the eight superseded run
directories and the three superseded integration workspaces out of
`repo-truth`, keep the live candidate's directory, `.homes` and the manifests,
and retry the baseline.

```text
Да
```

"Yes."

### (e) The debug mode - 20:29 and 20:30, journal entry "OPERATOR WORDS 2026-09-26 20:3x"

Typed during the series' first tick, unprompted. The first message is one line
in the transcript; the journal entry breaks it in two before "видно" ("visible"), and that
break is the journal's wrap, not the operator's.

```text
Здесь нужно подумать еще, может добавить какой-то debug режим? Чтобы не приходилось постоянно спрашивать одно и то же? Чтобы сразу было видно что внутри происходит?
```

"We need to think more here - maybe add some kind of debug mode? So that one
does not have to keep asking the same thing? So that what happens inside is
visible at once?"

```text
Я про добавить этот Режим в саму фабрику
```

"I mean adding this mode to the factory itself."

### (f) The priority - 20:33, journal entry "OPERATOR WORD 2026-09-26 20:3x"

It answered the seat's one question: does the debug-mode package go first
after the tick series, above M5-03?

```text
Да, ставь этот пакет первым после серии тиков
```

"Yes, put this package first after the series of ticks."

## 1. The decisions

### (1) The models packet, by the seat's hand

The word of (b)'s first line applied ADR 0031 section 1 (4)'s model choice to
`repo-truth` by the seat's hand rather than the operator's. It landed as that
repository's commit `d4731e7`: from its working directory
`git log -1 --format='%h %ad %s' --date=iso d4731e7` printed
`d4731e7 2026-09-26 18:35:09 +0300 chore: hard builder, adjudicator and scout on claude-opus-5-5`
on 2026-09-26 at 22:17, and it was pushed on the operator's word typed in the
acting seat's session. It is not an edit made to let a tick pass, for the
reason ADR 0031 section 1 (4) gives, which is pointed at here and not restated.

### (2) The second series of five, and what it measured

The word of (b)'s second line authorises five ticks on `repo-truth`. The
reading of a series - serial, each accepted by the seat before the next,
stopping earlier at the first infrastructure breaker or on the operator's
word, a sixth being a further word - is ADR 0031 section 1 (1)'s, pointed at.

The five ran as `M5-03-20260926T172852Z`, `...T173718Z`, `...T175025Z`,
`...T180205Z` and `...T181440Z`, and their results are facts of `repo-truth`'s
journal, which is their one home. Every figure below was re-run from
`repo-truth`'s working directory on 2026-09-26 at 22:17, with the run ids
abbreviated in the prose and written out in the commands:

- The verdicts:
  `grep '"type":"RUN_FINISHED"' factory/state/events.jsonl | grep -E 'M5-03-20260926T1(72852|73718|75025|80205|81440)Z' | grep -o '"verdict":"[a-z_]*","exit_code":[0-9][0-9]*' | sort | uniq -c`
  printed `1 "verdict":"dispatched","exit_code":0` and
  `4 "verdict":"dispatch_tempfail","exit_code":75`.
- Two gate verdicts were reached: the same run filter over
  `"type":"GATE_FAILED"` piped to `grep -c .` printed 2. In both, condition 6
  answered and passed for the first time -
  `sed -n '590p;747p' factory/state/events.jsonl | grep -o '"condition":"goal_evaluator","number":6,"status":"[a-z]*"'`
  printed two `"status":"pass"` lines - and in both, condition 2 was the one
  refusal: `sed -n '590p;747p' factory/state/events.jsonl | grep -o '"condition":"[a-z_]*","number":[0-9],"status":"[a-z]*"' | grep -v '"pass"'`
  printed `"condition":"reviewer_verdict_clean","number":2,"status":"error"`
  twice. No candidate has passed the gate in that repository:
  `grep -c '"type":"GATE_PASSED"' factory/state/events.jsonl` printed 0.
- The refusals the fence held, per run in the order above:
  `for r in 172852 173718 175025 180205 181440; do grep "\"run_id\":\"M5-03-20260926T${r}Z\"" factory/state/events.jsonl | grep -c '"type":"POLICY_REFUSED"'; done | paste -sd' '`
  printed `8 4 8 4 1`.
- The seats opened, by role and model:
  `grep '"type":"AGENT_STARTED"' factory/state/events.jsonl | grep -E 'M5-03-20260926T1(72852|73718|75025|80205|81440)Z' | grep -o '"role":"[a-z_]*"\|"model":"[a-z0-9.-]*"' | paste -d' ' - - | sort | uniq -c`
  printed builder on `claude-opus-5-5` 2, builder on `claude-sonnet-5` 1,
  goal_evaluator on `claude-haiku-4-5-20251001` 2, resumed_seat on
  `claude-sonnet-5` 2, reviewer on `claude-sonnet-5` 3 and scout on
  `claude-opus-5-5` 2. A `resumed_seat` row is "a row no worker is called on"
  (the docstring over `RESUMED_ROLE` in src/controller/deferred-seat.ts), so
  ten workers opened, not twelve.
- What they cost: the same run filter over `"type":"AGENT_FINISHED"` piped to
  `grep -o '"cost_usd":[0-9.]*' | cut -d: -f2 | awk '{s+=$1} END {printf "%.4f\n", s}'`
  printed 6.2997, in dollars as the CLI priced them. The same filter with
  `grep -v resumed_seat | grep -c '"cost_usd":null'` printed 1 - the third
  tick's reviewer, stopped by the working wall - so the priced sum is a floor
  on what the series spent, not its total.
- `repo-truth`'s heads were not moved by the series:
  `git rev-parse HEAD origin/main | cut -c1-7 | paste -sd' '` printed
  `d4731e7 d4731e7`.

The seat's journal summed the series up with a priced sum that differs in its
last digit from the command above; that figure is not carried. A further tick
is a further word, and the series' findings are rows.

### (3) The factory's leftovers, moved out of `repo-truth` by two words

The words of (c) and (d) sanctioned a named, reversible exception to the
boundary of ADR 0023 section 2: "a gap discovered between the contract and the
code is a FINDING and a spec, never a workaround in the second repository."
What makes it an exception to that boundary and not a workaround of the
contract is what was moved and what was not:

- The moved trees are the FACTORY's own run and integration workspaces, in a
  directory `repo-truth` ignores: from its working directory
  `git check-ignore -v factory/runs/RT-05-M5-03-20260926T181440Z` printed
  `.gitignore:4:factory/runs/` and the path on 2026-09-26 at 22:16.
- No tracked file and no commit moved: `repo-truth`'s HEAD is `d4731e7` before
  and after the moves (section 1 (1)), and `git status --short | wc -l`
  printed 0 there on 2026-09-26 at 22:17.
- The defect the moves worked around - a ladder that measures the consumer's
  working tree rather than the commit, and run trees nothing sweeps - is filed
  as rows.

What moved and where: `ls <control-root>/repo-truth/runs-archive/ | grep -c '^RT-'`
printed 9, and `ls <control-root>/repo-truth/runs-archive/integrations/ | grep -vc json`
printed 3, on 2026-09-26 at 22:17. What the moves left: the three integration
workspaces were linked worktrees, and from `repo-truth`'s working directory
`git worktree list | grep -c prunable` printed 3 the same minute. That is
stated as a fact; nothing in this package cleans it.

The exception covers exactly those trees on that day. The next move of a tree
out of `repo-truth` is a further word until the row that clears superseded
run trees lands.

### (4) The debug mode

The words of (e) are a mandate for rows in THIS repository, not a procedure
for the seat: the operator's second message says so ("в саму фабрику" - into
the factory itself).

THE SEAT'S READING OF "A MODE", [operator-confirmable]: nobody knows before a
run which run will need reading, so the evidence a later question needs is
kept BY DEFAULT; only the part that costs disk and changes the worker's
argument vector - the worker's session transcript - sits behind a switch, and
the switch is off by default. The reading names five parts: every ladder's
checks keep their output and the verdict names the file and the failing tests;
every seat keeps its raw CLI output; worker transcripts on a switch; one human
view of a run from the journal; and the ladder measures the commit it records in a
checkout of its own, never the consumer's working tree, with the factory
clearing its own superseded run workspaces out of that tree.

The word of (f) puts this package first after the series, and its rows above
M5-03, each with `outranks_roadmap` declared.

## 2. What this ADR does NOT decide

- **A sixth tick.** Section 1 (2) covers five.
- **Any further move in `repo-truth`, and the three prunable registrations.**
  A `git worktree prune` there is a write in the second repository and the
  operator's hand.
- **The transcript switch's default, and whether DESIGN.md section 7's worker
  argument vector gains a sentence for it.** The seat's reading in section 1
  (4) puts it off; the default and DESIGN's text are the operator's.
- **What condition 2 does with a dimension no stage can measure.** A row's
  question; the reading ADR 0029 section 1 (3) records - "the pointer is
  checked, what the entry means is not" - stands until the operator's word.
- **M5-03's landing and its reading of that row's acceptance on the tick.**
- **The budget exit's divergence from DESIGN.md section 7.** A finding, not an
  operator word; ADR 0033 records it.
- **The day's first word and the handover words.** They decide nothing this
  ADR records; they are the journal's entries "OPERATOR FIRST WORD 2026-09-26"
  and the entry of that day's handover between two foreman seats.

## 3. What is filed elsewhere

The rows this package minted or raised are named in its commit messages and are
not listed here, for ADR 0020 section 3's reason: a decision document that
carries a backlog acquires two homes for every row in it.

## 4. Rework

Reworked 2026-09-26 on the seat's verifier: section 0 now says which of the
transcript's entries hold each typed message once (the queued-prompt entries;
the same message also appears in other entry types).
